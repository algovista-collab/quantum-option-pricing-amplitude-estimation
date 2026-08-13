# Quantum Option Pricing via Amplitude Estimation

A Qiskit implementation of the quantum option pricing methodology from
**Stamatopoulos et al., "Option Pricing using Quantum Computers" (2020)** — a JPMorgan Chase
& IBM Quantum collaboration, [arXiv:1905.02666](https://arxiv.org/abs/1905.02666).

**Full write-up:** [Implementing "Option Pricing using Quantum Computers" in Qiskit](https://medium.com/@arpitha.rajeev37/implementing-option-pricing-using-quantum-computers-in-qiskit-6367982c3343)
**Paper implemented:** [arXiv:1905.02666](https://arxiv.org/abs/1905.02666)

## What this covers

The paper's core methodology for pricing options on a gate-based quantum computer using
**Amplitude Estimation (AE)**, which provides a quadratic speedup over classical Monte Carlo
simulation for computing expected payoffs — built up from QFT and Quantum Phase Estimation,
through every option type the paper describes, to a real-hardware reproduction of the paper's
own experiment.

## Progress

| # | Notebook | Covers | Status |
|---|---|---|---|
| 1 | `01_qft_qpe_foundations.ipynb` | QFT, phase kickback, Quantum Phase Estimation, worked from first principles and verified against Qiskit's `QFTGate` | Done |
| 2 | `02_amplitude_estimation_core.ipynb` | The `A` and `Q` operators -- `Q` built manually from two reflections and verified against the rotation theory; all three AE variants compared | Done |
| 3 | `03_vanilla_option.ipynb` | European call option -- distribution loading, comparator + payoff rotation, hand-verified against classical ground truth, real hardware execution | Done |
| 4 | `04_portfolio_options.ipynb` | Portfolios of options (call spread, Section 4.1.2) -- multiple strikes, multiple comparators | Done |
| 5 | `05_weighted_sum_adder.ipynb` | The quantum weighted-sum operator (Appendix A) -- half/full adder derivation, verified in isolation before use | Done |
| 6 | `06_basket_option.ipynb` | Basket options (Section 4.2.1) -- multi-asset, weighted-sum operator combining two assets | Done |
| 7 | `07_asian_option.ipynb` | Asian options (Section 4.2.2) -- equal-weighted average across time checkpoints | Done |
| 8 | `08_barrier_option.ipynb` | Barrier options (Section 4.2.3) -- path-dependent, logical OR across barrier checks, reproduced using the paper's own stated parameters | Done |
| 9 | `09_section5_reproduction.ipynb` | Section 5's real-hardware experiment -- the paper's exact parameters, Maximum Likelihood AE, CNOT-stretch error mitigation, Richardson extrapolation | In progress |

All five option types described in the paper (vanilla, portfolios, basket, Asian, barrier) are
implemented, verified against classical ground truth, and executed on real IBM Quantum hardware.
Basket and Asian options were run on real hardware here -- something the original paper only
ever simulated.

## Validation approach

Every circuit is validated in stages before being used as a building block for the next: first
against an independently, classically computed ground truth using exact statevector inspection,
then via Amplitude Estimation on a noiseless simulator, then -- where applicable -- on real IBM
Quantum hardware. Several notebooks document real bugs found and fixed along the way (a
comparator-branch payoff mismatch, a `qiskit-algorithms` real-hardware transpilation issue, a
rotation-angle convention mismatch against the paper's stated formula) -- these are left in the
notebooks and the accompanying blog posts, not smoothed over, since the debugging process is
often as informative as the final working result.

## Setup

```
pip install qiskit qiskit-finance qiskit-algorithms qiskit-aer qiskit-ibm-runtime sympy scipy
```

## References

- N. Stamatopoulos, D.J. Egger, Y. Sun, C. Zoufal, R. Iten, N. Shen, S. Woerner.
  *"Option Pricing using Quantum Computers."* Quantum 4, 291 (2020).
  [arXiv:1905.02666](https://arxiv.org/abs/1905.02666)
- Y. Suzuki, S. Uno, R. Raymond, T. Tanaka, T. Onodera, N. Yamamoto.
  *"Amplitude estimation without phase estimation."* Quantum Information Processing 19, 75 (2020).
