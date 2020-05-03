# DL012020
U4 project for UdeA Deep Learning course, second semester 2020

## Gender recognition through speech (Jaime Vergara - Luis F. Parra)

This project implements a model which detects the gender of a particular subject based on his/her waveform associated to his/her speech. The dataset consists in selected audios from the dataset “Common voice” from [kaggle](https://www.kaggle.com/mozillaorg/common-voice).  

Two main experiments were conducted: The first one consists on applying 2D convolutions over espectrograms and the second one consists in applying 1D convolutions over the raw speech signal. For both experiments a second was taken after the second second of each audio. This part of the audio was sampled at 48 kHz, using a window of 25 ms. long, with a step size of 10 ms.

#### Applying 2D convolutions over spectrograms

In this experiment, the input consists on 3 images of size 40x100. The first image is the spectrogram, the second and third images are the first and second derivatives from the spectrogram. This is similar to the feature extraction implemented in this [article](https://arxiv.org/pdf/1803.05427.pdf).

A model based on convolutional neural networks was built, with variations over the amount of units of the fully-connected layers. Also, batch normalization was implemented before the activation of the first convolutional layer. After some attemps with more complex models (4 convolutional layers and 2 fully connected layers), better results were obtained with simpler models (1 convolutional layer and 2 fully conected layers). Dropout is also implemented.

The notebook included in this repository collects the results of implementing 6 diferent models with variable size on the fully connected layers and the option of applying batch normalization after the first convolutional layer. Accuracies and loss are logged in tensorboard, and the best models in terms of validation accuracies are chosen and its results are shown.

![2D Conv. Architecture](https://github.com/jaimevt88/DL012020/blob/master/images/2d-2.png)
![2D Conv. Architecture - 2](https://github.com/jaimevt88/DL012020/blob/master/images/2d.png)

#### Applying 1D convolutions over raw audio signal

In this experiment the input consists on one vector of 48000 components, which is sampled from the raw audio signal. Here, different amount and filter sizes in the convolutional layer were explored in order to get better results. The best results were obtained when using a model with one convolutional layer with 40 filters of size 1800.

The notebook includes the results of implementing 6 diferent models with variable size on the fully connected layers and the option of applying batch normalization after the first convolutional layer.  

![1D Conv. Architecture](https://github.com/jaimevt88/DL012020/blob/master/images/1d.png)

#### Results

Simpler models (with less convolutional layers) worked better when doing gender detection tasks. 2D Convolutions seems to deliver better  performances than the ones obtained with 1D convolutions, this is probably due to the fact that both genders present  strong differences in the frequency domain.

A bigger amount of neurons in the fully-connected layers did not improve the performance in a significant way.

Batch Normalization improved the performance with more complex models (more convolutional layers). With simpler models, batch normalization did not provide any advantage. 



