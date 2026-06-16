# Wing Spar Static Strength Analysis  
**CS-25 +2.5g Maneuver | Static Stress**

End-to-end static analysis of a metallic aircraft wing spar following real aerospace workflow.

## Objective
Demonstrate complete static strength analysis process: Load Path → Hand Calculations (SFD/BMD) → Classical Stress & Margin of Safety → Optimization → FEM Validation using FreeCAD + PrePoMax.

## 1. Real Aircraft Load Case
- **+2.5g symmetric maneuver** (Limit Load per CS-25 / FAR-25)
- Ultimate Load Factor = 2.5g * 1.5 = **3.75g** 
- Semi-span = 15 m
- **Assumptions:**
        * Aircraft MTOW = 80,000 kg → Weight per wing ≈ 392 kN (at 1g). [Assumption as per A320](https://www.aircraft.airbus.com/sites/g/files/jlcbta126/files/2025-01/AC_A320_0624.pdf)
  
        * At +2.5g limit: Total lift per wing ≈ 980 kN.
  
        * Wing structural + fuel weight per wing ≈ 120 kN
  
        * Net upward force at 2.5g ≈ 860 kN.
  
        * Lift distribution: Elliptical → w(x) = w_0 * (1 - (x/L) [linearly tapered distributed load]
              - Max net distributed load at root w₀ = 115 kN/m
              - Linearly decreases to 0 at tip.

- Net root shear force ≈ **860 kN**
- Root bending moment ≈ **4312.5 kNm**

## 2. Load Path
Aerodynamic lift → transferred via ribs to spar → web carries shear, flanges carry bending moment → reacted at wing root/fuselage attachment.

<img width="800" height="600" alt="image" src="https://github.com/user-attachments/assets/d7587cf0-6719-4cff-a809-757be60b7bda" />

## 3. SFD & BMD
- Hand calculations + Python implementation for linearly tapered distributed load.
- Critical section identified at **wing root**.

<img width="1536" height="754" alt="1_sfd_bmd_plot" src="https://github.com/user-attachments/assets/e1691ef8-867e-493a-af58-13f8091c8495" />

## 4. Classical Stress Analysis (I-Beam)
- Material: Aluminum 7075-T6 (σy = 480 MPa, σu = 540 MPa)
- Geometry: h=800 mm, b=400 mm, tw=10 mm, tf=22 mm
- Young's Modulus E = 71700 MPa
- Moment of Inertia I = 3024e6 mm4
- Max bending stress (Limit) σmax = (M*y)/I = **570 MPa** (both spars)
- Max bending stress (Limit - one spar) = **285 MPa**
- Margin of Safety (Ultimate): (σy/σmax*1.5) - 1 = (540/285*1.5)-1 = **0.26**

## 5. Optimization
Parametric study on web and flange thickness.  
**Achieved 9.35% weight reduction** while maintaining positive Margin of Safety (**MS_ult ≥ 0.15**).

- Geometry: h=800 mm, b=400 mm, tw=22 mm, tf=19.91 mm
- Moment of Inertia I = 2755e6 mm4
- Max bending stress (Limit): **626.13 MPa** (both spars)
- Max bending stress (Limit - one spar): **313 MPa**
- Displacement (delta_max) = (w0 * L**4) / (30 * E * I) = **982 mm**

## 6. Design & FEM Validation (FreeCAD + PrePoMax)

**CAD Model:**
<img width="1918" height="985" alt="spar_geometry" src="https://github.com/user-attachments/assets/12038024-9f6e-4c54-ab5d-5ff54f50a990" />

**Finite Element Model:**
<img width="1911" height="986" alt="Spar_mesh" src="https://github.com/user-attachments/assets/40e2e51d-4c41-4c9e-8d8f-bd7a6fe3665b" />

<img width="1916" height="987" alt="Spar_triangular_load" src="https://github.com/user-attachments/assets/c2f4eb7c-5d16-4c3b-bc78-0781fa0a21ca" />

- Shell element model
- Classical vs FEM correlation: **< 5% - 8% difference** in peak stress
- Mesh convergence performed

**Displacement**
<img width="1918" height="1018" alt="displacement" src="https://github.com/user-attachments/assets/ca37360a-9092-42f3-bd98-739a5df2c68c" />


**Vonmises Stress**
<img width="1917" height="1017" alt="Vonmises_stress" src="https://github.com/user-attachments/assets/e5c0a48a-8fb4-4698-9513-03113f056e22" />


<img width="1000" height="500" alt="4_FEM_Validation_with_Classical" src="https://github.com/user-attachments/assets/60da3790-e7e5-4822-beab-125824c1b676" />


## Key Quantified Achievements
- Performed complete static strength analysis on primary wing structure under real CS-25 +2.5g maneuver load case.
- Calculated SFD, BMD, section properties, and Margins of Safety using classical beam theory.
- Optimized spar design resulting in **9.35% weight saving** while ensuring structural integrity (MS_ult > 0.15).
- Validated analytical results with detailed shell FEM model in PrePoMax, achieving <5% difference in peak stresses.
- Demonstrated complete workflow from fundamentals (load path & hand calcs) to numerical validation.
  
## Tools Used
- **Python** (numpy, matplotlib) – Analytical calculations & optimization
- **FreeCAD** – Geometry modeling
- **PrePoMax** (CalculiX solver) – FEM analysis & post-processing

## Relevance to Industry
This project strengthens my capabilities in static stress analysis, classical methods vs FEM correlation, and certification-oriented thinking required for **Static Stress Engineer** and **Berechnungsingenieur** positions.
