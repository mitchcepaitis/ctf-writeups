# Vigenere

### Challenge
- **Competition:** SECCON CTF 2016
- **Category:** Crypto
- **Points:** 100

> Vigenere
> 
> k: ????????????
> p: SECCON{???????????????????????????????????}
> c: LMIG}RPEDOEEWKJIQIWKJWMNDTSR}TFVUFWYOCBAJBQ
> 
> k=key, p=plain, c=cipher, md5(p)=f528a6ab914c1ecf856a1d93103948fe
> 
>  |ABCDEFGHIJKLMNOPQRSTUVWXYZ{}
> -+----------------------------
> A|ABCDEFGHIJKLMNOPQRSTUVWXYZ{}
> B|BCDEFGHIJKLMNOPQRSTUVWXYZ{}A
> C|CDEFGHIJKLMNOPQRSTUVWXYZ{}AB
> D|DEFGHIJKLMNOPQRSTUVWXYZ{}ABC
> E|EFGHIJKLMNOPQRSTUVWXYZ{}ABCD
> F|FGHIJKLMNOPQRSTUVWXYZ{}ABCDE
> G|GHIJKLMNOPQRSTUVWXYZ{}ABCDEF
> H|HIJKLMNOPQRSTUVWXYZ{}ABCDEFG
> I|IJKLMNOPQRSTUVWXYZ{}ABCDEFGH
> J|JKLMNOPQRSTUVWXYZ{}ABCDEFGHI
> K|KLMNOPQRSTUVWXYZ{}ABCDEFGHIJ
> L|LMNOPQRSTUVWXYZ{}ABCDEFGHIJK
> M|MNOPQRSTUVWXYZ{}ABCDEFGHIJKL
> N|NOPQRSTUVWXYZ{}ABCDEFGHIJKLM
> O|OPQRSTUVWXYZ{}ABCDEFGHIJKLMN
> P|PQRSTUVWXYZ{}ABCDEFGHIJKLMNO
> Q|QRSTUVWXYZ{}ABCDEFGHIJKLMNOP
> R|RSTUVWXYZ{}ABCDEFGHIJKLMNOPQ
> S|STUVWXYZ{}ABCDEFGHIJKLMNOPQR
> T|TUVWXYZ{}ABCDEFGHIJKLMNOPQRS
> U|UVWXYZ{}ABCDEFGHIJKLMNOPQRST
> V|VWXYZ{}ABCDEFGHIJKLMNOPQRSTU
> W|WXYZ{}ABCDEFGHIJKLMNOPQRSTUV
> X|XYZ{}ABCDEFGHIJKLMNOPQRSTUVW
> Y|YZ{}ABCDEFGHIJKLMNOPQRSTUVWX
> Z|Z{}ABCDEFGHIJKLMNOPQRSTUVWXY
> {|{}ABCDEFGHIJKLMNOPQRSTUVWXYZ
> }|}ABCDEFGHIJKLMNOPQRSTUVWXYZ{
> 
> Vigenere cipher:
> https://en.wikipedia.org/wiki/Vigen%C3%A8re_cipher


### Solution

A Vigenere cipher incorporates a changing Caesarian Shift, or ROT Shift.  Instead of using the same number to shift (like 13 for ROT13), each successive character is shifted by a different amount, based on a key.  This key is used to both encrypt and decrypt, and finding the key was the approach I used to complete this challenge.

We are given the key length, represented by question marks, and we know the first 7 characters of the plaintext message (SECCON{).  Using this information it is possible to get to the following point:

```none
k: VIGENER?????VIGENER?????VIGENER?????VIGENER
p: SECCON{?????BCDEDEF?????KLMNOPQ?????VWXYYZ}
c: LMIG}RPEDOEEWKJIQIWKJWMNDTSR}TFVUFWYOCBAJBQ
```

From this much of the plaintext message, it looks like the message just lists the alphabet with a few modifications throughout.  It is reasonable to guess that the key would contain the entire word `VIGENERE`, and making that leap gives:

```none
k: VIGENERE????VIGENERE????VIGENERE????VIGENER
p: SECCON{A????BCDEDEFG????KLMNOPQR????VWXYYZ}
c: LMIG}RPEDOEEWKJIQIWKJWMNDTSR}TFVUFWYOCBAJBQ
```

From this point it took some trial and error to find that the next two characters in the key were probably "CO", giving `VIGENERECO??`.  From this point it made sense that the last two characters *could* be "DE", giving `VIGENERECODE`.  This turned out to be the correct key, which provided the means to decrypt the entire flag.

### Flag

`SECCON{ABABABCDEDEFGHIJJKLMNOPQRSTTUVWXYYZ}`