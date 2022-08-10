---
layout: default
title: Week 8
parent: Weekly Progress
nav_order: 8
---
---
# Week 7
August 1 - August 7

---
- Had weekly meeting with Giulio Moro on Monday, 1 August, 4 pm CEST ( 7:30 pm IST ) and for minutes of meet [check here](https://git.beagleboard.org/gsoc/building-bela-images/-/wikis/Weekly-meeting-minutes-of-meet!#week8)
- Started working debian packaging of heavy hvcc compiler.
- Used [dh-virtualenv](https://dh-virtualenv.readthedocs.io/en/latest/index.html) to package the heavy hvcc compiler source.
- Debian packaged hvcc.

----

#### **Accomplishments**

- Add debian package of hvcc [[PR #62]](https://github.com/rcn-ee/repos/pull/62)
    
#### **Blockers**
- No Blockers

#### **Upcoming Targets**
- Work on last week pending targets 
- Debian package updated/packaged.
    - prudebug

- Build a bela-bullseye Image with all the changes made in upstream repo (omap-image-builder) by Aug 5 and after build test the Image and debug if it needs.
- Make some more Bela specific changes in omap-image-builder scripts and also to make sure Bela Image Development follows the workflow of omap-image builder build process.
    - bela_gadget files
    - systemd configuration
    - Installing Bela, bela kernel, Building kernel module (rtdm_pruss_irq), Setting-up clang
    - boot/drivers (BELABOOT)


