```
---
title: CryptoHack Favorite Byte
date: 2025-05-20 13:10:00 +/-0500
categories: [ctf]
tags: [cryptohack, intro_to_cryptohack, cryptography, programming, python]
math: true
---
```

### Goal
> I've hidden some data using XOR with a single byte, but that byte is a secret. Don't forget to decode from hex first.

```
73626960647f6b206821204f21254f7d694f7624662065622127234f726927756d
```
### Solution
From the challenge description, it appears that one byte was used to XOR each byte of the flag. Although we don't know the value of this secret byte, we can disclose it using the properties of the XOR operation. Say we have a value `C` which is derived from:

$$
C = A \oplus B
$$

Here, try to think of `C` as the first byte of the ciphertext. We know that the ciphertext is derived by XOR'ing each byte of the plaintext with the secret byte. So, we could say that `A` is the first byte of the plaintext and `B` is the secret byte. Although it may not be obvious at first, we now have all the information we need to find the secret byte! Remember the format of the flag? It always starts with the prefix `crypto{`. That means all we need to do is XOR the first byte of the ciphertext with the ASCII value of the character `c`.  This yields:

$$
B = C \oplus A
$$

This holds true via the self-inverse and identity properties of the XOR operation which we looked at in the previous challenge "XOR Properties".  To create a simple implementation of this in Python we can use the pwntools library which includes a custom function `xor()` that can perform XOR operations on non-integer data types. Here I use it to XOR every element in an array of each byte of the ciphertext with the secret byte. 

```python
from pwn import *

cipher = "73626960647f6b206821204f21254f7d694f7624662065622127234f726927756d"
cipher = [x for x in bytes.fromhex(cipher)]
first_byte = cipher[0]

# [!] Flag Format is crypto{..., so the first character is 'c'
secret_byte = first_byte ^ ord('c')
print(f"Secret Byte is {secret_byte}")

flag = xor(cipher, secret_byte)
print(f"Flag: {flag.decode()}")
# ---Output---
# Flag: crypto{..._by7e}
```

### Summary
This problem showed us an application of XOR's properties. It also builds upon a crucial skill used in a lot of various challenges. Without knowing the secret byte, we looked at the information we had and were able to draw connections about how we can use it to gain something new. Here we used the fact that the flag format is standardized, so we know the plaintext of at least one byte. From this, we could simply XOR the known plaintext with the first byte of the ciphertext to get the XOR key and decode the rest of the flag.