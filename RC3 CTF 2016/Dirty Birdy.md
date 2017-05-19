---
layout: post
title: RC3 CTF 2016 - Dirty Birdy (Forensics 400)
date: 2016-11-22 12:11:00
categories: 
- CTF 
- RC3 CTF 2016
---

## Challenge

> Description: We had an employee that was up to no good. Our SIEM caught him uploading files to a website from our file server but we canceled the transmission. We currently have an image of home directory that we store on our server. Take a look for yourself on what he stole.
>
> Download Link: https://drive.google.com/file/d/0Bw7N3lAmY5PCUWExQUJVZGVySXc/view?usp=sharing

###### Files

1. dtrump.img.zip


## Solution

After extracting and mounting the image, I immediately found a suspicious directory subtly named __secretfiles__.  This directory had the following contents:

```bash
$ ls -al
total 31
dr-xr-xr-x  3 root root  2048 Nov 18 18:20 .
dr-xr-xr-x 18 root root  4096 Nov 18 18:44 ..
-r--r--r--  1 root root    13 Nov 18 18:02 document.txt
dr-xr-xr-x  8 root root  2048 Nov 18 18:11 .git
-r--r--r--  1 root root    14 Nov 18 18:09 README.md
-r--r--r--  1 root root 22367 Nov 18 17:59 Workbook1.xlsx.gpg

$ cat README.md
# supersecret
$ cat document.txt
password123

file Workbook1.xlsx.gpg 
Workbook1.xlsx.gpg: PGP RSA encrypted session key - keyid: 1246B951 2DB12CE2 RSA (Encrypt or Sign) 1024b .
```

Ok, so I need to look for a PGP key of some sort...  Let's see what has been version controlled in the __.git__ directory:

```bash
$ cd .git
$ git log -p
commit 5fe6ff3f3eaf629e3e7cdc8a2ae456253b186370
Author: ThugG <nope@gmail.com>
Date:   Fri Nov 18 15:10:49 2016 -0800

    initial commit

diff --git a/private.key b/private.key
new file mode 100644
index 0000000..78a8994
--- /dev/null
+++ b/private.key
@@ -0,0 +1,48 @@
+-----BEGIN PGP PRIVATE KEY BLOCK-----
+Version: GnuPG v1
+
+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
+bOMsAtIU8D68fbCXhp0VRNs5
+=xRo0
+-----END PGP PRIVATE KEY BLOCK-----
```

Well that's convenient.  Next, I need to paste the newly found private key into a file to import.  When copying the private key block, the plus sign at the beginning of each line must be removed.  I pasted the private key block into a file called __private.key__.

Next, the command to import the private key: 

`gpg --import private.key`

Then, the command to decrypt the target file: 

`gpg --output Workbook1.xlsx --decrypt Workbook1.xlsx.gpg`

Now I had a decrypted .xlsx file.  I attempted to open it, but was greeted with an alert that I needed a password in order to view the file.  Dang.

Wait.  I have the password!  The file __document.txt__ had what seemed to be a password in it.  Sure enough, it worked.  I opened the file and found some kind of financial report with no relevant information.  However, there was a second sheet in the file.  Unfortunately it only contained blank cells.  I did a search for the flag string "RC3-2016" and one instance of this string was found.

The very last cell in the second sheet contained the flag typed in microscopic text.

## Flag
```none
RC3-2016-SNEAKY21
```