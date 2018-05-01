## Here, you will find audio clips to augment this thesis.

Current quantitative metrics (e.g. signal-to-noise ratio) can be helpful in generally assessing the capabilities of an audio processing technique, when the ground truth is known. However, given the subjective nature of instrumental audio, being able to audition the results is often more useful.


### 1. Source-separation as Denoising
We start with a recording of a piano and violin duet, playing a phrase from Bach.
<audio controls> <source src="https://raw.githubusercontent.com/SvenShade/Thesis_Demo/master/source_sep_full.wav" type='audio/wav'></audio>
We then apply the STFT to obtain a spectrogram, Mel-scale the frequencies, and apply the generator of our cGAN convolutionally. Finally, we reconstruct audio from this spectrogram, by rescaling the frequencies and performing Griffin-Lim reconstruction:
<audio controls> <source src="https://raw.githubusercontent.com/SvenShade/Thesis_Demo/master/source_sep_violin.wav" type='audio/wav'></audio>

### 2. Super-resolution as Spectral Inpainting
First, the Paganini violin phrase, at a sample rate of 4kHz (ultra low-fidelity).
<audio controls> <source src="https://raw.githubusercontent.com/SvenShade/Thesis_Demo/master/paganini_lofi.wav" type='audio/wav'></audio>
Then, after cGAN has performed inpainting on the lost (higher) frequencies, we reconstruct the audio.
<audio controls> <source src="https://raw.githubusercontent.com/SvenShade/Thesis_Demo/master/paganini_cGAN_bandavg.wav" type='audio/wav'></audio>
Here's the audio after a second cGAN has tried to restore detail from the lossy reconstruction process.
<audio controls> <source src="https://raw.githubusercontent.com/SvenShade/Thesis_Demo/master/paganini_bandavg-plus-logcont.wav" type='audio/wav'></audio>
Alternatively, we can use a Wavenet to reconstruct the raw audio directly from the Mel-spectrogram. However, this kind of modelling proved to be too resource intensive, taking over a fortnight to see convergence on our NVIDIA GTX1080ti, with less pleasant results than Griffin-Lim. Despite lacking the memory necessary to train a sufficiently complex model, the concept is there.
<audio controls> <source src="https://raw.githubusercontent.com/SvenShade/Thesis_Demo/master/paganini_WN_guidefactor30.wav" type='audio/wav'></audio>
This is the ground truth.
<audio controls> <source src="https://raw.githubusercontent.com/SvenShade/Thesis_Demo/master/paganini_truth.wav" type='audio/wav'></audio>
Another example. This time, from Chopin. Here is the lofi clip:
<audio controls> <source src="https://raw.githubusercontent.com/SvenShade/Thesis_Demo/master/chopin-lofi-clip.mp3" type='audio/mp3'></audio>
Here is baseline performance (linear interpolation):
<audio controls> <source src="https://raw.githubusercontent.com/SvenShade/Thesis_Demo/master/chopin-lin-clip.mp3" type='audio/mp3'></audio>
Here is the result of our cGAN process.
<audio controls> <source src="https://raw.githubusercontent.com/SvenShade/Thesis_Demo/master/chopin-LC-clip.mp3" type='audio/mp3'></audio>
Ground truth.
<audio controls> <source src="https://raw.githubusercontent.com/SvenShade/Thesis_Demo/master/chopin-gt-clip.mp3" type='audio/mp3'></audio>

### 3. Synthesis as Style Transfer Onto Harmonics

Here is the melody from the folk song, 'Scarborough Fair', as played by a sinewave generator.
These sinewaves include the fundamental as well as the first few harmonics, in order to provide structure for cGAN to translate.
<audio controls> <source src="https://raw.githubusercontent.com/SvenShade/Thesis_Demo/master/scarborough_H2R_harmonics.wav" type='audio/wav'></audio>
Here is the same harmonic track, with the violin 'style' applied:
<audio controls> <source src="https://raw.githubusercontent.com/SvenShade/Thesis_Demo/master/scarborough_H2R_enhance_linreconst_logcontr.wav" type='audio/wav'></audio>

Easter egg...
<audio controls> <source src="https://raw.githubusercontent.com/SvenShade/Thesis_Demo/master/rick_harmonics.wav" type='audio/wav'></audio>
<audio controls> <source src="https://raw.githubusercontent.com/SvenShade/Thesis_Demo/master/rick_synth.wav" type='audio/wav'></audio>
