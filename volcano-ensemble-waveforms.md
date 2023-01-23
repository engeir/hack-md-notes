---
tags: Showcase, Notes
geometry: margin=3cm,top=3cm
---

# Volcano Waveforms

[![hackmd-github-sync-badge](https://hackmd.io/j4L-EIhRQqGdl5KmiIZ-_w/badge)](https://hackmd.io/@engeir/HyXpCJ_C9)
[![view-on-github](https://img.shields.io/badge/View%20on-GitHub-yellowgreen)](https://github.com/engeir/hack-md-notes/blob/main/volcano-ensemble-waveforms.md)

This note looks into how the three different forcing strengths alter the temperature
signal. That is, if we normalize and do not care about the amplitude of the signals, do
the temperature show a similar shape across all three forcing strengths?

## Individual without normalization

We may first have a look at what the ensemble median and the 5th to 95th percentiles
look like.

![Medium (smallest) forcing
strength](https://raw.githubusercontent.com/engeir/hack-md-notes/4c76fa84d73699f3dd51cf9a8234d9142e54e9d1/assets/pic/volcano-ensemble-waveforms/medium-waveform.png
"Medium (smallest) forcing strength")

![Medium-plus (middle) forcing
strength](https://raw.githubusercontent.com/engeir/hack-md-notes/4c76fa84d73699f3dd51cf9a8234d9142e54e9d1/assets/pic/volcano-ensemble-waveforms/medium-plus-waveform.png
"Medium-plus (middle) forcing strength")

![Strong (strongest) forcing
strength](https://raw.githubusercontent.com/engeir/hack-md-notes/4c76fa84d73699f3dd51cf9a8234d9142e54e9d1/assets/pic/volcano-ensemble-waveforms/strong-waveform.png
"Strong (strongest) forcing strength")

## Comparing normalized time series

If we now normalize all time series by dividing by the integral over the whole time
series, where we first shift all time series so that the equilibrium temperature is at
zero, we get the plot shown below.

![Medium (blue and full), medium-plus (orage and dotted) and strong (green dashed)
overlaid. The black plots are the medians across the four participant ensemble, while
the coloured shading cover the 5th to the 95th
percentile](https://raw.githubusercontent.com/engeir/hack-md-notes/4c76fa84d73699f3dd51cf9a8234d9142e54e9d1/assets/pic/volcano-ensemble-waveforms/compare-waveform-integrate.png
"Medium (blue and full), medium-plus (orage and dotted) and strong (green dashed)
overlaid. The black plots are the medians across the four participant ensemble, while
the coloured shading cover the 5th to the 95th percentile")

![Same as above, but scaled by the maximum
value](https://raw.githubusercontent.com/engeir/hack-md-notes/4c76fa84d73699f3dd51cf9a8234d9142e54e9d1/assets/pic/volcano-ensemble-waveforms/compare-waveform-integrate.png
"Same as above, but scaled by the maximum value")
