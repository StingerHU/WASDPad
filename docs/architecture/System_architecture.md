# WASDPad+ System Architecture

**Document Version:** 0.9
**Hardware Revision:** Rev 1.5
**Status:** Engineering Validation / Pre-Prototype
**Last Updated:** 2026-08-18

---

# 1. Purpose

This document describes the system-level hardware architecture of **WASDPad+ Revision 1.5**.

It defines:

* major functional blocks
* signal flow
* power architecture
* input architecture
* FIRE1 and FIRE2 handling
* autofire architecture
* protection strategy
* status indication
* external controller interface
* architectural boundaries between Rev 1.5 and future revisions

Exact manufacturer part numbers and procurement information are maintained separately in:

```text
hardware/rev1.5/bom/
```

---

# 2. Architectural Principles

WASDPad+ Rev 1.5 follows five primary design principles.

## 2.1 Hardware-Only Operation

Normal controller operation requires:

* no microcontroller
* no firmware
* no operating-system driver
* no USB interface
* no programmable logic

Direction, FIRE and autofire functions are implemented entirely in hardware.

This provides deterministic behaviour and keeps the controller compatible with classic joystick interfaces without software dependencies.

---

## 2.2 Native Joystick-Port Interface

The controller connects directly to a classic Atari-style DE-9 / DB9 joystick port.

Primary target platforms are:

* Commodore 64
* Commodore 128
* Commodore Amiga

Compatibility with other DE-9 systems must be evaluated individually because electrical behaviour and use of auxiliary pins may differ.

---

## 2.3 Active-Low Signal Behaviour

The primary joystick inputs operate using the conventional active-low model.

Conceptually:

```text
Released input -> signal inactive
Pressed input  -> signal pulled active toward GND
```

The controller therefore behaves electrically like a conventional joystick rather than generating a digital communication protocol.

---

## 2.4 Host Protection

Rev 1.5 includes dedicated protection against:

* excessive +5 V current
* electrostatic discharge on external signal lines
* electrostatic discharge on the +5 V supply
* local supply transients

Protection is considered part of the core architecture rather than an optional accessory.

---

## 2.5 Serviceability

Primary gameplay switches use MX-compatible hot-swap sockets.

This allows mechanical switches to be replaced without soldering and separates the lifetime of the PCB from the lifetime or user preference of the individual switches.

---

# 3. System Block Diagram

```text
                         HOST COMPUTER
                              |
                       DE-9 / DB9 PORT
                              |
             +----------------+----------------+
             |                                 |
             |                              +5 V
             |                                 |
             |                          PPTC Protection
             |                                 |
             |                         +5 V ESD Protection
             |                                 |
             |                           Protected +5 V
             |                                 |
             |                 +---------------+---------------+
             |                 |               |               |
             |                 v               v               v
             |           Autofire Logic    LED Drivers     Supply Rails
             |           ICM7555 + CD4066      |               |
             |                 |               |               |
             |                 |               v               |
             |                 |          Status LEDs           |
             |                 |                               |
             v                 v                               |
      Signal ESD Protection    |                               |
             |                 |                               |
             v                 |                               |
       Direction / FIRE <------+                               |
             ^                                                 |
             |                                                 |
       MX Hot-Swap Inputs                                      |
                                                               |
                              GND ------------------------------+
```

The diagram represents functional relationships rather than physical PCB placement.

---

# 4. External Interface

The controller uses a 9-pin female DE-9 / DB9 cable connection.

The relevant controller interface includes:

| DB9 Pin | Function                                           |
| ------: | -------------------------------------------------- |
|       1 | UP                                                 |
|       2 | DOWN                                               |
|       3 | LEFT                                               |
|       4 | RIGHT                                              |
|       5 | Auxiliary / not used by the current cable assembly |
|       6 | FIRE1                                              |
|       7 | +5 V                                               |
|       8 | GND                                                |
|       9 | FIRE2 / POTX                                       |

The cable is soldered directly to PCB pads.

Detailed production wiring is maintained in:

```text
docs/assembly/CABLE_ASSEMBLY.md
```

Cable wire colours are **not** part of the electrical specification.

The first cable from every new supplier batch must be continuity-tested before production use.

---

# 5. Power Architecture

The controller receives its operating power from DB9 pin 7.

Conceptual power path:

```text
DB9 Pin 7
   |
   v
PPTC
   |
   v
Protected +5 V Rail
   |
   +----> +5 V ESD protection
   |
   +----> ICM7555
   |
   +----> CD4066
   |
   +----> LED circuitry
   |
   +----> supporting transistor / MOSFET logic
```

DB9 pin 8 provides the common ground reference.

---

# 6. Overcurrent Protection

Rev 1.5 introduces a resettable PPTC device in the incoming +5 V path.

Primary component:

**Littelfuse 1206L005/30WR**

Nominal characteristics:

```text
Hold current: 50 mA
Trip current: 150 mA
Maximum voltage: 30 V
Package: 1206
```

The relatively low hold-current class was intentionally selected because classic joystick ports have limited +5 V current capability.

The PPTC is intended to reduce the risk to the host computer in the event of a controller-side fault.

It does not replace correct assembly verification.

---

# 7. ESD Protection Architecture

Rev 1.5 provides separate ESD protection for signal lines and the power rail.

## 7.1 Signal-Line Protection

External joystick signals are protected using:

**Nexperia PESD5V0S4UD**

The devices provide multi-line ESD protection for externally accessible controller signals.

The protection components are positioned conceptually between:

```text
DB9 interface
      |
      v
ESD protection
      |
      v
internal controller circuitry
```

---

## 7.2 +5 V Protection

The +5 V rail uses:

**Nexperia PESD6V0L2UU**

Current validated schematic mapping:

```text
Pin 1 -> protected +5 V rail
Pin 2 -> NC
Pin 3 -> GND
```

Only one internal protection channel is required by the current implementation.

The topology and pin mapping have been verified against the manufacturer datasheet.

---

# 8. Supply Decoupling

Local supply decoupling is provided to reduce switching noise and stabilize the active circuitry.

A dedicated:

```text
100 nF X7R
```

decoupling capacitor is used across the +5 V and GND rails.

The decoupling capacitor associated with the active logic should be placed physically close to the relevant supply pins.

Additional capacitors are used in the timer and control networks.

---

# 9. User Input Architecture

Rev 1.5 contains eight primary gameplay switches.

These are installed using:

**Kailh / Kaihua CPG151101S11 MX hot-swap sockets**

Default mechanical switch:

**Gateron KS-8 Yellow**

The hot-swap architecture allows compatible MX-style switches to be replaced without soldering.

The electrical input architecture is independent of the mechanical switch feel.

Compatible linear, tactile or clicky switches may therefore be used where mechanical compatibility has been verified.

---

# 10. Directional Input Architecture

Four switches provide:

```text
UP
DOWN
LEFT
RIGHT
```

Each directional input ultimately controls the corresponding DB9 joystick signal.

The architecture intentionally avoids firmware-based scanning or matrix decoding.

Each direction therefore remains an independent hardware signal.

This is important for combinations such as simultaneous direction presses and for deterministic input behaviour.

---

# 11. FIRE Architecture

Rev 1.5 supports two FIRE functions.

```text
FIRE1 -> DB9 pin 6
FIRE2 -> DB9 pin 9 / POTX
```

FIRE1 supports both:

* direct manual firing
* hardware-generated autofire

FIRE2 remains independently available as a manual control.

The architecture does not require the host to understand any additional controller protocol.

---

# 12. MOSFET Signal Switching

2N7002 N-channel MOSFETs are used in FIRE/autofire signal handling.

Validated generic mapping:

```text
Pin 1 = Gate
Pin 2 = Source
Pin 3 = Drain
```

The MOSFET architecture allows the controller logic to manipulate FIRE signals while maintaining the required joystick-side electrical behaviour.

Manufacturer-specific pinout must be revalidated if the selected 2N7002 supplier changes.

---

# 13. Autofire Architecture

Autofire is generated entirely in hardware.

Primary functional blocks:

```text
Protected +5 V
     |
     v
ICM7555 oscillator
     |
     v
AF_CLK
     |
     v
CD4066 / control logic
     |
     v
FIRE1 switching stage
     |
     v
DB9 FIRE1
```

The primary oscillator device is:

**Renesas ICM7555CBAZ**

The CMOS implementation was selected to minimize supply-current demand compared with a traditional bipolar NE555.

---

# 14. Autofire Timing

Rev 1.5 provides two fixed autofire speeds.

Final timing resistors:

```text
FAST -> R13 = 330 kΩ
SLOW -> R14 = 680 kΩ
```

These values were selected through physical gameplay testing.

The objective is not merely to provide two electrically different frequencies, but to provide two settings that are clearly distinguishable during actual gameplay.

The physical speed-selector behaviour is:

```text
LEFT  -> SLOW
RIGHT -> FAST
```

These values and switch directions are considered part of the current Rev 1.5 behaviour and shall not be changed as normal BOM substitutions.

---

# 15. Autofire Enable Control

Autofire can be enabled or disabled independently of the speed selection.

The user therefore has two separate hardware controls:

```text
AUTO:
OFF / ON

SPEED:
SLOW / FAST
```

Both functions use physical toggle switches.

The current PCB/schematic mappings have been validated against the actual mechanical switch orientation.

Their KiCad footprint or symbol assignments should not be changed merely for naming consistency.

---

# 16. CD4066 Switching Logic

The autofire control architecture uses:

**Texas Instruments CD4066BM96**

The CD4066 provides four bilateral CMOS switch sections.

In Rev 1.5 it forms part of the autofire routing/control network.

Unused switch sections are handled explicitly in the schematic and must not be assumed to be arbitrary floating logic.

The device operates from the controller's protected supply rail.

---

# 17. Autofire OFF-State Behaviour

A key architectural requirement is that disabling autofire must restore predictable manual FIRE operation.

Conceptually:

```text
AUTOFIRE OFF
     |
     +----> oscillator influence removed/clamped
     |
     +----> manual FIRE1 remains available
```

Autofire logic must therefore never leave FIRE1 unintentionally asserted or floating when autofire is disabled.

---

# 18. Status Indication Architecture

Rev 1.5 uses two separate visual-indication systems:

```text
D1 -> Power indication
D7 -> Autofire status indication
```

They serve different purposes and should not be treated as a single generic RGB status system.

---

# 19. Power Indicator

D1 is a conventional 3 mm THT LED.

Its purpose is to indicate the presence of controller supply power.

The production LED colour may be selected as:

* Red
* Blue
* White

The selected colour is a product configuration option rather than a functional hardware revision.

---

# 20. Autofire Status Indicator

D7 is a 3 mm red/green dual-colour LED.

Primary component:

**Bivar 3BC-3-F**

Electrical configuration:

**Common Cathode**

Validated mapping:

```text
Pin 1 -> RED anode
Pin 2 -> Common cathode -> GND
Pin 3 -> GREEN anode
```

The two LED channels are controlled independently.

This allows the controller to provide visual differentiation of autofire operating state/speed without firmware.

---

# 21. LED Driver Architecture

D7 is driven using two MMBT3904 NPN transistor stages.

Validated transistor pin mapping:

```text
Pin 1 = Base
Pin 2 = Emitter
Pin 3 = Collector
```

The Rev 1.5 implementation uses the transistor stages as part of the LED status-driving network.

The schematic, transistor pinout and PCB footprint must remain mutually consistent.

---

# 22. Cable Architecture

The current Rev 1.5 production concept uses a molded DB9 female cable with flying leads.

Current sourcing is based on a Sega Mega Drive / Genesis 2 style replacement cable.

The cable itself is not treated as having a guaranteed wire-colour standard.

Therefore:

```text
DB9 pin number = authoritative
wire colour     = batch-specific assembly information
```

This distinction is important for manufacturing safety.

In particular:

```text
DB9 pin 7 = +5 V
DB9 pin 8 = GND
```

must always be verified before assembly.

---

# 23. J1 PCB Interface

The controller cable terminates directly at PCB solder pads.

J1 therefore represents an electrical PCB interface rather than a purchased board connector.

The architecture intentionally avoids an additional internal plug/socket connection.

Benefits include:

* reduced component count
* reduced contact resistance
* lower BOM cost
* fewer potential intermittent connections

Cable strain relief must instead be provided mechanically by the enclosure/assembly.

---

# 24. Mechanical Architecture

The PCB architecture must accommodate:

* eight MX-compatible switches
* eight hot-swap sockets
* two toggle switches
* one power LED
* one dual-colour autofire LED
* controller cable exit
* PCB mounting
* enclosure clearances

The hot-swap system is considered part of the Rev 1.5 mechanical architecture and must be preserved during PCB/layout changes.

---

# 25. No Firmware Layer

Rev 1.5 deliberately contains no firmware layer.

There is therefore no:

* key scanning firmware
* debounce software
* USB stack
* configuration storage
* bootloader
* field firmware update
* programmable autofire table

Any timing or behaviour change in Rev 1.5 is implemented through hardware component values or circuit topology.

This provides a clear architectural boundary between Rev 1.5 and future programmable revisions.

---

# 26. Compatibility Model

Primary Rev 1.5 compatibility targets:

| Platform        | Interface                      |
| --------------- | ------------------------------ |
| Commodore 64    | Atari-style joystick interface |
| Commodore 128   | Atari-style joystick interface |
| Commodore Amiga | Atari-style joystick interface |

Other systems using a physically similar DE-9 connector are **not automatically electrically compatible**.

Special attention must be given to:

* +5 V availability
* FIRE2 / POT line usage
* output-driver expectations
* auxiliary pin behaviour

Physical connector compatibility alone is insufficient.

---

# 27. Rev 1.2 to Rev 1.5 Evolution

Rev 1.5 is an evolutionary refinement of the earlier functional WASDPad architecture.

Major Rev 1.5 architectural improvements include:

* PPTC +5 V protection
* signal ESD protection
* +5 V ESD protection
* MX hot-swap sockets
* standardized default mechanical switches
* finalized SLOW / FAST autofire differentiation
* dual-colour autofire status indication
* improved component standardization
* documented cable assembly
* improved production validation requirements

The underlying hardware-only joystick concept remains unchanged.

---

# 28. Rev 1.5 Architectural Boundaries

The following are explicitly within the Rev 1.5 architecture:

* hardware-only operation
* fixed two-speed autofire
* physical autofire enable switch
* physical speed selector
* dual-colour autofire indication
* MX hot-swap switches
* FIRE1 and FIRE2
* passive/discrete protection
* DB9 host interface

The following are **not** Rev 1.5 features:

* microcontroller control
* firmware-adjustable autofire
* USB HID
* software configuration
* programmable profiles
* firmware-based debounce
* persistent digital settings

These belong to potential future hardware revisions.

---

# 29. Future Architecture — Rev 2.0

Rev 2.0 is expected to be architecturally separate from Rev 1.5.

Potential future functions may include:

* RP2040-class microcontroller
* firmware-controlled autofire
* adjustable autofire rate
* burst mode
* configurable debounce
* programmable profiles
* persistent configuration
* USB firmware update
* optional USB HID
* programmable LED behaviour

These concepts must not be retroactively incorporated into Rev 1.5 documentation unless the Rev 1.5 hardware itself is changed.

---

# 30. Engineering Validation Status

Current architecture-level status:

| Area                           | Status               |
| ------------------------------ | -------------------- |
| Hardware-only architecture     | Validated concept    |
| DB9 interface                  | Defined              |
| Direction controls             | Defined              |
| FIRE1                          | Defined              |
| FIRE2                          | Defined              |
| Autofire architecture          | Defined              |
| FAST/SLOW timing values        | Physically validated |
| PPTC protection                | Selected             |
| Signal ESD architecture        | Selected             |
| +5 V ESD architecture          | Pinout validated     |
| MX hot-swap architecture       | Defined              |
| Default switch                 | Selected             |
| Power indication               | Defined              |
| Dual-colour indication         | Pinout validated     |
| Controller cable architecture  | Defined              |
| Cable batch verification       | Documented           |
| Final schematic                | Engineering review   |
| Final PCB                      | Engineering review   |
| Rev 1.5 manufactured prototype | Pending              |
| Complete system validation     | Pending              |

---

# 31. Pre-Production Architectural Checks

Before Rev 1.5 is approved for manufacturing, the final schematic and PCB must be checked against this architecture.

Mandatory checks include:

* DB9 pin mapping
* +5 V / GND routing
* PPTC placement and rating
* D4/D5 ESD topology
* D6 ESD topology and pin mapping
* ICM7555 supply and timing network
* CD4066 supply and switch mapping
* 2N7002 pin mappings
* MMBT3904 pin mappings
* D7 common-cathode topology
* D7 physical footprint/pin numbering
* R13/R14 timing values
* SLOW/FAST physical switch direction
* FIRE1 manual operation with autofire disabled
* FIRE2 independence
* MX hot-swap footprint compatibility
* cable pad numbering

No production approval should be given solely from a clean ERC/DRC result; component pinout and functional topology checks remain mandatory.

---

# 32. Related Documentation

```text
README.md

docs/
├── README.md
├── architecture/
│   └── System_architecture.md
├── specification/
│   ├── PROJECT_SPECIFICATION.md
│   └── FEATURE_SPECIFICATION.md
└── assembly/
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

# 33. Document Versioning

Architecture-document versions are independent of PCB hardware revisions.

Current state:

```text
Hardware Revision:      Rev 1.5
Architecture Document:  v0.9
```

Documentation corrections or clarification do not require a new PCB revision unless the physical or electrical design changes.

---

# 34. Version History

| Version | Date           | Status                     | Changes                                                                                                                                                                                                                                                                                                                                   |
| ------- | -------------- | -------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 0.1     | Not recorded   | Draft                      | Initial system architecture documentation                                                                                                                                                                                                                                                                                                 |
| 0.4     | Not recorded   | Development                | Initial Rev 1.5 architecture and future-revision separation                                                                                                                                                                                                                                                                               |
| 0.6     | Not recorded   | Development                | Protection and hot-swap concepts introduced                                                                                                                                                                                                                                                                                               |
| 0.8     | Not recorded   | Engineering                | Rev 1.5 architecture refined during BOM/component selection                                                                                                                                                                                                                                                                               |
| **0.9** | **2026-08-18** | **Engineering Validation** | Updated to actual Rev 1.5 architecture; added PPTC and ESD architecture, finalized hot-swap system, Gateron switch baseline, ICM7555/CD4066 architecture, validated 330 kΩ / 680 kΩ autofire configuration, common-cathode dual-colour indication, cable/J1 architecture, compatibility boundaries and production validation requirements |

---

# 35. Next Version

The next planned architecture-document release is:

**Version 1.0**

Target milestone:

**First complete Rev 1.5 prototype manufactured and successfully validated against the final schematic, PCB and functional requirements.**

Until that milestone is reached:

```text
Hardware Revision: Rev 1.5
Architecture Status: Engineering Validation / Pre-Prototype
```
