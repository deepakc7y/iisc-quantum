# Classical One Time Pad (OTP)

The One Time Pad (OTP) [4] system of security was first described in 1882. This is said to be the most secure encryption technique known, provided, the secret key has already been shared securely between the two parties. Transmission of each message bit requires an independent and random key bit. Each key is used only once. Hence, the name one-time pad.

## Encryption Procedure:

1. Let the plain text of k binary bits which are to be transmitted be represented as, M = [m1, m2, m3…………mk].
2. Let the shared key of k binary bits be k= [ k1, k2, k3 ……… kk ]. 

The encrypted message E can be written as,
e1 = m1 ⊕ k1
e2 = m2 ⊕ k2
.
.
.
ek = mk ⊕ kk
E= [e1, e2, e3……… ek] is the encrypted message sent across the channel.

## Decryption Procedure:

1. Let the data received at the receiver be R= [r1, r2, r3, ………… rk ].
Let the shared key of k binary bits be k= [ k1, k2, k3 ……… kk ].
2. The received message can be decrypted as,
m1 = r1 ⊕ k1
m2 = r2 ⊕ k2
.
.
.
.
.
mk = rk ⊕ kk
M = [m1, m2, m3…………mk].

For an Eavesdropper, the probability of guessing the encoded message bit is exactly ½ as the encoded message is independent of the message. This provides security for the classical OTP.

## Pseudocode:

### Encryption:

```
def OTP_enc (key, msg, enc):
#key is the secret key shared using QKD protocol (e.g., BB84).
#msg -> plain text, enc -> encrypted message.

enc = msg ⊕ key
# modulo 2 addition, length of key should be equal to the length of msg.

return enc
```

### Decryption:

```
def OTP_decrypt (key, enc, decrypt):
decrypt = enc ⊕ key
#the property of reversibility of modulo 2 addition

return decrypt
```

# Quantum One Time Pad

Quantum one-time pad [5], a single message bit is operated upon by two operators. Therefore, the size of the key required for encryption is twice that of the message. The operators X (Bit flip) and Z (Phase flip) are used in series to encrypt one qubit.

## Encryption Procedure:
1. Let the message to be encrypted be |𝑚⟩. Let the keys be |𝑘1⟩ and |𝑘2⟩.
2. Then, the encrypted qubit |𝑒⟩ is given by,

|𝑒⟩ = X <sup>k1 Z k2</sup> |𝑚⟩
 where, X|𝑚⟩ = |𝑚<sub>1</sub>⟩ and Z|𝑚⟩ = (-1)<sup>m</sup> |𝑚⟩

## Decryption Procedure:

1. Let the received Qubit be |𝑒⟩, and the keys be |𝑘1⟩ and |𝑘2⟩.
2. |𝑚⟩ = Z <sup>k2</sup> X <sup>k1</sup>; |𝑒⟩ = Z <sup>k2</sup> X <sup>k1</sup> (X <sup>k1</sup> Z <sup>k2</sup> |𝑚⟩) = |𝑚⟩

Hence, the message can be decrypted correctly.

The qubit state received by any Eavesdropper is I/2 which the maximally mixed state, thereby allowing him/her to make a correct guess with only fifty percent probability.
