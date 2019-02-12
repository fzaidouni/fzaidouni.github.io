---
title: 'A new parallel feedback architecture'
date: 2018-09-11
permalink: /posts/2018/09/parallel-feedback-architecture
tags:
  - computational-neuroscience
  - research
  - vision
  - architecture
excerpt: "The forward-pass classification of the Deep Convolutional Networks (DCNs) inhibit them to actually understand the scene represented by the image. It is restricted to understand each image as lines and edges."
---

Neri in ['Object segmentation controls image reconstruction from natural scenes'](https://journals.plos.org/plosbiology/article?id=10.1371/journal.pbio.1002611) points out that "well defined boundaries within the eye may correspond to irrelevant features of the physical world, while critical features of the physical worlds may be nearly invisible at the retinal projection". Further, the paper hints that the circuitry for the inferior temporal cortex is an integration of both, top-down and bottom-up maps. Much is known about the bottom-up procedure for identification of lines, edges and textures but how top-down maps are constructed for segmentation is yet to be discovered. A new parallel feedback architecture aims to develop an evaluation procedure on *'how memory is used to construct top-down maps in the visual cortex'.*

The forward-pass classification of the Deep Convolutional Networks (DCNs) inhibit them to actually understand the scene represented by the image. It is restricted to understand each image as lines and edges. In a quoted section from Neri's paper,

 > the conceptual compartmentalisation associated with the bottom-up/top-down dichotomy may be more productively replaced by regarding these two processing modes as intimately integrated into a single adaptive mechanism, possibly providing a more appropriate framework for understanding early visual perception in humans.

In the above quoted section, the integrated mechanism of top-down/ bottom-up dichotomy can be imagined as a multi-pass procedure. Multiple passes through such a network will incrementally define the rich and poor locations on the image. The current scene understanding models use the components to define the scene, rather than using the general setting of the scene to predict the components.

![](/images/incrementalarch.png)

Working towards this new scheme of architectures based on scene context would indirectly eliminate computational burden on similar repetitive queries. To understand this better let us consider the following analogy:

> If we walk blindfolded in our home, we can navigate the ways much more quickly than navigating through a new building. Such can be the case since we have much more context information on our home than the new building. As we get more and more context information on similar scenes, the parameters of the scenes pass from fine to coarse down the hierarchy closer to the actual input (Refer to the figure). A coarse parameter set describing the home will return initial results much faster than a further down-the-hierarchy fine-parameter set.

This intuition is further strengthened by the [interactive activation model](http://psycnet.apa.org/record/1981-31825-001) which states that the perception of a letter is dependent upon the context of that letter.

The above discussed architecture closely relates to the compositional model proposed by [Lee and Mumford](https://dash.harvard.edu/bitstream/handle/1/3637109/mumford_hierarchbayesinfer.pdf?sequence=1). The composition model compartmentalised into visual areas has top-down, bottom-up and horizontal computations.

Another crucial component of such a model should be serial data processing which is emphasised heavily in Hawkins's [Hierarchical Temporal Models](https://numenta.com/assets/pdf/whitepapers/hierarchical-temporal-memory-cortical-learning-algorithm-0.2.1-en.pdf). The importance of stream-data is emphasised in the intuition below, which is another question I am currently working towards:

> The optic nerve encodes the perceived retinal images and sends it to the neocortex. The neocortex observes data in a stream fashion i.e. data is fed to the neocortex through the sensory input at all times. The brain makes its own internal representation of the observation but when the representation stored in memory, what is actually stored? a representation of the observation, or the representation of the transition of the observations? A representation of the observation might seem obvious to me at first, but a representation based on transitions would be invariant to scale, luminance and rotation making the storage more compact and generalised.
