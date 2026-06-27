# Primordial Black Holes from the Collapse of Fermi-balls

**PHYS 2640 Final Project — Brown University**

*Aman Singh (aman_singh@brown.edu)*

## Overview

This project models the production of Primordial Black Holes (PBHs) via the collapse of Fermi-balls formed during a first-order phase transition in the early universe. The goal is to identify parameters of a scalar-fermion Lagrangian that produce PBHs at the right mass and abundance to explain dark matter.

The system is governed by a Lagrangian coupling a scalar field $\varphi$ to a Dirac fermion $\chi$:

```math
\mathcal{L} = -\frac{1}{2} \partial_\mu \varphi \partial^\mu \varphi - U(\varphi,T) + \bar{\chi} i \gamma_\mu \partial^\mu \chi + y \varphi \bar{\chi} \chi
```

During a first-order phase transition, fermions trapped in the false vacuum are compressed into non-topological solitons (Fermi-balls), which subsequently collapse into PBHs as the Yukawa potential dominates over degeneracy pressure.

## Physics Pipeline

The simulation proceeds in four stages:

1. **Toy Potential** — Scans over the scalar cubic coupling $\mu_3$ in the potential U and temperature T to locate the critical temperature $T_c$ where the false and true vacua are degenerate.

2. **Simulation** — For each ($\mu_3$, y) configuration, with y the Yukawa coupling, computes the Fermi-ball number density, charge, mass, and radius, then the PBH mass and dark matter fraction $f_{\mathrm{PBH}} = \rho_{\mathrm{PBH}}/\rho{\mathrm{DM}}$.

3. **Best Configuration** — Minimizes a $\chi^2$ loss function over the grid to find the configuration closest to $f_{\mathrm{PBH}} = 1$ and $M_{\mathrm{PBH}} \sim 10^{17}$ g (the unconstrained asteroid-mass window).

4. **Monte Carlo Refinement** — Gaussian-samples 2000 points in (log $T_c$, log y) space around the best grid point to finely probe the optimal region.

## Results

The best configuration found is at $\mu_3$ = −50 GeV and y ≈ 0.23, giving:
- Critical temperature: $T_c$ ≈ 47.7 GeV
- PBH mass: $M_{\mathrm{PBH}}$ ≈ 3.75 × 10⁻³³ M☉ (~7.5 g)
- Dark matter fraction: $f_{\mathrm{PBH}}$ ≈ 1.89 (refined to ~0.85 via Monte Carlo)

The PBHs produced are far too light (~1g) to fall in the unconstrained asteroid-mass window (~10¹⁷–10²²g). This is attributed to the weak dependence of $M_{\mathrm{PBH}}$ on $\mu_3$ (scaling as $U_0^{\frac{1}{4}}$), meaning the optimum likely lies far outside the explored parameter space.

## Files

| File | Description |
|------|-------------|
| `pbh_fermi_ball_simulation.ipynb` | Full simulation notebook |
| `pbh_fermi_ball_report.pdf` | Written report |
| `pbh-theory/pbh_fermi_ball_presentation.ipynb` | Presentation on background theory (PHYS 2170 Final Project) |
| `pbh-theory/pbh_overview_report.pdf` | Written report on PBH as DM (PHYS 1280 Final Project) |
| `pbh-theory/pbh_overview_presentation.pdf` | Presentation on PBH as DM (PHYS 1280 Final Project) |

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
| $\eta_{\chi}$ | Fermion–antifermion asymmetry | 10⁻²⁵ |
| $w_0$ | T=0 true vacuum vev | 400 GeV |
| $M_{\varphi}$ | Scalar mass in true vacuum | 100 GeV |
| $c_{\mathrm{th}}$ | Thermal mass coefficient | 0.4 |
| g* | Relativistic degrees of freedom | 100 |

## References

1. A. M. Green, *Primordial black holes as a dark matter candidate – a brief overview* (2024), [arXiv:2402.15211](https://arxiv.org/abs/2402.15211)
2. J.-P. Hong, S. Jung, and K.-P. Xie, *Fermi-ball dark matter from a first-order phase transition*, Physical Review D **102** (2020)
3. K. Kawana and K.-P. Xie, *Primordial black holes from a cosmic phase transition: The collapse of fermi-balls*, Physics Letters B **824**, 136791 (2022)
