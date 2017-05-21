# Wait!!

### Challenge
- **Competition:** FIT-HACK 2017
- **Category:** Web
- **Points:** 50

> Please wait one minute
> https://wait.problem.ctf.nw.fit.ac.jp


### Solution
THE TIMER IS A RUSE.  Reading through the JavaScript reveals a URL.  Visiting the URL gives a Base 64 encoded string:

`RklUe2MzUnZjSE4wYjNCemRHOXd9VGltZeKAmXMgdXA=`

This string decodes as:

`RklUe2MzUnZjSE4wYjNCemRHOXd9 -> b64 decode = FIT{c3RvcHN0b3BzdG9w}`
`VGltZeKAmXMgdXA=  -> b64 decode = Time's Up`

There's our flag!


### Flag

`FIT{c3RvcHN0b3BzdG9w}`