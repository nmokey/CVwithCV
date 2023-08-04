---
layout: lecture
title: Object Detection
permalink: /lecture7/
---
- One possible way to output landmark detection is to output x and y coordinates of the feature (such as a nose).
- For localization, we can take it further to find the bounding box of the classified object, maybe through also outputting the width and height of the box.
- In order to train it, we can define the loss function as Intersection over Union (IoU), dividing how much space overlaps between boxes (desired and output) by the combined area of both boxes. Higher IoU means a better model.
- One step after classification + localization is object detection, where there may be multiple different objects in one image. 
- One possible method for object detection is **exhaustive search/sliding windows**, where we select many boxes of many sizes in the image and run classification networks on each box.
- However, this method is terrible because it's really slow and you may just skip over the object. One solution to this is an R-CNN network, which guesses likely bounding boxes and only running classification on those. 
- You can use classical segmentation to propose the boxes, because edges are likely to define object boundaries. We identify larger regions using a selective search algorithm, combining "similar regions." We run classification during each step.![[Pasted image 20230721201930.png]]
- R-CNN is still really slow. Instead of doing so many forward passes, we can make them faster by running convolutions on the image to generate a feature map. This extracts key information and runs classification on the feature map and not the image itself.
- YOLO (You Only Look Once) makes it even faster by replacing the entire pipeline with one convolutional network. The CNN outputs where the bounding boxes and the object classifications.![[Pasted image 20230721202538.png]]
- YOLO treats the image like a grid, and for every grid tile it runs a classification and outputs a bounding box of the object whose midpoint is there. However, the bounding box doesn't need to be contained in the grid tile.
- If multiple cells detect the same object, we use **non-max suppression** to avoid multiple bounding boxes for the same object. It picks the bounding box with the highest confidence.
- If multiple objects are in the same cell, we can have multiple classification vectors and use the fact that the objects have different bounding boxes to tell the network which object should be represented by which classification vector. (**anchor boxes**)
- YOLO is very fast, fully convolutional, matches R-CNN accuracy, and has output dimensions $S*S*B*(5+C)$ where S is the number of 16x16 cells, B is number of predictions per cell, and C is number of classes.  

Summary: For classification + localization, we can use a CNN to output the coordinates and bounding box dimensions of the object. However, object detection may have multiple objects to classify and localize, so we run classifications multiple times to identify them, and thus we need an efficient way to look through the image. The best way is YOLO, which uses one convolutional network to go through the image as a grid and outputs the bounding box of the object in each grid, and uses non-max suppression to avoid repeat boxes.