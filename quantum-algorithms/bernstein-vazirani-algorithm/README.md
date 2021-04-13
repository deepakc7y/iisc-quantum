# Bernstein Vazirani Algorithm

Let’s say there’s a hidden number inside a box which is described by n digits of 0’s and 1’s. How many tries would you say it would take us to guess that number? A classical computer to tell me the n-bit secret number, the first approach is to try all possible numbers from 0 to 2 𝑛−1. This leads to an exponential number of attempts as n grows. But a Quantum Computer can give us the secret number in just one try. It would use the Bernstein-Vazirani Algorithm to achieve that.

## The Classical Solution:

Let’s say my secret number is 1001. The classical computer would make its first guess as 0001 and it would perform AND operation between the two numbers. This will tell the computer if there is a 1 in that place (because AND (1,1) = 1) and would the process for a total of four times until it guesses the number correctly. This approach though pretty efficient, is tedious. It will have to perform as many numbers of operations as there are number of bits in our secret number. This is one such instance where we can prove the quantum supremacy over its classical counterpart.

## The Quantum Solution:
Consider a hidden Boolean function f which takes in a string of n bits {𝑥0, 𝑥1, . . . . . . 𝑥𝑛−1} and returns 1 for only a unique n-bit string 𝑠 = {𝑠0, 𝑠1, . . . . . 𝑠𝑛−1 } and 0 otherwise. It computes 𝑠. 𝑥 modulo 2 (i.e., computing the bitwise AND between the two numbers s and x, and adding up the results, and finally returning the sum modulo 2). For example, let us assume our secret number to be as 100101. Since the number of bits = 6, we initialize 6 input qubitsto state |0⟩ and 1 output qubit to state |1⟩ whose function shall be mentioned later. We Hadamard the first six qubits (i.e., we put them in superposition). Whenever we Hadamard a gate with state 0, we get |+⟩ state which is defined as:

<img src="https://github.com/deepkchoudhary/iisc-quantum/blob/main/images/hadamard-plus.JPG" width="300">

<img src="https://github.com/deepkchoudhary/iisc-quantum/blob/main/images/hadamard-minus.JPG" width="300">

The Quantum Algorithm performs CNOT operation on qubits with 1 from the secret number and target qubit for all these qubits is our output qubit q6. When our control bit is 1, the target bit will flip. This part of our algorithm is what constitutes as the black box (also called as the “oracle”). We will build it as a function that computes s.x modulo 2 by applying CX gates from the first n qubits onto the last qubit whenever there is a 1 in the secret number. We will do this in reverse order, meaning that there will be a CX gate from the nth qubit to the last qubit if the first bit of the secret number is 1. Eventually after applying this CNOT Gate, we changed the state of control bit from |+⟩ to |-⟩. The next step involves applying Hadamard to all six qubits to reverse their states from being in a superposition state to a fixed value such as |0⟩ or |1⟩. The last step of this Algorithm involves measuring the six qubits and storing them into classical bits. This measurement gives us our secret number. 

The best part about this Algorithm is that it gives us our secret number in just one try, no matter how many numbers of bits the secret number has.

<img src="https://github.com/deepkchoudhary/iisc-quantum/blob/main/images/bernstein-vazirani.jpg" width="600">

## Qiskit Implementation

### Implementing the Algorithm

```
secret = ‘101001’
qc=QuantumCircuit(len(secret)+1,len(secret))

#define hadamard gate for qubits q0 to q(n-1)
qc.h(range(len(secret)))

#for q6 define pauli-x gate followed by a hadamard gate
qc.x(len(secret)) 
qc.h(len(secret))
qc.barrier()

#define a cnot gate from qubit having 1 (control qubit) to q6 (target qubit)
for ii, yesno in enumerate(reversed(secret)):
if yesno == '1':
qc.cx(ii, len(secret))

qc.barrier()
qc.h(range(len(secret)))
qc.barrier()

#puts the results from qubits q0 to q5 to classical bits
qc.measure(range(len(secret)), range(len(secret)))
```

### Simulating the Result:

Here, we simulate the circuit on Aer's qasm_simulator. We will set the number of shots to 1.

```
sim = Aer.get_backend('qasm_simulator')
result = execute(qc, backend = sim, shots = 1).result()
counts = result.get_counts()
print(counts)

```
