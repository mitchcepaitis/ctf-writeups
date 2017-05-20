# Cats

### Challenge
- **Competition:** RC3 CTF 2016
- **Category:** Crypto
- **Points:** 300
- **File:** [output_rXpTX3.gif](./files/output_rXpTX3.gif)

> Figure out the purrr-fect flag right meow!
>
> http://gifmaker.cc/PlayGIFAnimation.php?folder=20161118085vPLNEX4hvpUMFkNV2NNEl&file=output_ztMAad.gif
>
> Here, I'll give you the first half of the flag: "RC3-2016-" so all you need to do is figure out the other eight characters.

### Solution

The given .gif was a series of static images with differing numbers of cats in each frame.  I started by counting and logging the number of cats in each frame:

```none
1 - 14
2 - 9
3 - 1
4 - 20
5 - 23
6 - 15
7 - 5
8 - 13
```

All of these numbers were within alphabetical range, so converting the numbers to their corresponding letters in the alphabet gave:

`NIATWOEM`

This seemed like it was backward (notice the "WOEM" is backward "MEOW" and the challenge is all about cats).  I reversed it and got the flag.

### Flag

`MEOWTAIN`