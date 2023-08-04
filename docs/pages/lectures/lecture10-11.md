---
layout: lecture
title: Generative Adversarial Networks (GANs)
permalink: /lecture10-11/
---
- For high dimensional outputs such as sentences or images, it can be hard to judge how good our model is using a loss function, so we can just have another network judge how realistic our outputs are for us.
- The GAN game: one network is generating data, and another has to guess whether it is real or fake. The only way for the generator to win is to make data that looks real. (game theory concept)![[Pasted image 20230725152838.png]]
- When the discriminator classifies the generated data, we can use the loss to backpropagate to the generator's weights.
- To train a GAN, you take a batch of real and generated data and alternate between updating the weights of the generator and discriminator, so they both improve. (*corporate needs you to find the difference between this picture and this picture*)
- They both start really poorly but as they improve they have to both get better at generating/discriminating real data in order to win the game. We update the discriminator multiple times so it can distinguish meaningful differences between real and fake.
- How many times you update the discriminator per generator update, $k$, is a hyperparameter to be tuned.
- The **value function** is the negative of basic cross-entropy loss. The discriminator wants to maximize it, while the generator wants to minimize it. The generator tries to figure out what features the discriminator is looking for to determine which images are real.
- **Conditional GANs** allows us to have control over what the generator is generating by appending the one-hot vector of the class we want. We incentivize the generator to use this by giving it to the discriminator as well, so it is trying to match the labels.
- One problem is that if the discriminator gets too good, the generator stops learning because the gradients vanish (weights go to 0). The generator can also get stuck outputting only a few outputs that work well (mode collapse).
- Also, the vanilla GAN setup doesn't converge and so the value function can swing back and forth 
- One tweak we can do is **Non-Saturating Loss**, which is to try to maximize the probability that generated images get classified as real rather than trying to minimize the value function. This allows the generator to learn faster when it is doing poorly.
- There are 3 major GAN architectures for computer vision: StyleGAN, CycleGAN, and BigGAN.
- Generally the discriminator will just be a classification CNN, which downsamples with convolutions, and the generator upsamples from a latent vector.
- **StyleGAN** ensures that latent vectors and pre-processed, and more closely connected to the convolutions in the network. It also provides access to randomness so it can generate better textures. Latents are accessible throughout the process.
- Pre-processing allows the network to have much more complex "codes" that get used by all the convolutions. StyleGAN also uses AdaIN, another form of normalization which rescales and adds biases, and adds Gaussian noise to feature maps before each convolution.
- **CycleGAN** can take a photo from one style and transfer it to another (e.g. painting -> photo, summer -> winter, horse -> zebra)
- It uses 2 generators and 2 discriminators, for each style of image. Also has a cycle loss function: converting an image and then back again should result in the same image.
- **BigGAN** is a conditional GAN trained for ImageNet, which has 1000 classes, so it is a very large network that makes tradeoffs between stability and quality using large batch sizes.  

Summary: GAN networks can be used to train generative networks when it is difficult to judge quality of outputs by hand, instead using a discriminator network to force the generator to create realistic images to be as similar as possible to real data. They are trained with a value function, which each network tries to skew in its direction to win. In order to force certain outputs we can use conditional GANs, which give both networks the desired label.