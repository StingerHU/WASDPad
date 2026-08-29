# WASDPad Hardware

This directory contains the hardware design, manufacturing documentation and revision-specific engineering records for the **WASDPad / WASDPad+** controller platform.

WASDPad is a hardware-based retro-computer game controller designed around the traditional digital joystick interface used by systems such as the **Commodore 64** and **Amiga**.

The project prioritizes:

* deterministic hardware operation
* extremely low input latency
* compatibility with original retro hardware
* serviceability
* replaceable mechanical controls
* electrical protection
* reproducible manufacturing
* documented component traceability

---

# Hardware Revision Structure

Hardware documentation is organized by PCB revision.

```text
hardware/
│
├── README.md
│
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

Each revision directory contains the engineering documentation applicable to that hardware generation.

---

# Current Hardware Generation

## WASDPad+ Rev1.5.1

**Status:** Production Release Candidate

Revision 1.5.1 is the current production-oriented discrete-hardware version of WASDPad+.

It evolves the validated earlier WASDPad design while retaining the fundamental architecture:

* no microcontroller
* no firmware
* no operating-system dependency
* direct hardware control
* CMOS/discrete autofire logic
* traditional retro-computer joystick signalling

Major Rev1.5.1 improvements include:

* Kailh MX-compatible hot-swap sockets
* replaceable mechanical switches
* +5 V resettable overcurrent protection
* controller-line ESD protection
* +5 V ESD/TVS protection
* dual-colour autofire status indication
* warm-white key backlighting
* independent backlight control
* improved PCB grounding
* manufacturing-oriented component selection
* complete Master BOM and CPL
* manufacturer MPN traceability
* datasheet documentation
* controlled alternate-part policy
* procurement and lifecycle documentation

Detailed documentation:

[`rev1.5/README.md`](rev1.5/README.md)

---

# Rev1.5.1 Engineering Status

The principal pre-production engineering stages have been completed.

| Engineering Area                | Status   |
| ------------------------------- | -------- |
| Hardware architecture           | Complete |
| Schematic                       | Complete |
| Component selection             | Complete |
| PCB layout                      | Complete |
| ERC                             | Passed   |
| PCB DRC                         | Passed   |
| Critical pinout review          | Passed   |
| Protection topology review      | Passed   |
| PCB assembly orientation review | Passed   |
| Gerber generation               | Complete |
| Drill data generation           | Complete |
| Master BOM                      | Complete |
| Master CPL                      | Complete |
| Datasheet traceability          | Complete |
| Alternate-part policy           | Complete |
| Procurement documentation       | Complete |
| Physical Rev1.5.1 validation    | Pending  |
| Production approval             | Pending  |

The current hardware may proceed to **production-candidate manufacture**.

Final Production Approved status requires successful physical validation of manufactured Rev1.5.1 hardware.

Engineering review record:

[`rev1.5/Review_Record.MD`](rev1.5/Review_Record.MD)

---

# Manufacturing Documentation

The authoritative Rev1.5.1 manufacturing documentation is located under:

[`rev1.5/bom/`](rev1.5/bom/)

The primary engineering records are:

## Master Bill of Materials

[`rev1.5/bom/WASDPad_Rev1.5.1_FULL_MASTER_BOM.csv`](rev1.5/bom/WASDPad_Rev1.5.1_FULL_MASTER_BOM.csv)

The Master BOM is the authoritative source for:

* component designators
* manufacturer part numbers
* quantities
* footprints
* assembly classification
* PCB side
* supplier identifiers where applicable

---

## Master Component Placement List

[`rev1.5/bom/WASDPad_Rev1.5.1_FULL_MASTER_CPL.csv`](rev1.5/bom/WASDPad_Rev1.5.1_FULL_MASTER_CPL.csv)

The Master CPL contains the complete component-placement dataset.

Assembly-house-specific CPL files may be generated as subsets of this file.

---

## Datasheet Index

[`rev1.5/bom/DATASHEET_INDEX.md`](rev1.5/bom/DATASHEET_INDEX.md)

Provides centralized manufacturer and technical references for production components.

---

## Alternate Parts

[`rev1.5/bom/ALTERNATE_PARTS.md`](rev1.5/bom/ALTERNATE_PARTS.md)

Defines the controlled component-substitution policy, including:

* Production Primary
* Approved Alternate
* Legacy Validated
* Candidate
* Not Approved

---

## Procurement Notes

[`rev1.5/bom/PROCUREMENT_NOTES.md`](rev1.5/bom/PROCUREMENT_NOTES.md)

Defines:

* sourcing policy
* supplier requirements
* assembly-house substitutions
* lifecycle management
* incoming component verification
* production traceability
* procurement change control

---

# Documentation Authority

For the current Rev1.5.1 hardware, engineering information should be resolved in the following order:

```text
Hardware architecture / revision status
        ↓
rev1.5/README.md

Engineering release validation
        ↓
rev1.5/Review_Record.MD

Production component identity
        ↓
rev1.5/bom/WASDPad_Rev1.5.1_FULL_MASTER_BOM.csv

Component placement
        ↓
rev1.5/bom/WASDPad_Rev1.5.1_FULL_MASTER_CPL.csv

Component technical references
        ↓
rev1.5/bom/DATASHEET_INDEX.md

Component substitutions
        ↓
rev1.5/bom/ALTERNATE_PARTS.md

Sourcing and lifecycle policy
        ↓
rev1.5/bom/PROCUREMENT_NOTES.md
```

The **Master BOM is authoritative for production component identity**.

---

# Hardware Design Philosophy

WASDPad intentionally follows a hardware-first design philosophy.

The controller avoids unnecessary abstraction between the player and the original computer hardware.

For the current discrete-hardware generation, this means:

* physical switches directly influence hardware logic
* no firmware input scanning
* no USB polling
* no operating-system driver
* no wireless protocol
* no software translation layer

The result is a controller architecture appropriate for original retro-computer hardware and latency-sensitive gameplay.

---

# Compatibility

WASDPad is based on the traditional digital joystick-interface architecture associated with classic systems including:

* Commodore 64
* Commodore Amiga
* compatible Atari-style digital joystick interfaces

Platform compatibility depends on the electrical implementation of the target system.

Features beyond the standard single-fire digital joystick interface, particularly **FIRE2**, may require platform or software support.

Compatibility with a platform should therefore be explicitly validated before being considered officially supported.

---

# Revision Policy

Hardware changes that affect any of the following should be documented under a new revision or controlled engineering update:

* schematic topology
* PCB layout
* pinout
* electrical protection
* timing behaviour
* component footprint
* mechanical compatibility
* external interface
* user-visible functionality

Simple sourcing changes may remain within the same hardware revision when the replacement is an approved equivalent and does not alter electrical or mechanical behaviour.

---

# Future Hardware

Revision 1.5.1 represents the mature **discrete-hardware** branch of WASDPad+.

More advanced features requiring programmable control are intentionally outside the scope of Rev1.5.1.

A future hardware generation may introduce capabilities such as:

* programmable autofire
* additional firing modes
* configurable profiles
* game-specific behaviour
* enhanced status indication

Such functionality should be implemented as a separate hardware generation rather than increasing the complexity of the stable Rev1.5.1 architecture.

---

# Current Release

**Current Hardware:** WASDPad+ Rev1.5.1
**Release Status:** Production Release Candidate
**Engineering Review:** PASS
**Physical Production Validation:** Pending

For detailed hardware information, continue with:

**[`rev1.5/README.md`](rev1.5/README.md)**

For the final pre-production engineering review:

**[`rev1.5/Review_Record.MD`](rev1.5/Review_Record.MD)**

For manufacturing and component documentation:

**[`rev1.5/bom/`](rev1.5/bom/)**
