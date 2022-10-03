---
tags: Showcase, Notes
geometry: margin=3cm,top=3cm
---

# How to trust deconvolution output

[![hackmd-github-sync-badge](https://hackmd.io/j4L-EIhRQqGdl5KmiIZ-_w/badge)](https://hackmd.io/@engeir/SJuISlKzs)
[![view-on-github](https://img.shields.io/badge/View%20on-GitHub-yellowgreen)](https://github.com/engeir/hack-md-notes/blob/main/do-we-trust-deconvolution.md)

We here want to have a look at how the deconvolution algorithm performes when met with
the data set CESM LME. We start by importing some libraries:

```python
"""Look at whether one can trust the result from deconvolving CESM LME data.

Roughly, 100 iterations take 16-17 seconds, 1000 take about 3 minutes.
"""

import matplotlib.pyplot as plt
import numpy as np
from fppanalysis import deconvolution_methods

import ensemble_run_analysis as era
```

Let us define one function to do deconvolution and one to create a simple plot of the
output:

```python
def _deconvolve(
    time_axis: np.ndarray,
    forcing: np.ndarray,
    temp: np.ndarray,
    iterations: int,
    guess: bool = True,
) -> tuple[np.ndarray, ...]:
    forcing = forcing if len(forcing) % 2 else forcing[:-1]
    temp = temp if len(temp) % 2 else temp[:-1]
    tau = np.arange(len(forcing)) - len(forcing) // 2
    the_time = np.arange(len(forcing))
    if time_axis is not None:
        sample_freq = time_axis[1] - time_axis[0]
        old_freq = tau[1] - tau[0]
        tau = tau * (sample_freq / old_freq)
        the_time = tau - tau[0] + time_axis[0]
    guess_shape = np.heaviside(tau, 1) if guess else None
    res, err = deconvolution_methods.RL_gauss_deconvolve(
        temp, forcing, iterations, initial_guess=guess_shape
    )
    return the_time, tau, forcing, temp, res, err


def _plot_all(t1, t2, f, t, r, e, save="") -> None:
    plt.subplots(2, 2)
    plt.subplot(2, 2, 1)
    plt.plot(t1, f)
    plt.subplot(2, 2, 2)
    plt.plot(t1, t)
    plt.subplot(2, 2, 3)
    plt.plot(t2, r)
    x0, y0, width, height = 0.5, 0.5, 0.4, 0.4
    ax1 = plt.gca().inset_axes([x0, y0, width, height])
    ax1.plot(t2, r)
    ax1.set_xlim([-10, 150])
    plt.subplot(2, 2, 4)
    plt.semilogy(e)
    if save:
        plt.savefig(save, dpi=200)
    plt.close()
```

## First case

The first case will be convolution without doing anything. The code simply become:

```python
def _get_cesm_lme() -> tuple[np.ndarray, ...]:
    # Nothing is altered.
    ensembles = {1, 2, 3, 4}
    frc_l = era.pre_made.cesm_lme_vars("FSNTOA", ens_numbers=ensembles)
    sig_l = era.pre_made.cesm_lme_vars("TREFHT", ens_numbers=ensembles)
    time_axis, frc = era.manipulate.get_mean(frc_l)
    _, sig = era.manipulate.get_mean(sig_l)
    return time_axis, frc, sig


_plot_all(*_deconvolve(*_get_cesm_lme(), 100, False), save="d1-1.png")
_plot_all(*_deconvolve(*_get_cesm_lme(), 100, True), save="d1-2.png")
_plot_all(*_deconvolve(*_get_cesm_lme(), 1000, False), save="d1-3.png")
_plot_all(*_deconvolve(*_get_cesm_lme(), 1000, True), save="d1-4.png")
```

![d11](https://github.com/engeir/hack-md-notes/raw/main/assets/pic/do-we-trust-deconv/d1-1.png)
![d12](https://github.com/engeir/hack-md-notes/raw/main/assets/pic/do-we-trust-deconv/d1-2.png)
![d13](https://github.com/engeir/hack-md-notes/raw/main/assets/pic/do-we-trust-deconv/d1-3.png)
![d14](https://github.com/engeir/hack-md-notes/raw/main/assets/pic/do-we-trust-deconv/d1-4.png)

## Second case

Second, we only smooth via the Fourier domain:

```python
def _get_cesm_lme_fourier() -> tuple[np.ndarray, ...]:
    # Fourier smoothing is applied.
    ensembles = {1, 2, 3, 4}
    frc_l = era.pre_made.cesm_lme_vars("FSNTOA", ens_numbers=ensembles)
    sig_l = era.pre_made.cesm_lme_vars("TREFHT", ens_numbers=ensembles)
    frc_l = era.manipulate.remove_seasonality(frc_l, "fourier")
    sig_l = era.manipulate.remove_seasonality(sig_l, "fourier")
    time_axis, frc = era.manipulate.get_mean(frc_l)
    _, sig = era.manipulate.get_mean(sig_l)
    return time_axis, frc, sig


_plot_all(*_deconvolve(*_get_cesm_lme_fourier(), 100, False), save="d2-1.png")
_plot_all(*_deconvolve(*_get_cesm_lme_fourier(), 100, True), save="d2-2.png")
_plot_all(*_deconvolve(*_get_cesm_lme_fourier(), 1000, False), save="d2-3.png")
_plot_all(*_deconvolve(*_get_cesm_lme_fourier(), 1000, True), save="d2-4.png")
```

![d22](https://github.com/engeir/hack-md-notes/raw/main/assets/pic/do-we-trust-deconv/d2-1.png)
![d23](https://github.com/engeir/hack-md-notes/raw/main/assets/pic/do-we-trust-deconv/d2-2.png)
![d24](https://github.com/engeir/hack-md-notes/raw/main/assets/pic/do-we-trust-deconv/d2-3.png)
![d25](https://github.com/engeir/hack-md-notes/raw/main/assets/pic/do-we-trust-deconv/d2-4.png)

## Third case

Next, we smooth via Fourier domain and shift the arrays so both have zero mean and unit
standard deviation:

```python
def _get_cesm_lme_fourier_shift() -> tuple[np.ndarray, ...]:
    # Fourier smoothing is applied, zero mean and unit standard deviation
    ensembles = {1, 2, 3, 4}
    frc_l = era.pre_made.cesm_lme_vars("FSNTOA", ens_numbers=ensembles)
    sig_l = era.pre_made.cesm_lme_vars("TREFHT", ens_numbers=ensembles)
    frc_l = era.manipulate.remove_seasonality(frc_l, "fourier")
    sig_l = era.manipulate.remove_seasonality(sig_l, "fourier")
    time_axis, frc = era.manipulate.get_mean(frc_l)
    _, sig = era.manipulate.get_mean(sig_l)
    frc = (frc - frc.mean()) / frc.std()
    sig = (sig - sig.mean()) / sig.std()
    return time_axis, frc, sig


_plot_all(*_deconvolve(*_get_cesm_lme_fourier_shift(), 100, False), save="d3-1.png")
_plot_all(*_deconvolve(*_get_cesm_lme_fourier_shift(), 100, True), save="d3-2.png")
_plot_all(*_deconvolve(*_get_cesm_lme_fourier_shift(), 1000, False), save="d3-3.png")
_plot_all(*_deconvolve(*_get_cesm_lme_fourier_shift(), 1000, True), save="d3-4.png")
```

![d31](https://github.com/engeir/hack-md-notes/raw/main/assets/pic/do-we-trust-deconv/d3-1.png)
![d32](https://github.com/engeir/hack-md-notes/raw/main/assets/pic/do-we-trust-deconv/d3-2.png)
![d33](https://github.com/engeir/hack-md-notes/raw/main/assets/pic/do-we-trust-deconv/d3-3.png)
![d34](https://github.com/engeir/hack-md-notes/raw/main/assets/pic/do-we-trust-deconv/d3-4.png)

## Fourth case

Then, we do as above, but let the arrays be non-negative:

```python
def _get_cesm_lme_fourier_shift_positive() -> tuple[np.ndarray, ...]:
    # Fourier smoothing is applied, minimum value of zero and unit standard deviation
    ensembles = {1, 2, 3, 4}
    frc_l = era.pre_made.cesm_lme_vars("FSNTOA", ens_numbers=ensembles)
    sig_l = era.pre_made.cesm_lme_vars("TREFHT", ens_numbers=ensembles)
    frc_l = era.manipulate.remove_seasonality(frc_l, "fourier")
    sig_l = era.manipulate.remove_seasonality(sig_l, "fourier")
    time_axis, frc = era.manipulate.get_mean(frc_l)
    _, sig = era.manipulate.get_mean(sig_l)
    frc = (frc - frc.mean()) / frc.std()
    sig = (sig - sig.mean()) / sig.std()
    frc -= frc.min()
    sig -= sig.min()
    return time_axis, frc, sig


# fmt: off
_plot_all(*_deconvolve(*_get_cesm_lme_fourier_shift_positive(), 100, False), save="d4-1.png")
_plot_all(*_deconvolve(*_get_cesm_lme_fourier_shift_positive(), 100, True), save="d4-2.png")
_plot_all(*_deconvolve(*_get_cesm_lme_fourier_shift_positive(), 1000, False), save="d4-3.png")
_plot_all(*_deconvolve(*_get_cesm_lme_fourier_shift_positive(), 1000, True), save="d4-4.png")
```

![d41](https://github.com/engeir/hack-md-notes/raw/main/assets/pic/do-we-trust-deconv/d4-1.png)
![d42](https://github.com/engeir/hack-md-notes/raw/main/assets/pic/do-we-trust-deconv/d4-2.png)
![d43](https://github.com/engeir/hack-md-notes/raw/main/assets/pic/do-we-trust-deconv/d4-3.png)
![d44](https://github.com/engeir/hack-md-notes/raw/main/assets/pic/do-we-trust-deconv/d4-4.png)

## Fifth case

Finally, we again do as above, but flip the arrays up-side-down:

```python
def _get_cesm_lme_fourier_shift_positive_updown() -> tuple[np.ndarray, ...]:
    # Fourier smoothing is applied, minimum value of zero and unit standard deviation,
    # positive perturbations
    ensembles = {1, 2, 3, 4}
    frc_l = era.pre_made.cesm_lme_vars("FSNTOA", ens_numbers=ensembles)
    sig_l = era.pre_made.cesm_lme_vars("TREFHT", ens_numbers=ensembles)
    frc_l = era.manipulate.remove_seasonality(frc_l, "fourier")
    sig_l = era.manipulate.remove_seasonality(sig_l, "fourier")
    time_axis, frc = era.manipulate.get_mean(frc_l)
    _, sig = era.manipulate.get_mean(sig_l)
    frc = (frc - frc.mean()) / frc.std()
    sig = (sig - sig.mean()) / sig.std()
    frc *= -1
    sig *= -1
    frc -= frc.min()
    sig -= sig.min()
    return time_axis, frc, sig


_plot_all(*_deconvolve(*_get_cesm_lme_fourier_shift_positive_updown(), 100, False), save="d5-1.png")
_plot_all(*_deconvolve(*_get_cesm_lme_fourier_shift_positive_updown(), 100, True), save="d5-2.png")
_plot_all(*_deconvolve(*_get_cesm_lme_fourier_shift_positive_updown(), 1000, False), save="d5-3.png")
_plot_all(*_deconvolve(*_get_cesm_lme_fourier_shift_positive_updown(), 1000, True), save="d5-4.png")
```

![d51](https://github.com/engeir/hack-md-notes/raw/main/assets/pic/do-we-trust-deconv/d5-1.png)
![d52](https://github.com/engeir/hack-md-notes/raw/main/assets/pic/do-we-trust-deconv/d5-2.png)
![d53](https://github.com/engeir/hack-md-notes/raw/main/assets/pic/do-we-trust-deconv/d5-3.png)
![d54](https://github.com/engeir/hack-md-notes/raw/main/assets/pic/do-we-trust-deconv/d5-4.png)
