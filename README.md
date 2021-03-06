**If you want to know more, I've written [an article](https://nicolasracchi.com/blog/digit-recognition) on my blog about this project!**

# Digit Recognizer
A Python implementation of the popular MNIST dataset application of Digit Recognition with Convolutional Neural Networks

This project was made to demonstrate a Python implementation of web inference capability.
The network was trained on the MNIST database in Jupyter Notebook with the Keras library with Tensorflow backend. The recognition error on the test data set is 0.75% after 12 epochs, without hyperparameter tuning. The convolutional neural network I used is an 8-layer Sequential model.


## Installation

```bash
# clone repo
git clone https://github.com/nicolas-racchi/digit_recognizer && cd digit_recognizer/flask_3

# If you're using MacOS/Linux:
export FLASK_APP=recognition.py

# If you're using Windors:
set FLASK_APP=recognition.py

# (Optional): create a virtual environment
virtualenv venv

# install and run
pip install -r requirements.txt
flask run
```

## How it works:

The neural network was trained on the MNIST dataset in a Jupyter Notebook in Python, using ADAM, an algorithm for first-order gradient-based optimization of stochastic objective functions, based on adaptive estimates of lower-order moments.
The loss function choosen was categorical crossentropy, since there are 10 classes.
The network itself is an 8 layer sequential model, which has 784 input units (28x28 resolution grayscale images, normalized to values ranging from [-1: 1]). The network structure is as follows:
							
  * 2 Convolutional layers with rectified linear unit activation
  * A Pooling layer to choose the best features of the digits
  * A Dropout layer to improve convergence
  * A Flatten layer since there are too many dimensions and we need only 10 classes
  * A Dense layer, fully connected, to get all relevant data
  * A second Dropout layer
  * A Dense layer with softmax activation to squash the matrix into output probabilities

Using this training method I was able to obtain 99.25% test accuracy after only 12 epochs, without hyperparameter tuning, so there is still room for improvement.
The training process took 16 seconds per epoch on a GRID 520 GPU.

### Preprocessing

When you draw an image in the canvas, you are writing into a 280x280px area. The preprocessing is needed so that the output of the canvas is as similar as possible to the training data, in order to not loose accuracy.
First of all, the image is converted in a base64 string, then its colors are inverted so that the majority of the canvas is black (this makes it easier for the classifier); finally, it is resized to 28x28px, the same as the training data.


### Notes on Deploying
Originally I had deployed this project on Google Cloud and mapped it to my personal domain, but after several months I have decided that it's not worth keeping it online as far as costs are concerned, for now.
