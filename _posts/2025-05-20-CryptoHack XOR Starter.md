```
---
title: CryptoHack XOR Starter
date: 2025-05-20 13:07:00 +/-0500
categories: [ctf]
tags: [cryptohack, intro_to_cryptohack, cryptography, programming, python]     
---
```

### Goal
> Given the string `label`, XOR each character with the integer `13`. Convert these integers back to a string and submit the flag as `crypto{new_string}`.

### Solution
XOR is a operation that is performed bit by bit on two values, which put simply checks if two bits are different. It has the following logic table:

| A   | B   | Output |
| --- | --- | ------ |
| 0   | 0   | 0      |
| 0   | 1   | 1      |
| 1   | 0   | 1      |
| 1   | 1   | 0      |

XOR also has a few more properties. If you XOR anything with 1 the bits will be flipped (0 becomes 1, and 1 becomes 0). Conversely, if you XOR anything with 0 it will stay the same (0 stays 0, and 1 stays 1). For this challenge we must XOR each letter in the string "label" with the number 13. Since XOR works on numbers, we must first convert each letter into a number. Then we can simply XOR each with 13. We can use the built-in function `ord()` in Python to do this. It converts a letter to its ASCII representation, which is an integer. The character to perform an XOR operation in Python is '`^`'. Altogether we have:


```python
a= "label"
b= 13
flag= ""

for character in a:
	decimal = ord(character) ^ b
	flag += chr(decimal)

print(f"Flag: {flag}")

# ---Output---
# Flag: al...
```

### Summary
In this challenge we learned about the basic logic behind the XOR operation and how it is implemented in Python. 