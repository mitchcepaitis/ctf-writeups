---
layout: post
title: H4ckIT CTF 2016 - FullyD00M3D (Web 50)
date: 2016-10-03 12:01:00
categories: 
- CTF 
- H4ckIT 2016

---
# FullyD00M3D

### Challenge
- **Competition:** HackIT CTF 2016
- **Category:** Web
- **Points:** 50

> Hell on the Earth!!
> Skulltag: ctf.com.ua:10666
> h4ck1t{flag.lower()}


### Solution

This wasn't really a challenge so much as an interesting distraction.  This was obviously somehow related to the video game Doom, and the port number `10666` really tipped me off that this was likely a Doom server (port `666` is the port used by Doom for multiplayer).  I researched [Skulltag](http://www.skulltag.com) and learned that it is a port of Doom with "Excellent online play", among other things.  The solution became fairly obvious.

I downloaded the Skulltag client, connected it to a [Doom wad file](https://en.wikipedia.org/wiki/Doom_WAD), and then joined the server.  Upon loading into the game successfully, I opened the console and the flag was displayed. 

### Flag

`h4ck1t{h4v3_s0m3_k1lls}`