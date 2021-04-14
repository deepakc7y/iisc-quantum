# Quantum Teleportation Algorithm

Quantum Teleportation can be defined as the transfer of quantum state(s) from one qubit to another. This does not mean physically transporting the qubits from one place to another, but actually it is transfer of quantum information from one qubit to another.

## What is need to do Quantum Teleportation?
In classical computers, to transfer a file we can just copy the file and transfer it to its destination. But in Quantum Computers, the act of “copying” itself isn’t allowed, because we are implicitly measuring thus destroying the quantum state that we are trying to copy. Therefore, here, we use entanglement as a resource and build a quantum teleportation circuit.

## Building Quantum Teleportation Circuit:

Let us say that we want to teleport a quantum state |𝜓⟩ from Alice to Bob. The steps involved in building our circuit are described as follows:

1. Create an entangled Bell pair between Alice and Bob’s Qubits. This is done by applying a Hadamard and CNOT Gate.

<img src="https://github.com/deepkchoudhary/iisc-quantum/blob/main/images/quantum-teleportation1.JPG" width="500">

2. Alice applies a series of operations between her qubit with state |𝜓⟩ and her half of the Bell pair.

<img src="https://github.com/deepkchoudhary/iisc-quantum/blob/main/images/quantum-teleportation2.JPG" width="500">

3. Alice will measure both qubits (the one with quantum state |𝜓⟩ and her half of the Bell pair) and report these results to Bob.

<img src="https://github.com/deepkchoudhary/iisc-quantum/blob/main/images/quantum-teleportation3.JPG" width="500">

4. Bob applies gates on his half of the Bell pair.

<img src="https://github.com/deepkchoudhary/iisc-quantum/blob/main/images/quantum-teleportation.jpg" width="600">

With this, Alice has successfully teleported the state of |𝜓⟩ to Bob’s qubit.

## Qiskit Implementation

### Teleportation Circuit

```
qc = QuantumCircuit(3,3)

#the following steps ensure that q1 and q2 are entangled
qc.x(0)
qc.barrier()
qc.h(1)
qc.cx(1,2)

#Alice performs a set of operations
qc.cx(0,1)
qc.h(0)

#Alice measures her side of the Bell pair
qc.barrier()
qc.measure([0,1],[0,1])

#Based on Alice's results, Bob applies gates
qc.barrier()
qc.cx(1,2)
qc.cz(0,2)

qc.draw(output='mpl')
```
### Simulation Circuit

```
qc.measure(2,2)
sim = Aer.get_backend('qasm_simulator')
result = execute(qc, backend = sim, shots = 1024).result()
counts = result.get_counts()
print(counts)
```

We get the following as the output when the above code is executed:

```
{'100': 263, '101': 270, '110': 239, '111': 252}
```
The numbers 100, 101, 110 and 111 denote the classical bits c<sub>2</sub>c<sub>1</sub>c<sub>0</sub> with the left-most bit being c<sub>2</sub>. As
we can see, the result is always c<sub>2</sub> = 1 because we teleported |1⟩ to qubit 2.
