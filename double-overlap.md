---
tags: Showcase, Notes
geometry: margin=3cm,top=3cm
---

# Double Volcano Event

[![hackmd-github-sync-badge](https://hackmd.io/j4L-EIhRQqGdl5KmiIZ-_w/badge)](https://hackmd.io/@engeir/BkbwDbxAq)
[![view-on-github](https://img.shields.io/badge/View%20on-GitHub-yellowgreen)](https://github.com/engeir/hack-md-notes/blob/main/double-overlap.md)

## Smoothing

Let us first have a look at the raw reference temperature output:

![Initial smoothing](https://github.com/engeir/hack-md-notes/raw/71d8ff5538414d38b4c340488678c0062d70c9f8/assets/pic/double-overlap/double-overlap-temp-smoothing.png "Initial smoothing")

The smoothing is done by subtracting a pure sinusoid (amplitude of the sinusoid found by
trial and error, what looked best) and by removing frequencies around one from the
Fourier domain. The volcanoes signal is merely to show where in time the volcanoes
appeared in the simulation.

The problem with subtracting a pure sinusoid is that the amplitude of the seasonal
variance changes with how much the temperature is perturbed. This is most evident in the
winter of 1853/54. Removing frequencies in the Fourier domain works best, but the sharp
initial response to the forcing is smoothed more than one would wish for.

## Forcing

We may have a closer look at the forcing as well. Here we see _total aerosol optical
depth in visible band_:

![Forcing AEROD_v](https://raw.githubusercontent.com/engeir/hack-md-notes/41979246af0f67763b300afda0217d3ec4734389/assets/pic/double-overlap/double-overlap-aerod_v.png "Forcing AEROD_v")

## Superposition

Finally, let us grab one of the single event simulations and try to add it to itself
with an appropriate shift in time, to see how close we get to the double event
simulation.

![Superposition of single events on top of Fourier smoothed temperature. Shading shows the length of the single event time series](https://github.com/engeir/hack-md-notes/raw/7ce37cbef16da459fc2692feffd6fad34a37883f/assets/pic/double-overlap/double-overlap-superpose.png "Superposition of single events on top of Fourier smoothed temperature. Shading shows the length of the single event time series")
