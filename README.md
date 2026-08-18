# WASDPad+

**Hardware WASD-style controller platform for Commodore 64, Amiga and Atari-compatible systems**

**Project Documentation Version:** 0.9  
**Current Hardware Revision:** Rev 1.5  
**Project Status:** Active Development / Rev 1.5 Engineering Validation  
**Last Updated:** 2026-08-18

---

## Overview

WASDPad+ is a custom hardware controller designed primarily for retro computers using the classic Atari-style DE-9 / DB9 joystick interface.

The project provides a keyboard-like WASD control layout while remaining electrically compatible with systems such as:

- Commodore 64
- Commodore 128
- Commodore Amiga
- Atari-compatible joystick interfaces
- other compatible active-low DE-9 controller ports

The design is entirely hardware-based.

No microcontroller, firmware, USB interface or software driver is required for normal controller operation.

The current development version is:

**WASDPad+ Hardware Revision 1.5**

Rev 1.5 focuses on improving electrical protection, serviceability, switch replacement, manufacturing consistency and status indication while retaining the proven hardware architecture of previous revisions.

---

# Main Features

WASDPad+ Rev 1.5 provides:

- WASD-style directional controls
- FIRE1 support
- FIRE2 / POTX support
- hardware autofire
- selectable autofire OFF / ON
- selectable SLOW / FAST autofire speed
- dual-colour autofire status indication
- dedicated power indicator LED
- MX-compatible mechanical switches
- Kailh hot-swap switch sockets
- Gateron KS-8 Yellow switches as the default switch configuration
- resettable +5 V overcurrent protection
- ESD protection on externally accessible signals
- protected +5 V input
- direct DB9 controller cable connection
- no firmware requirement
- no microcontroller dependency

---

# Design Philosophy

The WASDPad+ project follows several basic design principles.

## Native Retro Hardware Interface

The controller connects directly to the target computer's joystick port.

No protocol conversion is required.

---

## Hardware-Only Operation

Normal controller operation does not depend on:

- firmware
- operating-system drivers
- USB
- programmable microcontrollers
- software configuration

This keeps the signal path deterministic and suitable for latency-sensitive retro gaming.

---

## Serviceability

Revision 1.5 introduces MX hot-swap sockets so the primary gameplay switches can be replaced without soldering.

This allows the user to experiment with different MX-compatible mechanical switches and makes worn switches easy to replace.

---

## Electrical Protection

Rev 1.5 introduces dedicated protection for both the host computer and controller electronics.

Protection includes:

- resettable PPTC protection on the +5 V supply
- ESD protection on joystick signal lines
- ESD protection on the incoming +5 V rail
- supply decoupling

These additions are particularly important because the controller is powered directly from the host computer's joystick port.

---

# Current Hardware Revision

## WASDPad+ Rev 1.5

Revision 1.5 is the current engineering revision.

Its main development goals are:

- improved electrical protection
- improved manufacturing repeatability
- MX hot-swap support
- standardized component sourcing
- improved autofire speed differentiation
- dual-colour autofire indication
- documented cable assembly
- production-oriented BOM
- improved hardware validation procedures

The fundamental joystick interface and hardware-only architecture remain compatible with the previous validated design.

---

# Autofire

Rev 1.5 contains a hardware autofire generator based on a CMOS 555 timer.

Primary timer:

**Renesas ICM7555CBAZ**

Two fixed autofire rates are available.

| Mode | Timing Resistance |
|---|---:|
| FAST | 330 kΩ |
| SLOW | 680 kΩ |

The current physical switch behaviour is:

```text
LEFT  -> SLOW
RIGHT -> FAST
```

The final resistor values were selected through physical gameplay testing.

The SLOW mode provides a clearly distinguishable lower firing rate compared with FAST.

---

# Status Indication

## Power LED

The controller contains a dedicated 3 mm power LED.

The production configuration may use:

- Red
- Blue
- White

depending on the requested controller configuration.

---

## Autofire Status LED

Rev 1.5 uses a dual-colour 3 mm LED:

**Bivar 3BC-3-F**

Configuration:

**Common Cathode**

The two LED channels are independently driven and indicate autofire operating state/speed.

The selected LED pinout and driver transistor mapping have been verified against the component datasheets and KiCad footprints.

---

# Mechanical Switches

The default Rev 1.5 gameplay switch is:

**Gateron KS-8 Yellow**

Eight switches are used per controller.

The switches are installed into:

**Kailh CPG151101S11 MX hot-swap sockets**

This allows compatible MX-style switches to be replaced without soldering.

Other compatible switches may be supported where mechanical and electrical compatibility has been verified.

---

# Electrical Protection

## Overcurrent Protection

The +5 V supply uses a resettable PPTC:

**Littelfuse 1206L005/30WR**

Nominal characteristics:

- 50 mA hold current
- 150 mA trip current
- 30 V maximum voltage
- 1206 package

The selection takes the limited current capability of classic joystick ports into account.

---

## Signal ESD Protection

Joystick signal protection is provided by:

**Nexperia PESD5V0S4UD**

These devices protect externally accessible controller signal lines.

---

## +5 V ESD Protection

The protected +5 V rail uses:

**Nexperia PESD6V0L2UU**

The Rev 1.5 implementation uses one protection channel:

```text
Pin 1 -> protected +5 V rail
Pin 2 -> NC
Pin 3 -> GND
```

The device topology and pin mapping have been verified against the manufacturer datasheet.

---

# Controller Cable

Rev 1.5 currently uses a generic molded DB9 female controller cable with flying leads.

The validated supplier cable is sold as a Sega Mega Drive / Genesis 2 style replacement controller cable.

The cable is soldered directly to the PCB.

Detailed wiring and production verification instructions are documented in:

```text
docs/assembly/CABLE_ASSEMBLY.md
```

## Important Manufacturing Rule

Wire colours must **not** be assumed to remain identical between supplier batches.

The first cable from every new batch must undergo a complete DB9 pin-to-wire continuity test before production assembly begins.

Special attention must be paid to:

```text
DB9 pin 7 -> +5 V
DB9 pin 8 -> GND
```

An incorrect power-wire assignment may damage the controller or connected host computer.

---

# Repository Structure

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
│   └── assembly/
│       └── CABLE_ASSEMBLY.md
│
├── hardware/
│   │
│   └── rev1.5/
│       ├── README.md
│       │
│       ├── bom/
│       │   ├── README.md
│       │   ├── BOM.csv
│       │   ├── ALTERNATE_PARTS.md
│       │   └── PROCUREMENT_NOTES.md
│       │
│       ├── schematic/
│       │
│       └── pcb/
│
└── ...
```

The exact directory structure may evolve as manufacturing and release documentation is added.

---

# Documentation

## Rev 1.5 BOM

Component-selection documentation is located in:

```text
hardware/rev1.5/bom/
```

The BOM documentation contains:

- primary component selection
- manufacturer part numbers
- footprints
- datasheets
- approved alternates
- procurement notes
- component validation status

The Rev 1.5 BOM component-selection phase is currently considered:

**Pre-Release Validated**

---

## Cable Assembly

Cable assembly documentation is located in:

```text
docs/assembly/CABLE_ASSEMBLY.md
```

It contains:

- DB9 pin assignments
- validated wire-colour mapping
- J1 pad mapping
- unused conductor handling
- mandatory new-batch continuity testing
- final assembly verification

---

# Rev 1.5 Development Status

| Area | Status |
|---|---|
| Electrical architecture | ✅ Defined |
| Component selection | ✅ Complete |
| Rev 1.5 BOM | ✅ Pre-Release Validated |
| Autofire resistor values | ✅ Physically Validated |
| D6 ESD topology/pinout | ✅ Validated |
| D7 dual-colour LED pinout | ✅ Validated |
| Q1/Q2 transistor pinout | ✅ Validated |
| Hot-swap architecture | ✅ Defined |
| Controller cable mapping | ✅ Validated |
| Cable manufacturing procedure | ✅ Documented |
| Schematic | 🚧 Engineering Review |
| PCB layout | 🚧 Engineering Review |
| Rev 1.5 prototype | ⏳ Pending |
| Full functional validation | ⏳ Pending |
| Production release | ⏳ Pending |

---

# Current Development Focus

The primary component-selection phase for Rev 1.5 has been completed.

Current development work is focused on:

1. final Rev 1.5 schematic review
2. final symbol / footprint / pinout verification
3. PCB layout review
4. ERC and DRC validation
5. first Rev 1.5 prototype manufacturing
6. prototype electrical testing
7. gameplay validation
8. manufacturing documentation
9. production release preparation

---

# Pre-Production Validation

Before Rev 1.5 can be considered production-ready, the following validation must be completed.

## Electrical

- verify +5 V and GND resistance before power-up
- verify protected +5 V rail
- verify controller supply current
- verify FIRE1
- verify FIRE2
- verify UP
- verify DOWN
- verify LEFT
- verify RIGHT
- verify autofire OFF
- verify autofire SLOW
- verify autofire FAST
- verify power LED
- verify dual-colour autofire indication

## Design

- KiCad ERC passes
- KiCad PCB DRC passes
- all symbol-to-footprint mappings verified
- protection-device pinouts verified
- DB9 cable mapping verified
- no unintended +5 V / GND short circuit

## Mechanical

- all eight MX switches operate correctly
- all hot-swap sockets retain switches correctly
- toggle switches operate in the intended direction
- cable strain relief is adequate
- enclosure clearance is verified

---

# Known Assembly Considerations

## Solder Paste Under Fine-Pitch / SOIC Components

During prototype debugging, incompletely reflowed solder paste beneath the ICM7555 package caused an unintended low-resistance path between the supply rails.

After assembly:

- inspect U1 carefully
- remove excess solder paste and flux
- check +5 V-to-GND resistance before power-up
- do not assume a visually aligned IC is electrically correct

This check should form part of the Rev 1.5 production test procedure.

---

# Compatibility

The WASDPad+ electrical interface is intended for systems using the classic Atari-style joystick interface.

Primary development targets include:

- Commodore 64
- Commodore 128
- Commodore Amiga

Compatibility with other systems using similar DE-9 interfaces must be evaluated individually because pin usage and electrical behaviour may differ between platforms.

In particular, FIRE2 / POTX behaviour is system-dependent.

---

# Project Status

WASDPad+ is currently an active hardware-development project.

Rev 1.5 has completed its primary component-selection and BOM phase.

The project is now transitioning from component selection into:

**final design verification and prototype validation.**

Rev 1.5 shall not be considered production-approved until a complete Rev 1.5 prototype has been manufactured and successfully passed the documented validation procedure.

---

# Documentation Versioning

Documentation versions are independent from PCB hardware revisions.

For example:

```text
Hardware Revision: Rev 1.5
README Version:    0.9
BOM README:        0.9
```

Documentation-only corrections do not require a hardware revision increment.

A hardware revision shall only change when the electrical or physical PCB design changes in a way that affects manufactured hardware.

---

# Version History

| Documentation Version | Date | Project State | Changes |
|---|---|---|---|
| 0.1 | Not recorded | Initial | Initial repository documentation |
| 0.5 | Not recorded | Development | Rev 1.5 development structure and initial BOM work |
| 0.8 | Not recorded | Engineering | Rev 1.5 protection, hot-swap and autofire development |
| **0.9** | **2026-08-18** | **Engineering Validation** | Updated repository to current Rev 1.5 status; component selection completed; BOM pre-release validated; final autofire values documented; D6/D7/Q1/Q2 validation recorded; Gateron/Kailh switch architecture documented; DB9 cable assembly and batch-verification procedure added |

---

# Next Documentation Release

The next planned root documentation version is:

**README v1.0**

Target milestone:

**WASDPad+ Rev 1.5 prototype successfully manufactured and fully validated.**

At that point the Rev 1.5 documentation may transition from:

```text
Pre-Release / Engineering Validation
```

to:

```text
Production Validated
```

provided that all schematic, PCB, electrical, mechanical and functional validation requirements have passed.

---

# License

See the repository `LICENSE` file for licensing terms.

---

**WASDPad+ Rev 1.5 — Hardware controller development project**
