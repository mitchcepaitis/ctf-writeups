# Graphic Design

### Challenge
- **Competition:** RC3 CTF 2016
- **Category:** Forensics
- **Points:** 200
- **File:** [forensics200.obj](./files/forensics200.obj)

> The 3D Design students have been boasting about how they can trade sensitive information without anyone ever knowing. You’ve intercepted one of their USB’s and found this interesting file. Figure out what the hell is going on.
>
> Download Link: https://drive.google.com/file/d/0Bw7N3lAmY5PCTWg5YU1uNUk3cmc/view?usp=sharing
>
> -Your friendly neighborhood httpster

### Solution

What the heck is a .obj file?  Well, [Blender](https://www.blender.org) can import it, so I downloaded and launched it.  After importing this .obj file, I was greeted with the 3D model of a stegosaurus.  Neat!  After rotating the camera around for a while, it clipped into the model, and there was some text floating there.  I moved the stegosaurus model so the text was outside of it, and easy to read:

![rc3-2016-graphicdesign.jpg](./img/rc3-2016-graphicdesign.jpg "rc3-2016-graphicdesign.jpg")

This was a neat way to experience a type of software I've never used before.

### Flag

`RC3-2016-St3GG3rz`