---
layout: default
title: Week 5
parent: Weekly Progress
nav_order: 6
---
---
# Week 5
July 11 - July 17

---

#### **Accomplishments**
- Packaged [seasocks v1.4.4](https://git.beagleboard.org/gsoc/building-bela-images/-/tree/main/debian-packages/seasocks)
- Built [bela-stretch](https://github.com/RobertCNelson/omap-image-builder/commit/737a993c0ea5caa54399529981fd002a8dc85907) Image with omap-image-builder scripts

#### **Blockers**
- Unable to boot the built bela-stretch Image
- Not able to Install bela base packages with debootstrap by using omap-Imap-builder scripts.

#### **Upcoming Targets**
- Build latest bela-bullseye Image with omap-image-builder
   - flash and boot the image
   - copy on the board the Bela repo cd into it and do 'makelib'
   - enable the BB-BELA-00A0.dtbo device tree overlay
   - create a `root` user, make it the default user, with no password and also delete the `debian` user that would be there as default
   - `make EXAMPLE=Fundamentals/sinetone` in the Bela folder and it should work



