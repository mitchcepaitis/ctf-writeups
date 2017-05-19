---
layout: post
title: H4ckIT CTF 2016 - Evil_Corps (Crypto 115)
date: 2016-10-03 12:04:00
categories: 
- CTF 
- H4ckIT 2016
---

## Challenge

> Genegal Thompson welcomes you! <br>
> Let me be extremely brief. <br>
> Our forensic team have already been investigating <br>
> "The Great Plantation" project for 2 years. <br>
> During this long period we knew a lot of interesting things like: <br>
> 1) This is the project of Masons. <br>
> 2) The main target is to take over the world with planting own people into big companies. <br>
> 3) Masons do not trust modern encryption algorithms. <br>
> 4) Masons think their own alphabet will let them to communicate more securely than anything else. <br>
> Short time ago we have withdrawn the notebook of one of their members. <br>
> There was one interesting file named "THEPlantation.txt". <br>
> Surely, it was encrypted. Help us to pull the info out of this! <br>
> Yours, Gen. Tompson


###### Files

1. THEPlantation_c6aa4681e8135e731a7ee657ec9c64e7.txt


## Solution

With the given 'clues' from the challenge text in mind, I jumped right into the text file.  At first glance this file contained only junk characters.  I kept scanning the lines visually, hoping for some _actual_ letters to be hiding somewhere, but there weren't.  What was weird, though, was that I could almost read this supposed junk text.  Here's a snippet:

+θΔӕ¥ ωΣ ∫¦ɲӕλλ¥ Ͻθᛗ∏λΣ+ΣΔ +ϦΣ 9ʁΣӕ+ ∏λӕɲ+ӕ+¦θɲ ∏ʁθτΣϽ+
ӕɲΔ βΣλθω ¦§ Σɲ+¦+¦Σ§ ωΣ Ϧӕ✔Σ ¦ɲ θµʁ ∏θϽϟΣ+ ∫θʁ ɲθω

I kept working on just reading the symbols and eventually figured it out.  Points 3 and 4 from the challenge text sort of confirmed what I was beginning to suspect.  The text file was written in a simple letter substitution code.  After determining all of the corresponding substitutions, a simple script helped to 'translate' the text file.  Python was upset about the original file being UTF-8 encoded, so the script needed to include some code for working with it.  The "+" and "9" characters in the original text weren't processing correctly, so I made special exceptions for them in the script.  I need to go back and figure out what that problem was...

After running the script and reading through the more legible version of the text file, I found the following lines quickly:

```none
WELL TAKE YOUR JUICY FLAG CRYPTOMANIAC
FLAGIS MASSONSAREEVERYWHERELOOKBEHINDYOU
WELL TAKE YOUR JUICY FLAG CRYPTOMANIAC
```


## Script (Python)

```python

#!/usr/bin/env python
# -*- coding: utf-8 -*-

translation = {
	u'\u04D5': 'A',   #  ӕ 
	u'\u03B2': 'B',   #  β
	u'\u03FD': 'C',   #  Ͻ
	u'\u0394': 'D',   #  Δ
	u'\u03A3': 'E',   #  Σ
	u'\u222B': 'F',   #  ∫
	u'\u0039': 'G',   #  9
	u'\u03E6': 'H',   #  Ϧ
	u'\u00A6': 'I',   #  ¦
	u'\u03c4': 'J',   #  τ
	u'\u03DF': 'K',   #  ϟ
	u'\u03BB': 'L',   #  λ
	u'\u16D7': 'M',   #  ᛗ
	u'\u0272': 'N',   #  ɲ
	u'\u03B8': 'O',   #  θ
	u'\u220F': 'P',   #  ∏
	u'\u2d55': 'Q',   #  ⵕ
	u'\u0281': 'R',   #  ʁ
	u'\u00A7': 'S',   #  §
	u'\u002B': 'T',   #  +
	u'\u00B5': 'U',   #  µ
	u'\u2714': 'V',   #  ✔
	u'\u03C9': 'W',   #  ω
	u'\u2715': 'X',   #  ✕
	u'\u00A5': 'Y',   #  ¥
	u'\u0240': 'Z'    #  ɀ
}

final = ""

f = open('theplantation.txt', 'r')
message = unicode(f.read(), "utf-8")

skipthese = ['+', '9']

for char in message:
	if char != ' ' and char != '\n':
		if char not in skipthese:
			newchar = translation[char]
			final = final + newchar
		else:
			if char == "+":
				final = final + 'T'
			elif char == "9":
				final = final + 'G'
	else:
		if char == ' ':
			final = final + ' '
		elif char == '\n':
			final = final + '\n'
print(final)

```

## Flag

```none
h4ck1t{massonsareeverywherelookbehindyou}
```