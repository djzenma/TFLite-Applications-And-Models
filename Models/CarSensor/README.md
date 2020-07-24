# Vehicle Detector
This directory contains the trained TFLite models of the Mobile Accelerometer Car 12K dataset. The model predicts whether the user is in a vehicle or not depending on the accelerometer data.

## Table of Contents
*   [Quantization Options](https://github.com/djzenma/TFLite-Applications-And-Models/tree/master/Models/CarSensor#quantization-options)
*   [CNN Model](https://github.com/djzenma/TFLite-Applications-And-Models/tree/master/Models/CarSensor#cnn-model)
*   [Dataset](https://github.com/djzenma/TFLite-Applications-And-Models/tree/master/Models/CarSensor#dataset)
*   [Performance Analysis on Microcontrollers](https://github.com/djzenma/TFLite-Applications-And-Models/tree/master/Models/CarSensor#performanceanalysis-on-microcontrollers)

## Quantization Options
The different quantization options used are:

|Quantization Name| File| Weights Size (KB) | Accuracy (%)
|-----------------|-----|--------------|-------------|
|**Original Models**|
|Original Keras Model|[model.h5](https://github.com/djzenma/TFLite-Applications-And-Models/blob/master/Models/CarSensor/model.h5)| | 
|TFLite with no optimization|[no_quant.tflite](https://github.com/djzenma/TFLite-Applications-And-Models/blob/master/Models/CarSensor/no_quant.tflite)|  | 
|FLOAT 16|[float16.tflite](https://github.com/djzenma/TFLite-Applications-And-Models/blob/master/Models/CarSensor/float16.tflite)|  | 
|Dynamic Range (8-bit int)|[drange.tflite](https://github.com/djzenma/TFLite-Applications-And-Models/blob/master/Models/CarSensor/drange.tflite)|  | 
|||
|**Reduced Models**|
|Reduced Keras Model|[model_reduced.h5](https://github.com/djzenma/TFLite-Applications-And-Models/blob/master/Models/CarSensor/model_reduced.h5)| | 
|TFLite with no optimization|[reduced_no_quant.tflite](https://github.com/djzenma/TFLite-Applications-And-Models/blob/master/Models/CarSensor/reduced_no_quant.tflite)| 7.07 | 95.00
|FLOAT 16|[reduced_float16.tflite](https://github.com/djzenma/TFLite-Applications-And-Models/blob/master/Models/CarSensor/reduced_float16.tflite)| 3.54 | 95.00
|Dynamic Range (8-bit int)|[reduced_drange.tflite](https://github.com/djzenma/TFLite-Applications-And-Models/blob/master/Models/CarSensor/reduced_drange.tflite)| 2.57 | 95.00

The smallest model in terms of weights size is the dynamic range quantized model ([reduced_drange.tflite](https://github.com/djzenma/TFLite-Applications-And-Models/blob/master/Models/CarSensor/reduced_drange.tflite)) with a size of only **2.57 KB** and an accuracy of **95.00%**.

## CNN Model
The **original model** is:</br>
![Image of the original model](https://github.com/djzenma/TFLite-Applications-And-Models/blob/master/Models/CarSensor/original_model.png)

However, it was a bit big in terms of weight size (because there were too many layers ), so I reduced the model to be smaller in size. Here is the **reduced model**:</br>
![Image of the reduced model](https://github.com/djzenma/TFLite-Applications-And-Models/blob/master/Models/CarSensor/reduced_model.png)

### Model Reduction
The original model contained 3 Conv Blocs (Conv2D->MaxPooling2D), after reduction, 1 Conv block is removed. </br>
Also, I doubled the number of neurones at the Dense Layer.

## Dataset
The dataset can be found [here](https://www.kaggle.com/claudiobottari/mobile-accelerometer-car-12k).

## Performance Analysis on Microcontrollers
You can find the benchmarking of the performance of this model in the [Models_Analysis](https://github.com/djzenma/TFLite-Applications-And-Models/tree/master/Models_Analysis) directory.
