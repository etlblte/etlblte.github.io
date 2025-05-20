---
title: CryptoHack Hex
date: 2025-05-20 13:01:00 +/-0500
categories: [ctf]
tags: [cryptohack, intro_to_cryptohack, cryptography, programming, python] 
math: true
---

### Goal
> Included below is a flag encoded as a hex string. Decode this back into bytes to get the flag.
```python
0x63727970746f7b596f755f77696c6c5f62655f776f726b696e675f776974685f6865785f737472696e67735f615f6c6f747d
```
### Solution
[Hexadecimal](https://en.wikipedia.org/wiki/Hexadecimal) or "hex" is another way we can encode data. It's commonly used due to its portability across different systems. Hex uses a Base 16 system where a character represents a number 0-15. To avoid using two characters for numbers past 9, hex opts to use letters starting from 'a' instead. So we have 'a' representing 10, then 'b' representing 11, all the way to 'f' representing 15.  

Integers are represented as Base 10 numbers, where each character represents a number from 0 to 9. Reading the value of any number we sum each character multiplied by 10 to the power of its index from right to left. To illustrate this, here is how the Base 10 system works:

$$
415 = 5(10^0) + 1(10^1) + 4(10^2)= 5(1) + 1(10) + 4(100) = 5 + 10 + 400= 415
$$

Hex works the same way except we use 16 instead of 10 as our base. Say we have a hex encoded number `0x19F`. Here the prefix `0x` is typically used to indicate a number is represented in hex or Base 16. So we are really just looking at the value `19F`. This may look confusing but let's break it down:

$$
\text{0x19F} = \text{F}(16^0) + 9(16^1) + 1(16^2)= 15(1) + 9(16) + 1(256)= 15 + 144 + 256 = 415
$$

It's the same number! Luckily this process is much easier using Python. There are built-in functions that automatically convert a hexadecimal number to Base 10 and then from integer to letter. This is done using `bytes.fromhex()` which takes in a string containing hex characters and returns a byte string of its human readable translation. So, we can convert the given hex data to a string with one line of code. I append a call to `.decode()` since the function call returns a byte string. The function `.decode()` takes in a byte string and converts it to a regular ASCII string. There's not much difference in the output except for the fact that the byte string will output as `b"string"` and the ASCII string will print without the `b` and instead just show `string`. Altogether we can translate the given hex as follows: 
```python
ciphertext= "63727970746f7b596f755f77696c6c5f62655f776f726b696e675f776974685f6865785f737472696e67735f615f6c6f747d"

plaintext= bytes.fromhex(ciphertext).decode()

print(f"Flag: {plaintext}")

# ---Output---
# Flag: crypto{You_w...}
```

### Summary
Although this was only a few lines of code, there is a lot going on behind the scenes. We learned about how numbers are represented with various Bases and how we can translate between them. Using Python we converted a given hexadecimal string to an ASCII string using the built in `bytes.fromhex()` function. 
