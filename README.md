# Talon UCAV Aerodynamics Simulation
**Team SkyGuard Alliance** | *Supported by YTB (Yurtdışı Türkler ve Akraba Topluluklar Başkanlığı)*

This repository contains a high-fidelity Computational Fluid Dynamics (CFD) environment for the Talon UCAV. It is optimized for analyzing lift, drag, and pressure distribution at cruise velocities using **OpenFOAM 2512**.

---

## Technical Overview

| Feature | Specification |
| :--- | :--- |
| **Solver** | `simpleFoam` (Steady-state incompressible Navier-Stokes) |
| **Turbulence Model** | k-Omega SST (Shear Stress Transport) |
| **Mesh Density** | ~1.7 Million cells (Hex-dominant) |
| **Flow Velocity** | 20 m/s (Sea Level Conditions) |

---

## Prerequisites

You must have **Docker** installed. Pull the optimized SkyGuard engineering environment from Docker Hub:

```bash
docker pull allrider1127/ytb_teknofest_ucav
```

## EXECUTION


**1. Mesh Generation**

Extract surface features and generate the refined hex-dominant mesh:
```bash

surfaceFeatureExtract
blockMesh
snappyHexMesh -overwrite
```

**2. Domain Decomposition**

Prepare the mesh for parallel processing (set to 4 cores by default):

```bash
decomposePar
```

**3. Solving the Physics**

Execute the solver using MPI:
```bash

mpirun -np 4 simpleFoam -parallel
```

**4. Post-Processing**

Stitch the parallel results back together for visualization:
```bash
reconstructPar
touch view.foam
```

**Open view.foam in ParaView to analyze the results.**

Core Engineering Concepts


    - k-Omega SST: Utilized for its superior ability to predict flow separation and adverse pressure gradients on airfoil surfaces.
    - Mesh Refinement: High-density cell clustering on leading edges and trailing wakes to capture the "Stagnation Point" and boundary layer physics accurately.
    - Wake Analysis: Analysis of the velocity deficit in the wake region allows for iterative fuselage optimization to minimize parasitic drag.

<img width="3999" height="1860" alt="image" src="https://github.com/user-attachments/assets/0904fe96-28d6-4162-b93b-260cf0794011" />


## Visualization Note

The Docker container is optimized for headless compute. For visualization:
1. Ensure **ParaView** is installed on your local host.
2. Run `reconstructPar` in Docker to merge results.
3. Use the `view.foam` dummy file to open the directory in your local ParaView.
