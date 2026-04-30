# Modular-Wing-Flight-Test
Independent UAS flight test program characterizing lift and drag  performance across interchangeable wing configurations using XFLR5, ANSYS FLuent, ArduPlane telemetry, and custom Python analysis tools.
# Modular Wing Comparative Aerodynamics — UAS Flight Test Program

## Overview
Independent engineering project designing, fabricating, and flight 
testing a custom 3D-printed unmanned aircraft system (UAS) to 
characterize and compare aerodynamic performance across three 
interchangeable wing configurations.

The program is structured and executed to professional flight test 
standards — including a formal Systems Requirements Document, 
pre-flight aerodynamic predictions, written test cards, structured 
flight test execution, and a final Flight Test Report with measured 
versus predicted analysis.

## Objectives
- Design a common fuselage platform with modular, interchangeable 
  wing assemblies
- Characterize lift and drag polars (CL vs AoA, CL vs CD) for three 
  distinct wing configurations
- Compare flight-derived aerodynamic coefficients against XFLR5 and 
  ANSYS Fluent pre-flight predictions
- Develop a repeatable data acquisition and post-processing pipeline 
  from ArduPlane Blackbox telemetry

## Wing Test Matrix

| Config | Airfoil | Planform | Test Variable |
|--------|---------|----------|---------------|
| WING-A | NACA 0009 | Rectangular, AR 5 | Baseline |
| WING-B | MH45 | Rectangular, AR 5 | Airfoil effect |
| WING-C | MH45 | Tapered, AR 7 | Planform effect |

## Technical Approach

**Aerodynamic Design — XFLR5**
2D airfoil polar analysis at Re 100k–300k to select airfoil 
candidates based on CL/CD efficiency, CLmax, pitching moment 
behavior, and stall characteristics. 3D VLM wing analysis to 
validate planform geometry, CG location, and predict full aircraft 
polars prior to build.

**CFD Validation — ANSYS Fluent**
Full 3D Navier-Stokes analysis on final airframe geometry to 
generate high-fidelity pre-test aerodynamic predictions. Pressure 
distribution and flow separation analysis for each wing 
configuration.

**Hardware Platform**
- Airframe: Custom 3D-printed flying wing, FDM/PLA
- Motor: GT2205 2450KV brushless, 4S LiPo
- Flight controller: SpeedyBee F405 Wing Mini (ArduPlane)
- Data acquisition: ArduPlane Blackbox at 100Hz IMU + GPS

**Flight Test Execution**
Structured test campaign following formal test cards. Stabilized 
test points at three airspeeds (near-stall, cruise, fast) per wing 
configuration. All configurations flown in same session to control 
for environmental variability.

**Post-Flight Analysis — Python**
Custom data pipeline processing raw Blackbox .bbl logs to extract 
aerodynamic coefficients. Measured CL/CD polars overlaid against 
XFLR5 and OpenFOAM predictions.


## Program Status

| Phase | Status |
|-------|--------|
| Systems Requirements Document | Complete |
| Airfoil selection — XFLR5 2D analysis | Complete |
| 3D wing analysis — XFLR5 VLM | Complete |
| Pre-flight analysis pipeline — Python/Jupyter |🔄 In progress|
| Airframe CAD — Fusion 360 | 🔄 In progress |
| CFD analysis — ANSYS Fluent | 🔄 In progress |
| Fabrication | Planned |
| Flight test campaign | Planned |
| Post-flight analysis | Planned |
| Flight Test Report | Planned |

## Background
This project bridges hands-on hardware and full-loop systems 
engineering experience with an existing background in flight data 
analysis, 6DOF dynamics evaluation, and telemetry processing from 
professional autonomous aerostat systems development.

## Author
Colin Y. Cooper
Aerospace Engineer — Flight Data Analysis & UAS Systems
[https://www.linkedin.com/in/colin-cooper-a1a13614a/] | [colinycooper@gmail.com]
