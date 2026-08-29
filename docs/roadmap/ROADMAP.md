# WASDPad+ Development Roadmap

**Document Version:** 2.0
**Current Hardware Revision:** Rev1.5.1
**Current Status:** Production Release Candidate
**Last Updated:** 2026-08-29

---

# 1. Current Status

WASDPad+ **Rev1.5.1** has completed its principal engineering and pre-production design stages.

The hardware architecture is frozen for the production candidate.

Completed areas include:

* schematic design
* PCB layout
* component selection
* electrical protection
* hardware autofire
* hot-swap implementation
* status indication
* key backlighting
* PCB grounding
* ERC / DRC
* critical component validation
* assembly-orientation review
* Gerber and drill generation
* Master BOM
* Master CPL
* datasheet traceability
* alternate-component policy
* procurement documentation
* engineering release review

The project has therefore moved from active hardware development into the **manufacturing and physical validation phase**.

Current development path:

```text
Rev1.5.1
Production Release Candidate
        │
        ▼
PCB Manufacturing
        │
        ▼
Component Procurement
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
Real-System Gameplay Validation
        │
        ▼
Production Approval
        │
        ▼
Rev1.5.1 Stable Release
```

No additional Rev1.5.1 feature development is currently planned.

---

# 2. Rev1.5.1 — Engineering Complete

The following major development areas are complete.

## Core Controller

* [x] controller architecture
* [x] UP / DOWN / LEFT / RIGHT controls
* [x] dual FIRE1 controls
* [x] dual FIRE2 controls
* [x] direct retro-computer joystick signalling
* [x] hardware-only operation
* [x] no MCU / firmware dependency

---

## Autofire

* [x] hardware autofire architecture
* [x] CMOS 555 timing architecture
* [x] production TLC555 selection
* [x] FIRE1 autofire integration
* [x] autofire OFF / ON control
* [x] SLOW / FAST selection
* [x] final timing values
* [x] CD4066 hardware mode switching
* [x] MOSFET output logic
* [x] dual-colour autofire indication

Final Rev1.5.1 timing values:

```text
FAST -> R13 = 330 kΩ
SLOW -> R14 = 680 kΩ

LEFT  -> SLOW
RIGHT -> FAST
```

---

## Mechanical Controls

* [x] MX-compatible mechanical switch architecture
* [x] eight gameplay switch positions
* [x] Kailh hot-swap sockets
* [x] bottom-side socket placement
* [x] production gameplay switch selection
* [x] replaceable mechanical-switch architecture

Production fitted switch:

**Gateron KS-8 Yellow**

---

## Electrical Protection

* [x] +5 V resettable overcurrent protection
* [x] signal-line ESD protection
* [x] +5 V ESD / TVS protection
* [x] protection-device topology review
* [x] critical protection pinout verification
* [x] production protection-device selection

---

## Power System

* [x] +5 V distribution
* [x] resettable PTC protection
* [x] local decoupling
* [x] VCC-GND decoupling
* [x] power indication
* [x] F.Cu GND zone
* [x] B.Cu GND zone
* [x] GND stitching vias

---

## Key Backlighting

* [x] eight-key backlight architecture
* [x] warm-white LED selection
* [x] individual LED current limiting
* [x] low-current illumination design
* [x] independent backlight power rail
* [x] dedicated backlight ON/OFF control
* [x] U3 bottom-side implementation
* [x] U3 PCB-side correction
* [x] backlight routing correction

---

# 3. Rev1.5.1 — PCB Engineering Complete

The PCB has completed the final engineering review.

Completed:

* [x] schematic review
* [x] ERC
* [x] PCB routing
* [x] final PCB review
* [x] DRC
* [x] FIRE1_BTN_N routing correction
* [x] GND connectivity review
* [x] GND stitching
* [x] U3 bottom-side correction
* [x] U3 routing correction
* [x] critical footprint review
* [x] critical pinout review
* [x] assembly-orientation review

Final engineering status:

```text
ERC: PASS
DRC: PASS
PCB: PASS
```

No known schematic or PCB-layout issue currently blocks production-candidate manufacture.

---

# 4. Rev1.5.1 — Critical Component Validation Complete

Critical production components have completed the required engineering review.

This includes:

* [x] TLC555CDR
* [x] CD4066BM96
* [x] 2N7002LT1G
* [x] MMBT3904LT1G
* [x] PESD5V0S4UD signal ESD arrays
* [x] TPE0562BC3 +5 V TVS device
* [x] 3BC-3-F dual-colour status LED
* [x] XL-2012WWC backlight LEDs
* [x] 1206L005/30WR resettable PTC
* [x] PCM12SMTR backlight switch
* [x] CPG151101S11 hot-swap sockets
* [x] production resistor network
* [x] production capacitor selection

The previously identified **D6 topology/pinout** and **D7 LED pinout/polarity** validation items are closed.

---

# 5. Rev1.5.1 — Manufacturing Data Complete

The production-candidate manufacturing dataset has been prepared.

Completed:

* [x] final Gerber generation
* [x] copper layers
* [x] solder-mask layers
* [x] silkscreen layers
* [x] paste layers
* [x] Edge.Cuts
* [x] PTH drill data
* [x] NPTH drill data
* [x] Master BOM
* [x] Master CPL
* [x] component assembly classification
* [x] PCB-side classification
* [x] JLCPCB/LCSC sourcing references where applicable
* [x] assembly-orientation corrections
* [x] manufacturing preview review

Production-candidate manufacturing data is therefore considered ready for use.

---

# 6. Rev1.5.1 — Documentation Complete

The engineering and manufacturing documentation has been consolidated for Rev1.5.1.

Completed documentation includes:

* [x] hardware overview
* [x] system architecture
* [x] engineering review record
* [x] Master BOM
* [x] Master CPL
* [x] BOM documentation
* [x] datasheet index
* [x] alternate-parts policy
* [x] procurement notes
* [x] manufacturing traceability model
* [x] development roadmap

Primary Rev1.5.1 hardware documentation:

```text
hardware/rev1.5/
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

System architecture:

```text
docs/architecture/System_architecture.md
```

---

# 7. Rev1.5.1 — Design Freeze

Rev1.5.1 has reached **design freeze** for the production candidate.

The following areas shall not be changed without explicit engineering review:

* circuit topology
* PCB routing
* connector pinout
* protection architecture
* autofire timing
* PCB footprints
* critical component MPNs
* switch geometry
* mechanical PCB dimensions
* manufacturing orientation

Minor documentation corrections and approved sourcing substitutions do not necessarily require a hardware revision.

Any electrical or mechanical design change must be evaluated before manufacturing data is modified.

---

# 8. Current Phase — Manufacturing

The immediate project milestone is manufacture of the first complete Rev1.5.1 production-candidate hardware.

Remaining manufacturing tasks:

* [ ] order Rev1.5.1 PCBs
* [ ] procure remaining production components
* [ ] receive PCB assemblies
* [ ] perform incoming PCB inspection
* [ ] manually assemble components not included in automated assembly
* [ ] install Kailh hot-swap sockets
* [ ] install U3 where manually assembled
* [ ] install THT components
* [ ] install DB9 cable
* [ ] install mechanical switches
* [ ] assemble complete controller

No new feature development should be introduced during this phase.

---

# 9. Current Phase — Electrical Bring-Up

Before connection to a retro computer, the assembled controller must complete basic electrical validation.

Required checks:

* [ ] visual PCB inspection
* [ ] solder-joint inspection
* [ ] component-orientation inspection
* [ ] +5 V to GND short-circuit check
* [ ] DB9 continuity verification
* [ ] GND continuity verification
* [ ] +5 V rail verification
* [ ] power-indicator test
* [ ] abnormal current-consumption check
* [ ] abnormal heating check

Only after successful basic bring-up should the controller be connected to representative host hardware.

---

# 10. Current Phase — Functional Validation

The first complete Rev1.5.1 controller must validate all gameplay functions.

Required tests:

* [ ] UP
* [ ] DOWN
* [ ] LEFT
* [ ] RIGHT
* [ ] simultaneous-direction behaviour
* [ ] FIRE1 left
* [ ] FIRE1 right
* [ ] FIRE2 left
* [ ] FIRE2 right
* [ ] autofire OFF
* [ ] autofire SLOW
* [ ] autofire FAST
* [ ] SLOW / FAST selector orientation
* [ ] dual-colour status indication
* [ ] power indication
* [ ] D8–D15 key backlighting
* [ ] backlight ON/OFF control
* [ ] Kailh hot-swap operation
* [ ] mechanical-switch replacement
* [ ] DB9 cable assembly

Successful functional operation of the complete controller is the primary hardware acceptance criterion.

---

# 11. Real-System Validation

Following bench validation, Rev1.5.1 must be tested on representative original hardware.

Planned validation includes:

* [ ] Commodore 64 basic joystick operation
* [ ] Commodore 64 autofire gameplay
* [ ] representative FIRE2-capable software
* [ ] Amiga basic joystick operation
* [ ] representative Amiga gameplay
* [ ] extended gameplay session
* [ ] repeated switch operation
* [ ] repeated autofire mode changes
* [ ] extended backlight operation
* [ ] hot-swap socket retention check

Additional supported platforms may be validated separately.

---

# 12. Enclosure

The Rev1.5.1 enclosure is developed separately by **Dester3D**.

Mechanical design files and enclosure-specific documentation are maintained under:

```text
enclosure/
```

Final enclosure validation must be performed using the production Rev1.5.1 PCB and complete assembled controller.

Remaining enclosure milestone:

* [ ] verify final production PCB fit
* [ ] verify switch alignment
* [ ] verify DB9 cable routing
* [ ] verify autofire switch access
* [ ] verify backlight switch access
* [ ] verify LED visibility
* [ ] verify enclosure closure and mechanical stability
* [ ] perform assembled-controller gameplay validation

---

# 13. Rev1.5.1 Production Approval

Rev1.5.1 may move from:

**Production Release Candidate**

to:

**Production Approved**

when all of the following conditions have been met:

1. the production PCB is successfully manufactured,
2. the controller is successfully assembled,
3. electrical bring-up passes,
4. all controller inputs operate correctly,
5. SLOW and FAST autofire operate correctly,
6. status indication operates correctly,
7. key backlighting operates correctly,
8. hot-swap functionality operates correctly,
9. the DB9 cable assembly is verified,
10. the enclosure fits and functions correctly,
11. representative real-system gameplay validation succeeds,
12. no production-blocking electrical, mechanical or thermal issue is discovered.

After successful validation, the release status becomes:

```text
WASDPad+ Rev1.5.1
PRODUCTION APPROVED
```

---

# 14. Rev1.5.1 Stable Release

After Production Approval, Rev1.5.1 enters the stable maintenance phase.

The priorities then become:

* production consistency
* component availability
* approved alternate parts
* documentation maintenance
* manufacturing repeatability
* issue tracking
* field feedback
* lifecycle management

Rev1.5.1 should not become a continuing feature-development branch.

New functionality requiring architectural changes belongs to a future hardware revision.

---

# 15. Rev1.5.1 Maintenance Policy

Once released, changes should be categorized as follows.

## Documentation Change

Examples:

* wording correction
* datasheet-link update
* supplier information
* clarification

No hardware revision required.

## Sourcing Change

Examples:

* approved alternate manufacturer
* supplier change
* equivalent passive component

May remain Rev1.5.1 if electrical and mechanical behaviour is unchanged and the substitution is approved.

## Hardware Change

Examples:

* schematic change
* PCB routing change
* footprint change
* timing change
* connector change
* new functional feature

Requires explicit engineering review and may require a new hardware revision.

---

# 16. Future Rev2.0

Rev2.0 is a separate future programmable WASDPad platform.

It is **not** part of the Rev1.5.1 production program.

Potential concepts include:

* MCU-controlled autofire
* adjustable autofire parameters
* burst-fire modes
* programmable behaviour
* configurable debounce
* game-specific profiles
* persistent configuration
* programmable multi-colour indication
* USB configuration
* firmware update capability
* optional USB HID functionality

An MCU platform such as the **RP2040 family** may be evaluated for this generation.

No Rev2.0 architecture is considered frozen at this stage.

---

# 17. Rev2.0 Development Gate

Rev2.0 development should remain separated from Rev1.5.1 production stabilization.

Recommended sequence:

```text
Rev1.5.1 Production Candidate
            │
            ▼
Manufacture + Validate
            │
            ▼
Rev1.5.1 Production Approved
            │
            ▼
Stable Production / Maintenance
            │
            ▼
Rev2.0 Requirements Definition
            │
            ▼
Rev2.0 Architecture
            │
            ▼
Rev2.0 Development
```

This prevents future feature development from destabilizing the production-ready discrete hardware platform.

---

# 18. Long-Term Product Structure

The intended product-development structure is:

```text
WASDPad
│
├── Rev1.2
│   └── Validated original hardware platform
│
├── Rev1.5 / Rev1.5.1
│   └── Mature discrete-hardware platform
│       ├── protection
│       ├── hot-swap switches
│       ├── hardware autofire
│       ├── status indication
│       ├── key backlighting
│       └── production documentation
│
└── Future Rev2.0
    └── Programmable platform
        ├── MCU
        ├── firmware
        ├── configurable behaviour
        └── advanced gameplay functions
```

Rev1.5.1 and Rev2.0 therefore represent different design philosophies rather than simple feature increments.

---

# 19. Immediate Project Priority

The immediate project priority is:

> **Do not add new Rev1.5.1 features. Manufacture, assemble and validate the frozen production-candidate design.**

Current sequence:

```text
NOW
 │
 ├─ Rev1.5.1 design freeze              ✓
 │
 ├─ Engineering release review          ✓
 │
 ├─ Manufacturing documentation         ✓
 │
 ├─ PCB manufacturing                   ← CURRENT
 │
 ├─ Assembly
 │
 ├─ Electrical bring-up
 │
 ├─ Functional validation
 │
 ├─ Real-system gameplay validation
 │
 ├─ Enclosure validation
 │
 └─ Rev1.5.1 Production Approval
              │
              ▼
       Stable Production
              │
              ▼
          Maintenance
              │
              ▼
    Future Rev2.0 Development
```

---

# 20. Current Milestone

## WASDPad+ Rev1.5.1

**Engineering:** COMPLETE
**Design Freeze:** COMPLETE
**Engineering Review:** PASS
**PCB / Manufacturing Data:** COMPLETE
**Documentation:** COMPLETE
**Production-Candidate Manufacturing:** NEXT
**Physical Hardware Validation:** PENDING
**Production Approval:** PENDING

### Current Release Status

**PRODUCTION RELEASE CANDIDATE**

---

# 21. Version History

| Version | Date           | Changes                                                                                                                                                                                                                                                                                                                                                      |
| ------- | -------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 0.x     | Not recorded   | Initial development roadmap and Rev1.5 planning                                                                                                                                                                                                                                                                                                              |
| 1.0     | 2026-08-19     | Simplified roadmap for Rev1.5 pre-production state; major development areas marked complete and remaining work reduced to final design review, manufacturing, functional validation and release                                                                                                                                                              |
| **2.0** | **2026-08-29** | Updated roadmap to Rev1.5.1 Production Release Candidate; closed schematic/PCB/ERC/DRC, D6/D7 validation, manufacturing-data and documentation milestones; added design freeze, key-backlight system, electrical bring-up, physical validation, production approval and stable-maintenance gates; retained Rev2.0 as a separate future programmable platform |

---

**Current milestone: WASDPad+ Rev1.5.1 — Production Release Candidate / Ready for Manufacturing**
