---
layout: default
title: Week 10
parent: Weekly Progress
nav_order: 10
---
---
# Week 10
August 15 - August 21

---
- Attended GSoC Allyship and Inclusion Workshop for Contributors.
- Worked on  bela boot.
- Built a bela-bullseye Image with all the changes made till date in omap-image-builder (upstream repo)
- And, asked Giulio Moro and Dhruva Gole to test the bela-bullseye-image on board to get feedback and make changes upon it.
- Bela Images - [http://gfnd.rcn-ee.org:33044/workspace/bela-images/](http://gfnd.rcn-ee.org:33044/workspace/bela-images/)
- Added /etc/ssh/sshd_config.d/allow-unsecure.conf file in bela customizations
- Enabled Bela systemctl services
- Debugging the built image as boot partition is missing.
- Started working on rtdm_pruss_irq.

----

#### **Accomplishments**

- bela boot [[PR #208]](https://github.com/RobertCNelson/omap-image-builder/pull/208) 
- Built bela-bullseye image and also flash and booted the Image
    
#### **Blockers**
- Unable to install rtdm_pruss_irq need to understand clearly about the linux kernel headers that it required.

#### **Upcoming Targets**
- Make a new debian package that provide all these deb files with the appropriate branch from this repo https://github.com/RobertCNelson/ti-linux-kernel-dev builds:
     - *linux-image*deb
     - *linux*headers*deb
     - *linux*firmware*deb
     
need both built the bela_defconfig from bela-image-builder

- Xenomai repo (which contains libcobalt and the rtdm headers) _can_ be built as a Debian package: it contains a debian/ folder. 
TASK: build this as a package and make it available the usual way
- Build a Bela Image with all these changes made in and after build test the Image and debug if it needs.



