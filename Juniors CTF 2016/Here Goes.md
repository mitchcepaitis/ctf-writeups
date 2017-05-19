---
layout: post
title: Juniors CTF 2016 - Here Goes! (Trivial Crypto Recon)
date: 2016-11-28 12:03:00
categories: 
- CTF 
- Juniors CTF 2016
---

## Challenge

This challenge starts by giving the following image with some sort of intentional cryptic characters:

![juniors-2016-heregoes1.png](/img/2016/juniors-2016-heregoes1.png "juniors-2016-heregoes1.png")


## Solution

This whole CTF was themed around a TV show called Gravity Falls.  After a quick Google search for something like 'Gravity Falls decrypt', I found the following image which allowed me to decrypt the original message:

![juniors-2016-heregoes2.jpg](/img/2016/juniors-2016-heregoes2.jpg "juniors-2016-heregoes2.jpg")

The decrypted message was:

```none
FIXPROB
LEMQUIC
KLYWITH
GALVANI
ZEDJETS
```
The flag was just all of this text as a single string with no spaces.

## Flag
```none
FIXPROBLEMQUICKLYWITHGALVANIZEDJETS
```