# Quantum Option Pricing via Amplitude Estimation

A Qiskit implementation of the quantum option pricing methodology from
**Stamatopoulos et al., "Option Pricing using Quantum Computers" (2020)** — a JPMorgan Chase
& IBM Quantum collaboration, [arXiv:1905.02666](https://arxiv.org/abs/1905.02666).

**Full write-up:** [Implementing "Option Pricing using Quantum Computers" in Qiskit](https://medium.com/@arpitha.rajeev37/implementing-option-pricing-using-quantum-computers-in-qiskit-6367982c3343)

**Paper implemented:** [arXiv:1905.02666](https://arxiv.org/abs/1905.02666)

## What this covers

The paper's core methodology for pricing options on a gate-based quantum computer using
**Amplitude Estimation (AE)**, which provides a quadratic speedup over classical Monte Carlo
simulation for computing expected payoffs.

Planned scope:

1. **Distribution loading** — encoding a discretized asset-price probability distribution into
   qubit amplitudes via recursive binary-tree rotations, verified against hand-computed
   probability tables.
2. **Payoff circuits** — quantum comparators (Toffoli/CNOT-based) and controlled Y-rotations to
   encode piecewise-linear option payoffs (vanilla calls/puts, multi-strike portfolios).
3. **Amplitude Estimation** — three variants implemented and compared: canonical QPE-based AE,
   Iterative AE, and Maximum Likelihood AE (the method used in the original paper's hardware
   experiments).
4. **Multi-asset & path-dependent options** — basket options and Asian options, using a
   quantum weighted-sum (adder) operator to combine multiple price registers before applying
   the payoff circuit.
5. **Hardware validation** — execution on real IBM Quantum hardware, with CNOT-stretch error
   mitigation and Richardson extrapolation, reproducing the paper's Section 5 methodology.

## Validation approach

Every circuit is validated in two stages before being used as a building block for the next:
first against an independently hand-computed probability/payoff table using exact statevector
inspection, then via Amplitude Estimation on the Aer simulator, cross-checked against classical
Monte Carlo.

## Setup

```
pip install qiskit qiskit-finance qiskit-algorithms qiskit-aer
```

## References

- N. Stamatopoulos, D.J. Egger, Y. Sun, C. Zoufal, R. Iten, N. Shen, S. Woerner.
  *"Option Pricing using Quantum Computers."* Quantum 4, 291 (2020).
  [arXiv:1905.02666](https://arxiv.org/abs/1905.02666)
- Y. Suzuki, S. Uno, R. Raymond, T. Tanaka, T. Onodera, N. Yamamoto.
  *"Amplitude estimation without phase estimation."* Quantum Information Processing 19, 75 (2020).
