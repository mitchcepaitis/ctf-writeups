---
layout: post
title: Hack.lu CTF 2016 - simplepdf (Programming 150)
date: 2016-10-21 12:00:00
categories: 
- CTF 
- Hack.lu 2016
---

## Challenge

> This one is realy simple ... Just get the Flag out of this pdf.

##### Files

1. simple.pdf


## Solution

Like the challenge text says, this one was simple.  Using `pdftk`, the [PDF Toolkit](https://www.pdflabs.com/tools/pdftk-the-pdf-toolkit/), I was able to extract an embedded file within __simple.pdf__.  The embedded file was simply named __pdf10000.pdf__.  I ran the same command to unpack an embedded file within the newly unpacked __pdf10000.pdf__.

This newest file was simply named...  __pdf9999.pdf__.  Wait.  It's _that_.  

Ok, 10,000 layers of embedded files, no big deal.  One simple script later and the flag was mine.


## Script (Bash)

```bash
#!/bin/bash

pdftk simple.pdf unpack_files
pdftk pdf10000.pdf unpack_files

for i in {9999..1..-1}
do
        pdftk "pdf${i}.pdf" unpack_files

        temp=$((i+1))
        rm "pdf${temp}.pdf"

done
pdftk start.pdf unpack_files
```

## Flag

```none
flag{pdf_packing_is_fun}
```