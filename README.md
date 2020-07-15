# Machine Learning on Embedded Systems
TFLite applications: Optimized .tflite models (i.e. lightweight and low latency), tips and tricks to optimize your model and to make it require only about 6KB of memory, and code to run directly on your Microcontroller!

This repo is composed of the following:

|Directory| Description|
|---------|------------|
|Benchmarking_Tool | Tool to benchmark & analyze any TFLite model in terms of: <ul><li>Latency</li><li>Accuracy</li><li>Number of Weights</li><li>Weights memory size</li><li>Tensors Used</li><li>Every Tensor's memory allocation</li></ul>|
|Models_Analysis    | Benchmark of the TFLite MotionSense & Music Classifer models in excel sheets|
|Models/MotionSense| TF Models, with different options of quantization, infering depending on the data of grabbed from the accelerometer whether you are going: <ul><li>upstairs/downstairs</li><li>walking/jogging</li><li>walking/sitting</li></ul>|
|Models/MusicClassifier| TF Models, with different options of quantization, predicting one of the following music genres being played via the microphone: <ul><li>Blues</li><li>Classical</li><li>Country</li><li>Disco</li><li>Hip Hop</li><li>Jazz</li><li>Metal</li><li>Pop</li><li>Reggae</li><li>Rock</li></ul>|
|Models/KeywordSpotting| TF Models, with different options of quantization, predicting whether you are saying the wake word "on!" to the microphone |
|Models/CarSensor| TF Models, with different options of quantization, predicting whether you are riding a vehicle or not, depending on the data of the accelerometer|