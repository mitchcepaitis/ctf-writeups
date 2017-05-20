# Wonder Web

### Challenge
- **Competition:** School CTF 2016
- **Category:** Web
- **Points:** 100

> In the year 2337 we finally secured the WEB! Now we have headers for anything you want. Everybody can make their site secure just by setting ALL the headers on the server.
> 
> I just ported a demo page from the future to your time, so you can look how wonderful it is!
> 
> http://wonder.task.school-ctf.org


### Solution

The challenge text was fairly obvious about where to begin searching for the flag.  Using the __Live HTTP Headers__ extension for Firefox, I read through the headers that are transmitted when accessing the given web page.  There were all kinds of fantasy headers, some of which ended up containing information about the flag.  An example header:

`Flag-First-Part-Is-Here: encoding=base64; part1=U2Nob29sQ1RGezUwbTNkNHk=;`

Putting together the 'clues', this header translates to __"SchoolCTF{50m3d4y"__.  This is the obvious beginning of the flag.  All of the relevant headers were:

```none
Flag-First-Part-Is-Here: encoding=base64; part1=U2Nob29sQ1RGezUwbTNkNHk=;

Task: category=joy; ucucuga=sure; encoding=none; justString=true; flagPresent=1; flagPart2=17; flagPart4=b3;

X-ShellShock-vector: (){;}; echo "Want flag?"; python -c 'part3="77316c6c"; print part3.decode("hex")';

Content-Meaning: none; flag-part-number=5 part-content=54f3};

Flag-Parts-Connector: character=_; charCode=95; hexCharCode=0x5f;
```

The different fake headers gave the following different parts:


```none
SchoolCTF{50m3d4y

17

w1ll

b3

54f3}

_
```

Putting it all together gave the final flag.



### Flag

`SchoolCTF{50m3d4y_17_w1ll_b3_54f3}`