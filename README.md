# OmniPulse-X1

> **Open-Source Ultra-Wideband RF Layout Generator**

## Overview

OmniPulse-X1 is an open-source hardware project that generates a production-style GDSII layout for an experimental ultra-wideband RF integrated circuit using Python and the `gdstk` library.

The repository is intended to demonstrate a reproducible, script-generated IC layout workflow where the GDSII database is produced from editable source code rather than maintained as a manually edited binary artifact.

The project includes:

* Python-based layout generation
* GDSII mask generation
* Manufacturing geometry manifest
* Hardware documentation
* Open hardware licensing under CERN-OHL-S-2.0

---

# Features

* Script-generated GDSII layout
* Parametric geometry generation
* RF transmission path using `gdstk.FlexPath`
* Ground–Signal–Ground (GSG) pad array
* Via fence generation
* Ground lattice generation
* Automatic GDSII export
* Analytical example plot demonstrating a transmission-line-based return-loss calculation

---

# Repository Structure

```text
OmniPulse-X1/
│
├── LICENSE
├── README.md
├── HARDWARE.md
├── MANUFACTURING.md
├── SOURCE.md
├── SECURITY.md
├── CODE_OF_CONDUCT.md
├── source.py
├── omnipulse_x1_production (1).gds
│
├── production_manifest.txt
│
├── download (2).png
│
└── docs/
```

---

# Design Workflow

```text
Python Source
      │
      ▼
gdstk Geometry Generation
      │
      ▼
GDSII Layout
      │
      ▼
Manufacturing Manifest
      │
      ▼
Analytical Validation Plot
```

---

# Layer Map

| Layer | Purpose                              |
| ----: | ------------------------------------ |
|     1 | RF transmission geometry             |
|     2 | Via fence structures                 |
|     4 | Signal pads                          |
|     5 | Ground structures and guard geometry |

---

# Requirements

* Python 3.10 or newer
* gdstk
* NumPy
* Matplotlib

Install dependencies:

```bash
pip install gdstk numpy matplotlib
```

---

# Building the Layout

Generate the production GDSII:

```bash
python omnipulse_x1_generator.py
```

Generated outputs include:

* `omnipulse_x1_production.gds`
* `download (2).png`

---

# Design Philosophy

The layout is generated entirely from editable Python source, enabling repeatable and version-controlled hardware development.

Geometry is created programmatically using parameterized construction techniques rather than manual editing of the GDSII database.

---

# Validation

The repository includes an analytical example that computes a transmission-line-based return-loss curve and exports a visualization.

This analytical calculation is intended as an example workflow accompanying the layout generator. It should not be interpreted as a substitute for electromagnetic simulation or laboratory measurement of the generated layout.

---

# License

Unless otherwise noted, the hardware design files in this repository are licensed under the **CERN Open Hardware Licence Version 2 – Strongly Reciprocal (CERN-OHL-S-2.0)**.

See the `LICENSE` file for details.

---

# Contributing

Contributions are welcome.

Please read:

* `CODE_OF_CONDUCT.md`
* `SECURITY.md`

before submitting pull requests or issue reports.

---

# Disclaimer

This repository is provided for research, educational, and hardware development purposes.

Users are responsible for verifying compatibility with their target fabrication process, manufacturing constraints, and application requirements before producing physical hardware.
