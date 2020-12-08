ai_transfer_learning Repository
================================

Summary
-------

This repository provides scripts and training data to perform transfer learning with Tensorflow 2 on a mobilenet image detection model. The purpose is to use a model trained on image net and replace the classification layer with a new classifier that can detect if an image contains hotdogs or not. 

Information about the motivation can be found here :) https://www.youtube.com/watch?v=vIci3C4JkL0

Setup
-----
This flow is based on the The XMOS AIoT SDK.
See the `Getting Started Guide <https://github.com/xmos/aiot_sdk/blob/develop/documents/getting_started_guide.rst>`_ for instructions on installing and using the AI Toolchain Extensions.


Transfer leanring and testing
-----------------------------

The Jupyter Notebook transfer_learning_and_test.ipynb is dedicated to create the mobilenet model pre-trained on the imagenet dataset and then perform transfer learning using the images in the training_and_validation directory. 
The pre-trained model will effectively serve as a generic model of the visual world. With transfer learning we take advantage of these learned feature maps of the convolutional frontend and then train a new classifier on a custom image data set. 
Training only the final fully connected layer is a lot more efficient then training the whole network from scratch and produces a more accurate model by re-using what the convolutional frontend has learned from the whole Imagenet dataset.
Here is more information https://www.tensorflow.org/tutorials/images/transfer_learning

After the training step the new model is tested for accuracy using the images in the test_images directory.

The script will create (or update if it exists) the spreadsheet hyperparameter_tuning_autogen.xlsx showing the hyperparameters and the accuracies achieved for training, validation and test datasets.

Quantization and testing
------------------------
The Jupyter Notebook transfer_learning_and_test.ipynb is dedicated to perform quantisation of the floating point model. In the next step it will optimise the quantized model to use operators optimised for xCORE.ai. It saves both models to the quantized_models directory. It will run inference on the quantized models and the original floating point model and perform an accuracy comparison test. Images that are incorrectly classified will be shown to help the analysis.

The script will create (or update if it exists) the spreadsheet compare_float_and_quantized_models.xlsx showing some hyperparameters and the accuracies achieved for the floatig point model and the two quantized models.

Next steps
----------

The quantized models can be compiled and run on xCORE.ai. The corresponding example to use is located in the XMOS AIoT SDK folder examples/bare-metal/hotdog_not_hotdog. See the README.rst for details.




