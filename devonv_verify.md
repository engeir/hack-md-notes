---
geometry: margin=3cm,top=3cm
---

# Deconvolution of CESM2 data

## Looking at raw data

The raw data, median over an ensemble of four simulations, one for each season. Overlaid
are Savitzky-Golay filters, where the rise is swapped with a log func:

![Initial smoothing](./pic/easy_smooth.png)

## Change tails

Now giving the forcing an exponentially decaying tail and the temperature a power law
tail:

![New tails](./pic/extra_smooth.png)

## Extending the tails

Make the tails longer so that they (more or less) reach equilibrium (same as above, just
with longer exponential and power law tails):

![Extending the tails](./pic/extrapolate.png)

## Synthetic signal

Now, create a custom response signal, convolve with extended forcing above so it come
close to the extended temperature above:

![Extended forcing and temp, and new temp from convolving](./pic/fake_signal.png)
![Custom response](./pic/fake_signal_r.png)
\begin{figure}[!h]
\caption{Extended forcing and temp, and new temp from convolving with response (right)}
\end{figure}

## Adding noise

Adding some noise to the forcing and the temperature from convolution in fig.\ (4);
still too little noise on the forcing compared to the ogiginal in fig.\ (1):

![Additive noise to F and T in fig.\ (4)](./pic/add_noise.png)

And this is what the deconvolution gives back when feeding it the noisy forcing and the
custom response:

![Deconvolving F+N and R to give T estimate](./pic/add_noise_deconv.png)
![Deconvolving F+N and R to give T estimate](./pic/add_noise_deconv_clip.png)
\begin{figure}[!h]
\caption{Deconvolving F+N and R to give T estimate}
\end{figure}

## Train of pulses

Now appending the forcing to itself six times, then convolving and adding noise to the
outputted temperature signal. The added noise to the forcing is now increased to better
match the noise we have in the original from finding the median.

![Train of pulses](./pic/train_conv.png)
![Train of pulses](./pic/train_conv_clip.png)
\begin{figure}[!h]
\caption{Train of pulses with additivie noise}
\end{figure}

From the deconvolution we now get something that very much has the same shape as the
original we are looking for:

![Train deconvolved](./pic/train_conv_deconv.png)
![Train deconvolved](./pic/train_conv_deconv_clip.png)
\begin{figure}[!h]
\caption{Deconvolving (T+N) and (F+N) to get an estimate of R, with original overlaid}
\end{figure}
