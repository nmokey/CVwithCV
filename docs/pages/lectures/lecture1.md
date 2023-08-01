---
layout: lecture
title: Intro to Machine Learning
permalink: /lecture1/
---
- Machine learning is a **paradigm** of approximating a function from data
- Instead of programming a function ourselves to generate output, we give machine learning output so it can generate a function
- Think of ML as template creation - define a function but leave some parameters to learn from the data that dictate the behavior of the function
- The form our function takes is the "class" of the model. The parts of the function we are allowed to learn are "parameters."
	- **Supervised learning** - Task driven for regression/classification
	- **Unsupervised learning** - Data driven (clustering)
	- **Reinforcement** - learns to react to an environment
- Parameters/weights/biases denote parameters in ML models
- A hyperparameter is a non-learned parameter like model size, class, training procedure.
- *ML pipeline*: define problem -> prepare data -> define model and loss function -> minimize the loss function (training)
- Data is always represented by numbers and is usually represented in vectors (1d matrix).
- A one-hot vector is a way to represent data/labels where it just corresponds to a 1 in a vector, eg. \[0, 0, 1, 0, 0]
- Results are standardized across different models by using common training datasets such as MNIST
- Bias - tendency towards certain predictions, usually from lower complexity models 
- Variance - ability to match the spread of the data (needs to be both firm and flexible)
- Overfitting occurs when the model becomes too tuned to the training data and performs poorly on holdout data
- Underfitting occurs when training data performs similarly to holdout data. 