---
layout: lecture
title: Diffusion Models
permalink: /lecture12/
---
The goal of generative machine learning networks is to learn the distribution of data $p_{data}(x)$. We generate new data from sampling from the learned distribution. Both VAEs and GANs are trying to minimize some value in order to generate good outputs. Unlike previous networks, which take one big step from the latent vector (random noise) to the output, diffusion networks take multiple small steps through a Markov chain to convert the base distribution to the target distribution.  

A diffusion network has two parts: the forward and reverse process:
- The forward process takes an image and gradually adds Gaussian noise to it.
- The reverse process aims to learn the de-noising process to iteratively undo the forward process.

In order to figure out the distribution to take steps in the reverse process, we can approximate it. For small enough forward steps, we can assume the reverse process step is a Gaussian distribution. Diffusion attempts to learn the parameters of this Gaussian using a variational lower bound loss. We are trying to minimize the $D_{KL}$ divergence between the actual and learned distributions. There is an equation that lets us predict the noise that was added at $t_0$ to get to $t_t$. This would allow us to subtract the noise and get the original image back.  

To train the model, first you add noise to an image, then jump to some $x_t$ timestep. You then pass the noisy image into the model to predict the noise that was added, then try to minimize the difference between that and the actual noise. Repeat until converged Once the model is trained, you can start with random noise and pass it into the model to subtract predicted noise to get a new image. In order to get noise of the same dimensions as the image, we can use a UNet from the segmentation lecture as the noise predictive model. Using a cosine noise schedule instead of a linear one makes it easier for the model to learn the reverse process.  

Similar to conditional GANs, we can also apply to this to diffusion by taking a pre-trained model, then injecting the gradients of a classifier model trained on noisy images during sampling (classifier guidance). Instead of doing all this, a better way is to do **classifier-free guidance** in which you train a conditional diffusion model by feeding the class directly into the diffusion process. Guided images tend to be higher quality, but they are also less varied.  

One popular metric to judge how good the generated images are is FID and sFID, which measure how good the images are. Lower values mean better outputs. GANs were state-of-the-art until diffusion networks started performing much better and generating higher quality images.  

**Latent Diffusion Models** avoid the issue of training on computationally expensive images by focusing only on the bits that describe the semantic and compositional information of an image. This can be done by first training perceptual compression models which remove high-level details and learn a latent space that represents the image, then performing diffusion *on the latent space*. DALL-E 2 is a powerful diffusion text-to-image model, and Imagen from google. Video diffusion is also possible as well, done by Facebook and Google. DreamFusion can generate 3d models from text using diffusion.  

Summary: