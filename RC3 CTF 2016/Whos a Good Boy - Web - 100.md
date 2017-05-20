# Who's a Good Boy?

### Challenge
- **Competition:** RC3 CTF 2016
- **Category:** Web
- **Points:** 100

> You’re trying to see the cute dog pictures on ctf.rc3.club. But every time you click on one of them, it brings you to a bad gateway.
>
> https://ctf.rc3.club:3000/
>
> -- Your friendly neighborhood webadmin

### Solution

A great lesson I learned during my time in the OSCP labs was to never ignore CSS files.  They aren't necessarily directly exploitable, but they can sometimes contain a useful piece of information that ultimately leads to discovering a vulnerability.  This challenge was a great instance of needing to explore CSS.

Looking at the head of the HTML source, I saw that the CSS file was named __doge.css__, which is pretty nonstandard.  Granted, the whole challenge was pretty nonstandard, but that was a clue to be sure.  The following text was contained in __doge.css__:

```css
.philarydufflebag{
	/*hiya*/
	/*compress your frontend*/
	/*here's a flag :)*/
	flag:RC3-2016-CanineSS
}
```

The flag was simply in the css.  Simple.

### Flag

`RC3-2016-CanineSS`