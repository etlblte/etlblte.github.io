---
title: CryptoHack ASCII
date: 2025-05-20 13:00:00 +/-0500
categories: [ctf]
tags: [cryptohack, intro_to_cryptohack, cryptography, programming, python]     
---

### Goal
> Using the below integer array, convert the numbers to their corresponding ASCII characters to obtain a flag.
```python
[99, 114, 121, 112, 116, 111, 123, 65, 83, 67, 73, 73, 95, 112, 114, 49, 110, 116, 52, 98, 108, 51, 125]
```

### Solution
[ASCII](https://www.ascii-code.com/) is a standard code used to represent letters using integers. The most commonly used "printable" characters are those found on our keyboard and are reserved within the range 0 to 127. In Python we can convert an integer to its corresponding ASCII letter representation using the `chr()` function. Conversely, if we want to convert a letter to an integer we can use `ord()`. Here we only need to translate an ASCII encoded string so we'll use `chr()`. 
```python
ciphertext= [99, 114, 121, 112, 116, 111, 123, 65, 83, 67, 73, 73, 95, 112, 114, 49, 110, 116, 52, 98, 108, 51, 125]
plaintext= ""

for ascii_letter in ciphertext:
	plaintext += chr(ascii_letter)

print(f"Flag: {plaintext}")

# ---Output---
# Flag: crypto{ASC...}
```
### Summary
Here we letter how letters can be encoded as integers using the ASCII standard. We also learned how to convert to and from ASCII using the two built-in Python functions `chr()` and `ord()`. 
