# WASDPad+ Documentation

**Document Version:** 0.9
**Current Hardware Revision:** Rev 1.5
**Status:** Engineering Validation
**Last Updated:** 2026-08-18

This directory contains the technical, manufacturing and assembly documentation for the **WASDPad+** project.

For the general project overview and current development status, see the repository root:

```text
README.md
```

---

# Documentation Index

## Architecture

```text
docs/architecture/
└── System_architecture.md
```

### `System_architecture.md`

System-level description of the WASDPad+ hardware architecture, including:

* controller signal flow
* power architecture
* FIRE logic
* autofire architecture
* hardware functional blocks

---

## Specifications

```text
docs/specification/
├── PROJECT_SPECIFICATION.md
└── FEATURE_SPECIFICATION.md
```

### `PROJECT_SPECIFICATION.md`

Defines the overall technical requirements and design objectives of the WASDPad+ platform.

### `FEATURE_SPECIFICATION.md`

Defines individual controller features and their expected behaviour.

---

## Assembly

```text
docs/assembly/
└── CABLE_ASSEMBLY.md
```

### `CABLE_ASSEMBLY.md`

Defines the Rev 1.5 DB9 cable assembly and verification procedure.

Includes:

* DB9 pin assignment
* cable wire-colour mapping
* J1 pad mapping
* unused pin-5 handling
* mandatory new-batch continuity testing
* +5 V / GND verification
* final cable assembly inspection

> **Important:** Cable wire colours are not considered a controlled electrical specification. The first cable from every new supplier batch must be verified by continuity measurement.

---

# Hardware Documentation

Revision-specific hardware documentation is maintained outside the `docs/` directory under:

```text
hardware/
└── rev1.5/
    ├── README.md
    ├── bom/
    ├── schematic/
    └── pcb/
```

## Rev 1.5 Hardware Overview

```text
hardware/rev1.5/README.md
```

Contains the current Rev 1.5:

* hardware architecture
* component decisions
* protection architecture
* autofire configuration
* switch architecture
* engineering validation status
* production-release criteria

---

# BOM Documentation

```text
├── bom/
│   ├── README.md
│   ├── wasdpad+v1.5.csv
│   ├── ALTERNATE_PARTS.md
│   └── PROCUREMENT_NOTES.md
```

### `README.md`

Engineering description of the Rev 1.5 BOM and primary component selections.

### `BOM.csv`

Authoritative Rev 1.5 component list.

Contains:

* reference designators
* quantities
* values
* footprints
* manufacturer information
* part numbers
* datasheets
* assembly items

### `ALTERNATE_PARTS.md`

Defines approved, conditional and candidate replacement-component strategies.

### `PROCUREMENT_NOTES.md`

Compact sourcing guidance covering:

* preferred suppliers
* protection components
* core ICs
* passive components
* LEDs
* switches
* hot-swap sockets
* controller cable sourcing
* supplier-batch validation

---

# Current Documentation Structure

```text
WASDPad/
│
├── README.md
│
├── LICENSE
│
├── docs/
│   ├── README.md
│   │
│   ├── architecture/
│   │   └── System_architecture.md
│   │
│   ├── specification/
│   │   ├── PROJECT_SPECIFICATION.md
│   │   └── FEATURE_SPECIFICATION.md
│   │
│   └── assembly/
│       └── CABLE_ASSEMBLY.md
│
└── hardware/
    └── rev1.5/
        ├── README.md
        │
        ├── bom/
        │   ├── README.md
        │   ├── BOM.csv
        │   ├── ALTERNATE_PARTS.md
        │   └── PROCUREMENT_NOTES.md
        │
        ├── schematic/
        │
        └── pcb/
```

The structure may expand as production, testing and enclosure documentation is added.

---

# Recommended Reading Order

For a new developer:

```text
1. /README.md
2. docs/specification/PROJECT_SPECIFICATION.md
3. docs/specification/FEATURE_SPECIFICATION.md
4. docs/architecture/System_architecture.md
5. hardware/rev1.5/README.md
6. hardware/rev1.5/bom/README.md
```

For PCB / electronics work:

```text
1. hardware/rev1.5/README.md
2. hardware/rev1.5/bom/BOM.csv
3. hardware/rev1.5/bom/ALTERNATE_PARTS.md
4. hardware/rev1.5/bom/PROCUREMENT_NOTES.md
5. schematic and PCB source files
```

For assembly / manufacturing:

```text
1. hardware/rev1.5/bom/BOM.csv
2. hardware/rev1.5/bom/PROCUREMENT_NOTES.md
3. docs/assembly/CABLE_ASSEMBLY.md
4. hardware/rev1.5/README.md
```

---

# Documentation Status

| Area                      | Status             |
| ------------------------- | ------------------ |
| Project overview          | Current            |
| Rev 1.5 hardware overview | Current            |
| Rev 1.5 BOM documentation | Current            |
| Alternate-parts strategy  | Current            |
| Procurement guidance      | Current            |
| Cable assembly procedure  | Current            |
| System architecture       | Review recommended |
| Project specification     | Review recommended |
| Feature specification     | Review recommended |
| Production test procedure | Planned            |
| PCB assembly procedure    | Planned            |
| Enclosure documentation   | Planned            |

---

# Planned Documentation

As Rev 1.5 moves toward production validation, the following documents should be added:

```text
docs/
├── assembly/
│   ├── CABLE_ASSEMBLY.md
│   └── PCB_ASSEMBLY.md          # planned
│
├── testing/
│   └── PRODUCTION_TEST.md       # planned
│
└── mechanical/
    └── ENCLOSURE.md             # planned
```

The highest-priority future document is the **production test procedure**, which should define electrical checks required before connecting an assembled controller to a host computer.

---

# Documentation Versioning

Documentation revisions are independent from hardware revisions.

Example:

```text
Hardware Revision: Rev 1.5
Documentation:     v0.9
```

Documentation-only changes do not require a hardware revision increment.

---

# Version History

| Version | Date           | Status                     | Changes                                                                                                                                                                            |
| ------- | -------------- | -------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 0.1     | Not recorded   | Initial                    | Initial documentation placeholder                                                                                                                                                  |
| **0.9** | **2026-08-18** | **Engineering Validation** | Converted to documentation index; updated Rev 1.5 structure; added assembly documentation, BOM documentation index, recommended reading paths and planned production documentation |
| **0.9.1** | **2026-08-18** | **Engineering Validation** | Documentation consistency update; corrected the authoritative Rev 1.5 BOM filename and aligned repository references with the current directory structure |
---

# Next Version

**Version 1.0**

Target milestone:

**WASDPad+ Rev 1.5 prototype successfully assembled, tested and production documentation completed.**
