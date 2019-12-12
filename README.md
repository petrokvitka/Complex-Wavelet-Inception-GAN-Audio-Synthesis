# Complex-Wavelet-Inception-GAN-Audio-Synthesis
This is a github project of an unpublished manuscript improving the quality of unsupervised audio synthesis.
## Why is waveform data so intractable?
The waveform data can hardly be modelled by convolutional neural network or fully connected layers. The reason is that, firstly, waveform data such as optical spectrum or audio signal is a complex mixture of various waves; secondly, unlike image, audio oscillates up and down, which reflects not only amplitude but also phase. It is impossible to extract audio features effectively by the ordinary convolutional kernels. In computer vision, adjacent pixels do not oscillate back and forth fiercely like in audio synthesis, but change rather smoothly.  
  
Because the direct modeling of waveform data is tough, many studies choose to model the intermediate spectrogram, a two-dimensional image-like product of short time Fourier transform. However, spectrogram is still different from images, because the horizontal axis means time and the vertical axis means frequency. A minor translation could cause little difference in vision as the object does not change, but it makes huge difference in hearing. Also, as the human hearing is very sensitive, even tiny little noise may cause uncomfortable experience to ears. The current unsupervised audio generation is limited by effective reconstruction of fine structure of wave. An advanced modeling approach is needed for computer hearing and optical spectrum analysis.
## Previous works have not proposed an effective learning representation on waveform.
The adversarial audio synthesis first started from the work of Chris Donahua et al.(https://github.com/chrisdonahue/wavegan).  
Following studies used various strategies to further improve the fidelity of generated audio, such as Phase Gradient Heap Integration introduced by  
Andr´es Maraﬁoti et al.(https://tifgan.github.io/#S-E),  
IF-Phase learning proposed by Jesse Engel et al.(github.com/tensorflow/magenta/tree/master/magenta/models/gansynth),  
inverse transform of Melspectrogram to raw wave audio (https://github.com/descriptinc/melgan-neurips), etc.   
  
Their studies contributed a lot to improve the fidelity of audio, but were only focused on the learning of spectrogram.  
We used different original approaches including complex-valued convolution, wavelet transform, and inception generator to improve the direct modeling of fine structure of waveform.
## Solution1. Complex-valued convolution for complex spectrogram
The learning representation of complex spectrogram can avoid scattering the information of phase. The complex spectrogram, however, can hardly be processed by real-valued neural network. Introducing the architecture of DEEP COMPLEX NETWORKS (Chiheb Trabelsi et al.), we learned complex spectrogram directly.
## Solution2. Wavelet transform to replace short time Fourier Transform
The short time Fourier Transform is not flexible enough to filter audio features at different frequency scales. This is not a significant improvement in experiments, since the major problems are the quality of generation and phase recovery.
## Solution3. Inception generator to capture features at different frequency scales
Inspired by wavelet transform and inception network, we designed a generator architecture that provides convolution filters of flexible sizes to capture audio features at different frequency scales. Audio signal is a mixture of various foundamental waves and harmonic waves. Different foundamental waves are at different frequency ranges, and their harmonic waves are at their multiple frequencies. All these together are too complicated and twisted for a single-sized convolution to process. Therefore, we proposed to use multi-sized filters to generate waveform audio signal at first layer, just like an inversed version inception network. This modification can boost the quality of generated audio drastically, following the direction of WaveGAN, without generating the intermediate spectrogram.
## What is next?
We are working in progress to experiment and aggregate the findings to impress the academia with a significantly valuable contribution. Although the variable-length kernel sizes have boosted performance by a considerable margin experimentally, further experiments and mathematical explanation in the article is still required. 
## Author Information
Yingtao Luo, Siqi Sun, Kun He, Huazhong University of Science and Technology
