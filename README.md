## Computer Aided Engineering (CAE) Project 2: Structural & Beam Analysis Suite

## Project Description
This engineering repository documents the structural modeling, verification, and dynamic cross-platform simulation of a multi-material perpendicular T-joint structure. Designed to model a physical metal table frame, the assembly consists of a horizontal $40\times60\text{ mm}$ Aluminium Alloy rectangular top beam and a vertical $40\times40\text{ mm}$ Stainless Steel square bottom beam, both featuring a $500\text{ mm}$ span and a $2.6\text{ mm}$ shell offset. 

The primary objective of this study was to convert the physical geometry into highly reliable finite element models, predicting structural deflection, stress distributions, boundary condition behaviors, and vibrational responses across varying simulation environments. 

---

## Technical Approach & Cross-Software Methodology

The analysis evaluates structural reactions by staging parallel simulation workflows across a comprehensive engineering suite:

* **SolidWorks (CAD Initialization):** Used to construct the baseline geometric parts, shell offsets, and standard STEP assembly models for downstream deployment.
* **ANSYS Workbench (Non-Linear FEA Solver):** Conducts high-fidelity static and modal studies. To compute highly accurate local interface data, a refined spherical mesh control ($2.75\text{ mm}$ elements) is implemented over a non-linear **Frictional** contact formulation at the beam junction. 
* **FEMAP (Linear FEA Solver):** Slices the hollow geometry to apply structured **Hexagonal Solid Meshing** elements. It resolves deformation and natural frequencies utilizing a linear **Contact** formulation to serve as a direct comparative package.
* **MATLAB (Analytical Reference Matrix Suite):** Executes numerical eigenvalue computations via a 3D Rotordynamics engine to serve as a baseline mathematical benchmark.

---

## Key Analysis Findings

| Engineering Metric | MATLAB (Analytical Reference) | ANSYS Workbench (Non-Linear FEA) | Siemens FEMAP (Linear FEA) |
| :--- | :--- | :--- | :--- |
| **Boundary Conditions** | **Free-Free** (Unconstrained Model) | **Constrained** (Fixed Vertical Base, -1000N Y-Axis Edge Load) | **Constrained** (Fixed Vertical Base, -1000N Y-Axis Edge Load) |
| **First Non-Zero Mode** | $\approx 969.23\text{ Hz}$ (Mode 13) | $\approx 178.98\text{ Hz}$ (Mode 1) | $\approx 178.47\text{ Hz}$ (Mode 1) |
| **Primary Rigidity Behavior** | Captures 8 zero-frequency modes representing unconstrained rigid-body motion. | Shows low torsional stiffness; Mode 2 is a pure **Torsional** shape ($182.93\text{ Hz}$) due to frictional sliding interfaces. | Proves **7.4 times stiffer** in maximum total deformation ($0.000049\text{ m}$ vs $0.00036\text{ m}$); sticking contact resists twisting, pushing torsion out to higher frequencies. |

---

## Analysis Optimization & Validation Filters

* **Eigenmode Filtering Strategy:** Of the 20 processed mode shapes, higher-order modes (above the 10th mode) showcasing non-representative localized warping or extreme numerical instabilities were discarded. Retaining physically significant modes (such as Mode 6's symmetric "S-curve" bending) confirms material-dominated bending resistance independent of boundary definitions.
* **Proposed Suite Enhancements:** Future revisions could achieve closer convergence limits by implementing uniform hexagonal mesh sizes across both FEA software packages, mapping a standardized free-free layout to unify MATLAB comparison, and conducting formal grid convergence index (GCI) studies.

***

> 🖫 **Documentation Access Note**
> Due to repository file size limitations, high-resolution CAD assemblies, complete manufacturing drawings, detailed electrical schematics, and raw FEA simulation datasets are omitted from this directory. Please contact me directly via email to request the complete final version package.
