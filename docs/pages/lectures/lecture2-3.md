---
layout: lecture
title: Intro to Deep Learning
permalink: /lecture2-3/
---
- The dot product of two vectors is repeated multiplication between each element and adding at the end.![[Pasted image 20230717170423.png]]
- Matrix-vector multiplication is repeated vector dot products between the rows of W and vector x. (stacked dot products)
- ![[Pasted image 20230717171427.png]]
- For vector functions, x is an input vector, y is a label vector, and W, b, and theta are parameters. W for a matrix, b for a vector, and theta for general.
- If a function outputs scalars, you can take the derivative of the output with respect to a component of the input vector (also a scalar).
- Motivation of neural networks: can tackle non-linear tasks like regression and imitate the human brain (universal function approximator)
- the **perceptron** is the mathematical approximation of a neuron, which takes in many weighted inputs and takes the sum, then activate with a step function (ReLU function).
- The $w_{0}$ term is the bias value (b)![[Pasted image 20230717183407.png]]
- This can be compressed as the dot product between a weight vector and input vector plus a bias: $b+\bar{w} \intercal \bar{x}$.
- So the perceptron function is $$f(\bar{x}, \bar{w}, b) = ReLU(b+\bar{w} \intercal \bar{x})$$.
- A **[[Neural Network]]** stacks and cascades perceptrons. Each stack is called a layer, and the middle layers are called hidden layers. Each layer takes inputs and weighs and sums them according to the perceptron function.
- A layer of perceptrons is a vector where each row is the equation of a different perceptron.![[Pasted image 20230717184527.png]]
- Each perceptron in the layer can be compacted further: The whole perceptron function  becomes $f(\bar{x}, \bar{w}, b) = ReLU(W\bar{x}+\bar{b})$. This is done by each perceptron in the layer, and each layer step is called a **forward pass**. (x is input, w is weights, and b is the bias)
- **Softmax** ensures that an output can be interpreted as a probability by making sure all outputs sum to 1, and are in the range \[0,1]. 
- A [[loss function]] is a metric of how good the network is, and is low when our outputs are good. they must be differentiable (you take the derivative of the loss with respect to inputs).
	- A common loss function is Mean Squared Error: take the difference between output and actual vectors, square each difference, and sum them.
	- It outputs a scalar value and is also a differentiable function.
- [[Gradient descent]] takes the negative of the gradient vector (steepest upwards slope at a point) to find the local minima of the loss function.
- The gradient is a partial derivative of the output (Loss function) with respect to inputs (parameters).
- We can choose arbitrary parameters (weights and biases) then use gradient descent to start minimizing our loss function.
- The gradient step size is scaled by a factor $\lambda$ to prevent us from stepping too far.
- We can define the true loss to be the mean loss across *all* training examples, then minimze that for our model.
- Batch gradient descent looks at chunks of the dataset instead of the whole thing and uses it as an approximator for the entire dataset.
- Question: why is a function like ReLU necessary to keep the step function complex?
- Back-propagation allows us to, instead of redoing multiplication for the loss of each layer, work from the end of the network to the front and save values as we go along.
- There are some optimizers for gradient descent: Momentum, RMSProp, and Adam.
	- Momentum ensures that a random local minima doesn't halt our descent by adding the weighted average of previous gradients to the current gradient. (ball rolling down a hill)
	- RMSProp stores a weighted average of the components of the previous gradient squared instead of all past gradients (like a moving average). Similar to momentum
	- Adam is the **best optimizer** because it combines both. It keeps 2 moving averages: one for gradients and one for squared gradient components and gets the benefits of both Momentum and RMSProp.
- BatchNorm normalizes our neuron outputs throughout the network and gives us nicer gradients.
- Ensembling is when you make many different models with random parameters and averaging the predictions, but requires lots of computation and gives little performance.
- Dropout is when you randomly set a bunch of neurons to zero, so the model has to learn how to use different combinations of neurons. This gives us the same effect of ensembling.
- Skip connections allows us to build arbitrarily deep networks because we can just pass good information (once our classification is done) to the end of the model.
- PyTorch uses Numpy can calculate the derivatives of functions at a certain value, so it can be used for backprop and gradient descent.  

Summary: A neural network is made of many layers of neurons which each take in an input vector, calculate a weighted sum using its own weight vector and adds a bias, then passes it on to the next layer, which eventually produces output. The output can be normalized to represent a probability using Softmax, and the results can be assessed with a loss function (produces a scalar). Gradient descent is used to optimize the parameters (weights and biases) in order to minimize the loss, and can be made better using optimizers such as Adam. 