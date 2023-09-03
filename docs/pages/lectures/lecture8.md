---
layout: lecture
title: Semantic Segmentation
permalink: /lecture8/
---
**Segmentation** is a continuation of object detection, and is split into two types:
- Semantic segmentation says what type of object is at each pixel on the screen.
- Instance segmentation shows where specifically is each instance of each class in the image.

Segmentation is useful because we can identify which components/pixels go together. To approach segmentation, we can simply create connected "segments" by grouping pixels based on similarity criteria, such as intensity, color, texture, edge strength, etc.  

An extremely inefficient deep learning method is to use sliding windows to classify the center pixel of each window. A better way is to use convolutions end-to-end to compute all features at once. This approach is size-agnostic of the input (the convolutions do not change the dimensions of the output, maybe through padding). However, this can be extremely slow on high resolution images. We can fix this using **Fully Convolutional Nets (FCNs)** to downsample the image by increasing the stride of the convolutions, then upsampling at the end to predict for the whole image.  

One classical approach to upsampling the image at the end is **Bilinear Interpolation**: filling in new space between pixels linearly. However, we can upsample using a learned algorithm with **deconvolutions:** we pass the filter over the output (original) using the values of the input (smaller one). These improvements result in **UNet**, which also utilizes skip connections. This allows outputs from earlier layers to feed directly as input into later layers. To expand to instance segmentation, we can reuse faster R-CNN to propose potential segments, and add object mask prediction to learn object masks.  

Summary: Segmentation is like object detection but it also identifies the pixels of each object identified. There are two types: semantic just identifies what class each pixel is, whereas instance shows the location of each instance of the object classified. This can be done through end-to-end convolutions to detect features and learn object masks, and can be more efficient by downsampling throughout the convolutions then upsampling at the end.