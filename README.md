# BB84 - Quantum Key Exchange Protocol

The original paper can be found here:
[Quantum cryptography: Public key distribution and coin tossing](https://arxiv.org/abs/2003.06557)

## Overview
BB84 Quantum Key Distribution algorithm is utilizing quantum mechanical phenomena and a quantum channel in combination with an ordinary insecure classical channel. The outcome of the execution is a generated One-Time-Pad, protected from eavesdropping due to photonic properties.

## Algorithm
For the ease of explanation, the process is described by a traditional Alice and Bob's interaction.
1. The initial step of the algorithm is Alice generating 2 random bitstrings $T$ of length $N$, such that $$T=[x_1, x_2, ... , x_n], x=\\{0,1\\}$$ The first bitstring $T_1$ represents the states Alice wants to transmit to Bob, and $T_2$ is her chosen encoding bases. The randomization of bits is achieved through putting qubits in superposition and measuring them, resulting in a random state $\\{0,1\\}$. At this stage, Alice does not disclose her data and keeps it strictly private.
3. Using $T_2$, Alice encodes qubits in a following way:
    - If the selected basis $T_2[i]$ is 0, qubit is encoded rectilinearly and gaining the value of $\\{0,1\\}$
    - If the selected basis $T_2[i]$ is 1, qubit is encoded diagonally with using Hadamard transform and gaining the superposition of $\vert+\rangle$ or $\vert-\rangle$. The values of diagonal encoding can be expressed as: $$\vert+\rangle=\frac{\vert0\rangle-\vert1\rangle}{\sqrt[2]{2}}, \vert-\rangle=\frac{\vert0\rangle+\vert1\rangle}{\sqrt[2]{2}}$$ After encoding, qubits are transmitted to Bob via the quantum channel.
4. After receiving Alice's qubits, Bob generates random bitstring $T_3$, representing his selected measurement bases and an attempt to guess the encoding Alice performed on qubits. Measurements are performed the following way:
    - If the selected basis $T_3[i]$ is 0, qubit is measured rectilinearly.
    - If the selected basis $T_3[i]$ is 1, qubit is measured diagonally using Hadamard transform. Previously created superposition collapses into the originally encoded value.
After performing measurements, Bob receives the final bitstring $T_4$, representing supposed Alice's state.
5. Finally, Alice and Bob open communication via classical channel to compare their selected measurement bases. For every $T_2[i]=T_3[i]$, element $T_4[i]$ is extracted and added to the final key. By the end of comparison, secure key is generated, marking the end of communication.
