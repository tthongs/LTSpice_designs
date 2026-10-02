# LTspice Circuit Designs

A repository for analog, mixed-signal, and power electronics circuit schematics designed and simulated in **LTspice**. Each project folder contains the schematic (`.asc`), simulation profiles/data (`.raw`, `.plt`, `.log`), and high-resolution waveform/circuit screenshots.

---

## Repository Index

| Design | Category | Description | Primary Components | Simulation Type | Directory |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Level Shifter** | Signal Conditioning / Interface | 10V-to-3.3V active level shifter & attenuator | LTC6240, 100kΩ / 33kΩ network, RC filter | Transient (`.tran 50m`) | [`Level_shifter/`](./Level_shifter/) |

---

## Circuit Showcase

### 1. Level Shifter (10V to 3.3V)

* **Directory**: [`Level_shifter/`](./Level_shifter/)
* **Schematic File**: [`Level_shifter_schematic.asc`](./Level_shifter/Level_shifter_schematic.asc)
* **Simulation Type**: Transient Analysis (`.tran 50m`)

#### Overview
This circuit translates higher-voltage digital or pulsed signals (0–10V) down to microcontroller-compatible logic levels (~0–3.3V). It utilizes an **LTC6240** rail-to-rail CMOS operational amplifier configured in a balanced attenuating divider topology with an output low-pass filter stage to deliver clean edges into a capacitive load.

#### Circuit Schematic & Simulation Waveforms
![Level Shifter Schematic and Waveforms](./Level_shifter/Screenshot%202026-09-28%20222037.png)

#### Key Circuit Details
* **Operational Amplifier**: Analog Devices / Linear Technology **LTC6240** (Rail-to-Rail Output, Low Noise CMOS Op-Amp).
* **Divider / Feedback Network**:
  * $R_1 = 100\,\text{k}\Omega$, $R_2 = 33\,\text{k}\Omega$ (Feedback network)
  * $R_3 = 100\,\text{k}\Omega$, $R_4 = 33\,\text{k}\Omega$ (Input divider network)
  * Attenuation Ratio: $\approx \frac{33\,\text{k}}{100\,\text{k} + 33\,\text{k}} \approx 0.248$ (translating 10V down to ~2.5V–3.3V swing depending on biasing).
* **Output Filter & Load**:
  * $R_{\text{load}} = 100\,\Omega$
  * $C_1 = 2.2\,\text{nF}$ (RC filtering stage)
* **Sources**:
  * **Input Signal ($V_1$)**: `PULSE(0 10 0 10n 10n 0.5m 1m)` (0V to 10V square wave, 1 kHz frequency, 50% duty cycle, 10 ns rise/fall time).
  * **Supplies ($V_2, V_3$)**: $10\,\text{V}$ DC rail sources.

#### Waveform Results
* **Input `V(n006)` (Green)**: 10V peak square wave switching between 0V and 10V.
* **Output `V(output)` (Blue)**: Scaled logic signal shifting clean 0V to ~3.3V levels with controlled rise/fall characteristics across the load.

---

## Directory & File Structure Conventions

Every circuit project follows this standardized folder structure:

```text
LTSpice_designs/
├── <Design_Name>/
│   ├── <Design_Name>_schematic.asc      # LTspice schematic file
│   ├── <Design_Name>_schematic.plt      # Waveform plot configuration
│   ├── <Design_Name>_schematic.log      # SPICE simulation log & operating point details
│   ├── <Design_Name>_schematic.raw      # Simulation binary data (optional / generated)
│   └── Screenshot <timestamp>.png       # Waveform & circuit schematic captures
└── README.md                            # Comprehensive index and project documentation
```

---

## Getting Started & Running Simulations

1. **Install LTspice**: Download and install the latest version from [Analog Devices LTspice](https://www.analog.com/en/resources/design-tools-and-calculators/ltspice-simulator.html).
2. **Open the Circuit**:
   * Open LTspice.
   * Go to **File -> Open** and select the desired `.asc` file (e.g., `Level_shifter/Level_shifter_schematic.asc`).
3. **Run Simulation**:
   * Click the **Run** button (running person icon) or select **Simulate -> Run**.
   * The transient waveform viewer will display the saved signal traces (`.plt` settings will be loaded automatically if present).

---

## Repository Maintenance Guideline

> **Note for Contributions & Commits:**  
> Whenever a new circuit design or updated simulation is added to this repository:
> 1. Add the design folder containing the `.asc` schematic and image capture(s).
> 2. Update this `README.md` with:
>    * An entry in the [Repository Index](#repository-index).
>    * A dedicated section under [Circuit Showcase](#circuit-showcase) with schematic details, component parameters, and waveform image references.
> 3. Stage and commit both the design files and the updated `README.md` with a descriptive commit message.
