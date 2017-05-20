# Blinky DLINK

### Challenge
- **Competition:** School CTF 2016
- **Category:** Joy
- **Points:** 500
- **File:** [blink.mp4](./files/blink.mp4)

> Today my router went crazy and showed me a little light show. Does he think he is a discoball or is he trying to tell me something?

### Solution

The supplied video was shot in a dark room and showed a device alternating between lighting up all eight of its lights and a specific combination of some lights on and some lights off.  The fact that there were eight lights was an immediate clue that these lights were programmed to light up such that a message encoded in 8-bit binary could be interpreted.  The following lists the various sequences of lights shown in the video, 1 indicates on and 0 indicates off:

```none
01010011
01100011
01101000
01101111
01101111
01101100
01000011
01010100
01000110
01111011
01000010
01100101
01100101
01110000
01011111
01100010
01101100
01101001
01101110
01101011
01011111
01100100
01101111
01011111
01100100
01100101
01100101
01011111
01100100
01101001
01101100
01101001
01011111
01100100
01101111
01111101
```

Converting that from binary to ascii gave the flag.

### Flag

`SchoolCTF{Beep_blink_do_dee_dili_do}`