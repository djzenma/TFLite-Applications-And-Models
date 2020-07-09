# Machine Learning on Embedded Systems
TFLite applications: Optimized .tflite models (i.e. lightweight and low latency), tips and tricks to optimize your model and to make it require only about 6KB of memory, and code to run directly on your Microcontroller!

This repo is composed of the following:

|Directory| Description|
|---------|------------|
|Benchmarking_Tool | Tool to benchmark & analyze any TFLite model in terms of: <ul><li>Latency</li><li>Accuracy</li><li>Number of Weights</li><li>Weights memory size</li><li>Tensors Used</li><li>Every Tensor's memory allocation</li></ul>|
|Models_Analysis    | Benchmark of the TFLite MotionSense & Music Classifer models in excel sheets|
|Models/MotionSense| TF Models, with different options of quantization, infering whether you are going upstairs/downstairs, walking/jogging, or walking/sitting depending on the data of grabbed from an accelerometer|
|Models/MusicClassifier| TF Models, with different options of quantization, infering the genre of the music being played to the microphone|