# Primordial Black Holes from the Collapse of Fermi-balls

**PHYS 2640 Final Project — Brown University**
*Aman Singh (aman_singh@brown.edu)*

## Overview

This project models the production of Primordial Black Holes (PBHs) via the collapse of Fermi-balls formed during a first-order phase transition in the early universe. The goal is to identify parameters of a scalar-fermion Lagrangian that produce PBHs at the right mass and abundance to explain dark matter.

The system is governed by a Lagrangian coupling a scalar field φ to a Dirac fermion χ:

```
L = -½ ∂μφ∂μφ - U(φ,T) + χ̄ i∂̸ χ + yφχ̄χ
```

During a first-order phase transition, fermions trapped in the false vacuum are compressed into non-topological solitons (Fermi-balls), which subsequently collapse into PBHs as the Yukawa potential dominates over degeneracy pressure.

## Physics Pipeline

The simulation proceeds in four stages:

1. **Toy Potential** — Scans over the scalar cubic coupling μ₃ and temperature T to locate the critical temperature Tₒ where the false and true vacua are degenerate.

2. **Simulation** — For each (μ₃, y) configuration, computes the Fermi-ball number density, charge, mass, and radius, then the PBH mass and dark matter fraction fₚBH = ρₚBH/ρDM.

3. **Best Configuration** — Minimizes a χ² loss function over the grid to find the configuration closest to fₚBH = 1 and Mₚbh ~ 10¹⁷g (the unconstrained asteroid-mass window).

4. **Monte Carlo Refinement** — Gaussian-samples 2000 points in (log Tₒ, log y) space around the best grid point to finely probe the optimal region.

## Results

The best configuration found is at μ₃ = −50 GeV and y ≈ 0.23, giving:
- Critical temperature: Tₒ ≈ 47.7 GeV
- PBH mass: Mₚbh ≈ 3.75 × 10⁻³³ M☉ (~7.5 g)
- Dark matter fraction: fₚBH ≈ 1.89 (refined to ~0.85 via Monte Carlo)

The PBHs produced are far too light (~1g) to fall in the unconstrained asteroid-mass window (~10¹⁷–10²²g). This is attributed to the weak dependence of Mₚbh on μ₃ (scaling as U₀^(1/4)), meaning the optimum likely lies far outside the explored parameter space.

## Files

| File | Description |
|------|-------------|
| `Aman_Singh_PHYS_2640_Final_Project.ipynb` | Full simulation notebook |
| `Aman_Singh_PHYS_2640_Final_Project.pdf` | Written report (APS-style) |

## Requirements

```
numpy
matplotlib
scipy
```

Install with:

```bash
pip install numpy matplotlib scipy
```

## Usage

Open and run the notebook end-to-end:

```bash
jupyter notebook Aman_Singh_PHYS_2640_Final_Project.ipynb
```

The main driver (last cell) defines the parameter space and runs the full pipeline in order: toy potential → simulation → best configuration → Monte Carlo refinement → plots.

Fixed parameters (from Hong et al. 2020 and Kawana & Xie 2021):

| Parameter | Description | Value |
|-----------|-------------|-------|
| ηχ | Fermion–antifermion asymmetry | 10⁻²⁵ |
| w₀ | T=0 true vacuum vev | 400 GeV |
| Mφ | Scalar mass in true vacuum | 100 GeV |
| c_th | Thermal mass coefficient | 0.4 |
| g* | Relativistic degrees of freedom | 100 |

## References

1. A. M. Green, *Primordial black holes as a dark matter candidate – a brief overview* (2024), [arXiv:2402.15211](https://arxiv.org/abs/2402.15211)
2. J.-P. Hong, S. Jung, and K.-P. Xie, *Fermi-ball dark matter from a first-order phase transition*, Physical Review D **102** (2020)
3. K. Kawana and K.-P. Xie, *Primordial black holes from a cosmic phase transition: The collapse of fermi-balls*, Physics Letters B **824**, 136791 (2022)
