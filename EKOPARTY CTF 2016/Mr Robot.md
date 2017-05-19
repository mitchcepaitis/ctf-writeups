# Mr. Robot
*Web 25*

### Challenge

> Disallow it!


### Solution

The clues made this challenge painfully obvious that I needed to check out the __robots.txt__ file.  Sure enough, there was an interesting entry:

```none
User-agent: *
Disallow: /static/wIMti7Z27b.txt
```

The file `/static/wIMti7Z27b.txt` contained the flag.  Navigating to it displayed the flag in the browser window.

### Flag

```none
EKO{robot_is_following_us}
```