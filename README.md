# Machine Learning on Embedded Systems
TFLite applications: Optimized .tflite models (i.e. lightweight and low latency), tips and tricks to optimize your model and to make it require only about 6KB of memory, and code to run directly on your Microcontroller!

This repo is composed of the following:

|Directory| Description|
|---------|------------|
|Benchmarking_Tool | Tool to benchmark & analyze any TFLite model in terms of: <ul><li>Latency</li><li>Accuracy</li><li>Number of Weights</li><li>Weights memory size</li><li>Tensors Used</li><li>Every Tensor's memory allocation</li></ul>|
|Models_Analysis    | Benchmark of the TFLite models mentionned below in excel sheets|
|Models/MotionSense| TF Models, with different options of quantization, infering depending on the data of grabbed from the accelerometer whether you are going: <ul><li>upstairs/downstairs</li><li>walking/jogging</li><li>standing/sitting</li></ul>|
|Models/MusicClassifier| TF Models, with different options of quantization, predicting one of the following music genres being played via the microphone: <ul><li>Blues</li><li>Classical</li><li>Country</li><li>Disco</li><li>Hip Hop</li><li>Jazz</li><li>Metal</li><li>Pop</li><li>Reggae</li><li>Rock</li></ul>|
|Models/KeywordSpotting| TF Models, with different options of quantization, predicting whether you are saying the wake word "on!" to the microphone |
|Models/CarSensor| TF Models, with different options of quantization, predicting whether you are riding a vehicle or not, depending on the data of the accelerometer|

------------

|Model|Weights Size (KB)|Accuracy (%)|
|-----|-------------|-------|
|MotionSense|6.02|92.31|
|MusicClassifier|42|88.45|
|KeywordSpotting|6.01|98.21|
|CarSensor|2.57|95.00|
------------


## Model Reduction (Optimization) Methodology
### Building Blocks
All of the applications mentionned above are time series data, and therefore CNN architectures were suitable for all of them. Most CNNs have kind of a similar structure as this one below: </br>
Input Layer -> (Conv -> MaxPoolingxPi)xN -> (Dense Layer -> Regularizor)xM -> Output Layer </br>

where N = Number of Conv Blocks, M =  Number of Dense Blocks, Pi = Number of Pooling Layers in the ith Conv Block. </br>

An important trick in reducing the number of weights in a CNN is adding Pooling Layers as it outputs half the number of its input weights.

Now that we have our building blocks, we can define our optimization algorithm.

### Algorithm

Optimizing the CNN network can be done by reducing N and M, and varying Pi of every ith Conv Block until we are satisfied with a good compromise of accuracy and weights size values. In fact, applying a search algorithm on these 2 hyperparameters while having as score the accuracy of the network and the weights size leads to the reduced optimized model. The final part is to find a good loss function to feed to the search algorithm for it to minimize it. For now a weighted average of both accuracy and weights size will do the job, but it might be subject to improvement.
