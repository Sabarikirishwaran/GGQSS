# Geometry-Guided Quantum SAT Solver

This project presents a geometry-guided, measurement-driven quantum SAT solver that leverages Riemannian optimization techniques to navigate Hilbert space efficiently toward satisfying assignments of Boolean formulas. The work integrates concepts from quantum measurement theory, geometric control, and manifold optimization, providing a novel framework for clause-by-clause quantum constraint satisfaction.

---

# Related Works

Research into quantum approaches for the Boolean satisfiability problem (SAT) has progressed through several conceptual phases, each shaped by different computational paradigms. The trajectory begins with early unstructured quantum search, evolves through probabilistic improvements over classical randomized algorithms, and ultimately advances toward measurement-driven and geometry-informed strategies. Despite this evolution, a key gap remains: the lack of methods that treat SAT solving as a geometric navigation problem on Hilbert space and exploit subspace geometry to guide measurement sequences.

---

## Early Quantum Search and Amplitude Amplification

The earliest quantum contributions to SAT-solving emerged from the development of **Grover’s search algorithm** [Grover, 1996], which established that a quantum computer can search an unstructured space of size \(N\) in \(O(\sqrt{N})\) time. This provided a **quadratic speedup** over classical brute-force SAT solving and led to the broader framework of **amplitude amplification** [Brassard et al., 2002], which generalizes Grover’s method to boost the success probability of any probabilistic algorithm.

Shortly thereafter, researchers showed that **Schöning’s randomized SAT algorithm** [Schöning, 1999] could be quadratically accelerated using amplitude amplification [Dürr & Høyer, 1996]. This resulted in quantum runtimes of the form:

\[
O(\sqrt{T(n)}\, \text{poly}(n)),
\]

where \(T(n)\) is the classical randomized runtime. These methods remained fundamentally tied to treating SAT as a **black-box search problem**, without exploiting the structural or geometric properties of its solution space.

---

## Measurement-Driven Quantum SAT Solvers

A key conceptual shift occurred in the late 2010s when SAT solvers based on **sequential projective measurements** were introduced (e.g., the 2017 proposal). These solvers replaced amplitude amplification with **direct projection onto clause-satisfying subspaces**, iteratively refining the quantum state by eliminating violating assignments.

By 2025, refinements incorporated improved clause ordering, stabilizing projections, and heuristic measurement schedules. These works demonstrated that measurement-based solvers can outperform naive projection strategies but still rely on **fixed measurement bases**. No adaptive geometric mechanism was used to deform or rotate the measurement basis before applying clause projectors. As a result, the projections remain vulnerable to collapse into undesirable subspaces, especially in instances with low clause redundancy or sparse satisfying assignments.

---

## Sparse Ground States and Structured Ansatz Research

Parallel developments in quantum optimization revealed that many constraint satisfaction problems, including SAT, have **sparse ground states**. Techniques such as the **Variational Quantum Eigensolver (VQE)** [Peruzzo et al., 2014] and the **Quantum Approximate Optimization Algorithm (QAOA)** [Farhi et al., 2014] attempted to exploit this structure by preparing parameterized ansätze that approximate low-energy or satisfying configurations.

Further studies explored structured ansatz families, Hamiltonian sparsity, and state overlap amplification. However:

1. These methods are **variational**, requiring repeated classical–quantum iterations.  
2. They are restricted by **ansatz expressibility** and **circuit depth limitations**.  
3. They do not utilize **measurement sequences** as their core computational mechanism.  

Consequently, they never addressed the core obstacle in measurement-driven SAT: how to geometrically position the quantum state prior to projection to maximize clause satisfaction success.

---

## Quantum Geometric Control and Manifold Optimization

In parallel with SAT research, significant advances were made in **quantum geometric control**, focusing on:

- **Stiefel manifolds** (spaces of orthonormal frames)  
- **Grassmannians** (spaces of subspaces)  
- **Flag manifolds** (spaces of nested subspaces)

Notable contributions include works using **Riemannian gradients**, **retraction-based optimization**, and **geodesic approximations** for designing quantum gates, state preparation protocols, and Hamiltonian simulation [Absil et al., 2008; Dong & Petersen, 2010].

Despite their power, these geometric tools remained confined to quantum control and were **never integrated into SAT-solving algorithms**. The idea of interpreting SAT as a problem of **geodesic navigation toward solution subspaces**, or **optimizing measurement bases via Stiefel manifold gradients**, remained unexplored.

---

## The Gap

Across the evolution from amplitude amplification to measurement-driven solvers, the following elements remain absent from all known peer-reviewed research:

1. **Riemannian optimization of measurement bases** that maximize clause success probability.  
2. **Modeling SAT-solving as navigation through a flag manifold** corresponding to increasing clause satisfaction.  
3. **Use of quantum geometric metrics**, such as the Fubini–Study distance, as guidance signals.  
4. **Systematic geometric steering** to avoid collapse into undesired subspaces during projection.  
5. **A solver architecture** that replaces classical–quantum variational loops and non-adaptive measurement with a principled geometric control framework.

Thus, although the literature has independently developed measurement-driven SAT solvers and geometric methods for quantum control, **no work unifies these into a geometry-guided SAT solver**. The present work addresses this gap by constructing a solver that uses Stiefel manifold optimization to adaptively select measurement bases, thereby guiding the quantum state toward the solution subspace in a geometrically informed manner.

## 2. This Work

1. **Geometric Reformulation of Measurement-driven SAT Solving**

   * This work frames clause-by-clause satisfaction as navigation through a hierarchy of subspaces, conceptualized as a flag manifold.

2. **Stiefel Manifold Optimization for Measurement Bases**

   * Prior to each clause projection, a unitary transformation is optimized using gradient-based Riemannian methods and orthonormal-frame retraction.
   * This basis transformation increases the probability of successful projection onto clause-satisfying subspaces.

3. **Integration of Quantum Geometric Metrics**

   * Fubini–Study angles are computed at each step to quantify alignment between the evolving state and the full-solution subspace.
   * This information provides insight into state evolution and guides parameter choices.

4. **A Complete Solver Implementation without Variational Circuits**

   * Unlike VQE or QAOA approaches, this solver uses no parametrized quantum circuits.
   * The computational primitive is projective measurement paired with optimized basis rotations.

5. **Benchmarking and Comparative Analysis**

   * The solver is compared against an unguided measurement baseline.
   * Empirical results demonstrate significantly improved success probabilities and more stable state trajectories.

## 3. License

This project is licensed under the **Polyform Noncommercial License**.

You may use, modify, and share this software only for **noncommercial** purposes, under the terms specified in the Polyform Noncommercial license.

For the full text of the license, see the [`LICENSE`](./LICENSE) file in this repository.


# Bibliography

- Absil, P.-A., Mahony, R., & Sepulchre, R. (2008). *Optimization Algorithms on Matrix Manifolds*. Princeton University Press.  
- Brassard, G., Høyer, P., Mosca, M., & Tapp, A. (2002). Quantum amplitude amplification and estimation. *Contemporary Mathematics*, 305, 53–74.  
- Dong, D., & Petersen, I. R. (2010). Quantum control theory and applications: A survey. *IET Control Theory & Applications*, 4(12), 2651–2671.  
- Dürr, C., & Høyer, P. (1996). A quantum algorithm for finding the minimum. arXiv:quant-ph/9607014.  
- Farhi, E., Goldstone, J., & Gutmann, S. (2014). A quantum approximate optimization algorithm. arXiv:1411.4028.  
- Grover, L. K. (1996). A fast quantum mechanical algorithm for database search. *Proceedings of STOC ‘96*.  
- Peruzzo, A., et al. (2014). A variational eigenvalue solver on a quantum processor. *Nature Communications*, 5, 4213.  
- Schöning, U. (1999). A probabilistic algorithm for k-SAT and constraint satisfaction problems. *FOCS ‘99*.  




