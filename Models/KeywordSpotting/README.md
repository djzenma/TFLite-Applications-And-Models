# Keyword Spotting
This directory contains the trained TFLite models of the Google Speech Commands dataset. The model wakes up (predicts 1) when the user says the wake word "on!" in the mic.

## Table of Contents
*   [Quantization Options](https://github.com/djzenma/TFLite-Applications-And-Models/tree/master/Models/KeywordSpotting#quantization-options)
*   [CNN Model](https://github.com/djzenma/TFLite-Applications-And-Models/tree/master/Models/KeywordSpotting#cnn-model)
*   [Dataset](https://github.com/djzenma/TFLite-Applications-And-Models/tree/master/Models/KeywordSpotting#dataset)
*   [Performance Analysis on Microcontrollers](https://github.com/djzenma/TFLite-Applications-And-Models/tree/master/Models/KeywordSpotting#performanceanalysis-on-microcontrollers)

## Quantization Options
The different quantization options used are:

|Quantization Name| File| Weights Size (KB) | Accuracy (%)
|-----------------|-----|--------------|-------------|
|**Original Models**|
|Original Keras Model|[wake_on_original.h5](https://github.com/djzenma/TFLite-Applications-And-Models/blob/master/Models/KeywordSpotting/wake_on_original.h5)| | 
|TFLite with no optimization|[no_quant.tflite](https://github.com/djzenma/TFLite-Applications-And-Models/blob/master/Models/KeywordSpotting/no_quant.tflite)|  | 
|FLOAT 16|[float16.tflite](https://github.com/djzenma/TFLite-Applications-And-Models/blob/master/Models/KeywordSpotting/float16.tflite)|  | 
|Dynamic Range (8-bit int)|[drange.tflite](https://github.com/djzenma/TFLite-Applications-And-Models/blob/master/Models/KeywordSpotting/drange.tflite)|  | 
|||
|**Reduced Models**|
|Reduced Keras Model|[wake_on_reduced.h5](https://github.com/djzenma/TFLite-Applications-And-Models/blob/master/Models/KeywordSpotting/wake_on_reduced.h5)| | 
|TFLite with no optimization|[reduced_no_quant.tflite](https://github.com/djzenma/TFLite-Applications-And-Models/blob/master/Models/KeywordSpotting/reduced_no_quant.tflite)| 21 | 98.42
|FLOAT 16|[reduced_float16.tflite](https://github.com/djzenma/TFLite-Applications-And-Models/blob/master/Models/KeywordSpotting/reduced_float16.tflite)| 10.5 | 98.42
|Dynamic Range (8-bit int)|[reduced_drange.tflite](https://github.com/djzenma/TFLite-Applications-And-Models/blob/master/Models/KeywordSpotting/reduced_drange.tflite)| 6.01 | 98.21

The smallest model in terms of weights size is the dynamic range quantized model ([reduced_drange.tflite](https://github.com/djzenma/TFLite-Applications-And-Models/blob/master/Models/KeywordSpotting/reduced_drange.tflite)) with a size of only **6.01 KB** and an accuracy of **98.21%**.

## CNN Model
The **original model** is:</br>
![Image of the original model](https://github.com/djzenma/TFLite-Applications-And-Models/blob/master/Models/KeywordSpotting/original_model.png)

However, it was too big in terms of weight size (because there were too many layers and neurones), so I reduced the model to be smaller in size. Here is the **reduced model**:</br>
![Image of the reduced model](https://github.com/djzenma/TFLite-Applications-And-Models/blob/master/Models/KeywordSpotting/reduced_model.png)

### Model Reduction
The original model contained 3 Conv Blocs (Conv2D->MaxPooling2D), after reduction, 1 Conv block is removed. </br>
Also, I halved the number of neurones at each Dense Layer.

## Dataset
The dataset can be found [here](https://storage.cloud.google.com/download.tensorflow.org/data/speech_commands_v0.02.tar.gz).

## Performance Analysis on Microcontrollers
You can find the benchmarking of the performance of this model in the [Models_Analysis](https://github.com/djzenma/TFLite-Applications-And-Models/tree/master/Models_Analysis) directory.
