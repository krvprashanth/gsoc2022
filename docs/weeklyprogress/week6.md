---
layout: default
title: Week 6
parent: Weekly Progress
nav_order: 7
---
---
# Week 6
July 18 - July 24

---

- Placed order for USB to TTL Serial Cable - UART connection to debug boot process.
- Had weekly meeting with Giulio Moro on  Monday, 20 June, 4:30 pm CEST ( 8:00 IST ) and for minutes of meet [check here](https://git.beagleboard.org/gsoc/building-bela-images/-/wikis/Weekly-meeting-minutes-of-meet!#week6)
- Flash and booted the bela-stretch image which built in lask week and couldn't test the image with examlpe sintone working and as per mentor suggestion started building latest bullseye image for bela.
- Initially, when i tried with the all Bela required packages that were in packages.txt of bela-image-builder and the build getting failed at the point resolving packages and none of the packages weren't able to install via debootstrap. Tried with including bela-image-builder parameters for debootstrap in omap-image-builder scripts though it showed same error.
- Much time was spent on debootstrap trying to figure where it's coming from and it fixed with Robert Nelson help.
- Solution: There's a [sed script](https://github.com/RobertCNelson/omap-image-builder/blob/master/scripts/debootstrap.sh#L41-L54) that reads *.conf file, it's currently only knows about `<tabs>` but yeah, it was always tabs and it's more about more than one space `sed 's/ /,/g'`
- bela.io-debian-bullseye-v4.14-ti-xenomai-armhf build completes all the way and ready for boot testing and figured out what packages broke and then moved that packages under "deb_addition_pkgs" in bela-bullseye conf file.
- Studied about [Debian Live Manual/Customizing Contents](https://live-team.pages.debian.net/live-manual/html/live-manual/customizing-contents.en.html)
- Experimented on different ideas that which is suitable method for cross-compiling  xenomai-3 for Bela with omap-image-builder including in /target/chroot script or chroot_before_hook in /configs bela-bullseye file.
- Updated the target/chroot script (bela.io-bullseye.sh) with installation scripts to repos that bela ships and removed the ones that were not required for bela.
- And, also spent some time on understanding Jenkins build systems as every git commit of omap-image-builder get's built and a full log is available, So it's quick to see if something broke and it just as a validate/helper.
- bela-bullseye Image build logs can be seen [here](http://eewiki.org:8080/job/ci-image-builder/view/change-requests/builds)

----

#### **Accomplishments**
- Built bela-bullseye Image with omap-image-builder scripts
    - Added package list of what currently bela ships [[PR #199]](https://github.com/RobertCNelson/omap-image-builder/pull/199)
    - bela-bullseye-image-build [[PR #200]](https://github.com/RobertCNelson/omap-image-builder/pull/200)
    - Figured out what packages failed to install via debootstrap and made necessary changes [[PR #201]](https://github.com/RobertCNelson/omap-image-builder/pull/201)
    - Modified bela-bullseye chroot script [[PR #202]](https://github.com/RobertCNelson/omap-image-builder/pull/202)
    - Quick-wiki: [Present workflow to build a Bela Image would look like](https://krvprashanth.in/gsoc2022/docs/documentation/building-bela-images/)

- Tested the built bela-bullseye Image
    - Flash and booted the Image
    - Installed Xenomai Kernel and Libraries, am335x PRU package, seasocks
    

#### **Blockers**
- No Blockers

#### **Upcoming Targets**
- Add these files to Bela Image build scripts in omap-image-builder
    - `bela-image-builder/misc/rootfs/lib/systemd/system`
    - `bela-image-builder/misc/rootfs/opt/Bela`
    - more in general all the files that are in `bela-image-builder/misc/rootfs` have a reason to be there.
    
- And also those in 
    - `/lib/system` : copy them over and enable bela_button, bela_ide (systemctl enable bela_button bela_ide)
    - `/opt/Bela`: copy them over
    - `/root` : copy them over
    - `/etc`: need to be checked one by one to see what special settings have been applied

- bela_gadget files
    - check what differences there are with the omap-image-builder version (They have a service called bb-usb-gadgets.service . See what that does and what file it uses)
    - see whether it can "inject" some of these changes in the upstream version or whether we should be maintaining a "forked" version
- `/lib/systemd/system/bela_flash_emmc.service` and `/opt/Bela/bela_flash_emmc.sh` has similar problems.
      


