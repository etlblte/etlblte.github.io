```
---
title: CryptoHack You either know, XOR you don't
date: 2025-05-20 13:12:00 +/-0500
categories: [ctf]
tags: [cryptohack, intro_to_cryptohack, cryptography, programming, python]     
---
```

### Goal
> I've encrypted the flag with my secret key, you'll never be able to guess it.

```
0e0b213f26041e480b26217f27342e175d0e070a3c5b103e2526217f27342e175d0e077e263451150104
```

### Solution
Similar to the last challenge, we are given an XOR encoded string but we don't know the key used. However, we can disclose the key again by XOR'ing the ciphertext with the known plaintext. Since the standard prefix for the flag (`crypto{`) is seven characters long, we can recover the first seven characters of the XOR key:

```python
from pwn import *

cipher = "0e0b213f26041e480b26217f27342e175d0e070a3c5b103e2526217f27342e175d0e077e263451150104"
cipher = bytes.fromhex(cipher)

# [!] Flag Format is crypto{ (this is 7 characters)
potential_key = xor(cipher, "crypto{")
potential_key = potential_key.decode()[:7]
print(f"Potential Key: {potential_key}")

# ---Output---
# Potential Key: myXORke
```

This gives us the incomplete string `myXORke`. We can extrapolate from this and fill in the rest of the word `key` and see what happens:

```python
potential_key += "y"

flag = xor(cipher, potential_key)
print(f"Flag: {flag.decode()}")

# ---Output---
# Flag: crypto{1f_y0u...}
```

And this works!
### Summary
Extending the concepts learned in the previous challenge "Favorite Byte", we can disclose a ciphertext encoded with a longer key by again using the standardized flag prefix `crypto{`. This time we aren't given the full key, but we can make an assumption for what the missing characters are. Then lastly we can test the potential key to see if it gives us a readable output. 