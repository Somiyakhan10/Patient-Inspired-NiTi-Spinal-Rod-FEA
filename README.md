# Patient-Inspired NiTi Spinal Rod FEA

### Finite Element Analysis of a Scoliotic Spine Under Corrective Loading

[![COMSOL](https://img.shields.io/badge/COMSOL-6.1-blue)](https://www.comsol.com)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Status](https://img.shields.io/badge/Status-Complete-brightgreen)]()
[![Field](https://img.shields.io/badge/Field-Biomechanics-orange)]()

A computational study of a patient-inspired scoliotic spine under 
corrective loading, motivated by NiTi (Nitinol) shape memory alloy 
spinal rods used in scoliosis surgery.

---

## 📖 Introduction

Scoliosis is a three-dimensional deformity of the spine affecting 
2–3% of adolescents worldwide. When the lateral curvature exceeds 
40–50°, surgical correction with instrumented spinal fusion becomes 
necessary. Modern systems increasingly use **NiTi (Nitinol) shape 
memory alloy rods** due to their superelasticity, biocompatibility, 
and ability to apply gradual corrective forces.

This project builds a **simplified finite element model** of a 
scoliotic spine and simulates its mechanical response under a 
40 N corrective load. The goal is to evaluate the stress distribution 
and safety margin of the spine under clinically relevant loading.


---

## 📊 Results

### 1. Von Mises Stress Distribution

<img width="969" height="614" alt="image" src="https://github.com/user-attachments/assets/47917b10-40e5-4ecd-b1d5-7077e628dd69" />


**Peak von Mises stress: 1.1 MPa** at the top vertebra where the 
corrective load is applied. This is ~100× below the yield strength 
of cortical bone (~120 MPa), confirming a wide safety margin.



### 2. Solver Convergence

<img width="974" height="708" alt="image" src="https://github.com/user-attachments/assets/0fdec9fe-ad30-43bb-8c3d-942470a2c8a6" />


The nonlinear solver converged in **25 Newton iterations** with the 
residual dropping from 3 × 10² to 5 × 10⁻². Solution time: **84 seconds**.

### 5. Mesh

<img width="981" height="666" alt="image" src="https://github.com/user-attachments/assets/bcdcb957-da2b-4742-921c-dd8b8d64f4c7" />


Coarse tetrahedral mesh with ~10,000 elements, sufficient for 
capturing the load path at this scale.

### 6. Geometry

<img width="988" height="592" alt="image" src="https://github.com/user-attachments/assets/230b97b5-0c5d-40c3-818c-36c4b90d5a9e" />


10 vertebral bodies (35 × 25 × 14 mm) and 9 intervertebral discs 
(6 mm thick) with a scoliotic curvature amplitude of 28 mm.

---

## 📋 Key Results Summary

| Quantity | Value | Unit |
|---|---|---|
| Peak von Mises stress | 1.1 | MPa |
| Peak total displacement | 0.5 | mm |
| Peak equivalent strain | 1.1 × 10⁻⁵ | — |
| Degrees of freedom | 94,220 | — |
| Newton iterations | 25 | — |
| Solution time | 84 | s |
| Safety factor vs. bone yield | ~100× | — |

---

## 🔧 Methods Overview

### Geometry

| Component | Count | Dimensions |
|---|---|---|
| Vertebral bodies | 10 | 35 × 25 × 14 mm (ellipsoids) |
| Intervertebral discs | 9 | 15 mm radius × 6 mm thick |
| Spine length | — | 200 mm |
| Scoliotic amplitude | — | 28 mm lateral offset |

### Material Properties

| Property | Value | Justification |
|---|---|---|
| Young's modulus (E) | 100 MPa | Simplified cortical bone |
| Poisson's ratio (ν) | 0.30 | Literature average |
| Density (ρ) | 1900 kg/m³ | Typical bone density |

### Boundary Conditions

| BC | Location | Value |
|---|---|---|
| **Fixed Constraint** | Bottom vertebra (z ≈ 0) | All DOF = 0 |
| **Boundary Load** | Top vertebra (z ≈ 180) | F = (0, 0, −40) N |

### Mesh

- Free tetrahedral, `hauto = 8` (very coarse)
- ~10,000 elements
- Verified convergence for this load case

### Solver

| Setting | Value |
|---|---|
| Study | Stationary |
| Physics | Solid Mechanics (linear elastic) |
| Linear solver | MUMPS (direct) |
| Nonlinear solver | Newton (automatic) |
| Solution time | 84 s |

---

## 🔮 Future Work

This project provides a foundation for more advanced biomechanical 
studies. The following extensions are planned:

- [ ] **Add the NiTi rod** — include the spinal rod geometry with 
      Form Assembly and Contact Pairs to model the rod-vertebra 
      interface properly

- [ ] **Model NiTi superelasticity** — replace linear elasticity with 
      COMSOL's Shape Memory Alloy (SMA) material law to capture the 
      superelastic hysteresis of NiTi

- [ ] **Include paraspinal muscle forces** — add follower loads 
      representing the erector spinae and multifidus muscles that 
      carry physiological loads

- [ ] **Patient-specific geometry** — import vertebra and disc 
      geometries from CT or MRI scans for individualized modeling

- [ ] **Fatigue analysis** — evaluate the NiTi rod's performance over 
      millions of cyclic loading events (walking, sitting, breathing)

- [ ] **Parametric study** — sweep rod diameter (4–7 mm) and 
      curvature (0.2–0.8) to identify optimal implant geometry

- [ ] **Shape optimization** — use topology or shape optimization 
      to minimize peak stress while maintaining corrective capability
