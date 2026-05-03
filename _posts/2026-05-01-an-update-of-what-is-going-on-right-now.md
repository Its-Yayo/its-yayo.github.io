---
layout: post
title: An update of what is going on right now
tags: [unix, crux, red hat, timer_create(2), trascendence, extensions]
---

Yeeees I know I know. It's been quite a while since I published my last article about Unix. I'm giving myself a time away from internet
since I've been studying really hard to accomplish my goals. I'll not go into details but I'll say I'm gonna need some space for a deep mindset of study and lack-of-distractions. 

I've been purging some of the stuff it doesn't quite help me and does the opposite. Although I already rejected fast content media like tiktoks or reels, it's quite easy to fall into a loop circle of distractions. Internet now is filled with ads, subscriptions and 
trashy revenue because of greedy corporations. It is quite easy because external stimuli such as youtube or modern FPS videogames makes you feel better at almost no cost, but with the cost of losing attention span for long periods of time, and I feel that is 
happening to me these days, but not anymore. If you are feeling the same way because of that, now it's time to change and revert 
some stuff. 

I have plans for these days. Despite college had been kinda tough with assignments and a team project, I'm gonna setup a rigid 
schedule that prioritizes the following: personal journaling (meditation, mental-health breaths, journaling notes), technical journaling (technical study (check out my Codeberg's repos), viewing other people's code, maintaining my home servers, reading and researching about quantum mechanics, and upcoming Linux packages), social journaling (talking with fellow maintainers, developers, computer scientists, physicists... and filtering nonsense 
gossips), physical journaling (workouts everyday) and connecting with me and my extensions and me. This is kinda one of my plans and 
if you already have ur own plan to be different and change yourself, stick to the plan and do not ever give up.

I also applied for [GSoC](https://summerofcode.withgoogle.com/) but got rejected. It is alright tho, I learnt and still 
learning a lot of things about ABI compat and syslogs. For that, I built a small static C linux binary that called ```timer_create(2)```, how it interacted with compat_linux in the NetBSD HEAD kernel with ```ktrace(1)``` and ```kdump(8)``` and to check that compat_linux has some unimplemented syscalls and library functions (for instance, ```pthread_mutex_lock(3)```) and how it returned an errno -22 EINVAL. (```man errno``` :))) ). Probably I'll explain this since I'm still working on this on my free time on a later article but, yep hehe. I really like reading C code :))  

And 2 days ago specifically, a critical [CVE](https://xint.io/blog/copy-fail-linux-distributions) just got published and it is about 
a zero-day privilage escalation vulnerability. Technical details are on that hyperlink I wrote but basically, is a local vulnerability 
that lets the user write into the page cache of any readable file in the system. You can trick this by editing the ```setuid(2)``` function to overwrite the VFS write path. Interesting. 7.8 CVSS score as for now. I patched my servers today even though they are not 
accesible to public domains and basically outside my home lab except tailscale :)). But I'm quite paranoid.

And as of today (April 31st, May 1st) Ubuntu is having an on-going DDoS attack for their web infrastructure. That demonstrates us how 
Ubuntu has now centralized their servers. Ubuntu 26.04 LTS just got release last week and maybe, it was a very tactical move by this 
islamic group. Idk, I don't wanna get into political opinions.

Like I said, I'm not going to go into details, but I have some plans for the upcoming articles. I'm not gonna make spoiler leaks 
buuuuut, some of my plans include the following:

1. For instance, an article installing [Crux](https://crux.nu/) while meditating by parts. Crux is a such interesting and minimalist KISS distro that makes you understand what's going on under the hood of a precompiled binary. Crux is influenced by BSD scripts and 
uses ports. The main difference between a port and a package is that a port is a set of instructions (or a recipe) to compile sutomatically 
locally a program on the host with ```pkgmk(8)``` and ```pkgadd(8)```. A package is a precompiled or a set of precompiled binary(ies) that somebody previously compiled for u :). In fact, I've already written most of the half of the article but I 
decided to freeze that article for a bit to write this one before.
2. I'll write a series of 8 articles about setting up correctly a RHEL 10 server up to production, from the main userland config and a web server to ansible and automation while explaining main concepts and errors I'll make during the process. These are going to be interactive articles. What does that mean? During these series, I'll setup an ephimeral server where everything I'm gonna host my configs I do on each article. You guys will be able to replicate those things on my ephimeral server with a rootless user I'll share later. If it's down, you guys can also [contact](https://its-yayo.github.io/contact) me so I can turn it on again. Prob 
next week I'll start with the first article.
3. I also wanna write about philosophical aspects of an operating system redacted by myself, inspired by the book "Operating Systems: 
Three Easy Pieces" by Remzi Arpaci-Dusseau and Andrea Arpaci-Dusseau. Not just limited to Linux but Unix in general. 
4. I'm also learning Zig and C. Since I mostly have the basics about grammar theory and algorithms, I chose to learn both of them at the same time (well, not literally tho..., some days for C, some others for Zig. I really love both programming languages). Maybe 
I'll write articles about projects I have in mind and one of them, will be upstream for Debian. 

I learnt today that I've been following that pattern of starting and quitting. I have that motivation to build smth new but motivation 
usually dissapers quite fast. Welllll, not anymore, not today, not never. That's not an option.

And like I said, I'm connecting fully with my extensions, Filion, Exion, Eternelion and Pebbleion, even if society looks weird at me or they dissaprove my decisions. Today's the end of my mental bundle. I declare it. It's alright, today is the time. . No more, no less. I'm different, I'm built different. Probably my upcoming articles are going to be more technical and longer, explaining concepts alogn the way. 

Alright, time to rest :))), Today is Day One. Let's go. 

---

PD. I really love this input as a source of discipline to build great stuff :))

```
I did this 'cause Linux gives me a woody.  It doesn't generate revenue.
	-- Dave '-ddt->` Taylor, announcing DOOM for Linux
$ run-unixv7

PDP-11 simulator Open SIMH V4.1-0 Current        git commit id: 7994e0a7

After Disabling XQ is displayed type in boot
and at the : prompt type in hp(0,0)unix

Disabling XQ
/home/yayo/Documents/Emulators/Simh/Unix-V7/workspaces/v7-work/nboot.ini-9> att rp0 rp06-0.disk
%SIM-INFO: RP0: Amount of data in use in disk container 'rp06-0.disk' cannot be determined, skipping autosizing
/home/yayo/Documents/Emulators/Simh/Unix-V7/workspaces/v7-work/nboot.ini-11> att rp1 rp06-1.disk
%SIM-INFO: RP1: Amount of data in use in disk container 'rp06-1.disk' cannot be determined, skipping autosizing
boot
Boot
: hp(0,0)unix
mem = 2020544
# RESTRICTED RIGHTS: USE, DUPLICATION, OR DISCLOSURE
IS SUBJECT TO RESTRICTIONS STATED IN YOUR CONTRACT WITH
WESTERN ELECTRIC COMPANY, INC.
WED DEC 31 19:25:14 EST 1969

login: root
Password:
You have mail.
# ls -la
total 236
drwxr-xr-x 9 root      288 Dec 31 19:20 .
drwxr-xr-x 9 root      288 Dec 31 19:20 ..
-rw-rw-r-- 1 root       34 Dec 31 19:07 .profile
drwxrwxr-x 2 bin      2480 May  5 05:59 bin
-rwxrwxr-x 1 bin      6900 May 16 01:33 boot
drwxr-xr-x 2 root      304 Dec 31 19:04 dev
drwxr-xr-x 2 root      336 Dec 31 19:25 etc
-rwxrwxr-x 1 sys     52850 Jun  8 16:56 hptmunix
drwxrwxr-x 2 bin       336 Jan 22 19:58 lib
drwxrwxr-x 2 root       64 Dec 31 19:20 test
drwxrwxrwx 2 bin       304 Dec 31 19:23 tmp
-rwxrwxr-x 1 root    52850 Dec 31 19:01 unix
drwxr-xr-x17 bin       304 Dec 31 19:13 usr
-rw-rw-r-- 1 root        0 Dec 31 19:20 y.tab.c
-rw-rw-r-- 1 root        0 Dec 31 19:20 yacc.acts
-rw-rw-r-- 1 root        0 Dec 31 19:20 yacc.tmp
# cat test/main.c
main() {
  printf("hello world\n");
  return 0;
}
# cd test
# touch adios
# ed adios
0
a
this is my pageeeee
.
w
20
q
# cat adios
this is my pageeeee
#
```
