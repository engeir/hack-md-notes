---
tags: Showcase, Notes
---

# Deconvolution of CESM LME data

[![hackmd-github-sync-badge](https://hackmd.io/j4L-EIhRQqGdl5KmiIZ-_w/badge)](https://hackmd.io/@engeir/Sy1iHzrgs)
[![view-on-github](https://img.shields.io/badge/View%20on-GitHub-yellowgreen)](https://github.com/engeir/hack-md-notes/blob/main/cesm_lme_deconvolution.md)

## Data

The data is from a series of CESM simulations of the last millennium, part of the CESM
last millennium ensemble (LME) project.

The forcing used is _net solar flux at the top of the atmosphere_ while the temperature
used is the _reference height temperature_. From the CESM LME set of simulations, an
ensemble of five runs were performed where volcanoes were the only external forcing.

## All ensemble members averaging

We use all ensemble members to average over, where each ensemble run have been smoothed
prior to averaging by removing frequencies in the Fourier domain. This include the
seasonal variability and some of the overtones found at multiples of the seasonal
frequency.

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
"Response from deconvolution of the forcing and temperature signals above, 100 iterations")
![Response from deconvolution of the forcing and temperature signals above, 1000
iterations](https://raw.githubusercontent.com/engeir/hack-md-notes/bc886d14675a7adf135447fdcaa8683dd90fdb97/assets/pic/deconv-cesm-lme/cesm_lme_deconvolution_ensall_mean_1000-respnse.png
"Response from deconvolution of the forcing and temperature signals above, 1000
iterations")
![Response from deconvolution of the forcing and temperature signals above, 10000
iterations](https://raw.githubusercontent.com/engeir/hack-md-notes/bc886d14675a7adf135447fdcaa8683dd90fdb97/assets/pic/deconv-cesm-lme/cesm_lme_deconvolution_ensall_mean-10000_respnse.png
"Response from deconvolution of the forcing and temperature signals above, 10000
iterations")
