---
tags: Showcase, Notes
---

# Deconvolution of CESM LME data

[![hackmd-github-sync-badge](https://hackmd.io/j4L-EIhRQqGdl5KmiIZ-_w/badge)](https://hackmd.io/j4L-EIhRQqGdl5KmiIZ-_w)
[![view-on-github](https://img.shields.io/badge/View%20on-GitHub-yellowgreen)](https://github.com/engeir/hack-md-notes/blob/main/cesm_lme_deconvolution.md)

## Data

The data is from a series of CESM simulations of the last millennium, part of the CESM
last millennium ensemble (LME) project.

The forcing used is _net solar flux at the top of the atmosphere_ while the temperature
used is the _reference height temperature_. From the CESM LME set of simulations, an
ensemble of five runs were performed where volcanoes were the only external forcing.

## Single ensemble member

Let us first have a look at one single ensemble member, without any processing, just the
raw output from the model. Both the forcing and the temperature will have strong
seasonal dependence, but it may still be useful as a check of the deconvolution
algorithm.
