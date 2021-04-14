# BB84

BB84 [6] was the first quantum communication protocol, proposed by, Bennett and Brassard in 1984.

This is provably secure and is used as a key distribution protocol for schemes like the one-time pad.

## Steps involved in the protocol assuming a noise-free channel:
1. Alice sends Bob non-entangled BB84 states (standard basis pair and Hadamard basis pair).
2. Bob measures the qubits sent by Alice by randomly selecting his bases (here, Hadamard, and standard bases) and announces that he has measured all the qubits.
3. If Bob would have measured the bits using the same base as Alice used to transmit the qubits, Bob’s measurement is correct with a unit probability. Else, Bob would have measured it right with only 50% probability. So, Alice and Bob exchange the states they have transmitted and measured respectively. They discard all the qubits measured using incorrect states. i.e, if è<sub>A</sub> ≠ è<sub>B</sub> the corresponding qubits are discarded. (è<sub>A</sub> is the state used by Alice and è<sub>B</sub> is the state used by Bob).
4. Alice then chooses n qubits out of the remaining qubits for testing. Alice and Bob exchange these n qubits to verify.
5. Error rate (ä) in the exchanged qubits is then calculated. If ä≠0 or if ä exceeds a predetermined threshold, the protocol is aborted and restarted as this is indicative of an Eavesdropper trying to tap data. If ä is very small, some error correction codes are sent.
6. Information reconciliation [7] and Privacy Amplification [8] is then done.
7. Alice computes the key K<sub>A</sub> using two universal extractors and sends the seed used for extraction to Bob.
8. Bob generates the key K<sub>B</sub> using the seed in the extractor function.

The above protocol can be purified using quantum entanglement as follows.
- In step 1, Alice can create entangled pairs and can send one qubit out of each pair to Bob.
- Then, in step 2, Alice can randomly measure n qubits. Bob can verify the changes in the corresponding qubits he had received.

The above protocol will be correct as the keys KA and KB will be the same. This is also secure owing to the nature of qubit measurement. (Superposition, Entanglement, and No-cloning theorem).

<img src="https://github.com/deepkchoudhary/iisc-quantum/blob/main/images/bb84.jpg" width="500">

## Pseudocode:

```
#THE NUMBER OF BITS IN KEY SHARED IS ‘m’ >>> ‘n’ (key length)

def BB84_alice():

for (i=0 ; i<m ; i=i+1):
#transmission at Alice’s end
#random number gen giving 1(standard basis) or 0 (hadamard basis)
if(rand_1(0,1)):
alice_basis[i] = ‘HV’
#standard basis
if(rand_2(0,1)):
#1 -> qubit 1
tx_qbit[i] = [0;1]
else :
#0 -> qubit 0
tx_qbit[i]= [1;0]

else:
alice_basis[i] = ‘Diagonal’
#Hadamard basis
if(rand_2(0,1)): 
#1 -> + state corresponding to bit’1’
tx_qbit[i]=(1/\sqrt2)[1;0] + (1/\sqrt2)[0;1]
else :
#0 -> - state corresponding to bit ‘0’
tx_qbit[i]= (1/\sqrt2)[1;0] - (1/\sqrt2)[0;1]

return alice_basis 

#array of m values of basis

def BB84_bob(input_qubit):
#bob measuring the qubit received from Alice
for (j=0;j<m;j++)
if(rand_1(1,0)):
#if random number generator give 1 -> we measure in standard basis if 0 -> then we measure in diagonal basis
bob_basis[i]= ’HV’
rx_qbit[i]=measure_HV(input_qubit[i])
else:
bob_basis[i]=’Diagonal’
rx_qbit[i]=measure_diagonal(input_qubit[i])
return bob_basis

def comparison(alice_basis, bob_basis,rx_qbit):
key=[]
for(j=0;j<m;j++)
if(alice_basis[i] == bob_basis[i]):
key.append(rx_qbit[i])
else:
drop_measured_bit(rx_bit[i])
return key
#this key can be assured to be correctly transmitted and same on both transmitter and receiver end

def bit_comparison(rx_qbit,tx_qbit):
k=rand_1(0,n) #n<m
#to make sure there is no eavesdropping, we compare a subset of key
if(rx_qbit[0: k] == tx_qbit[0:k]):
QKD_status = ‘completed’
else :
QKD_status = ‘ error in key distribution’
drop_key(key)
restart_protocol()
```

Following the protocol, we selected n bits for (m-q) bits (q -> no. of bits dropped in the correctness check procedure). The key that is generated and distributed using the above protocol can be used along with OTP to establish secure communication between transmitter (Alice) and receiver (Bob). 

## Python Implementation for BB84 Protocol

### Importing functions and variable definition:

```
import numpy as np
import random as rd

rt = np.sqrt(2)      #root 2

z = np.array([[1],[0]]) #zero bit in standard basis
o = np.array([[0],[1]]) #bit 1 in standard basis 
p = np.array([[1/rt],[1/rt]]) #bit 0 in hadamard basis
m = np.array([[1/rt],[-(1/rt)]]) #bit 1 in hadamard basis

st_measure = np.array([[1,0],[0,1]]) #for measurement in standard basis

hd_measure = np.array([[(1/rt),(1/rt)],[(1/rt),(1/rt)]]) #measuremnet in hadamard basis

data= [0,1,0,0,0,0,0,1]            #ascii equivalent of "A"
```
### Transmission Scheme (Alice’s End):

```
def bb84_alice_tx(number):
alice_basis=[]                    #public list of basis
alice_bits=[]                     #private list of actual bit value
alice_qbits= []                   #public qubits sent to bob
for i in range(number):
if(rd.randint(0,1)):              #1 ---> qubit in standard basis
alice_basis.append('s')
if(rd.randint(0,1)):              #1 ----> qubit |1> prepared
alice_bits.append(1)
alice_qbits.append(o)

else:                             #0 ----> |0> is prepared
alice_bits.append(0)
alice_qbits.append(z)

else:                             #0 ----> qubit in hadamard basis
alice_basis.append('h')
if(rd.randint(0,1)):              #1 ---> qubit |+> prepared
alice_bits.append(1)
alice_qbits.append(m)

else:                             #0 ---> qubit |-> prepared
alice_bits.append(0)
alice_qbits.append(p)

print("list of basis at alice ---> ",alice_basis)
print("list of bits at alice ---> ",alice_bits)

return alice_qbits,alice_basis,alice_bits
```

### Qubit State Comparison

```
def qbit_comp(q1,q2):    #for comparing 2 qubits
q1=np.ceil(q1)
comp=(q1==q2)
return comp.all()
```


### Reception Scheme (Bob’s end):

```
def bb84_bob_rx(input_qbit,number):
bob_basis=[]                              #basis in which bob measures
bob_bits=[]                               #actual bits
temp =[]
for i in range(number):
if(rd.randint(0,1)):                      #1 --> measurement in standard basis
bob_basis.append('s')
bob_qbit=np.dot(st_measure,input_qbit[i])
#bob_qbit=np.transpose(bob_qbit)
temp.append(bob_qbit)
if (qbit_comp(bob_qbit,z)):                 #0 was detected in standard basis 
bob_bits.append(0)
else:
bob_bits.append(1)                          #1 was detected in standard basis

else:
bob_basis.append('h')
bob_qbit=np.dot(hd_measure,input_qbit[i])
temp.append(bob_qbit)
if (qbit_comp(bob_qbit,z)):                 #0 was detected in hadamard basis
bob_bits.append(0)
else:
bob_bits.append(1)                          #1 was detected in hadamard basis

print("list of basis at bob ---> ",bob_basis)
print("list of bits at bob ---> ",bob_bits)

return bob_bits,bob_basis ,temp

Tx_qbit , a_basis ,al_bit = bb84_alice_tx(20)
b_bits,b_basis,test_q = bb84_bob_rx(Tx_qbit,20)
```

### Post Processing at Transmitter and Receiver’s ends:

```
def post_processing_alice(a_basis,b_basis,al_bit):    #post processing at alice
a_final_key=[]
for j in range(len(a_basis)):
if(a_basis[j]==b_basis[j]):
a_final_key.append(al_bit[j])
else:
pass
return a_final_key                                    #the corrected bits at alice

def post_processing_bob(a_basis,b_basis,b_bits):      #post processing at bob
b_final_key=[]
for k in range(len(a_basis)):
if(a_basis[k]==b_basis[k]):
b_final_key.append(b_bits[k])
else:
pass
return b_final_key                                    #the corrected bits at bob
```

### One Time Pad:

```
#OTP protocol for encryption of binary information
def OTP(msg,key):
enc_dec=[]
for i in range(len(msg)):
enc_dec.append((msg[i]+key[i])%2)        #modulo 2 addition or exor operation
return enc_dec                           #msg, key and encrypted data of are same length
```

### Output Results:

```
key_alice =post_processing_alice(a_basis,b_basis,al_bit)
key_bob = post_processing_bob(a_basis,b_basis,b_bits) 

enc_data = OTP(data,key_alice[0:8])
dec_data =OTP(enc_data,key_bob[0:8])

print('final key with alice ---> ',key_alice)
print('final key with bob ---> ',key_bob)

print("Message to be sent ----> ",data)

print("Data encrypted by Alice ---- > ", enc_data)
print("Data decrypted by Bob ---- > ", dec_data)
```

## Results:

### Encryption of the character ‘A’ using BB84 and OTP:

### Output of BB84:

<img src="https://github.com/deepkchoudhary/iisc-quantum/blob/main/images/bb84-output.jpg" width="800">

### Output of One Time Pad:

<img src="https://github.com/deepkchoudhary/iisc-quantum/blob/main/images/bb84-output2.JPG" width="800">
