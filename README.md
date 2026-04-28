# Talon UCAV Aerodynamics Simulation
**Team 	SkyGuard Alliance**
Yürtdışı Türkler ve Akraba Topluluklar Bakanlığı (YTB)

This repository contains a high-fidelity Computational Fluid Dynamics (CFD) setup for the Talon UCAV. 
It is designed to run within an OpenFOAM 2512 environment (Dockerized) to analyze lift, drag, and pressure
distribution at cruise velocities.

## Technical Specifications
- **Solver:** `simpleFoam` (Steady-state incompressible Navier-Stokes)
- **Turbulence Model:** k-Omega SST (Menter's Shear Stress Transport)
- **Mesh:** ~1.7 Million cells (Hex-dominant via `snappyHexMesh`)
- **Conditions:** 20 m/s airspeed at Sea Level.

## Prerequisites
- **Docker:** Pull the optimized environment:


  ```bash
  
  docker pull allrider1127/ytb_teknofest_ucav
