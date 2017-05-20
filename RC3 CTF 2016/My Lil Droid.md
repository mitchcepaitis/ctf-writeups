# My Lil Droid

### Challenge
- **Competition:** RC3 CTF 2016
- **Category:** Forensics
- **Points:** 100
- **File:** [youtube.apk](./files/youtube.apk)

> Sometimes not all files are needed.
>
> Download Link: https://drive.google.com/file/d/0Bw7N3lAmY5PCOFNQZFgtSVlFZ3M/view?usp=sharing

### Solution

Finding the flag for this challenge was extremely quick and painless.  In order to open and view the contents of __youtube.apk__, I renamed it to __youtube.zip__ and extracted the contents.  I skimmed through a few files before I came to the file __build-data.properties__.  I skimmed through this file as well, but noticed what looked like a Base64 encoded string at the end of the file that looked extremely out of place:

`UkMz-2016-R09URU0yMQ==`

Base 64 decoding this string gave the flag.

### Flag

`RC3-2016-GOTEM21`