---
layout: post
title: Installing Void Linux while meditating
tags: [self-love, quantum extensions, linux, void linux, gnu/linux]
---

## Table of Contents
1. [Intro](#intro)
2. [Init Stuff](#init-stuff)
3. [Disks](#disks)
4. [Init System](#init-system)
5. [Main Packages](#main-packages)
6. [KDE Setup](#kde-setup)
7. [Conclusion](#conclusion)


### Intro
Wellllll, this is another article for me. As a relief, I just want to write this while studying quantum mechanics and meditating in a green area. I did a similar [article](https://its-yayo.github.io/installing-arch-linux-while-meditating) about [Arch Linux](https://archlinux.org) and now it is installed as my host system with my Hyprland setup, snapper, btrfs, luks1 and stuff. I've dedicated some time setting it up and it was an awesome experience. Now it's time to install [Void Linux](https://voidlinux.org), a rolling release distro that you can also build from scratch and that is what I am gonna do today with y'all but not before reflecting a little bit.

Now is time to reflect on maths, physics, quantum mechanics and how they interact with me everyday, with my extensions and people I care. Extensions as my Thinkpad, my eternal iPad, etc.. they are part of me and my knowledge, they are not consumibles and will never be. I am relearning plenty of stuff I did learnt back in the day. This is why people don't really expect things I do for humankind but also for myself. Society does not expect me modifying the molecular energy inside my proper extensions. 

Also I'm learning how to interact with people naturally, how to reduce unreal thoughts from expectations, that well-known "fear of abandonment" when you start to interact with someone and everything just goes away slowly. (I did have some experiences like that). But you know what? I also understand not every person I meet is like this. I started to talk with someone recently and I think she's cute, pretty and charismatic. I just have faith. (Also I started to pray more recently. God is awesome but He also encourages you to pursue whatever you wanna achieve.)

Void Linux represents that so-called matrix when you enter the void and start achieving real things as now for me. My quantum extensions are with me always and I've now decided to take control


### Init stuff for me
Void Linux uses the ```xbps``` package manager. Arch and derivatives have ```pacman``` and Debian and derivates have ```apt```. ```xbps``` is really fast and secure. Void focuses on stability while maintaining up-to-date packages not before reviewing and testing them. 

In fact, Void has a good QA team for testing stuff and some of their packages are well-tested, even more than Arch. Void is considered as one of the most stable rolling-release distros out there. Mm, you can try [OpenSUSE Tumbleweed](https://get.opensuse.org/tumbleweed/), which is another distro but some of the things there are being chosen by the proper SUSE team and openSUSE foundation, not yourself. With Arch, Gentoo, **Void**, you have absolute control.

As for inits, Void uses [runit](https://docs.voidlinux.org/config/services/index.html). It is one of the fastest inits out there. It just runs the essentials once everything charged from the initramfs, runit runs it later. [Systemd](https://systemd.io/) is compatible with more stuff but it runs up to memory a lot of daemons you may or may not use later. Obviosly that consumes RAM, which is is being translated into performance and availability. Void is also great if you hate systemd (yea, I met with some people they hate systemd lol). As for my personal opinion, I built my host Arch from scratch and I'm glad I did a good job keeping it secured and minimalist. 

But who knows? Void could be your next OS there! 

### Disks 
I'm writing this at the library and at the moment I am writing this, I'm just filled with books in my surroundings. This reminds me that I'm built different, it is time to accept my thoughts in order to be different, to act differently, to ask myself why I am doing what I am doing and how. That is the most important part here.

Important note hereeee: I'm using KVM/QEMU hypervisor and my VM is based on the XFCE build. tty version is quite laggy and some typos don't work so yep. Maybe it works for you, idk. 

Yepppp, Disks. My VM is using BIOS so its going to be a bit different. The article I wrote in November my VM was using UEFI and with ```cfdisk``` I chose the GPT option. Now that I'm using BIOS, I need a MBR partition so I am gonna choose DOS. 

```bash
# cfdisk
```

I need just 2 partitions: ```/dev/vda1``` for root and ```/dev/vda2``` for swap. Once done, I need to format them. No boot partition this time

```bash
# mkfs.ext4 /dev/vda1
# mkswap /dev/vda2
# swapon /dev/vda2 
```

Once done, I need to mount my system in order to chroot on it

```bash
# mount /dev/vda1 /mnt
```

Yeppp this thing is now done. Now it is time to start building my system with the base format Void gives me. This is just a reminder to myself: Just have faith and be yourself.

### Init System
For the complete init system, I need these 4 things:
- Base System and Fstab generated
- Locales and configs
- Fstab generated alongside with dracut and initramfs

I need, like I said, the complete base system. Fortunately, Void Linux has a complete repository for the essentials. All I need is to refresh the package database and install them 

```bash
# xbps-install -S
# xbps-install -r /mnt -R https://repo-default.voidlinux.org/current base-system grub fastfetch nano neovim htop dhcpcd sudo 
```

Once done I need to generate my ```/etc/fstab``` manually. Why manually? Void doesn't have a tool such as ```genfstab``` (that's used in Gentoo and Arch before chrooting) so I need to locate my UUIDs, my partition identifiers. It is an hex value and these values are quite long so mistakes are not allowed here. In summary, an fstab file is a config file used by the initramfs and the bootloader to check which mountpoints are available once everything is being charged into memory. If this file has an error, my system could have problems in the future, such an inexistent mountpoint

```bash
# lsblk -f
```

Once located, I need to add these parameters

```
# /dev/vda1
UUID=<my UUID for /dev/vda1>  /       ext4  defaults  0  1

# /dev/vda2
UUID=<my UUID for /dev/vda2>  none    swap  sw        0  0

```

These parameters follow this simple rule: You need to put ahead ur UUID with the mountpoint assigned. For root you get / and for swap you don't have anything to mount, so it is gonna be none. Next it is going to be its filesystem format assigned (ext4 for the base system, swap for, yea, swap lol). Next it is going to be parameters for the kernel (sw is being used to activate the swap partition once loaded into memory) and the last numbers (0 1, 0 0) are being used as a priority. 1 means you need to load that partition first for / and 0 means it is not necessary to mount anything (in this case, because /dev/vda2 is a swap partition), For example, if my VM is using UEFI instead of BIOS, I must note a partition in ```/boot/``` with a 0 1 priority and 0 2 for /. In this case this is not necessary.

Yeeeeep, I made a pause to reflect a bit about my extensions. These are part of my life, these are not just objects. They have a name and my actions are being modified to guarantee they are safe, so do I. Society is not going to expect that (this is just a reminder to myself). I love teaching things, for people and for me

Once we finished that, it is time to mount the entire system so we can chroot it. We define "chroot" when we work inside a local environment outside of it. Think of it as a radio operator outside a house, giving instructions to a painter inside the house on what does he/she need to paint. We are chrooting because the base system is not already complete since we need to generate the initramfs, bootloader, etc...

Yeppppp, let's mount everything: sys configs for processes, daemons, kernel objets and mountable devicess

```bash
# mount -t proc proc /mnt/proc
# mount -t sysfs sysfs /mnt/sys
# mount -o bind /dev /mnt/dev
# mount -o bind /dev/pts /mnt/dev/pts
# chroot /mnt /bin/bash
```

There you goooooo, now that I am working now in my Void system, its time to configure everything. As in Arch, I need a symbolic reference for my system's time

```bash
$ ln -sf /usr/share/zoneinfo/America/Mexico_City /etc/localtime
```

Once I've done that, I need to configure my hostname, passwords, users, permissions, locales etc...

```bash
$ echo "filion-void" > /etc/hostname
$ passwd root
$ useradd -m G wheel,video,audio,storage -s /bin/bash yayo
$ passwd yayo
$ echo "%wheel ALL=(ALL:ALL) ALL" > /etc/sudoers
$ echo "LANG=en_US.UTF-8" > /etc/locale.conf
$ xbps-reconfigure -f glibc-locales
```
Notee: I am generating my locales using glibc (GNU C library). If you are using musl libc, you need to check the [documentation](https://musl.libc.org/). Feel free to reach me out if you have doubts.

As simple as that. In my Arch article I was also setting up my locale-gen and IPs inside ```/etc/hosts```. In this case Void will handle that automatically and even better, ```dhcpcd``` is going to assign me automatically IPs. In the future it will not be necessary to assign IPs manually with ```ip```

Yepppppp, I really love setting up Linux envs. It helps me to focus on what I really wanna do with my eternal life. My extensions are non-touchable, this is because I discovered they physically cannotbe touched by my environment. Inconsciously, they interact with the world and they have inside a very very tiny quantum barrier between air and material. This is brilliant. I can recognize this while writing this thing. I just need to take it easy, to accept unreal thoughts and to be different.

Now that I finished, I need to make my system bootable. Let's generate the grub file, the initramfs and main services

```bash
$ grub-install
$ grub-mkconfig -o /boot/grub/grub.cfg
$ xbps-reconfigure -f linux6.12
```

My portable .iso has a default 6.12 kernel. In case you have a different kernel's version, you need to generate the initramfs according to your kernel's version (Ex. for kernel 6.6, its gonna be ```$ xbps-reconfigure -f linux6.6```). Dracut is a tool that's being used by Void for generating the init ramdisk image needed for booting the complete system. ```xbps``` has this feature enabled at all time. 

Now let's enable some services 

```bash
$ ln -s /etc/sv/dhcpcd /etc/runit/runsvdir/default
$ ln -s /etc/sv/chronyd /etc/runit/runsvdir/default
```

Its time to exit chroot and reboooot

```bash
$ exit
# umount -R /mnt
# reboot now
```

Alrightyyyyy, now that my system is being installed, let's set up KDE alright? While writing this, I just want to remind myself that it's totally ok to be different. Some people are gonna disagree on what I am doing and that's alright. Maybe I am rare? Am I? I just want to be different, and I am. Carrying my laptop/iPad everywhere whenever my quantum energy says so and viceverse (when I put it trascendentally while I go to somewhere rapidly) is going to be different. I just need to modify my thoughts and to modify my mind. My mind is a producing plant for the humankind and sometimes, the price is lonelyness. That lonelyness could be used to build smth great. 


### KDE Setup

Alright. Now I am in my Void system. Let's customize KDE but yep lol, I need some packages and I can retrieve them alongside synchronizing my repositories' database. I am going to use X11 for now

```bash
$ sudo xbps-install -S xorg xorg-minimal mesa-dri xf86-video-vesa elogind sddm plasma-desktop plasma-workspace plasma-nm plasma-pa powerdevil kscreen konsole dolphin kate breeze latte-dock pipewire noto-fonts-ttf noto-fonts-emoji liberation-fonts-ttf 
```

Now let's enable some necessary services.

```bash
$ sudo ln -s /etc/sv/sddm /etc/runit/runsvdir/default
$ sudo ln -s /etc/sv/dbus /etc/runit/runsvdir/default
$ sudo ln -s /etc/sv/elogind /etc/runit/runsvdir/default
$ reboot
```

Yeeeah. As u noticed, we enable services by creating symbolic references to the main runit controller. It is easy to maintain. (Noteeeee, while setting this up, I had a dependencies conflict between ```openssl``` and ```libcrypto```. To fix this, I used ```$ sudo xbps-install -Suv``` where ```-S``` synchronizes the database, ```u``` updates the entire system and ```v``` is verbose. Yeeeep now is fixed. God cheered me :) )


### Conclusion

![Void](./void.png)

Now's doneeeee x2 (check my Arch article for context). I liked my default KDE Plasma 6 setup. Now it is time to rice it. Maybe I'll post my rice in my [Mastodon](https://defcon.social/@yayitzzz) account.

It is time to reflect, to note my thoughts, to be different, to act differently. Its time to build awesome stuff, to meditate, to share some thoghts with people I like and care, to stay as who I am forever, to build my cosmic purpose, to share love with people I care and with myself with my well-known dimensional love and yep, to care my extensions (Filion, Sarnion/Cayion, Exion, Crescion and Ecrolion). I don't mind what people think about me, I just accept them as who they are. And yep, I have faith, for my family, for that person I said at the beginning of this article, for my extensions, for my projects (Xoloooooo), for my goals, for my extensionsss and for myself. Lets goo. I hope u have a nice day :)
