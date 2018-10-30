## Here, you will find spectrograms and audio clips to augment our paper.

Quantitative metrics can be helpful in generally assessing the capabilities of an audio processing technique, when the ground truth is known. However, given the subjective nature of instrumental audio, being able to audition the results is often more useful.

In our paper, we highlight analogous image tasks to each MIR task. To recap:

1. Source-separation becomes a denoising problem, reconstructing frequencies related to the signal and ignoring others. 

2. Super-resolution is analogous to inpainting, where the blank half of a spectrogram is filled by considering the first half (the low frequencies) and prior knowledge.

3. Synthesis becomes a style transfer problem, where the model has extracted the overall harmonic ‘style’ of an instrument, and seeks to apply this to sine-waves serving as a harmonic blueprint

4. Pitchtracking can be thought of as semantic segmentation in the same way that a satellite image might be translated into a road map. 

We introduce two pipelines to achieve this, shown below. The top details GAN-S, which uses a secondary cGAN stage to aid reconstruction, while the bottom details GAN-WN.
![Pipelines](https://raw.githubusercontent.com/SvenShade/Thesis_Demo/master/pipeline.png)

Below is an example linear spectrogram, restored using the secondary cGAN. From left to right: descaled spectrogram, restoration, ground truth.
![Reconst](https://raw.githubusercontent.com/SvenShade/Thesis_Demo/master/GAN-S_reconst.jpg)

Given the subjective nature of the first three tasks, we provide an audio demonstration of each below.

### 1. Source-separation as Denoising
We start with a recording of a piano and violin duet, playing a phrase from Bach.
<audio controls> <source src="https://raw.githubusercontent.com/SvenShade/Thesis_Demo/master/source_sep_full.wav" type='audio/wav'></audio>
Following the top pipeline from the above figure, our process looks for frequencies specific to the violin, and attempts to silence the piano.
<audio controls> <source src="https://raw.githubusercontent.com/SvenShade/Thesis_Demo/master/source_sep_violin.wav" type='audio/wav'></audio>
Another example from the same piece.
<audio controls> <source src="https://raw.githubusercontent.com/SvenShade/Thesis_Demo/master/SS-ref.wav" type='audio/wav'></audio>
Now, our CNN baseline has a go at isolating the violin.
<audio controls> <source src="https://raw.githubusercontent.com/SvenShade/Thesis_Demo/master/SS-CNN.wav" type='audio/wav'></audio>
The result from our method. It introduces a different sort of artefact, losing high-frequency fidelity primarily due to the lossy spectrogram reconstruction process. Yet, notice the piano source is much better attenuated.
<audio controls> <source src="https://raw.githubusercontent.com/SvenShade/Thesis_Demo/master/SS-cGAN-Secx2.wav" type='audio/wav'></audio>

Below, we give a closer look at source-separation, with a ground-truth difference overlay. Alignments with ground truth are cyan. Areas where ground truth is missed are red. Interference (piano) is white. Observe cGAN's precision in removing interference, sometimes at the cost of detail.
![Pipelines](https://raw.githubusercontent.com/SvenShade/Thesis_Demo/master/overlay.jpg)

### 2. Super-resolution as Spectral Inpainting
We start with a violin phrase by Paganini, at a sample rate of 4kHz (ultra low-fidelity).
<audio controls> <source src="https://raw.githubusercontent.com/SvenShade/Thesis_Demo/master/paganini_lofi.wav" type='audio/wav'></audio>
Here's the result of our method.
<audio controls> <source src="https://raw.githubusercontent.com/SvenShade/Thesis_Demo/master/paganini_bandavg-plus-logcont.wav" type='audio/wav'></audio>
This is the ground truth.
<audio controls> <source src="https://raw.githubusercontent.com/SvenShade/Thesis_Demo/master/paganini_truth.wav" type='audio/wav'></audio>
Another example. This time, from Chopin. Here is the lofi clip:
<audio controls> <source src="https://raw.githubusercontent.com/SvenShade/Thesis_Demo/master/chopin-lofi-clip.mp3" type='audio/mp3'></audio>
Here is the baseline performance (linear interpolation):
<audio controls> <source src="https://raw.githubusercontent.com/SvenShade/Thesis_Demo/master/chopin-lin-clip.mp3" type='audio/mp3'></audio>
Here is the result of our cGAN process.
<audio controls> <source src="https://raw.githubusercontent.com/SvenShade/Thesis_Demo/master/chopin-LC-clip.mp3" type='audio/mp3'></audio>
Ground truth.
<audio controls> <source src="https://raw.githubusercontent.com/SvenShade/Thesis_Demo/master/chopin-gt-clip.mp3" type='audio/mp3'></audio>

Alternatively, we can use a Wavenet to reconstruct the raw audio directly from the Mel-spectrogram (see the lower pipeline in the figure from before). This kind of modelling proved to be highly resource intensive, with training taking over a fortnight to see convergence on our NVIDIA GTX1080ti. Despite lacking the memory necessary to train a sufficiently complex model, the concept is there.
<audio controls> <source src="https://raw.githubusercontent.com/SvenShade/Thesis_Demo/master/paganini_WN_guidefactor30.wav" type='audio/wav'></audio>
We can further improve the output of our unstable Wavenet. Instead of conditioning Wavenet on the spectrogram alone, we also feed in the timesteps of the original, lofi audio. At every step, we now take the average of both original audio and Wavenet's prediction (weighted towards the former). This can be thought of as a sort of teacher-forcing generation. As usual, that timestep becomes part of the series, and in turn influences future predictions. Here, we apply this to our Chopin clip.
<audio controls> <source src="https://raw.githubusercontent.com/SvenShade/Thesis_Demo/master/lofi-WN-20-iter1.wav" type='audio/wav'></audio>


### 3. Synthesis as Style Transfer Onto Harmonics

Here is the melody from the folk song, 'Scarborough Fair', as played by a sinewave generator.
These sinewaves include the fundamental as well as the first few harmonics, in order to provide structure for cGAN to translate.
<audio controls> <source src="https://raw.githubusercontent.com/SvenShade/Thesis_Demo/master/scarborough_H2R_harmonics.wav" type='audio/wav'></audio>
Here is the same harmonic track, with the violin 'style' applied:
<audio controls> <source src="https://raw.githubusercontent.com/SvenShade/Thesis_Demo/master/scarborough_H2R_enhance_linreconst_logcontr.wav" type='audio/wav'></audio>

Finally, we leave the reader with the first 7 notes of the chorus of Rick Astley's "Never Gonna Give You Up", as played by a sinewave generator.
<audio controls> <source src="https://raw.githubusercontent.com/SvenShade/Thesis_Demo/master/rick_harmonics.wav" type='audio/wav'></audio>
Here is the result of our method, applying violin stylisation :)
<audio controls> <source src="https://raw.githubusercontent.com/SvenShade/Thesis_Demo/master/rick_synth.wav" type='audio/wav'></audio>
