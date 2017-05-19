---
layout: post
title: Juniors CTF 2016 - Black Suprematic Square (Trivial Web)
date: 2016-11-28 12:00:00
categories: 
- CTF 
- Juniors CTF 2016
---

## Challenge

The challenge consisted of a simple web page with the following photo of the painting 'Black Suprematic Square' by [Kazimir Malevich](https://en.wikipedia.org/wiki/Kazimir_Malevich):

![juniors-2016-blacksuprematicsquare1.jpg](/img/2016/juniors-2016-blacksuprematicsquare1.jpg "juniors-2016-blacksuprematicsquare1.jpg")


## Solution

Looking through the source code gave this challenge away very quickly.  There was another JPG file 'hidden' underneath the 'Black Suprematic Square' image:

![juniors-2016-blacksuprematicsquare2.jpg](/img/2016/juniors-2016-blacksuprematicsquare2.jpg "juniors-2016-blacksuprematicsquare2.jpg")

After trying to decipher this seemingly random text for a short while, I simply tried submitting it as a single string of text as the flag and it ended up working.

## Flag
```none
aima0AiwahsidupaiToehoong1PhieruqueivahphieKah7uceetair9aiGae1eSsaedoo4becooShohhu8eifahXi7EJoh2gaephechei5chiP9
```