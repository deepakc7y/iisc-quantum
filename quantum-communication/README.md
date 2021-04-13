# Quantum Communication

The behaviour of elementary particles is subject to special rules called the postulates of quantum mechanics and so are any computing and communication devices built from them. In this section, we will repeatedly use Bob, Alice and Eve who shall send, receive and/or eavesdrop information depending on the scenario. In classical scenario, light belongs to Electromagnetic waves having special property characterized by polarization. In quantum scenario, light behaves as a bunch of elementary particles (photons), it preserves polarization which behaves the laws of quantum mechanics. We shall discuss three solutions/scenario for communication:

## Simple Classical way of Communication

This one is purely a classical communication. So, suppose Alice wants to send several bits of information over an optical fibre to Bob. In this method, she can easily encode information: for logical 1 she emits light (light here means photon), while for logical 0 she sends nothing. And also, in the coin analogy, If Alice wants to communicate 1, she gives a coin to Bob in a given timeframe; otherwise, to communicate 0, she gives nothing to Bob.

## Communication on the Classical and Quantum Border 

Here Alice uses the property of Polarization to encode the information. In figure, we can see that the polarization can be split into its horizontal and vertical components denoted as Ph and Pv respectively. Alice can choose to represent logical 1 using vertically polarized photons and logical 0 using horizontally polarized photons and the information can be sent to Bob using this ideology. The receiver on Bob’s side can decode the information into logical values by determining their polarization. The important point to note here is that the communication between Alice and Bob is still classical.

<img src="https://github.com/deepkchoudhary/iisc-quantum/blob/main/images/quantum-communication1.jpg" width="300">
<br>
<img src="https://github.com/deepkchoudhary/iisc-quantum/blob/main/images/quantum-communication2.jpg" width="300">

## Fully Quantum Communication

Alice knows that light can be polarized, not just horizontally (0°) or vertically (90°), but at any angle. Alice prepares a photon with 45° polarization as in figure. But Bob’s decoder can only detect orthogonal polarization i.e., 0° or 90° only. Therefore, P<sub>45</sub> is represented using linear combination of P<sub>v</sub> and P<sub>h</sub> multiplied by a coefficient of ‘a’ (because P<sub>45</sub> is equidistant from P<sub>v</sub> and P<sub>h</sub>) i.e., 

<img src="https://github.com/deepkchoudhary/iisc-quantum/blob/main/images/p45-communication.JPG" width="200">

Now what happens is that if Alice sends many photons, all in P45 polarization then, Bob’s receiver (also called as measurement device) will answer logical 0 in half of the times and logical 1 in the remaining half, which is all done randomly. In classical sense, no information is sent to Bob. Thus, the photon prepared in P45 polarization carries the value of both 0 and 1. Hence, this is a fully quantum operation.

To make the above communication completely noise-free, we return to coin-based analogy where Eve stands between Alice and Bob, and plays the role of the bit-flip channel. Similar to the second step, Alice prepares her coin by facing it upward to show heads (0) or tails (1) and gives it to Eve.  Randomly and with probability 1/2, Eve either leaves the coin unchanged or turns it upside down (i.e., flips it), and then hands it to Bob. As before, because of Eve’s random flip operation, Bob cannot be sure which bit value was sent originally by Alice.

<img src="https://github.com/deepkchoudhary/iisc-quantum/blob/main/images/fully-quantum-communication.jpg" width="400">

However, in reality, we cannot establish a proper quantum communication setup for more than 300 kilometres. So, we need to use something called as quantum repeaters in order to extend this range of communication between Alice and Bob. This type of setup can be seen in Tokyo where to cover a large distance we introduce a repeater called as trusted repeater (say Charlie) Alice gives her Key to Charlie and so does Bob and what Charlie will do is he will sum up the keys and makes it a public key and that way Alice and Bob can decode each other’s key. We are assuming that Charlie is faithful and won't leak anything. [9]

### Why is it difficult to establish quantum entanglement across a long path?

Let's assume Alice and Bob are connected via quantum channel and also its a noise free channel. First Alice prepares an entangled state locally inside the memory as we can see in the diagram and she takes one of the qubits and encodes it to a photon and sends it over to Bob. Then Bob will store the qubit in his quantum memory and both Alice and Bob will be entangled, but it is not that simple actually. The problem is that Bob might never receive anything. The probability of Bob receiving the qubit scales exponentially over distance as we can see in the figure. Tau is defined as the attenuation length, if we assume the Tau to be 50 km then for every 50 km the probability reduces 1/10th. To resolve this problem let's introduce the quantum repeater (Charlie) who is located equidistant from Alice and Bob in the middle. In the figure, those multiple qubits over the channel are called as multiplexing wherein they keep sending photons one after the other. The main advantage that the quantum repeaters gives us is that the attenuation length is reduced by half therefore increasing our probability. We can install multiple repeaters between Alice and Bob to increase the probability. So now what happens here is the photons that are leaving the quantum memory of Alice try to entangle with the ones in Charlie's and so does Charlie's Photons with Bob's. Once the photons are entangled between Charlie and Alice and also Bob and Charlie, we get the desired entanglement between Alice and Bob. Thus, using this method of quantum repeaters, we can completely eliminate the problem of losses in the quantum channel.

<img src="https://github.com/deepkchoudhary/iisc-quantum/blob/main/images/quantum-entanglement-communication.jpg" width="400">

<img src="https://github.com/deepkchoudhary/iisc-quantum/blob/main/images/quantum-entanglement-communication2.jpg" width="400">
