---
layout: lecture
title: Advanced CV Architectures
permalink: /lecture6/
--- 
AlexNet, VGG, and ResNet are 3 models that have been large contributions and milestonesto the field of CV.
The issue that ResNet tries to solve is that as more and more layers are added, the learning signal becomes weak due to vanishing gradients and the model struggles to learn anything. The solution is to keep information from previous stages (residuals) for future computations to learn the identity transform. ResNet is a deep model, and adding skip connections makes the identity easy to learn. Normalizing your data through **BatchNorm** can fix vanishing gradients, as well as residuals, in order to maintain the identity throughout the network. ResNet also uses **global average pooling**, which is designed to replace Fully Connected (FC) layers in CNNs. Instead of adding FC layers on feature maps, you take the average of each feature map and the resultant vector is put into Softmax.  

MobileNets reduces the number of parameters in a network by processing each channel separately, then combine them while retaining data from each channel. (**depthwise separable convolutions**)  

**Pointwise (1x1) convolutions** are the quickest way to increase or decrease the number of channels, which allows us to stack many filters. We can use them on a depthwise convolution to reduce the layers to 1. They are used to modify the number of channels but not the input size, and are used in VGG and InceptionNets.

This means MobileNet can have high accuracy with much fewer parameters and complexity. All of these different model architectures essentially just take a bunch of different building blocks and put them together in different ways.  