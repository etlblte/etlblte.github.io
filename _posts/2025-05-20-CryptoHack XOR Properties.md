```
---
title: CryptoHack XOR Properties
date: 2025-05-20 13:09:09 +/-0500
categories: [ctf]
tags: [cryptohack, intro_to_cryptohack, cryptography, programming, python]   
math: true
---
```

### Goal
> Let's put this into practice! Below is a series of outputs where three random keys have been XOR'd together and with the flag. Use XOR properties to undo the encryption in the final line to obtain the flag.

```
KEY1 = a6c8b6733c9b22de7bc0253266a3867df55acde8635e19c73313  
KEY2 ^ KEY1 = 37dcb292030faa90d07eec17e3b1c6d8daf94c35d4c9191a5e1e  
KEY2 ^ KEY3 = c1545756687e7573db23aa1c3452a098b71a7fbf0fddddde5fc1  
FLAG ^ KEY1 ^ KEY3 ^ KEY2 = 04ee9855208a2cd59091d04767ae47963170d1660df7f56f5faf
```
### Solution
Before completing this challenge, let's look at four main properties of XOR. First we have the commutative property, which lets us perform XOR operations in any sequence:

$$
\text{1.) Commutative: } A \oplus B = B \oplus A 
$$

Next we have the associative property, which allows us to not worry about any order of operations: 

$$
\text{2.) Associative: } A \oplus (B \oplus C) = (A \oplus B) \oplus C
$$

Third, the identity property states that anything XOR'ed with 0 does nothing:

$$
\text{3.) Identity: } A \oplus 0 = A
$$

Lastly, the self-inverse property means that anything XOR'ed with itself will cancel out and become a value of 0:

$$
\text{4.) Self-Inverse: } A \oplus A = 0
$$
From the given variables for this challenge, we are only given one decoded value KEY1. However, using the properties of XOR we can derive all the other values. For instance, using the self-inverse, identity, and associative properties we can gather the following if we XOR the values `KEY2 ^ KEY1` and `KEY1`:

$$
\text{(KEY2} \oplus  \text{KEY1)} \oplus \text{KEY1} = \text{KEY2} \oplus  \text{KEY1} \oplus \text{KEY1} = \text{KEY2} \oplus  0 = \text{KEY2}
$$

Using this behavior we can construct a script that decodes the rest of the keys:

```python
from pwn import *

KEY1 = "a6c8b6733c9b22de7bc0253266a3867df55acde8635e19c73313"
KEY1 = bytes.fromhex(KEY1)

KEY2_xor_KEY1 = "37dcb292030faa90d07eec17e3b1c6d8daf94c35d4c9191a5e1e"
KEY2_xor_KEY1 = bytes.fromhex(KEY2_xor_KEY1)

KEY2_xor_KEY3 = "c1545756687e7573db23aa1c3452a098b71a7fbf0fddddde5fc1"  
KEY2_xor_KEY3 = bytes.fromhex(KEY2_xor_KEY3)

FLAG_xor_KEY1_xor_KEY3_xor_KEY2 = "04ee9855208a2cd59091d04767ae47963170d1660df7f56f5faf"
FLAG_xor_KEY1_xor_KEY3_xor_KEY2 = bytes.fromhex(FLAG_xor_KEY1_xor_KEY3_xor_KEY2)

#---

KEY2 = xor(KEY1, KEY2_xor_KEY1) # KEY2 = (KEY2 ^ KEY1) ^ KEY1 = KEY2 ^ 0

KEY3 = xor(KEY2, KEY2_xor_KEY3) # KEY3 = (KEY2 ^ KEY3) ^ KEY3 = KEY3 ^ 0

FLAG = xor(xor(FLAG_xor_KEY1_xor_KEY3_xor_KEY2, KEY2_xor_KEY3), KEY1)

print(f"Flag: {FLAG}")
# ---Output---
# Flag: crypto{x0r_i...}
```
### Summary
In this challenge we learned four fundamental properties of the XOR operation: commutative, associative, identity, and self-inverse. These indicate, through this challenge, that the XOR operation is reversible. Thus by itself XOR is not a secure method of encryption. From one only one decoded value, we can disclose other encoded data through the properties of XOR alone. 