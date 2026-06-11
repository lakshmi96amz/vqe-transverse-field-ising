# Variational Quantum Eigensolver for the Frustrated Transverse-Field Ising Model

## Overview

This project implements a Variational Quantum Eigensolver (VQE) to compute the ground-state energy and approximate ground-state wavefunction of a frustrated transverse-field Ising model (TFIM) using Qiskit.

The work explores how variational quantum algorithms can be applied to quantum many-body systems exhibiting frustration, where competing interactions prevent simultaneous minimization of all local interaction energies. Such systems give rise to highly nontrivial energy landscapes, strong correlations, and entangled ground states that become increasingly difficult to study using exact classical methods as system size grows.

This implementation uses a physics-inspired QAOA-style variational ansatz that mirrors the structure of the underlying Hamiltonian, allowing efficient preparation of correlated trial states while maintaining a shallow circuit depth.

---

## Physical Model

The transverse-field Ising Hamiltonian studied in this project is

```math
H = J (Z_1Z_2 + Z_2Z_3 + Z_3Z_1)
+ h (X_1 + X_2 + X_3)
```

where:

* (J) is the interaction strength between neighboring spins.
* (h) is the transverse-field strength.
* (Z_i) and (X_i) are Pauli operators acting on spin (i).

The triangular interaction geometry introduces frustration when the couplings are antiferromagnetic ((J > 0)), since all pairwise interactions cannot be simultaneously satisfied.

---

## Methodology

### Variational Quantum Eigensolver (VQE)

VQE is a hybrid quantum-classical algorithm that leverages the variational principle:

```math
E(\theta) = \langle \psi(\theta) | H | \psi(\theta) \rangle \ge E_0
```

where:

* (|\psi(\theta)\rangle) is a parameterized trial state.
* (E_0) is the true ground-state energy.

The algorithm iteratively:

1. Prepares a parameterized quantum state.
2. Measures the energy expectation value.
3. Uses a classical optimizer to update circuit parameters.
4. Repeats until convergence.

---

## Variational Ansatz

The project employs a QAOA-inspired ansatz:

```math
|\psi(\beta,\gamma)\rangle =
e^{-i\beta \sum_i X_i}
e^{-i\gamma \sum_{\langle i,j\rangle} Z_i Z_j}
|+\rangle^{\otimes 3}
```

The circuit consists of:

### Initial State Preparation

A uniform superposition state

```math
|+\rangle^{\otimes 3}
```

generated using Hadamard gates.

### Interaction Layer

Implements

```math
e^{-i\gamma Z_iZ_j}
```

for each edge of the frustrated triangle.

### Mixer Layer

Implements

```math
e^{-i\beta X_i}
```

using parameterized RX rotations.

This structure naturally captures the competing interaction and transverse-field physics of the Hamiltonian.

---

## Technologies Used

* Python
* Qiskit
* NumPy

---

## Results

The VQE workflow successfully converges to the ground-state energy of the frustrated TFIM and produces variational states with high overlap with the exact ground state. Ground-state energies are validated against exact diagonalization results for small system sizes, providing a benchmark for the accuracy of the variational approach.

The project demonstrates how frustration and transverse-field strength influence the energy landscape, optimization process, and structure of the ground state.

---

## References

1. A. Peruzzo et al., *A Variational Eigenvalue Solver on a Quantum Processor* (2014)
2. E. Farhi et al., *A Quantum Approximate Optimization Algorithm* (2014)
3. Literature on VQE, QAOA, and quantum many-body simulation

