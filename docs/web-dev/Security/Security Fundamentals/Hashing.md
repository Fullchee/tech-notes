[YouTube](https://youtu.be/NuyzuNBFWxQ)

## Encryption vs Hashing

**Hashing**
- one way conversion of data -> gibberish
- Always returns a string of the same length
- Culinary term: hash brown
	- Chopped and mixed

**Encryption**
- convert data into gibberish
- can convert it back


## HMAC

hash function that also takes in a shared secret key as an input

1. message integrity: know that the message wasn't tampered with

2. authentication
   (I know who the sender is)

SSL will give more security guarantees than HMAC

PyGitHub API

[[JSON Web Tokens (JWTs)]] can be integrity protected
- verify that the user didn't edit the payload

How do symmetric & asymmetric encryption work together?
asymmetric securely send a key (or use Diffie Hellman)

symmetric w/ the shared key to encrypt all the data

## Storing passwords

Bcrypt

Salt 

Rainbow table

Timing attack
- Attacker uses computation time to get info


Pepper

## Digital signature

Private key to sign a hash of the original message

Recipient uses public key to validate the message