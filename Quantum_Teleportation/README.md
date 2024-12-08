# Quantum Teleportation
Quantum teleportation is a foundational quantum protocol that allows the precise transfer of an unknown quantum state from a sender (Alice) to a receiver (Bob). The resources required for this protocol are:

1. **Quantum Entanglement**: A shared entangled state between Alice and Bob.  
2. **Classical Communication**: A classical channel to transmit measurement results. 

## Overview of the Protocol  

To perform quantum teleportation, Alice and Bob must first establish a shared two-qubit entangled state. For this purpose, I will use the maximally entangled Bell state 

$$ |\Phi^+⟩ = \frac{1}{\sqrt{2}} (|00⟩ + |11⟩). $$

Once the entangled state is generated, Alice can transmit a generic quantum state 

$$ |\psi⟩ = \alpha|0⟩ + \beta|1⟩ \quad \text{where } |\alpha|^2 + |\beta|^2 = 1, $$

accurately to Bob, even though she does not directly send the qubit carrying $|\psi⟩$.

This remarkable process leverages the principles of quantum mechanics, allowing information encoded in $|\psi⟩$ to be reconstructed on Bob's side without the need for the quantum state to travel through the classical channel.

## Step 1: Constructing the Initial State for Teleportation  

To begin the process of teleporting the state $|\psi⟩$ to Bob, Alice must prepare a composite system that is the tensor product of the generic state $|\psi⟩$ and the shared entangled state $|\Phi^+⟩$. The preparation of the state is as follows:

$$ |\psi_0⟩ = |\psi⟩_A |\Phi^+⟩ _{AB} $$

Expanding the entangled state $|\Phi^+⟩ $:

$$|\psi_0⟩ = |\psi⟩_A ( \frac{|0⟩_A |0⟩_B + |1⟩_A |1⟩_B}{\sqrt{2}} ) $$

Substituting $|\psi⟩ = \alpha|0⟩ + \beta|1⟩ $, we get:

$$ |\psi_0⟩ = (\alpha |0⟩ + \beta |1⟩ )_A (\frac{|0⟩_A |0⟩_B + |1⟩_A |1⟩_B}{\sqrt{2}} ) $$

Expanding the terms:

$$|\psi_0⟩ = \frac{1}{\sqrt{2}} (\alpha |0⟩_A (|0⟩_A |0⟩_B + |1⟩_A |1⟩_B) + \beta |1⟩_A (|0⟩_A |0⟩_B + |1⟩_A |1⟩_B))$$

This prepared state $|\psi_0⟩$ is the starting point for the teleportation process, containing both the generic state $|\psi⟩$ and the shared entanglement between Alice and Bob.

## Step 2: Applying CNOT and Hadamard Gates  

After preparing the initial state $|\psi_0⟩$, Alice applies a CNOT gate and then a Hadamard gate to her qubits to make the state ready for the final measurement. The operations are as follows:

$$ |\psi_1 \rangle = (H \otimes \mathbb{I} \otimes \mathbb{I}) \, \text{CNOT}(1, 2) |\psi_0⟩ $$

Expanding $|\psi_0⟩$:

$$|\psi_1 \rangle = (H \otimes \mathbb{I} \otimes \mathbb{I}) \left(\alpha |0\rangle_A (\frac{|0\rangle_A |0\rangle_B + |1\rangle_A |1\rangle_B}{\sqrt{2}} ) + \beta |1\rangle_A (\frac{|1\rangle_A |0\rangle_B + |0\rangle_A |1\rangle_B}{\sqrt{2}} )\right)$$

Applying the Hadamard gate to Alice's qubit:

$$|\psi_1 \rangle = \alpha \left(\frac{|0\rangle_A + |1\rangle_A}{\sqrt{2}} \right) \left(\frac{|0\rangle_A |0\rangle_B + |1\rangle_A |1\rangle_B}{\sqrt{2}} \right)+ \beta \left(\frac{|0\rangle_A - |1\rangle_A}{\sqrt{2}} \right)\left(\frac{|1\rangle_A |0\rangle_B + |0\rangle_A |1\rangle_B}{\sqrt{2}} \right)$$

Expanding the terms:

$$|\psi_1 \rangle = \frac{1}{2} \left[\alpha |00\rangle_A |0\rangle_B + \alpha |01\rangle_A |1\rangle_B + \alpha |10\rangle_A |0\rangle_B + \alpha |11\rangle_A |1\rangle_B + \beta |00\rangle_A |0\rangle_B - \beta |01\rangle_A |1\rangle_B - \beta |10\rangle_A |0\rangle_B + \beta |11\rangle_A |1\rangle_B \right]$$

or more simpler

This state $|\psi_1 \rangle$ is now prepared for Alice's measurement in the subsequent step of the protocol.

$$|\psi_1 \rangle = \frac{1}{2} \left[|00\rangle_A (\alpha |0\rangle_B+\beta |1\rangle_B) + |01\rangle_A (\alpha |1\rangle_B+\beta |0\rangle_B) +|10\rangle_A (\alpha |0\rangle_B - \beta |1\rangle_B) +|11\rangle_A (\alpha |1\rangle_B-\beta |0\rangle_B) + \right]$$

## Step 3: Measurment

The Alice's measurement can have four possible states $'00'$, $'01'$, $'10'$, and $'11'$, the following table represent the details of measurement and Bob state

| Alice's Result | Bob's State      | **Bob Manipulation** |
|----------------|--------------------------------|-------------------------|
**00** | $α|0⟩ + β|1⟩$  | $\mathbb{I}$  |
**01** | $α|1⟩ + β|0⟩$  | $X$         |
**10** | $α|0⟩ - β|1⟩$  | $Z$         |
**11** | $α|1⟩ - β|0⟩$  | $ZX$        |


in the following circuit we can see the final quantum circuit, and also Bob manipulation for reconstructing an exact $|\psi\rangle$.



