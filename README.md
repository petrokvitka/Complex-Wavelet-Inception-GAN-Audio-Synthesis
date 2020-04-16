# Complex-Wavelet-Inception-GAN-Audio-Synthesis
This is a github project improving the learning representation of waveform signal such as audio.  
Our discussion focuses on the High Fidelity (HiFi) Audio Synthesis, which can be applied in various applications such as TTS and music generation. The previous works including Tacotron2, GANSynth, Wavenet have demonstrated high quality simulations of sound sources, which are nearly undistinguishable. However, in the field of HiFi music and/or HiFi speech synthesis, we are still interested in higher-resolution audio representation to push the modeling of fine-grained waveform signals even further. 
## Why is waveform data so intractable in general?
Through previous reports, we already know that waveform data can hardly be modelled by 1D convolutional layers or perceptron. The spectral properties of sounds are non-local, as waveform audio is a complex mixture of various fundamental waves and their harmonics. Unlike image, audio oscillates up and down, which reflects not only amplitude but also phase.
## Previous works are limited by STFT-spectrogram
Because the direct modeling of waveform data is tough, many studies choose to model intermediate spectrogram, a two-dimensional image-like time-frequency product of short time Fourier transform. In early 21 centuries, many studies have reported that the mel-scaled STFT spectrogram is the most effective representation for audio classification, which outperformed many other time-frequency analysis tools such as CQT, MFCC, CWT, etc. Just recently, deep learning audio syntheses have also demonstrated that mel-scaled spectrogram with advantages in seperating harmonics and adapting human ears have successfully brings about high-fidelity audio/speech synthesis. People have overcome the problems of audio reconstruction by IF learning (github.com/tensorflow/magenta/tree/master/magenta/models/gansynth), Phase Gradient Heap Integration (https://tifgan.github.io/#S-E), neural inverse transform (github.com/descriptinc/melgan-neurips) and Wavenet-based vocoder (https://github.com/NVIDIA/tacotron2).  
  
However, from the theory of signal processing, we know that STFT is not perfect. Short Time Fourier Transform imposes assumptions that are non-trivial in reality on audio. For example, STFT decomposes the time domain into many equal-length processes and assumes that each of them is stationary; however, due to Heisenberg Inequity, time and frequency resolutions face a trade-off. If the window is too narrow, it will lead to inaccurate analysis and poor frequency resolution. If the window is too wide, the time domain is not fine enough to cover enough information. For time-varying unsteady signals like audio, in general, small windows suit high frequencies and large windows suit low frequencies. However, the width and overlap rate of STFT windows is fixed, not flexible enough to model audio.  
  
On the other hand, wavelet transform replaces the infinite-length trigonometric function basis with a finite-length decaying orthogonal wavelet basis so that we can know the specfic location in the time domain without information redundancy. Moreover, while the Gibbs effect appeared in Fourier transform, Wavelet Transform can tackle mutation signals. Despite all these advantages, wavelet transform-based scalogram is not widely applied in machine hearing because the advantages of mel scaling seem more vital for audio fidelity. This reminds us that if we can carefully design a mel-filtered wavelet basis, we would simultaneously have multiple advantages of adapting to the mutation signal, breaking the time-frequency trade-off, and adpating to the human hearing.
## How is that Wavelet alleviates information redundancy?
In practice, we adopted the mel-scaled synchrosqueezed wavelet transform (MelWSST) that alikes empirical mode decomposition to replace STFT. This novel wavelet transform can accurately represent the time-frequency features of audio signals. As shown, the left figure denotes the STFT of a quadratic signal, and the right figure denotes the synchrosqueezed wavelet transform. It is not hard to see that WSST reduces energy emission to the minimum, unlike STFT that is much more fussy. This is very important as to seperate the foundamental and harmonic waves to better represent the audio time-frequency features.
![image](https://github.com/yingtaoluo/Complex-Wavelet-Inception-GAN-Audio-Synthesis/blob/master/stft.vs.wsst.png)  
## How does this mel-scaled scalogram look like?  
The proposed Mel-scaled scalogram can be viewed as a higher time-resolution time-frequency image. For example, while STFT transforms a (16000) shaped audio into (128x128) spectrogram, our method transforms it into (128x16000) scalogram, without time-domain "downscale" error. In CV, higher-resolution image synthesis improves the authenticity and quality of generated image. In machine hearing, we can also foresee that such an improvement can bring about a more perfect hearing experience.
## Author Affiliation Information (Temporarily)
Yingtao Luo, Siqi Sun, Kun He, et al., Huazhong University of Science and Technology, et al.
