---
title: CryptoHack Bytes and Big Integers
date: 2025-05-20 13:04:00 +/-0500
categories: [ctf]
tags: [cryptohack, intro_to_cryptohack, cryptography, programming, python]     
---

### Goal
> Convert the following integer back into a message:
```python
11515195063862318899931685488813747395775516287289682636499965282714637259206269
```

### Solution
One way to create an encoded string is to encode each character and then append the encoded values together.  For instance we can create a hex string from the message HELLO like so:
```
message: HELLO  
ascii bytes: [72, 69, 76, 76, 79]  
hex bytes: [0x48, 0x45, 0x4c, 0x4c, 0x4f]  
base-16: 0x48454c4c4f
```

This process also works when encoding a message with Base 10 numbers, and is used in algorithms like RSA. One way to convert a long number to a string is by using the PyCryptodome library in Python. It has two functions that can help us with this task: `bytes_to_long()` and `long_to_bytes()`. 
```python
from Crypto.Util.number import *

ciphertext= 11515195063862318899931685488813747395775516287289682636499965282714637259206269
plaintext= long_to_bytes(ciphertext)

print(f"Flag: {plaintext.decode()}")

# ---Output---
# Flag: crypto{3nc...}
```

### Summary
Here we show how to encode and decode messages to and from Base 10 numbers. This is applicable in various encoding algorithms such as RSA. 
