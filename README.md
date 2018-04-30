## Here, you will find audio clips to augment this thesis.

Current quantitative metrics (e.g. signal-to-noise ratio) can be helpful in generally assessing the capabilities of an audio processing technique, when the ground truth is known. However, given the subjective nature of instrumental audio, being able to audition the results is often more useful.


### 1. Source-separation as Denoising
<audio controls> <source src="https://raw.githubusercontent.com/SvenShade/Thesis_Demo/master/source_sep_full.wav" type='audio/wav'></audio>
<audio controls> <source src="https://raw.githubusercontent.com/SvenShade/Thesis_Demo/master/source_sep_violin.wav" type='audio/wav'></audio>

### 2. Super-resolution as Spectral Inpainting
<audio controls> <source src="https://raw.githubusercontent.com/SvenShade/Thesis_Demo/master/paganini_lofi.wav" type='audio/wav'></audio>
<audio controls> <source src="https://raw.githubusercontent.com/SvenShade/Thesis_Demo/master/paganini_cGAN_bandavg.wav" type='audio/wav'></audio>
<audio controls> <source src="https://raw.githubusercontent.com/SvenShade/Thesis_Demo/master/paganini_cGAN_logcont.wav" type='audio/wav'></audio>
<audio controls> <source src="https://raw.githubusercontent.com/SvenShade/Thesis_Demo/master/paganini_WN_unguided.wav" type='audio/wav'></audio>
<audio controls> <source src="https://raw.githubusercontent.com/SvenShade/Thesis_Demo/master/paganini_WN_guidefactor30.wav" type='audio/wav'></audio>
<audio controls> <source src="https://raw.githubusercontent.com/SvenShade/Thesis_Demo/master/paganini_truth.wav" type='audio/wav'></audio>

### 3. Synthesis as Style Transfer Onto Harmonics

Here is the melody from the folk song, 'Scarborough Fair', as played by a sinewave generator.
These sinewaves include the fundamental as well as the first few harmonics, in order to provide structure for cGAN to translate.
<audio controls> <source src="https://raw.githubusercontent.com/SvenShade/Thesis_Demo/master/scarborough_H2R_harmonics.wav" type='audio/wav'></audio>
Here is the same harmonic track, with the violin 'style' applied:
<audio controls> <source src="https://raw.githubusercontent.com/SvenShade/Thesis_Demo/master/scarborough_H2R_enhance_bandavg.wav" type='audio/wav'></audio>
<audio controls> <source src="https://raw.githubusercontent.com/SvenShade/Thesis_Demo/master/scarborough_H2R_enhance_linreconst_logcontr.wav" type='audio/wav'></audio>

Easter egg...
<audio controls> <source src="https://raw.githubusercontent.com/SvenShade/Thesis_Demo/master/rick_harmonics.wav" type='audio/wav'></audio>
<audio controls> <source src="https://raw.githubusercontent.com/SvenShade/Thesis_Demo/master/rick_synth.wav" type='audio/wav'></audio>
