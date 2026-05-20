# Molecular-Dynamics-Investigation-of-Mechanical-Properties-of-Sugarcane-Bagasse-Fiber-in-LAMMPS

This repository contains a complete LAMMPS molecular dynamics pipeline for atomistic-scale characterization of the mechanical properties of sugarcane bagasse lignocellulosic fiber. The workflow was developed for Q1 journal publication and provides a reproducible framework for simulating the structural and tensile behavior of biomass-based fiber systems.

## Overview

A fully atomistic model consisting of 97,083 atoms was constructed to represent the major lignocellulosic constituents of sugarcane bagasse fiber. The system includes cellulose Iβ (49,875 atoms), arabinoxylan hemicellulose (24,890 atoms), lignin (13,624 atoms), and TIP3P explicit water (7,446 atoms). The simulation box size is approximately 80 × 80 × 215 Å under periodic boundary conditions, and the final equilibrated density reached 1.366 g/cm³, which agrees closely with the experimental target of about 1.35 g/cm³.

## Force Field

The simulations use CHARMM36/CGenFF parameters for cellulose, hemicellulose, and lignin, together with TIP3P water and SHAKE constraints. Long-range electrostatic interactions are treated using PPPM with an accuracy of 1×10⁻⁵. Short-range interactions are modeled using `lj/charmm/coul/long` with a 10–12 Å cutoff and `special_bonds charmm`.

## Simulation Pipeline

The molecular dynamics workflow is organized into five stages:

1. **Stage 0 — Overlap Removal and Thermalization**  
   Soft potential ladder (B1–B8) combined with Langevin dynamics and `nve/limit` stabilization.

2. **Stage 1 — NVT Heating**  
   Controlled heating from 10 K to 300 K.

3. **Stage 2 — Density Equilibration**  
   Box relaxation using `fix deform` and NPT dynamics to approach the target density. The system evolved within the range of 1.17–1.37 g/cm³ before converging.

4. **Stage 3 — NVT Production**  
   A 200 ps reference trajectory generated at 300 K.

5. **Stage 4 — Uniaxial Tensile Deformation**  
   Tensile loading along the Z-axis using an NPT → NVT → NVE protocol at a strain rate of 1×10⁻⁷ fs⁻¹ over 0–1% engineering strain.

## Outputs

The repository provides:

- `tensile_results_final.txt` containing stress–strain data (`σ_zz`, `σ_xx`, `σ_yy`)
- Mechanical property extraction, including Young’s modulus, ultimate tensile strength, Poisson’s ratio, and toughness
- Nine publication-quality Python analysis plots generated using NumPy, Matplotlib, and SciPy
- OVITO-compatible trajectory dump files for all stages
- `tensile_results.xlsx`, a four-sheet Excel summary of the simulation results

## Key Results

- **Equilibrated density:** 1.366 g/cm³
- **Young’s modulus:** ~32–42 GPa
- **Ultimate tensile strength (UTS):** ~521 MPa
- **Stable NPT temperature:** 300 K
- **Total simulation time:** ~750 ps

## Hardware and Software

- **LAMMPS:** 29 Aug 2024
- **Operating system:** Windows 11 with WSL Ubuntu
- **Python:** 3.13
- **Analysis libraries:** NumPy, Matplotlib, SciPy

## Applications

This repository can support research in:

- Natural fiber mechanics
- Lignocellulosic biomass modeling
- Bio-based composite design
- Structure–property relationship analysis
- Sustainable materials engineering

## Repository Goal

The main objective of this work is to provide a reliable and reusable atomistic simulation pipeline for understanding the deformation behavior and mechanical performance of sugarcane bagasse fiber. The workflow is suitable for future extension to chemically modified fibers, moisture-dependent systems, and hybrid bio-composite materials.



## Author

Sadman Shabab Kabir
