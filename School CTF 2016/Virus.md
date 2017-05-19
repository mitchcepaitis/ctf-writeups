---
layout: post
title: School CTF 2016 - Virus (Stegano 200)
date: 2016-11-07 12:02:00
categories: 
- CTF 
- School CTF 2016
---

## Challenge

> My computer is infected with a virus which has hidden all my files.
>
> Can you help me to find my data?

##### Files

1. files_4def417f9aa76bc745bdf347bd8248561a5cf0fb.zip


## Solution

I dove right in and unzipped the archive file to find an image file name __task.png__.  The image showed only a grumpy cat.  Running `foremost` against __task.png__ produced several files which were embedded within.  The flag was found displayed in one of two JPG files which were recovered using `foremost`:

![schoolctf-2016-virus.jpg](/img/2016/schoolctf-2016-virus.jpg "schoolctf-2016-virus.jpg")


## Flag

```none
SchoolCTF{v1rus_ar7_is_r34l_art}
```