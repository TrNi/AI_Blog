+++
title = 'Diffusion Models in Computer Vision'
date = 2024-06-09T13:52:55-07:00
draft = false
+++

> Diffusion models have proven to be very successful at image generation in computer vision, offering more tractability in the noise-removal / image synthesis process by splitting it into small tasks per step. This post provides an overview and insight into evolution of diffusion models in recent years.

Papers in this post:
<!--% Previous posts [Display label 1]({{< ref "postname.md" >}}). -->

1. **"Deep Unsupervised Learning using Non-equilibrium Thermodynamics"**, Jascha Sohl-Dickstein et al., 2015, [arXiv:1503.03585](http://arxiv.org/abs/1503.03585) 
2. **"Denoising Diffusion Probabilistic Models"**, Jonathan Ho et al., 2020, [arXiv:2006.11239](https://arxiv.org/abs/2006.11239) 
3. **"Improved Denoising Diffusion Probabilistic Models"**, Alex Nichol et al., 2021, [arXiv:2102.09672](https://arxiv.org/abs/2102.09672) 
4. **"Diffusion Models Beat GANs on Image Synthesis"**, Prafulla Dhariwal et al., 2021, [arXiv:2105.05233](https://arxiv.org/abs/2105.05233)

### 1. Deep Unsupervised Learning using Non-equilibrium Thermodynamics
Jascha Sohl-Dickstein et al., 2015, [arXiv:1503.03585](http://arxiv.org/abs/1503.03585), also published in PMLR, 2015. 

This paper (abbrev. DUL-Therm) drew ideas from non-equilibrium statistical physics and introduced two processes:

**A. Forward Diffusion Process:**
Iteratively destroy structure in a data distribution. For the case of general images, the authors use Gaussian noise with mean and variance changing for each step. Starting from a clean image, iteratively add noise until reaching identity covariance on each pixel. 

**B. Reverse Diffusion Process:**
Iteratively restore structure in data by predicting noise parameters at each step. Starting from an image with identity covariance on each pixel, iteratively denoise it until reaching a clean image.

The authors list contributions of this paper as:
1. extreme flexibility in model structure, 
2. exact sampling,
3. easy multiplication with other distributions, e.g. in order to compute a posterior, and
4. the model log likelihood, and the probability of individual states, to be cheaply evaluated.

Efficacy of this un-supervised diffusion algorithm is demonstrated on datasets such as a 2D swiss roll, binary sequence, handwritten digits (MNIST), and natural images (CIFAR-10, bark, and dead leaves).

Notation:

- **$\mathbf{x}_t$**: Image at time-step $t$
- **T**: Total steps
- $q(\mathbf{x}_t \mid \mathbf{x}_{t-1})$: Forward process: Given an image $\mathbf{x}_{t-1}$, add noise to get $\mathbf{x}_t$
- $p(\mathbf{x}_{t-1} \mid \mathbf{x}_t)$: Reverse process: Given a noisy image $\mathbf{x}_t$, predict noise of step $t$ and subtract it from $\mathbf{x}_t$ to get cleaner image $\mathbf{x}_{t-1}$

