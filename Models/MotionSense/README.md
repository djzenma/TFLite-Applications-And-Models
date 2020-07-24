# Motion Sense Classifier
This directory contains the trained TFLite models of the Motion Sense dataset. The model predicts the motion of the user, either: walking/jogging, standing/sitting, going upstairs/downstairs.

## Table of Contents
*   [Quantization Options](https://github.com/djzenma/TFLite-Applications-And-Models/tree/master/Models/MotionSense#quantization-options)
*   [CNN Model](https://github.com/efabless-ML-SoC/SoC-FPGA-ML/blob/master/MusicClassifier#cnn-model)
    -   [Stacking MaxPool Layers](https://github.com/djzenma/TFLite-Applications-And-Models/tree/master/Models/MotionSense#stacking-maxpool-layers)
*   [Dataset](https://github.com/djzenma/TFLite-Applications-And-Models/tree/master/Models/MotionSense#dataset)
*   [Performance Analysis on Microcontrollers](https://github.com/djzenma/TFLite-Applications-And-Models/tree/master/Models/MotionSense#performanceanalysis-on-microcontrollers)

## Quantization Options
The different quantization options used are:

|Quantization Name| File| Weights Size (KB) | Accuracy (%)|
|-----------------|-----|-------------------|-------------|
|**Original Models**|
|Original Keras Model|[model.h5](https://github.com/djzenma/TFLite-Applications-And-Models/blob/master/Models/MotionSense/model.h5)| | 97.436
|TFLite with no optimization|[no_quant.tflite](https://github.com/djzenma/TFLite-Applications-And-Models/blob/master/Models/MotionSense/no_quant.tflite)| 326 | 97.436
|FLOAT 16|[float16.tflite](https://github.com/djzenma/TFLite-Applications-And-Models/blob/master/Models/MotionSense/float16.tflite)| 163 | 97.436
|Dynamic Range (8-bit int)|[drange_fixed.tflite](https://github.com/djzenma/TFLite-Applications-And-Models/blob/master/Models/MotionSense/drange_fixed.tflite)| 94.8 | 97.436
|||
|**Reduced Models**|
|Reduced Keras Model|[reduced_model.h5](https://github.com/djzenma/TFLite-Applications-And-Models/blob/master/Models/MotionSense/reduced_model.h5)| | 92.31
|TFLite with no optimization|[reduced_no_quant.tflite](https://github.com/djzenma/TFLite-Applications-And-Models/blob/master/Models/MotionSense/reduced_no_quant.tflite)| 19.5 | 92.31
|FLOAT 16|[reduced_float16.tflite](https://github.com/djzenma/TFLite-Applications-And-Models/blob/master/Models/MotionSense/reduced_float16.tflite)| 9.76 | 92.31
|Dynamic Range (8-bit int)|[reduced_drange.tflite](https://github.com/djzenma/TFLite-Applications-And-Models/blob/master/Models/MotionSense/reduced_drange.tflite)| 6.02 | 92.31

The smallest model in terms of weights size is the dynamic range quantized reduced model ([reduced_drange.tflite](https://github.com/djzenma/TFLite-Applications-And-Models/tree/master/Models/MotionSense/reduced_drange_8.tflite)) with a size of only **6.02 KB** and an accuracy of **92.31%** !

## CNN Model
The **original model** is:</br>
![Image of the original model](https://github.com/djzenma/TFLite-Applications-And-Models/blob/master/Models/MotionSense/original_model.png)

However, it was too big in terms of weight size (because there were too many layers and neurones), so I reduced the model to be smaller in size. Here is the **reduced model**:</br>
![Image of the reduced model](https://github.com/djzenma/TFLite-Applications-And-Models/blob/master/Models/MotionSense/reduced_model.png)

### Stacking MaxPool Layers
Notice how in the reduced model, multiple **MaxPool2D** layers are stacked up over each other. The reason is that, because we only have 1 Conv Block, and when the output of this latter is flattened to the Dense Layers, the dimensions are too big. However, by adding MaxPool2D Layers, the dimensions are cut by half after every layer, hence reducing the number of weights and thus the memory requirements.

## Dataset
The dataset can be found [here](https://www.kaggle.com/malekzadeh/motionsense-dataset).

## Performance Analysis on Microcontrollers
You can find the benchmarking of the performance of this model in the [Models_Analysis](https://github.com/djzenma/TFLite-Applications-And-Models/tree/master/Models_Analysis) directory.
