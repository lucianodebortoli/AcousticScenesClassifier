# Sound Scene Classifier

Luciano De Bortoli <br/>
National University of Tres de Febrero <br/>

## Dataset:

* TUT 2017
* TUT 2018

After a manual inspection, preprocessing is applied to the dataset audio files, consisting of filtering and sample cleaning.
Some classes from the datasets are selected and combined to form a new dataset called "COMBI".

<img src="images/combi.png">

## Descriptors

From each audio file, a Mel-scale spectrogram is extracted with 128 frequency components. <br/>
Each spectrogram has 128 time components representing 2.7 seconds of audio. <br/>
The spectrogram is obtained by computing an FFT every 1024 audio samples,
using Hanning windows of 2048 samples in size. <br/>

<img src="images/mels.png">  
Average Mel-scale spectrogram magnitudes per class  

## Model:

A CNN-based architecture is used for the classifier model.

<img src="images/model.png">

## Data Augmentation

During model training, each batch is modified to apply data augmentation processes to the spectrograms.
These processes consist of applying a random Butterworth-type filter, which showed improvements in performance.

<img src="images/augment.png">

## Training

The model is trained for 40 epochs, selecting the version with the best performance on validation data.

<img src="images/training.png">

## Evaluation

The model is evaluated using the BADB evaluation dataset, which consists of audio recordings from
different locations in Buenos Aires, using a single mobile device (Motorola G4).

<img src="images/confusion.png">

The results obtained with this BADB evaluation set differ from those obtained with the COMBI evaluation split,
showing that the model does not fully generalize across all sound scene classes. However,
its performance for classifying indoor home environments, cars, and buses stands out.

## Discussion

It is believed that the most important limitation lies in the training datasets, which show a strong bias toward
sound scenes recorded in European cities and a limited variety of mobile devices.

## DEMO

To perform a prediction on an audio signal using the classifier, run `predict.py` from a console.
Provide the path to the audio file (.wav) as an argument.
As output, an image is generated showing the model's predictions for each 2.7-second segment.
The model used for inference is `CNN.tflite`, which is the same file used in the Android app.

<img src="images/predict.png">
