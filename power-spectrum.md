---
tags: Showcase, Notes
geometry: margin=3cm,top=3cm
---

# Power Spectrum of Response Functions

> And the shape of the temperature decay!

[![hackmd-github-sync-badge](https://hackmd.io/j4L-EIhRQqGdl5KmiIZ-_w/badge)](https://hackmd.io/@engeir/SyCB0N-_i)
[![view-on-github](https://img.shields.io/badge/View%20on-GitHub-yellowgreen)](https://github.com/engeir/hack-md-notes/blob/main/power-spectrum.md)

## Temperature decay

We first do a quick comparison between the decaying phase of the temperature time
series and a couple of analytical functions.

All fits are made with the [**lmfit**](https://lmfit.github.io/lmfit-py/) library.

As one can see, the single exponential does not do a good job, while the double
exponential and the power law both follow the decay of the original time series well.
From the statistics provided by **lmfit**, the double exponential fit comes out on top
concerning the `R-squared` value, with a value $0.006222$ higher than what the power law
fit obtained. The fitting parameters are four for the double exponential, and two for
the power law. One should note, however, that the time axis has also been adjusted to
improve the fit of the power law.

### Exponential(s)

In the plots below, we try both with one single exponential and with two superposed
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

![Log-log
axis](https://raw.githubusercontent.com/engeir/hack-md-notes/5c18d59d54162b51f663da287d065a095813e90f/assets/pic/deconv-power-spectrum/loglog.png
"Log-log axis")
![Logarithmic
y-axis](https://raw.githubusercontent.com/engeir/hack-md-notes/5c18d59d54162b51f663da287d065a095813e90f/assets/pic/deconv-power-spectrum/semilogy.png
"Logarithmic y-axis")

## Power Spectrum of the Response function

We first define how PSD is to be calculated. We do this with the Welch method from the
**scipy** library:

```python
def spectrum(signal) -> tuple[np.ndarray, np.ndarray]:
    """Calculate the one sided spectrum of the signal."""
    signal = (signal - signal.mean()) / signal.std()
    sample_frequency = 365
    frequency, power = ssi.welch(
        signal, sample_frequency, nperseg=2**13, return_onesided=False
    )
    frequency_plus = frequency[frequency > 0]
    power_plus = power[frequency > 0]
    return np.asarray(frequency_plus[1:]), np.asarray(power_plus[1:])
```

The power spectrum of the response function obtained from the CESM LME data set follows
a power law, which can be seen when plotted on the log-log axis. In this case, we see
the weakness of the [**lmfit**](https://lmfit.github.io/lmfit-py/) library (red line in
the plot below), since it does not properly consider data as being on a log-log scale.
That is, the absolute difference on a linear axis is used, which for the small values in
the tail makes for a bad fit when plotted on log-log.

Let us see if the [**powerlaw**](https://github.com/jeffalstott/powerlaw) library can
cook up something better. This is the yellow fit in the figure below, which does come
closer to the original power spectrum (blue). This library returns an exponent of
`1.824` (the library defines the power law as $p(x)\propto x^{-\alpha}$) while **lmfit**
returns an exponent of `-1.306`.

Also included is a double exponential fit, again using the **lmfit** library, which in
this case does not provide a good fit over the full frequency range.

**lmfit** output from power law fit of the power spectra of the response function.

```toml
[[Model]]
    Model(powerlaw)
[[Fit Statistics]]
    # fitting method   = leastsq
    # function evals   = 35
    # data points      = 896
    # variables        = 2
    chi-square         = 0.00280794
    reduced chi-square = 3.1409e-06
    Akaike info crit   = -11351.2270
    Bayesian info crit = -11341.6311
    R-squared          = 0.90466032
[[Variables]]
    amplitude:  0.00518431 +/- 1.9615e-04 (3.78%) (init = 0.001236972)
    exponent:  -1.30151327 +/- 0.01797807 (1.38%) (init = -2.078565)
[[Correlations]] (unreported correlations are < 0.100)
    C(amplitude, exponent) = 0.958
```

**powerlaw** output from power law fit of the power spectra of the response function,
where `sigma` is the standard deviation on the power `alpha`.

```toml
fit.power_law.alpha = 1.8239139860706672
fit.power_law.sigma = 0.5826287465799062
```

![Log-log
axis](https://raw.githubusercontent.com/engeir/hack-md-notes/50bb4f5fbdafa6ac5b37facd39610756a802eb85/assets/pic/deconv-power-spectrum/loglog-newest.png
"Log-log axis")

### All PSDs

![180-day running
mean](https://raw.githubusercontent.com/engeir/hack-md-notes/c205d5901f991cde5a0715d7560cb39ae2cd4aca/assets/pic/deconv-power-spectrum/loglog-all-newest.png
"180-day running mean")

![15-day running
mean](https://raw.githubusercontent.com/engeir/hack-md-notes/c205d5901f991cde5a0715d7560cb39ae2cd4aca/assets/pic/deconv-power-spectrum/loglog-all-new2.png
"15-day running mean")

![No running
mean](https://raw.githubusercontent.com/engeir/hack-md-notes/8627648fed0dcf3bd59e79d1aac84089fd800e66/assets/pic/deconv-power-spectrum/loglog-all-old-daily-3000it.png
"No running mean")

![No running
mean, log-lin scale](https://raw.githubusercontent.com/engeir/hack-md-notes/8b377384f3aab852ae3907358177afc57bdf20c8/assets/pic/deconv-power-spectrum/loglog-all-old-daily-3000it-log-lin.png
"No running mean, log-lin scale")

```toml
[[Model]]
    Model(powerlaw)
[[Fit Statistics]]
    # fitting method   = leastsq
    # function evals   = 13
    # data points      = 889
    # variables        = 2
    chi-square         = 5.5977e-20
    reduced chi-square = 6.3108e-23
    Akaike info crit   = -45441.1908
    Bayesian info crit = -45431.6106
    R-squared          = 1.00000000
[[Variables]]
    amplitude:  0.00109805 +/- 1.5096e-05 (1.37%) (init = 0.001195273)
    exponent:  -2.03713872 +/- 0.00465884 (0.23%) (init = -2.066896)
[[Correlations]] (unreported correlations are < 0.100)
    C(amplitude, exponent) = -0.970
#######################################################################
[[Model]]
    Model(powerlaw)
[[Fit Statistics]]
    # fitting method   = leastsq
    # function evals   = 22
    # data points      = 889
    # variables        = 2
    chi-square         = 3.0428e-19
    reduced chi-square = 3.4305e-22
    Akaike info crit   = -43936.0946
    Bayesian info crit = -43926.5144
    R-squared          = 1.00000000
[[Variables]]
    amplitude:  0.00847024 +/- 3.4066e-04 (4.02%) (init = 0.005694137)
    exponent:  -2.47469249 +/- 0.01655384 (0.67%) (init = -2.380111)
[[Correlations]] (unreported correlations are < 0.100)
    C(amplitude, exponent) = -0.917
#######################################################################
[[Model]]
    Model(powerlaw)
[[Fit Statistics]]
    # fitting method   = leastsq
    # function evals   = 26
    # data points      = 889
    # variables        = 2
    chi-square         = 2.1253e-17
    reduced chi-square = 2.3961e-20
    Akaike info crit   = -40161.1313
    Bayesian info crit = -40151.5511
    R-squared          = 1.00000000
[[Variables]]
    amplitude:  0.00544160 +/- 4.3852e-04 (8.06%) (init = 0.002388811)
    exponent:  -1.40405019 +/- 0.02461607 (1.75%) (init = -1.153645)
[[Correlations]] (unreported correlations are < 0.100)
    C(amplitude, exponent) = -0.991
```

![PSD and power estimate for a smaller range of frequencies of the above three response
functions](https://raw.githubusercontent.com/engeir/hack-md-notes/8627648fed0dcf3bd59e79d1aac84089fd800e66/assets/pic/deconv-power-spectrum/loglog-newest_new2_olddaily.png
"PSD and power estimate for a smaller range of frequencies of the above three response
functions")
