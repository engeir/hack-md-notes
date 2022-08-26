---
tags: Showcase, Notes
geometry: margin=3cm,top=3cm
---

# GCM Temperature Decay Times

[![hackmd-github-sync-badge](https://hackmd.io/j4L-EIhRQqGdl5KmiIZ-_w/badge)](https://hackmd.io/@engeir/S1XVyfNC5)
[![view-on-github](https://img.shields.io/badge/View%20on-GitHub-yellowgreen)](https://github.com/engeir/hack-md-notes/blob/main/gcm_temperature_dacay.md)

## Raw data

The below plot is showing a control run, three different single-event runs with
differently sized volcanic forcing, and a double-event run where the two volcanoes are
both of the same size as the middle single-event volcano.

![Raw surface air reference temperature for a control run, single-event runs and a
double-event
run](https://raw.githubusercontent.com/engeir/hack-md-notes/fa58e16e7d510e15ffe8a589ad09984fb795e327/assets/pic/gcm-temperature-decay/temperature-decay-raw.png
"Raw surface air reference temperature for a control run, single-event runs and a
double-event run")

Let us have a different look at this where we average over each year:

![Yearly averaged surface air reference temperature for a control run, single-event runs
and a double-event
run](https://raw.githubusercontent.com/engeir/hack-md-notes/fa58e16e7d510e15ffe8a589ad09984fb795e327/assets/pic/gcm-temperature-decay/temperature-decay-avg.png
"Yearly averaged surface air reference temperature for a control run, single-event runs
and a double-event run")

The temperature clearly do not revert to equilibrium for the medium and large volcanoes,
even a decade after the volcanic eruption.

## Forcing size

Let us further compare the size of the volcanic forcing to some historical eruptions,
just to get a feel for the likelihood of them happening or if they are completely
unrealistic.

The below show _total aerosol optical depth in visible band_ corresponding to the
simulations above.

![Forcing represented by the variable AEROD_v corresponding to the above temperature
plot](https://raw.githubusercontent.com/engeir/hack-md-notes/9b9a0c0ec490b45097cd861e0a9b876363b9d11d/assets/pic/gcm-temperature-decay/temperature-decay-aerod_v.png
"Forcing represented by the variable AEROD_v corresponding to the above temperature
plot")

## Comparing to historical eruptions

| Eruption Name      |    AEROD_v     |     SO2 [Tg]     |
| :----------------- | :------------: | :--------------: |
| Control            |      0.0       |        0         |
| Medium             |      0.3       |       26.1       |
| Medium-plus        |      3.5       |       400        |
| Strong             |       12       |      1629.4      |
| Mt. Pinatubo       |    ~0.1[^1]    |    14-20[^2]     |
| Yellowstone        | ~10[^3]^,^[^4] | ~1000[^3]^,^[^4] |
| Youngest Toba Tuff |      ---       |   ~5400[^ytt]    |

The smallest eruption (medium) is comparable in size to the Mt. Pinatubo eruption and as
such a very realistic scenario. The two larger eruptions of $400\,\mathrm{Tg}$ and
$1629.4\,\mathrm{Tg}$ SO~2~ are not unrealistic from a historical perspective, the
eruption in Yellowstone about $150000$ years ago was similar in size, and the Youngest
Toba Tuff eruption has an estimated sulphur dioxide amount of 5.8 billion tonnes[^ytt],
but also from $10$ to $360$ time Mount Pinatubo[^5]. Whether the climate model can deal
with such perturbations realistically, as it should with Pinatubo-like eruptions, is
more uncertain.

_[GCM]: General Circulation Model
_[AEROD_v]: total aerosol optical depth in visible band

[^1]:
    Toohey, M., Stevens, B., et al. (2016), Easy Volcanic Aerosol (EVA v1.0): An
    idealized forcing generator for climate simulations.

[^2]:
    Ollila, A. (2016), Climate Sensitivity Parameter in the Test of the Mount Pinatubo
    Eruption.

[^3]:
    About 100 times Mt. Pinatubo.
    [https://bg.copernicus.org/preprints/9/8693/2012/bgd-9-8693-2012.pdf](https://bg.copernicus.org/preprints/9/8693/2012/bgd-9-8693-2012.pdf)

[^4]:
    Timmreck, C., Graf, H-F., et al. (2010), Aerosol size confines climate response to
    volcanic super-eruptions.

[^ytt]: https://en.wikipedia.org/wiki/Toba_catastrophe_theory#Volcanic_winter_and_global_cooling_computer_models
