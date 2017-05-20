# Virus

### Challenge
- **Competition:** School CTF 2016
- **Category:** Steganography
- **Points:** 200
- **File:** [task.png](./files/task.png)

> My computer is infected with a virus which has hidden all my files.
>
> Can you help me to find my data?

### Solution

The given image showed only a grumpy cat.  Running `foremost` against __task.png__ produced several files which were embedded within.  The flag was found displayed in one of two JPG files which were recovered using `foremost`:

![schoolctf-2016-virus.jpg](./img/schoolctf-2016-virus.jpg "schoolctf-2016-virus.jpg")


### Flag

`SchoolCTF{v1rus_ar7_is_r34l_art}`