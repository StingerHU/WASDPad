# WASDPad+ Development Roadmap

**Document Version:** 0.9  
**Current Hardware Revision:** Rev 1.5  
**Current Phase:** Engineering Validation / Pre-Prototype  
**Last Updated:** 2026-08-18

---

# 1. Purpose

This document tracks the development milestones of the **WASDPad+** project.

The current engineering priority is the completion and validation of **Hardware Revision 1.5**.

Future programmable hardware development, including Rev 2.0, remains a separate project phase and shall not delay or redefine the Rev 1.5 production-validation milestone.

---

# 2. Revision Overview

| Revision | Purpose | Status |
|---|---|---|
| Rev 1.2 | Validated predecessor hardware | Complete / Reference |
| **Rev 1.5** | Protected, serviceable hardware-only controller | **Engineering Validation** |
| Rev 2.0 | Future programmable platform | Future / Planning |

---

# 3. Rev 1.2 — Validated Predecessor

Rev 1.2 established the functional hardware basis of WASDPad+.

Its primary role is now to serve as the validated predecessor architecture for Rev 1.5.

### Completed

- [x] WASD-style directional control
- [x] FIRE control architecture
- [x] hardware-only operation
- [x] hardware autofire concept
- [x] direct Atari-style DB9 interface
- [x] physical gameplay testing
- [x] functional controller architecture

Rev 1.2 is not the current production-development target.

---

# 4. Rev 1.5 — Current Development Revision

## Goal

Rev 1.5 evolves the proven hardware-only architecture into a more:

- protected
- serviceable
- reproducible
- manufacturable
- documented

controller platform.

Current status:

**Engineering Validation / Pre-Prototype**

---

# 5. Rev 1.5 — Architecture

### Completed

- [x] Hardware-only architecture retained
- [x] No microcontroller required
- [x] No firmware dependency
- [x] Direct DB9 joystick interface retained
- [x] Independent UP / DOWN / LEFT / RIGHT signals
- [x] FIRE1 architecture defined
- [x] FIRE2 / POTX architecture defined
- [x] Hardware autofire architecture defined
- [x] Separate autofire OFF / ON control defined
- [x] Separate SLOW / FAST selector defined
- [x] Rev 1.5 system architecture documented

Reference:

```text
docs/architecture/System_architecture.md
```

---

# 6. Rev 1.5 — Autofire

### Completed

- [x] CMOS hardware autofire architecture
- [x] Renesas ICM7555 selected
- [x] CD4066 switching architecture selected
- [x] FAST timing physically evaluated
- [x] SLOW timing physically evaluated
- [x] Final FAST resistor selected
- [x] Final SLOW resistor selected
- [x] Physical speed-selector orientation validated

Final Rev 1.5 configuration:

```text
FAST -> R13 = 330 kΩ
SLOW -> R14 = 680 kΩ

LEFT  -> SLOW
RIGHT -> FAST
```

### Pending

- [ ] Validate both timing modes on final Rev 1.5 prototype
- [ ] Measure final prototype autofire frequencies
- [ ] Confirm reliable long-duration autofire operation

---

# 7. Rev 1.5 — Electrical Protection

### Completed

- [x] Resettable +5 V overcurrent protection defined
- [x] Littelfuse 1206L005/30WR selected
- [x] Signal-line ESD architecture defined
- [x] Nexperia PESD5V0S4UD selected
- [x] +5 V ESD protection defined
- [x] Nexperia PESD6V0L2UU selected
- [x] D6 schematic topology reviewed
- [x] D6 datasheet pinout reviewed
- [x] Supply decoupling defined

Validated D6 mapping:

```text
Pin 1 -> protected +5 V
Pin 2 -> NC
Pin 3 -> GND
```

### Mandatory Final Review

- [ ] Recheck D6 PESD6V0L2UU datasheet topology against final schematic
- [ ] Recheck D6 physical footprint/pad numbering against final PCB
- [ ] Review D4/D5 ESD placement and return paths
- [ ] Validate protected +5 V rail on prototype
- [ ] Measure final controller supply current

---

# 8. Rev 1.5 — Mechanical Switch System

### Completed

- [x] MX-compatible gameplay-switch architecture selected
- [x] Hot-swap requirement defined
- [x] Kailh / Kaihua CPG151101S11 selected
- [x] PCB hot-swap footprint selected
- [x] Gateron KS-8 Yellow selected as default gameplay switch
- [x] Eight gameplay-switch positions defined
- [x] Alternate MX-switch strategy documented

### Pending

- [ ] Validate all eight sockets on final PCB
- [ ] Verify switch retention
- [ ] Verify repeated insertion/removal
- [ ] Verify enclosure clearance
- [ ] Verify PCB mechanical stability during switch replacement

---

# 9. Rev 1.5 — Status Indication

### Power LED

Completed:

- [x] Dedicated D1 power indicator defined
- [x] 3 mm THT footprint selected
- [x] Red / Blue / White product variants allowed
- [x] Series resistor defined

### Autofire Indicator

Completed:

- [x] Separate dual-colour autofire LED defined
- [x] Red / Green indication selected
- [x] Common-cathode topology selected
- [x] Bivar 3BC-3-F selected
- [x] D7 datasheet pinout reviewed
- [x] MMBT3904 driver architecture reviewed
- [x] Q1/Q2 transistor pin mapping reviewed

Current D7 mapping:

```text
Pin 1 -> RED anode -> R22
Pin 2 -> Common cathode -> GND
Pin 3 -> GREEN anode -> R23
```

### Mandatory Final Review

- [ ] Recheck D7 manufacturer datasheet against final schematic
- [ ] Recheck D7 physical footprint pad numbering
- [ ] Recheck common-cathode configuration
- [ ] Recheck RED / GREEN channel assignment
- [ ] Validate both LED channels on final prototype
- [ ] Confirm final user-visible colour/state mapping

---

# 10. Rev 1.5 — Component Selection and BOM

### Completed

- [x] Primary component selection
- [x] Core IC selection
- [x] MOSFET selection
- [x] transistor selection
- [x] resistor-family standardization
- [x] capacitor selection
- [x] ESD component selection
- [x] PPTC selection
- [x] power LED strategy
- [x] dual-colour LED selection
- [x] toggle-switch selection
- [x] MX hot-swap socket selection
- [x] default gameplay-switch selection
- [x] controller-cable sourcing strategy
- [x] alternate-parts strategy
- [x] procurement strategy

Current BOM status:

**Pre-Release Validated / Component Selection Complete**

Documentation:

```text
hardware/rev1.5/bom/
├── README.md
├── wasdpad+v1.5.csv
├── ALTERNATE_PARTS.md
└── PROCUREMENT_NOTES.md
```

---

# 11. Rev 1.5 — Controller Cable

### Completed

- [x] DB9 female cable architecture defined
- [x] Current supplier cable identified
- [x] PCB flying-lead connection defined
- [x] J1 solder-pad interface defined
- [x] DB9-to-wire mapping validated
- [x] Unused conductor handling documented
- [x] New-batch continuity-test requirement defined
- [x] Cable assembly procedure documented

Reference:

```text
docs/assembly/CABLE_ASSEMBLY.md
```

### Pending

- [ ] Validate cable routing in final enclosure
- [ ] Validate strain relief
- [ ] Validate production cable assembly on final prototype

---

# 12. Rev 1.5 — Documentation

### Completed / Current

- [x] Root project README
- [x] Documentation index
- [x] Rev 1.5 hardware README
- [x] System architecture
- [x] Project specification
- [x] Feature specification
- [x] BOM documentation
- [x] Alternate-parts strategy
- [x] Procurement notes
- [x] Cable assembly procedure
- [x] Feature acceptance criteria
- [x] Documentation version tracking introduced

### Planned

- [ ] PCB assembly procedure
- [ ] Production test procedure
- [ ] Mechanical / enclosure documentation
- [ ] Final Rev 1.5 release notes

Planned structure:

```text
docs/
├── assembly/
│   ├── CABLE_ASSEMBLY.md
│   └── PCB_ASSEMBLY.md
│
├── testing/
│   └── PRODUCTION_TEST.md
│
└── mechanical/
    └── ENCLOSURE.md
```

---

# 13. Rev 1.5 — Schematic Validation

Current status:

**Engineering Review**

### Required Before Release

- [ ] Complete full schematic review
- [ ] Run final KiCad ERC
- [ ] Resolve all unexplained ERC warnings
- [ ] Verify every symbol-to-footprint mapping
- [ ] Verify power rails
- [ ] Verify FIRE1 signal path
- [ ] Verify FIRE2 signal path
- [ ] Verify ICM7555 timing network
- [ ] Verify CD4066 connectivity
- [ ] Verify unused IC sections/pins
- [ ] Verify all 2N7002 G/S/D mappings
- [ ] Verify MMBT3904 B/E/C mappings
- [ ] Recheck D6 topology and pinout
- [ ] Recheck D7 common-cathode pinout
- [ ] Verify all LED polarities
- [ ] Verify R13 = 330 kΩ
- [ ] Verify R14 = 680 kΩ
- [ ] Verify SLOW / FAST switch mapping
- [ ] Verify DB9/J1 signal mapping

A clean ERC result alone is not sufficient for schematic approval.

---

# 14. Rev 1.5 — PCB Validation

Current status:

**Engineering Review**

### Required Before Manufacturing

- [ ] Run final KiCad DRC
- [ ] Resolve all unexplained DRC warnings
- [ ] Review component orientations
- [ ] Review SMD footprint pad numbering
- [ ] Review THT LED polarity
- [ ] Review D6 footprint/pad mapping
- [ ] Review D7 footprint/pad mapping
- [ ] Review ESD placement
- [ ] Review ESD return paths
- [ ] Review +5 V routing
- [ ] Review GND routing
- [ ] Review hot-swap socket geometry
- [ ] Review toggle-switch orientation
- [ ] Review cable solder-pad accessibility
- [ ] Review mounting holes
- [ ] Review enclosure clearances
- [ ] Perform final Gerber visual inspection

A clean DRC result alone is not sufficient for PCB approval.

---

# 15. Rev 1.5 — Prototype Manufacturing

Current status:

**Pending**

### Milestone

Manufacture the first complete PCB implementing the finalized Rev 1.5 schematic and PCB layout.

Required:

- [ ] Generate final Gerbers
- [ ] Generate drill files
- [ ] Archive manufacturing outputs
- [ ] Order Rev 1.5 PCB
- [ ] Receive and visually inspect PCB
- [ ] Assemble first complete Rev 1.5 prototype

---

# 16. Rev 1.5 — Prototype Electrical Validation

### Pre-Power Tests

- [ ] Inspect soldering
- [ ] Inspect U1 for bridges / excess solder paste
- [ ] Measure +5 V-to-GND resistance
- [ ] Verify DB9 cable continuity
- [ ] Verify +5 V polarity
- [ ] Verify GND
- [ ] Verify absence of unintended shorts

### Powered Tests

- [ ] Measure incoming +5 V
- [ ] Measure protected +5 V rail
- [ ] Measure total controller current
- [ ] Verify D1 power LED
- [ ] Check active IC supply voltages
- [ ] Confirm no abnormal component heating

---

# 17. Rev 1.5 — Functional Validation

Required final prototype tests:

- [ ] UP
- [ ] DOWN
- [ ] LEFT
- [ ] RIGHT
- [ ] simultaneous direction combinations
- [ ] FIRE1 manual
- [ ] FIRE2 manual
- [ ] autofire OFF
- [ ] autofire ON
- [ ] SLOW
- [ ] FAST
- [ ] LEFT = SLOW
- [ ] RIGHT = FAST
- [ ] D7 SLOW indication
- [ ] D7 FAST indication
- [ ] FIRE1 release stops autofire
- [ ] FIRE2 remains independent
- [ ] no unintended joystick-line activation

These tests shall later be formalized in:

```text
docs/testing/PRODUCTION_TEST.md
```

---

# 18. Rev 1.5 — Mechanical Validation

- [ ] Verify all eight switches
- [ ] Verify all hot-swap sockets
- [ ] Verify toggle-switch access
- [ ] Verify LED alignment
- [ ] Verify PCB mounting
- [ ] Verify enclosure fit
- [ ] Verify cable exit
- [ ] Verify cable strain relief
- [ ] Verify switch replacement with enclosure design
- [ ] Verify normal gameplay ergonomics

---

# 19. Rev 1.5 — Gameplay Validation

After electrical validation:

- [ ] Test on Commodore 64
- [ ] Test on Commodore 128 where available
- [ ] Test on Commodore Amiga
- [ ] Verify manual FIRE response
- [ ] Verify FIRE2 behaviour
- [ ] Verify SLOW autofire usability
- [ ] Verify FAST autofire usability
- [ ] Verify extended gameplay stability
- [ ] Verify controller current remains acceptable
- [ ] Verify no abnormal host behaviour

Other platforms may be tested separately but are not required to complete the primary Rev 1.5 validation milestone.

---

# 20. Rev 1.5 — Production Documentation

Before production approval:

- [ ] Create `PCB_ASSEMBLY.md`
- [ ] Create `PRODUCTION_TEST.md`
- [ ] Create enclosure/mechanical documentation
- [ ] Finalize production cable procedure
- [ ] Finalize approved BOM
- [ ] Finalize alternate-parts list
- [ ] Finalize procurement notes
- [ ] Record prototype validation results
- [ ] Create Rev 1.5 release notes

---

# 21. Rev 1.5 — Production Release Milestone

Rev 1.5 may transition from:

```text
Engineering Validation
```

to:

```text
Production Validated
```

only after all of the following are complete:

1. Final schematic review
2. ERC passed
3. Final PCB review
4. DRC passed
5. Rev 1.5 PCB manufactured
6. Complete prototype assembled
7. Electrical validation passed
8. Functional validation passed
9. Mechanical validation passed
10. Gameplay validation passed
11. Production test procedure completed
12. Manufacturing documentation completed

This milestone will also permit the primary Rev 1.5 documentation to transition from pre-release to production-validated status.

---

# 22. Immediate Next Actions

Current priority order:

```text
1. Final schematic audit
2. Final PCB audit
3. Final ERC / DRC
4. Create PRODUCTION_TEST.md
5. Create PCB_ASSEMBLY.md
6. Manufacture Rev 1.5 prototype
7. Electrical validation
8. Functional validation
9. Mechanical / gameplay validation
10. Production release
```

The highest technical priority is currently the **final schematic and PCB audit**.

---

# 23. Rev 2.0 — Future Platform

Rev 2.0 is planned as a separate programmable architecture.

It shall not block completion of Rev 1.5.

Potential Rev 2.0 features include:

- [ ] RP2040-class microcontroller
- [ ] firmware-controlled autofire
- [ ] adjustable FAST autofire
- [ ] burst mode
- [ ] configurable debounce
- [ ] game-specific profiles
- [ ] persistent configuration
- [ ] programmable multi-colour status indication
- [ ] USB firmware update
- [ ] optional USB HID support

Detailed Rev 2.0 requirements shall be created separately when active development begins.

---

# 24. Deferred / Undecided Features

The following concepts are intentionally not part of the current Rev 1.5 release milestone:

- FIRE2 autofire
- firmware-based behaviour
- programmable autofire
- burst mode
- game profiles
- macros
- USB HID
- wireless operation

These features require a separate engineering decision and shall not be added silently to Rev 1.5 scope.

---

# 25. Project Milestones

| Milestone | Status |
|---|---|
| Rev 1.2 functional architecture | ✅ Complete |
| Rev 1.5 requirements | ✅ Complete |
| Rev 1.5 architecture | ✅ Complete |
| Rev 1.5 component selection | ✅ Complete |
| Rev 1.5 BOM | ✅ Pre-Release Validated |
| Rev 1.5 technical documentation refresh | ✅ Substantially Complete |
| Rev 1.5 schematic | 🚧 Engineering Review |
| Rev 1.5 PCB | 🚧 Engineering Review |
| Rev 1.5 production test specification | ⏳ Planned |
| Rev 1.5 prototype manufacturing | ⏳ Pending |
| Rev 1.5 prototype validation | ⏳ Pending |
| Rev 1.5 production release | ⏳ Pending |
| Rev 2.0 active development | ⏳ Future |

---

# 26. Related Documentation

```text
README.md
docs/README.md

docs/architecture/
└── System_architecture.md

docs/specification/
├── PROJECT_SPECIFICATION.md
└── FEATURE_SPECIFICATION.md

docs/assembly/
└── CABLE_ASSEMBLY.md

hardware/rev1.5/
├── README.md
└── bom/
    ├── README.md
    ├── wasdpad+v1.5.csv
    ├── ALTERNATE_PARTS.md
    └── PROCUREMENT_NOTES.md
```

---

# 27. Document Versioning

Roadmap-document versions are independent from hardware revisions.

Current state:

```text
Hardware Revision: Rev 1.5
Roadmap Version:   0.9
```

Checkbox/status updates do not require a hardware revision change.

A roadmap version should be incremented when project milestones, scope or development priorities materially change.

---

# 28. Version History

| Version | Date | Status | Changes |
|---|---|---|---|
| 0.1 | Not recorded | Initial | Initial WASDPad+ development roadmap |
| 0.4 | Not recorded | Planning | Rev 1.5 protection and hot-swap goals introduced |
| 0.6 | Not recorded | Development | Rev 1.5 component and autofire planning expanded |
| 0.8 | Not recorded | Engineering | BOM and hardware-development tasks expanded |
| **0.9** | **2026-08-18** | **Engineering Validation** | Updated roadmap to actual Rev 1.5 state; marked architecture, component selection, BOM, protection architecture, hot-swap system, autofire values, D6/D7 validation, cable documentation and specification refresh as completed; added final schematic/PCB audit, prototype, production-test and release milestones; separated Rev 2.0 future scope |

---

# 29. Next Roadmap Version

The next planned roadmap version is:

**v1.0**

Target milestone:

**Rev 1.5 first complete prototype successfully manufactured and validated.**

At that point the roadmap should record actual validation results and define the remaining steps toward production release.

---

**Current Project Priority: Complete Rev 1.5 engineering validation before beginning active Rev 2.0 development.**
