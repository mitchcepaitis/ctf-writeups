# number

### Challenge
- **Competition:** FIT-HACK 2017
- **Category:** Binary
- **Points:** 50
- **File:** [number.zip](./files/number.zip)

> Number is beautiful


### Solution
Finding the input which the program is searching for is how I solved this challenge.  Looking through the program's assembly instructions, I found 2 instructions which give the answer.  The first instruction subtracts 26 (0x1a) from the user input.

`sub eax, 0x1a`

Shortly after, the second instruction compares the user input, minus 26, to the constant number 1126 (0x466).

`cmp eax, 0x466`

If the `cmp` instruction returns zero, the flag is printed.  The `cmp` instruction will return zero if the following is true:

`user input - 26 = 1126`

If the user input is initially __1152__, this condition will be met and the flag will be printed.  The flag ends up being [Euler's number](https://en.wikipedia.org/wiki/E_(mathematical_constant)).


### Flag

`FIT{2.718281828}`