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
## **Build Instructions :**
### 1. Download RobertCNelson/omap-image-builder

    git clone https://github.com/RobertCNelson/omap-image-builder
    cd ./omap-image-builder
    
### 2. **Generate**: Base Debian Images 
#### Debian Stretch 9.13
    ./RootStock-NG.sh -c bela.io-debian-stretch-armhf-v4.14-ti-xenomai
       
#### Debian Bullseye 11.4
    ./RootStock-NG.sh -c bela.io-debian-bullseye-v4.14-ti-xenomai-armhf
        
### Archive will be under './deploy/'

### 3. **Finalize**: Bela specific version:

    sudo ./setup_sdcard.sh --img-4gb bela-example --dtb beaglebone --distro-bootloader --enable-cape-universal --enable-uboot-enable-pru
    
---
# Achieved Milestones

---

---
#  Pull Requests

---


| Repository | PR | Status |
| --- | ---   | ---  |
| **[ rcn-ee/repos ](https://github.com/rcn-ee/repos)** | [Xenomai, seasocks Debian packages](https://github.com/rcn-ee/repos/pull/60) | Closed |
| **[RobertCNelson/omap-image-builder](https://github.com/RobertCNelson/omap-image-builder)** | [Update packages list of Bela in configs](https://github.com/RobertCNelson/omap-image-builder/pull/199) | Closed |
| **[RobertCNelson/omap-image-builder](https://github.com/RobertCNelson/omap-image-builder)** | [bela-bullseye-image-build](https://github.com/RobertCNelson/omap-image-builder/pull/200) | Merged |
