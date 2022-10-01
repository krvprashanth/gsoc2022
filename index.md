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

       sudo ./setup_sdcard.sh --img-4gb bela-image --dtb beaglebone --distro-bootloader --enable-cape-universal --enable-load-bela-overlay
    
After the script finishes running, we will have an image file generated.

### **Brief Overview of Bela Image** <a name="overview"></a> 
- Image uses Debian 11 (Bullseye) with the [ti-linux-xenomai-bela-4.14.y](https://github.com/RobertCNelson/ti-linux-kernel-dev/tree/ti-linux-xenomai-bela-4.14.y) and `Xenomai v3.0.13`
- Image have the default root user with no password.
- On the first boot, the image will expand to fill the eMMC or SD card.
- Root login over ssh is enabled.
- The hostname is set to the name of board it’s for as Bela
- Loads Bela IDE over browser, `bela.local`
- Uses Robert Nelson's Beaglebone image-builder scripts to build image.

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

Cape device tree overlays (src): [https://github.com/beagleboard/bb.org-overlays/](https://github.com/beagleboard/bb.org-overlays/)

Debian package: bb-cape-overlays

    uboot_overlay_addr0=/lib/firmware/<file0>.dtbo
    uboot_overlay_addr1=/lib/firmware/<file1>.dtbo
    uboot_overlay_addr2=/lib/firmware/<file2>.dtbo
    uboot_overlay_addr3=/lib/firmware/<file3>.dtbo

If for some reason we need to disable the auto-loading of any of ^ those, use the option that matches addrX: 

    disable_uboot_overlay_addr0=1
    disable_uboot_overlay_addr1=1
    disable_uboot_overlay_addr2=1
    disable_uboot_overlay_addr3=1

4 more capes can be loaded via: 

    uboot_overlay_addr4=/lib/firmware/<file4>.dtbo
    uboot_overlay_addr5=/lib/firmware/<file5>.dtbo
    uboot_overlay_addr6=/lib/firmware/<file6>.dtbo
    uboot_overlay_addr7=/lib/firmware/<file7>.dtbo

Plus one custom cape:

    dtb_overlay=/lib/firmware/<file8>.dtbo  


##### **U-Boot /boot/uEnv.txt configuration**
/boot/uEnv.txt: 

In Bela Image build used this configuration to load-bela-overlay, Use Distro Bootloader, and Cape Universal Enable

    --distro-bootloader --enable-cape-universal --enable-load-bela-overlay 




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
###### **Boot Partition**
###### **Rootfs Partition**

### **Bela Software**

##### **Bela Core**

`seasocks`, `am335x_pru_package`, `Bela IDE`, `prudebug`, `rtdm_pruss_irq`, `hvcc` are installed through [/target/chroot/bela.io-bullseye.sh](https://github.com/RobertCNelson/omap-image-builder/blob/master/target/chroot/bela.io-bullseye.sh) script and `custom xenomai kernel` and all other `Bela required packages` are installed through [/configs/bela.io-debian-bullseye-v4.14-ti-xenomai-armhf.conf](/configs/bela.io-debian-bullseye-v4.14-ti-xenomai-armhf.conf)

##### **Bela Customizations**
The `bela-customizations` debian package ships these ([https://github.com/BelaPlatform/bela-image-builder/tree/master/misc/rootfs](https://github.com/BelaPlatform/bela-image-builder/tree/master/misc/rootfs)) files as it is to bela image.

Initialized a repo for bela-customizations and copied the /misc/rootfs of bela-image-builder repo in it and used this repo as source for packaging.

###### **Removed**

- `dhcp.conf` cause bela-customizations package failed to install due to '/etc/dhcp/dhcpd.conf', which is also in package isc-dhcp-server and better file, this has dhcp enabled..., that exact same setup is done thru systemd-network.. with: bb-usb-gadget package... [https://github.com/rcn-ee/repos/blob/master/bb-usb-gadgets/suite/bullseye/debian/usb0-DHCP.network](https://github.com/rcn-ee/repos/blob/master/bb-usb-gadgets/suite/bullseye/debian/usb0-DHCP.network)
- `securetty` In Debian Bullseye, the runtime that use to use etc/securetty no longer uses that file.. it was completely removed as a legacy option.. Reference: [https://www.debian.org/lts/security/2021/dla-2596](https://www.debian.org/lts/security/2021/dla-2596)
- `fstab`, `hosts` these files are generated when we run setup_sdcard.sh of omap-image-builder
- `interfaces` systemd-network uses a new inteface..
- `wpa_supplicant.conf` will find it already pre-installed..


#### **Changes that need to be done**

###### **Bela Bootloader**
---
This still need to be converted...  [bela_bootloader.sh](https://github.com/rcn-ee/repos/blob/master/bela-customizations/suite/bullseye/debian/bela_bootloader.sh#L99-L102)


     echo "log: dd if=/mnt/boot/MLO of=${DEVICE} seek=${dd_spl_uboot_seek} bs=${dd_spl_uboot_bs}"
     dd if=/mnt/boot/MLO of=${DEVICE} seek=${dd_spl_uboot_seek} bs=${dd_spl_uboot_bs}
     echo "log: dd if=/mnt/boot/u-boot.img of=${DEVICE} seek=${dd_uboot_seek} bs=${dd_uboot_bs}"
     dd if=/mnt/boot/u-boot.img of=${DEVICE} seek=${dd_uboot_seek} bs=${dd_uboot_bs}

This should just call and depend on debian package bb-u-boot-am335x-evm

     /opt/u-boot/bb-u-boot-am335x-evm/install-mmcblk1.sh

###### **DHCP  /etc/dhcp/dhcpd.conf**
---
Bela using dhcp to set usb0/usb1... [https://github.com/rcn-ee/repos/blob/master/bela-customizations/suite/bullseye/debian/dhcpd.conf#L40-L46](https://github.com/rcn-ee/repos/blob/master/bela-customizations/suite/bullseye/debian/dhcpd.conf#L40-L46)

        subnet 192.168.7.0 netmask 255.255.255.0 {
            range 192.168.7.1;
        }

        subnet 192.168.6.0 netmask 255.255.255.0 {

In Bullsye, the exact same setup is done through systemd-network.. with: bb-usb-gadget package [https://github.com/rcn-ee/repos/blob/master/bb-usb-gadgets/suite/bullseye/debian/usb0-DHCP.network](https://github.com/rcn-ee/repos/blob/master/bb-usb-gadgets/suite/bullseye/debian/usb0-DHCP.network)

###### **Bela Gadget**
---
This should be tweaked [https://github.com/BelaPlatform/bela-image-builder/blob/master/misc/rootfs/opt/Bela/bela_gadget.sh](https://github.com/BelaPlatform/bela-image-builder/blob/master/misc/rootfs/opt/Bela/bela_gadget.sh) in an option in: [https://github.com/rcn-ee/repos/blob/master/bb-usb-gadgets/suite/bullseye/debian/bb-start-acm-ncm-rndis-old-gadget](https://github.com/rcn-ee/repos/blob/master/bb-usb-gadgets/suite/bullseye/debian/bb-start-acm-ncm-rndis-old-gadget) as it auto loads the gadget driver.

    [Unit]
    Description=BeagleBoard.org USB gadgets
    After=usb-gadget.target
    ConditionFileIsExecutable=/usr/bin/bb-start-usb-gadgets


### **Writings**
I maintained weekly log my progress throughout the program. For the most part it has my work progress for the week and for the issue documented.

 [**Weekly Progress**](https://krvprashanth.in/gsoc2022/docs/weeklyprogress/)

 [**How-To Guides**](https://krvprashanth.in/gsoc2022/docs/documentation/how-to-guides/)
 
 [**Project Notes**](https://krvprashanth.in/gsoc2022/docs/documentation/project-notes/)
 
 [**Weekly Meeting Minutes**](https://git.beagleboard.org/gsoc/building-bela-images/-/wikis/Weekly-meeting-minutes-of-meet!)
  



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
