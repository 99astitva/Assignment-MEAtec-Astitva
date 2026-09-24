# Assignment-MEAtec-Astitva

## A123 ANR26650M1B LFP Cell Modelling and Calibration using PyBaMM

### Overview

This project develops and calibrates a Doyle-Fuller-Newman (DFN) electrochemical model for the A123 ANR26650M1B (Lithium Werks) 2.5 Ah LFP/Graphite cell using PyBaMM.

The work is divided into three stages:

1. Baseline DFN simulation using the Prada2013 parameter set.
2. Parameter calibration and optimization using discharge and HPPC data.
3. Final optimized DFN / MP-DFN validation model.

---

## Software Requirements

Install the required Python packages:

```bash
pip install pybamm numpy scipy matplotlib
```

---

## Required Data Files

Place the following files in the same working directory as the notebooks/scripts:

```text
HPPC_5458.mat
1C_Discharge.mat
```

---

# 1. DFN Simulation (Baseline Model)

### File

```text
DFN simulation
```

### Purpose

This notebook contains the initial DFN model before optimization.

The model:

- Uses the Prada2013 parameter set.
- Loads HPPC current and voltage data.
- Applies the HPPC current profile to a DFN model.
- Simulates terminal voltage.
- Compares simulated voltage with experimental voltage.
- Calculates RMSE, MAE and maximum voltage error.
- Generates voltage and residual plots.

### How to Run

Open the notebook and execute:

```python
Run All Cells
```

### Required Input

```text
HPPC_5458.mat
```

### Outputs

```text
Measured vs Simulated Voltage Plot
Voltage Residual Plot
RMSE
MAE
Maximum Voltage Error
```

### Notes

A scaled-current approach was used during the initial study to obtain a stable baseline model and identify parameter mismatches prior to calibration.

---

# 2. DFN Optimisation Steps

### File

```text
DFN optimisation steps.html
```

### Purpose

This notebook documents the complete optimization and calibration workflow.

The following studies were performed:

#### Stoichiometry Optimization

Optimized:

```text
theta_n_init
theta_p_init
```

#### Geometry Calibration

Optimized:

```text
Negative electrode thickness
Positive electrode thickness
Positive active material volume fraction
```

#### OCP Calibration

Implemented:

```text
Literature-based LFP cathode OCP
Positive OCP voltage shift
```

#### Dynamic Parameter Calibration

Optimized:

```text
Positive solid diffusivity
Exchange-current multipliers
Electrolyte conductivity multiplier
```

#### HPPC Validation

Evaluated:

```text
Overall RMSE
Charge pulse RMSE
Discharge pulse RMSE
Rest voltage error
Bias
```

#### MP-DFN Development

Introduced:

```text
Particle-size distribution
```

to improve transient response prediction.

### How to Run

Execute the notebook sequentially from top to bottom:

```python
Run Cells Sequentially
```

### Required Inputs

```text
1C_Discharge.mat
HPPC_5458.mat
```

### Outputs

```text
Optimized Stoichiometries
Optimized Geometry Parameters
Optimized Dynamic Parameters
Calibration Plots
Validation Plots
Intermediate RMSE Results
```

---

# 3. DFN Optimised Model

### File

```text
DFN optimised model.html
```

### Purpose

This notebook contains the final calibrated DFN / MP-DFN model.

The model includes:

- Optimized electrode stoichiometries.
- Optimized electrode geometry.
- Literature-based LFP cathode OCP.
- Positive OCP alignment correction.
- Calibrated diffusivity.
- Calibrated electrochemical kinetics.
- Calibrated electrolyte transport properties.
- Particle-size distribution modelling.
- HPPC validation metrics.

### How to Run

Execute:

```python
Run All Cells
```

### Required Input

```text
HPPC_5458.mat
```

### Outputs

```text
Measured vs Simulated Voltage Plot

Voltage Residual Plot

Overall RMSE

Overall MAE

Maximum Error

Charge Pulse RMSE

Discharge Pulse RMSE

Rest Period RMSE

Bias Analysis

Particle Size Distribution Plots

Physical Variable Plots
```

---

# Final Optimized Parameters

```text
Initial negative stoichiometry (theta_n_init) = 0.905

Initial positive stoichiometry (theta_p_init) = 0.5075

Negative electrode thickness = 129e-6 m

Positive electrode thickness = 171e-6 m

Positive active material volume fraction = 0.55

Positive particle radius = 2.5e-6 m

Positive solid diffusivity = 1.0e-13 m²/s

Positive exchange-current multiplier = 30.0

Negative exchange-current multiplier = 30.0

Electrolyte conductivity multiplier = 1.6

Electrolyte diffusivity multiplier = 1.0

Contact resistance = 0 Ω

Model temperature = 296.62 K

Positive OCP voltage shift = +0.10 V
```

---

# Summary of Results

### Baseline DFN

```text
RMSE ≈ 0.19 V
```

Observations:

```text
Large voltage mismatch
Capacity mismatch
Poor pulse prediction
```

### Calibrated DFN

```text
1C Discharge RMSE ≈ 26 mV
HPPC RMSE ≈ 30 mV
```

Observations:

```text
Improved voltage prediction
Improved discharge behaviour
Improved transient response
```

### MP-DFN

```text
HPPC RMSE ≈ 28 mV
```

Observations:

```text
Best overall HPPC prediction
Improved pulse matching
Improved charge/discharge transient behaviour
```

---

# Notes

- Prada2013 was used as the baseline parameter set.
- A literature-derived LFP cathode OCP was incorporated for improved voltage prediction.
- Calibration was performed using 1C discharge and HPPC datasets.
- Particle-size distribution modelling was introduced through an MP-DFN formulation.
- The final model achieves approximately 26–30 mV voltage RMSE while maintaining physical interpretability.
- Remaining model error is primarily attributed to LFP hysteresis and phase-transition behaviour not explicitly represented in the standard DFN formulation.
