# Diffusion Probabilistic Models

This repository provides a reference implementation of the method described in the paper:<br>
> Sohl-Dickstein, Jascha and Weiss, Eric A. and Maheswaranathan, Niru and Ganguli, Surya.<br>
> Deep Unsupervised Learning using Nonequilibrium Thermodynamics.<br>
> International Conference on Machine Learning. 2015<br>
> http://arxiv.org/abs/1503.03585

From the abstract: 
The essential idea behind the algorithm, inspired by non-equilibrium statistical physics, is to systematically and slowly destroy structure in a data distribution through an iterative forward diffusion process. 
We then train a reverse diffusion process that restores structure in data, yielding a highly flexible and tractable generative model of the data. 
This approach allows us to rapidly learn, sample from, and evaluate probabilities in deep generative models with thousands of layers or time steps, as well as to compute conditional and posterior probabilities under the learned model. 

## Using the Software

In order to train a diffusion probabilistic model on MNIST, simply install dependencies (see below), and then run
``python train.py``.

### Dependencies

1. Install `Blocks` and dependencies following [these instructions](http://blocks.readthedocs.org/en/latest/setup.html)
2. Setup `Fuel` and download MNIST following [these instructions](https://github.com/mila-udem/fuel/blob/master/docs/built_in_datasets.rst).

### Output

The objective function being minimized is the bound on the negative log likelihood in bits per pixel, minus the negative log likelihood under an identity-covariance Gaussian model. That is, it is the negative of the number in the final column in Table 1 in the paper.

Logging information is printed to the terminal once per training epoch, including the current value of the objective on the training set.

Figures showing samples from the model, parameters, gradients, and training progress are also output periodically (every 25 epochs by default -- see ``train.py``).

The samples from the model are of three types -- standard samples, samples inpainting the left half of masked images, and samples denoising images with Gaussian noise added (by default, the signal-to-noise ratio is 1). This demonstrate the straightforward way in which inpainting, denoising, and sampling from a posterior in general can be performed using this framework. 
Here is what samples look like after 825 training epochs 
<img src="https://github.com/Sohl-Dickstein/Diffusion-Probabilistic-Models/blob/master/samples-_t0000_epoch0825.png" width="500">

## Miscellaneous

**Multi-scale convolution** - As described in the paper, multi-scale convolutional layers were used when applying this algorithm to large images. This is not yet included in this implementation. I am in the process of implementing multi-scale convolutional layers in Blocks, so this should be available soon.

**Different nonlinearities** - In the paper, we used soft ReLU units in the convolutional layers, and tanh units in the dense layers. In this implementation, I used leaky ReLU units everywhere. 

**Original source code** - This repository is a thorough re-factoring of the code used to run the experiments in the published paper. In the name of reproducibility, if you email me a request I am willing to share the original source code. It is uncommented and made significantly out of metaphorical duct tape though. For almost any application, you will be much better off using the reference implementation provided here.

**Contact** - I would love to hear from you. Let me know what goes right/wrong! <jascha@stanford.edu>
