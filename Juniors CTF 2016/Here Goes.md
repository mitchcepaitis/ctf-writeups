# Here Goes!

### Challenge
- **Competition:** Juniors CTF 2016
- **Category:** Trivial Crypto Recon

This challenge starts by giving the following image with some sort of intentional cryptic characters:

![juniors-2016-heregoes1.png](./img/juniors-2016-heregoes1.png "juniors-2016-heregoes1.png")


### Solution

This whole CTF was themed around a TV show called Gravity Falls.  After a quick Google search for something like 'Gravity Falls decrypt', I found the following image which allowed me to decrypt the original message:

![juniors-2016-heregoes2.jpg](./img/juniors-2016-heregoes2.jpg "juniors-2016-heregoes2.jpg")

The decrypted message was:

```none
FIXPROB
LEMQUIC
KLYWITH
GALVANI
ZEDJETS
```
The flag was just all of this text as a single string with no spaces.

### Flag

`FIXPROBLEMQUICKLYWITHGALVANIZEDJETS`