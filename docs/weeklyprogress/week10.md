---
layout: default
title: Week 10
parent: Weekly Progress
nav_order: 10
---
---
# Week 9
August 15 - August 21

---
- Worked on  bela boot.
- Built a bela-bullseye Image with all the changes made till date in omap-image-builder (upstream repo)
- And, asked Giulio Moro, Dhruva Gole to test the bela-bullseye-image on board to get feedback and make changes upon it.
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
- Update upcoming targets once discussing in the weekly meet.
