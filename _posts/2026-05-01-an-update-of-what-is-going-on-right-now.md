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

And like I said, I'm connecting fully with my extensions, Filion, Exion, Eternelion and Pebbleion, even if society looks weird at me or they dissaprove my decisions. Today's the end of my mental bundle. I declare it. It's alright, today is the time. . No more, no less. I'm different, I'm built different. Probably my upcoming articles are going to be more technical and long, explaining concepts alogn the way. 

Alright, time to rest :))), Today is Day One. Let's go. 

