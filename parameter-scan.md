---
tags: Showcase, Papers
---

# Parameter Scan

[![hackmd-github-sync-badge](https://hackmd.io/j4L-EIhRQqGdl5KmiIZ-_w/badge)](https://hackmd.io/@engeir/SkEWr9Okh)
[![view-on-github](https://img.shields.io/badge/View%20on-GitHub-yellowgreen)](https://github.com/engeir/hack-md-notes/blob/main/parameter-scan.md)

This note first looks into how the three different forcing strengths alter the
temperature signal. That is if we normalize and do not care about the amplitude of the
signals, does the temperature show a similar shape across all three forcing strengths?

## Individual without normalization

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

## Comparing normalized time series

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

## Smoothing

Let us first consider the raw reference temperature. The smoothing is done by removing
frequencies around $1$ in the Fourier domain.

Removing frequencies in the Fourier domain works quite well, but the sharp initial
response to the forcing is smoothed more than one would hope for.

## Superposition

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

## Different forcings compared to temperature
