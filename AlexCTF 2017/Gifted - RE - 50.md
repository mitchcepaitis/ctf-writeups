# Gifted

### Challenge
- **Competition:** Alex CTF 2017
- **Category:** RE
- **Points:** 50
- **File:** [gifted](./files/gifted)

> Challenge Text


### Solution

This was a simple reverse engineering challenge which was quickly completed by simply running `strings` against the given __gifted__ binary.

```bash
$ strings gifted
/lib/ld-linux.so.2
libc.so.6
_IO_stdin_used
exit
__isoc99_scanf
puts
printf
malloc
strcmp
__libc_start_main
__gmon_start__
GLIBC_2.7
GLIBC_2.0
PTRh
QVh+
UWVS
t$,U

[^_]
Enter the flag:
AlexCTF{Y0u_h4v3_45t0n15h1ng_futur3_1n_r3v3r5ing}
You got it right dude!
Try harder!
;*2$"
GCC: (GNU) 6.1.1 20160721 (Red Hat 6.1.1-4)
GCC: (GNU) 6.2.1 20160916 (Red Hat 6.2.1-2)
.shstrtab
.interp
.note.ABI-tag
.note.gnu.build-id
.gnu.hash
.dynsym
.dynstr
.gnu.version
.gnu.version_r
.rel.dyn
.rel.plt
.init
.plt.got
.text
.fini
.rodata
.eh_frame_hdr
.eh_frame
.init_array
.fini_array
.jcr
.dynamic
.got.plt
.data
.bss
.comment
```


### Flag

`AlexCTF{Y0u_h4v3_45t0n15h1ng_futur3_1n_r3v3r5ing}`