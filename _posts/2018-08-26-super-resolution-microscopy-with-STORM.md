---
layout: post
title: Super-resolution microscopy with STORM
date: 2018-08-26 00:00:00 +0300
description: An explanation of STORM super-resolution microscopy and how I have used it.
img: croatiaislands.jpg
tags: [CV, Physics, Research]
---

Over the past three years I have done a lot of super-resolution imaging using the STORM microscope that was built in the Photon Science Institute at the University of Manchester.

### The diffraction limit and the need for super-resolution

With a little money you can try to achieve higher resolution camera images by upgrading your cameras sensor or lens. However, the diffraction limit usually will play a part eventually, and is generally the limiting factor in many modern camera lenses. It is also the dominant limiting factor in the resolution of microscopes.

Diffraction occurs when light passes through a hole (or aperture) and causes the light rays to spread out. You can read more about it [here][diffraction]. The spreading out of light as it passes through the lens makes objects appear blurry and thus limits the resolution of your camera or microscope.

The diffraction limit for some of the most state-of-the-art microscope lenses operating with visible light is approximately 250 nm. Although this might sound small, biological samples can be very small and when we want to image the structures and processes going on within bacteria and cells a resolution of 250 nm is often not enough.

### Super-resolution imaging

With the advent of modern computing power and image processing techniques super-resolution imaging has been born to attempt to beat the classical diffraction limit.

All of these techniques rely on careful control of the fluorescent dyes which we use to label our samples and see them under the microscope. The wikipedia article on [super-resolution imaging][super-res wiki] has a lot more information on the different techniques out there but we will focus on STORM.

### STORM

STORM stands for STochastic Optical Reconstruction Microscopy which is a bit of a mouthful, hence the acronym. However, the basic technique only has a few steps which need to be completed to make the final image. There is a [good video][youtube-blinking] showing the process that you might want to watch whilst reading the explanation below.

#### 1. Use blinking fluorescent dyes to induce a state of partial illumination of the sample.

STORM relies upon the choice of special fluorescent dye molecules which feature the capability to blink on and off. The dye molecules are either in a "bright" state or a "dark" state and they randomly change between the two states over time.

However, the average time the dye spends in each state is different and the dye spends a much longer time in the dark state. The effect of this is that at any one time almost all (95-99%) of the dye molecules are in the dark state and only a few are in the bright state and therefore visible.

INSERT IMAGE OF BRIGHTNESS OVER TIME FOR ONE DYE

The overall effect of this is that the when we look at the sample in the microscope the whole display looks like the nights sky, except all the stars are constantly turning on and off.

The important element here is that the light from each dye molecule does not overlap with the light from any other - i.e. all we see are well separated spots of light. This process generates the "original image" side of the [STORM Eiffel Tower video][youtube-blinking].

IMAGE OF FULLY VS PARTIALLY ILLUMINATED SAMPLE

#### 2. Record thousands of images of the partially illuminated sample.

Now that the sample is blinking away we record many thousands of images of the sample (e.g. 30,000). This is needed because one image doesn't give us enough information to create a complete image of the sample. To do this we need information about all the dye molecules that are on the sample. As the dye molecules randomly change between bright and dark, then by recording lots of images we make sure that every dye molecule appears in at least one of the many images we record.

#### 3. "Localise" each dye molecule in the images.

Now we have all our raw data, we can process it to start forming our final image. As we have recorded an image of each dye molecule on its own - as all the dye around it was in the "dark" state, we know that each should produce a spot with a size equal to the diffraction-limited resolution. We can use a computer to determine the position of each dye molecule which produces every spot in our images. 

By doing this we can find the position of each dye molecule in our sample with an accuracy that is much better than the diffraction-limited resolution. This gives us a very large table of dye locations or "localisations".

This step is the "particle detection" part of the [STORM Eiffel Tower video][youtube-blinking].

IMAGE OF THE FITTING OF A DYE MOLECULE SIDE PROFILE

#### 4. Form our final image using the position of each dye molecule.

The final step is to form the final image, and typically this is done by generating a grid over our sample. Then we count how many localisations are in each square of the grid, this then becomes the brightness of the square. As shown in the "Reconstruction" part of the [STORM Eiffel Tower video][youtube-blinking].

STANDARD VS STORM IMAGE






[diffraction]:https://isaacphysics.org/concepts/cp_diffraction
[super-res wiki]:https://en.wikipedia.org/wiki/Super-resolution_microscopy
[youtube-blinking]:https://www.youtube.com/watch?v=RE70GuMCzww
