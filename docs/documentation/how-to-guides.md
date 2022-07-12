---
layout: default
title: How-To Guides
parent: Documentation
nav_order: 1
---

---------------------------------------------------------------------------------------------------
## Table of Contents


- [ARM Cross-Compilation on Debian x86 Machine](#quick-wiki-arm-cross-compilation-on-debian-x86-machine)
- [Find SD card device name](#find-sd-card-device-name)

 --------------------------------------------------------------------------
 
### **Quick-wiki: ARM Cross-Compilation on Debian x86 Machine**
---
The latest versions of DebianDebian has excellent support for cross-building through Debian Cross-toolchains ( see wiki: [https://wiki.debian.org/ToolChain/Cross](https://wiki.debian.org/ToolChain/Cross) ).

Toolchains are set of software development tools and libraries (such as gcc , gdb , glibc ) that are chained together to enable you to build executable code on one operating system on one type of machine, such as a 64-bit Linux OS on an Intel x86 machine, but to execute them on a different operating system and/or a different architecture, such as a 32-bit Linux OS on an ARM device.

Debian cross toolchain is a good starting point. We can list the available toolchains as follows:
    
    prashanth@krv:~$ apt-cache search cross-build-essential
    crossbuild-essential-amd64 - Informational list of cross-build-essential packages
    crossbuild-essential-arm64 - Informational list of cross-build-essential packages
    crossbuild-essential-armel - Informational list of cross-build-essential packages
    crossbuild-essential-armhf - Informational list of cross-build-essential packages
    crossbuild-essential-i386 - Informational list of cross-build-essential packages
    crossbuild-essential-powerpc - Informational list of cross-build-essential packages
    crossbuild-essential-ppc64el - Informational list of cross-build-essential packages
    crossbuild-essential-s390x - Informational list of cross-build-essential packages
    crossbuild-essential-mips - Informational list of cross-build-essential packages
    crossbuild-essential-mips64 - Informational list of cross-build-essential packages
    crossbuild-essential-mips64el - Informational list of cross-build-essential packages
    crossbuild-essential-mips64r6 - Informational list of cross-build-essential packages
    crossbuild-essential-mips64r6el - Informational list of cross-build-essential packages
    crossbuild-essential-mipsel - Informational list of cross-build-essential packages
    crossbuild-essential-mipsr6 - Informational list of cross-build-essential packages
    crossbuild-essential-mipsr6el - Informational list of cross-build-essential packages

The main purpose of these packages is to allow cross-compiling of Linux programs for different architecture distributions, but these can be used also for bare metal programming. One thing to be aware is the fact that the compiler by default tries to link the Linux standard C libraries that in bare metal programming have no use.

Here, I'm using ARM hard float ( armhf ) package for writing programs that is
deployed to the Beagle boards.

    prashanth@krv:~$ sudo apt install crossbuild-essential-armhf
    Preparing to unpack .../crossbuild-essential-armhf_12.9_all.deb ...
    Unpacking crossbuild-essential-armhf (12.9) ...
    Setting up crossbuild-essential-armhf (12.9) ...

Test installation by calling the compiler directly.

    prashanth@krv:~$ arm-linux-gnueabihf-g++ -v
    COLLECT_GCC=arm-linux-gnueabihf-g++
    Thread model: posix
    gcc version 10.2.1 20210110 (Debian 10.2.1-6) 

I’m writing a short C++ program, testcross.cpp , which can be compiled into binary code using the cross-compiler.

    prashanth@krv:~$ gedit testcross.cpp
    prashanth@krv:~$ more testcross.cpp
    #include<iostream>
    using namespace std;
    int main(){
    cout << "Testing cross compilation for armhf" << endl;
    return 0;
    }
    prashanth@krv:~$ arm-linux-gnueabihf-g++ testcross.cpp -o testcross
    prashanth@krv:~$ ls -l testcross*
    -rwxr-xr-x 1 prashanth prashanth 9064 Apr  5 13:02 testcross
    -rw-r--r-- 1 prashanth prashanth  119 Apr  5 13:00 testcross.cpp

The binary file has an executable flag, but when the binary is invoked, it fails to execute. This is unsurprising, as we are attempting to execute ARM binary instructions on an Intel x86 machine.

    prashanth@krv:~$ ./testcross
    arm-binfmt-P: Could not open '/lib/ld-linux-armhf.so.3': No such file or directory

This error indicates that the ld-linux-armhf.so.3 file is not in the system library directory. A search of the filesystem locates it in the /usr/arm-linux-gnueabihf/lib/ directory.

    prashanth@krv:~$ stat /usr/arm-linux-gnueabihf/lib/ld-linux-armhf.so.3
      File: /usr/arm-linux-gnueabihf/lib/ld-linux-armhf.so.3 -> ld-2.31.so
      Size: 10        	Blocks: 0          IO Block: 4096   symbolic link
    Device: b302h/45826d	Inode: 1447823     Links: 1
    Access: (0777/lrwxrwxrwx)  Uid: (    0/    root)   Gid: (    0/    root)
    Access: 2022-04-05 13:02:21.727259593 +0530
    Modify: 2021-03-03 17:24:20.000000000 +0530
    Change: 2022-03-29 20:49:01.659052574 +0530
    Birth: 2022-03-29 20:49:01.631052872 +0530

One approach to solve this issue is to explicitly call the QEMU tool and specify the library directory, whereupon the program is emulated correctly.

    prashanth@krv:~$ qemu-arm-static -L /usr/arm-linux-gnueabihf/ testcross
    Testing cross compilation for armhf

Success! If we see this output, then we are able to build a binary on the x86 machine that can be executed directly on the ARM machine. 

 --------------------------------------------------------------------------
### **Find SD card device name**
 --------------------------------------------------------------------------
The SD card is an essential part of the Embedded Linux Systems. It's often necessary to copy(or "flash") the software from our machine to an SD card for use in Embedded Linux System, or to back up projects ot the entire contents of SD card.

This guide is about to find the SD card's device name! *choosing the wrong drive will likely result in data loss or even worse harm to our machine*.

My machine has an Integrated SD card reader and it is connected by a multiport USB unit and will be presented as `/dev/sdx`, where `X` is a single letter. The first hard drive is often /dev/sda. In most of the machines with SD card slots, this wiil be often be `/dev/mmcblk0`.

I find the following method to be handy and simple:

**Step1**: Open a terminal

**Step2**: Get the list of existing devices in our system into a temporary file (say, /tmp/before_sd):
      
    prashanth@krv:~$ ls /dev > /tmp/before_sd
     
**Step3**: Insert SD card (be it via an external reader or directly to the SD port of your computer)

**Step4**: Get again the list of devices into a second temporary file (say, /tmp/after_sd):
 
    prashanth@krv:~$ ls /dev > /tmp/after_sd
 
**Step5**: Compare them
   
    prashanth@krv:~$ diff /tmp/before_sd /tmp/after_sd
    36a37,39
    > mmcblk0
    > mmcblk0p1
    > mmcblk0p2
 
 Or, if the device follows `sdX`, it would be:
 
    prashanth@krv:~$ diff /tmp/before_sd /tmp/after_sd
    55a57,59
    > sda
    > sda1 
    

 
 **Note**: The topmost name we received - In my case, `sda`. That’s the device we want to write to! (the other devices will point to partitions within the media we inserted).

