# TFLite Model Benchmarking
This tool is meant to analyze and Benchmark a given TensorFlow Lite (TFLite) model with respect to its timing and space requirements.

## Workflow: Criteria & Tools
To analyze a TFLite model, we will benchmark it by the following attributes:
*   Latency
*   Accuracy
*   Number of Weights
*   Weights memory size
*   Tensors Used
*   Every Tensor's memory allocation

To measure the above attributes we will use the following open-source tools:

*   [Netron](https://github.com/lutzroeder/netron): visualizes the model's architecture. It is useful for debugging the converted TFLite model to know every component of the original model (e.g. keras) has been mapped to its lightweight TFLite counterpart.
*   [TF Benchmark Tool](https://github.com/tensorflow/tensorflow/tree/master/tensorflow/lite/tools/benchmark): This tool is found in the tensorflow repo and is used to estimate the model's latency by measuring the initialization time, 1st inference time, average warmup time, average inference time.
*   [tflite_analyzer](https://github.com/PeteBlackerThe3rd/tflite_analyser): This tool estimates the memory requirements of the model, i.e. the Number of weights, their memory size, the name of the tensors used, and their dynamic memory allocation.
*   TFLite Python Interpreter: Finally, we will measure the accuracy of our model using the python TFLite Interpreter.



## Unsupported Operations
Your original model (before converting to TFLite) might be using operations (ops) that are not supported yet by TFLite, i.e. not the built in [TFLite ops](https://www.tensorflow.org/lite/guide/ops_compatibility). These unsupported ops fall under 1 of 2 categories: [Select Ops](https://www.tensorflow.org/lite/guide/ops_select) or [Custom Ops](https://www.tensorflow.org/lite/guide/ops_custom). If you are using one of them, then your converted TFLite model will not be lightweight because it didn't optimize these operations.

[**Select Ops**](https://www.tensorflow.org/lite/guide/ops_select) are ops that are supported by TF but not yet by TFLite (keep in mind that it is still in the experimental phase) and [**Custom Ops**](https://www.tensorflow.org/lite/guide/ops_custom) are ops that you implemented yourself (and not built in in TF). To find out if your model uses one of the select ops, you can either visit the [documentation](https://www.tensorflow.org/lite/guide/ops_compatibility) of TFLite where they have a list of all of their built in ops, or you can find out during the conversion process to TFLite. To clarify this latter option, when you are converting your model to TFLite, if the model converts successfully without the following line:

```
converter.target_spec.supported_ops = [tf.lite.OpsSet.SELECT_TF_OPS]
```
then your model does not use any Select Ops. If an error occurs, try putting this line, if it converts then you are using a Select Op. If it doesn't convert both ways, then you are most probably using a Custom Op.

To know how to convert a model with Select Ops and for further details on Select Ops, refer to TF's [documentation](https://www.tensorflow.org/lite/guide/ops_select).

To know how to convert a model with Custom Ops and for further details on Custom Ops, refer to TF's [documentation](https://www.tensorflow.org/lite/guide/ops_custom).

### Example of a SELECT operation
This example was found empirically and I don't think that it is mentionned anywhere in the TF documentation. It is the `data_format` attribute found in the `tf.keras.layers.Conv2D` component. If you are using it then remove it (the default is the `channels_last` option) and don't overwrite the default to `channels_first`. This way, your model will be optimized.