---
tags: Showcase, Notes
---

# Hidden Forcing

[![hackmd-github-sync-badge](https://hackmd.io/j4L-EIhRQqGdl5KmiIZ-_w/badge)](https://hackmd.io/@engeir/SJPvH8Ecj)
[![view-on-github](https://img.shields.io/badge/View%20on-GitHub-yellowgreen)](https://github.com/engeir/hack-md-notes/blob/main/hidden-linear-forcing.md)

> How does the different forcings relate to the temperature, and does any of them have a
> linear relationship with temperature?

With this, we want to look at how close the different forcings come to forming a linear
relationship with the temperature signal.

## Temperature

Let us first have a look at the temperature response as a deviation from the equilibrium
for three different volcanic eruption strengths.

![Temperature anomaly for three different volcanic
eruptions](https://raw.githubusercontent.com/engeir/hack-md-notes/8f00ad6973ddabc008c2f26d45b8473bc8790f2b/assets/pic/hidden-linear-forcing/trefht-which-forcing.png
"Temperature anomaly for three different volcanic eruptions")

## Forcings

Now, let us create an equivalent plot for the three different forcing time series;
aerosol optical depth, total injected sulphate and top of the atmosphere radiation
imbalance.

![Aerosol optical depth for three different volcanic
eruptions](<https://raw.githubusercontent.com/engeir/hack-md-notes/23da90d9caad1afbb1cf9ebe5dda0b137c550a85/assets/pic/hidden-linear-forcing/aod-which-forcing.png>
"Aerosol optical depth for three different volcanic eruptions" =33%x) ![Total injected
sulphate for three different volcanic
eruptions](<https://raw.githubusercontent.com/engeir/hack-md-notes/23da90d9caad1afbb1cf9ebe5dda0b137c550a85/assets/pic/hidden-linear-forcing/injected-which-forcing.png>
"Total injected sulphate for three different volcanic eruptions" =32%x) ![Radiation
imbalance for three different volcanic
eruptions](<https://raw.githubusercontent.com/engeir/hack-md-notes/23da90d9caad1afbb1cf9ebe5dda0b137c550a85/assets/pic/hidden-linear-forcing/raddiff-which-forcing.png>
"Radiation imbalance for three different volcanic eruptions" =33%x)

## Comparison

Now, let us use the peak values, marked in each plot above with red, horizontal lines,
and plot forcing peaks against temperature peaks.

![Aerosol optical depth versus
temperature](<https://raw.githubusercontent.com/engeir/hack-md-notes/23da90d9caad1afbb1cf9ebe5dda0b137c550a85/assets/pic/hidden-linear-forcing/aod-trefht-which-forcing.png>
"Aerosol optical depth versus temperature" =33%x) ![Total injected sulphate versus
temperature](<https://raw.githubusercontent.com/engeir/hack-md-notes/23da90d9caad1afbb1cf9ebe5dda0b137c550a85/assets/pic/hidden-linear-forcing/injected-trefht-which-forcing.png>
"Total injected sulphate versus temperature" =32%x) ![Radiation imbalance versus
temperature](<https://raw.githubusercontent.com/engeir/hack-md-notes/23da90d9caad1afbb1cf9ebe5dda0b137c550a85/assets/pic/hidden-linear-forcing/raddiff-trefht-which-forcing.png>
"Radiation imbalance versus temperature" =33%x)

## CESM LME

But in the above, we have only three data points to compare, which are many too few. Let
us instead try to plot all non-zero values in the CESM LME forcing time series and the
corresponding temperature value at that element. There will be significant noise to
consider especially for the smallest eruptions, and some eruptions that follow close may
get unrealistically large temperature values, but maybe the large number of events will
clear things up. We may also use the deconvolution algorithm to get a response function
estimate that we subsequently use to estimate the temperature, thus reducing the noise.

![Injection versus
temperature](https://raw.githubusercontent.com/engeir/hack-md-notes/b9109bd/assets/pic/hidden-linear-forcing/injection_vs_temperature.png
"Injection versus temperature")

![Injection versus temperature without
deconvolution](https://raw.githubusercontent.com/engeir/hack-md-notes/b9109bd/assets/pic/hidden-linear-forcing/injection_vs_temperature_orig.png
"Injection versus temperature without deconvolution")

![Injection versus aerosol optical
depth](https://raw.githubusercontent.com/engeir/hack-md-notes/b9109bd/assets/pic/hidden-linear-forcing/injection_vs_aod.png
"Injection versus aerosol optical depth")

== DEPRECATED ==

![Injection versus aerosol optical depth on log-log
axis](https://raw.githubusercontent.com/engeir/hack-md-notes/5e6c202/assets/pic/hidden-linear-forcing/injection_vs_aod_loglog.png
"Injection versus aerosol optical depth")

== DEPRECATED ==

![Aerosol optical depth versus
temperature](https://raw.githubusercontent.com/engeir/hack-md-notes/a3ae5d0/assets/pic/hidden-linear-forcing/aod_vs_temperature.png
"Aerosol optical depth versus temperature")

![Aerosol optical depth versus temperature on semilog-x
axis](https://raw.githubusercontent.com/engeir/hack-md-notes/b9109bd/assets/pic/hidden-linear-forcing/aod_vs_temperature_semilogx.png
"Aerosol optical depth versus temperature")
