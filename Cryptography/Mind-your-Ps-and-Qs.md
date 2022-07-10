# Mind your Ps and Qs

## Description: ##

In RSA, a small e value can be problematic, but what about N? Can you decrypt this?

>Hint: Bits are expensive, I used only a little bit over 100 to save money

## Solution: ##

We are given a file `values`, which is ASCII text that reads:
> Decrypt my super sick RSA:
c: 62324783949134119159408816513334912534343517300880137691662780895409992760262021
n: 1280678415822214057864524798453297819181910621573945477544758171055968245116423923
e: 65537

Our task is to decrypt the ciphertext `c` given the variables `n` (modulus) and `e`, which is the standard 65537.

My favorite way of doing this is through the use of [RsaCtfTool](https://github.com/RsaCtfTool/RsaCtfTool), which takes those arguments and runs a factordb attack to determine p and q.

```bash
$ ./RsaCtfTool.py --uncipher 62324783949134119159408816513334912534343517300880137691662780895409992760262021 -n 1280678415822214057864524798453297819181910621573945477544758171055968245116423923 -e 65537
```

In this case, we use the argument --uncipher (and provide the ciphertext `c`), -n, and -e.

This will output the flag in HEX, INT, and UTF-8, which displays it in plaintext.

Of course, this could have been done manually by factorizing p + q (use factordb), then using python to calculate phi, d, and m like this:

```python
from Crypto.Util.number import inverse

phi = ( p - 1 ) * (q - 1 )
d = inverse(e,phi)
m = pow( c, d, n )
```
