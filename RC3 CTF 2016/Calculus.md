---
layout: post
title: RC3 CTF 2016 - Calculus (Crypto 200)
date: 2016-11-22 12:03:00
categories: 
- CTF 
- RC3 CTF 2016
---

## Challenge

> I hope you like calculus :)
>
> Google Word Doc:
> https://docs.google.com/document/d/1fy05WIVTxymehT5i_n64V0IScTcGAXcKjeW6mLZnBp4/edit?usp=sharing

## Solution

The challenge document contained a list of simple calculus calculations:

![rc3-2016-calculus.jpg](/img/2016/rc3-2016-calculus.jpg "rc3-2016-calculus.jpg")

Solving these gave:

```none
a^1
n^2
t^3
i^4
2d^5
e^6
r^7 + r^5 + r^3 + r + 1
v^8 + v^7 + v^4 + v^2 + 9v
```

Looking at the exponents, a pattern emerged.  The letters are already in the correct order, but the fact that they are also arranged by ascending exponent (ignoring the extra r and v results) reinforced the answer, __antiderv__.

## Flag
```none
RC3-2016-antiderv
```