# WASDPad+ Rev 1.5

**Hardware Revision:** Rev 1.5  
**Document Version:** 0.9  
**Status:** Engineering Validation / Pre-Prototype  
**Last Updated:** 2026-08-19

---

## Overview

WASDPad+ Rev 1.5 is a hardware-only gaming controller designed primarily for classic computers using the Atari-style DE-9 joystick interface.

The controller combines keyboard-style mechanical switches with direct joystick signalling and hardware-generated autofire.

Rev 1.5 focuses on:

- low and deterministic input latency
- direct hardware signalling
- two-button operation
- hardware autofire
- MX-compatible hot-swap switches
- host-side electrical protection
- serviceability
- reproducible component selection

No microcontroller, firmware, driver or configuration software is required.

---

## Current Status

Rev 1.5 is currently in **Engineering Validation / Pre-Prototype**.

| Area | Status |
|---|---|
| Architecture | Complete |
| Feature specification | Current |
| Component selection | Complete |
| BOM | Pre-release validated |
| Autofire timing selection | Validated |
| Cable mapping | Validated |
| Schematic | Final engineering review |
| PCB | Final engineering review |
| Rev 1.5 prototype | Pending |
| Production validation | Pending |

The next major milestone is the manufacture and validation of the first complete Rev 1.5 prototype.

---

## Main Features

Rev 1.5 provides:

- UP
- DOWN
- LEFT
- RIGHT
- FIRE1
- FIRE2
- hardware autofire for FIRE1
- autofire OFF / ON control
- SLOW / FAST autofire selection
- dual-colour autofire status indication
- dedicated power LED
- eight MX-compatible hot-swap switch positions
- resettable +5 V overcurrent protection
- ESD protection
- direct DE-9 controller connection

---

## Control Architecture

The directional controls use independent electrical paths:

```text
UP
DOWN
LEFT
RIGHT
```

Rev 1.5 does not use firmware scanning, keyboard-matrix scanning or software-generated joystick signals.

Multiple physical directions may therefore be activated simultaneously.

No SOCD filtering is implemented.

---

## FIRE Controls

### FIRE1

FIRE1 is the primary action button.

```text
DE-9 pin 6
```

It supports:

- normal manual operation
- hardware autofire

With autofire disabled, FIRE1 behaves as a conventional joystick fire button.

### FIRE2

FIRE2 is an independent secondary action button.

```text
DE-9 pin 9 / POTX
```

Rev 1.5 does not apply autofire to FIRE2.

FIRE2 support depends on the connected host system and software.

---

## Hardware Autofire

Autofire is implemented entirely in hardware.

The main circuit uses:

- Renesas ICM7555 CMOS timer
- Texas Instruments CD4066B analog switch
- discrete MOSFET/transistor stages
- passive timing components

There are two separate physical controls:

```text
AUTO:
OFF / ON

SPEED:
SLOW / FAST
```

The final Rev 1.5 timing resistors are:

| Mode | Component | Value |
|---|---|---:|
| FAST | R13 | 330 kΩ |
| SLOW | R14 | 680 kΩ |

These values were selected through physical gameplay testing.

Validated speed-selector orientation:

```text
LEFT  -> SLOW
RIGHT -> FAST
```

The 330 kΩ and 680 kΩ values are functional design values and should not be changed as ordinary procurement substitutions.

---

## Mechanical Switch System

Rev 1.5 uses eight MX-compatible hot-swap gameplay switches.

### Default Switch

**Gateron KS-8 Yellow**

### Hot-Swap Socket

**Kailh / Kaihua CPG151101S11**

The hot-swap system allows gameplay switches to be replaced without soldering them directly to the PCB.

Other MX-compatible switches may be used when their electrical and mechanical compatibility is confirmed.

---

## Power

The controller is powered from the host joystick port:

```text
DE-9 pin 7 -> +5 V
DE-9 pin 8 -> GND
```

Rev 1.5 is designed as a low-power hardware-only controller.

Local supply decoupling is provided around the active circuitry.

---

## Electrical Protection

Rev 1.5 includes protection for the controller and connected host interface.

### +5 V Overcurrent Protection

Primary device:

**Littelfuse 1206L005/30WR**

Nominal characteristics:

```text
Hold current:    50 mA
Trip current:   150 mA
Maximum voltage: 30 V
```

### Signal ESD Protection

Primary device:

**Nexperia PESD5V0S4UD**

### +5 V ESD Protection

Primary device:

**Nexperia PESD6V0L2UU**

The protection system is intended to reduce the risk of controller faults or external electrostatic events reaching sensitive host circuitry.

---

## Status Indication

Rev 1.5 uses two separate indicators.

### D1 — Power

D1 is a 3 mm THT power indicator LED.

Production variants may use:

- Red
- Blue
- White

depending on the requested controller configuration.

### D7 — Autofire Status

Primary component:

**Bivar 3BC-3-F**

Configuration:

**Common Cathode**

The dual-colour LED provides red/green indication for the autofire system.

The final user-visible colour/state behaviour shall be confirmed on the complete Rev 1.5 prototype.

---

## Controller Cable

Rev 1.5 uses a molded female DE-9 cable with flying leads soldered directly to the PCB.

The current cable is sourced as a Sega Mega Drive / Genesis 2 style replacement cable.

The physical cable contains more conductors than required by the Rev 1.5 implementation; unused conductors are not connected.

Wire colour is **not** considered an authoritative electrical reference because colour assignments may vary between suppliers or manufacturing batches.

DE-9 pin number is authoritative.

New cable batches should therefore be continuity-tested before assembly.

Cable assembly details are documented in:

```text
docs/assembly/CABLE_ASSEMBLY.md
```

---

## DE-9 Interface

Primary Rev 1.5 interface:

| Pin | Function |
|---:|---|
| 1 | UP |
| 2 | DOWN |
| 3 | LEFT |
| 4 | RIGHT |
| 5 | Auxiliary / unused by current Rev 1.5 cable assembly |
| 6 | FIRE1 |
| 7 | +5 V |
| 8 | GND |
| 9 | FIRE2 / POTX |

The connector shape alone does not guarantee compatibility with every system using a DE-9 connector.

Primary Rev 1.5 target platforms are:

- Commodore 64
- Commodore 128
- Commodore Amiga

Other Atari-style joystick systems may also be compatible, but should be electrically verified before being listed as officially supported.

---

## Primary Components

The main active and electromechanical components used by Rev 1.5 include:

| Function | Device |
|---|---|
| Autofire timer | Renesas ICM7555CBAZ |
| Analog switching | Texas Instruments CD4066BM |
| MOSFET switching | 2N7002 |
| LED driver | MMBT3904 |
| +5 V protection | Littelfuse 1206L005/30WR |
| Signal ESD | Nexperia PESD5V0S4UD |
| +5 V ESD | Nexperia PESD6V0L2UU |
| Dual-colour LED | Bivar 3BC-3-F |
| Hot-swap socket | Kailh / Kaihua CPG151101S11 |
| Default gameplay switch | Gateron KS-8 Yellow |

This table is an overview only.

The authoritative component list is:

```text
hardware/rev1.5/bom/wasdpad+v1.5.csv
```

---

## BOM and Procurement

Rev 1.5 component documentation is maintained under:

```text
hardware/rev1.5/bom/
├── README.md
├── wasdpad+v1.5.csv
├── ALTERNATE_PARTS.md
└── PROCUREMENT_NOTES.md
```

### `wasdpad+v1.5.csv`

The authoritative Rev 1.5 component list.

It contains the selected component values, quantities, footprints, manufacturer references and manufacturer part numbers.

### `ALTERNATE_PARTS.md`

Defines component substitution strategies where alternatives require explicit engineering consideration.

### `PROCUREMENT_NOTES.md`

Contains sourcing and procurement information that does not belong in the electrical design description.

---

## Critical Final Design Checks

Before the Rev 1.5 schematic and PCB are approved for manufacturing, several component mappings require explicit manual review in addition to normal ERC/DRC checks.

### D6 — PESD6V0L2UU

Verify the final:

- manufacturer datasheet
- schematic symbol
- net assignment
- footprint
- PCB pad numbering

against each other.

The currently validated schematic connection is:

```text
Pin 1 -> protected +5 V
Pin 2 -> NC
Pin 3 -> GND
```

### D7 — Dual-Colour LED

Verify the final Bivar device against:

- common-cathode configuration
- KiCad symbol
- red/green pin assignment
- physical footprint
- PCB pad numbering

These are design-release checks.

Once the PCB design has been validated, normal controller acceptance is based primarily on correct functional operation.

---

## Final Schematic / PCB Review

Before ordering the Rev 1.5 prototype:

- run final ERC
- run final DRC
- verify component orientations
- verify semiconductor pin mappings
- verify LED polarity and pinout
- verify protection-device pinouts
- verify DE-9 mapping
- verify +5 V and GND routing
- verify R13 = 330 kΩ
- verify R14 = 680 kΩ
- verify LEFT = SLOW / RIGHT = FAST
- verify hot-swap socket geometry
- visually inspect final manufacturing outputs

Automated ERC/DRC results do not replace the final manual design review.

---

## Prototype Validation

The first complete Rev 1.5 prototype shall verify the actual controller functions:

```text
Power indication

UP
DOWN
LEFT
RIGHT

FIRE1
FIRE2

Autofire OFF
Autofire SLOW
Autofire FAST

Autofire status indication
```

The prototype shall also confirm:

- all gameplay switches operate correctly
- hot-swap sockets operate correctly
- controller cable operates correctly
- enclosure and PCB are mechanically compatible
- extended gameplay operation is reliable

Successful functional validation is the primary acceptance criterion for Rev 1.5.

---

## Enclosure

The Rev 1.5 enclosure is designed and maintained separately by **Dester3D**.

Mechanical CAD, printable models and enclosure-specific manufacturing files are maintained under:

```text
enclosure/
```

The enclosure design will be validated against the final Rev 1.5 PCB and production components.

Electronic hardware documentation defines the required electrical and PCB interfaces; detailed enclosure design remains part of the Dester3D mechanical design.

---

## Firmware

Rev 1.5 uses **no firmware**.

The repository:

```text
firmware/
```

directory is reserved for future programmable WASDPad+ revisions.

Firmware-related functionality is not part of Rev 1.5.

---

## Current Development Path

```text
Architecture             COMPLETE
        |
Component selection      COMPLETE
        |
BOM                      COMPLETE
        |
Autofire values          VALIDATED
        |
Cable mapping            VALIDATED
        |
Final schematic audit    IN PROGRESS
        |
Final PCB audit          IN PROGRESS
        |
Rev 1.5 prototype
        |
Functional validation
        |
Rev 1.5 release
```

The current priority is completing the final schematic and PCB review before prototype manufacturing.

---

## Related Documentation

The Rev 1.5 documentation is intentionally kept compact.

### Project Documentation

```text
docs/
├── README.md
├── architecture/
│   └── System_architecture.md
├── assembly/
│   └── CABLE_ASSEMBLY.md
├── legal/
│   ├── LICENSES.md
│   └── TRADEMARKS.md
├── roadmap/
│   └── ROADMAP.md
└── specification/
    └── FEATURE_SPECIFICATION.md
```

### Rev 1.5 Component Documentation

```text
hardware/rev1.5/bom/
├── README.md
├── wasdpad+v1.5.csv
├── ALTERNATE_PARTS.md
└── PROCUREMENT_NOTES.md
```

The primary technical references are:

- `System_architecture.md` — controller architecture
- `FEATURE_SPECIFICATION.md` — functional behaviour and requirements
- `CABLE_ASSEMBLY.md` — controller cable wiring and assembly
- `ROADMAP.md` — development status and remaining milestones
- `wasdpad+v1.5.csv` — authoritative component list

Documentation should remain intentionally compact.

Information should be maintained in the most appropriate authoritative location rather than duplicated across multiple documents.

---

## Rev 2.0

Rev 2.0 is a future programmable WASDPad+ platform and is separate from the current Rev 1.5 development.

Potential concepts include:

- adjustable FAST autofire
- burst mode
- programmable behaviour
- configurable debounce
- profiles
- USB configuration/update
- multi-colour status indication

Rev 2.0 development shall not expand or delay the Rev 1.5 validation scope.

---

## Version History

| Version | Date | Changes |
|---|---|---|
| 0.1 | Not recorded | Initial Rev 1.5 documentation |
| 0.5 | Not recorded | Rev 1.5 development information expanded |
| **0.9** | **2026-08-19** | Consolidated Rev 1.5 hardware documentation; updated actual engineering status, final component selections, autofire values, hot-swap system, protection architecture, LED configuration and cable strategy; removed references to obsolete documentation and aligned all references with the current repository structure |

---

**WASDPad+ Rev 1.5 — Engineering Validation / Pre-Prototype**
