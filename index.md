---
layout: default
title: Home
nav_order: 1
---

# GSoC'22 - Building Bela Images
---
![intro](assets/images/photo6100226193669337986.jpg)

The project idea is to Improve the maintainability of the Bela Image development by adding the functionalities of the Bela Image builder repo to the BeagleBoard Image builder repo. 

## About
- _Student Name:_ [Kurva Prashanth](https://krvprashanth.in)
- _Mentors:_ Giulio Moro, Vedant Paranjape, Vaishnav Achath
- _GSoC Entry link:_ [GSoC entry](https://summerofcode.withgoogle.com/programs/2022/projects/ykkMkxcR)
- _Wiki:_ [BB.org forum building-bela-images](https://forum.beagleboard.org/t/building-bela-images/32104)
- _Blog Link:_ [Building Bela Images](https://krvprashanth.in/gsoc2022/) <br>

## Table of Contents
1. [Introduction](#intro)
2. [Implementation Details](#implementation)
	- [Background](#background)
3. [Benefit](#benefit)
4. [References](#ref)

## Introduction <a name="intro"></a>
As given in the official website, Bela is a hardware and software platform for creating beautiful interaction with sensors, sound and it is designed for artists, musicians, researchers and makers, Bela brings the power of ultra-low latency interactive audio and sensors to digital systems.

Bela Platform uses the Bela software which is a customised Debian distribution including a custom xenomai kernel, minimal clutter, and custom systemd configurations and It takes advantage of features of the BeagleBone computers and can achieve extremely fast audio and sensor processing times. 
## Implementation Details <a name="implementation"></a>
In order to add the Bela Image builder features to BeagleBoard Image builder. Firstly, I try building Bela Image by using BeagleBoard Image builder scripts and making necessary changes in scripts to build Image. After this we will be getting a clear idea to where to change and semantic rebase the features of Bela Image builder to BeagleBoard Image builder one.


Here are typical changes need to do in BeagleBoard Image builder repo

   - Bela-specific changes will be made conditional in RootStock-NG.sh script in BeagleBoard Image builder repo
       - Add Bela Image builder scripts features in RootStock-NG.sh script
            - bootloader, kernel, xenomai, downloads, emmc-flasher-chroot and pre-chroot
   - Use config template and create bela-image.conf file and also add bela required packages list to it
   - Make necessary changes in build scripts to Optimise boot times as Bela Image has fast boot time campared to BeagleBoard Image
   - After building Bela Image using Beagleboard Image builder functionalities make changes to the Image-builder repo
    
### Background <a name="background"></a>
Bela Image development repo is heavily based and which was initially inspired by Beagleboard Image-builder scripts. Currently, the Beagle board Image development repo diverged greatly from a common functionalities of building Images.

There is a requirement to "rebase" the functionalities of the Bela Image builder repo to the Beagleboard Image builder one. As the two codebases are drastically different we need to understand and “semantic rebase” the features of the Bela Image builder repo (xenomai kernel building scripts along with a bunch of other stuff) to Beagleboard Image builder repo. After these changes the Bela Image development will follow more closely with the Beagleboard Image development and as a result Bela Image will be updated more often and it minimizes future development effort. 

## Benefit <a name="benefit"></a>
This project adds support for the Bela Image development to make Bela Image follow more closely with BeagleBoard Images. I mean after Bela specific changes made conditional to the Image-builder repository. The Bela Image development will be updated more often, more easily in parallel with BeagleBoard Images. 

## References <a name="ref"></a>
- [Original GSoC Project idea](https://elinux.org/BeagleBoard/GSoC/Ideas-2022)
- [https://github.com/BelaPlatform](https://github.com/BelaPlatform)
- [https://github.com/RobertCNelson/Bootloader-Builder](https://github.com/RobertCNelson/Bootloader-Builder)
- [https://github.com/RobertCNelson/omap-image-builder](https://github.com/RobertCNelson/omap-image-builder)
- [http://www.denx.de/wiki/U-Boot](http://www.denx.de/wiki/U-Boot)
