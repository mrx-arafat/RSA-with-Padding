### With Padding Mini RSA Challenge

#### Introduction

This repository contains the solution to the Mini RSA challenge from PicoCTF 2021. The challenge focuses on the RSA encryption algorithm, specifically what happens when a small exponent is used. The plaintext is padded so that \( M^e \) is just slightly larger than \( N \).

#### Problem Statement

What happens if you have a small exponent in RSA encryption? The plaintext is padded so that \( M^e \) is just barely larger than \( N \). The challenge is to decrypt the given ciphertext.

#### Solution

1. **Research**: Spent a considerable amount of time researching resources to solve this challenge. Found the solution in a [Cryptography StackExchange comment](https://crypto.stackexchange.com/questions/6770/cracking-an-rsa-with-no-padding-and-very-small-e/6771#6771).
2. **Understanding the Math**: Without padding, encryption of \( m \) is \( m^e \mod n \). If \( e = 3 \) and \( m \) is short, then \( m^3 \) could be an integer smaller than \( n \), making the modulo operation a no-operation.
3. **Algorithm**: With a short \( m \) slightly wider than \( n^{1/e} \), we are given \( c = m^e \mod n \) and can find \( k \) such that \( k \times n + c \) is an \( e^{th} \) power. Then \( m = (k \times n + c)^{1/e} \).
4. **Python Script**: A Python script is used to search through thousands of values for \( k \) until we find one that contains the start of the flag. The precision is then increased to get the entire flag.

#### Flag

The flag for this challenge is `picoCTF{e_sh0u1d_b3_lArg3r_0b39bbb1}`

#### Additional Resources

- RSA Padding Schemes - Wikipedia
- Cryptography StackExchange

#### Questions and Insights

1. **Why is Padding Necessary?**: The challenge introduces a slight amount of padding to the message to make \( m^e \) larger than \( n \). What are the security implications of this?
2. **Small Exponent**: The challenge uses a small exponent \( e \). What are the vulnerabilities associated with using a small exponent in RSA?
3. **Optimizing the Python Script**: The Python script uses enumeration to find \( k \). Are there more efficient algorithms to solve this problem?

---

Special thanks to **haydenhousen**
