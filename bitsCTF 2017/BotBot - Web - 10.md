# BotBot

### Challenge
- **Competition:** bitsCTF 2017
- **Category:** Web
- **Points:** 10

> Should not ask for the description of a 5 marker.
> botbot.bitsctf.bits-quark.org


### Solution
This challenge was solved by simply viewing the contents of the __robots.txt__ file on the server and navigating to the `Disallow`ed page.

__robots.txt__
```none
Useragent *
Disallow: /fl4g
```


### Flag

`BITCTF{take_a_look_at_googles_robots_txt}`