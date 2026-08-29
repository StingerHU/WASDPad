# WASDPad+ Hardware

## Revision 1.5.1

**Status:** Production Release Candidate
**Hardware Revision:** Rev1.5.1
**Last Updated:** 2026-08-29

---

# Overview

WASDPad+ Revision 1.5.1 is the production-oriented evolution of the proven Revision 1.2 hardware platform.

The fundamental design philosophy remains unchanged:

* fully hardware-based operation
* direct retro-computer controller interface
* no microcontroller
* no firmware
* no software dependency
* minimal input latency
* serviceable mechanical construction

Revision 1.5.1 focuses on improving:

* electrical protection
* reliability
* serviceability
* manufacturability
* component traceability
* switch replacement
* status indication
* key illumination
* production documentation

The controller remains fundamentally compatible with the classic digital joystick interface architecture used by systems such as the Commodore 64 and Amiga.

---

# Key Improvements over Revision 1.2

Revision 1.5.1 introduces the following major hardware improvements:

* Kailh MX-compatible hot-swap sockets
* replaceable Gateron / Cherry MX-compatible mechanical switches
* resettable +5 V overcurrent protection
* ESD protection on externally accessible controller signal lines
* dedicated +5 V ESD/TVS protection
* redesigned dual-colour autofire status indication
* warm-white key backlighting
* independent backlight ON/OFF control
* standardized SMD passive components
* improved PCB routing
* improved grounding
* GND stitching vias
* production-oriented component selection
* manufacturer MPN traceability
* Master BOM
* Master CPL
* centralized datasheet index
* alternate-component policy
* procurement and lifecycle documentation

---

# Architecture

Revision 1.5.1 remains a **fully hardware-based controller**.

It does not contain:

* a microcontroller
* firmware
* USB connectivity
* user profiles
* software configuration
* programmable logic
* operating-system dependencies

All controller functions are implemented using discrete hardware and CMOS logic.

This architecture preserves the immediate electrical behaviour expected from traditional retro-computer controllers.

---

# Direction and Fire Inputs

The primary gameplay controls use MX-compatible mechanical switches.

Revision 1.5.1 provides eight switch positions:

* UP
* DOWN
* LEFT
* RIGHT
* FIRE1 left
* FIRE1 right
* FIRE2 left
* FIRE2 right

The duplicated fire buttons provide an ambidextrous control layout.

Mechanical switches are installed through **Kailh `CPG151101S11` hot-swap sockets**.

This allows compatible switches to be replaced without soldering.

The production-fitted switch type is:

**Gateron KS-8 Yellow**

Other mechanically compatible MX-style switches may be used according to the component-substitution policy.

---

# Autofire System

Autofire remains implemented entirely in hardware.

Revision 1.5.1 uses:

**Texas Instruments `TLC555CDR`**

as the production-selected CMOS timer.

The TLC555 replaces the ICM7555 used during earlier development while retaining the CMOS 555 timing architecture.

Autofire is available on **FIRE1**.

Two fixed speed modes are provided:

| Mode | Timing Resistance |
| ---- | ----------------: |
| FAST |            330 kΩ |
| SLOW |            680 kΩ |

The values were selected through physical gameplay testing.

Autofire control is provided through dedicated hardware switches:

* Autofire ON/OFF
* SLOW/FAST speed selection

No firmware or software timing is involved.

---

# Autofire Status Indication

Revision 1.5.1 uses a dedicated red/green dual-colour status LED.

Production component:

**Bivar `3BC-3-F`**

Configuration:

**Common cathode**

The status circuit uses dedicated transistor drivers for the two LED channels.

The indicator provides immediate visual feedback for the selected autofire state/speed.

---

# Key Backlighting

Revision 1.5.1 adds subtle warm-white illumination beneath the eight mechanical keys.

Production LEDs:

**XINGLIGHT `XL-2012WWC`**

Quantity:

**8**

Each LED uses an individual current-limiting resistor.

The circuit intentionally operates the LEDs at relatively low current to create subtle illumination rather than high-intensity decorative lighting.

Backlighting can be enabled or disabled using the bottom-mounted:

**C&K `PCM12SMTR`**

slide switch.

---

# Electrical Protection

Revision 1.5.1 adds several protection stages intended to improve robustness when connected to vintage computer hardware.

## Overcurrent Protection

The +5 V controller-port supply is protected by a resettable PPTC.

Production component:

**Littelfuse `1206L005/30WR`**

---

## Signal-Line ESD Protection

Externally accessible controller signal lines are protected using ESD arrays.

Production components:

**D4 / D5 — TECH PUBLIC `PESD5V0S4UD`**

These devices protect the relevant digital controller lines against electrostatic discharge.

---

## +5 V ESD / TVS Protection

The +5 V supply path uses a dedicated protection device.

Production component:

**D6 — TECH PUBLIC `TPE0562BC3`**

The selected component and PCB connection were specifically validated for Revision 1.5.1.

---

# Logic and Switching

Revision 1.5.1 uses discrete CMOS and transistor logic rather than programmable devices.

Primary active devices include:

| Function            | Device              |
| ------------------- | ------------------- |
| Autofire timer      | TI TLC555CDR        |
| Bilateral switching | TI CD4066BM96       |
| Logic MOSFETs       | onsemi 2N7002LT1G   |
| Status LED drivers  | onsemi MMBT3904LT1G |

This maintains deterministic hardware operation without firmware.

---

# PCB Design

The Revision 1.5.1 PCB has completed the primary design and DRC process.

The board includes:

* front and back copper layers
* GND copper zones
* GND stitching vias
* SMD logic and protection circuitry
* THT user-interface components
* bottom-mounted Kailh hot-swap sockets
* bottom-mounted backlight switch
* PCB solder pads for the DB9 cable

PCB routing and grounding were reviewed as part of the Rev1.5.1 manufacturing preparation.

The final design passed KiCad DRC with no unresolved electrical routing violations.

---

# Assembly Architecture

Revision 1.5.1 intentionally uses a mixed assembly process.

## Top SMD

Includes the majority of:

* logic
* protection
* resistors
* capacitors
* transistor stages
* backlight LEDs

These components are suitable for automated SMT assembly.

## Bottom SMD / Manual

Includes:

* Kailh MX hot-swap sockets
* backlight control switch

These may be manually installed depending on the manufacturing configuration.

## Through-Hole

Includes selected:

* status LEDs
* diode
* autofire switches

## Mechanical / Manual

Includes:

* eight replaceable mechanical switches

## Cable / Manual

The DB9 controller cable is soldered directly to dedicated PCB pads.

---

# Manufacturing Documentation

Revision 1.5.1 uses a structured manufacturing-documentation model.

The authoritative BOM documentation is located under:

```text id="rc5jpx"
hardware/rev1.5/bom/
```

Primary files include:

```text id="4ixzsv"
WASDPad_Rev1.5.1_FULL_MASTER_BOM.csv
WASDPad_Rev1.5.1_FULL_MASTER_CPL.csv
DATASHEET_INDEX.md
ALTERNATE_PARTS.md
PROCUREMENT_NOTES.md
```

---

# Master BOM

`WASDPad_Rev1.5.1_FULL_MASTER_BOM.csv`

is the authoritative component list for the hardware revision.

It records:

* designators
* manufacturer part numbers
* quantities
* footprints
* component descriptions
* JLCPCB/LCSC identifiers where applicable
* PCB side
* assembly classification

---

# Master CPL

`WASDPad_Rev1.5.1_FULL_MASTER_CPL.csv`

provides the complete component-placement dataset.

Manufacturing-house-specific CPL files may be generated as subsets of the Master CPL.

---

# Datasheet Traceability

`DATASHEET_INDEX.md`

maps production components to manufacturer or trusted supplier documentation.

The traceability model is:

```text id="izyl77"
PCB Designator
      ↓
Master BOM
      ↓
Manufacturer MPN
      ↓
DATASHEET_INDEX.md
      ↓
Manufacturer Datasheet
```

---

# Alternate Components

`ALTERNATE_PARTS.md`

defines:

* Production Primary components
* Approved Alternates
* Legacy Validated components
* Candidates
* prohibited uncontrolled substitutions

Critical components require explicit engineering validation before substitution.

---

# Procurement

`PROCUREMENT_NOTES.md`

defines:

* sourcing policy
* preferred suppliers
* assembly-house substitution policy
* lifecycle management
* incoming inspection
* cable batch verification
* production traceability
* procurement change control

---

# Design Validation

The Rev1.5.1 design has completed the principal pre-production engineering stages.

| Area                              | Status   |
| --------------------------------- | -------- |
| Architecture                      | Complete |
| Feature specification             | Complete |
| Component selection               | Complete |
| Schematic                         | Complete |
| PCB layout                        | Complete |
| ERC                               | Passed   |
| PCB DRC                           | Passed   |
| Protection-device topology review | Passed   |
| Critical footprint/pinout review  | Passed   |
| Gerber generation                 | Complete |
| Master BOM                        | Complete |
| Master CPL                        | Complete |
| Datasheet index                   | Complete |
| Alternate-part policy             | Complete |
| Procurement documentation         | Complete |
| Assembly data preparation         | Complete |
| Production PCB assembly           | Pending  |
| Rev1.5.1 physical validation      | Pending  |
| Production approval               | Pending  |

---

# Production Release Status

Revision 1.5.1 is currently classified as:

**Production Release Candidate**

This means that:

* the electrical design is complete
* the PCB layout is complete
* manufacturing data has been generated
* component selection has been frozen for the production candidate
* BOM/CPL documentation is complete
* critical component pinouts and protection topology have been reviewed

Final **Production Approved** status requires successful assembly and physical functional validation of the Rev1.5.1 production hardware.

---

# Validation Before Production Approval

The assembled Rev1.5.1 controller should be tested for:

* UP
* DOWN
* LEFT
* RIGHT
* FIRE1 left
* FIRE1 right
* FIRE2 left
* FIRE2 right
* autofire OFF
* autofire SLOW
* autofire FAST
* dual-colour autofire indication
* key backlight
* backlight ON/OFF control
* +5 V continuity
* GND continuity
* absence of VCC-GND short circuit
* DB9 cable mapping
* hot-swap socket operation
* mechanical-switch replacement
* operation on representative target retro-computer hardware

Successful completion of the validation procedure allows promotion from:

**Production Release Candidate**

to:

**Production Approved**

---

# Compatibility Philosophy

WASDPad+ is designed around the electrical behaviour of traditional digital joystick interfaces.

The controller intentionally avoids active digital protocols, USB conversion and software translation.

This provides:

* deterministic behaviour
* direct electrical switching
* very low input latency
* independence from operating systems and drivers
* compatibility with original retro-computer hardware philosophy

Platform-specific electrical compatibility shall nevertheless be verified before claiming support for an additional computer platform.

---

# Revision Philosophy

Revision 1.5.1 represents the mature discrete-hardware branch of WASDPad+.

More advanced programmable features are intentionally outside the scope of this revision.

Features requiring a microcontroller or firmware belong to a future hardware generation rather than Revision 1.5.1.

This separation keeps Rev1.5.1:

* simple
* deterministic
* repairable
* understandable
* retro-hardware appropriate
* production friendly

---

# Revision History

| Revision     | Status                           | Description                                                                                                                                                                   |
| ------------ | -------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Rev1.2       | Production validated             | Original validated WASDPad hardware platform                                                                                                                                  |
| Rev1.5       | Development branch               | Reliability, protection, hot-swap and manufacturing improvements                                                                                                              |
| **Rev1.5.1** | **Production Release Candidate** | Completed discrete-hardware production design with ESD/PTC protection, hot-swap sockets, dual-colour status indication, key backlighting and full manufacturing documentation |
