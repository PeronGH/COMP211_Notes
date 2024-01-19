## Network Security

### Goals (CIA Triad)

- **Confidentiality**
- **Integrity**
- **Availability**

### Cryptography

- **Caesar cipher** is a substitution cipher that shifts the letters of the plaintext by a fixed number of positions down the alphabet.

#### Symmetric Key Cryptography

- **Mono-alphabetic cipher** is a type of encryption where each letter of the plaintext is substituted with a corresponding unique letter of the cipher alphabet (`Map<Letter, Letter>`).
  - Cipher-text only attack: brute force or statistical analysis
  - Known-plaintext attack
    - Chosen-plaintext attack

- **Poly-alphabetic encryption** uses multiple substitution alphabets to encrypt the plaintext.
- **Block ciphers** are encryption methods that divide plaintext data into fixed-size blocks and encrypt each block individually using the same key. 
  - **Cipher Block Chaining** (CBC) is an encryption method where each plaintext block is XORed with the previous ciphertext block before being encrypted, using a different initialisation vector for the first block.

- **DES**
- **AES**

#### Public Key Cryptography

- **Requirements**:

  - $K^-_B(K^+_B(m)) = m$
    - $K^+_B$: Public key
    - $K^-_B$: Private key

  - $K^-_B$ can’t be easily computed from $K^+_B$

- **RSA**

  - Modular arithmetic:
    - $((a \mod n) + (b \mod n)) \mod n = (a+b) \mod n$
    - $((a \mod n) - (b \mod n)) \mod n = (a-b) \mod n$
    - $((a \mod n) \cdot (b \mod n)) \mod n = (a \cdot b) \mod n$
    - Thus, $(a \mod n)^d \mod n = a^d \mod n$
  - Creating $K^+_B$  and $K^-_B$:
    1. Choose: 2 large prime numbers: $p$ and $q$
    2. Compute: $n=pq$, $z=(p-1)(q-1)$
    3. Choose: $e$ where $e < n$ and $e$ has no common factors with $z$
    4. Choose: $d$ where $ed \mod z = 1$
    5. $K^+_B = (n, e)$  and $K^-_B = (n, d)$

  - Encryption and Decryption:
    - $m < n$
    - $c = m^e \mod n$ (Encryption)
    - $m = c^d \mod n$ (Decryption)

  - $K^-_B(K^+_B(m)) = m = K^+_B(K^-_B(m))$

### Authentication and Integrity

#### Hash Function

- **Requirements**:
  - $H(m) = x$
  - Fixed-length output
  - $m$ can’t be easily computed from $x$

- **MD5**: 128-bit
- **SHA1**: 160-bit

##### **Digital Signature**

Hash and encrypt with private key. (RSA property)

#### CA

CA provides digital signature of public key.

### Usage

- PGP
- TLS