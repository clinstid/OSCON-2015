# Stop building insecure systems: Cryptography 101

# Passwords & Authentication

Passwords are just a subtype of encryption key - passwords easy to guess, keys should not be. We need to make our passwords better keys.

## Key Derivation Function
- function that derives one or more secret values (keys) from one secret value

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

# hkdf
- HMAC based extract and expand
- not for use with passwords

# Key Management

# Data at Rest

# Signing & Verification
