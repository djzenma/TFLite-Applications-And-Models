# Music Genre Classifier
This directory contains the trained TFLite models of the music classification dataset. The model predicts the genre of the music being played to the mic.

## Table of Contents
*   [Quantization Options](https://github.com/djzenma/TFLite-Applications-And-Models/tree/master/Models/MusicClassifier#quantization-options)
*   [CNN Model](https://github.com/djzenma/TFLite-Applications-And-Models/tree/master/Models/MusicClassifier#cnn-model)
*   [Dataset](https://github.com/djzenma/TFLite-Applications-And-Models/tree/master/Models/MusicClassifier#dataset)
*   [Performance Analysis on Microcontrollers](https://github.com/djzenma/TFLite-Applications-And-Models/tree/master/Models/MusicClassifier#performanceanalysis-on-microcontrollers)

## Quantization Options
The different quantization options used are:

|Quantization Name| File| Weights Size (KB) | Accuracy (%)
|-----------------|-----|--------------|-------------|
|TFLite with no optimization|[reduced_no_quant.tflite](https://github.com/djzenma/TFLite-Applications-And-Models/tree/master/Models/MusicClassifier/reduced_no_quant.tflite)| 159 | 88.45
|FLOAT 16|[reduced_float16.tflite](https://github.com/djzenma/TFLite-Applications-And-Models/tree/master/Models/MusicClassifier/reduced_float16.tflite)| 79.5 | 88.38
|Dynamic Range (8-bit int)|[reduced_drange.tflite](https://github.com/djzenma/TFLite-Applications-And-Models/tree/master/Models/MusicClassifier/reduced_drange.tflite)| 42 | 88.45

The smallest model in terms of weights size is the dynamic range quantized model ([drange.tflite](https://github.com/djzenma/TFLite-Applications-And-Models/tree/master/Models/MusicClassifier/drange.tflite)) with a size of only **42 KB** and an accuracy of **88.45%**.

## CNN Model
The **original model** is:</br>
![Image of the original model](https://github.com/djzenma/TFLite-Applications-And-Models/tree/master/Models/MusicClassifier/original_model.png)

However, it was too big in terms of weight size (because there were too many layers and neurones), so I reduced the model to be smaller in size. Here is the **reduced model**:</br>
![Image of the reduced model](https://github.com/djzenma/TFLite-Applications-And-Models/tree/master/Models/MusicClassifier/reduced_model.png)

## Dataset
The dataset can be found [here](https://www.kaggle.com/andradaolteanu/gtzan-dataset-music-genre-classification).

## Performance Analysis on Microcontrollers
You can find the benchmarking of the performance of this model in the [Models_Analysis](https://github.com/djzenma/TFLite-Applications-And-Models/tree/master/Models_Analysis) directory.
