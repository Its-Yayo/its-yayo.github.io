---
layout: post
title: Installing Arch Linux while meditating
tags: [self-love, linux, arch linux, gnu/linux]
---

## Table of Contents
1. [Intro](#intro)
2. [Init Stuff](#init-stuff)
3. [Disks](#disks)
4. [Init System](#init-system)
5. [Core Packages](#core-packages)
6. [Main Packages](#main-packages)
7. [Conclusion](#conclusion)



### Intro

This is also a personal article I'm writing aside installing [Arch Linux](https://archlinux.org/) (Note, this article is not intended as a tutorial form, but it may help you if you want to install Arch linux as well). In my [skills](https://its-yayo.github.io/skills) page I mentioned that my main OS is Debian GNU/Linux 12 and I use it for everything. However, in this case, I'm running a QEMU virtual machine with the Arch Linux ISO file pre-configured in order to install it from scratch. I'll not use the archinstall script or any other script that allows me to automatize this process. 

Also I said about smth related to meditation and that's true. Recently I've been changing my thoughts in accordance to my deep purpose/eternity path and now it's time to be strong and disciplined. My main [layout page](https://its-yayo.github.io) has a powerful quote about this. In this case, I'm discovering on 2 things: The influence on special and emotional things (materia) and it's structural particle's modifications. I believe this is real. Also I'm discovering on how these things are natually with you by simply using the logic on "recharging" them like as in a watch or a phone, denying all useless emotions and dopamine shots of getting something new (like a new iPhone or idk, clothes). Anyway, I'm replacing my previous thoughts with these ones now. Also I'm accepting my previous thoughts now derived from some habits I grounded very deeply, but I'm not fighting with them anymore. 

Let's get started. 


### Init stuff

When you download the Arch iso, it does not come with a GUI installer as in Ubuntu or Manjaro so, it is not recommended for first-time linux users. I'll breakdown why I'm following the steps I'm writing not only to describe why it is important to follow these steps but also to record myself a mental tape of this. For starters, I need to change the keyboard config. In my case, it is spanish.

```
# loadkeys es
```

I also need to check if my system is connected to internet (which in most cases, it doesn't)

```
# ping -c 1 its-yayo.github.io
```

If you got this message "1 packets transmitted, 1 received, 0% packet loss"; it means you are connected to internet. If not, you must use the iwctl command. In my case, I'm connected so I'll go to the next step but here's the official [wiki](https://wiki.archlinux.org/title/Iwd) if you need some sort of help

Now it's time to configure the locales. In my case I'm in a GMT-6 time zone.


```
# timedatectl set-ntp true
# timedatectl set-timezone "America/Mexico_City"
# timedatectl status
```

(Note, at this time I figured out that if you list the timezones available with the grep command, most of them they are not actual timezones supported by timedatectl, so u have to chech out if ur universal time zone is either MST or UTC). 


### Disks

Let's begin with disk partitions. I assigned 25gb to my local VM so in this case using UEFI mode, so in this case, I need 600 MB for the EFI partition (basically, the boot partition) and the rest for the root (/). 

Using this command will allow me to check which disks are located. In my case, I need to check if the ```/dev/vda``` disk is on.

```
# lsblk
NAME  mMAJ:MIN RM  SIZE RO TYPE MOUNTPOINTS
loop0    7:0    0  810M  1 loop /run/archiso/airootfs
vda    254:0    0   25G  0 disk 
```

Yeaaa it is. Not it's time to use cfdisk to start configuring it. I'll use GPT since I'm using UEFI. cfdisk will launch a "GUI" which you can create, write, resize or dump partitions. In my case, as I said before, I need 600 MB for the EFI system and the rest for the root (remember that Linux uses the ext4 format). My disks are now named ```/dev/vda1``` for the EFI system and ```/dev/vda2``` for the root

I have to format as well both partitions. For the EFI partition, i need to use FAT32 format

```
# mkfs.fat -F32 /dev/vda1
# mkts.ext4 /dev/vda2
```

I have to mount them as well in the ```/mnt``` directory

``` 
# mkdir -p /mnt/boot/efi
# mount /dev/vda1 /mnt/boot/efi
# mount /dev/vda2 /mnt
```

### Init System

Partitions are done, so let's start with the critical files and yea, the linux kernel. Let's wait until the process finishes. I'm using pacstrap as a tool to retrieve system packages. (This was a long wait since I don't have a good download and upload speed so I took the time to meditate on what I said at the beginning of this post and why it is real, that sometimes solitude is good when discovering things, swimming against the tide is tough but trascendental.)

```
# pacstrap -K /mnt base linux linux-firmware 
```

Once it finished, I need to order my boot partitions in order before initiating my system. genfstab will help me with this stuff

```
# genfstab -U /mnt >> /mnt/etc/fstab
```

With both partitions set on, it's now to change my Arch prompt. 


### Core Packages

At this time, I went to sleep to rest my mind to keep growing so now I'm back. (I took a moment to still realize that my sub-conscious mind just normalized such habits that nowadays I reject, so yea, it is a laborious process but real.)

By using the command ```arch-chroot /mnt``` the prompt will be changed since I'm already working with my Arch system, not the init installer. 

As for default, I need the following:
- Set the local time (for my Arch core system)
- Set my Arch hostname and password
- Install grub

Alright, so let's begin. The ```ln``` command will allow me to create a reference (or a link) between the zoneinfo and the localtime

``` bash
$ ln -sf /usr/share/zoneinfo/America/Mexico_City /etc/localtime
```

Also I need to synchronize the hardware clock.

```bash
$ hwclock --systohc
```

Now I need to configure the local language of the Arch core system. I'll use english and spanish so I need to uncomment the locales ```en_US.UTF-8 UTF-8``` and ```es_MX.UTF-8 UTF-8``` located in ```/etc/locale.gen```. If it is ur first time using nano, you just can save the file with ctrl+O and quit with ctrl+X

```bash
$ pacman -S nano
$ nano /etc/locale
$ locale-gen
```

Now they are ganerated, I just need to choose which one I'll use. In my case, spanish is my native language but I'll keep it in english. 

```bash
$ echo LANG=en_US.UTF-8 > /etc/locale.conf
```

Now, let's set up the hostname and password (as for root and user), as well as personal users and more configs. This is quite simple. It is not recommended to assign root privilages to the regular user, but in this case, I'm learning and I'm in my home-made env. 

```bash
$ echo "yayo-arch" > /etc/hostname
$ cat /etc/hostname
$ passwd
$ useradd -m -G wheel -s /bin/bash yayo
$ passwd yayo
$ pacman -S sudo
$ nano visudo
```

I need to uncomment these lines to the visudo file, in order to assign privilages .

```
%wheel ALL=(ALL:ALL) ALL
```

Before continuing, I had to setup the basic config in ```/etc/hosts``` by adding these lines 

```
127.0.0.1 localhost
::1 localhost
127.0.1.1 yayo-arch.localdomain yayo-arch
```

Let's now begin with grub. This is basically the bootloader for Arch so everytime I want to power on my system, grub will allow me to init my system (or troubleshoot it if something is wrong). 

```bash
$ pacman -S grub efibootmgr dosfstools os-prober mtools
```

Once it finishes, I need to mount grub in the ```/dev/vda1``` disk, with previusly I set up up as my EFI system located in ```/mnt/boot/efi```. (Note, in this step I had so many errors since the --target flag was not recognizing the x86_64 parameter, so I had to troubleshoot it by reinstalling the packages. Basically the other error also was that ```/etc/fstab``` was not showing the EFI partition so I had to start all over again on mounting it. To solve it, I re-created the ```/mnt/boot/efi``` in chroot and I mounted it as well. I added the config setup in ```/etc/fstab```  for ```/dev/vda1```, adding these parameters: ```UUID:<uuid> /mnt/boot/efi vfat umask=0077 0 2``` where UUID is the partition identifier, ```/mnt/boot/efi``` is the boot partition, ```vfat``` is the format (FAT32), ```umask=0077 0 2``` is used for file permissions and options  
```bash
$ mount -a
$ cat /etc/fstab
```
These errors are helping me to grow and to get a full understanding of linux :) ).

```bash
$ grub-install --target=x86_64-efi --efi-directory=/mnt/boot/efi --bootloader-id=GRUB 
$ mkdir -p /boot/grub
$ grub-mkconfig -o /boot/grub/grub.cfg
$ exit
```

While doing this, noticed that my VM doesn't support x86_64 and efibootmgr was giving me config errors, so I had to start all over again lol, it's good so I have more time to reflect about these new thoughts and energy I'm building.

Now I'm back, let's continue. It's time to exit the chroot env and reboot

```
# umount -R /mnt
# reboot now
```

When I had to eat smth to take a break, ChatGPT gave me this quote: "Thoughts in themselves don't have power unless you give them power. They are like random clouds but they should not direct your actions or ur proper energy. When a thought comes up, it doesn't mean it has power over you". I used to talk about every thought it comes from my mind but from now, I'll just accept them as they are and 
**I'll refocus myself and my mind on what I'm building now and forever. There's no need to pay attention to those thoughts peacefully anymore.** 


### Main Packages

Alright, now I have a fully-installed Arch Linux, but it is quite empty, I have to install some proper useful packages. Here's a basic summary

- System locales
- Network config
- Main packages (desktop env, git, paru...)

While I was doing this, I noticed that, well, my main core Arch was not installed so in this case, I checked my available interfaces. 
``` bash
$ ip addr
```

My VM is using NAT since my host (my beaity lap with Debian) doesn't have ethernet ports and I had not support for bridged interfaces because of my limited resources. (I tried everything, creating a new interface with ```ip link add``` didn't work) 
My interface in the VM is ```enp1s0``` but the state is down (Chech out the line that says ```STATE DOWM``` or ```STATE UP```) and i had not any IP assigned to it and since I'm using NAT,
I need to setup my IP manually, alongside the gateway. And also, I have to edit the ```/etc/resolv.conf``` file to add the Google's DNS in order to test my manual config.

``` bash
$ sudo ip link set enp1s0 up
$ sudo ip addr add 192.168.122.100/24 dev enp1s0
$ sudo ip route add default via 192.168.122.1
```

(Note, everytime I boot the system I need to repeat this process since I'm assiigning the IPs manually and not by a default DHCP.(Maybe later I'll set them on) 
Now that I have internet and I tested it out by pinging Google's servers, now I can install some fresh packages.

Let's install a graphical environment. I use gnome so I'll install it, as well as the Gnome Display Manager (gdm) for user's logins and sessions. (It took some time to install it so I paused a minute to keep meditating)

``` bash
$ sudo pacman -S gnome gnome-extras gdm
$ sudo systemctl enable --now gdm
$ reboot
```

### Conclusion

![Arch](./arch.png)

Now's done!. I mean, after this I'll keep reflecting but from now I've done it. I also installed htop and firefox. Like I said before, everytime I boot, I need to assign again the configs and the IP address into the network interface but that's a post-installation process. Keyboard config is also laggy but I'll check it out later. 

I just remember myself my first time in Linux using Ubuntu 20.04 in a Windows 10/11 host, but not anymore since I use the mighty Debiannnnn. I think that Linux is now part of my purpose/eternity path because it is helping me to achieve great things and yea, as well as to be different. 

Soon I'll post an article about the Linux filesystem and how it works!. Thank you for reading, I hope you have a great day ♡. 



