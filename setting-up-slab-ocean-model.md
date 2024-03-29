---
tags: Showcase, Notes
lang: en-GB
---

# Setting up slab ocean model

[![hackmd-github-sync-badge](https://hackmd.io/j4L-EIhRQqGdl5KmiIZ-_w/badge)](https://hackmd.io/@engeir/B1GswcMf2)
[![view-on-github](https://img.shields.io/badge/View%20on-GitHub-yellowgreen)](https://github.com/engeir/hack-md-notes/blob/main/setting-up-slab-ocean-model.md)

## Q-flux files

We first want to generate q-flux files that go with the slab ocean simulation, based on
the fully dynamical model.

We ran the **BWma1850** compset in its default setting from 1850 to 1902 and generated
the q-flux files based on the years 1856 to 1900. Below is a plot of the temperature
and ice fraction evolution during the whole control run.

![Reference height temperature](https://raw.githubusercontent.com/engeir/hack-md-notes/bc8bbfb/assets/pic/setting-up-slab-ocean-model/trefht-slab-ocean-control.webp)

![Ice fraction](https://raw.githubusercontent.com/engeir/hack-md-notes/bc8bbfb/assets/pic/setting-up-slab-ocean-model/icefrac-slab-ocean-control.webp)

In the above plots, the red line is the control run used to generate the q-flux files.

## Problems

We also see some other simulations in the plot. In particular, the orange line is the
**EWma1850** compset, which is supposed to be the slab ocean model run with the WACCM6
atmosphere. However, the ice fraction and surface temperature are not stable and keep
diverging far from the level of the control. Why is that?

## Simulations

There seems to be some issues with the climate reaching a new state.

![Temperature](./assets/pic/setting-up-slab-ocean-model/temp_m.png)

![Ice fraction](./assets/pic/setting-up-slab-ocean-model/ice_m.png)

![Temperature](./assets/pic/setting-up-slab-ocean-model/temp_s.png)

![Ice fraction](./assets/pic/setting-up-slab-ocean-model/ice_s.png)
