# Quantum Cryptography

Most of the classical encryption schemes rely on the fact that they are “computationally complex” to brute force. For instance “RSA” an asymmetric scheme that uses the fact that it is difficult to find the factor of a composite number when the factors are prime numbers (prime factorization).

## Quantum - a double-edged sword !!!

The rise of quantum computers, with their enormous computational power, parallel processing capabilities will render most of the state-of-the-art encryption schemes useless in the future.

- It would take a classical computer around “300 trillion years” to break an RSA-2048-bit encryption key. [1]
- A quantum computer with 4099 perfectly stable qubits could break the RSA-2048 encryption in 10 seconds!!!! [1]
- The two approaches in breaking this encryption, Shor's algorithm, and Quantum Annealing.
- Even though this might not be true for the near future, but definitely it is a potential threat as classical information can be stored.

## Provable Security:

We can define a system as provably secure if the security of the system ultimately relies upon a mechanism or rule which has some logical or mathematical proof.

## Shannon’s Condition:

A necessary and sufficient condition for perfect secrecy is that:

### P(E=e/M=m) = P(E=e), for all M and E

That is P(E) must be independent of M. In other words, all the valid encryption keys are equiprobable. [2]

All of this leads us to “Quantum Key Distribution (QKD)” [3]
- Quantum Key Distribution provides a way of sharing secret keys (k) that are necessary for cryptographic protocols.
- The importance here is in ensuring that keys remain private, i.e., between the communicating parties.
- To achieve this, we rely on principles of Quantum mechanics.
- QKD is only used to produce and distribute a key, not to transmit any message data.

### The need for Key Distribution?

Encryption is an essential part of data security. It provides a fundamental layer of protection that shields confidential data from exposure to attacks. It is needed to protect information transferred across telecommunications networks, as well as residing in files and databases. The most secure and widely used methods to protect the confidentiality and integrity of data transmission are Based on symmetric cryptography. Even better security is delivered with a mathematically unbreakable form of encryption called a one-time pad, whereby data is encrypted using a truly random key of the same length as the data being encrypted. In both cases, the main practical challenge is how to securely share the keys between the concerned parties.

### How does QKD work?

The security of QKD is based on a fundamental characteristic of quantum mechanics: The act of measuring a quantum system disturbs the system. Thus, an eavesdropper trying to intercept a quantum exchange will inevitably leave detectable traces. The legitimate exchanging parties can decide either to discard the corrupted information, or reduce the information available to the eavesdropper to nought by distilling a shorter key.

A QKD implementation typically includes the following components:
- Both errors and potential information leakage are removed during subsequent error correction and privacy amplification post-processing steps, leaving Bob and Alice with a shared key known only to them.
- A fibre or free-space quantum channel to send quantum states of light between the transmitter (Alice) and receiver (Bob). This channel does not need to be secured A public but authenticated communication link between the two parties to perform post-processing steps and distil a correct and secret key.
- A key exchange protocol that exploits quantum properties to ensure security by detecting eavesdropping or errors, and by calculating the amount of information that has been intercepted or lost. Since QKD first appeared as a promising theoretical concept, a variety of protocols have emerged and been demonstrated in many real-world scenarios. The first approach is Discrete Variable QKD, which encodes quantum information in discrete variables and uses single photon detectors to measure the received quantum states.
- Examples are the BB84 protocol and the E912 protocol. A second approach is continuousvariable QKD (CV-QKD). In this approach, the quantum information is encoded onto the amplitude and phase quadrature of a coherent laser, and can then be measured by the receiver using homodyne detectors.

## Counter – Factual QKD

In counterfactual quantum key distribution (QKD), two remote parties can securely share random polarization-encoded bits through the blocking rather than the transmission of particles. We propose a semi-counterfactual QKD, i.e., one where the secret bit is shared, and also encoded, based on the blocking or non-blocking of a particle. The scheme is thus semi - counterfactual and not based on polarization encoding. As with other counterfactual schemes and the Goldenberg-Vaidman protocol, but unlike BB84, the encoding states are orthogonal and security arises ultimately from single-particle non-locality. Unlike any of them, however, the secret bit generated is maximally indeterminate until the joint action of Alice and Bob. We prove the general security of the protocol, and study the most general photon-number-preserving incoherent attack in detail.[8] 

Semi-counterfactual quantum cryptography: The experimental architecture of the proposed QKD using Michelson-type interferometer. Alice’s station consisting of the source S initiates the protocol by sending light pulses through the optical circulator OC to the beam splitter BS, which splits them into beams along arms a and b. The optical delay OD mains the phase between the arm by compensating for the path difference in the two arms. Light along arm a is subjected to absorption or reflection by Alice based on her switch state. Likewise, by Bob along arm b who also possesses SW, Abs and FM.

### Comparison of QKD with CQKD

- In Comparison with other QKD protocols – which encode based on orthogonal states and single-particle non-locality protocols, CQKD generated the secret bit after the actions performed by Alice and Bob.
- Eve’s attempt to determine Bob’s action will tend to localize the particle into one or the other arm, forcing a particle nature, and thereby disrupting the coherence between the two geographically separated wave packets in the two arms. This will be reflected in a reduction of visibility, which can be observed.
- When the secret bit generated is 1, then Bob applied the operation A, and the photon never physically travelled on the exposed arm b. This seems to make the generation of this bit inherently safe from an eavesdropper Eve monitoring the arm.

### Types of Attacks by Eve

- Translating No Cloning Theorem:
Reduced density operator of the particle in the exposed arm during the forward transmission is polarization dependent, and thus correlated with the secret state. Therefore, Protocol is not very secure.

- General Incoherent Attack:
Eve prepares n ancillas in a state and applies the operation on Bob-Eve System which is more prone to eve finding out the secure key.

- General Photon Number Preserving Incoherent Attack:
The above general attack only indicates that the protocol is secure if no noise is detected. In practice noise will be unavoidable, even in the absence of an eavesdropper. On the other hand, conservatively, we must assume that all noise is due to Eve. By upper-bounding her information on the secret key, we can derive the tolerable error rate.

### Comparison of QKD Protocols:

#### Similarities among different established protocols:

- Security of all the protocol relies on the fact that the information is encrypted by laws of physics and not only on mathematical support (prime factorization).
- The very act of measurement perturbs the state, hence providing a tool for detection of eaves-dropping.
- Security depends on no-cloning and the indistinguishability of non-orthogonal states.
- All the Quantum protocols have the added advantage of getting true random bits.
- All the protocols usually have a classical processing step (like reconciliation and privacy amplification) which follows the quantum steps of protocol.
- Most of them have been implemented in an experiment and a few commercially.
- All the protocols produce secure key which can be later used in schemes like OTP.

#### Differences:

1. Principle of sharing information:
- Traditional Protocols (BB84):
Sharing of information is accomplished by sharing particles or energy through the channel.
- Counterfactual Protocols:
Information is shared between concerned parties by blocking the particle or energy.
- Semi Counterfactual Protocol:
The protocol is counterfactual with respect to one of the bits (bit 1 here), but in case of other the particle has to travel physically through the channel (bit 0).

2. Check for correctness of shared information:
- Traditional Protocols: Subset of basis of measurement of both the concerned parties are compared, in case they aren’t same key is dis-guarded, usually it done conservatively.
- Counterfactual Protocols and semi counterfactual: After both the parties have received the secret key, they are verified for figure of merits like error rate on subset of the share key.

3. Principle of encoding the information:
- Traditional Protocols: Information is encoded by polarizing photon using conjugate states, example H V and the Hadamard Bases.
- Counterfactual Protocols: Information can be encoded using the orthogonal states.
- Semi-counterfactual Protocol: Information can be encoded using blocking or non-blocking of
the particle itself.
