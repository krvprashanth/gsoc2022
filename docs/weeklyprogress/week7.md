---
layout: default
title: Week 7
parent: Weekly Progress
nav_order: 8
---
---
# Week 7
July 25 - July 31

---
- Had weekly meeting with Giulio Moro on Monday, 25 June, 4:00 pm CEST ( 7:30 pm IST ) and for minutes of meet [check here](https://git.beagleboard.org/gsoc/building-bela-images/-/wikis/Weekly-meeting-minutes-of-meet!#week7)
- Currently, bela-image-builder ships [hvcc](https://github.com/giuliomoro/hvcc) (heavy hvcc compiler) that has `python2` dependencies of `pip2`, `enum`, `jinja2` and Debian 11 (bullseye) has removed the " `python` package and the `/usr/bin/python` symlink due to the deprecation of Python 2.. though it has minimal support for python 2.7 adjusted everything for `python3-<package name>` ( updated python3 version of [hvcc](https://github.com/Wasted-Audio/hvcc/) and added dependency package `tox` in bela-bullseye conf ) and also removed `enum` package that no more it required.
- Looked at how [bela-gadget](https://github.com/BelaPlatform/bela-image-builder/blob/master/misc/rootfs/opt/Bela/bela_gadget.sh) is different with compared to bb-usb-gadget (what that does and what file it uses) and whether it can be 'inject' some of bela changes init.
- bb-usb-gadget, takes over anything to do with usb gadget loading.. and it has a systemd script which didn't exist in prior then bullseye ([https://github.com/rcn-ee/repos/blob/master/bb-usb-gadgets/suite/bullseye/debian/bb-usb-gadgets.bb-usb-gadgets.service](https://github.com/rcn-ee/repos/blob/master/bb-usb-gadgets/suite/bullseye/debian/bb-usb-gadgets.bb-usb-gadgets.service))
- Started working on to create a bela-customizations debian package.
- Initialized a repo for [bela-customizations](https://git.beagleboard.org/krvprashanth/bela-customizations) and copied the /misc/rootfs of bela-image-builder repo ( [https://github.com/BelaPlatform/bela-image-builder/tree/master/misc/rootfs](https://github.com/BelaPlatform/bela-image-builder/tree/master/misc/rootfs) ) into it and used this repo as source for debian packaging.
- Studied about [systemd System and Service Manager](https://www.freedesktop.org/wiki/Software/systemd/) and [Lennart Poettering’s](http://0pointer.de/blog/) blog which has lots of information about `systemd`
- Debian packaged bela customizations.
- Used this [dh_installsystemd](https://man7.org/linux/man-pages/man1/dh_installsystemd.1.html) to package the bela systemd files.
- While packaging systemd files learnt a lot about systemd and service manager spent some good time on this and systemd files are fun to deal with.. bela had a tone of them!!!! :)

----

#### **Accomplishments**
- update to python3 version of hvcc compiler [[PR #205]](https://github.com/RobertCNelson/omap-image-builder/pull/205) 
- Add debian package configuration of bela customizations [[PR #61]](https://github.com/rcn-ee/repos/pull/61)
    

#### **Blockers**
- No Blockers

#### **Upcoming Targets**
- Debian package updated/packaged.
    - hvcc
    - prudebug

2 package/week (taking a comfortable room, if some package needs more work). 

- Build a bela-bullseye Image with all the changes made in upstream repo (omap-image-builder) by Aug 5 and after build test the Image and debug if it needs.
- Make some more Bela specific changes in omap-image-builder scripts and also to make sure Bela Image Development follows the workflow of omap-image builder build process.
    - bela_gadget files
    - systemd configuration
    - Installing Bela, bela kernel, Building kernel module (rtdm_pruss_irq), Setting-up clang
    - boot/drivers (BELABOOT)







