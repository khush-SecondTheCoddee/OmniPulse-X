# OmniPulse-X1 Hardware Documentation

## Overview

OmniPulse-X1 is an open-source hardware project that generates an experimental integrated-circuit layout using Python and the `gdstk` geometry library. The repository demonstrates a reproducible workflow for creating a GDSII layout from editable source code.

The generated layout includes:

* RF transmission geometry
* Ground structures
* Via fences
* Ground–Signal–Ground (GSG) pad structures

The design is intended as a reference implementation for script-based physical layout generation.

---

# Hardware Architecture

The layout consists of four primary functional regions:

```text
┌────────────────────────────────────────────┐
│           Ground Lattice (Layer 5)         │
├────────────────────────────────────────────┤
│                                            │
│          RF Transmission Geometry          │
│               (Layer 1)                    │
│                                            │
│    Via Fence          Via Fence            │
│     (Layer 2)          (Layer 2)           │
│                                            │
├────────────────────────────────────────────┤
│       Ground–Signal–Ground Pad Array       │
│           Layers 4 and 5                   │
└────────────────────────────────────────────┘
```

---

# Functional Blocks

## 1. RF Transmission Geometry

**Layer:** 1

The RF path is generated using `gdstk.FlexPath`.

Characteristics:

* Parameterized centerline
* Variable path width
* Continuous geometry generation
* GDSII-native implementation

The current implementation generates a tapered transmission path whose width changes along predefined control points.

---

## 2. Ground Structures

**Layer:** 5

Ground regions are produced as a regular lattice of square polygons.

Purpose:

* Demonstrate scripted geometry generation
* Provide repeatable reference structures
* Illustrate layer assignment within the layout

---

## 3. Via Fence

**Layer:** 2

Two parallel via rows are generated programmatically.

Purpose:

* Demonstrate repetitive feature generation
* Represent via fence placement in the layout

The current implementation places vias at fixed spacing along the Y-axis.

---

## 4. Ground–Signal–Ground Pad Array

**Layers:**

* Layer 4 — Signal pads
* Layer 5 — Ground pads

The script generates multiple GSG groups using parameterized spacing.

Each group contains:

```text
Ground
Signal
Ground
```

This arrangement is commonly used for high-frequency probing and interconnection.

---

# Layer Stack

| Layer | Description                       |
| ----: | --------------------------------- |
|     1 | RF transmission geometry          |
|     2 | Via fence structures              |
|     4 | Signal pads                       |
|     5 | Ground lattice and guard geometry |

---

# Coordinate System

The layout uses a Cartesian coordinate system.

* Positive X extends to the right.
* Positive Y extends upward.
* Coordinates are defined directly within the Python source.

The origin is determined by the geometry specified in the generator script.

---

# Units

The Python generator specifies coordinates numerically for GDSII generation through `gdstk`.

Users should configure and verify database units and fabrication units as appropriate for their intended manufacturing workflow.

---

# Geometry Generation

Geometry is created procedurally using Python rather than edited directly in a layout editor.

Primary geometry primitives include:

* rectangles
* polygons
* FlexPath objects

This enables reproducible layout generation from version-controlled source.

---

# Output Files

The generator produces:

* `omnipulse_x1_final_production.gds`
* `production_validation.png`

Additional documentation or manifests may also be generated depending on the project configuration.

---

# Verification

The repository includes an analytical example demonstrating a transmission-line-based return-loss calculation.

This analytical calculation is separate from the physical layout generation process.

Verification of a fabricated implementation—including electromagnetic simulation, circuit simulation, design-rule checking (DRC), layout-versus-schematic (LVS), or laboratory measurement—is outside the scope of the current generator and should be performed independently when required.

---

# Design Assumptions

The current implementation assumes:

* script-generated geometry
* parameterized layout construction
* editable Python source as the preferred form for modification
* GDSII output for downstream fabrication workflows

No assumptions regarding a specific semiconductor process, process design kit (PDK), or fabrication facility are encoded in the generator unless explicitly added by the user.

---

# Intended Use

OmniPulse-X1 is intended for:

* open hardware research
* layout automation experiments
* reproducible IC layout generation
* educational demonstrations of Python-based GDSII creation
* further extension by contributors

Users should evaluate the generated layout against the requirements of their target fabrication process before manufacturing.
