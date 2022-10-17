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
seed = 20
show = False
```

## A Clean Run

For our first experiment, we just create a forcing and corresponding temperature from
convolving with a response function. This of course works well.

```python
exp().related_timeseries(seed=seed).deconvolve().combined_view(save="v1", show=show)  # This one is easy!
```

![v1](https://github.com/engeir/hack-md-notes/raw/main/assets/pic/de-verify/v1.png)

## Flip

If we use the same time series as above, but flip them around (so that they occupy the
same range in `y`), suddenly deconvolving become really hard!

```python
# When the time series are flipped, it already become quite hard!
exp().related_timeseries(seed=seed).flip().deconvolve().combined_view(save="v2", show=show)
exp().related_timeseries(seed=seed).flip().deconvolve(1000).combined_view(save="v3", show=show)
exp().related_timeseries(seed=seed).flip().vertical_shift(-2).deconvolve(1000).combined_view(save="v4", show=show)
exp().related_timeseries(seed=seed).flip().deconvolve(1000, scale_factor=10).combined_view(save="v5", show=show)
```

![v2](https://github.com/engeir/hack-md-notes/raw/main/assets/pic/de-verify/v2.png)
![v3](https://github.com/engeir/hack-md-notes/raw/main/assets/pic/de-verify/v3.png)
![v4](https://github.com/engeir/hack-md-notes/raw/main/assets/pic/de-verify/v4.png)
![v5](https://github.com/engeir/hack-md-notes/raw/main/assets/pic/de-verify/v5.png)

## Noisy

Let us add some noise to our clean time series. We expect the deconvolution to handle
this, and sure enough, if the standard deviation is 0.2 times the standard deviation of
the time series, we can obtain good estimates of the response function. Note, however,
that if we do something as (seemingly) harmless as to shift the time series up so that
the equilibrium is no longer at zero along `y`, all goes to hell. Instead, the minimum
value (including the added noise) is now at zero.

```python
# This amount of noise is not a big problem!
exp().related_timeseries(seed=seed).noise(0.2).deconvolve(100).combined_view(save="v6", show=show)
# But, it sure looks like one should have the true equilibrium at zero, and not let the
# "negative" noise be positive!
exp().related_timeseries(seed=seed).noise(0.2).set2zero().deconvolve(100).combined_view(save="v7", show=show)
exp().related_timeseries(seed=seed).noise(0.2).deconvolve(100, scale_factor=10).combined_view(save="v8", show=show)
exp().related_timeseries(seed=seed).noise(0.2).deconvolve(2000, scale_factor=10).combined_view(save="v9", show=show)
exp().related_timeseries(seed=seed).noise(0.6).deconvolve(100, scale_factor=10).combined_view(save="v10", show=show)
```

![v6](https://github.com/engeir/hack-md-notes/raw/main/assets/pic/de-verify/v6.png)
![v7](https://github.com/engeir/hack-md-notes/raw/main/assets/pic/de-verify/v7.png)
![v8](https://github.com/engeir/hack-md-notes/raw/main/assets/pic/de-verify/v8.png)
![v9](https://github.com/engeir/hack-md-notes/raw/main/assets/pic/de-verify/v9.png)
![v10](https://github.com/engeir/hack-md-notes/raw/main/assets/pic/de-verify/v10.png)

## Vertical Adjustment

If we look more closely at what happens if we shift the time series along the
`y`-direction, we notice that it is really hard to get any good estimates from it.

**Make sure that the real equilibrium is at zero!** _(Easier said than done…)_

```python
# A simple vertical shift also complicates things!
exp().related_timeseries(seed=seed).vertical_shift((50, 278)).deconvolve(100).combined_view(save="v11", show=show)
exp().related_timeseries(seed=seed).vertical_shift((1, 1)).deconvolve(100).combined_view(save="v12", show=show)
exp().related_timeseries(seed=seed).vertical_shift((1, 1)).deconvolve(1000).combined_view(save="v13", show=show)
exp().related_timeseries(seed=seed).vertical_shift((1, 1)).deconvolve(1000, scale_factor=10).combined_view(save="v14", show=show)
exp().related_timeseries(seed=seed).vertical_shift((1, 1)).deconvolve(1000, cutoff=10).combined_view(save="v15", show=show)
```

![v11](https://github.com/engeir/hack-md-notes/raw/main/assets/pic/de-verify/v11.png)
![v12](https://github.com/engeir/hack-md-notes/raw/main/assets/pic/de-verify/v12.png)
![v13](https://github.com/engeir/hack-md-notes/raw/main/assets/pic/de-verify/v13.png)
![v14](https://github.com/engeir/hack-md-notes/raw/main/assets/pic/de-verify/v14.png)
![v15](https://github.com/engeir/hack-md-notes/raw/main/assets/pic/de-verify/v15.png)

## Scaling

Now, what about scaling the pure and clean time series? Both, or just one of them? That
is fine, luckily.

```python
exp().related_timeseries(seed=seed).scale(10).deconvolve().combined_view(save="v16", show=show)
exp().related_timeseries(seed=seed).scale((10, 100)).deconvolve().combined_view(save="v17", show=show)
exp().related_timeseries(seed=seed).scale((100, 35)).deconvolve(1000).combined_view(save="v18", show=show)
exp().related_timeseries(years=100, gamma=10, wide_forcing=True, seed=seed).scale((100, 35)).deconvolve(1000).combined_view(save="v19", show=show)
exp().related_timeseries(wide_forcing=True, seed=seed).scale((100, 35)).vertical_shift((1, 0)).deconvolve(1000).combined_view(save="v20", show=show)
exp().related_timeseries(wide_forcing=True, seed=seed).scale((100, 35)).vertical_shift((1, 1)).deconvolve(1000).combined_view(save="v21", show=show)
```

![v16](https://github.com/engeir/hack-md-notes/raw/main/assets/pic/de-verify/v16.png)
![v17](https://github.com/engeir/hack-md-notes/raw/main/assets/pic/de-verify/v17.png)
![v18](https://github.com/engeir/hack-md-notes/raw/main/assets/pic/de-verify/v18.png)
![v19](https://github.com/engeir/hack-md-notes/raw/main/assets/pic/de-verify/v19.png)
![v20](https://github.com/engeir/hack-md-notes/raw/main/assets/pic/de-verify/v20.png)
![v21](https://github.com/engeir/hack-md-notes/raw/main/assets/pic/de-verify/v21.png)

## Syncing Issues

Let us go back to forcing and temperature signals that themselves are not altered.
Instead, we make them be out of sync. In the below plots, the forcing shown and the
forcing used to generate the temperature from convolution of the response function are
almost identical. The difference is that the arrival times of the forcing used to
generate the temperature are shifted by one single index back, forward or nothing at all
with equal probability. This has a big effect on the estimated response function,
especially in the case where the forcing has a decay.

In the third plot, the forcing has no decay, but the shift between arrival times are set
to 100 indices (vs 1 above, where one index/step is one day), indicating how much harder
it is to deconvolve when the forcing has a shape to it rather than just an arrival time
and amplitude.

```python
exp().peripheral_timeseries(shift=1, seed=seed).deconvolve(1_000).combined_view(save="v22", show=show)
exp().peripheral_timeseries(shift=1, wide_forcing=True, seed=seed).deconvolve(1_000).combined_view(save="v23", show=show)
exp().peripheral_timeseries(shift=100, seed=seed).deconvolve(1_000).combined_view(save="v24", show=show)
```

![v22](https://github.com/engeir/hack-md-notes/raw/main/assets/pic/de-verify/v22.png)
![v23](https://github.com/engeir/hack-md-notes/raw/main/assets/pic/de-verify/v23.png)
![v24](https://github.com/engeir/hack-md-notes/raw/main/assets/pic/de-verify/v24.png)
