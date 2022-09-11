---
layout: default
title: Building Bela Images
parent: Documentation
nav_order: 3
---
---
# Building Bela Images

Bela Image builds with [RobertCNelson/omap-image-builder scripts](https://github.com/RobertCNelson/omap-image-builder)

---
These are the same build scripts that were used to generate the official BeagleBoard Images, found here: [https://beagleboard.org/latest-images](https://beagleboard.org/latest-images)

### **Build Instructions**
__________
These scripts are tested on Debian x86 machine.


A typical workflow to build a Bela Image would look like:

1. Download RobertCNelson/omap-image-builder

       git clone https://github.com/RobertCNelson/omap-image-builder
       cd ./omap-image-builder
    
2. **Generate**: Base Debian Images 
       
Debian Bullseye 11.4

       ./RootStock-NG.sh -c bela.io-debian-bullseye-v4.14-ti-xenomai-armhf
        
Archive will be under `./deploy/`

3. **Finalize**: Bela specific version:

       sudo ./setup_sdcard.sh --img-4gb bela-example --dtb beaglebone --distro-bootloader --enable-load-bela-overlay
    
After the script finishes running, we will have an image file generated.



