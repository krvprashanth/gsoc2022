---
layout: default
title: Home
nav_order: 1
---
# **Building Bela Images**
## **[GSoC'2022 | BeagleBoard.org](https://summerofcode.withgoogle.com/programs/2022/organizations/beagleboardorg)**

---
![intro](assets/images/photo6100226193669337986.jpg)

The project idea was to Improve the maintainability of the Bela Image development by adding the functionalities of the Bela Image builder repo to the BeagleBoard Image builder repo. 


## **About**
- _Student Name:_ [Kurva Prashanth](https://krvprashanth.in)
- _Mentors:_ Giulio Moro, Vedant Paranjape, Vaishnav Achath
- _GSoC Entry link:_ [Program Project Page](https://summerofcode.withgoogle.com/programs/2022/projects/ykkMkxcR)
- _Wiki:_ [Building Bela Images](https://bela.io/gsoc)
- _Blog Link:_ [Building Bela Images](https://krvprashanth.in/gsoc2022/) <br>

## **Table of Contents**
1. [Introduction](#intro)
    - [Why Bela Image has been built again?](#rebuild)
    - [Project Preview](#preview)
    - [Brief Overview of Bela Image](#overview)
2. [Documentation](#docs)
    - [Debian -- Packages](#debian-packages)
    - [omap-image-builder](#omap)
    - [Bela Software](#belasoftware)
    - [Writings](#writings)
3. [Contributions](#contribution)
    - [Achieved Milestones](#milestones)
    - [Git Repositories](#repos)
    - [Pull Requests](#pr)
4. [Further Implementation](#scope)
5. [Conclusion](#conclusion)
6. [Helpful Links](#ref)

---

## **Introduction** <a name="intro"></a>

Bela is an open hardware hardware and software platform for creating beautiful interaction with sensors, sound and it is designed for artists, musicians, researchers and makers, Bela brings the power of ultra-low latency interactive audio and sensors to digital systems.

Bela Platform uses the Bela software which is a customised Debian distribution including a custom xenomai kernel, minimal clutter, and custom systemd configurations and It takes advantage of features of the BeagleBone computers and can achieve extremely fast audio and sensor processing times. 

### **Why Bela Image has been built again?** <a name="rebuild"></a>

The Bela Image development repo is heavily based and which was initially inspired by Beagleboard Image-builder scripts. Currently, the Beagle board Image development repo diverged greatly from a common functionalities of building Images.

And, there is an requirement to “rebase” the functionalities of the Bela Image builder repo to the Beagleboard Image builder one. As the two codebases are drastically different and need to rebuild the Bela Image and add the features of the Bela Image builder repo (xenomai kernel building scripts along with a bunch of Bela core) to Beagleboard Image builder repo. 

Now, after the specific changes the Bela Image development is following more closely with the Beagleboard Image development and as a result from now the Bela Image will be updated more often and it minimized further development effort.

### **Project Preview** <a name="preview"></a> 

The main goal is to Improve the maintainability of the Bela Image development by adding the functionalities of the Bela Image builder repo to the BeagleBoard Image builder repo.

**Note**: *This project isn't rewrite omap-image-builder with bela changes, it's merge bela changes into omap-image-builder*.

Bela Image builds with [RobertCNelson/omap-image-builder scripts](https://github.com/RobertCNelson/omap-image-builder), These are the same build scripts that were used to generate the official BeagleBoard Images, found here: [https://beagleboard.org/latest-images](https://beagleboard.org/latest-images)


##### **Bela - Build-Script Instructions**

These scripts are tested on Debian x86 machine.


A typical workflow to build a Bela Image would look like:

- Download RobertCNelson/omap-image-builder

       git clone https://github.com/RobertCNelson/omap-image-builder
       cd ./omap-image-builder
    
- **Generate**: Debian root file system 
       
Debian Bullseye 11.5

       ./RootStock-NG.sh -c bela.io-debian-bullseye-v4.14-ti-xenomai-armhf
        
Archive will be under `./deploy/`

- **Finalize**: Bela specific version:

       sudo ./setup_sdcard.sh --img-4gb bela-image --dtb beaglebone --distro-bootloader --enable-load-bela-overlay
    
After the script finishes running, we will have an image file generated.

### **Brief Overview of Bela Image** <a name="overview"></a> 
- Image uses Debian 11 (Bullseye) with the [ti-linux-xenomai-bela-4.14.y](https://github.com/RobertCNelson/ti-linux-kernel-dev/tree/ti-linux-xenomai-bela-4.14.y) and `Xenomai v3.0.13`
- Image have the default root user with no password.
- On the first boot, the image will expand to fill the eMMC or SD card.
- Root login over ssh is enabled.
- The hostname is set to the name of board it’s for as Bela
- Loads Bela IDE over browser, `bela.local`


TODO (elaborate)

---
## **Documentation** <a name="docs"></a> 

### **Debian -- Packages**

##### **Introductory notes**
Debian package updated/packaged the dependencies of Bela and pushed to apt packager manager at [https://rcn-ee.com](https://rcn-ee.com) that used in omap-image-builder along with mainline Debian apt package manager.

Debian 11: (bullseye): [http://repos.rcn-ee.com/debian/](http://repos.rcn-ee.com/debian/)

    deb [arch=armhf] http://repos.rcn-ee.com/debian/ bullseye main
    #deb-src [arch=armhf] http://repos.rcn-ee.com/debian/ bullseye main


##### **Package lists**
These are the Bela required packages that are up in [https://rcn-ee.com](https://rcn-ee.com)

| ---   | ---  |
| bela-customizations | Bela customizations |
| bela-seasocks | Simple, small, C++ embeddable webserver with WebSockets support |
| hvcc | hvcc compiler for Pure Data patches - python3 |
| libxenomai1-v3.0 | Shared libraries for Xenomai |
| libxenomai-v3.0-dev |  Headers and static libraries for Xenomai |
| linux-image-4.14.108-ti-xenomai-bela-r2 | linux-image*deb |
| linux-headers-4.14.108-ti-xenomai-bela-r2 | linux-headers*deb |
| xenomai-v3.0-kernel-source | Sources of the Xenomai 2.x kernel |
| xenomai-v3.0-runtime	 | Xenomai runtime utilities |

### **omap-image-builder**

##### **Bootloader: U-Boot**
TODO

##### **U-Boot /boot/uEnv.txt configuration**
TODO

##### **Enable and Load Custom Device Tree Overlay**

In  [omap-image-builder/tools/setup_sdcard.sh](https://github.com/RobertCNelson/omap-image-builder/blob/master/tools/setup_sdcard.sh) 
 
Just tweak it here: [https://github.com/RobertCNelson/omap-image-builder/blob/f9b6785eca8c275dc665012efef06141400c5846/tools/setup_sdcard.sh#L1289](https://github.com/RobertCNelson/omap-image-builder/blob/f9b6785eca8c275dc665012efef06141400c5846/tools/setup_sdcard.sh#L1289)
				
       ###Todo: make this more generic so you can specify any overlay...
	       if [ "x${load_custom_overlay}" = "xenable" ] ; then
	              echo "###" >> ${wfile}
	              echo "dtb_overlay=PB-HACKADAY-2021.dtbo" >> ${wfile}
	               echo "" >> ${wfile}
	       fi

Load With: [https://github.com/RobertCNelson/omap-image-builder/blob/f9b6785eca8c275dc665012efef06141400c5846/tools/setup_sdcard.sh#L2102](https://github.com/RobertCNelson/omap-image-builder/blob/f9b6785eca8c275dc665012efef06141400c5846/tools/setup_sdcard.sh#L2102)

	--enable-load-custom-overlay)
		load_custom_overlay="enable"
		;;

##### **Populating rootfs and Boot Partition**
TODO

### **Bela Software**
TODO

### **Writings**
I maintained weekly log my progress throughout the program. For the most part it has my work progress for the week and for the issue documented.

 [**Weekly Progress**](https://krvprashanth.in/gsoc2022/docs/weeklyprogress/)

 **How-To Guides**
 ( TODO )

 **Project Notes**
 ( TODO )

 **Weekly Meeting Minutes**
  ( TODO )



---
## **Contributions** <a name="contribution"></a>

### **Achieved Milestones** <a name="milestones"></a> 
TODO
### **Git Repositories** <a name="repos"></a> 

Common software that is on or used for building bela image.

- [rcn-ee/repos](https://github.com/rcn-ee/repos) - Debian package configuration
- [RobertCNelson/omap-image-builder](https://github.com/RobertCNelson/omap-image-builder) - Image builder
- [RobertCNelson/ti-linux-kernel-dev](https://github.com/RobertCNelson/ti-linux-kernel-dev) - ti-linux-xenomai-bela-4.14.y
- [Kurva Prashanth/bela-customizations](https://git.beagleboard.org/krvprashanth/bela-customizations) - Source for bela-customizations debian package

### **Pull Requests** <a name="pr"></a> 

In the following table, I present the pull requests (PRs) I created during the GSoC program. 

##### [rcn-ee/repos](https://github.com/rcn-ee/repos)

| PR | Status |
| ---   | ---  |
| Add seasocks, xenomai debian packages configuration [[PR #60]](https://github.com/rcn-ee/repos/pull/60) | Closed |
| Add debian package configuration of bela customizations [[PR #61]](https://github.com/rcn-ee/repos/pull/61) | Merged |
| Add debian package configuration of hvcc [[PR #62]](https://github.com/rcn-ee/repos/pull/62) | Merged |
| Add xenomai (stable/v3.0.x) debian packages configuration [[PR #63]](https://github.com/rcn-ee/repos/pull/63) | Closed |
|bela-customizations: cleanup and add bb-start-acm-ncm-rndis-old-gadget [[PR #64]](https://github.com/rcn-ee/repos/pull/64) | Merged |

##### [RobertCNelson/omap-image-builder](https://github.com/RobertCNelson/omap-image-builder)

| PR | Status |
| ---   | ---  |
| Update packages list of Bela in configs [[PR  #199]](https://github.com/RobertCNelson/omap-image-builder/pull/199) | Closed |
| bela-bullseye-image-build [[PR  #200]](https://github.com/RobertCNelson/omap-image-builder/pull/200) | Merged |
| figured out what packages failed to install and made necessary changes [[PR  #201]](https://github.com/RobertCNelson/omap-image-builder/pull/201) | Merged |
| modify bela-bullseye chroot script [[PR #202]](https://github.com/RobertCNelson/omap-image-builder/pull/202) | Merged |
| update to python3 version of hvcc compiler [[PR #205]](https://github.com/RobertCNelson/omap-image-builder/pull/205) | Merged |
| bela boot [[#208]](https://github.com/RobertCNelson/omap-image-builder/pull/208) | Merged |
| some more bela specific changes [[#209]](https://github.com/RobertCNelson/omap-image-builder/pull/209) | Merged |

##### [RobertCNelson/ti-linux-kernel-dev](https://github.com/RobertCNelson/ti-linux-kernel-dev)
 
| PR | Status |
| ---   | ---  |
| source to build the ti-linux-xenomai-4.14.y kernel debian package with bela configured config [[PR #53]](https://github.com/RobertCNelson/ti-linux-kernel-dev/pull/53) | Merged |


---
## **Further Implementation** 
TODO

---
## **Conclusion**
TODO

---

## **Helpful Links**
- [Original GSoC Project idea](https://elinux.org/BeagleBoard/GSoC/Ideas-2022)
- [https://github.com/BelaPlatform](https://github.com/BelaPlatform)
- [https://bela.io](https://bela.io)
- [https://github.com/beagleboard/image-builder](https://github.com/beagleboard/image-builder)
- [https://github.com/BelaPlatform/bela-image-builder](https://github.com/BelaPlatform/bela-image-builder)
