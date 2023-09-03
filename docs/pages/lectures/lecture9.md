---
layout: lecture
title: Autoencoders, VAEs, and Generative Modeling
permalink: /lecture9/
---
This lecture takes a different path from previous topics in computer vision and instead focuses on **generative modeling**, which is the process of using ML to create new content. Image formats such as JPEG save space by compressing images using patterns. Compression is important because it requires some understanding about the data. They use Fourier transforms to determine which details are important in the image. We can take this further to considering compression algorithms for specific objects: making deeper assumptions about the objects and their structures.  

One technique that can be used is **Variational Autoencoders** (VAEs). An **autoencoder** takes an input and puts it through some layers until it reaches the **bottleneck layer/code/latent**. By making the network compress the image to the bottleneck size and still produce a similar output, we are forcing it to learn features of the image. The generative framework is: latent $z$ is sampled from prior $p(x)$. Then image $x$ is sampled from $p(x\|z)$. Analogy: z is to genes as x is to facial structure.  

**Variational autoencoders** allows us to average latent vectors and produce images that are merged in a meaningful way.  We want to force the latent space to be sensible, so we use probabilistic encoding: map the latent vector $z$ to some probability distribution $f(x)$. This forces nearby/similar latents to decode to the original image as well. In VAEs, instead of directly producing $z$ from $x$, we are instead outputting the parameters of some Gaussian distribution, then sampling $z$ from that Gaussian. The loss function for this network considers the difference between $x$ and $\hat{x}$, and also how much the output of the encoder looks like a Normal distribution.  

VAEs allow us to interpolate between images in a meaningful way, and generate new images by choosing a latent $z$ and decoding it.  You can't use backprop on these networks, but there are ways to get around it (which are very technical). Vector Quantized VAEs (VQ-VAEs) allow us to work with discrete non-continuous latents such as text, which is used in Natural Language Processing.  

**Vector quantization** finds a vector within a "codebook" closest to the input vector, similar to 1-NN algorithm. This is applied after sampling the Gaussian. The codebook is learned through another complicated loss formula, based on how similar the input and output images are and how close the vectors are to the codewords.  

Summary: Autoencoders take an input image, compress it, and output the same image. VAEs can create linear combinations of images by forcing the latent space to be a Gaussian distribution. For discrete setups, VQ-VAEs quantize the latent $z$ before decoding it.