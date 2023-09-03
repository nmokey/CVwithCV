---
layout: lecture
title: Pretraining and Augmentations
permalink: /lecture4/
---
The classical machine learning pipeline: take in an input x, feature extraction of features $\phi$, pass into model $f(\phi, \theta)$, to predict an output y. However, to make feature extractors automatic instead of handwritten, you can learn the feature extractor using deep learning.  

A **convolutional layer** can extract features from an image, and has parameters that can be learned instead of prewritten. A **deep neural network** combines feature extraction and output prediction to streamline the entire process and have it completely automated (learned from the data). Deep learning is **representation learning**, since features are a way to represent what the input is supposed to look like.  

Each layer of the neural network is a learned feature extractor, and you can chain the layers together. They are hierarchal: later representations are more abstract than earlier ones. The motivation for transfer learning is that models don't have to learn from scratch every time they do something new, so we can use pre-trained models.  

We can transfer knowledge by classifiers to networks for other tasks. The old task is the pretext task, and the new task is the downstream task (such as computer vision, natural language processing, etc.) We can do this by taking certain earlier layers from the pretrained network and keeping them for the next model, which is called **freezing layers**.
Instead of freezing from pretrained networks, we can train it more to fine-tune it for the new model. Freezing vs fine-tuning is determined by the similarity of the datasets and the sizes.  

An **embedding** is the output of a map from some (discrete or continuous) space to a different continuous space. They can represent complex data. A **latent space** captures a lower-dimensional structure of high dimensional data which aims to encode all meaningful information required to represent it. (data can be embedded in a latent space.)  

Pretrained networks are good because they tend to be trained on massive datasets, and embeddings can be pre-computed and stored instead of using original high-dimensional data.
- In *unsupervised learning*, there are no labels to guide the model's learning. (usually clustering tasks)
- *Self-supervised learning* has the model create labels from raw data and then train in a supervised manner. It creates labels by hiding parts of input and predicting it. SSL can be used for image orientation, word prediction, waveforms, etc.  

Summary: The difference between classical machine learning and deep learning is that deep learning allows feature detection to also be learned, and thus combines the processes of feature detection and classification. The network can learn a representation of the input by passing it through convolutional layers, which are feature detectors that learn a feature of th eimage in a hierarchal order. Models can be built off of pretrained models by fine-tuning to the specific task or by freezing early layers of the pretrained model to make it easier to do a new task. 