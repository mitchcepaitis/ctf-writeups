# iLs

### Challenge
- **Competition:** School CTF 2016
- **Category:** Forensics
- **Points:** 300

> Famed school pentester Johnny Droptables is still improving his skills in computer security. Unfortunately it’s not always harmless for others. Some days ago he got access to server with very important information. He has created a great amount of folders and left a message:
> 
> Olololo! Storing secret data on server accessible from the Internet with such a password… Search now your file in these bunch of folders with the same files. I hope you learned your lesson and henceforth you will be careful with your data.
>
> $ ssh -p31337 guest@ssh.task.school-ctf.org
>
> (password guest)

### Solution

The goal of this challenge was to find a non-empty file which contained the flag.  This one file was hidden somewhere amongst many others, which were themselves spread across many different layers of folders.

Connecting to the server dropped me into a very limited shell.  I tried to use the typical escape techniques, none of which worked.  The useful allowed commands were `cd` and `cat`.  Trying to `cat 1/*` or something similar would crash the connection to the server.  I decided to write a script which would create a text file with all possible file locations, and use it as input to the limited SSH shell.

The command that I used to feed the possible folder and file combinations to the SSH shell was as follows:

`sshpass -p 'guest' ssh -p31337 guest@ssh.task.school-ctf.org < ils.txt 1> results.txt 2>/dev/null`

Let me explain this command a little bit, in case it isn't obvious.

- `sshpass -p 'guest'` is simply a command to pass the SSH password to the `ssh` program.  I (mistakenly) thought that I needed this, but in retrospect it was probably not necessary.
- `ssh -p31337 guest@ssh.task.school-ctf.org` is the initiation of an SSH connection to the server __ssh.task.school-ctf.org__ on port __31337__ as user __guest__.  Remember, the password was supplied by the previous `sshpass` command.
- `<ils.txt` redirects input to the `ssh` command.  Instead of using the keyboard, the file __ils.txt__ is used as input.  Each line in __ils.txt__ contains a `cat` command followed by a possible location for the target file.
- `1> results.txt` redirects the standard output from the command line to the specified file, __results.txt__.  This simply prints what you would have seen on screen to the file.
- `2>/dev/null` redirects the standard error output to a device used for erasing the data that it receives.  This effectively keeps any errors from being printed. 

After running that command and looking through the created __results.txt__ file, the flag was easily found.


### Script (Bash)

```bash
#!/bin/bash
commandcat="cat "
file="somefile"
slash="/"
for a in 1 2 3 4 5 6
do
	for b in 1 2 3 4 5 6
	do
		for c in 1 2 3 4 5 6
		do
			for d in 1 2 3 4 5 6
			do
				for e in 1 2 3 4 5 6
				do
					for f in 1 2 3 4 5 6
					do
						echo "$commandcat$a$slash$b$slash$c$slash$d$slash$e$slash$f$slash$file" >> ils.txt
					done
				done
			done
		done
	done
done
exit 0
```

### Flag

`SchoolCTF{5UPP3r_1D3n71f13R_Fl49}`