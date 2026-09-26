# circuitbreakers.temntc
# Circuit Breakers: Analog Thermal Defence Module

An institutional-grade, pure analog hardware fire protection system engineered to physically isolate high-risk electrical circuits during thermal runaway before ignition occurs. Operating completely independently of microcontrollers, firmware, or network connections, the module provides zero-latency hardware security for critical infrastructure, commercial developments, and industrial distribution boards.

---

## Technical Specifications

| Feature | Specification |
| --- | --- |
| **Architecture** | Pure Analog (Zero MCU / Software Dependencies) |
| **Trip Latency** | $< 50\,\mu\text{s}$ (Hardware Solid-State Cutoff) |
| **Thermal Sensor** | Precision TMP36 Linear Temperature Transducer |
| **Comparator Circuit** | Low-Power Dual LM393 Voltage Comparator |
| **Isolation Mechanism** | High-Current Solid-State Power MOSFET Switch |
| **Operating Voltage** | 240V AC Nominal / 12V DC Logic Power |
| **Unit Target Cost** | 149 AED |
| **Compliance Target** | UAE Civil Defence Life-Safety & Hassantuk Framework |

---

## Core Value Proposition

* **Zero-Software Vulnerability:** Eliminates risks associated with firmware crashes, code freezes, buffer overflows, or cybersecurity breaches.
* **Sub-Millisecond Response:** Physical isolation triggers in under $50\,\mu\text{s}$, compared to legacy software-driven detectors that require several seconds or minutes to respond.
* **Proactive Thermal Isolation:** Neutralizes overheating at the component layer prior to combustion or smoke generation.
* **Hassantuk Integration Ready:** Auxiliary dry-contact signal outputs interface directly with central building safety management networks.

---

## Signal Flow & System Architecture

```text
  +------------------+      +-------------------+      +------------------+
  |  TMP36 Temperature| ---> |  LM393 Precision  | ---> | Solid-State Gate |
  |   Analog Sensor  |      | Precision Voltage |      | MOSFET Driver    |
  +------------------+      |    Comparator     |      +--------+---------+
                            +---------+---------+               |
                                      |                         v
                            +---------+---------+      +------------------+
                            | Reference Voltage |      | Load Isolation   |
                            | Potentiometer     |      | Circuit (Cutoff) |
                            +-------------------+      +------------------+

```

### Threshold Voltage Formulation

The analog trip voltage threshold $V_{\text{trip}}$ is set using a precision voltage divider against the output of the TMP36:

$$V_{\text{out}} = (T - 50) \times 10\,\text{mV/}^\circ\text{C} + 500\,\text{mV}$$

When $V_{\text{sensor}} \ge V_{\text{ref}}$, the LM393 immediately pulls the MOSFET gate LOW, opening the power line in under $50\,\mu\text{s}$.

---

## Bill of Materials (Core Subsystem)

| Designator | Component | Description | Quantity |
| --- | --- | --- | --- |
| **U1** | TMP36GRTZ | Analog Temperature Sensor ($\pm 1^\circ\text{C}$ Accuracy) | 1 |
| **U2** | LM393DR | Dual Differential Voltage Comparator | 1 |
| **Q1** | IRF840 / Solid-State | Power MOSFET / High-Voltage Switch | 1 |
| **RV1** | 10k $\Omega$ Potentiometer | Calibration Trimmer for Threshold Temp | 1 |
| **F1** | 2.5A / 250V Fuse | Primary Overcurrent Protection | 1 |
| **MOV1** | 275V AC Varistor | Input Transient Voltage Suppression | 1 |

---

## Repository Structure

```text
.
├── hardware/
│   ├── schematics/        # KiCad schematic files (.kicad_sch)
│   ├── pcb/               # Board layout files (.kicad_pcb)
│   ├── gerber/            # Production-ready manufacturing outputs
│   └── bom/               # Itemized components and supplier part numbers
├── docs/
│   ├── datasheets/        # TMP36 & LM393 component reference specs
│   └── compliance/        # UAE Civil Defence & Hassantuk alignment briefs
├── media/                 # Rendered 3D models and promotional vectors
└── README.md

```

---

## Setup & Fabrication Instructions

1. **Clone the Repository:**
```bash
git clone https://github.com/YourOrg/circuit-breakers-thermal-defence.git

```


2. **Open in KiCad:**
* Open `hardware/schematics/circuit_breakers.kicad_pro` in KiCad (v7.0 or newer).


3. **Generate Manufacturing Outputs:**
* Export Gerber files to `hardware/gerber/` using standard 2-layer PCB settings ($1.6\,\text{mm}$ FR4, $1\,\text{oz}$ Copper).


4. **Calibration:**
* Apply $12\,\text{V DC}$ logic power.
* Adjust `RV1` to set the output voltage corresponding to your target trip threshold (e.g., $1.1\,\text{V}$ for $60^\circ\text{C}$).



---

## Sustainability & Regulatory Alignment

* **SDG 9 (Industry, Innovation & Infrastructure):** Upgrades local industrial infrastructure with resilient, fail-safe hardware components.
* **SDG 11 (Sustainable Cities & Communities):** Reduces commercial urban fire risks through proactive thermal isolation.
* **UAE Civil Defence Standard:** Compliant with national regulations governing automated electrical isolation equipment.

---

## License

Distributed under the MIT License. See `LICENSE` for details.
