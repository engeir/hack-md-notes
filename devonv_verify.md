---
geometry: margin=3cm,top=3cm
---

# Deconvolution of CESM2 data

## Looking at raw data

The raw data, median over an ensemble of four simulations, one for each season. Overlaid
are Savitzky-Golay filters, but where the initial rise is swapped with a log func:

![Initial smoothing](https://raw.githubusercontent.com/engeir/state-of-art-volcanoes-in-climate/636abd85af0142d8f162aaa1636f567f5c020ede/pic/easy_smooth.png?token=GHSAT0AAAAAABWTVV7KLTMZ4CPQF55VM5KKYWQLUYA "Initial smoothing")

## Change tails

Now giving the forcing an exponentially decaying tail and the temperature a power law
tail:

![New tails](https://raw.githubusercontent.com/engeir/state-of-art-volcanoes-in-climate/636abd85af0142d8f162aaa1636f567f5c020ede/pic/extra_smooth.png?token=GHSAT0AAAAAABWTVV7KP2OAMAXPKIART6FEYWQLWPA "New tails")

## Extending the tails

Make the tails longer so that they (more or less) reach equilibrium (same as above, just
with longer exponential and power law tails):

![Extending the tails](https://raw.githubusercontent.com/engeir/state-of-art-volcanoes-in-climate/636abd85af0142d8f162aaa1636f567f5c020ede/pic/extrapolate.png?token=GHSAT0AAAAAABWTVV7L5QE3YG4HUOBWSL4MYWQLXFA "Extending the tails")

## Synthetic signal

Now, create a custom response signal, convolve with extended forcing above so it come
close to the extended temperature above:

![Extended forcing and temp, and new temp from convolving](https://raw.githubusercontent.com/engeir/state-of-art-volcanoes-in-climate/636abd85af0142d8f162aaa1636f567f5c020ede/pic/fake_signal.png?token=GHSAT0AAAAAABWTVV7LFWLKBTOVMY5DGEBAYWQLX4Q "Extended forcing and temp, and new temp from convolving")

![Custom response](https://raw.githubusercontent.com/engeir/state-of-art-volcanoes-in-climate/636abd85af0142d8f162aaa1636f567f5c020ede/pic/fake_signal_r.png?token=GHSAT0AAAAAABWTVV7KNWTYQHUDOCK5A5EOYWQLYJQ "Custom response")

<!-- \begin{figure}[!h] -->
<!-- \caption{Extended forcing and temp, and new temp from convolving with response (right)} -->
<!-- \end{figure} -->

## Adding noise

Adding some noise to the forcing and the temperature from convolution in fig.\ (4);
still too little noise on the forcing compared to the ogiginal in fig.\ (1):

![Additive noise to F and T in fig.\ (4)](https://raw.githubusercontent.com/engeir/state-of-art-volcanoes-in-climate/636abd85af0142d8f162aaa1636f567f5c020ede/pic/add_noise.png?token=GHSAT0AAAAAABWTVV7LDDS2QX63SDIBJ4JMYWQLY2A "Additive noise to F and T in fig. (4)")

And this is what the deconvolution gives back when feeding it the noisy forcing and the
custom response:

![Deconvolving F+N and R to give T estimate](https://raw.githubusercontent.com/engeir/state-of-art-volcanoes-in-climate/636abd85af0142d8f162aaa1636f567f5c020ede/pic/add_noise_deconv.png?token=GHSAT0AAAAAABWTVV7LWMZECPZP7RHNITWCYWQLZOA "Deconvolving F+N and R to give T estimate")

![Deconvolving F+N and R to give T estimate](https://raw.githubusercontent.com/engeir/state-of-art-volcanoes-in-climate/636abd85af0142d8f162aaa1636f567f5c020ede/pic/add_noise_deconv_clip.png?token=GHSAT0AAAAAABWTVV7KPMLMIGY3S4PYW3AUYWQLZ7A "Deconvolving F+N and R to give T estimate")

<!-- \begin{figure}[!h] -->
<!-- \caption{Deconvolving F+N and R to give T estimate} -->
<!-- \end{figure} -->

## Train of pulses

Now appending the forcing to itself six times, then convolving and adding noise to the
outputted temperature signal. The added noise to the forcing is now increased to better
match the noise we have in the original from finding the median.

![Train of pulses](https://raw.githubusercontent.com/engeir/state-of-art-volcanoes-in-climate/636abd85af0142d8f162aaa1636f567f5c020ede/pic/train_conv.png?token=GHSAT0AAAAAABWTVV7LA6PEEQDCC6FJPU4SYWQL2RA "Train of pulses")

![Train of pulses](https://raw.githubusercontent.com/engeir/state-of-art-volcanoes-in-climate/636abd85af0142d8f162aaa1636f567f5c020ede/pic/train_conv_clip.png?token=GHSAT0AAAAAABWTVV7KGFFJCEG62IZ2XHG6YWQL3GA "Train of pulses")

<!-- \begin{figure}[!h] -->
<!-- \caption{Train of pulses with additivie noise} -->
<!-- \end{figure} -->

From the deconvolution we now get something that very much has the same shape as the
original we are looking for:

![Train deconvolved](https://raw.githubusercontent.com/engeir/state-of-art-volcanoes-in-climate/636abd85af0142d8f162aaa1636f567f5c020ede/pic/train_conv_deconv.png?token=GHSAT0AAAAAABWTVV7KVQWOTLAIVR2P7OKGYWQL3UA "Train deconvolved")

![Train deconvolved](https://raw.githubusercontent.com/engeir/state-of-art-volcanoes-in-climate/636abd85af0142d8f162aaa1636f567f5c020ede/pic/train_conv_deconv_clip.png?token=GHSAT0AAAAAABWTVV7KJBT3JMHP4YKDIDS2YWQL37Q "Train deconvolved")

<!-- \begin{figure}[!h] -->
<!-- \caption{Deconvolving (T+N) and (F+N) to get an estimate of R, with original overlaid} -->
<!-- \end{figure} -->
