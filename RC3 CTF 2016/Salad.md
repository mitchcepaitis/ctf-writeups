---
layout: post
title: RC3 CTF 2016 - Salad (Crypto 100)
date: 2016-11-22 12:01:00
categories: 
- CTF 
- RC3 CTF 2016
---

## Challenge

> “The fault, dear Brutus, is not in our stars, but in ourselves.” (I.ii.141) Julius Caesar in William Shakespeare’s Julius Caesar
>
> Cipher Text: 7sj-ighm-742q3w4t

## Solution

The clues made it painfully obvious that this was a simple [Caesarian cipher](https://en.wikipedia.org/wiki/Caesar_cipher), but there was a little bit of a twist to this challenge.  I ran the cipher text through several online ROT-n deciphers, but none of them produced anything intelligible. 

Usually numbers in this kind of challenge will end up being 1337 speak, but this time they were an integral part of the rotational scheme.  It was announced that the flag would always start with "RC3-2016", so translating the beginning of the cipher text revealed that each character needed to be shifted by +20 and that the possible characters were a-z0-9.

Applying that shift to the whole cipher revealed the flag.

## Flag
```none
RC3-2016-ROMANGOD
```