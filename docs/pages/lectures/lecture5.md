---
layout: lecture
title: Intro to Computer Vision
permalink: /lecture5/
---
Computer vision is the field of AI that deals with extracting information from an image.
- *Classification* shows what an image is.
- *Localization* classifies the image but also puts a bounding box on the object.
- *Object detection* can classify multiple objects in an image and bounds them.
- *Image segmentation* detects multiple objects in an image and also shows their outlines.

The most basic model used in computer vision is a **convolutional neural network (CNN)**. When working with images, we can represent them as data (matrices). Grayscale images can just use 0-255 to represent each pixel. Color images uses 3 matrices stacked on each other for RGB, with each layer/color called a **channel**. The 3d matrix is referred to by a **tensor**. It has 3 channels, one for each color.  

CNNs are useful because we can avoid requiring way too many parameters, and because it doesn't make sense to treat each individual pixel as a "feature." We can instead focus on local regions of an image rather than individual pixels. Deep learning is also the process of extracting hierarchal representations of an input, from general features to specific (edges, colors, textures)  

The concept of **translational equivariance** says that if you translate (move) the pixels of an object, you should also translate its representations. **Invariance to translation** says that the semantic meaning of the image does not change due to a translation.  

**Convolutions**: instead of processing an entire image at once, we can process patches instead. Each patch is processed by a layer parameterized by the same weights and biases (weight sharing), which preserves translational equivariance and invariance. A convolution takes an image and slides a kernel/weight filter (a smaller matrix) over it and takes dot products between the kernel and image patch along the way. This ensures that we are looking at local patches of the image, and we are preserving translational equivariance and invariance by using the same weight filter for each patch.  

Different weight filters can be designed for different features, such as edge detection or sharpening/blurring the image. Since this is deep learning, we can make the model learn the weight filters, which serve as the feature extractors. The process of convolutions can be generalized for 3d images by making the weight filter also be 3D.  

The output of a convolution is a **feature/activation map**. If we have $n$ feature detectors/filters, we will get $n$ activation maps. These can be stacked into a tensor, similar to the depth of RGB tensors. Convolutions: input tensor of CxHxW, convolved with F filters of CxKxK, and output tensor FxH'xW'.  

A **receptive field** is the region of the original input image that each element of the activation map is influenced by/looks at. Too small RF can miss important info, but too large RF can cause overfitting. Two 3x3 convolutions has the same RF of one 5x5 convolutions but having stacked convolutions has more non-linearities (like ReLU) and less parameters. You can also speed up increasing the receptive field throughout the model with **pooling layers,** which reduces the dimensions of the activation max by taking the max/average element in patches of the input.  

**Padding** (like from css) allows us to preserve the height and width of the output activation map as the input by adding extra padding elements around the input image. *Valid* padding refers to no padding, and *same* padding has padding.  

**Stride** is the amount of pixels that the weight filter slides during the convolution. Has a similar effect to pooling layers. The output dimension of the activation map is given by $ceil[(W-F+2P/S)/S]+1$ where W is the input dimension, F is the filter size, P is the padding size, and S is the stride.  

Backprop with convolutions is similar to the regular backprop algorithm, and can also be done through PyTorch command `torch.nn.Conv2d()`. The final layer should be for classification/processing of the final convolution features. We flatten the last convolution output and pass it into an MLP (multilayer perceptron). There are usually established architectures for CNNs which involve stacking convolutions with pooling to get a smaller representation of the input, which is then flattened. Images should be normalized during preprocessing from 0-255 to 0-1 to prevent gradients from exploding.  

You can also artificially create more data from a single image by flipping or adjusting it, which is called **data augmentation**. It is important to periodically save your CNN model (maybe through TensorFlow) as it is training so that you don't lose everything.  

Summary: A convolutional neural network is a model that is great for CV because it allows us to look at local batches of an image at once instead of going pixel by pixel. It is similar to a neural network but each layer is usually convolutional or pooling. A convolutional layer has parameters such as stride, padding, and kernel size. Pooling layers can quickly shrink features without too much information loss, and can take the max or average of each patch. The image tensor is passed through these as its dimensions are shrunk. The final step, classification layers, flatten or pool the output before passing it to an MLP, which has the most parameters.