# OmniPulse-X1 Manufacturing Guide

## Purpose

This document describes the manufacturing workflow for the OmniPulse-X1 project, including generation of the GDSII layout, preparation for fabrication, and recommended verification steps before submission to a semiconductor foundry.

This project distributes the layout as editable Python source together with the generated GDSII database.

---

# Manufacturing Workflow

```text
Python Source
      │
      ▼
Geometry Generation (gdstk)
      │
      ▼
GDSII Layout Database
      │
      ▼
Layout Inspection
      │
      ▼
Design Verification
      │
      ▼
Foundry Submission
```

---

# Repository Inputs

Primary design source:

* `source.py`

Generated outputs:

* `layouts/omnipulse_x1_final_production.gds`
* `validation/production_validation.png`

Supporting files:

* `manifests/production_manifest.txt`

---

# Software Requirements

Recommended environment:

| Software     | Purpose                 |
| ------------ | ----------------------- |
| Python 3.10+ | Layout generation       |
| gdstk        | GDSII geometry creation |
| NumPy        | Analytical calculations |
| Matplotlib   | Plot generation         |

Install dependencies:

```bash
pip install gdstk numpy matplotlib
```

---

# Generating the Layout

Run:

```bash
python source.py.py
```

Successful execution generates:

* GDSII layout
* Analytical validation plot

The script prints completion information when finished.

---

# Layer Assignment

| Layer | Function                 |
| ----: | ------------------------ |
|     1 | RF transmission geometry |
|     2 | Via fence structures     |
|     4 | Signal pads              |
|     5 | Ground structures        |

These assignments are defined directly in the Python source and can be modified as needed for a target fabrication process.

---

# Geometry Generation

The layout is created procedurally.

Current geometry primitives include:

* Rectangles
* Polygons
* FlexPath objects

Because the layout is script-generated, changes should be made in the Python source rather than editing the generated GDSII whenever possible.

---

# GDSII Output

Output file:

```text
layouts/omnipulse_x1_final_production.gds
```

This file represents the generated physical layout database suitable for downstream inspection or integration into a fabrication workflow.

---

# Layout Inspection

Before fabrication, it is recommended to inspect the generated GDSII using a compatible layout viewer such as KLayout or another GDSII-compatible tool.

Recommended inspection items include:

* layer visibility
* geometry placement
* path continuity
* pad locations
* bounding box
* unintended overlaps
* scaling and units

---

# Process Adaptation

The generated layout is process-agnostic.

Before manufacturing, users should adapt the layout to the requirements of the intended fabrication process, including:

* layer mapping
* database units
* minimum feature sizes
* spacing rules
* enclosure rules
* density requirements
* process-specific design rules

---

# Recommended Verification

Prior to fabrication, the following checks are recommended where applicable:

* Design Rule Check (DRC)
* Layout Versus Schematic (LVS)
* Electrical Rule Check (ERC)
* Antenna Rule Check
* Density Verification
* Geometry Inspection
* GDSII Integrity Verification

The current repository does not automatically perform these verification steps.

---

# Analytical Plot

The generator also produces:

```text
validation/production_validation.png
```

This figure is generated from the analytical calculation implemented in the Python script.

It is intended as an example output accompanying the layout generator and should not be interpreted as a substitute for electromagnetic simulation or laboratory measurement of the generated layout.

---

# Manufacturing Dependencies

The repository intentionally avoids embedding proprietary process design kits (PDKs), standard-cell libraries, or foundry-specific technology files.

If a target fabrication process requires proprietary design resources, users are responsible for obtaining them under the applicable license agreements.

---

# Reproducibility

The preferred form for modification is the Python source used to generate the layout.

Reproducing the published GDSII should consist of:

1. Installing the required software.
2. Running the generator script.
3. Comparing the regenerated GDSII with the published version.
4. Reviewing the generated layout before use.

---

# User Responsibilities

Before submitting the design for fabrication, users are responsible for verifying that:

* the generated layout satisfies the rules of the selected fabrication process,
* any required process-specific modifications have been applied,
* verification checks have been completed, and
* the resulting design is appropriate for the intended application.

The maintainers of this repository do not guarantee manufacturability or performance for any particular fabrication process.

---

# Revision History

| Version | Description                         |
| ------- | ----------------------------------- |
| V1      | Initial manufacturing documentation |
