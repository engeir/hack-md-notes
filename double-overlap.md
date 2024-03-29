---
tags: Showcase, Notes
geometry: margin=3cm,top=3cm
---

# Double Volcano Event

[![hackmd-github-sync-badge](https://hackmd.io/j4L-EIhRQqGdl5KmiIZ-_w/badge)](https://hackmd.io/@engeir/BkbwDbxAq)
[![view-on-github](https://img.shields.io/badge/View%20on-GitHub-yellowgreen)](https://github.com/engeir/hack-md-notes/blob/main/double-overlap.md)

## Smoothing

Let us first have a look at the raw reference temperature:

![Initial
smoothing](https://raw.githubusercontent.com/engeir/hack-md-notes/1e3d1dca42484fc10c418dd1ede027301c9a532d/assets/pic/double-overlap/double-overlap-temp-smoothing-simple.png
"Initial smoothing")

The smoothing is done by subtracting a pure sinusoid (amplitude of the sinusoid found by
trial and error, what looked best) and by removing frequencies around one in the
Fourier domain. The _volcanoes_ signal is merely to show where in time the volcanoes
appeared in the simulation.

The problem with subtracting a pure sinusoid is that the amplitude of the seasonal
variance changes with how much the temperature is perturbed. This is most evident in the
winter of 1853/54. Removing frequencies in the Fourier domain works better, but the
sharp initial response to the forcing is smoothed more than one would hope for.

## Forcing

We may have a closer look at the forcing as well. Here is _total aerosol optical depth
in visible band_:

![Forcing
AEROD_v](https://raw.githubusercontent.com/engeir/hack-md-notes/a19bdfc5ad051cd259bd9741e67e1bf3ebe1e718/assets/pic/double-overlap/double-overlap-aerod_v.png
"Forcing AEROD_v")

Two single events (black) is plotted on top of the double event aerosol forcing (red).

## Superposition

Finally, let us grab one of the single event simulations and try to superpose a copy of
itself with an appropriate shift in time, to see how close we get to the double event
simulation.

![Superposition (blue) of two single events (black) on top of Fourier smoothed
temperature (red). Shading shows the length of the single event time series without
padding](https://raw.githubusercontent.com/engeir/hack-md-notes/1e3d1dca42484fc10c418dd1ede027301c9a532d/assets/pic/double-overlap/double-overlap-superpose.png
"Superposition (blue) of two single events (black) on top of Fourier smoothed
temperature (red). Shading shows the length of the single event time series without
padding")

The two single events are not long enough to cover to whole double event time series,
but still come close to replicating the double event until the end of the first shadowed
region. After this, the tail of the first single event is lost.
