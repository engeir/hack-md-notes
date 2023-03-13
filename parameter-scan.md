---
tags: Showcase, Papers
---

# Parameter Scan

[![hackmd-github-sync-badge](https://hackmd.io/j4L-EIhRQqGdl5KmiIZ-_w/badge)](https://hackmd.io/@engeir/SkEWr9Okh)
[![view-on-github](https://img.shields.io/badge/View%20on-GitHub-yellowgreen)](https://github.com/engeir/hack-md-notes/blob/main/parameter-scan.md)

## Introduction

### EGU abstract

> We investigate how the global mean temperature responds to single volcanic events of
> different magnitudes and to multiple events occurring close in time. We are using the
> Community Earth System Model version 2 (CESM2) to simulate the Earth system forced
> only with stratospheric aerosols from explosive volcanoes, with the rest of the
> climate system fixed at 1850 conditions. The model is run with a dynamical ocean
> component, and the Whole Atmosphere Community Climate Model version 6 (WACCM6)
> atmosphere component using middle atmosphere chemistry.
>
> Previous efforts of estimating a response function assume a linear relationship
> between the forcing and the deterministic temperature response to the
> forcing[^@rypdal2016b], defined as $T^{\mathrm{det}}(t)=\hat{L}[F(t)]$. Studies also
> show that the forcing is similar across forcing agents[^@richardson2019] (although
> this is not a settled debate[^@salvi2022]), in which case volcanoes could provide a
> valuable means of estimating global temperature response to radiative forcing due to
> their short-lived and large temperature responses.
>
> We present simulations of single volcano events with ejected sulphate aerosol loadings
> differing in orders of magnitude and simulations where two volcanic eruptions are
> close enough in time that the second eruption occurs as the temperature is still
> recovering from the first event.
>
> We show that the functional form of the temperature response is similar for volcanic
> events of different magnitudes and that non-linearities are not important as a second
> eruption occurs when the temperature is well below equilibrium in a perturbed state.
> The results further suggest the global mean temperature time series may be reduced to
> a simple superposition of individual pulses, and thus that it may be described by a
> convolution between a linear response function and some forcing, analogous to the
> model used by[^@rypdal2016b].

### Data

#### Own CESM2 simulations

We have simulated volcanic eruptions using the CESM2(WACCM6) climate model. This is run
with the component setting (compset) "BWma1850", which is a compset that runs the model
with external forcing cycling on 1850s conditions. Its atmospheric resolution is nominal
two degrees, with the "middle atmosphere" chemistry package.

Volcanoes are specified by giving an amount of injected SO~2~ for a given latitude and
longitude column and in given altitude levels. From there, the climate model spread the
SO~2~ and takes care of chemical reactions. Across the different CESM2 simulations, the
only difference in forcing is the amount of SO~2~ injected; latitude, longitude and
altitude are the same in all cases.

#### Other volcanic eruption data

<!-- FIXME: -->
**VolMIP 1 and 2** are from a simulation where the aerosol optical depth of the Tambora
1816 eruption was investigated, where the VolMIP1 AOD is from the EVA(eVolv2k) dataset
and VolMIP2 AOD is from the ICI reconstruction. The injection value is the default SO~2~
used in VolMIP simulations and the temperature response is from unknown.

**Obs. Pinatubo** is from observational data of the Mount Pinatubo eruption of 1991. The
temperature data is from the GISS paper of Hansen et al. (1999), the aerosol optical
depth is based on the reports of Sukhodolov (2018), and the injection data is from for
example Sukhodolov (2018) or Jones et al. (2005).

The **100 times Pinatubo** data is from Jones et al. (2005).

The **CESM1 LME** data is from a large project with Otto-Bliesner as the principal
investigator. The injected SO~2~ used is from the Gao et al. (2008) ice-core derived
estimates, and temperature records are the ensemble median over five simulation runs.

## Results

### CESM2 Simulations

Let us first have a look into how the three different forcing strengths alter the
temperature signal. That is if we normalize and do not care about the amplitude of the
signals, does the temperature show a similar shape across all three forcing strengths?

#### Individual without normalization

We may first have a look at what the ensemble median and the 5th to 95th percentiles
look like.

![Medium (smallest) forcing
strength](<https://raw.githubusercontent.com/engeir/hack-md-notes/4c76fa84d73699f3dd51cf9a8234d9142e54e9d1/assets/pic/volcano-ensemble-waveforms/medium-waveform.png>
"Medium (smallest) forcing strength" =32%x)
![Medium-plus (middle) forcing
strength](<https://raw.githubusercontent.com/engeir/hack-md-notes/4c76fa84d73699f3dd51cf9a8234d9142e54e9d1/assets/pic/volcano-ensemble-waveforms/medium-plus-waveform.png>
"Medium-plus (middle) forcing strength" =32%x)
![Strong (strongest) forcing
strength](<https://raw.githubusercontent.com/engeir/hack-md-notes/4c76fa84d73699f3dd51cf9a8234d9142e54e9d1/assets/pic/volcano-ensemble-waveforms/strong-waveform.png>
"Strong (strongest) forcing strength" =32%x)

<sup>**Figure:** Three simulations of a volcanic eruption of identical
location in space and time, but with three different magnitudes of injected SO~2~. All
magnitudes include four simulations, one in each season (Feb, May, Aug, Nov). Seasonal
variability is removed first in Fourier domain, then their median and the 5^th^ to
95^th^ percentiles are calculated</sup>

#### Comparing normalized time series

If we now normalize all the time series by dividing by the integral over the whole time
series, where we first shift all the time series so that the equilibrium temperature is
at zero, we get the plot shown below.

![Medium (blue and full), medium-plus (orange and dotted) and strong (green dashed)
overlaid. The black plots are the medians across the four participant ensemble, while
the coloured shading covers the 5th to the 95th
percentile](<https://raw.githubusercontent.com/engeir/hack-md-notes/91302ea7b928b6a0072972295f121a76536bef7a/assets/pic/volcano-ensemble-waveforms/compare-waveform-integrate.png>
"Medium (blue and full), medium-plus (orange and dotted) and strong (green dashed)
overlaid. The black plots are the medians across the four participant ensemble, while
the coloured shading covers the 5th to the 95th percentile" =49%x)
![Same as above, but scaled by the maximum
value](<https://raw.githubusercontent.com/engeir/hack-md-notes/91302ea7b928b6a0072972295f121a76536bef7a/assets/pic/volcano-ensemble-waveforms/compare-waveform-max.png>
"Same as above, but scaled by the maximum value" =49%x)

#### Smoothing

Let us first consider the raw reference temperature. The smoothing is done by removing
frequencies around $1$ in the Fourier domain.

Removing frequencies in the Fourier domain works quite well, but the sharp initial
response to the forcing is smoothed more than one would hope for.

#### Superposition

Finally, let us grab one of the single-event simulations and try to superpose a copy of
itself with an appropriate shift in time, to see how close we get to the double-event
simulation.

The two single-event time series are not long enough to cover to whole double-event time
series but do come close to replicating the double-event until the end of the first
shadowed region. After this, the tail of the first single-event time series is lost.

![Initial
smoothing](<https://raw.githubusercontent.com/engeir/hack-md-notes/1e3d1dca42484fc10c418dd1ede027301c9a532d/assets/pic/double-overlap/double-overlap-temp-smoothing-simple.png>
"Initial smoothing" =49%x)
![Superposition (blue) of two single events (black) on top of Fourier smoothed
temperature (red). Shading shows the length of the single event time series without
padding](<https://raw.githubusercontent.com/engeir/hack-md-notes/1e3d1dca42484fc10c418dd1ede027301c9a532d/assets/pic/double-overlap/double-overlap-superpose.png>
"Superposition (blue) of two single events (black) on top of Fourier smoothed
temperature (red). Shading shows the length of the single event time series without
padding" =49%x)

### Aggregated data

#### Different forcings compared to temperature

How do the different forcings relate to the temperature, and does any of them have a
linear relationship with temperature?

With this, we want to look at how close the different forcings come to forming a linear
relationship with the temperature signal.

Let us try to plot all non-zero values in the CESM LME forcing time series and the
corresponding temperature value at that element. There will be significant noise to
consider, especially for the smallest eruptions, and some eruptions that follow close
may get unrealistically large temperature values, but maybe numerous events will clear
things up. We may also use the deconvolution algorithm to get a response function
estimate that we subsequently use to estimate the temperature, thus reducing the noise.

We also add the CESM2 simulations and other simulation and observation data that we find
elsewhere to the mix.

![Injection versus
temperature](<https://raw.githubusercontent.com/engeir/hack-md-notes/b9109bd/assets/pic/hidden-linear-forcing/injection_vs_temperature.png>
"Injection versus temperature" =49%x)
![Injection versus temperature without
deconvolution](<https://raw.githubusercontent.com/engeir/hack-md-notes/b9109bd/assets/pic/hidden-linear-forcing/injection_vs_temperature_orig.png>
"Injection versus temperature without deconvolution" =49%x)

<sup>**Figure:** Temperature anomaly against injected SO~2~. The left plot show data
from CESM1 LME where the temperature values are from a re-created time series from
convolving with the forcing and an estimated response function. The right plot show the
raw temperature values at the given forcing position</sup>

![Injection versus aerosol optical
depth](<https://raw.githubusercontent.com/engeir/hack-md-notes/b9109bd/assets/pic/hidden-linear-forcing/injection_vs_aod.png>
"Injection versus aerosol optical depth" =49%x)
![Injection versus aerosol optical depth on log-log
axis](<https://raw.githubusercontent.com/engeir/hack-md-notes/97a5f57/assets/pic/hidden-linear-forcing/injection_vs_aod_loglog.png>
"Injection versus aerosol optical depth" =49%x)

<sup>**Figure:** Aerosol optical depth against injected SO~2~ on linear-linear axis
(left) and log-log axis (right)</sup>

![Aerosol optical depth versus
temperature](<https://raw.githubusercontent.com/engeir/hack-md-notes/97a5f57/assets/pic/hidden-linear-forcing/aod_vs_temperature.png>
"Aerosol optical depth versus temperature" =49%x)
![Aerosol optical depth versus temperature on semilog-x
axis](<https://raw.githubusercontent.com/engeir/hack-md-notes/b9109bd/assets/pic/hidden-linear-forcing/aod_vs_temperature_semilogx.png>
"Aerosol optical depth versus temperature" =49%x)

<sup>**Figure:** Temperature anomaly against aerosol optical depth at the same locations
as defined by the injected SO~2~ forcing time series</sup>

[^@rypdal2016b]:
    K. Rypdal and M. Rypdal, ‘Comment on “Scaling regimes and linear/nonlinear responses
    of last millennium climate to volcanic and solar forcing” by S. Lovejoy and C.
    Varotsos (2016)’, Earth System Dynamics, 2016, vol. 7, no. 3, pp. 597–609.
[^@richardson2019]:
    T. B. Richardson et al., ‘Efficacy of Climate Forcings in PDRMIP Models’, Journal of
    Geophysical Research: Atmospheres, 2019, vol. 124, no. 23, pp. 12824–12844.
[^@salvi2022]:
    P. Salvi, P. Ceppi, and J. M. Gregory, ‘Interpreting differences in radiative
    feedbacks from aerosols versus greenhouse gases’, Geophysical Research Letters,
    2022, vol. 49, no. 8, p. e2022GL097766.
