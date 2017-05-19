---
layout: post
title: SECCON CTF 2016 - Vigenere (Crypto 100)
date: 2016-12-11 02:00:00
categories: 
- CTF 
- SECCON CTF 2016
---

## Challenge

> Vigenere
> 
> k: ????????????<br>
> p: SECCON{???????????????????????????????????}<br>
> c: LMIG}RPEDOEEWKJIQIWKJWMNDTSR}TFVUFWYOCBAJBQ<br>
> 
> k=key, p=plain, c=cipher, md5(p)=f528a6ab914c1ecf856a1d93103948fe
> 
>  |ABCDEFGHIJKLMNOPQRSTUVWXYZ{}<br>
> -+----------------------------<br>
> A|ABCDEFGHIJKLMNOPQRSTUVWXYZ{}<br>
> B|BCDEFGHIJKLMNOPQRSTUVWXYZ{}A<br>
> C|CDEFGHIJKLMNOPQRSTUVWXYZ{}AB<br>
> D|DEFGHIJKLMNOPQRSTUVWXYZ{}ABC<br>
> E|EFGHIJKLMNOPQRSTUVWXYZ{}ABCD<br>
> F|FGHIJKLMNOPQRSTUVWXYZ{}ABCDE<br>
> G|GHIJKLMNOPQRSTUVWXYZ{}ABCDEF<br>
> H|HIJKLMNOPQRSTUVWXYZ{}ABCDEFG<br>
> I|IJKLMNOPQRSTUVWXYZ{}ABCDEFGH<br>
> J|JKLMNOPQRSTUVWXYZ{}ABCDEFGHI<br>
> K|KLMNOPQRSTUVWXYZ{}ABCDEFGHIJ<br>
> L|LMNOPQRSTUVWXYZ{}ABCDEFGHIJK<br>
> M|MNOPQRSTUVWXYZ{}ABCDEFGHIJKL<br>
> N|NOPQRSTUVWXYZ{}ABCDEFGHIJKLM<br>
> O|OPQRSTUVWXYZ{}ABCDEFGHIJKLMN<br>
> P|PQRSTUVWXYZ{}ABCDEFGHIJKLMNO<br>
> Q|QRSTUVWXYZ{}ABCDEFGHIJKLMNOP<br>
> R|RSTUVWXYZ{}ABCDEFGHIJKLMNOPQ<br>
> S|STUVWXYZ{}ABCDEFGHIJKLMNOPQR<br>
> T|TUVWXYZ{}ABCDEFGHIJKLMNOPQRS<br>
> U|UVWXYZ{}ABCDEFGHIJKLMNOPQRST<br>
> V|VWXYZ{}ABCDEFGHIJKLMNOPQRSTU<br>
> W|WXYZ{}ABCDEFGHIJKLMNOPQRSTUV<br>
> X|XYZ{}ABCDEFGHIJKLMNOPQRSTUVW<br>
> Y|YZ{}ABCDEFGHIJKLMNOPQRSTUVWX<br>
> Z|Z{}ABCDEFGHIJKLMNOPQRSTUVWXY<br>
> {|{}ABCDEFGHIJKLMNOPQRSTUVWXYZ<br>
> }|}ABCDEFGHIJKLMNOPQRSTUVWXYZ{<br>
> 
> Vigenere cipher:<br>
> https://en.wikipedia.org/wiki/Vigen%C3%A8re_cipher


## Solution

A Vigenere cipher incorporates a changing Caesarian Shift, or ROT Shift.  Instead of using the same number to shift (like 13 for ROT13), each successive character is shifted by a different amount, based on a key.  This key is used to both encrypt and decrypt, and finding the key was the approach I used to complete this challenge.

We are given the key length, represented by question marks, and we know the first 7 characters of the plaintext message (SECCON{).  Using this information it is possible to get to the following point:

```none
k: VIGENER?????VIGENER?????VIGENER?????VIGENER
p: SECCON{?????BCDEDEF?????KLMNOPQ?????VWXYYZ}
c: LMIG}RPEDOEEWKJIQIWKJWMNDTSR}TFVUFWYOCBAJBQ
```

From this much of the plaintext message, it looks like the message just recites the alphabet with a few modifications throughout.  It is reasonable to guess that the key would contain the entire word `VIGENERE`, and making that leap gives:

```none
k: VIGENERE????VIGENERE????VIGENERE????VIGENER
p: SECCON{A????BCDEDEFG????KLMNOPQR????VWXYYZ}
c: LMIG}RPEDOEEWKJIQIWKJWMNDTSR}TFVUFWYOCBAJBQ
```

From this point it took some trial and error to find that the next two characters in the key were probably "CO", giving `VIGENERECO??`.  From this point it made sense that the last two characters *could* be "DE", giving `VIGENERECODE`.  This turned out to be the correct key, which provided the means to decrypt the entire flag.

## Flag
```none
SECCON{ABABABCDEDEFGHIJJKLMNOPQRSTTUVWXYYZ}
```