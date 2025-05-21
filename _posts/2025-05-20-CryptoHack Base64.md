```
---
title: CryptoHack Base64
date: 2025-05-20 13:02:00 +/-0500
categories: [ctf]
tags: [cryptohack, intro_to_cryptohack, cryptography, programming, python]
---
```

### Goal
> Take the below hex string, _decode_ it into bytes and then _encode_ it into Base64.

### Solution
[Base64](https://en.wikipedia.org/wiki/Base64) is another encoding scheme like hexadecimal. In Base64, one character is represented by 6 bits and can represent one of 64 values. Unlike hex, one number or letter does not represent one character in Base64. Three bytes of data (3 * 8= 24 bits) in a Base64 string represents four Base64 characters (6 * 4 = 24 bits). 

Base64 is commonly used online for web encoding. One advantage of using this encoding is that it creates [printable characters](https://www.redhat.com/en/blog/base64-encoding). This lets it be transported over various protocols that may or may not require plaintext characters. It can also be used to encode an image or file so that they can be easily transferred or stored in HTML/CSS files.

For this challenge we are given two tasks. First we must decode the string from hexadecimal and then encode it into Base64. In Python we can use the module `base64` to encode data into Base64.  Once imported we can simply call the `base64.b64encode()` function.

```python
import base64

ciphertext_hex= "72bca9b68fc16ac7beeb8f849dca1d8a783e8acf9679bf9269f7bf"
ciphertext_bytes= bytes.fromhex(ciphertext_hex)

flag= base64.b64encode(ciphertext_bytes)

print(f"Flag: {flag.decode()}")

# ---Output---
# Flag: crypto/B.../
```

Another helpful function in this module is the `base64.b64decode()` which can be used to [translate code from Base64](https://www.geeksforgeeks.org/encoding-and-decoding-base64-strings-in-python/). 
### Summary
In this task we learned about another encoding scheme Base64. One character in Base64 is represented with 6 bits and can represent one of 64 different values. This is typically used in web applications for its portability.