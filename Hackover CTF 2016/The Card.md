---
layout: post
title: Hackover CTF 2016 - thecard (Forensics 9)
date: 2016-10-10 12:00:00
categories: 
- CTF 
- Hackover 2016
---

## Challenge

> We obtained a cyber terrorist's SD card, but it seems to be broken. Can you help us recover its content?

##### Files

1. thecard.img.xz


## Solution

First, I extracted the .xz file contents with `xz -d thecard.img.xz`, which produced __thecard.img__.

This seemed to be a disk image file.  Attempting to mount it returned an error: __needs journal recovery__.  After some googling, I found [this helpful post on stackexchange](http://unix.stackexchange.com/questions/60249/ext4-fs-needs-journal-recovery-what-does-this-mean).

I ran `e2fsck` on __thecard.img__ as mentioned in the link and was then able to mount the file system.

```bash
$ e2fsck thecard.img
e2fsck 1.42.13 (17-May-2015)
thecard.img: recovering journal
thecard.img contains a file system with errors, check forced.
Pass 1: Checking inodes, blocks, and sizes
Pass 2: Checking directory structure
Pass 3: Checking directory connectivity
Pass 4: Checking reference counts
Unattached inode 13
Connect to /lost+found<y>? yes
Inode 13 ref count is 2, should be 1.  Fix<y>? yes
Unattached inode 14
Connect to /lost+found<y>? yes
Inode 14 ref count is 2, should be 1.  Fix<y>? yes
Unattached inode 15
Connect to /lost+found<y>? yes
Inode 15 ref count is 2, should be 1.  Fix<y>? yes
Unattached inode 16
Connect to /lost+found<y>? yes
Inode 16 ref count is 2, should be 1.  Fix<y>? yes
Pass 5: Checking group summary information

thecard.img: ***** FILE SYSTEM WAS MODIFIED *****
thecard.img: 16/4096 files (0.0% non-contiguous), 14504/16384 blocks
```

Within the newly mounted file system was a file that wasn't opening properly and didn't seem to have a file type.  Checking it out in `hexeditor` quickly revealed that it was an image file with the first part of the 'magic number' changed to an incorrect value.  

I copied the file to my desktop (the mounted file system was read only) and changed the first two characters of the magic number from __00__ to __FF__.  The image was now happy to open and display the flag:

![hackover-2016-thecard.jpg](/img/2016/hackover-2016-thecard.jpg "hackover-2016-thecard.jpg")

## Flag

```none
hackover16{DontWorryItsJustADoll!}
```