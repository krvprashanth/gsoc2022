---
layout: default
title: Week 11
parent: Weekly Progress
nav_order: 11
---
---
# Week 11
August 22 - August 28

---
- Had weekly meeting with Giulio Moro, Dhruva Gole on Monday, 22 August, 4:30 pm CEST ( 8:00 IST ) and for minutes of meet [check here](https://git.beagleboard.org/gsoc/building-bela-images/-/wikis/Weekly-meeting-minutes-of-meet!#week11)
- Started working on debian packaging `ti-linux-xenomai-4.14.y` kernel branch with bela configured config from [https://github.com/RobertCNelson/ti-linux-kernel-dev](https://github.com/RobertCNelson/ti-linux-kernel-dev) builds
- `ti-linux-xenomai-bela-4.14.y` branch was forked from `ti-linux-xenomai-4.14.y` to build the ti-linux-xenomai-4.14.y kernel debian package for bela images with bela's config and initialized bela_deconfig from bela-image-builder/kernel and overwritten patches/deconfig.

**The build results in the following packages:** 

| ---   | ---  |
| linux-image-4.14.108-ti-xenomai-bela-r2 | linux-image*deb |
| linux-headers-4.14.108-ti-xenomai-bela-r2 | linux-headers*deb |

- Debian packaged Xenomai repo (which contains libcobalt and the rtdm headers) and also it contains a debian packages configuration and rebuilt it v3.0.13 and made it available the usual way as it was. 

**The build results in the following packages:**

| ---   | ---  |
| xenomai-v3.0-runtime	 | Xenomai runtime utilities |
| libxenomai1-v3.0 | Shared libraries for Xenomai |
| libxenomai-v3.0-dev |  Headers and static libraries for Xenomai |
| xenomai-v3.0-kernel-source | Sources of the Xenomai 2.x kernel |


**target/chroot/bela.io-bullseye.sh** 

- Added bela install script along with install required deb packages and also change source installation path to `/root`
- Installed seasocks, am335x_pru_package before building bela so the later does not fail
- Cleaned up checkinstall and also xenomai installation script in chroot in order to install with deb packages 

**configs/bela.io-debian-bullseye-v4.14-ti-xenomai-armhf.conf**

- Added `clang`,`tree`, xenomai-v3.0.13 (l`ibxenomai-v3.0-dev`, `xenomai-v3.0-kernel-source`, `xenomai-v3.0-runtime`, `libxenomai1-v3.0`) and removed `libstdc++6-10-dbg`,`clang-3.9`
- Updated naming and description to bela specific

Built a Bela Image with all these changes made and also flash and booted the Image on board.

----

#### **Accomplishments**

- source to build the ti-linux-xenomai-4.14.y kernel debian package with bela configured config [[PR #53]](https://github.com/RobertCNelson/ti-linux-kernel-dev/pull/53) 
- Add xenomai (stable/v3.0.x) debian packages configuration [PR #63](https://github.com/rcn-ee/repos/pull/63) 
- some more bela specific changes [[PR #209]](https://github.com/RobertCNelson/omap-image-builder/pull/209) 
- Built a Bela Image with all these changes made and also flash and booted the Image on board.
    
#### **Blockers**
- Unable to install rtdm_pruss_irq

#### **Upcoming Targets**
- Work on rtdm_pruss_irq installation and demo running sinetone example
- Create detailed Documentation about the changes made in Bela Image development process and also a  guide about contributing to Bela Image development and how to make use of code base.
- Write the overall project summary and outcomes.


