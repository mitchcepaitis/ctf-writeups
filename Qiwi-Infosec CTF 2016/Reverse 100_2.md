# Reverse 100_2

### Challenge
- **Competition:** Qiwi-Infosec CTF 2016
- **Category:** Reverse
- **Points:** 100
- **File:** [task.pyc](./files/task.pyc)

> I have a snake. CrackMe!

### Solution

I've never worked with a python executable file before, but I quickly found the program __uncompyle2__ to do the job for me.  Decompiling the given .pyc gave the following result:

```python
# 2016.11.17 08:20:30 EST
#Embedded file name: task.py
import marshal
src = 'YwAAAAADAAAAGAAAAEMAAABz7wAAAGQBAGoAAGcAAGQCAGQDAGQEAGQFAGQGAGQHAGQIAGQJAGQKAGQLAGQMAGQNAGQOAGQPAGQMAGcPAERdHAB9AAB0AQB0AgB8AACDAQBkEAAXgwEAXgIAcToAgwEAfQEAdAMAZBEAgwEAfQIAfAIAfAEAawIAcuYAZAEAagAAZwAAZBIAZBMAZBQAZBUAZBYAZBcAZBgAZBkAZBoAZBsAZBwAZB0AZB4AZAsAZBwAZB8AZAMAZB0AZAgAZB4AZCAAZCEAZxYARF0VAH0AAHwAAGoEAGQiAIMBAF4CAHHGAIMBAEdIbgUAZCMAR0hkAABTKCQAAABOdAAAAAB0AQAAAF50AQAAADR0AQAAAEt0AQAAAGl0AQAAAC50AQAAAC90AQAAAE50AQAAAGp0AQAAAFB0AQAAAG90AQAAAD90AQAAAGx0AQAAADJ0AQAAAFRpAwAAAHMJAAAAWW91IHBhc3M6dAEAAABzdAEAAAB5dAEAAABudAEAAAB0dAEAAAA6dAEAAAB7dAEAAAB3dAEAAABxdAEAAABFdAEAAAA2dAEAAABmdAEAAABYdAEAAAB1dAEAAABhdAEAAAAxdAEAAAB9dAUAAABST1QxM3MFAAAATm8gOigoBQAAAHQEAAAAam9pbnQDAAAAY2hydAMAAABvcmR0CQAAAHJhd19pbnB1dHQGAAAAZGVjb2RlKAMAAAB0AQAAAGV0AwAAAHRtcHQGAAAAcGFzc3dkKAAAAAAoAAAAAHMHAAAAdGFzay5weVIcAAAAAgAAAHMKAAAAAAFfAQwBDAFvAQ=='.decode('base64')
code = marshal.loads(src)
exec code
+++ okay decompyling task.pyc 
# decompiled 1 files: 1 okay, 0 failed, 0 verify failed
# 2016.11.17 08:20:30 EST
```

This code essentially creates a __Python Code Object__ by decoding the Base64 string and interpreting it with [marshal](https://docs.python.org/2/library/marshal.html).  After researching how to reverse a code object, I found the [dis](https://docs.python.org/2/library/dis.html) library.  I simply substituted the `exec code` statement in the above script with a __dis__ statement to decompile the code object named __code__.  The output produced by this script included the following:

```none
6       119 LOAD_CONST               1 ('')
        122 LOAD_ATTR                0 (join)
        125 BUILD_LIST               0
        128 LOAD_CONST              18 ('s')
        131 LOAD_CONST              19 ('y')
        134 LOAD_CONST              20 ('n')
        137 LOAD_CONST              21 ('t')
        140 LOAD_CONST              22 (':')
        143 LOAD_CONST              23 ('{')
        146 LOAD_CONST              24 ('w')
        149 LOAD_CONST              25 ('q')
        152 LOAD_CONST              26 ('E')
        155 LOAD_CONST              27 ('6')
        158 LOAD_CONST              28 ('f')
        161 LOAD_CONST              29 ('X')
        164 LOAD_CONST              30 ('u')
        167 LOAD_CONST              11 ('o')
        170 LOAD_CONST              28 ('f')
        173 LOAD_CONST              31 ('a')
        176 LOAD_CONST               3 ('4')
        179 LOAD_CONST              29 ('X')
        182 LOAD_CONST               8 ('N')
        185 LOAD_CONST              30 ('u')
        188 LOAD_CONST              32 ('1')
        191 LOAD_CONST              33 ('}')
        194 BUILD_LIST              22
        197 GET_ITER            
    >>  198 FOR_ITER                21 (to 222)
        201 STORE_FAST               0 (e)
        204 LOAD_FAST                0 (e)
        207 LOAD_ATTR                4 (decode)
        210 LOAD_CONST              34 ('ROT13')
        213 CALL_FUNCTION            1
```

This seemed like a good lead to follow, so I constructed the string and applied a ROT-13 shift to the text.  This ended up being the flag:

`synt:{wqE6fxuofa4XNu1}` __==> ROT-13 ==>__ `flag:{jdR6skhbsn4KAh1}`


### Flag

`{jdR6skhbsn4KAh1}`