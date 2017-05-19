---
layout: post
title: RC3 CTF 2016 - My Lil Droid (Forensics 100)
date: 2016-11-22 12:00:00
categories: 
- CTF 
- RC3 CTF 2016
---

## Challenge

> Sometimes not all files are needed.
>
> Download Link: https://drive.google.com/file/d/0Bw7N3lAmY5PCOFNQZFgtSVlFZ3M/view?usp=sharing

##### Files

1. youtube.apk


## Solution

Finding the flag for this challenge was extremely quick and painless.  In order to open and view the contents of __youtube.apk__, I renamed it to __youtube.zip__ and extracted the contents.  I skimmed through a few files before I came to the file __build-data.properties__.  I skimmed through this file as well, but noticed what looked like a Base64 encoded string at the end of the file that looked extremely out of place:

`UkMz-2016-R09URU0yMQ==`

Decoding this string gave the flag.

## Flag
```none
RC3-2016-GOTEM21
```