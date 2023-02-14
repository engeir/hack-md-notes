---
tags: Showcase, Notes
lang: en-GB
---

# Convolve forcing with made-up responses

[![hackmd-github-sync-badge](https://hackmd.io/j4L-EIhRQqGdl5KmiIZ-_w/badge)](https://hackmd.io/@engeir/ByJm9tCno)
[![view-on-github](https://img.shields.io/badge/View%20on-GitHub-yellowgreen)](https://github.com/engeir/hack-md-notes/blob/main/convolve-forcing-comparison.md)

Here, we want to create a response function from a functional form and convolve it with
different forcing alternatives that we get from CESM2.

## Forcing

The forcing alternatives are

1. Total aerosol optical depth in visible band (AOD)
2. Total injected SO2 aerosols (Injection)
3. Radiation imbalance at the top of the atmosphere (Imbalance)

The figure below shows the three alternatives scaled to have similar maximum amplitudes.

![Forcing alternatives,
medium](https://raw.githubusercontent.com/engeir/hack-md-notes/600b766e13a589d9ef67821931f3b03f89f995ee/assets/pic/convolve-forcing-comparison/forcing-convolution-forcings-medium.png
"Forcing alternatives, medium")

![Forcing alternatives,
medium-plus](https://raw.githubusercontent.com/engeir/hack-md-notes/600b766e13a589d9ef67821931f3b03f89f995ee/assets/pic/convolve-forcing-comparison/forcing-convolution-forcings-medium-plus.png
"Forcing alternatives, medium-plus")

![Forcing alternatives,
strong](https://raw.githubusercontent.com/engeir/hack-md-notes/600b766e13a589d9ef67821931f3b03f89f995ee/assets/pic/convolve-forcing-comparison/forcing-convolution-forcings-strong.png
"Forcing alternatives, strong")

![Forcing alternatives, strong, with a log-lin
axis](https://raw.githubusercontent.com/engeir/hack-md-notes/6f220e7/assets/pic/convolve-forcing-comparison/forcing-convolution-forcings-strong-semilogy.png
"Forcing alternatives, strong, with a log-lin axis")

## Response

We create two different response functions; one with exponential decay and one with
algebraic decay. Specifically, we define them in python as

```python
res[mid:] = np.exp(-tau[mid:] / 4)
res[mid:] = (tau[mid:] + 1) ** (-1.1)
```

Values before `mid` are all zeros and `tau[mid] == 0`.

## Results

Let us look at the case where the volcano was at its strongest. This is the simulation
that has the longest run, covering 1850 to 1874.

From the plots below, we find the exponential decay to be a worse fit when convolved
with all forcing time series. The algebraically decaying response function performs well
with the radiation imbalance forcing.

![Strong
eruption](https://raw.githubusercontent.com/engeir/hack-md-notes/d4abc883db5243f4ee4130fd529e88727c0dd7ad/assets/pic/convolve-forcing-comparison/forcing-convolution-algebraic-strong.png
"Strong eruption")

![Strong
eruption](https://raw.githubusercontent.com/engeir/hack-md-notes/d4abc883db5243f4ee4130fd529e88727c0dd7ad/assets/pic/convolve-forcing-comparison/forcing-convolution-exponential-strong.png
"Strong eruption")

During the first six years, there are only small differences between convolving with an
algebraic vs. exponential function, but after this, the algebraic outperforms the other.

This is the case with the medium-sized eruption as well, that the algebraic decay fit
better than the exponential.

![Medium
eruption](https://raw.githubusercontent.com/engeir/hack-md-notes/d4abc883db5243f4ee4130fd529e88727c0dd7ad/assets/pic/convolve-forcing-comparison/forcing-convolution-algebraic-medium-plus.png
"Medium eruption")

![Medium
eruption](https://raw.githubusercontent.com/engeir/hack-md-notes/d4abc883db5243f4ee4130fd529e88727c0dd7ad/assets/pic/convolve-forcing-comparison/forcing-convolution-exponential-medium-plus.png
"Medium eruption")

In the last example, with a small eruption, the amount of noise in the temperature
signal makes it hard to draw any real conclusion about which is better. Both the
algebraic and the exponential decay work well.

![Weak
eruption](https://raw.githubusercontent.com/engeir/hack-md-notes/d4abc883db5243f4ee4130fd529e88727c0dd7ad/assets/pic/convolve-forcing-comparison/forcing-convolution-algebraic-medium.png
"Weak eruption")

![Weak
eruption](https://raw.githubusercontent.com/engeir/hack-md-notes/d4abc883db5243f4ee4130fd529e88727c0dd7ad/assets/pic/convolve-forcing-comparison/forcing-convolution-exponential-medium.png
"Weak eruption")
