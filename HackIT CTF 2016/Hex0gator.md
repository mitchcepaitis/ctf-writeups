---
layout: post
title: H4ckIT CTF 2016 - Hex0gator (PPC 250)
date: 2016-10-03 12:15:00
categories: 
- CTF 
- H4ckIT 2016
---
# Hex0gator

### Challenge
- **Competition:** HackIT CTF 2016
- **Category:** PPC
- **Points:** 250
- **File:** [100](./files/100)

> All Experts of The Silver Shield Project can't decipher the intercepted data. Who knows, maybe you can do it?

### Solution

Before I could attempt to do anything at all, I needed to know what kind of file I was given.  After transferring it over to Linux, it had an icon for a compressed file type, like Zip.  Running the `file` command confirmed this.  I peeked inside of the compressed file by double clicking the icon and was greeted with a folder, named __work_folder__.  Inside this delightful little folder was another file.  Named __99__.

Oh.  It's _that_.

This was a black hole of compressed files within compressed files.  I got a little script started that would unzip the file, moving the __work_folder__ out of the archive, then move the next compressed file out of the __work_folder__, and finally delete the __work_folder__.  This left me with just the new compressed file.  The script would then repeat the process until it hit a filetype that wasn't accounted for in the code.

It's kind of a mess of a script, I'll admit.  Surely there is a Python way to unzip and untar and unrar.  I think it even ends by erroring out...  But I got the flag in the end.  I definitely want to improve my scripting.


### Script (Python)

```python
import sys
import os
import subprocess
import shutil

# file --mime-type
# zip  == application/zip
# gzip == application/gzip
# rar  == application/x-rar
# tar  == application/x-tar

filename = sys.argv[1]


filetype = subprocess.check_output(['file', '--mime-type', filename])
if "zip" in filetype and "gzip" not in filetype:
	subprocess.call(['unzip', filename])
elif "gzip" in filetype:
	subprocess.call(['gunzip', filename])
elif "rar" in filetype:
	subprocess.call(['unrar', 'x', filename])
elif "tar" in filetype:
	subprocess.check_call(['tar', '-xvf', file])
else:
	# Print the filetype so it can be added to the script
	print(filetype)



def unzip(file):
		filetype = subprocess.check_output(['file', '--mime-type', file])
		print(filetype)
		if "zip" in filetype and "gzip" not in filetype:
			subprocess.check_call(['unzip', file])
			os.remove(file)
		elif "gzip" in filetype:
			subprocess.check_call(['tar', '-xvzf', file])
			os.remove(file)
		elif "rar" in filetype:
			subprocess.check_call(['unrar', 'x', file])
			os.remove(file)
		elif "tar" in filetype:
			subprocess.check_call(['tar', '-xvf', file])
			os.remove(file)
		else:
			print(filetype)

while True:
	if os.listdir('work_folder'):
		files = os.listdir('work_folder')

		for file in files:
			shutil.move('work_folder/'+file, '.')
			shutil.rmtree('work_folder')
			unzip(file)
	else:
		break
```

### Flag

`h4ck1t{0W_MY_G0D_Y0U_M4D3_1T}`