# WASDPad+

### Hardware WASD-style controller for Commodore 64, Amiga and compatible retro computers

**Current Hardware:** Rev1.5.1
**Status:** Production Release Candidate
**Architecture:** Pure hardware — no MCU, firmware or drivers

---

## Modern controls. Original hardware.

**WASDPad+** is an open hardware game controller designed for classic computers using the traditional Atari-style digital joystick interface.

It combines the familiar precision of a keyboard-style WASD layout with an electrical architecture designed specifically for original retro hardware.

The controller connects directly to the joystick port.

No USB conversion.
No Bluetooth.
No firmware.
No software driver.
No input polling.

Just switches, discrete hardware and the original computer.

```text
PLAYER
   │
   ▼
MX MECHANICAL SWITCH
   │
   ▼
DISCRETE HARDWARE
   │
   ▼
PROTECTED DE-9 SIGNAL
   │
   ▼
RETRO COMPUTER
```

The current **Rev1.5.1** hardware is the production-oriented evolution of the WASDPad platform, adding hot-swappable mechanical switches, hardware autofire, electrical protection, dual-colour status indication and subtle key backlighting while retaining the direct hardware signal path of the original design.

---

# Why WASDPad?

Classic joystick games were designed around digital inputs:

```text
UP
DOWN
LEFT
RIGHT
FIRE
```

Traditional joysticks translate these into movement of a physical stick.

WASDPad takes a different approach.

The directional controls are individual mechanical keys arranged in a familiar keyboard-style layout.

This provides:

* short physical travel
* crisp digital actuation
* independent directional control
* familiar WASD ergonomics
* replaceable mechanical switches
* direct electrical signalling

The controller does not emulate a joystick through software.

**Electrically, it is the joystick.**

---

# Rev1.5.1 Highlights

## ⌨️ Eight Mechanical Gameplay Switches

Rev1.5.1 provides eight primary gameplay controls:

```text
UP
DOWN
LEFT
RIGHT

FIRE1 LEFT
FIRE1 RIGHT

FIRE2 LEFT
FIRE2 RIGHT
```

The duplicated FIRE buttons create an ambidextrous layout.

---

## 🔄 MX Hot-Swap

All eight gameplay switches use **Kailh MX-compatible hot-swap sockets**.

Production socket:

**Kailh / Kaihua CPG151101S11**

Default switch:

**Gateron KS-8 Yellow**

Mechanical switches can therefore be replaced without soldering.

This makes it possible to:

* replace worn switches
* experiment with different switch types
* customize switch feel
* service the controller without PCB rework

---

## 🔥 Hardware Autofire

FIRE1 includes a completely hardware-generated autofire system.

The production circuit uses a:

**Texas Instruments TLC555CDR CMOS timer**

with hardware mode selection through a:

**Texas Instruments CD4066BM96**

Two fixed autofire rates are available:

| Mode | Timing Resistance |
| ---- | ----------------: |
| SLOW |            680 kΩ |
| FAST |            330 kΩ |

Physical selector orientation:

```text
LEFT  -> SLOW
RIGHT -> FAST
```

Autofire can be independently enabled or disabled.

When disabled, FIRE1 behaves as a conventional joystick fire button.

There is no firmware involved in generating the autofire pulses.

---

## 🔴🟢 Dual-Colour Autofire Status

A dedicated red/green status LED provides visual feedback for the autofire system.

Production LED:

**Bivar 3BC-3-F**

The indicator uses independent transistor driver stages and is electrically separated from the gameplay signal path.

A separate red LED provides controller power indication.

---

## 💡 Warm-White Key Backlighting

Rev1.5.1 introduces subtle illumination beneath all eight gameplay switches.

Eight warm-white SMD LEDs provide the backlight:

**XINGLIGHT XL-2012WWC**

Each LED has an independent current-limiting resistor and is intentionally operated at low current.

The goal is not high-brightness decorative lighting.

The goal is a restrained, functional glow beneath the keys.

A dedicated hardware switch allows the entire backlight system to be turned on or off independently from controller operation.

---

# Electrical Protection

Original retro computers were not designed with modern hot-plugging and ESD expectations in mind.

Rev1.5.1 therefore includes dedicated protection between the external controller environment and the host computer.

## +5 V Overcurrent Protection

The joystick-port +5 V supply passes through a resettable PPTC:

**Littelfuse 1206L005/30WR**

This limits current during sustained fault conditions and automatically resets after the fault is removed.

---

## Signal-Line ESD Protection

Externally accessible joystick signals are protected using dedicated multi-line ESD arrays.

Production devices:

**TECH PUBLIC PESD5V0S4UD**

Protected signal architecture includes the direction and fire interfaces.

---

## +5 V Transient Protection

The protected +5 V rail includes dedicated ESD / TVS protection.

Production device:

**TECH PUBLIC TPE0562BC3**

The protection topology and PCB connection were explicitly reviewed as part of the Rev1.5.1 engineering release process.

---

# Direct Retro Hardware Interface

WASDPad+ does not insert a digital protocol between the player and the computer.

For normal manual inputs:

```text
Mechanical Switch
       │
       ▼
Hardware Signal Path
       │
       ▼
Host Joystick Input
```

There is no:

* USB polling interval
* wireless transmission
* firmware input scan
* operating-system driver
* software translation
* protocol conversion

This makes the architecture deterministic and particularly suitable for latency-sensitive retro gaming.

---

# FIRE1 and FIRE2

Rev1.5.1 provides two independent fire functions.

### FIRE1

DE-9 pin 6

Supports:

* manual fire
* hardware autofire

### FIRE2

DE-9 pin 9 / POTX

Supports:

* independent manual second-fire input

FIRE2 functionality depends on the target computer and software.

Autofire applies to **FIRE1 only** in Rev1.5.1.

---

# DE-9 Interface

The controller follows the classic digital joystick interface architecture.

| DE-9 Pin | Function                                     |
| -------: | -------------------------------------------- |
|        1 | UP                                           |
|        2 | DOWN                                         |
|        3 | LEFT                                         |
|        4 | RIGHT                                        |
|        5 | Auxiliary / unused in current cable assembly |
|        6 | FIRE1                                        |
|        7 | +5 V                                         |
|        8 | GND                                          |
|        9 | FIRE2 / POTX                                 |

The electrical pin number is authoritative.

Cable conductor colours are **not** considered authoritative because they may vary between manufacturing batches.

---

# Target Platforms

Primary development targets are:

* **Commodore 64**
* **Commodore 128**
* **Commodore Amiga**

The architecture may also work with other systems using electrically compatible Atari-style digital joystick interfaces.

Compatibility must be evaluated electrically — connector shape alone does not guarantee compatibility.

The Commodore Plus/4 family can be supported through an appropriate passive pin-mapping adapter.

---

# Rev1.5.1 Architecture

The controller remains intentionally modular.

```text
                    HOST DE-9 PORT
                         │
              ┌──────────┴──────────┐
              │                     │
             +5 V                  GND
              │                     │
              ▼                     │
       Resettable PPTC              │
              │                     │
              ▼                     │
       ESD / TVS Protection         │
              │                     │
              ▼                     │
      Protected Power Rail          │
              │                     │
      ┌───────┼────────┬────────────┤
      │       │        │            │
      ▼       ▼        ▼            ▼
   Inputs  Autofire  Status      Backlight
            Logic     LEDs         System
      │       │
      └───┬───┘
          ▼
    Output Switching
          │
          ▼
   Protected Signals
          │
          ▼
      HOST COMPUTER
```

The visual systems are deliberately separated from the primary gameplay path.

A backlight or indicator failure should not intentionally prevent basic manual controller operation.

---

# Hardware-Only by Design

Rev1.5.1 deliberately does **not** contain a microcontroller.

That is not a limitation accidentally left in the design.

It is part of the design philosophy.

The current generation prioritizes:

* simplicity
* deterministic behaviour
* repairability
* low power consumption
* compatibility with vintage hardware
* understandable electronics
* long-term serviceability

There is no programmed component required for normal operation.

---

# PCB and Manufacturing

Rev1.5.1 has completed its principal pre-production engineering stages.

The PCB design includes:

* two-layer construction
* GND copper zones on both layers
* GND stitching vias
* SMD logic and protection electronics
* bottom-mounted MX hot-swap sockets
* bottom-mounted backlight control
* THT user-interface components
* direct controller-cable connection
* mixed automated/manual assembly

Engineering checks completed:

```text
Schematic Review                 PASS
ERC                              PASS
PCB Layout Review                PASS
DRC                              PASS
Critical Pinout Review           PASS
Protection Topology Review       PASS
Assembly Orientation Review      PASS
Gerber Generation                COMPLETE
Master BOM                       COMPLETE
Master CPL                       COMPLETE
Manufacturing Documentation      COMPLETE
```

---

# Current Release Status

## WASDPad+ Rev1.5.1

**Production Release Candidate**

The Rev1.5.1 design is frozen for production-candidate manufacture.

Completed:

* [x] hardware architecture
* [x] schematic
* [x] component selection
* [x] PCB layout
* [x] electrical protection
* [x] hardware autofire
* [x] hot-swap architecture
* [x] status indication
* [x] key backlighting
* [x] ERC
* [x] DRC
* [x] critical pinout validation
* [x] protection topology validation
* [x] assembly orientation review
* [x] Gerber generation
* [x] Master BOM
* [x] Master CPL
* [x] datasheet traceability
* [x] alternate-part policy
* [x] procurement documentation
* [x] engineering release review

Remaining:

* [ ] production-candidate manufacture
* [ ] complete physical assembly
* [ ] electrical bring-up
* [ ] functional validation
* [ ] real-system gameplay validation
* [ ] final enclosure validation
* [ ] Production Approval

The project intentionally distinguishes between:

**engineering-ready for manufacture**

and

**physically production-validated hardware**.

Rev1.5.1 currently satisfies the first condition.

---

# Release Path

```text
                    Rev1.5.1
                DESIGN FREEZE
                     ✓
                     │
                     ▼
             Engineering Review
                    PASS
                     │
                     ▼
          Production-Candidate
              Manufacturing
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
             PRODUCTION
               APPROVED
```

No additional Rev1.5.1 feature development is planned before this validation process is complete.

---

# Documentation

The project maintains separate documents for feature behaviour, architecture, manufacturing and engineering validation.

## Start Here

### [Documentation Index](docs/README.md)

The documentation index provides the complete map of the current Rev1.5.1 documentation set.

---

## Feature Specification

### [Rev1.5.1 Feature Specification](docs/specification/FEATURE_SPECIFICATION.md)

Defines:

> **What does WASDPad+ Rev1.5.1 do?**

Includes:

* controls
* FIRE1 / FIRE2
* autofire behaviour
* hot-swap functionality
* status indication
* backlighting
* protection features
* interface behaviour
* validation requirements

---

## System Architecture

### [System Architecture](docs/architecture/System_architecture.md)

Defines:

> **How does WASDPad+ Rev1.5.1 work?**

Includes:

* signal architecture
* power architecture
* protection architecture
* autofire architecture
* switching
* backlighting
* PCB architecture
* assembly architecture
* compatibility philosophy

---

## Hardware Engineering

### [Rev1.5.1 Hardware Documentation](hardware/rev1.5/README.md)

Primary revision-specific hardware engineering documentation.

---

## Engineering Review

### [Rev1.5.1 Engineering Review Record](hardware/rev1.5/Review_Record.MD)

Formal pre-production engineering review and release decision.

---

## Development Roadmap

### [Development Roadmap](docs/roadmap/ROADMAP.md)

Tracks:

* current release state
* manufacturing
* physical validation
* Production Approval
* stable Rev1.5.1 maintenance
* future Rev2.0 direction

---

## Cable Assembly

### [Cable Assembly Procedure](docs/assembly/CABLE_ASSEMBLY.md)

Defines the controller cable mapping and mandatory production-batch continuity verification procedure.

---

# Manufacturing Documentation

Production documentation is maintained under:

[`hardware/rev1.5/bom/`](hardware/rev1.5/bom/)

Important files include:

### [Master BOM](hardware/rev1.5/bom/WASDPad_Rev1.5.1_FULL_MASTER_BOM.csv)

Authoritative source for production component identity.

### [Master CPL](hardware/rev1.5/bom/WASDPad_Rev1.5.1_FULL_MASTER_CPL.csv)

Authoritative component-placement dataset.

### [Datasheet Index](hardware/rev1.5/bom/DATASHEET_INDEX.md)

Centralized technical references for production components.

### [Alternate Parts](hardware/rev1.5/bom/ALTERNATE_PARTS.md)

Controlled component-substitution policy.

### [Procurement Notes](hardware/rev1.5/bom/PROCUREMENT_NOTES.md)

Sourcing, lifecycle, incoming-verification and procurement-control policy.

---

# Repository Structure

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
│   ├── README.md
│   ├── architecture/
│   │   └── System_architecture.md
│   ├── assembly/
│   │   └── CABLE_ASSEMBLY.md
│   ├── roadmap/
│   │   └── ROADMAP.md
│   └── specification/
│       └── FEATURE_SPECIFICATION.md
│
└── hardware/
    ├── README.md
    └── rev1.5/
        ├── README.md
        ├── Review_Record.MD
        ├── datasheets/
        └── bom/
            ├── README.md
            ├── WASDPad_Rev1.5.1_FULL_MASTER_BOM.csv
            ├── WASDPad_Rev1.5.1_FULL_MASTER_CPL.csv
            ├── DATASHEET_INDEX.md
            ├── ALTERNATE_PARTS.md
            └── PROCUREMENT_NOTES.md
```

---

# Manufacturing Philosophy

WASDPad+ is not documented only as a schematic.

Rev1.5.1 maintains a controlled production dataset covering:

* component identity
* manufacturer MPNs
* supplier references
* component placement
* PCB side
* assembly classification
* datasheet traceability
* approved / candidate alternates
* procurement rules
* cable verification
* engineering release status

The **Master BOM** is authoritative for production component identity.

The **Master CPL** is authoritative for component placement.

Assembly-house-specific files may be derived from these records but do not redefine them.

---

# Serviceability

Rev1.5.1 was designed to remain repairable.

The controller uses:

* replaceable MX gameplay switches
* hot-swap sockets
* conventional discrete components
* documented semiconductor MPNs
* documented passive components
* standard electronic packages
* replaceable external cable
* no programmed device required for operation

This makes the hardware suitable not only for manufacture, but also for long-term maintenance.

---

# Rev1.2 → Rev1.5.1

Rev1.5.1 builds on the earlier validated WASDPad hardware platform.

The goal was not to replace the fundamental controller concept.

The goal was to mature it.

Major improvements include:

```text
Rev1.2
  │
  ├── Proven hardware control concept
  ├── Direction + FIRE architecture
  └── Hardware autofire
          │
          ▼
Rev1.5.1
  │
  ├── MX hot-swap sockets
  ├── Production component selection
  ├── Improved autofire implementation
  ├── Dual-colour status indication
  ├── +5 V overcurrent protection
  ├── Signal ESD protection
  ├── +5 V transient protection
  ├── Improved PCB grounding
  ├── Warm-white key backlighting
  ├── Independent backlight control
  ├── Master BOM / CPL
  └── Production engineering documentation
```

Rev1.5.1 represents the mature discrete-hardware branch of the project.

---

# Future Rev2.0

A future Rev2.0 may explore a programmable architecture.

Possible concepts include:

* MCU-controlled autofire
* adjustable firing rates
* burst-fire modes
* configurable debounce
* game-specific profiles
* persistent configuration
* programmable indication
* USB configuration
* optional USB HID support

An MCU platform such as the **RP2040 family** may be evaluated.

Rev2.0 is intentionally separated from Rev1.5.1.

The objective is to stabilize and validate the discrete Rev1.5.1 platform before introducing programmable complexity.

---

# Contributing

Engineering contributions, testing results and compatibility findings are welcome.

When proposing hardware changes, please distinguish between:

* documentation corrections
* sourcing substitutions
* electrical design changes
* PCB changes
* mechanical changes
* new features

Changes affecting manufactured hardware should be reviewed against the current Rev1.5.1 architecture and production documentation before being considered compatible with the existing revision.

---

# License

See the repository [`LICENSE`](LICENSE) file for licensing terms.

Third-party component names, product names and trademarks remain the property of their respective owners.

---

# Project Snapshot

```text
Project              WASDPad+
Current Hardware     Rev1.5.1
Architecture         Discrete / Hardware-Only
Interface            DE-9 Digital Joystick
Primary Platforms    Commodore 64 / 128 / Amiga
Gameplay Switches    8 × MX-Compatible Hot-Swap
FIRE Inputs          FIRE1 + FIRE2
Autofire             Hardware / FIRE1
Autofire Modes       OFF / SLOW / FAST
Key Backlight        8 × Warm-White LED
Protection           PPTC + Signal ESD + +5 V TVS
Firmware             None
Drivers              None
Current Status       Production Release Candidate
```

---

## WASDPad+ Rev1.5.1

### Built for the machines that made digital controls matter.

**Direct hardware. Mechanical switches. No firmware between you and the game.**
