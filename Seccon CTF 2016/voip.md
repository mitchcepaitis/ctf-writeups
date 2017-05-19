---
layout: post
title: SECCON CTF 2016 - VoIP (Forensics 100)
date: 2016-12-11 02:05:00
categories: 
- CTF 
- SECCON CTF 2016
---

## Challenge

> VoIP
>
> Extract a voice.
> The flag format is SECCON{[A-Z0-9]}.

##### Files

1. voip.pcap


## Solution

This was an extremely interesting introduction to a feature of Wireshark that can reconstruct audio of VoIP calls.  

First, open the __Telephony__ menu, then click __VoIP Calls__.
![seccon-2016-voip1.jpg](/img/2016/seccon-2016-voip1.jpg "seccon-2016-voip1.jpg")
<br><br><br><br>
In the next popup window, highlight the stream and click the __Play Streams__ button.
![seccon-2016-voip2.jpg](/img/2016/seccon-2016-voip2.jpg "seccon-2016-voip2.jpg")
<br><br><br><br>
In the final popup window, click the play button (triangle shape) to playback the audio of the VoIP call.
![seccon-2016-voip3.jpg](/img/2016/seccon-2016-voip3.jpg "seccon-2016-voip3.jpg")
<br><br>
The audio read back the flag in a robotic text-to-speech voice.

## Flag
```none
SECCON{9001IVR}
```