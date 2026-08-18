# WASDPad+ Project Specification

**Document Version:** 1.1  
**Project:** WASDPad+  
**Current Hardware Revision:** Rev 1.5  
**Status:** Engineering Specification  
**Last Updated:** 2026-08-18

---

# 1. Purpose

This document defines the high-level technical and functional requirements of the **WASDPad+ controller platform**.

It covers:

- project objectives
- supported interface model
- functional requirements
- electrical requirements
- mechanical requirements
- current Rev 1.5 requirements
- validation requirements
- revision strategy
- future platform requirements

This is a **project-level specification**.

Revision-specific implementation details are maintained separately.

Current Rev 1.5 implementation documentation:

```text
hardware/rev1.5/README.md
hardware/rev1.5/bom/
docs/architecture/System_architecture.md
```

---

# 2. Project Objective

WASDPad+ is a custom gaming controller platform designed primarily for classic computers using Atari-style DE-9 / DB9 joystick interfaces.

The primary design objective is to provide a keyboard-like WASD control layout while preserving the electrical behaviour expected from a conventional joystick.

The project emphasizes:

- low and deterministic input latency
- direct hardware signalling
- retro-system compatibility
- reliable FIRE controls
- hardware autofire
- replaceable mechanical switches
- host-system protection
- serviceability
- reproducible manufacturing
- documented validation procedures

---

# 3. Current Project State

The current development platform is:

**WASDPad+ Hardware Revision 1.5**

Current state:

```text
Architecture:          Defined
Component Selection:   Complete
BOM:                   Pre-Release Validated
Schematic:             Engineering Review
PCB Layout:            Engineering Review
Prototype:             Pending
Production Validation: Pending
```

Rev 1.5 remains in:

**Engineering Validation / Pre-Prototype**

It shall not be considered production-approved until a complete Rev 1.5 prototype has passed electrical, functional and mechanical validation.

---

# 4. Revision Scope

The WASDPad+ project currently separates functionality into two architectural generations.

## 4.1 Rev 1.x Platform

The Rev 1.x platform is hardware-only.

Rev 1.5 uses:

- passive components
- CMOS timer logic
- CMOS analog switching
- discrete MOSFETs
- discrete transistors
- mechanical switches

It contains no programmable controller.

---

## 4.2 Future Rev 2.0 Platform

Rev 2.0 is planned as a programmable platform.

Potential features include:

- microcontroller-based control
- firmware-controlled autofire
- adjustable autofire rate
- burst mode
- configurable debounce
- game profiles
- persistent configuration
- USB firmware update
- optional USB HID support
- programmable LED indication

These are **future requirements** and shall not be interpreted as Rev 1.5 functionality.

---

# 5. Target Platforms

## 5.1 Primary Targets

The primary Rev 1.5 development targets are:

- Commodore 64
- Commodore 128
- Commodore Amiga

These systems use joystick interfaces compatible with the fundamental Atari-style active-low control model.

---

## 5.2 Secondary Compatibility

Other systems using a physically similar DE-9 joystick connector may be compatible.

Possible examples include:

- Atari 8-bit systems
- Atari ST
- VIC-20
- Commodore Plus/4
- Commodore 16 / 116
- other Atari-compatible joystick interfaces

Compatibility shall **not** be assumed solely from connector shape.

Electrical compatibility must be evaluated before a platform is formally declared supported.

---

## 5.3 Adapter-Dependent Systems

Systems requiring:

- pin remapping
- signal conversion
- voltage conversion
- connector conversion

shall be considered **adapter-dependent** rather than natively supported.

Adapter compatibility must be documented separately.

---

# 6. External Interface

Rev 1.5 uses a female DE-9 / DB9 controller connection.

Primary interface assignment:

| DB9 Pin | Function |
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

DB9 numbering is the authoritative electrical reference.

Wire colour is not part of the electrical interface specification.

---

# 7. Electrical Interface Model

Primary joystick controls shall use the conventional active-low signalling model.

Conceptually:

```text
Released -> signal inactive
Pressed  -> signal pulled active toward GND
```

The controller shall not require a serial protocol, host driver or software interpretation for normal joystick operation.

---

# 8. Directional Controls

The controller shall provide four independent directional inputs:

- UP
- DOWN
- LEFT
- RIGHT

Each direction shall have an independent electrical signal path.

Rev 1.5 shall not use:

- keyboard matrix scanning
- firmware key scanning
- software-generated direction signals

Simultaneous electrical activation of multiple independent directions may occur when multiple physical switches are pressed.

The controller shall not create unintended additional direction signals beyond those physically commanded.

Game-specific handling of opposing or simultaneous directions is outside the basic Rev 1.5 hardware specification.

---

# 9. Gameplay Switches

Rev 1.5 shall use MX-compatible mechanical gameplay switches.

Primary switch:

**Gateron KS-8 Yellow**

Primary socket:

**Kailh / Kaihua CPG151101S11**

Eight hot-swap sockets are used.

The hot-swap architecture shall allow compatible switches to be replaced without PCB soldering.

Mechanical compatibility must include:

- contact geometry
- socket engagement
- switch height
- enclosure clearance

---

# 10. FIRE Controls

The controller shall provide two independent FIRE functions.

## FIRE1

FIRE1 shall support:

- normal manual operation
- hardware autofire

Primary host connection:

```text
DB9 pin 6
```

## FIRE2

FIRE2 shall remain independently available as a manual input.

Primary Rev 1.5 host connection:

```text
DB9 pin 9 / POTX
```

FIRE1 and FIRE2 shall **not** be specified as electrically identical because their host-side functions differ.

---

# 11. FIRE Isolation

FIRE switching shall reproduce the electrical behaviour expected by the host joystick interface without directly exposing internal logic outputs to the host signal line.

Rev 1.5 uses discrete MOSFET stages for FIRE-related switching.

The design shall prevent internal autofire logic from forcing unintended FIRE states.

---

# 12. Autofire Requirement

Rev 1.5 shall provide hardware-generated autofire for FIRE1.

The autofire generator shall:

- require no firmware
- operate from the controller supply
- support OFF / ON selection
- support two fixed speed settings
- preserve manual FIRE operation when autofire is disabled

Primary oscillator:

**Renesas ICM7555CBAZ**

---

# 13. Autofire Timing

Rev 1.5 uses two fixed autofire timing selections.

Final validated timing resistors:

| Mode | Resistance |
|---|---:|
| FAST | 330 kΩ |
| SLOW | 680 kΩ |

References:

```text
R13 = 330 kΩ -> FAST
R14 = 680 kΩ -> SLOW
```

These values were selected through physical gameplay testing.

They are considered functional Rev 1.5 values and shall not be changed as normal procurement substitutions.

---

# 14. Autofire Controls

Rev 1.5 shall provide two independent user controls.

## Autofire Enable

```text
OFF
ON
```

## Autofire Speed

```text
SLOW
FAST
```

Validated physical speed-selector behaviour:

```text
LEFT  -> SLOW
RIGHT -> FAST
```

The physical switch implementation shall match the validated PCB orientation.

---

# 15. Autofire Logic

Rev 1.5 autofire control uses hardware logic based on:

- ICM7555 CMOS timer
- CD4066 CMOS bilateral switch
- discrete transistor/MOSFET circuitry
- passive timing components

No processor is present.

The term **processing subsystem** shall therefore not be used to describe Rev 1.5.

---

# 16. Autofire OFF Behaviour

When autofire is disabled:

- automatic FIRE pulses shall not reach the FIRE1 output
- FIRE1 shall remain available for normal manual use
- FIRE1 shall not remain unintentionally asserted
- the FIRE output shall not be left in an undefined state

This is a mandatory functional requirement.

---

# 17. Power Requirements

Rev 1.5 receives operating power from the host joystick port.

Primary supply:

```text
DB9 pin 7 -> +5 V
DB9 pin 8 -> GND
```

The controller shall minimize supply-current demand.

Low-power CMOS logic is preferred where practical.

---

# 18. Overcurrent Protection

Rev 1.5 shall include resettable overcurrent protection on the incoming +5 V rail.

Primary device:

**Littelfuse 1206L005/30WR**

Nominal characteristics:

```text
Hold current: 50 mA
Trip current: 150 mA
Maximum voltage: 30 V
```

The current class shall not be increased without engineering review.

The protection strategy is intended to reduce risk to the host joystick port during controller faults.

---

# 19. ESD Protection

Rev 1.5 shall include ESD protection on externally accessible electrical interfaces.

## Signal Protection

Primary device:

**Nexperia PESD5V0S4UD**

Used for external joystick signal protection.

## Supply Protection

Primary device:

**Nexperia PESD6V0L2UU**

Validated Rev 1.5 connection:

```text
Pin 1 -> protected +5 V
Pin 2 -> NC
Pin 3 -> GND
```

Protection-device topology and pinout must be checked against the manufacturer datasheet before production approval.

---

# 20. Supply Decoupling

Rev 1.5 shall include local supply decoupling.

Primary decoupling value:

```text
100 nF X7R
```

The decoupling capacitor shall be placed close to the relevant active circuitry.

Supply decoupling does not replace correct PCB power routing.

---

# 21. Power Indicator

Rev 1.5 shall provide a dedicated power indicator LED.

D1 shall use a 3 mm THT LED.

Supported product variants:

- Red
- Blue
- White

The selected colour does not alter controller functionality.

---

# 22. Autofire Status Indicator

Rev 1.5 shall provide visual autofire status indication using a dual-colour LED.

Primary device:

**Bivar 3BC-3-F**

Configuration:

**Common Cathode**

Validated pinout:

```text
Pin 1 -> RED anode
Pin 2 -> Common cathode -> GND
Pin 3 -> GREEN anode
```

The LED channels shall be independently driven.

Common-anode versions are not drop-in replacements for the current Rev 1.5 topology.

---

# 23. LED Driver Requirement

The dual-colour LED is driven by discrete transistor stages.

Primary transistor family:

**MMBT3904**

Validated pin mapping:

```text
Pin 1 = Base
Pin 2 = Emitter
Pin 3 = Collector
```

The manufacturer device, KiCad symbol and PCB footprint shall use consistent pin numbering.

---

# 24. Controller Cable

Rev 1.5 uses a molded DB9 female cable with flying leads.

The cable may be sourced as a generic Sega Mega Drive / Genesis 2 style replacement cable where electrically and mechanically suitable.

The cable shall be soldered directly to PCB pads.

Cable wire colours shall not be treated as a controlled specification.

---

# 25. Cable Batch Verification

The first cable from every new supplier or manufacturing batch shall undergo continuity testing.

All DB9 pins shall be mapped to the corresponding conductors.

Special attention shall be given to:

```text
DB9 pin 7 -> +5 V
DB9 pin 8 -> GND
```

Production assembly shall not begin until the cable batch has been validated.

Detailed procedure:

```text
docs/assembly/CABLE_ASSEMBLY.md
```

---

# 26. Mechanical Requirements

Rev 1.5 mechanical design shall accommodate:

- eight MX-compatible gameplay switches
- eight Kailh hot-swap sockets
- two autofire toggle switches
- one power LED
- one dual-colour status LED
- controller PCB
- DB9 cable exit
- cable strain relief
- PCB mounting
- enclosure clearances

The enclosure shall allow switches to operate without mechanical interference.

---

# 27. Serviceability Requirements

Rev 1.5 should allow normal wear components to be replaced with minimal soldering.

The primary serviceable components are the gameplay switches.

Hot-swap sockets shall allow these switches to be removed and replaced without PCB soldering.

Cable, PCB and toggle-switch replacement may require disassembly and soldering.

---

# 28. Latency Requirement

Rev 1.5 shall not introduce intentional software or firmware latency.

Input propagation is determined by:

- mechanical switch behaviour
- passive circuitry
- discrete switching
- CMOS logic propagation

There is no firmware polling interval.

---

# 29. Firmware Requirements

## Rev 1.5

There are **no firmware requirements** for Rev 1.5.

Rev 1.5 shall operate fully without:

- firmware
- microcontroller
- bootloader
- configuration software
- USB update process

---

## Future Rev 2.0

Potential firmware requirements for Rev 2.0 may include:

- adjustable autofire
- burst mode
- configurable debounce
- profile storage
- game-specific profiles
- configuration persistence
- USB firmware update
- programmable status indication

These remain future requirements and are not part of Rev 1.5 acceptance criteria.

---

# 30. Software Architecture

Rev 1.5 contains no software architecture.

Any future software architecture shall belong to a programmable hardware revision such as Rev 2.0.

Potential future layers may include:

```text
Hardware Abstraction
        |
Input Processing
        |
Configuration / Profiles
        |
Output Control
        |
USB / Configuration Interface
```

This model is conceptual only and does not describe Rev 1.5.

---

# 31. Safety and Host Protection Requirements

The controller shall be designed to minimize the risk of damaging the connected host.

Before connection to a host computer, an assembled controller shall be checked for:

- +5 V-to-GND short circuits
- incorrect DB9 cable wiring
- reversed supply wiring
- solder bridges
- incorrect semiconductor orientation
- incorrect protection-device pinout

A clean schematic ERC or PCB DRC result does not replace electrical inspection.

---

# 32. PCB Design Requirements

The final PCB shall satisfy:

- correct component footprints
- correct pin mappings
- suitable trace widths
- appropriate power routing
- appropriate ground routing
- short ESD return paths
- practical component placement
- enclosure clearance
- switch alignment
- cable solder-pad accessibility

ESD protection should be positioned so that externally introduced transients are diverted before propagating deeply into the controller circuitry.

---

# 33. Schematic Validation Requirements

Before production release:

- ERC shall pass
- all symbols shall have correct footprints
- semiconductor pinouts shall be checked
- LED polarity shall be checked
- protection-device topology shall be checked
- unused IC sections/pins shall be handled correctly
- power rails shall be verified
- component values shall match the approved BOM

Critical Rev 1.5 checks include:

```text
D6 PESD6V0L2UU pinout/topology
D7 Bivar 3BC-3-F common-cathode pinout
MMBT3904 B/E/C mapping
2N7002 G/S/D mapping
R13 = 330 kΩ
R14 = 680 kΩ
```

---

# 34. PCB Validation Requirements

Before manufacturing:

- DRC shall pass
- footprint orientation shall be reviewed
- connector and switch orientation shall be reviewed
- ESD placement shall be reviewed
- +5 V and GND routing shall be reviewed
- hot-swap socket geometry shall be reviewed
- LED orientation shall be reviewed
- enclosure/mechanical clearances shall be reviewed

Automated DRC is necessary but not sufficient for production approval.

---

# 35. Prototype Validation Requirements

The first complete Rev 1.5 prototype shall be tested before production approval.

Required functional tests:

- UP
- DOWN
- LEFT
- RIGHT
- FIRE1
- FIRE2
- autofire OFF
- autofire SLOW
- autofire FAST
- power indication
- dual-colour status indication

Required electrical tests:

- +5 V-to-GND resistance before power-up
- supply voltage
- controller current consumption
- DB9 continuity
- absence of unintended shorts

Required mechanical tests:

- all eight hot-swap sockets
- switch retention
- toggle-switch direction
- cable strain relief
- enclosure clearance

---

# 36. Production Test Requirement

A repeatable production-test procedure shall be created before Rev 1.5 production approval.

Planned document:

```text
docs/testing/PRODUCTION_TEST.md
```

The procedure shall define:

- pre-power resistance tests
- cable verification
- supply tests
- direction tests
- FIRE tests
- autofire tests
- LED tests
- final inspection

---

# 37. Manufacturing Requirements

The design should use components that are:

- actively manufactured where practical
- available from reputable distributors
- mechanically standardized
- replaceable with documented alternatives where appropriate

Protection devices and core semiconductors should not depend on unverified marketplace sourcing.

Mechanical commodity items may use marketplace sourcing when appropriate batch verification exists.

---

# 38. Component Substitution

Primary component selection is defined by the Rev 1.5 BOM.

Approved substitution strategy:

```text
hardware/rev1.5/bom/ALTERNATE_PARTS.md
```

Procurement guidance:

```text
hardware/rev1.5/bom/PROCUREMENT_NOTES.md
```

A substitute requiring a different:

- footprint
- pinout
- polarity
- topology
- mechanical geometry

shall be treated as an engineering change rather than a normal procurement substitution.

---

# 39. Documentation Requirements

Project documentation shall remain separated by purpose.

Current structure:

```text
docs/
├── README.md
├── architecture/
│   └── System_architecture.md
├── specification/
│   ├── PROJECT_SPECIFICATION.md
│   └── FEATURE_SPECIFICATION.md
└── assembly/
    └── CABLE_ASSEMBLY.md

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

Future production documentation may add:

```text
docs/testing/
docs/mechanical/
```

---

# 40. Revision Strategy

## Rev 1.2

Role:

**Validated predecessor architecture**

Rev 1.2 established the functional hardware basis from which Rev 1.5 evolved.

---

## Rev 1.5

Role:

**Protected and serviceable hardware-only platform**

Primary improvements:

- PPTC protection
- ESD protection
- MX hot-swap
- standardized switch selection
- improved autofire differentiation
- dual-colour status indication
- standardized BOM
- manufacturing documentation

Current status:

**Engineering Validation / Pre-Prototype**

---

## Rev 2.0

Role:

**Future programmable platform**

Expected to introduce functionality that fundamentally changes the architecture, potentially including firmware and microcontroller-based control.

Rev 2.0 development shall remain separate from Rev 1.5 production validation.

---

# 41. Change-Control Requirements

A documentation-only correction does not require a hardware revision change.

A hardware revision shall be considered when a change affects:

- PCB connectivity
- component topology
- physical PCB geometry
- connector mapping
- switch placement
- host electrical behaviour
- major mechanical compatibility

Component substitutions that remain within an explicitly approved alternate specification do not necessarily require a hardware revision.

---

# 42. Rev 1.5 Release Criteria

Rev 1.5 may be declared production validated only after:

1. component selection is complete
2. BOM is approved
3. schematic review is complete
4. ERC passes
5. PCB review is complete
6. DRC passes
7. first Rev 1.5 PCB is manufactured
8. complete controller is assembled
9. electrical validation passes
10. functional validation passes
11. mechanical validation passes
12. cable assembly procedure is validated
13. production test procedure is completed
14. manufacturing documentation is complete

Until these conditions are satisfied, the hardware remains:

**Engineering Validation**

---

# 43. Current Rev 1.5 Requirement Status

| Requirement Area | Status |
|---|---|
| Project architecture | Defined |
| Hardware-only operation | Defined |
| Direction architecture | Defined |
| FIRE1 / FIRE2 architecture | Defined |
| Autofire architecture | Defined |
| FAST / SLOW values | Physically Validated |
| Autofire switch behaviour | Physically Validated |
| MX hot-swap architecture | Defined |
| Default mechanical switch | Selected |
| PTC protection | Selected |
| Signal ESD protection | Selected |
| +5 V ESD pinout | Validated |
| Power LED strategy | Defined |
| Dual-colour LED | Validated |
| MMBT3904 mapping | Validated |
| Cable mapping | Validated |
| Cable batch procedure | Documented |
| BOM | Pre-Release Validated |
| Final schematic | Engineering Review |
| Final PCB | Engineering Review |
| Prototype | Pending |
| Production test procedure | Planned |
| Production approval | Pending |

---

# 44. Related Documents

Primary project documentation:

```text
README.md
docs/README.md
docs/architecture/System_architecture.md
docs/specification/FEATURE_SPECIFICATION.md
docs/assembly/CABLE_ASSEMBLY.md
hardware/rev1.5/README.md
hardware/rev1.5/bom/README.md
hardware/rev1.5/bom/wasdpad+v1.5.csv
hardware/rev1.5/bom/ALTERNATE_PARTS.md
hardware/rev1.5/bom/PROCUREMENT_NOTES.md
```

---

# 45. Document Versioning

Project specification versions are independent from hardware revisions.

Current state:

```text
Hardware Revision:      Rev 1.5
Project Specification:  v1.1
```

The project specification may evolve without requiring a PCB revision when changes only clarify requirements or future plans.

---

# 46. Version History

| Version | Date | Status | Changes |
|---|---|---|---|
| 1.0 | Not recorded | Draft | Initial project-level requirements; combined current hardware and future programmable concepts |
| **1.1** | **2026-08-18** | **Engineering Specification** | Restructured project-level requirements; separated Rev 1.5 hardware-only requirements from future Rev 2.0 firmware concepts; updated platform compatibility model, FIRE1/FIRE2 requirements, final autofire values, hot-swap architecture, PPTC/ESD protection, LED architecture, cable validation, manufacturing requirements and Rev 1.5 release criteria |

---

# 47. Next Version

The next specification revision should be created when a material project-level requirement changes.

The **Rev 1.5 production milestone does not automatically require PROJECT_SPECIFICATION v2.0**.

Minor validation/status updates may use:

```text
1.2
1.3
...
```

A major specification version increment should be reserved for a significant change in project requirements or architecture, such as formal adoption of the programmable Rev 2.0 platform.

---

**WASDPad+ Project Specification — Rev 1.5 current platform / Rev 2.0 future architecture**
