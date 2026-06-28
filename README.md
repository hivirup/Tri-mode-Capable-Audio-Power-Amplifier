# Tri-mode Capable Audio Power Amplifier

## Overview

https://github.com/user-attachments/assets/d86d677f-6a97-4e2f-b168-3dc96ac75fd9

This repository documents the design and evaluation of a high-fidelity tri-mode audio power amplifier. The system is engineered to drive dual speaker outputs across three distinct configurations, allowing it to adapt to varying acoustic environments and power requirements without requiring hardware modifications.

The versatility of the system is derived from a flexible signal routing architecture. By utilizing specific input processing and amplification stages, the device can be reconfigured to prioritize either spatial stereo separation or maximum monophonic power delivery through bridge-tied load (BTL) operation.

### Operational Modes
* **Stereo Mode:** The Left and Right input channels are amplified individually, driving two speakers independently to maintain high-fidelity spatial imaging.
* **Mono Mode:** The Left and Right input signals are summed and amplified, delivering an identical monophonic signal to both speakers simultaneously.
* **Bridge Mode:** Both internal power amplifiers are utilized to drive a single speaker in a BTL configuration. This arrangement provides a theoretical four-fold increase in output power compared to standard modes.

---

## Features
* **Tri-mode Routing:** Versatile speaker configurations providing adaptable output for Stereo, Mono, and Bridge modes.
* **Class-AB Topology:** Features a discrete push-pull output stage to ensure high-fidelity performance with minimal distortion.
* **Crossover Distortion Elimination:** Dedicated biasing network consisting of two 1N4007 silicon diodes in series.
* **Thermal Stability:** Enhanced thermal stability achieved through 0.22Ω emitter degeneration resistors, preventing thermal runaway during high-power operation.
* **Low-Noise Analogue Path:** Utilizes industry-standard, precision components to maintain signal integrity.

---

## Technical Overview

### Component Selection
* **NE5532 Operational Amplifier:** Selected as the primary voltage gain stage. The NE5532 is an industry standard for high-fidelity audio due to its exceptionally low noise and 9 V/µs slew rate, which significantly exceeds the calculated 0.879 V/µs requirement for 20 kHz operation.
* **TIP41/TIP42 Complementary Pair:** This NPN/PNP BJT pair provides the current capability required to drive 4Ω loads. These transistors support 6A of continuous current and are housed in TO-220 packages for efficient thermal coupling to aluminum heatsinks.
* **1N4007 Biasing Diodes:** Two diodes are connected in series to provide a stable forward voltage drop. This ensures the output transistors remain biased in the active region, successfully transitioning the amplifier from Class-B to Class-AB performance.

### Schematics
*(Add your schematic images here using Markdown image tags if available, e.g., `![Schematic](Media/schematic.png)`)*

---

## Design Verification
System performance was verified using LTSpice for gain calibration and distortion analysis. Simulations confirmed that the feedback network accurately maintained a theoretical voltage gain of approximately 5.6. 

However, during hardware characterization using an oscilloscope, the practical voltage gain was measured at approximately 4.64. This discrepancy is attributed to real-world component tolerances and base-current limitations of the driver stage when under load.

---

## Performance Specifications

### Output Power (Stereo/Mono)
Calculated based on measured Peak-to-Peak voltage across a 4Ω load ($R_L$) using the formula:

$$P_{out} = \frac{V_{pp}^2}{8 \cdot R_L}$$

| Supply Voltage ($\pm V_{CC}$) | Max Output $V_{pp}$ (V) | Calculated $P_{out}$ (W) |
| :--- | :--- | :--- |
| 10 V | 9.6 | 2.88 |
| 12 V | 11.8 | 4.35 |
| 15 V | 12.8 | 5.12 |
| 18 V | 14.6 | 6.66 |
| 20 V | 15.6 | 7.61 |

### Output Power (Bridge Mode)
Bridge mode utilizes both internal amplifiers to drive a single load, demonstrating the expected four-fold power increase.

| Supply Voltage ($\pm V_{CC}$) | Max Output $V_{pp}$ (V) | Calculated $P_{out}$ (W) |
| :--- | :--- | :--- |
| 10 V | 18.4 | 10.58 |
| 12 V | 23.2 | 16.82 |
| 15 V | 27.0 | 22.78 |
| 18 V | 29.4 | 27.01 |
| 20 V | 30.2 | 28.50 |

### Efficiency & Quiescent Current
The total power drawn ($P_{in}$) is the sum of the constant idle power ($P_{idle}$) and the dynamic power ($P_{dynamic}$). Efficiency ($\eta$) is calculated as follows:

$$P_{idle} = 2 \cdot V_{CC} \cdot I_q$$

$$P_{dynamic} = \frac{2 \cdot V_{CC} \cdot V_{peak}}{\pi \cdot R_L}$$

$$\eta = \left( \frac{P_{out}}{P_{idle} + P_{dynamic}} \right) \times 100\%$$

| Supply Voltage ($\pm V_{CC}$) | Measured $I_q$ (mA) | Efficiency ($\eta$ %) |
| :--- | :--- | :--- |
| 10 V | 16.50 | 36.14% |
| 12 V | 20.11 | 37.01% |
| 15 V | 25.66 | 31.90% |
| 18 V | 31.37 | 30.21% |
| 20 V | 35.24 | 29.00% |

### Technical Metrics
* **Amplifier Bandwidth:** 23.8 kHz
* **Slew Rate:** 1.25 V/µs (Exceeding the 0.879 V/µs requirement)

---

## Testing & Analysis
Hardware verification was conducted using a constant 4Ω load. Oscilloscope analysis compared input and output waveforms to ensure linear tracking across the audible spectrum.

Fast Fourier Transform (FFT) analysis confirmed that harmonic distortion is non-observable at fundamental audio frequencies, validating the efficacy of the Class-AB biasing and the overall integrity of the analogue signal path.

---

## Team - Group 19

| Member Name | Index Number |
| :--- | :--- |
| H.H. Palihena | 230458P |
| S.M.R.P. Samarasekara | 230564L |
| S.M.R.R. Samarasinghe | 230566U |
| M.N.N. Shehan | 230613M |

---

## Repository Contents
```text
├── /Simulations     # LTSpice design files
├── /Report          # Technical documentation and data sheets
├── /Media           # Schematic images and waveforms
└── README.md        # Project description
