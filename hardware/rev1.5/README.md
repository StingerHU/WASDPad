# WASDPad+ Hardware

## Revision 1.5.2 — Final Production Release

**Hardware Revision:** **Rev1.5.2**  
**Status:** **FINAL PRODUCTION RELEASE — manufactured Rev1.5.2 functional PASS**  
**Release updated:** 2026-10-19

The SPEED-switch common-pad problem identified on Rev1.5.1 was measured, repaired on an existing board and corrected in the Rev1.5.2 schematic, PCB routing and matching Gerber outputs. A **newly manufactured Rev1.5.2 controller was physically tested and all reported functionality passed** (project-owner confirmation, October 2026). The preceding Rev1.5.1 manufacturing review is retained as historical evidence, not the current revision's release verdict.

The [Rev1.5.2 manufacturing release notes](REV1.5.2_MANUFACTURING_RELEASE_NOTES.md) are the current release record; see the [Rev1.5.1 engineering erratum](REV1.5.1_TO_REV1.5.2_SPEED_SELECTOR_ERRATUM.md) and [original engineering review](Rev1.5.1-Engineering-Manufacturing-Record.MD) for revision history.

---

# Overview

WASDPad+ Revision 1.5.2 is the final, physically validated evolution of the proven Revision 1.2 hardware platform.

The fundamental design philosophy remains unchanged:

* fully hardware-based operation
* direct retro-computer controller interface
* no microcontroller
* no firmware
* no software dependency
* minimal input latency
* serviceable mechanical construction

The earlier Rev1.5.1 revision introduced, and Rev1.5.2 retains, improvements in:

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

The Rev1.5 hardware generation introduced the following major improvements, all retained in Rev1.5.2:

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

Revision 1.5.2 remains a **fully hardware-based controller**.

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

PCB routing and grounding were reviewed as part of the Rev1.5 development and Rev1.5.2 production preparation.

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

The **current released revision is Rev1.5.2**. The owner confirms corrected PCB/gerber outputs were manufactured successfully and the resulting controller passed its complete functional test. The public repo ZIP does **not** contain the corresponding Rev1.5.2 CAD/gerber/BOM/CPL output bundle; do not use only the historical Rev1.5.1 BOM/CPL filenames as proof of the final assembly configuration.

**Historical Rev1.5.1 engineering and sourcing records still present in this repository:**

```text
hardware/rev1.5/
├── Rev1.5.1-Engineering-Manufacturing-Record.MD
├── REV1.5.1_TO_REV1.5.2_SPEED_SELECTOR_ERRATUM.md
├── REV1.5.2_MANUFACTURING_RELEASE_NOTES.md
├── datasheets/
│   └── WASDPad_Rev1.5.1_DATASHEET_INDEX.md
└── bom/
    ├── README.md
    ├── WASDPad_Rev1.5.1_FULL_MASTER_BOM.csv
    ├── WASDPad_Rev1.5.1_FULL_MASTER_CPL.csv
    ├── ALTERNATE_PARTS.md
    └── PROCUREMENT_NOTES.md
```

Preserve the exact Rev1.5.2 production-file set from the actual fabrication order separately, if not yet published here. The `Rev1.5.1`-named entries are not automatically valid for manufacturing Rev1.5.2.

---

# Master BOM — historical Rev1.5.1 source

[`WASDPad_Rev1.5.1_FULL_MASTER_BOM.csv`](bom/WASDPad_Rev1.5.1_FULL_MASTER_BOM.csv) records the previous revision's component selection, quantities and footprints. It is not labelled or independently approved as the final Rev1.5.2 BOM in this repository export. A Rev1.5.2 order must be matched against its own released production dataset.

---

# Master CPL — historical Rev1.5.1 source

[`WASDPad_Rev1.5.1_FULL_MASTER_CPL.csv`](bom/WASDPad_Rev1.5.1_FULL_MASTER_CPL.csv) records the previous revision's placement data. In particular, do not assume a historical dataset is unchanged or suitable for a new Rev1.5.2 assembly without production-release reconciliation.

---

# Datasheet Traceability

The repository contains a [Rev1.5.1 component datasheet index](datasheets/WASDPad_Rev1.5.1_DATASHEET_INDEX.md). Use it as manufacturer reference information and reconcile component identity against the actual released Rev1.5.2 BOM before manufacturing. It does not establish a new Rev1.5.2 part list by itself.

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

| Validation evidence | Result |
| --- | --- |
| Original Rev1.5.1 pre-production review | Historical PASS; physical SPEED-selector fault discovered afterwards |
| Rev1.5.1 electrical diagnosis | PASS — pin-2 common contact, contact closure and faulty nets confirmed |
| Existing Rev1.5.1 physical correction | PASS — cuts/jumpers, bench measurements and Amiga 1200 gameplay |
| Rev1.5.2 schematic / PCB revision | Corrected; previously reported ERC 0 errors / 0 warnings; DRC 0 errors / 0 unconnected pads |
| Recorded custom-footprint/J1 DRC warnings | 46 in prior report; independent final waiver record not attached to this ZIP |
| Rev1.5.2 production fabrication outputs | Updated and manufactured, project-owner confirmation |
| **Newly manufactured Rev1.5.2 full functional test** | **PASS — project-owner confirmation, October 2026** |
| **Current release status** | **FINAL PRODUCTION RELEASE** |

**Scope:** A manufactured Rev1.5.2 sample passed all reported controller functions. Production batch inspection, traceable BOM/CPL and any conformity/independent certification are separate matters and are not inferred from gameplay alone. See [manufacturing release notes](REV1.5.2_MANUFACTURING_RELEASE_NOTES.md).

---

# Production Release Status

**Rev1.5.2 — FINAL PRODUCTION RELEASE / PHYSICALLY FUNCTIONALLY VALIDATED.** The project owner has received and tested an actual fabricated Rev1.5.2 PCB, confirming that the SPEED selector fix and the controller's complete reported functionality work. The obsolete original Rev1.5.1 Gerbers shall not be reused for new manufacturing.

The historic Rev1.5.1 Production Release Candidate status is retained only in its date-specific engineering record. It does not describe the current release.

---

# Repeatable acceptance checks for manufactured units

A first manufactured Rev1.5.2 controller has already **passed complete reported functional validation** (owner confirmation). To keep future production repeatable, perform the following on new units or batches:

- PCB revision, assembly orientation, DB9 mapping, power-to-ground short and initial +5 V checks
- UP / DOWN / LEFT / RIGHT, both FIRE1 controls, both FIRE2 controls
- AUTO OFF / ON, **FAST and SLOW correctly distinguished**, manual FIRE1 retained
- Power and red/green autofire indication
- Hot-swap switches, key backlight, dedicated backlight control
- Representative real-system play and enclosure/mechanical fit
- Traceability against the correct **Rev1.5.2** Gerber/BOM/CPL handoff

This is routine production QA and does not reclassify the already verified Rev1.5.2 design as an untested release.

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

Revision 1.5.2 is the final, fully functionally validated discrete-hardware branch of WASDPad+.

More advanced programmable features are intentionally outside the scope of this revision.

Features requiring a microcontroller or firmware belong to the future Rev2.0 platform, not Rev1.5.2.

This separation keeps Rev1.5.2:

* simple
* deterministic
* repairable
* understandable
* retro-hardware appropriate
* production friendly

---

# Revision History

| Revision | Status | Description |
| --- | --- | --- |
| Rev1.2 | Validated legacy design | Original proven discrete-controller architecture |
| Rev1.5 | Historical development | ESD protection, hot-swap, hardware autofire and backlight additions |
| Rev1.5.1 | **Superseded — not a current production Gerber baseline** | Initial production-oriented design; physical selector mapping fault found; one unit successfully reworked and tested on Amiga 1200 |
| **Rev1.5.2** | **FINAL PRODUCTION RELEASE — manufactured first-article functionality PASS** | Corrected `SW_SPEED1` common pin 2 mapping and PCB routing; updated Gerbers; newly fabricated Rev1.5.2 controller fully function-tested (owner confirmed October 2026) |
