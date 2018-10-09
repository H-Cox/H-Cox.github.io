---
layout: post
title: Super-resolution microscopy with STORM
date: 2018-08-26 00:00:00 +0300
description: An explanation of STORM super-resolution microscopy and how I have used it.
img: microscope.jpg
tags: [CV, Physics, Research]
---

Over the past three years I have done a lot of super-resolution imaging using the STORM microscope that was built in the Photon Science Institute at the University of Manchester. In this post I describe how the technique works and the general process that goes in to each super-resolution image.

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

The image below shows an example of what we might expect from the brightness of one pixel over time. The dye starts in the bright state and then has two short periods in the on state, where the intensity is over 100 but spends most of the time in the dark state and has low light intensity.

<div style="text-align:center"><img src ="{{site.baseurl}}/assets/img/STORM/LocaTime.pdf"/></div>

The overall effect of this is that the when we look at the sample in the microscope the whole display looks like the nights sky, except all the stars are constantly turning on and off.

The important element here is that the light from each dye molecule does not overlap with the light from any other - i.e. all we see are well separated spots of light. This process generates the "original image" side of the [STORM Eiffel Tower video][youtube-blinking].


#### 2. Record thousands of images of the partially illuminated sample.

Now that the sample is blinking away we record many thousands of images of the sample (e.g. 30,000). This is needed because one image doesn't give us enough information to create a complete image of the sample. To do this we need information about all the dye molecules that are on the sample. As the dye molecules randomly change between bright and dark, then by recording lots of images we make sure that every dye molecule appears in at least one of the many images we record.

#### 3. "Localise" each dye molecule in the images.

Now we have all our raw data, we can process it to start forming our final image. As we have recorded an image of each dye molecule on its own - as all the dye around it was in the "dark" state, we know that each should produce a spot with a size equal to the diffraction-limited resolution. We can use a computer to determine the position of each dye molecule which produces every spot in our images. 

By doing this we can find the position of each dye molecule in our sample with an accuracy that is much better than the diffraction-limited resolution. The accuracy is typically down to about 20 nm, which is ten times less than the diffraction-limit and is acheived by applying different statistical models to the data, for example the maximum-likelyhood estimator is a popular choice. This process gives us a very large table of dye locations or "localisations", typically at least a million.

This step is the "particle detection" part of the [STORM Eiffel Tower video][youtube-blinking].

<div style="text-align:center"><img src ="{{site.baseurl}}/assets/img/STORM/STORMFit.pdf"/></div>

As an example, I have have fit the localisation above by taking the pixel values along the blue line in the image. The raw data is fit with a Gaussian profile and finds the location of the dye that created the blink with sub-pixel resolution, i.e. at pixel 6.25 with an error of 0.13 pixels. The pixels on our camera are 130 nm in size so therefore the error is approximately 17 nm.

#### 4. Cleaning the data

To obtain the best images we really need to be fussy with our data and one of the largest causes of poor image quality is sample drift in the plane of the image. As we have a potential resolution of < 20 nm, any slight movement of the sample of this much over the 5 minute image capture time will cause blur in the images. Luckily we can group the data according to time and then cross-correlate it to determine if any drifting has occured and correct for it.

Other cleaning operations typically involve removing data points which have unphysical attributes. For example, each blink should be as wide as the diffraction-limited resolution so if it is much bigger or much smaller then it is probably due to noise or an artifact in the raw data. Furthermore, we can remove localisations which are not close to any other localisations. As each dye blinks it should appear multiple times in the image, any localisation that is on its own is probably due to noise and will just make the image look worse.

#### 5. Form our final image using the position of each dye molecule.

The final step is to form the final image, and typically this is done by generating a grid over our sample. Then we count how many localisations are in each square of the grid, this then becomes the brightness of the square. As shown in the "Reconstruction" part of the [STORM Eiffel Tower video][youtube-blinking].

<div style="text-align:center"><img src ="{{site.baseurl}}/assets/img/STORM/StandardvsStorm.pdf"/></div>

Above is an image taken from one of my samples I use in my PhD, the synthetic peptide I<sub>3</sub>K, which forms long thin fibrils. As you can see the STORM image is much clearer and we can see what is going on in the images much better. Furthermore, the background in the STORM images is almost zero, which is due to the specific nature of the fitting and post-processing which only allows localisations through which meet certain criteria.

If you got this far, I hope it made sense as it is quite a complicated procedure. If you have any further questions then feel free to get [in touch][my email].




[diffraction]:https://isaacphysics.org/concepts/cp_diffraction
[super-res wiki]:https://en.wikipedia.org/wiki/Super-resolution_microscopy
[youtube-blinking]:https://www.youtube.com/watch?v=RE70GuMCzww
[my email]:mailto:henryfcox@live.com
