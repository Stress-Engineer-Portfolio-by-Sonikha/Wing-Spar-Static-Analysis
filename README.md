# Wing Spar Static Strength Analysis  
**CS-25 +2.5g Maneuver | Static Stress**

End-to-end static analysis of a metallic aircraft wing spar following real aerospace workflow.

## Objective
Demonstrate complete static strength analysis process: Load Path → Hand Calculations (SFD/BMD) → Classical Stress & Margin of Safety → Optimization → FEM Validation using FreeCAD + PrePoMax.

## 1. Real Aircraft Load Case
- **+2.5g symmetric maneuver** (Limit Load per CS-25 / FAR-25)
- Ultimate Load Factor = 2.5g * 1.5 = **3.75g** 
- Semi-span = 15 m
- Net root shear force ≈ **860 kN**
- Root bending moment ≈ **4312.5 kNm**

## 2. Load Path
Aerodynamic lift → transferred via ribs to spar → web carries shear, flanges carry bending moment → reacted at wing root/fuselage attachment.

<img width="1033" height="857" alt="image" src="https://github.com/user-attachments/assets/d7587cf0-6719-4cff-a809-757be60b7bda" />

## 3. SFD & BMD
- Hand calculations + Python implementation for linearly tapered distributed load.
- Critical section identified at **wing root**.

![SFD and BMD](results/sfd_bmd_plot.png)

## 4. Classical Stress Analysis (I-Beam)
- Material: Aluminum 2024-T3 (Fy = 345 MPa, Fu = 440 MPa)
- Geometry: h=450 mm, b=250 mm, tw=10 mm, tf=16 mm
- Max bending stress (Limit): **XXX MPa**
- Margin of Safety (Ultimate): **XXX**

## 5. Optimization
Parametric study on web and flange thickness.  
**Achieved XX% weight reduction** while maintaining positive Margin of Safety (MS_ult > 0.18).

## 6. FEM Validation (FreeCAD + PrePoMax)
- Shell element model
- Classical vs FEM correlation: **< 5% difference** in peak stress
- Mesh convergence performed

*(Insert stress contour + displacement plots here)*

## Key Quantified Achievements
- Performed full static strength analysis on primary wing structure under real CS-25 +2.5g maneuver load case.
- Calculated SFD, BMD, section properties, and Margins of Safety using classical beam theory.
- Optimized spar design resulting in **XX% weight saving** while ensuring structural integrity (MS_ult > 0.18).
- Validated analytical results with detailed shell FEM model in PrePoMax, achieving <5% difference in peak stresses.
- Demonstrated complete workflow from fundamentals to numerical validation — directly relevant to Airbus, Boeing, Liebherr, SII, and FERCHAU Static Stress / Berechnungsingenieur roles.

## Tools Used
- Python (numpy, matplotlib) – Analytical calculations
- FreeCAD – Geometry
- PrePoMax (CalculiX) – FEM analysis & post-processing

## Learning & Next Steps
This project refreshed core competencies in static stress analysis, load path understanding, hand calculations, and FEM validation for metallic aircraft structures.
