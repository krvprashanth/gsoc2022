---
layout: default
title: Building Bela Images
parent: Documentation
nav_order: 3
---
---
# Building Bela Images
Exerimental Bela Image build with [RobertCNelson/omap-image-builder scripts](https://github.com/RobertCNelson/omap-image-builder)

---
## **Generate**: Base Debian Images
 
 
### Debian Stretch 9.13

    git clone https://github.com/RobertCNelson/omap-image-builder
    cd ./omap-image-builder
    ./RootStock-NG.sh -c bela.io-debian-stretch-armhf-v4.14-ti-xenomai
    
    
### Debian Bullseye 11.4

    git clone https://github.com/RobertCNelson/omap-image-builder
    cd ./omap-image-builder
    ./RootStock-NG.sh -c bela.io-debian-bullseye-v4.14-ti-xenomai-armhf
        
    

### Archive will be under './deploy/'

### Finalize: Bela specific version:

    sudo ./setup_sdcard.sh --img-4gb bela-example --dtb beaglebone --distro-bootloader --enable-cape-universal --enable-uboot-disable-pru


