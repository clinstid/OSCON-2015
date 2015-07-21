# Stop building insecure systems: Cryptography 101

* [Presentation](Crypto Tutorial 16x9.pdf)
* [Source](https://github.com/dmend/oscon-crypto-tutorial)

# Passwords & Authentication
Passwords are just a subtype of encryption key - passwords easy to guess, keys should not be. We need to make our passwords better keys.

## Key Derivation Function
A KDF is a function that derives one or more secret values (keys) from one secret value.

### Work factor
The work factor is the amount of work required to encrypt/hash. A higher work factor will make it harder to brute force captured hashes. However, it also affects how hard your own servers will have to work to decrypt encrypted data, so testing should be done to figure out a reasonable work factor for your servers.

Another facet of this is that newer hardware is able to handle more work and some sources of attacks may have far more resources available, so a higher work factor may not be as safe as you think.

### bcrypt
- based on blowfish symmetric cypher
- default password storage for a lot of systems
- 128-bit salt combined with 192-bit key
- doesn't require salt, it's taken care of for you

### scrypt
- designed to be resistant to large-scale customer hardware attacks
- raises resource demands of the algorithm by making it more expensive to implement in hardware by requiring more memory
- need to be careful on large systems because you may end up causing issues with your servers if you push algorithm requirements too high

bcrypt is still widely available, but scrypt is becoming more available.

### pbkdf2
- Used for standardized, military grade crypto
- Kind of old, work factor needs to be pretty high at this point for it to be effective

### hkdf
- HMAC based extract and expand
- not for use with passwords

# Key Management

## Randomness
Ensure that you are using a cryptographically secure random number generator that has been correctly seeded.
- Linux: urandom

## Storing Keys
- Don't put the key in a source repository (duh).
- Put the key in an environment variable.
- Generate configuration file at provision time that includes the secret key (make sure it came from a secure environment).
- Secure and trusted storage is mostly software at the moment, but Intel is working on a solution (TPM)

# Data at Rest
Three general ways to protect data at rest:
- Hashing
- Symmetric Encryption
- Asymmetric Encryption

## Hashing
If you can't throw away the data, but don't need to retrieve it, then hashing is a good option.

## Symmetric Encryption
Same key for encryption and decryption. Works for internal encryption for data that doesn't need to be shared or exposed to external systems.

Lots of different options for symmetric encryption. A good option is the [Fernet project](https://cryptography.io/en/latest/fernet/). Fernet is nice because it has a good set of sane defaults and in addition to encryption, it also does hashing to provide data integrity checks. That can cause issues with trying to stream a file because you have to decrypt all of the data for integrity check before you can start streaming the file, but it works well for smaller sizes of data.

## Asymmetric Encryption
Multiple keys - public key that can encrypt data to be decrypted by the private key. Used for data and connections that must be shared outside a trust boundary.

# Signing & Verification
Signing data allows the user to verify the authenticity and integrity of the data.

Generally has:
- Key Generation Algorithm
- Signature Generation Algorithm
- Signature Verification Algorithm
- A Storage Mechanism

