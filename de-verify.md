---
tags: Showcase, Notes
geometry: margin=3cm,top=3cm
---

# Deconvolution of strange data

[![hackmd-github-sync-badge](https://hackmd.io/j4L-EIhRQqGdl5KmiIZ-_w/badge)](https://hackmd.io/@engeir/SyMdeKsfi)
[![view-on-github](https://img.shields.io/badge/View%20on-GitHub-yellowgreen)](https://github.com/engeir/hack-md-notes/blob/main/de-verify.md)

## The Set-Up

Let us run some experiments with short and longer (if results are bad) deconvolution
iteration, to try to mask out what make deconvolving hard.

```python
import de_verify
exp = de_verify.Experiment
```

## A Clean Run

For our first experiment, we just create a forcing and corresponding temperature from
convolving with a response function. This of course works well.

```python
exp().related_timeseries().deconvolve().combined_view()  # This one is easy!
```

![v1](https://github.com/engeir/hack-md-notes/raw/main/assets/pic/de-verify/v1.png)

## Kick Flip

If we use the same time series as above, but flip them around (so that they occupy the
same range in `y`), suddenly deconvolving become really hard!

```python
# When the time series are flipped, it already become quite hard!
exp().related_timeseries().flip().deconvolve().combined_view()
exp().related_timeseries().flip().deconvolve(1000).combined_view()
exp().related_timeseries().flip().vertical_shift(-2).deconvolve(1000).combined_view()
exp().related_timeseries().flip().deconvolve(1000, scale_factor=10).combined_view()
```

![v2](https://github.com/engeir/hack-md-notes/raw/main/assets/pic/de-verify/v2.png)
![v3](https://github.com/engeir/hack-md-notes/raw/main/assets/pic/de-verify/v3.png)
![v4](https://github.com/engeir/hack-md-notes/raw/main/assets/pic/de-verify/v4.png)
![v5](https://github.com/engeir/hack-md-notes/raw/main/assets/pic/de-verify/v5.png)

## Noisy Minimum

Let us add some noise to our clean time series. We expect the deconvolution to handle
this, and sure enough, if the standard deviation is 0.2 times the standard deviation of
the time series, we can obtain good estimates of the response function. Note, however,
that if we do something as (seemingly) harmless as to shift the time series up so that
the equilibrium is no longer at zero along `y`, all goes to hell. Instead, the minimum
value (including the added noise) is now at zero.

```python
# This amount of noise is not a big problem!
exp().related_timeseries().noise(0.2).deconvolve(100).combined_view()
# But, it sure looks like one should have the true equilibrium at zero, and not let the
# "negative" noise be positive!
exp().related_timeseries().noise(0.2).set2zero().deconvolve(100).combined_view()
exp().related_timeseries().noise(0.2).deconvolve(100, scale_factor=10).combined_view()
exp().related_timeseries().noise(0.2).deconvolve(2000, scale_factor=10).combined_view()
exp().related_timeseries().noise(0.6).deconvolve(100, scale_factor=10).combined_view()
```

![v6](https://github.com/engeir/hack-md-notes/raw/main/assets/pic/de-verify/v6.png)
![v7](https://github.com/engeir/hack-md-notes/raw/main/assets/pic/de-verify/v7.png)
![v8](https://github.com/engeir/hack-md-notes/raw/main/assets/pic/de-verify/v8.png)
![v9](https://github.com/engeir/hack-md-notes/raw/main/assets/pic/de-verify/v9.png)
![v10](https://github.com/engeir/hack-md-notes/raw/main/assets/pic/de-verify/v10.png)

## Vertically Rising Issues

If we look more closely at what happens if we shift the time series along the
`y`-direction, we notice that it is really hard to get any good estimates from it.

**Make sure that the real equilibrium is at zero!** _(Easier said than done…)_

```python
# A simple vertical shift also complicates things!
exp().related_timeseries().vertical_shift((50, 278)).deconvolve(100).combined_view()
exp().related_timeseries().vertical_shift((1, 1)).deconvolve(100).combined_view()
exp().related_timeseries().vertical_shift((1, 1)).deconvolve(1000).combined_view()
exp().related_timeseries().vertical_shift((1, 1)).deconvolve(1000, scale_factor=10).combined_view()
exp().related_timeseries().vertical_shift((1, 1)).deconvolve(1000, cutoff=10).combined_view()
```

![v11](https://github.com/engeir/hack-md-notes/raw/main/assets/pic/de-verify/v11.png)
![v12](https://github.com/engeir/hack-md-notes/raw/main/assets/pic/de-verify/v12.png)
![v13](https://github.com/engeir/hack-md-notes/raw/main/assets/pic/de-verify/v13.png)
![v14](https://github.com/engeir/hack-md-notes/raw/main/assets/pic/de-verify/v14.png)
![v15](https://github.com/engeir/hack-md-notes/raw/main/assets/pic/de-verify/v15.png)

## The Scale of the Issue

Now, what about scaling the pure and clean time series? Both, or just one of them? That
is fine, luckily.

```python
exp().related_timeseries().scale(10).deconvolve().combined_view()
exp().related_timeseries().scale((10, 100)).deconvolve().combined_view()
exp().related_timeseries().scale((100, 35)).deconvolve(1000).combined_view()
```

![v16](https://github.com/engeir/hack-md-notes/raw/main/assets/pic/de-verify/v16.png)
![v17](https://github.com/engeir/hack-md-notes/raw/main/assets/pic/de-verify/v17.png)
![v18](https://github.com/engeir/hack-md-notes/raw/main/assets/pic/de-verify/v18.png)
