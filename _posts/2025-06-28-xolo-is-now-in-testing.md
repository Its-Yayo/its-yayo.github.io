---
layout: post
title: Xolo is now in testing
tags: [linux, security]
---

I've wanted to write this for a couple of weeks but now its the time. Right now its 8:40 pm and I'm just
reflecting with myself about some mental thoughts I've been having lately. In the meantime, my team and I 
already started with the development of Xolo so for starters, I made a couple of changes starting with the OS's flow and
goal. Xolo Linux is a Debian-based distro focused on security, privacy and freedom built for daily use, whether if you wanna use as an operating system
that represents freedom to you or as a security operating system for critical operations. Some specific bullet points:

- Debian-based OS (testing channel)
- Hrdened kernel (6.12 LTS for beta releases)
- AppArmor and strong ufw rules
- Some other great features coming out!...

Also, as a beta release, we planned to develop a self-hosted model trained with Ollama locally. In other words, its like
a self-hosted copilot but only using your CPU (or NPU if u have one). You will be able to opt-in or opt-out at any moment.

Xolo Linux will be a great distro, I already defined some flags with live-build at the moment of this article (Jun 28th). I did a ```build.sh``` bash script with the following structure (everything was built on an existing Debian Testing VM):
- I update the current system with new packages
- ```set -e``` is going to set my shell as "no-exec mode", it just reads the stdin in order to read the syntaxis of the following instructions
- I clean the previous build with ```rm -rf chroot/ cache/``` and ```lb clean --purge```
- I set the live-build parameters
- ```lb build``` sets everything to go

Also I'm adding hooks to automatize packages. Since Xolo Linux will be released with 2 formats (Xolo Day for end-users and Xolo Labs for scientists), its important to include all the 
necessary packages for both versions. Some of the folders as /etc, /usr, /sbin... in the bash script are built automatically by live-bulid

And finally, I'm gonna use (for now) the official installer that Debian (and Kali) use. d-i uses some preseeds that are going to allow me to harden some of the things that Debian doesn't do. I'm also
auto-enabling an automatic LVM-encrypted setup and some strong ufw rules. I might block Google, why now? lol. That's it for now. Branding and the packaging's freezing process
are still on the run. 

I wanted to write this a little bit earlier but I didn't. Tbh, these last 3 weeks were pretty tough for me, not only physically but mentally, just had a long semester. Fortunately, I'm very strong and my sentimental things are along with me everytime (I discovered some quantum 
theories about them!, just noting them, they are not touchable. Just need to calm that somantic memory and irreal thoughts). Just felt that some close friends and people that I love just went away from me, y'know? I mean I can't do anything about that, but I can with my reaction. I love being lonely and having some peace. I'll keep meditating

I'll keep y'all updated. Peace coding :))
