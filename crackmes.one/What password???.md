**Platform:**  crackmes.one
**Category:**  String / data encryption, xor
**Difficulty:**  1.7
**Date:** 2026-08-23  
**Tags:** string / data encryption, xor

---

## Overview
We are given a file and need to find the password in order to get the correct message

## Reconnaissance
Do a little test first see what happens, how the program acts:

![](../assets/what%20password???/wp1.png)

Load into ghidra 

![](../assets/what%20password???/wp2.png)

This is the decompiled code of the program, does not seem very complicated, I've renamed some of the variables, it's a basic for, as we can see, in the variable `toFind`, we store a character from the `pw` vector, xor it with key `0x27` and add `i` to it, then the program checks with the input we gave and increases the value for `i` and `counter`, so basically the formula is  `toFind = (pw[counter]^0x27) + 2*counter or i where i belongs to multiple of 2 starting with 2`, let's check the bytes of `pw` 

![](../assets/what%20password???/wp3.png)

`4e 49 1d 42 7c 41 7c 33 75 6a 6b 3c 7e 7f cb`, these are the bytes used for making up the password, we will write a simple python program to compute the password easier

```python
bytes = [0x4e, 0x49, 0x1d, 0x42, 0x7c, 0x41, 0x7c, 0x33, 0x75, 0x6a, 0x6b, 0x3c, 0x7e, 0x7f, 0xcb]

counter = 2
out = ""

for b in bytes:
	c = (b ^ 0x27) + counter
	out = out + chr(c)
	counter = counter + 2

print(out)
```

And we can check to see if we were right:

![](../assets/what%20password???/wp4.png)

The password is actually without the last character, the last character `0xcb` was meant for `\n` this is why it formats this way when applied with the formula
## Flag 
`kr@meri$dab3st` 