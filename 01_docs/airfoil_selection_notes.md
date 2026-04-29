# Aerodynamic Analysis — Findings & Selection Rationale
**Document:** Airfoil Selection & Wing Configuration Analysis 
**Author:** Colin Y. Cooper
**Tool:** XFLR5
**Date:** April 2026
**Status:** Complete - Pre Flight prediction phase

--- 

## 1. Analysis Objectives 

1. Select the optimal airfoil for a low Reynolds number flying wing UAS operating at Re 130,000–300,000
2. Define three wing configurations for comparative flight testing
3. Generate quantitative pre-flight aerodynamic predictions for each configuration to be compared against measured flight test data

---

## 2. Operating Conditions & Reynolds Number

Reynolds number governs airfoil behavior at this scale and was the primary design driver for the airfoil selection. Motor selection drove reynolds number airspeed assumption. 

**Reynolds number equation:**

Re = (V × c) / ν

Where:
- V = airspeed (m/s)
- c = chord length (m) = 0.180m
- ν = kinematic viscosity of air = 1.5×10⁻⁵ m²/s

| Flight Condition | Speed (m/s) | Speed (km/h) | Reynolds Number |
|-----------------|-------------|--------------|-----------------|
| Near stall      | 11          | 40           | ~132,000        |
| Slow test point | 15          | 54           | ~180,000        |
| Cruise          | 22          | 79           | ~264,000        |
| Fast test point | 28          | 101          | ~336,000        |

**Analysis range:** Re 100,000 / 200,000 / 300,000  
**Primary focus:** Re 200,000 (closest to cruise condition)

### Why Reynolds number is a key design driver at this scale

At Re 100,000 - 300,000 (low Re regime), Boundary layer differs significantly from full-scale aircraft. Laminar flow seperation happens early causing laminar seperation bubbles which result 
in sudden stall and high drag/low lift. Airfoil must be specifically designed for this flight regime. 

## 3. Airfoil Selection 

Three airfoils were evaluated:

| Airfoil | Type | Design Intent |
|---------|------|---------------|
| MH45 | Reflexed cambered | Purpose-designed for low Re flying wings |
| NACA 0009 | Symmetric | Classic general-purpose baseline |
| E214 | Cambered (Eppler) | Low Re performance, no reflex |


**MH45*** - Designed specifically for flying wings at Re 100,000 - 500,000. 
Near-zero pitching moment, important for tailless configuration. Well documented performance data available. 

**NACA 0009** - Symmetric airfoil, zero camber means zero pitching moment at zero AoA. 
Ideal baseline because of symmetry, and well documented across wide Re range. 

**E214** - High performance low Re candidate for comparison. Strong lift and efficiency characteristics at low Re


### Criterion 1 - Pitching Moment Coefficient 

On conventional aircrafts horizontal tail provides pitch stability. A flying wing must produce pitch stability from airfoil geometry and wing sweep. 

Negative Cm (nose down moment) means elevons deflect upward to maintain level flight, creating:
- Trim drag - continuous drag throughout flight
- Reduced control effectiveness - less elevon travel available
- Increasing instability as AoA increases toward stall

**Requirement:** Cm must be near zero across the operational angle of attack range at cruise

## Criterion 3 - Maximum Lift Coefficient 

Determines stall speed. SRD requirement: stall speed ≤ 40 km/h.

Stall speed equation:
V_stall = √(2W / (ρ × S × CLmax))

Where W = 5.9N (600g AUW), ρ = 1.225 kg/m³, S = 0.162 m²

Higher CLmax = lower stall speed = safer slow test points.

### Criterion 4 — Stall Character

How abruptly CL drops past CLmax. A gradual rounded peak gives 
warning before stall. A sharp cliff-edge drop is dangerous on a 
flying wing with no tail for recovery assistance.

Evaluated qualitatively from the CL vs Alpha polar shape.

### Criterion 5 — Thickness Ratio

Structural and printability constraint. Minimum ~8% thickness 
required to accommodate 6mm OD carbon spar tube within the section 
at 180mm chord. Maximum ~12% to keep weight manageable.

## 5. XFLR5 Analysis Setup

**Module:** XFoil Direct Analysis  
**Polar type:** Type 1 (fixed speed)  
**AoA sweep:** -6° to +14° in 0.5° increments  
**Reynolds numbers:** 100,000 / 200,000 / 300,000  
**NCrit:** 9 (standard outdoor calm air turbulence level)  
**Forced transitions:** 1.0 top and bottom (free transition)  

---

## 6. 2D Airfoil Analysis Results — Re 200,000

### 6.1 Measured Values


| Parameter | MH45 | NACA 0009 | E214 |
|-----------|------|-----------|------|
| CLmax | 1.15 | 0.90 | 1.30 |
| AoA at CLmax (°) | 13 | 10 | 13 |
| Minimum CD | ~0.010 | ~0.010 | ~0.011 |
| Peak CL/CD | ~60 | ~24 | ~65 |
| AoA at peak CL/CD (°) | ~3–5 | ~3–5 | ~3–5 |
| Cm at AoA = 3° | -0.02 to 0 | ~0 | Negative throughout |
| Cm zero crossing | ~-0.5° | 0° | Never crosses zero |
| Stall speed (m/s) | 7.2 | 8.1 | 6.8 |
| Stall speed (km/h) | 26 | 29 | 24 |

(note: these are approximate values with more accurate representations done in python analysis)

### 6.2 Key Observations

**CL vs Alpha:**
- E214 achieves highest CLmax (1.30) followed by MH45 (1.15) 
  then NACA 0009 (0.90)
- All three airfoils stall between 10–13° 
- MH45 and E214 show later stall than NACA 0009 due to camber

**CL vs CD (Drag Polar):**
- E214 has the leftmost curve — lowest CD at a given CL, 
  highest efficiency in 2D
- MH45 is significantly more efficient than NACA 0009 in the 
  positive CL range (CL/CD ratio ~60 vs ~24 at cruise)
- MH45 is slightly less efficient than NACA 0009 at negative CL

**Cm vs Alpha — Critical Finding:**
- E214: Cm negative across the entire AoA range — persistent 
  nose-down pitching moment. Not suitable for flying wing.
- NACA 0009: Cm = 0 at AoA = 0°, then negative slope with AoA. 
- MH45: Cm between -0.02 and 0 at cruise AoA. Near-zero 
  throughout operating range 

**CD vs Alpha:**
- All three reach minimum CD around AoA = 1°
- Minimum CD values similar (~0.010) confirming viscous drag 
  dominated at zero lift condition

