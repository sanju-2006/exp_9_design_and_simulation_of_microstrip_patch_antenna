
# Experiment 9 — Design and Simulation of a Microstrip Patch Antenna Using Ansys HFSS

## Aim
To design and simulate a rectangular microstrip patch antenna at a specified resonant frequency using Ansys HFSS, and to study its return loss, VSWR, bandwidth, gain and radiation pattern.

## Software Used
Ansys HFSS (High Frequency Structure Simulator)

## Theory
A microstrip patch antenna consists of a thin metallic patch on one side of a dielectric substrate, with a ground plane on the other side. It is low profile, lightweight, easy to fabricate and integrate with microwave circuits, making it popular in wireless communication, radar and satellite applications. Its main drawbacks are narrow bandwidth and low gain compared to other antenna types.

### Design Equations
For a rectangular patch operating in the dominant TM₀₁₀ mode, the standard transmission-line model gives:

1. Width of the patch:

   **W = (c / 2f_r) × √(2 / (ε_r + 1))**

2. Effective dielectric constant:

   **ε_reff = (ε_r + 1)/2 + (ε_r − 1)/2 × [1 + 12h/W]^(−1/2)**

3. Length extension (fringing effect):

   **ΔL = 0.412h × [(ε_reff + 0.3)(W/h + 0.264)] / [(ε_reff − 0.258)(W/h + 0.8)]**

4. Actual length of the patch:

   **L = c / (2 f_r √ε_reff) − 2ΔL**

5. Ground plane dimensions (typically extended by 6h on each side):

   **L_g = L + 6h**
   **W_g = W + 6h**

where:
- c = velocity of light
- f_r = resonant (design) frequency
- ε_r = dielectric constant of the substrate
- h = height (thickness) of the substrate

### Feeding Techniques
The patch can be excited using several methods, most commonly:
- **Microstrip line feed** — an edge feed with an inset cut into the patch to match the 50 Ω line impedance.
- **Coaxial (probe) feed** — the inner conductor of a coaxial connector is soldered directly to the patch at a point where the input impedance is 50 Ω.

This experiment uses the inset microstrip line feed for excitation.

## Design Calculations (f_r = 2.4 GHz, FR-4, ε_r = 4.4, h = 1.6 mm)

- W = (3×10⁸ / 2×2.4×10⁹) × √(2/5.4) = 62.5 × 0.6086 = **38.04 mm**
- ε_reff = 2.7 + 1.7 × [1 + 12(1.6)/38.04]^(−1/2) = **4.086**
- ΔL = 0.412 × 1.6 × [(4.386)(24.04)] / [(3.828)(24.58)] = **0.739 mm**
- L = 62.5/√4.086 − 2(0.739) = 30.92 − 1.48 = **29.44 mm**
- L_g = 29.44 + 6(1.6) = **39.04 mm**
- W_g = 38.04 + 6(1.6) = **47.64 mm**

## Design Specifications

| Parameter | Value |
|---|---|
| Resonant frequency, f_r | 2.4 GHz |
| Dielectric constant, ε_r | 4.4 (FR-4), loss tangent 0.02 |
| Substrate height, h | 1.6 mm |
| Patch width, W | 38.04 mm |
| Patch length, L | 29.44 mm |
| Ground plane dimensions, L_g × W_g | 39.04 mm × 47.64 mm |
| Feed type | Microstrip inset feed |
| Feed line width (50 Ω) | 3.06 mm |
| Feed line length | 15 mm |
| Inset depth | 10 mm |
| Inset gap (each side of feed line) | 1 mm |
| Air box (λ/4 = 31.25 mm buffer on all sides) | approx. 101.5 × 110 × 64 mm |
| Solution frequency | 2.4 GHz |
| Frequency sweep | 2.0 GHz to 3.0 GHz, step 0.01 GHz |

## Procedure
1. Launch Ansys HFSS and create a new project. Insert an HFSS Design with solution type **Driven Terminal** or **Driven Modal**.
2. Set the model units to mm.
3. Draw the substrate:
   - Create a rectangular box of dimensions L_g × W_g × h = 39.04 × 47.64 × 1.6 mm and assign FR-4 (ε_r = 4.4).
4. Draw the ground plane:
   - Create a rectangular sheet of L_g × W_g on the bottom face of the substrate and assign it as a **Perfect E (PEC)** boundary.
5. Draw the patch:
   - Create a rectangular sheet of L × W = 29.44 × 38.04 mm on the top face of the substrate and assign it as **Perfect E (PEC)**.
6. Design the feed line:
   - Draw a 50 Ω feed line of width 3.06 mm connecting to the patch (with a 10 mm inset notch and 1 mm gaps), and excite it with a **Lumped Port** at the outer edge.
   - (For a coaxial feed, create a probe from the ground plane to the patch at the 50 Ω point and excite it with a Lumped Port or Wave Port.)
7. Create the air box and radiation boundary:
   - Draw an air box around the entire structure, at least λ/4 away from the patch on all sides (and above it).
   - Assign the outer faces of the air box as a **Radiation Boundary**.
8. Set up the analysis:
   - Add a Solution Setup with the solution frequency equal to f_r (2.4 GHz).
   - Add a Frequency Sweep (Interpolating/Fast) from 2.0 to 3.0 GHz.
9. Add far-field reports:
   - Insert a Far Field Setup (Infinite Sphere) for the 2-D and 3-D radiation patterns.
10. Validate and run the simulation (Validation Check → Analyze All).
11. Post-process the results:
    - Plot S11 (return loss) vs frequency and note the resonant frequency and −10 dB bandwidth.
    - Plot VSWR vs frequency.
    - Plot the 2-D E-plane and H-plane radiation patterns and the 3-D gain pattern.
    - Note the gain, directivity and radiation efficiency at resonance.

## Observations

| Quantity | Observed value |
|---|---|
| Resonant frequency | 2.40 GHz |
| Return loss (S11) | −24 dB |
| VSWR | 1.14 |
| Bandwidth (S11 < −10 dB) | ≈ 80 MHz (about 3.3%) |
| Gain | 3.2 dBi |
| Directivity | 6.5 dBi |
| Radiation efficiency | ≈ 50% (FR-4 is lossy) |

## Graphs
<img width="1200" height="1600" alt="WhatsApp Image 2026-09-19 at 10 38 51 AM (3)" src="https://github.com/user-attachments/assets/a447add3-1c4a-4557-a060-7a0d8ca02438" />
<img width="1200" height="1600" alt="WhatsApp Image 2026-09-19 at 10 38 51 AM (4)" src="https://github.com/user-attachments/assets/7e785f3b-e1ce-409d-bc76-ff9a62f8e3a2" />


## Precautions
- Ensure the air box / radiation boundary is at least λ/4 away from the patch structure on all sides.
- Use a fine mesh near the feed point and patch edges for accurate convergence.
- Verify the substrate material properties (ε_r, loss tangent, thickness) before running the simulation.
- Check the port impedance and de-embedding settings before reading S11/VSWR values.
- Validate the geometry (no overlapping or unassigned boundaries) before analysis.

## Result
- **Resonant Frequency** = 2.4 GHz
- **Return loss** = −24 dB
- **VSWR** = 1.14
- **Gain** = 3.2 dBi

## Conclusion
A rectangular microstrip patch antenna was designed and simulated at 2.4 GHz using Ansys HFSS on an FR-4 substrate (ε_r = 4.4, h = 1.6 mm) with an inset microstrip line feed. The antenna resonated at about 2.4 GHz with a return loss below −10 dB and a VSWR below 2, showing a good match to the 50 Ω port. The −10 dB bandwidth was about 80 MHz, which is narrow, as expected for a patch antenna. The gain of about 3.2 dBi is modest because of the lossy FR-4 substrate, and the radiation pattern was broadside, as expected for the TM₀₁₀ mode.

