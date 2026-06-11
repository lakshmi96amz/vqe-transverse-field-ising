# Variational Quantum Eigensolver for the Frustrated Transverse-Field Ising Model

This project implements a Variational Quantum Eigensolver (VQE) to compute the ground-state energy and approximate ground-state wavefunction of a frustrated transverse-field Ising model (TFIM) using Qiskit.

The work explores how variational quantum algorithms can be applied to quantum many-body systems exhibiting frustration, where competing interactions prevent simultaneous minimization of all local interaction energies. Such systems give rise to highly nontrivial energy landscapes, strong correlations, and entangled ground states that become increasingly difficult to study using exact classical methods as system size grows.

This implementation uses a physics-inspired QAOA-style variational ansatz that mirrors the structure of the underlying Hamiltonian, allowing efficient preparation of correlated trial states while maintaining a shallow circuit depth.

Physical Model

The transverse-field Ising Hamiltonian studied in this project is
$$H = J (Z_0 Z_1 + Z_1 Z_2 + Z_2 Z_0) + h (X_0 + X_1 + X_2) $$
where 
\begin{itemize}
\item J is the interaction strength between neighboring spins.
h is the transverse-field strength.
\item h is the transverse-field strength.
\item $Z_i$ and $X_i$ are Pauli operators acting on spin i.
\end{itemize}
The triangular interaction geometry introduces frustration when the couplings are antiferromagnetic (J>0), since all pairwise interactions cannot be simultaneously satisfied.


