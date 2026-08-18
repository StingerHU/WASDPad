# WASDPad+ Hardware

**Document Version:** 0.9  
**Current Hardware Revision:** Rev 1.5  
**Status:** Engineering Validation  
**Last Updated:** 2026-08-18

---

# 1. Purpose

This directory contains revision-specific hardware design files and supporting documentation for the **WASDPad+** controller.

The current development target is:

**WASDPad+ Hardware Revision 1.5**

Rev 1.5 is currently in:

**Engineering Validation / Pre-Prototype**

---

# 2. Hardware Revisions

| Revision | Role | Status |
|---|---|---|
| Rev 1.2 | Validated predecessor / reference design | Complete / Reference |
| **Rev 1.5** | Current protected and serviceable hardware-only design | **Engineering Validation** |
| Rev 2.0 | Future programmable architecture | Future |

---

# 3. Rev 1.5

Rev 1.5 is the current hardware development revision.

Major characteristics include:

- hardware-only operation
- direct Atari-style DE-9 / DB9 interface
- independent directional controls
- FIRE1 and FIRE2
- two-speed hardware autofire
- dedicated autofire OFF / ON control
- SLOW / FAST selector
- MX-compatible hot-swap gameplay switches
- PPTC +5 V protection
- signal-line ESD protection
- +5 V ESD protection
- power indication
- dual-colour autofire indication

Rev 1.5 requires no:

- microcontroller
- firmware
- USB interface
- host driver
- configuration software

---

# 4. Rev 1.5 Directory

```text
hardware/
└── rev1.5/
    ├── README.md
    ├── bom/
    │   ├── README.md
    │   ├── wasdpad+v1.5.csv
    │   ├── ALTERNATE_PARTS.md
    │   └── PROCUREMENT_NOTES.md
    ├── schematic/
    └── pcb/
```

The revision-specific README is the primary entry point:

```text
hardware/rev1.5/README.md
```

---

# 5. BOM

Rev 1.5 component documentation is maintained under:

```text
hardware/rev1.5/bom/
```

## `wasdpad+v1.5.csv`

Authoritative Rev 1.5 component list.

Contains the selected:

- components
- values
- quantities
- footprints
- manufacturer references
- manufacturer part numbers
- datasheet references

## `README.md`

Engineering overview of the BOM and major component decisions.

## `ALTERNATE_PARTS.md`

Defines approved and conditional component-substitution strategies.

## `PROCUREMENT_NOTES.md`

Defines sourcing and procurement guidance.

---

# 6. Schematic

Rev 1.5 schematic files are maintained under:

```text
hardware/rev1.5/schematic/
```

Current status:

**Engineering Review**

Before manufacturing approval, the final schematic must pass both automated and manual validation.

Critical manual checks include:

- DB9 signal mapping
- +5 V / GND routing
- FIRE1 and FIRE2 paths
- ICM7555 timing network
- CD4066 connectivity
- 2N7002 pin mapping
- MMBT3904 pin mapping
- D6 ESD topology and pinout
- D7 dual-colour LED topology and pinout
- autofire timing values
- physical SLOW / FAST switch mapping

A clean ERC result alone is not sufficient for release approval.

---

# 7. PCB

Rev 1.5 PCB files are maintained under:

```text
hardware/rev1.5/pcb/
```

Current status:

**Engineering Review**

Before manufacturing approval, the final PCB must be checked for:

- DRC compliance
- component orientation
- footprint/pad numbering
- ESD placement
- +5 V and GND routing
- hot-swap socket geometry
- toggle-switch orientation
- LED orientation
- cable-pad accessibility
- mechanical clearances
- final Gerber integrity

A clean DRC result alone is not sufficient for production approval.

---

# 8. Critical Rev 1.5 Hardware Values

The following values are part of the validated Rev 1.5 behaviour:

```text
R13 = 330 kΩ -> FAST
R14 = 680 kΩ -> SLOW

Speed selector:
LEFT  -> SLOW
RIGHT -> FAST
```

These shall not be changed as ordinary procurement substitutions.

---

# 9. Protection Architecture

Rev 1.5 introduces dedicated host-interface protection.

Primary components:

```text
PPTC:
Littelfuse 1206L005/30WR

Signal ESD:
Nexperia PESD5V0S4UD

+5 V ESD:
Nexperia PESD6V0L2UU
```

Protection components and their PCB implementation must be checked against the manufacturer datasheets before manufacturing release.

---

# 10. Switch System

Primary hot-swap socket:

**Kailh / Kaihua CPG151101S11**

Default gameplay switch:

**Gateron KS-8 Yellow**

Rev 1.5 uses eight MX-compatible hot-swap gameplay-switch positions.

Alternative MX-style switches may be used only when mechanical compatibility is confirmed.

---

# 11. Status LEDs

Rev 1.5 contains two independent status indicators.

## D1 — Power

3 mm THT LED.

Available product variants may include:

- Red
- Blue
- White

## D7 — Autofire

Primary component:

**Bivar 3BC-3-F**

Configuration:

**Common Cathode**

Validated logical pin assignment:

```text
Pin 1 -> RED
Pin 2 -> Common Cathode / GND
Pin 3 -> GREEN
```

The manufacturer datasheet, KiCad symbol and physical PCB footprint must be rechecked together before manufacturing approval.

---

# 12. Manufacturing State

Current Rev 1.5 state:

| Area | Status |
|---|---|
| Architecture | Defined |
| Project requirements | Defined |
| Feature requirements | Defined |
| Component selection | Complete |
| BOM | Pre-Release Validated |
| Cable assembly | Documented |
| Schematic | Engineering Review |
| PCB | Engineering Review |
| Prototype manufacturing | Pending |
| Prototype validation | Pending |
| Production test procedure | Planned |
| Production release | Pending |

---

# 13. Related Documentation

Project-level documentation:

```text
README.md
docs/README.md
```

Architecture:

```text
docs/architecture/System_architecture.md
```

Specifications:

```text
docs/specification/PROJECT_SPECIFICATION.md
docs/specification/FEATURE_SPECIFICATION.md
```

Assembly:

```text
docs/assembly/CABLE_ASSEMBLY.md
```

Development roadmap:

```text
docs/roadmap/ROADMAP.md
```

---

# 14. Rev 2.0

Rev 2.0 is a future architecture and is not part of the current Rev 1.5 release process.

Potential Rev 2.0 functionality includes:

- microcontroller-based operation
- firmware-controlled autofire
- adjustable autofire timing
- burst mode
- configurable debounce
- game profiles
- persistent configuration
- programmable status indication
- USB firmware update
- optional USB HID

Rev 2.0 development shall remain separate from Rev 1.5 engineering validation.

---

# 15. Current Hardware Priority

The current hardware-development sequence is:

```text
Final schematic audit
        |
        v
Final PCB audit
        |
        v
ERC / DRC
        |
        v
Manufacturing outputs
        |
        v
Rev 1.5 prototype
        |
        v
Electrical validation
        |
        v
Functional validation
        |
        v
Mechanical validation
        |
        v
Production release
```

The immediate priority is the **final Rev 1.5 schematic and PCB audit**.

---

# 16. Version History

| Version | Date | Status | Changes |
|---|---|---|---|
| 0.1 | Not recorded | Placeholder | Initial hardware directory placeholder |
| **0.9** | **2026-08-18** | **Engineering Validation** | Converted hardware README into revision index; documented Rev 1.5 status, hardware structure, BOM, schematic and PCB state, protection architecture, hot-swap system, critical autofire values, status LEDs, manufacturing state and Rev 2.0 boundary |

---

# 17. Next Version

The next planned version is:

**v1.0**

Target milestone:

**Rev 1.5 first complete prototype successfully manufactured and validated.**

---

**Current Hardware Target: WASDPad+ Rev 1.5 — Engineering Validation / Pre-Prototype**
