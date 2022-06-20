---
layout: default
title: Week 1
parent: Weekly Progress
nav_order: 3
---
---
# Week 1
June 13 - June 19

---
- Bela Cape has shipped from London. (13 June)
- Had #1 weekly meet with mentors Giulio Moro, Vedant Paranjape, and Vaishnav Achath regarding project progress and doubts. 
- Minutes Of Meeting Monday, 13 June, 4pm CEST ( 7:30 IST ):
    - I summarised my learnings from bela build process as it is slow when i tried to reproduce and required a lot of network bandwidth and took the longest after the first run, does all downloads, including the kernal.
    - @Giulio Moro suggested to use sudo ./build_bela.sh --no-kernel --no-bootloader --no-build-xenomai --no-downloads In case need to re-run the build process as it saves time a lot.
    - And addressed some general questions from my side regarding what mentors expecting to be done in the project by first phase of coding period ends and rescheduling my timeline as I have my semester final exams from June 27 to July 6 (approax for two weeks). 
- BeagleBone Black arrived today evening. (15 June)
    - Flashed Debian console Image via microSD card (without flashing the eMMC)
-  A video conference was held to introduce ourselves and meet this year's students! and Jason Kridner addressed on what Beagle cares about, contributing upstream, Asking smart questions, issue submissions on blockers, weekly status reports and growing connections within and beyong the BeagleBoard.org community. Here is a meeting recording [click here](https://youtu.be/8FW5SziGzD4). (15 June, 10pm IST)
- Worked on to understand the workflows of both bela-image-builder and BeagleBoard Image builder repos by rebuilding bela, beagleboard Images and spent most hours on resolving build issues, and downloading code to my build machine.
- Giulio Moro pushed a couple of updates to bela-image-builder that allowed to reproduce image with out any issues.
- Went through the proposal to revise the workflow and made few changes.


