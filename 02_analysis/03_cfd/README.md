# CFD Analysis — Ansys Fluent Student

## Setup
Solver: Ansys Fluent 2026 R1 Student
License limit: 1,000,000 cells
Model: Half body with symmetry plane
Turbulence: SST k-omega Gamma Transport
Low Re corrections: enabled

## Boundary Conditions
Inlet: Velocity inlet 22 m/s
       Direction: X=0.9994 Y=-0.0349 (2° AoA)
Outlet: Pressure outlet gauge P=0
Symmetry: Aircraft centerline + top/bottom/far field
Wall: Aircraft surfaces (no-slip)

## Reference Values
Area: 0.081 m² (half wing)
Length: 0.180 m (MAC)
Density: 1.225 kg/m³
Velocity: 22 m/s

## Mesh Strategy
Global size: 15mm
Wing surface: 3mm
Leading edge: 0.5mm
Inflation layers: 7 layers, first cell 0.002mm
y+ target: 30-100 (wall functions)
Total cells: ~900,000

## Results

| Config | AoA | CL    | CD    | L/D  | Notes              |
|--------|-----|-------|-------|------|--------------------|
| WING-B | 0°  | 0.56  | 0.157 | 3.57 | Initial — faceted  |
| WING-B | 0°  | —     | —     | 7.0  | After mesh fixes   |
| WING-B | 2°  | —     | —     | 10.0 | Cruise AoA ✓       |

## Validation Against XFLR5

| Metric    | XFLR5 | CFD  | Gap  | Explanation              |
|-----------|-------|------|------|--------------------------|
| L/D       | 22    | 10.0 | 55%  | Viscous + fuselage drag  |
| CL at 2°  | ~0.8  | —    | —    | 3D effects               |

## Known Limitations
Cell count limited to 1M by student license
Fully turbulent assumption in boundary layer
No propeller modeled — base drag present
Wing-fuselage junction without fairing

## Lessons Learned
1. Sharp Trailing edge geometry leads to mesh
   failure, must resolve this by reducing edge
   sharpness. 

3. Turbulence intensity at inlet must
   match physical conditions (0.1% outdoor)
   5% inlet intensity forces early transition
   inflates skin friction significantly

4. AoA must match design operating point
   0° AoA gives artificially low L/D for
   cambered MH45 airfoil
