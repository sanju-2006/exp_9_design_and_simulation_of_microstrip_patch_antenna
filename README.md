# exp_9_design_and_simulation_of_microstrip_patch_antenna
Design and Simulation of a Microstrip Patch Antenna using using Ansys HFSS

# Experiment 9 — Design and Simulation of a Microstrip Patch Antenna Using Ansys HFSS

---

## Aim

To design and simulate a rectangular microstrip patch antenna at a specified resonant frequency using Ansys HFSS, and to study its return loss, VSWR, bandwidth, gain and radiation pattern.

## Software Used

Ansys HFSS (High Frequency Structure Simulator)

---

## Theory

A **microstrip patch antenna** consists of a thin metallic patch on one side of a dielectric substrate, with a ground plane on the other side. It is low profile, lightweight, easy to fabricate and integrate with microwave circuits, making it popular in wireless communication, radar and satellite applications. Its main drawbacks are narrow bandwidth and low gain compared to other antenna types.

### Design Equations

For a rectangular patch operating in the dominant TM₀₁₀ mode, the standard transmission-line model gives:

**1. Width of the patch:**

```
W = (c / 2f_r) × √(2 / (ε_r + 1))
```

**2. Effective dielectric constant:**

```
ε_reff = (ε_r + 1)/2 + (ε_r − 1)/2 × [1 + 12h/W]^(−1/2)
```

**3. Length extension (fringing effect):**

```
ΔL = 0.412h × [(ε_reff + 0.3)(W/h + 0.264)] / [(ε_reff − 0.258)(W/h + 0.8)]
```

**4. Actual length of the patch:**

```
L = c / (2 f_r √ε_reff) − 2ΔL
```

**5. Ground plane dimensions** (typically extended by 6h on each side):

```
L_g = L + 6h
W_g = W + 6h
```

where:

* c = velocity of light
* f_r = resonant (design) frequency
* ε_r = dielectric constant of the substrate
* h = height (thickness) of the substrate

### Feeding Techniques

The patch can be excited using several methods, most commonly:

* **Microstrip line feed** — an edge feed with an inset cut into the patch to match the 50 Ω line impedance.
* **Coaxial (probe) feed** — the inner conductor of a coaxial connector is soldered directly to the patch at a point where the input impedance is 50 Ω.

This experiment uses the **inset microstrip line feed** (or coaxial probe feed, as specified) for excitation.

---

## Design Specifications

| Parameter | Value |
|---|---|
| Resonant frequency, f_r | ______ GHz |
| Dielectric constant, ε_r | ______ (e.g., 4.4 for FR-4, 2.2 for RT/Duroid) |
| Substrate height, h | ______ mm |
| Patch width, W | ______ mm |
| Patch length, L | ______ mm |
| Ground plane dimensions, L_g × W_g | ______ mm |
| Feed type | Microstrip inset feed / Coaxial probe feed |
| Feed line width (50 Ω) | ______ mm |
| Feed point / inset depth | ______ mm |

---

## Procedure

1. **Launch Ansys HFSS** and create a new project. Insert an **HFSS Design** with solution type **Driven Terminal** or **Driven Modal**.
2. **Set the model units** to mm.
3. **Draw the substrate:**
   - Create a rectangular box of dimensions L_g × W_g × h and assign the dielectric material (e.g., FR-4, Rogers RT/Duroid) with the required ε_r.
4. **Draw the ground plane:**
   - Create a rectangular sheet of L_g × W_g on the bottom face of the substrate and assign it as a **Perfect E (PEC)** boundary.
5. **Draw the patch:**
   - Create a rectangular sheet of L × W on the top face of the substrate and assign it as **Perfect E (PEC)**.
6. **Design the feed line:**
   - For a microstrip feed, draw a 50 Ω feed line of the calculated width connecting to the patch (with an inset notch if using inset feed), and excite it with a **Lumped Port** at the outer edge.
   - For a coaxial feed, create a via/probe from the ground plane to the patch at the 50 Ω impedance point and excite it with a **Lumped Port** or **Wave Port** at the coaxial cross-section.
7. **Create the air box and radiation boundary:**
   - Draw an air box around the entire structure, at least λ/4 away from the patch on all sides (and above it).
   - Assign the outer faces of the air box as a **Radiation Boundary**.
8. **Set up the analysis:**
   - Add a **Solution Setup** with the solution frequency equal to f_r.
   - Add a **Frequency Sweep** (Interpolating/Fast) covering the band of interest.
9. **Add far-field reports:**
   - Insert a **Far Field Setup** (Infinite Sphere) for the 2-D and 3-D radiation patterns.
10. **Validate and run the simulation** (Validation Check → Analyze All).
11. **Post-process the results:**
    - Plot **S11 (return loss)** vs frequency and note the resonant frequency and −10 dB bandwidth.
    - Plot **VSWR** vs frequency.
    - Plot the **2-D E-plane and H-plane** radiation patterns and the **3-D gain pattern**.
    - Note the **gain**, **directivity** and **radiation efficiency** at resonance.

---

## Observations

<img width="522" height="597" alt="image" src="https://github.com/user-attachments/assets/cb151c86-0c86-4f82-ae99-66b79863536e" />



### Graphs


<img width="537" height="480" alt="image" src="https://github.com/user-attachments/assets/7ce94bc2-b0c4-4b00-996b-08cba349206e" />



---

## Precautions

1. Ensure the air box / radiation boundary is at least λ/4 away from the patch structure on all sides.
2. Use a fine mesh near the feed point and patch edges for accurate convergence.
3. Verify the substrate material properties (ε_r, loss tangent, thickness) before running the simulation.
4. Check the port impedance and de-embedding settings before reading S11/VSWR values.
5. Validate the geometry (no overlapping or unassigned boundaries) before analysis.

## Result

Resonant Frequency = 2.4GHz

Return loss = -20dB

VSWR = 1.22

Gain = 2.15DBI

## Conclusion

A rectangular microstrip patch antenna was designed and simulated at ______ GHz using Ansys HFSS.

