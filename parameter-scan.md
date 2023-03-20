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

**VolMIP 1 and 2** are from a simulation where the aerosol optical depth of the Tambora
1815 eruption was investigated, where the VolMIP1 AOD is from the EVA(eVolv2k) dataset
and VolMIP2 AOD is from the ICI reconstruction (figure 5 in Toohey and Sigl,
2017)[^@toohey2017]. The injection value is the default SO~2~ used in VolMIP
simulations[^volmip-volc-long-eq] and the temperature response is from inspecting one of
the contributions to the **volc-long-eq** experiment[^volmip-volc-long-eq-realisation],
which used the MPI-ESM1.2-LR climate model.

**Obs. Pinatubo** is from observational data of the Mount Pinatubo eruption of 1991. The
temperature data is from the GISS paper of Hansen et al. (1999)[^@hansen1999], the
aerosol optical depth is based on the reports of Sukhodolov (2018)[^@sukhodolov2018],
and the injection data is from Guo et al. (2004)[^@guo2004].

The **100 times Pinatubo** data is from Jones et al. (2005)[^@jones2005]. This uses the
third-generation Hadley Centre AOGCM, HadCM3.

The **CESM1 LME** data is from a large project with Otto-Bliesner as the principal
investigator[^@ottobliesner2016]. The injected SO~2~ used is from the Gao et al.
(2008)[^@gao2008] ice-core derived estimates, and temperature records are the ensemble
median over five simulation runs.

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

<sup>**Figure:** Three simulations of a volcanic eruption of identical location in space
and time, but with three different magnitudes of injected SO~2~. All magnitudes include
four simulations, one in each season (Feb, May, Aug, Nov). Seasonal variability is
removed first in the Fourier domain, then their median and the 5^th^ to 95^th^
percentiles are calculated</sup>

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

<sup>**Figure:** Normalized temperature anomalies of the three different magnitude
simulations. The normalization constant is given in each label; on the left found by
making sure all temperature time series integrate to unity, on the right found as the
value that makes the minimum value equal to unity</sup>

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

<sup>**Figure:** The time series of the double-event simulation overlaid with
single-event simulations of the same magnitude, superposed and as individual time
series</sup>

### Aggregated data

#### Different forcings compared to temperature

How do the different forcings relate to the temperature, and does any of them have a
linear relationship with temperature?

With this, we want to look at how close the different forcings come to forming a linear
relationship with the temperature signal, that is, the absolute value of the temperature
anomaly due to the forcing.

Let us try to plot all non-zero values in the CESM LME forcing time series and the
corresponding temperature value at that element. There will be significant noise to
consider, especially for the smallest eruptions, and some eruptions that follow close
may get too large temperature values, but maybe numerous events will clear things up. We
may also use the deconvolution algorithm to get a response function estimate that we
subsequently use to estimate the temperature, thus reducing the noise.

We also add the CESM2 simulations and other simulation and observation data that we find
elsewhere to the mix.

> **_Legend explanation:_** Circles indicate CESM, triangles indicate VolMIP and
> quadrilaterals indicate Pinatubo. Short names relate to long names as follows:
>
> | Short Name | Long Name                    |
> | :--------- | :--------------------------- |
> | C2W        | CESM2(WACCM6)                |
> | C2WN       | CESM2(WACCM6), high latitude |
> | C2C        | CESM2(CAM6)                  |
> | C1C        | CESM1(CAM5)                  |
> | P          | Pinatubo, observational      |
> | P100       | 100 times Pinatubo           |
> | V1         | VolMIP, version 1            |
> | V2         | VolMIP, version 2            |

![Injection versus
temperature](<https://raw.githubusercontent.com/engeir/hack-md-notes/8821260/assets/pic/hidden-linear-forcing/injection_vs_temperature.png>
"Injection versus temperature" =49%x)
![Injection versus temperature on
semilog-x](<https://raw.githubusercontent.com/engeir/hack-md-notes/8821260/assets/pic/hidden-linear-forcing/injection_vs_temperature_logscale.png>
"Injection versus temperature on semilog-x" =49%x)

<sup>**Figure:** Temperature anomaly against injected SO~2~ on linear-linear axis (left)
and semilog-x axis (right)</sup>

![Injection versus aerosol optical
depth](<https://raw.githubusercontent.com/engeir/hack-md-notes/8821260/assets/pic/hidden-linear-forcing/injection_vs_aod.png>
"Injection versus aerosol optical depth" =49%x)
![Injection versus aerosol optical depth on log-log
axis](<https://raw.githubusercontent.com/engeir/hack-md-notes/8821260/assets/pic/hidden-linear-forcing/injection_vs_aod_logscale.png>
"Injection versus aerosol optical depth" =49%x)

<sup>**Figure:** Aerosol optical depth against injected SO~2~ on linear-linear axis
(left) and log-log axis (right)</sup>

![Aerosol optical depth versus
temperature](<https://raw.githubusercontent.com/engeir/hack-md-notes/8821260/assets/pic/hidden-linear-forcing/aod_vs_temperature.png>
"Aerosol optical depth versus temperature" =49%x)
![Aerosol optical depth versus temperature on semilog-x
axis](<https://raw.githubusercontent.com/engeir/hack-md-notes/8821260/assets/pic/hidden-linear-forcing/aod_vs_temperature_logscale.png>
"Aerosol optical depth versus temperature" =49%x)

<sup>**Figure:** Temperature anomaly against aerosol optical depth at the same locations
as defined by the injected SO~2~ forcing time series</sup>

#### Note on CESM-LME aerosol optical depth

The AODVIS field from the CESM LME data set seems to be too small, or at least very much
smaller than the corresponding fields that I get form my own CESM2 simulations.
Therefore, in the above plots, the CESM LME AOD has been scaled up by 24.05.

Let us first have a look at the fields that can be found in CESM2 that says something
about aerosol optical depth. This include:

| Legend   | Short Name | Long name                                             |
| :------- | :--------- | :---------------------------------------------------- |
| AOD(d)   | AODVIS     | Aerosol optical depth 550 nm, day only                |
| AOD(dn)  | AODVISdn   | Aerosol optical depth 550 nm, day night               |
| SAOD(nd) | AODVISstdn | Stratospheric aerosol optical depth 550 nm, day night |

We also include for reference the difference between `AOD(dn)` and `SAOD(dn)`.

![Different CESM2 AOD
fields](https://raw.githubusercontent.com/engeir/hack-md-notes/30fe88b/assets/pic/cesm-lme-aodvis/cesm2_field.png
"Different CESM2 AOD fields")

<sup>**Figure:** Different CESM2 AOD fields</sup>

Let us then focus more on the difference time series, namely `AOD(dn)-SAOD(dn)`, and
compare this to the AOD field that is found in the CESM LME data set. This also include
a shifted version, where the biggest eruption (1258) has been placed in 1852. This
eruption has an estimated injected SO~2~ of 258 Tg, while the CESM2 simulation we
compare with now uses an injected SO~2~ of 400 Tg.

| Legend      | Short Name | Long name                                     |
| :---------- | :--------- | :-------------------------------------------- |
| CL AOD      | AODVIS     | Aerosol optical depth 550 nm                  |
| CL AOD 1258 | AODVIS     | Aerosol optical depth 550 nm, shifted version |

![CESM LME original and shifted compared to the difference time series. Also included
for reference is the AOD(dn) time
series](https://raw.githubusercontent.com/engeir/hack-md-notes/30fe88b/assets/pic/cesm-lme-aodvis/compared_view.png
"CESM LME original and shifted compared to the difference time series. Also included for
reference is the AOD(dn) time series")

<sup>**Figure:** CESM LME original and shifted compared to the difference time series.
Also included for reference is the AOD(dn) time series</sup>

To better see the prominence of the 1258 eruption and where it was shifted to, below is
a plot of the full CESM LME AOD time series with both the original and shifted version.

![CESM LME original and shifted
version](https://raw.githubusercontent.com/engeir/hack-md-notes/30fe88b/assets/pic/cesm-lme-aodvis/view_shifted.png
"CESM LME original and shifted version")

<sup>**Figure:** CESM LME original and shifted version</sup>

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

[^@ottobliesner2016]:
    Otto-Bliesner, B. L., Brady, E. C., et al., 'Climate Variability and Change since
    850 CE: An Ensemble Approach with the Community Earth System Model', Bulletin of the
    American Meteorological Society, 2016, vol. 97, no. 5, p. 735–754.

[^@guo2004]:
    Guo, S., Bluth, G. J. S., et al., 'Re-evaluation of SO2 release of the 15 June 1991
    Pinatubo eruption using ultraviolet and infrared satellite sensors', Geochemistry,
    Geophysics, Geosystems, 2004, vol. 5, no. 4, p. Q04001.

[^@sukhodolov2018]:
    Sukhodolov, T., Sheng, J-X., et al., 'Stratospheric aerosol evolution after Pinatubo
    simulated with a coupled size-resolved aerosol-chemistry-climate model,
    SOCOL-AERv1.0', Geoscientific Model Development, 2018, vol. 11, no. 7, p. 2633–2647.

[^@jones2005]:
    Jones, G. S., Gregory, J. M., et al., 'An AOGCM simulation of the climate response
    to a volcanic super-eruption', Climate Dynamics, 2005, vol. 25, no. 7, p. 725–738.

[^@hansen1999]:
    Hansen, J., Ruedy, R., et al., 'GISS analysis of surface temperature change',
    Journal of Geophysical Research: Atmospheres, 1999, vol. 104, no. D24, p.
    30997–31022.

[^@gao2008]:
    Gao, C., Robock, A., et al., 'Volcanic forcing of climate over the past 1500 years:
    An improved ice core-based index for climate models', Journal of Geophysical
    Research: Atmospheres, 2008, vol. 113, no. D23, p. D23111.

[^@toohey2017]:
    Toohey, M. and Sigl, M., 'Volcanic stratospheric sulfur injections and aerosol
    optical depth from 500\,BCE to 1900\,CE', Earth System Science Data, 2017, vol. 9,
    no. 2, p. 809–831.

[^volmip-volc-long-eq]: https://view.es-doc.org/index.html?renderMethod=id&project=cmip6&id=fc04f8eb-feff-4fa4-ba91-41cf9041a2ef&version=1
[^volmip-volc-long-eq-realisation]: https://furtherinfo.es-doc.org/CMIP6.MPI-M.MPI-ESM1-2-LR.volc-long-eq.none.r11i1p1f1
