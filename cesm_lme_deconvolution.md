---
tags: Showcase, Notes
---

# Deconvolution of CESM LME data

[![hackmd-github-sync-badge](https://hackmd.io/j4L-EIhRQqGdl5KmiIZ-_w/badge)](https://hackmd.io/@engeir/Sy1iHzrgs)
[![view-on-github](https://img.shields.io/badge/View%20on-GitHub-yellowgreen)](https://github.com/engeir/hack-md-notes/blob/main/cesm_lme_deconvolution.md)

## Data

The data is from a series of CESM simulations of the last millennium, part of the CESM
last millennium ensemble (LME) project.

The forcing used is the _net solar flux at the top of the atmosphere_ while the
temperature used is the _reference height temperature_. From the CESM LME set of
simulations, an ensemble of five runs was performed where volcanoes were the only
external forcing.

## All ensemble members averaging

We use all ensemble members to average over, where each ensemble run has been smoothed
before averaging by removing frequencies in the Fourier domain. This includes the
seasonal variability and some overtones found at multiples of the seasonal frequency.

After this, the time series are flipped (multiplied by -1), then shifted and scaled to
have a mean of zero and unit standard deviation. Finally, the time series are again
shifted vertically to have the mean equilibrium value at zero, where the mean
equilibrium value is calculated from the first 200 years.

![Forcing of all ensembles with
averaging](<https://raw.githubusercontent.com/engeir/hack-md-notes/bc886d14675a7adf135447fdcaa8683dd90fdb97/assets/pic/deconv-cesm-lme/cesm_lme_deconvolution_ensall_mean_10000_forcing.png>
"Forcing of all ensembles with averaging" =45%x)
![Temperature of all ensembles with
averaging](<https://raw.githubusercontent.com/engeir/hack-md-notes/bc886d14675a7adf135447fdcaa8683dd90fdb97/assets/pic/deconv-cesm-lme/cesm_lme_deconvolution_ensall_mean_10000_temperature.png>
"Temperature of all ensembles with averaging" =45%x)

Below are three estimates of the response function, where the variation is in the number
of iterations allowed for the deconvolution algorithm.

![Response from deconvolution of the forcing and temperature signals above, 100
iterations](https://raw.githubusercontent.com/engeir/hack-md-notes/bc886d14675a7adf135447fdcaa8683dd90fdb97/assets/pic/deconv-cesm-lme/cesm_lme_deconvolution_ensall_mean_100-respnse.png
"Response from deconvolution of the forcing and temperature signals above, 100
iterations")
![Response from deconvolution of the forcing and temperature signals above, 1000
iterations](https://raw.githubusercontent.com/engeir/hack-md-notes/bc886d14675a7adf135447fdcaa8683dd90fdb97/assets/pic/deconv-cesm-lme/cesm_lme_deconvolution_ensall_mean_1000-respnse.png
"Response from deconvolution of the forcing and temperature signals above, 1000
iterations")
![Response from deconvolution of the forcing and temperature signals above, 10000
iterations](https://raw.githubusercontent.com/engeir/hack-md-notes/bc886d14675a7adf135447fdcaa8683dd90fdb97/assets/pic/deconv-cesm-lme/cesm_lme_deconvolution_ensall_mean-10000_respnse.png
"Response from deconvolution of the forcing and temperature signals above, 10000
iterations")

## Using delta pulse forcing

From [Deconvolution of strange data](/FFrnfgKrRTmOC8BqAiVgEA) it is evident that the
forcing with some duration time on all peaks, a decaying part, is much harder to
deconvolve than a forcing that only contains arrival times and amplitude. Therefore, we
instead find the raw volcanic forcing used in CESM1 to make the CESM LME simulations and
deconvolve this with the temperature.

![Forcing](<https://raw.githubusercontent.com/engeir/hack-md-notes/main/assets/pic/deconv-cesm-lme/cesm_lme_deconvolution_delta_1000_forcing.png>
"With 1000 iterations: forcing" =45%x)
![Temperature](<https://raw.githubusercontent.com/engeir/hack-md-notes/main/assets/pic/deconv-cesm-lme/cesm_lme_deconvolution_delta_1000_temperature.png>
"With 1000 iterations: temperature" =45%x)

The first response shown below is when running the algorithm for 1000 iterations, while
the bottom is from using 10000 iterations. The shape is robust.

![With 1000 iterations:
response](https://raw.githubusercontent.com/engeir/hack-md-notes/main/assets/pic/deconv-cesm-lme/cesm_lme_deconvolution_delta_1000-respnse.png
"With 1000 iterations: response")
![With 10000 iterations:
response](https://raw.githubusercontent.com/engeir/hack-md-notes/main/assets/pic/deconv-cesm-lme/cesm_lme_deconvolution_delta_10000-respnse.png
"With 10000 iterations: response")

## Noise

Three different cut-offs, with the same x-axis.

![Cut off after 3
years](https://raw.githubusercontent.com/engeir/hack-md-notes/aaa8494525cd9b2e50ae76219b22a48f84611a10/assets/pic/deconv-cesm-lme/cesm-lme-cut3-iter50.png
"Cut off after 3 years") ![Cut off after 20
years](https://raw.githubusercontent.com/engeir/hack-md-notes/aaa8494525cd9b2e50ae76219b22a48f84611a10/assets/pic/deconv-cesm-lme/cesm-lme-cut20-iter50.png
"Cut off after 20 years") ![Cut off after 70
years](https://raw.githubusercontent.com/engeir/hack-md-notes/aaa8494525cd9b2e50ae76219b22a48f84611a10/assets/pic/deconv-cesm-lme/cesm-lme-cut70-iter50.png
"Cut off after 70 years")

Cut-off after 90 years.

![Cut off after 90
years](https://raw.githubusercontent.com/engeir/hack-md-notes/aaa8494525cd9b2e50ae76219b22a48f84611a10/assets/pic/deconv-cesm-lme/cesm-lme-cut90-iter50.png
"Cut off after 90 years")

Cut-off after 90 and 200 years, zoomed in on the year 194.

![Cut off after 90
years](https://raw.githubusercontent.com/engeir/hack-md-notes/aaa8494525cd9b2e50ae76219b22a48f84611a10/assets/pic/deconv-cesm-lme/cesm-lme-cut90-iter50-example194.png
"Cut off after 90 years") ![Cut off after 200
years](https://raw.githubusercontent.com/engeir/hack-md-notes/aaa8494525cd9b2e50ae76219b22a48f84611a10/assets/pic/deconv-cesm-lme/cesm-lme-cut200-iter50-example194.png
"Cut off after 200 years")

Cut-off after 8 years, zoomed in on the initial peak.

![Cut off after 8 years, zoomed in on year
6](https://raw.githubusercontent.com/engeir/hack-md-notes/aaa8494525cd9b2e50ae76219b22a48f84611a10/assets/pic/deconv-cesm-lme/cesm-lme-cut8-iter50-example6.png
"Cut off after 8 years, zoomed in on year 6")
