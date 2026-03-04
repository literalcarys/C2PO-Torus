# C2PO-Torus: Clumpy 2-Phase Obscuring Torus Model

**A physically-based X-ray spectral model for AGN, designed as a counterpart to the SKIRTOR SED model.**

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![arXiv](https://img.shields.io/badge/arXiv-26xx.xxxxx-B31B1B.svg)](https://arxiv.org/)

## Overview

**C2PO-Torus** (Clumpy 2-Phase Obscuring Torus) is a new X-ray spectral model generated using the state-of-the-art radiative transfer code [SKIRT](https://skirt.ugent.be/). 

It is designed to be self-consistent with the **SKIRTOR** model used in infrared SED fitting (e.g., in CIGALE). By using C2PO-Torus for X-ray analysis and SKIRTOR for SED fitting, astronomers can constrain physical torus parameters (such as opening angle and inclination) more accurately, bridging the gap between X-ray and mid-IR/SED analysis.

### Key Features
*   **Physically Motivated:** Based on a "two-phase" wedge-shaped geometry (high-density clumps + low-density interclump media).
*   **SKIRTOR Compatible:** Uses the exact same geometry and parameter space as the popular IR model.
*   **Full Radiative Transfer:** Includes anisotropic scattering, absorption, and re-emission simulated via Monte Carlo methods.
*   **XSPEC Ready:** Provided as additive table models for easy integration into standard fitting workflows.

---

## Model Geometry

The model assumes a clumpy wedge-shaped torus where dust is distributed between high-density clumps and low-density interclump regions. The primary emission is anisotropic, reshaping the inner radius of the torus according to the polar angle.

*   **Geometry:** Wedge-shaped torus with spherical clumps.
*   **Emission Profile:** Netzer (1987) anisotropic emission ($L(\theta) \propto \cos \theta (2 \cos \theta + 1)$).
*   **Phases:** 
    1.  **C2POTorusD:** Represents the obscured intrinsic powerlaw emission (Direct).
    2.  **C2POTorusR:** Represents the reprocessed emission (scattered and reflected).

---

## Installation & Usage

### 1. Download
Download the XSPEC table models from the [models directory](./models) (Coming Soon):
*   C2POTorusD.fits
*   C2POTorusR.fits

### 2. Load into XSPEC
Load the files as additive table models:

XSPEC12> model phabs * (atable{C2POTorusD.fits} + const*atable{C2POTorusR.fits})

As described in Gilbert et al. (2026), the standard configuration in XSPEC contains the following:

*   **phabs:** Galactic absorption.
*   **const:** Scaling constant for the reprocessed component (can be fixed at 1 or left free).

**Linking:** All physical parameters (Inclination, Opening Angle, etc.) should be tied between the D and R components during fitting.

---

## Parameters

The model grid covers the following parameter space:

| Parameter | Symbol | Range | Description |
| :--- | :---: | :--- | :--- |
| **Photon Index** | $\Gamma$ | $1.4 - 2.6$ | Slope of the primary power law. |
| **Eq. Column Density** | $N_{H,eq}$ | $10^{21} - 5 \times 10^{25}$ cm$^{-2}$ | Average equatorial column density. |
| **Inclination** | $i$ | $0^\circ - 90^\circ$ | Viewing angle ($0^\circ$=Face-on/Type 1, $90^\circ$=Edge-on/Type 2). |
| **Opening Angle** | $\Theta$ | $10^\circ - 80^\circ$ | Half-opening angle of the torus. |
| **Redshift** | $z$ | - | Source redshift. |
| **Normalization** | $norm$ | - | Normalization of the model. |

*Note: Following SKIRTOR, the concentration parameter $p$ and polar gradient $q$ are fixed in the standard grid to optimize fitting efficiency.*

---

## Citation

If you use C2PO-Torus in your research, please cite the following paper:

**A New Hope for AGN SED Fitting: X-Ray Spectral Analysis of 12MGS AGN with the C2PO-Torus Model**  
*Carys J. E. Gilbert, Lucia Marchetti, Luigi Barchiesi, and Mattia Vaccari (2026)*  
MNRAS (Preprint).


## Contact

For questions regarding the model or installation, please contact:
**Carys J. E. Gilbert**  
Department of Astronomy, University of Cape Town  
Email: glbcar006@myuct.ac.za
