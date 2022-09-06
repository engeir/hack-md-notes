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
used is the _reference height temperature_. From the CESM LAME set of simulations, an
ensemble of five runs were performed where volcanoes were the only external forcing.

## Single ensemble member

Let us first have a look at one single ensemble member, without any processing, just the
raw output from the model. Both the forcing and the temperature will have strong
seasonal dependence, but it may still be useful as a check of the deconvolution
algorithm.

![Forcing of ensemble 1 without
averaging](<https://raw.githubusercontent.com/engeir/hack-md-notes/819f9dcb33ead0d409a80bcc386f4ceebd891dc3/assets/pic/deconv-cesm-lme/cesm_lme_deconvolution_ens1_nomean_forcing.png>
"Forcing of ensemble 1 without averaging" =45%x)
![Temperature of ensemble 1 without
averaging](<https://raw.githubusercontent.com/engeir/hack-md-notes/819f9dcb33ead0d409a80bcc386f4ceebd891dc3/assets/pic/deconv-cesm-lme/cesm_lme_deconvolution_ens1_nomean_temperature.png>
"Temperature of ensemble 1 without averaging" =45%x)

![Response from deconvolution of the forcing and temperature signals above](https://raw.githubusercontent.com/engeir/hack-md-notes/819f9dcb33ead0d409a80bcc386f4ceebd891dc3/assets/pic/deconv-cesm-lme/cesm_lme_deconvolution_ens1_nomean-respnse.png "Response from deconvolution of the forcing and temperature signals above")

## Single ensemble member averaging

Let us then see what averaging by means of removing frequencies near 1 in Fourier domain
will do to our signal. Again, only one ensemble member is used.

![Forcing of ensemble 1 with
averaging](<https://raw.githubusercontent.com/engeir/hack-md-notes/6c20ab748912530c65e30e648c04b4e45a55b838/assets/pic/deconv-cesm-lme/cesm_lme_deconvolution_ens1_mean_forcing.png>
"Forcing of ensemble 1 with averaging" =45%x)
![Temperature of ensemble 1 with
averaging](<https://raw.githubusercontent.com/engeir/hack-md-notes/6c20ab748912530c65e30e648c04b4e45a55b838/assets/pic/deconv-cesm-lme/cesm_lme_deconvolution_ens1_mean_temperature.png>
"Temperature of ensemble 1 with averaging" =45%x)

![Response from deconvolution of the forcing and temperature signals above](https://raw.githubusercontent.com/engeir/hack-md-notes/6c20ab748912530c65e30e648c04b4e45a55b838/assets/pic/deconv-cesm-lme/cesm_lme_deconvolution_ens1_mean-respnse.png "Response from deconvolution of the forcing and temperature signals above")

## All ensemble members

Now we do the same analysis as in the first section, namely without averaging, but where
we take all five ensemble members and compute their mean to get a common forcing and
temperature.

![Forcing of all ensembles without
averaging](<https://raw.githubusercontent.com/engeir/hack-md-notes/6c20ab748912530c65e30e648c04b4e45a55b838/assets/pic/deconv-cesm-lme/cesm_lme_deconvolution_ensall_nomean_forcing.png>
"Forcing of all ensembles without averaging" =45%x)
![Temperature of all ensembles without
averaging](<https://raw.githubusercontent.com/engeir/hack-md-notes/6c20ab748912530c65e30e648c04b4e45a55b838/assets/pic/deconv-cesm-lme/cesm_lme_deconvolution_ensall_nomean_temperature.png>
"Temperature of all ensembles without averaging" =45%x)

![Response from deconvolution of the forcing and temperature signals above](https://raw.githubusercontent.com/engeir/hack-md-notes/6c20ab748912530c65e30e648c04b4e45a55b838/assets/pic/deconv-cesm-lme/cesm_lme_deconvolution_ensall_nomean-respnse.png "Response from deconvolution of the forcing and temperature signals above")

## All ensemble members averaging

Finally, we now use all five ensemble members, remove frequencies around 1 on all of
them individually, before a common mean is computed across the ensemble to give the
forcing and temperature.

![Forcing of all ensembles without
averaging](<https://raw.githubusercontent.com/engeir/hack-md-notes/6c20ab748912530c65e30e648c04b4e45a55b838/assets/pic/deconv-cesm-lme/cesm_lme_deconvolution_ensall_mean_forcing.png>
"Forcing of all ensembles without averaging" =45%x)
![Temperature of all ensembles without
averaging](<https://raw.githubusercontent.com/engeir/hack-md-notes/6c20ab748912530c65e30e648c04b4e45a55b838/assets/pic/deconv-cesm-lme/cesm_lme_deconvolution_ensall_mean_temperature.png>
"Temperature of all ensembles without averaging" =45%x)

![Response from deconvolution of the forcing and temperature signals above](https://raw.githubusercontent.com/engeir/hack-md-notes/6c20ab748912530c65e30e648c04b4e45a55b838/assets/pic/deconv-cesm-lme/cesm_lme_deconvolution_ensall_mean-respnse.png "Response from deconvolution of the forcing and temperature signals above")
