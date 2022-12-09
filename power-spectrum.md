---
tags: Showcase, Notes
geometry: margin=3cm,top=3cm
---

# Power Spectrum of Response Functions

> And the shape of the temperature decay!

[![hackmd-github-sync-badge](https://hackmd.io/j4L-EIhRQqGdl5KmiIZ-_w/badge)](https://hackmd.io/@engeir/SyMdeKsfi)
[![view-on-github](https://img.shields.io/badge/View%20on-GitHub-yellowgreen)](https://github.com/engeir/hack-md-notes/blob/main/power-spectrum.md)

## Temperature decay

We first do a quick comparison between the decaying phase of the temperature time
series, and a couple of analytical functions.

All fits are made with the [**lmfit**](https://lmfit.github.io/lmfit-py/) library.

As one can see, the single exponential does not do a good job, while the double
exponential and the power law both follow the decay of the original time series well.

The fitting parameters are four for the double exponential, and two for the power law.
One should note, however, that the time axis has also been adjusted to improve the fit
of the power law.

### Exponential(s)

In the plots below, we try both with one single exponential, and with two superposed
exponentials.

The single exponential was made using the following fitting parameters:

```toml
[[Model]]
    Model(exponential)
[[Fit Statistics]]
    # fitting method   = leastsq
    # function evals   = 32
    # data points      = 7200
    # variables        = 2
    chi-square         = 0.69728364
    reduced chi-square = 9.6872e-05
    Akaike info crit   = -66541.2750
    Bayesian info crit = -66527.5114
    R-squared          = 0.90800218
[[Variables]]
    amplitude:  0.25565769 +/- 0.00155324 (0.61%) (init = 0.1137494)
    decay:      4.77277534 +/- 0.02355057 (0.49%) (init = 8.94272)
[[Correlations]] (unreported correlations are < 0.100)
    C(amplitude, decay) = -0.915
```

The double exponential was made using the following fitting parameters:

```toml
[[Model]]
    (Model(exponential, prefix='exp1_') + Model(exponential, prefix='exp2_'))
[[Fit Statistics]]
    # fitting method   = leastsq
    # function evals   = 66
    # data points      = 7200
    # variables        = 4
    chi-square         = 0.12422683
    reduced chi-square = 1.7263e-05
    Akaike info crit   = -78957.8737
    Bayesian info crit = -78930.3463
    R-squared          = 0.98360983
[[Variables]]
    exp1_amplitude:  0.03284301 +/- 7.1478e-04 (2.18%) (init = 1)
    exp1_decay:      25.2601488 +/- 0.80882239 (3.20%) (init = 80)
    exp2_amplitude:  0.49291210 +/- 0.00397228 (0.81%) (init = 2)
    exp2_decay:      2.30849841 +/- 0.01661270 (0.72%) (init = 2)
[[Correlations]] (unreported correlations are < 0.100)
    C(exp1_amplitude, exp1_decay)     = -0.983
    C(exp2_amplitude, exp2_decay)     = -0.923
    C(exp1_amplitude, exp2_decay)     = -0.884
    C(exp1_decay, exp2_decay)         = 0.830
    C(exp1_amplitude, exp2_amplitude) = 0.661
    C(exp1_decay, exp2_amplitude)     = -0.598
```

### Power Law

The power law was made using the following fitting parameters:

```toml
[[Model]]
    Model(powerlaw)
[[Fit Statistics]]
    # fitting method   = leastsq
    # function evals   = 13
    # data points      = 7200
    # variables        = 2
    chi-square         = 0.17138784
    reduced chi-square = 2.3810e-05
    Akaike info crit   = -76644.7702
    Bayesian info crit = -76631.0065
    R-squared          = 0.97738753
[[Variables]]
    amplitude:  0.77438211 +/- 0.00346024 (0.45%) (init = 0.5914298)
    exponent:  -1.39394516 +/- 0.00268833 (0.19%) (init = -1.269584)
[[Correlations]] (unreported correlations are < 0.100)
    C(amplitude, exponent) = -0.964
```

![Log-log axis](./assets/pic/deconv-power-spectrum/loglog.png "Log-log axis")
![Logarithmic y-axis](./assets/pic/deconv-power-spectrum/semilogy.png "Logarithmic
y-axis")

## Power Spectrum of the Response function