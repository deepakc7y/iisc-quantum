## Introduction

Ever since the invention of Quantum Physics in the early 1900s, it has given rise to countless discussions about its meaning and about how to interpret the theory correctly. These discussions focus on issues like the Einstein-Podolsky-Rosen paradox, quantum non-locality and the role of measurement in quantum physics. In recent years, however, research into the very foundations of quantum mechanics has also led to a new field – quantum information technology. The use of quantum physics could revolutionize the way we communicate and process information. 

Two-state systems are also used to encode information in quantum systems and it is traditional to call the two quantum states |0〉 and |1〉. The really novel feature of quantum information technology is that a quantum system can be in a superposition of different states. In a sense, the quantum bit can be in both the |0〉 state and the |1〉 state at the same time. This new feature has no parallel in classical information theory and in 1995 Ben Schumacher of Kenyon College in the US coined the word “qubit” to describe a quantum bit.

## Qubits

A classical computer performs operations using classical bits i,e. either zero(0) or one (1). In contrast a Quantum Computer uses Quantum bits (also called as Qubits) which can be zero or one both at the same time, and this is what gives Quantum Computer its superior computing power. There are a number of physical objects that can be used as Qubits like a photon, a nucleus or even an electron. Each electron has an associated magnetic field and when you place such an electron in a magnetic field, the electron tends to align itself to the magnetic field as expected. This is called as the “Spin Down” state of the electron and it is the lowest energy state. We can put that electron in a “Spin Up” state but that requires a lot of energy and this state of the electron is the highest magnetic state and its direction is completely opposite to that of the magnetic field it is placed in.

<center><img src="https://github.com/deepkchoudhary/iisc-quantum/blob/main/images/qubit.jpg" width="400"></center>

## Superposition

Like waves in classical physics, Quantum States can be added together (superposed) and the result will be another valid quantum state and conversely, we can also state that each quantum state can be represented as a sum of two or more distinct states. In Quantum Information theory, a qubit state is a quantum superposition of the basic states |0⟩ and |1⟩ where |0⟩ is the Dirac Notation for a quantum state that always gives the result 0 when converted to classical logic and likewise |1⟩ is the state that always converts to 1. While the classical bit can only exist as either 0 or 1, a qubit may be in superposition of both states. The probabilities of 0 and 1 may vary for each quantum state.

<!-- Mathematical Representation of Superposition can be given as: -->

<!-- ![alt text](http://url/to/img.png) -->

<!-- where -->

### Bloch Sphere Representation

The state of a qubit can be represented in terms of two parameters i.e., θ(theta) and Φ(phi) where the value of θ ranges between 0 and π, and the value of Φ ranges between 0 and 2π. 

<!-- The representation is obtained as follows: -->

<!-- ![alt text](http://url/to/img.png) -->

In complex vector space i.e., 2D Space the 0 and 1 were orthogonal states. But when we represent them on the Bloch Sphere, they’re actually anti-polar states i.e., opposite to each other. The states in x, y, and z directions can be calculated using the above formula.

<!-- ![bloch-sphere](https://user-images.githubusercontent.com/48193113/103323473-fd338b80-4a68-11eb-81d1-b9e3e37540ac.jpg) -->

## Measurement

In Quantum Mechanics, if we know the quantum state of a particle i.e., its wave function then we can use Schrödinger’s equation to calculate what that particle will do in the future. Usually, it spreads out over time as a wave function. The problem is that we never actually observe the wave function but when we measure it, we find the particle at a single point in space.

<!-- ![alt text](http://url/to/img.png) is the Schrödinger’s equation. -->

<!-- ![measurement](https://user-images.githubusercontent.com/48193113/103323477-fdcc2200-4a68-11eb-92e2-1f80f0767807.jpg) -->

Let us assume we have a qubit and now let’s say that this quantum state is passed through a measuring apparatus and the output we get is

-	Zero (0) with probability |α|^2
- One (1) with probability |β|^2

So, what exactly happens?

We are entangling the qubit with the needle of the measuring apparatus and we enter into this superposition and somehow the nature does not appreciate superpositions at a macroscopic level and somewhere along the time with some abstraction the superposition collapses and we get the measurement as given above. 

<!-- ![measurement2](https://user-images.githubusercontent.com/48193113/103323632-d0cc3f00-4a69-11eb-8283-fdc7a55efb00.jpg) -->

<!-- ## Entanglement -->

<!-- ### Resources -->
