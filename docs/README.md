# WASDPad+ Documentation

**Document Version:** 1.0
**Current Hardware Revision:** Rev1.5.1
**Hardware Status:** Production Release Candidate
**Last Updated:** 2026-08-29

This directory contains the technical documentation for the **WASDPad / WASDPad+** controller project.

The current hardware generation is:

**WASDPad+ Rev1.5.1 — Production Release Candidate**

Rev1.5.1 has completed its principal engineering, PCB and manufacturing-data preparation stages and is currently awaiting physical production-candidate manufacture and validation.

For the general project overview, see the repository root:

[`README.md`](../README.md)

---

# Documentation Index

## Architecture

```text
docs/architecture/
└── System_architecture.md
```

### [`System_architecture.md`](architecture/System_architecture.md)

Defines the Rev1.5.1 system-level hardware architecture.

Topics include:

* controller signal architecture
* direction and FIRE signal paths
* hardware autofire architecture
* power distribution
* overcurrent protection
* ESD / TVS protection
* hot-swap switch architecture
* status indication
* key backlighting
* PCB architecture
* assembly architecture
* latency philosophy
* platform compatibility
* Rev1.5.1 architectural boundaries

Use this document when the question is:

> **How does WASDPad+ Rev1.5.1 work?**

---

# Feature Specification

```text
docs/specification/
└── FEATURE_SPECIFICATION.md
```

### [`FEATURE_SPECIFICATION.md`](specification/FEATURE_SPECIFICATION.md)

Defines the functional features and expected user-visible behaviour of Rev1.5.1.

Topics include:

* directional controls
* FIRE1
* FIRE2
* ambidextrous FIRE controls
* MX-compatible hot-swap switches
* hardware autofire
* SLOW / FAST modes
* autofire status indication
* power indication
* key backlighting
* backlight control
* electrical protection
* DE-9 interface
* platform compatibility
* serviceability
* validation requirements
* Rev1.5.1 feature boundaries

Use this document when the question is:

> **What does WASDPad+ Rev1.5.1 do?**

---

# Assembly Documentation

```text
docs/assembly/
└── CABLE_ASSEMBLY.md
```

### [`CABLE_ASSEMBLY.md`](assembly/CABLE_ASSEMBLY.md)

Defines the controller cable assembly and verification procedure.

Topics include:

* DE-9 pin assignment
* J1 PCB pad mapping
* cable continuity verification
* unused pin handling
* +5 V verification
* GND verification
* cable-batch validation
* final cable inspection

> **Important:** Cable wire colours are not considered a controlled electrical specification.

The first cable from every new supplier or production batch must be verified by continuity measurement.

---

# Development Roadmap

```text
docs/roadmap/
└── ROADMAP.md
```

### [`ROADMAP.md`](roadmap/ROADMAP.md)

Defines the current development and release path.

The current sequence is:

```text
Rev1.5.1 Design Freeze
        │
        ▼
Production-Candidate Manufacturing
        │
        ▼
Assembly
        │
        ▼
Electrical Bring-Up
        │
        ▼
Functional Validation
        │
        ▼
Real-System Validation
        │
        ▼
Production Approval
        │
        ▼
Stable Rev1.5.1 Release
```

The roadmap also separates the stable Rev1.5.1 discrete-hardware platform from possible future programmable Rev2.0 development.

---

# Hardware Documentation

Revision-specific engineering and manufacturing documentation is maintained under:

```text
hardware/
└── rev1.5/
```

Hardware documentation is intentionally separated from the general `docs/` directory.

---

## Hardware Overview

### [`hardware/rev1.5/README.md`](../hardware/rev1.5/README.md)

This is the primary Rev1.5.1 hardware engineering overview.

It describes:

* hardware architecture
* major Rev1.5.1 improvements
* component architecture
* autofire implementation
* protection system
* hot-swap implementation
* key backlighting
* PCB design
* assembly architecture
* manufacturing documentation
* validation status
* production-release criteria

Use this document as the main entry point for Rev1.5.1 hardware engineering.

---

# Engineering Review Record

### [`hardware/rev1.5/Review_Record.MD`](../hardware/rev1.5/Review_Record.MD)

Contains the formal engineering and manufacturing release review for Rev1.5.1.

The review covers:

* power architecture
* overcurrent protection
* ESD protection
* direction controls
* FIRE1 / FIRE2
* autofire
* status indication
* key backlighting
* PCB routing
* ERC
* DRC
* critical component pinouts
* footprint validation
* component orientation
* Gerber output
* Master BOM
* Master CPL
* datasheet traceability
* alternate-part control
* procurement control
* remaining physical validation gate

Current result:

```text
Engineering Review: PASS
Release Status: Production Release Candidate
```

Physical Rev1.5.1 validation remains required before Production Approval.

---

# Manufacturing Documentation

The authoritative Rev1.5.1 manufacturing documentation is located under:

```text
hardware/rev1.5/bom/
```

Current structure:

```text
hardware/rev1.5/bom/
├── README.md
├── WASDPad_Rev1.5.1_FULL_MASTER_BOM.csv
├── WASDPad_Rev1.5.1_FULL_MASTER_CPL.csv
├── DATASHEET_INDEX.md
├── ALTERNATE_PARTS.md
└── PROCUREMENT_NOTES.md
```

---

## Master BOM

### [`WASDPad_Rev1.5.1_FULL_MASTER_BOM.csv`](../hardware/rev1.5/bom/WASDPad_Rev1.5.1_FULL_MASTER_BOM.csv)

The Master BOM is the authoritative source for production component identity.

It contains:

* reference designators
* quantities
* component values
* footprints
* manufacturer names
* manufacturer part numbers
* supplier identifiers where applicable
* assembly classification
* PCB side information
* mechanical and cable items

When another document conflicts with the Master BOM regarding component identity, the **Master BOM takes precedence**.

---

# Master CPL

### [`WASDPad_Rev1.5.1_FULL_MASTER_CPL.csv`](../hardware/rev1.5/bom/WASDPad_Rev1.5.1_FULL_MASTER_CPL.csv)

The Master CPL is the authoritative component-placement dataset.

It defines:

* designator
* X position
* Y position
* PCB side
* component rotation

Assembly-house-specific placement files may be derived from the Master CPL.

Such manufacturing subsets do not replace the Master CPL as the project placement reference.

---

# BOM Documentation

### [`hardware/rev1.5/bom/README.md`](../hardware/rev1.5/bom/README.md)

Describes the Rev1.5.1 production BOM structure and component-selection policy.

It also defines the relationship between:

* Master BOM
* Master CPL
* datasheet documentation
* alternate components
* procurement documentation
* manufacturing-house subsets

---

# Datasheet Index

### [`DATASHEET_INDEX.md`](../hardware/rev1.5/bom/DATASHEET_INDEX.md)

Provides centralized technical references for production components.

The index is intended to support:

* component verification
* pinout verification
* package verification
* electrical review
* sourcing review
* lifecycle maintenance

Manufacturer documentation is preferred where available.

---

# Alternate Parts

### [`ALTERNATE_PARTS.md`](../hardware/rev1.5/bom/ALTERNATE_PARTS.md)

Defines controlled component substitution.

Component status categories include:

```text
Production Primary
Approved Alternate
Legacy Validated
Candidate
Not Approved
Not Evaluated
```

A mechanically or electrically similar component must not automatically be considered a drop-in replacement.

Protection devices, ICs, semiconductors and mechanically critical components require explicit review before substitution.

---

# Procurement Documentation

### [`PROCUREMENT_NOTES.md`](../hardware/rev1.5/bom/PROCUREMENT_NOTES.md)

Defines Rev1.5.1 sourcing and procurement policy.

Topics include:

* preferred suppliers
* manufacturer part-number control
* JLCPCB / LCSC sourcing
* assembly-house substitutions
* semiconductor sourcing
* passive-component sourcing
* switch sourcing
* hot-swap sockets
* controller cables
* incoming verification
* production-lot traceability
* compliance documentation
* lifecycle management
* procurement change control

---

# Documentation Structure

The primary current documentation structure is:

```text
WASDPad/
│
├── README.md
│
├── LICENSE
│
├── enclosure/
│
├── docs/
│   │
│   ├── README.md
│   │
│   ├── architecture/
│   │   └── System_architecture.md
│   │
│   ├── assembly/
│   │   └── CABLE_ASSEMBLY.md
│   │
│   ├── roadmap/
│   │   └── ROADMAP.md
│   │
│   └── specification/
│       └── FEATURE_SPECIFICATION.md
│
└── hardware/
    ├── README.md
    │
    └── rev1.5/
        ├── README.md
        ├── Review_Record.MD
        │
        ├── datasheets/
        │
        └── bom/
            ├── README.md
            ├── WASDPad_Rev1.5.1_FULL_MASTER_BOM.csv
            ├── WASDPad_Rev1.5.1_FULL_MASTER_CPL.csv
            ├── DATASHEET_INDEX.md
            ├── ALTERNATE_PARTS.md
            └── PROCUREMENT_NOTES.md
```

Additional production, testing or mechanical documentation may be added as Rev1.5.1 progresses through physical validation.

---

# Documentation Authority

Different documents have different authoritative roles.

| Information                   | Authoritative Document                        |
| ----------------------------- | --------------------------------------------- |
| General project overview      | `/README.md`                                  |
| Feature behaviour             | `docs/specification/FEATURE_SPECIFICATION.md` |
| System architecture           | `docs/architecture/System_architecture.md`    |
| Development / release status  | `docs/roadmap/ROADMAP.md`                     |
| Hardware engineering overview | `hardware/rev1.5/README.md`                   |
| Engineering release review    | `hardware/rev1.5/Review_Record.MD`            |
| Production component identity | `WASDPad_Rev1.5.1_FULL_MASTER_BOM.csv`        |
| Component placement           | `WASDPad_Rev1.5.1_FULL_MASTER_CPL.csv`        |
| Datasheet references          | `DATASHEET_INDEX.md`                          |
| Component substitutions       | `ALTERNATE_PARTS.md`                          |
| Procurement policy            | `PROCUREMENT_NOTES.md`                        |
| Cable assembly                | `docs/assembly/CABLE_ASSEMBLY.md`             |

This hierarchy prevents duplicated documentation from becoming competing sources of truth.

---

# Recommended Reading Order

## New Developer / Contributor

```text
1. /README.md
2. docs/README.md
3. docs/specification/FEATURE_SPECIFICATION.md
4. docs/architecture/System_architecture.md
5. hardware/rev1.5/README.md
6. docs/roadmap/ROADMAP.md
```

This path explains the project from feature behaviour through implementation and current release state.

---

## Electronics / PCB Engineering

```text
1. hardware/rev1.5/README.md
2. docs/architecture/System_architecture.md
3. hardware/rev1.5/Review_Record.MD
4. hardware/rev1.5/bom/WASDPad_Rev1.5.1_FULL_MASTER_BOM.csv
5. hardware/rev1.5/bom/WASDPad_Rev1.5.1_FULL_MASTER_CPL.csv
6. hardware/rev1.5/bom/DATASHEET_INDEX.md
7. hardware/rev1.5/bom/ALTERNATE_PARTS.md
```

---

## Procurement

```text
1. hardware/rev1.5/bom/WASDPad_Rev1.5.1_FULL_MASTER_BOM.csv
2. hardware/rev1.5/bom/PROCUREMENT_NOTES.md
3. hardware/rev1.5/bom/ALTERNATE_PARTS.md
4. hardware/rev1.5/bom/DATASHEET_INDEX.md
```

---

## Manufacturing / Assembly

```text
1. hardware/rev1.5/bom/WASDPad_Rev1.5.1_FULL_MASTER_BOM.csv
2. hardware/rev1.5/bom/WASDPad_Rev1.5.1_FULL_MASTER_CPL.csv
3. hardware/rev1.5/README.md
4. hardware/rev1.5/Review_Record.MD
5. hardware/rev1.5/bom/PROCUREMENT_NOTES.md
6. docs/assembly/CABLE_ASSEMBLY.md
```

---

## Software / Game Developer

For developers targeting WASDPad+ features from retro-computer software:

```text
1. docs/specification/FEATURE_SPECIFICATION.md
2. docs/architecture/System_architecture.md
```

The most relevant interface-level features are:

* UP
* DOWN
* LEFT
* RIGHT
* FIRE1
* FIRE2
* hardware-generated FIRE1 autofire

The controller does not require a software API, driver or protocol.

---

# Current Documentation Status

| Area                                  | Status  |
| ------------------------------------- | ------- |
| Project overview                      | Current |
| Documentation index                   | Current |
| Rev1.5.1 hardware overview            | Current |
| Feature specification                 | Current |
| System architecture                   | Current |
| Development roadmap                   | Current |
| Engineering review record             | Current |
| Master BOM                            | Current |
| Master CPL                            | Current |
| BOM documentation                     | Current |
| Datasheet index                       | Current |
| Alternate-parts policy                | Current |
| Procurement documentation             | Current |
| Cable assembly procedure              | Current |
| Physical production validation record | Pending |
| Production test procedure             | Planned |
| Final enclosure validation            | Pending |

The core Rev1.5.1 engineering and manufacturing documentation set is therefore considered complete for **Production Release Candidate** status.

---

# Current Hardware Status

WASDPad+ Rev1.5.1 has completed:

```text
Architecture                    ✓
Feature definition              ✓
Schematic                       ✓
Component selection             ✓
PCB layout                      ✓
ERC                             ✓
DRC                             ✓
Protection review               ✓
Critical pinout review          ✓
Assembly orientation review     ✓
Gerber generation               ✓
Master BOM                      ✓
Master CPL                      ✓
Datasheet traceability          ✓
Alternate-part policy           ✓
Procurement documentation       ✓
Engineering release review      ✓
Documentation consolidation     ✓
```

Remaining release path:

```text
Production-Candidate Manufacture
                │
                ▼
             Assembly
                │
                ▼
        Electrical Bring-Up
                │
                ▼
       Functional Validation
                │
                ▼
      Real-System Validation
                │
                ▼
        Enclosure Validation
                │
                ▼
       Production Approval
```

Current classification:

**Production Release Candidate**

---

# Documentation Versioning

Documentation versions are independent from hardware revisions.

For example:

```text
Hardware Revision:    Rev1.5.1
Document Version:     1.0
Hardware Status:      Production Release Candidate
```

Documentation-only changes do not require a hardware revision increment.

Hardware changes that affect electrical, mechanical or functional behaviour must be evaluated separately under the hardware revision policy.

---

# Future Documentation

The highest-priority documentation after manufacture of the production-candidate hardware is the **production test procedure**.

It should define repeatable acceptance tests for manufactured controllers, including:

* pre-power inspection
* +5 V / GND checks
* current consumption
* direction inputs
* FIRE1
* FIRE2
* autofire OFF
* autofire SLOW
* autofire FAST
* status LED behaviour
* key backlighting
* backlight control
* DB9 cable verification
* hot-swap operation
* representative host-system test
* final pass / fail criteria

This document should be based on results from the first physical Rev1.5.1 production-candidate validation.

---

# Rev1.5.1 Documentation Freeze

The principal Rev1.5.1 engineering documentation is now aligned with the Production Release Candidate hardware.

The following documents form the core frozen documentation set:

```text
README.md

docs/
├── README.md
├── architecture/System_architecture.md
├── specification/FEATURE_SPECIFICATION.md
├── roadmap/ROADMAP.md
└── assembly/CABLE_ASSEMBLY.md

hardware/
├── README.md
└── rev1.5/
    ├── README.md
    ├── Review_Record.MD
    └── bom/
        ├── README.md
        ├── WASDPad_Rev1.5.1_FULL_MASTER_BOM.csv
        ├── WASDPad_Rev1.5.1_FULL_MASTER_CPL.csv
        ├── DATASHEET_INDEX.md
        ├── ALTERNATE_PARTS.md
        └── PROCUREMENT_NOTES.md
```

Future corrections should preserve consistency across this documentation set.

---

# Version History

| Version | Date           | Status                           | Changes                                                                                                                                                                                                                                                                         |
| ------- | -------------- | -------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 0.1     | Not recorded   | Initial                          | Initial documentation placeholder                                                                                                                                                                                                                                               |
| 0.9     | 2026-08-18     | Engineering Validation           | Converted to documentation index and added Rev1.5 engineering documentation structure                                                                                                                                                                                           |
| 0.9.1   | 2026-08-18     | Engineering Validation           | Documentation consistency update                                                                                                                                                                                                                                                |
| **1.0** | **2026-08-29** | **Production Release Candidate** | Updated documentation index to Rev1.5.1; removed obsolete Project Specification and legacy BOM references; added Master BOM/CPL, Review Record, Datasheet Index and Roadmap; updated documentation authority, reading paths, production status and physical-validation boundary |

---

# Current Documentation Release

**WASDPad+ Rev1.5.1**

**Documentation Version:** 1.0
**Hardware Status:** Production Release Candidate
**Core Engineering Documentation:** Complete
**Physical Production Validation:** Pending
**Production Approval:** Pending
