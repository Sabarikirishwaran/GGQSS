# Geometry-Guided Quantum SAT Solver

This project presents a geometry-guided, measurement-driven quantum SAT solver that leverages Riemannian optimization techniques to navigate Hilbert space efficiently toward satisfying assignments of Boolean formulas. The work integrates concepts from quantum measurement theory, geometric control, and manifold optimization, providing a novel framework for clause-by-clause quantum constraint satisfaction.

---



## 2. Contribution of This Work

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
