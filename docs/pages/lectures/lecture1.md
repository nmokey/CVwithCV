---
layout: lecture
title: Intro to Machine Learning
permalink: /lecture1/
---
Machine learning is a **paradigm*** of approximating a function from data. Instead of programming a function ourselves to generate output (which is what you do in traditional programming), we give machine learning models output so it can generate a function! Think of ML as template creation - we are loosely defining a function, but leaving some parameters to learn from the data that dictate the behavior of the function.  

The form our function takes is the "class" of the model. The parts of the function we are allowed to learn are **parameters**. There are 3 main types of learning:
- **Supervised learning** - Task driven for regression/classification
- **Unsupervised learning** - Data driven (clustering)
- **Reinforcement** - learns to react to an environment

In ML models, you may see the terms **parameters, weights, and biases**, but they all mean the same thing. A **hyperparameter** is a special parameter which we tell the model, like the model size, class, training procedure. These usually have to be tuned by hand, and aren't learned by the model.
*ML pipeline*: define problem -> prepare data -> define model and loss function -> minimize the loss function (training)  

It is important to note that all data, even images and audio, is always represented by numbers, usually represented in vectors (1d matrix). One way we can represent outputs of a model is a **one-hot vector**. A one-hot vector is a way to represent data/labels where it just corresponds to a 1 in a vector, eg. $[0, 0, 1, 0, 0]$  

It's also important that we have a way to objectively tell how well a model is performing. Results are standardized across different models by using common training datasets such as MNIST. When assessing a model, there are a couple things to consider:
- **Bias** - tendency towards certain predictions, usually from lower complexity models 
- **Variance** - ability to match the spread of the data (needs to be both firm and flexible)
- **Overfitting** occurs when the model becomes too tuned to the training data and performs poorly on holdout data
- **Underfitting** occurs when training data performs similarly to holdout data. 

*\*Paradigm: A certain approach to solving a problem*