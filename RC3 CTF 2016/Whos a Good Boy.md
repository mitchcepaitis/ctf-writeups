---
layout: post
title: RC3 CTF 2016 - Who's a Good Boy? (Web 100)
date: 2016-11-22 12:12:00
categories: 
- CTF 
- RC3 CTF 2016
---

## Challenge

> You’re trying to see the cute dog pictures on ctf.rc3.club. But every time you click on one of them, it brings you to a bad gateway.
>
> https://ctf.rc3.club:3000/
>
> -- Your friendly neighborhood webadmin

## Solution

A great lesson I learned during my time in the OSCP labs was to never ignore CSS files.  They aren't necessarily directly exploitable, but they can sometimes contain a useful piece of information that ultimately leads to discovering a vulnerability.  This challenge was a great instance of needing to explore CSS.

Looking at the head of the HTML source, I saw that the CSS file was named __doge.css__, which is pretty nonstandard.  Granted, the whole challenge was pretty nonstandard, but that was a clue that the default CSS was probably changed in some way.  The following text was contained in __doge.css__:

```css
.philarydufflebag{
	/*hiya*/
	/*compress your frontend*/
	/*here's a flag :)*/
	flag:RC3-2016-CanineSS
}
```

The flag was simply in the css.  Simple.

## Flag
```none
RC3-2016-CanineSS
```