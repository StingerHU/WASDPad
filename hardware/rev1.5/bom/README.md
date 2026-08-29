# WASDPad+ Revision 1.5.1

## Bill of Materials and Manufacturing Documentation

**Document Version:** 1.0
**Hardware Revision:** Rev1.5.1
**Status:** Production Release Candidate
**Last Updated:** 2026-08-29

---

# 1. Purpose

This directory contains the authoritative component, placement, sourcing and manufacturing documentation for **WASDPad+ Hardware Revision 1.5.1**.

Revision 1.5.1 is based on the validated WASDPad hardware architecture and introduces or finalizes:

* electrical protection
* resettable +5 V overcurrent protection
* DB9 signal ESD protection
* +5 V rail ESD/TVS protection
* MX hot-swap switch sockets
* replaceable mechanical switches
* dual-colour autofire status indication
* switch backlighting
* backlight enable/disable control
* standardized SMD passive components
* manufacturing-oriented BOM and CPL data
* component traceability by manufacturer part number
* centralized datasheet references

The fundamental operating principle remains fully hardware-based.

**Revision 1.5.1 does not require a microcontroller or firmware.**

---

# 2. Authoritative Files

The BOM directory contains the following primary documentation:

```text
hardware/rev1.5/bom/
│
├── README.md
├── WASDPad_Rev1.5.1_FULL_MASTER_BOM.csv
├── WASDPad_Rev1.5.1_FULL_MASTER_CPL.csv
├── DATASHEET_INDEX.md
├── ALTERNATE_PARTS.md
└── PROCUREMENT_NOTES.md
```

## `WASDPad_Rev1.5.1_FULL_MASTER_BOM.csv`

This is the **authoritative Master Bill of Materials** for WASDPad+ Rev1.5.1.

It contains:

* reference designators
* manufacturer part numbers
* quantities
* KiCad footprints
* component descriptions
* JLCPCB/LCSC part numbers where applicable
* PCB side / layer information
* assembly classification
* THT components
* bottom-side components
* manually installed mechanical components
* cable and PCB-interface items

If information in another BOM-related document conflicts with the Master BOM, the **Master BOM takes precedence**.

---

## `WASDPad_Rev1.5.1_FULL_MASTER_CPL.csv`

This is the complete Master Component Placement List.

It contains placement information for:

* top-side SMD components
* bottom-side SMD components
* through-hole components
* Kailh hot-swap sockets
* manually installed mechanical switches

The Master CPL is intended for manufacturing documentation and traceability.

Assembly-house-specific CPL files may be generated as subsets of this master file.

---

## `DATASHEET_INDEX.md`

Centralized datasheet and manufacturer-reference index.

Components are grouped by category, including:

* integrated circuits
* protection devices
* transistors and MOSFETs
* switches and sockets
* LEDs and optoelectronics
* diodes
* capacitors
* resistors
* mechanical switches
* cable/interface components

The Master BOM MPN remains the authoritative component identity.

---

## `ALTERNATE_PARTS.md`

Contains approved or technically evaluated replacement components.

Alternate parts shall only be used after verification of:

* electrical compatibility
* package compatibility
* footprint compatibility
* pinout
* polarity
* voltage/current ratings
* functional behaviour

Protection devices require additional topology verification.

---

## `PROCUREMENT_NOTES.md`

Contains sourcing, lifecycle, supplier and production information that does not belong in the schematic or Master BOM.

---

# 3. Revision 1.5.1 Component Status

| Component Group            | Status                                              |
| -------------------------- | --------------------------------------------------- |
| Autofire timer             | Production selected                                 |
| CMOS switching logic       | Production selected                                 |
| MOSFET logic stages        | Production selected                                 |
| Status LED drivers         | Production selected                                 |
| Autofire timing resistors  | Validated                                           |
| General resistors          | Production selected                                 |
| Timing capacitors          | Production selected                                 |
| Supply decoupling          | Production selected                                 |
| PTC overcurrent protection | Production selected                                 |
| DB9 signal ESD protection  | Production selected                                 |
| +5 V ESD/TVS protection    | Production selected                                 |
| MX hot-swap sockets        | Production selected                                 |
| Mechanical switches        | Selected / replaceable                              |
| Dual-colour status LED     | Validated                                           |
| Key backlight LEDs         | Production selected                                 |
| Backlight control switch   | Selected                                            |
| Autofire toggle switch     | Validated                                           |
| Speed selector switch      | Validated                                           |
| Controller cable           | Supplier type selected; batch verification required |
| PCB solder pads            | PCB feature / no procurement item                   |

---

# 4. Core Active Components

## 4.1 Autofire Timer

**Reference:** U1
**Manufacturer:** Texas Instruments
**MPN:** `TLC555CDR`
**Function:** CMOS timer / hardware autofire oscillator
**Package:** SOIC-8
**JLCPCB/LCSC:** `C6986`

KiCad footprint:

```text
Package_SO:SOIC-8_3.9x4.9mm_P1.27mm
```

The TLC555CDR is the production-selected timer for Rev1.5.1.

It replaces the ICM7555 used during earlier development while preserving the CMOS 555 operating principle and required pin compatibility.

Bipolar NE555-family devices are not preferred because of their higher supply-current characteristics.

---

## 4.2 Bilateral Switching Logic

**Reference:** U2
**Manufacturer:** Texas Instruments
**MPN:** `CD4066BM96`
**Function:** Quad bilateral CMOS switch
**Package:** SOIC-14
**JLCPCB/LCSC:** `C54755`

KiCad footprint:

```text
Package_SO:SO-14_3.9x8.65mm_P1.27mm
```

The CD4066 provides hardware switching for the autofire speed-selection circuitry.

---

## 4.3 MOSFET Logic

**References:** Q1–Q7
**Manufacturer:** onsemi
**MPN:** `2N7002LT1G`
**Type:** N-channel MOSFET
**Package:** SOT-23
**JLCPCB/LCSC:** `C16338`

The FIRE and autofire logic stages use seven 2N7002 MOSFETs.

Validated device mapping:

```text
Pin 1 = Gate
Pin 2 = Source
Pin 3 = Drain
```

---

## 4.4 Autofire Status Drivers

**References:** Q8, Q9
**Manufacturer:** onsemi
**MPN:** `MMBT3904LT1G`
**Type:** NPN transistor
**Package:** SOT-23
**JLCPCB/LCSC:** `C81464`

These transistors drive the red and green channels of the autofire status LED.

Validated mapping:

```text
Pin 1 = Base
Pin 2 = Emitter
Pin 3 = Collector
```

---

# 5. Autofire Timing

Revision 1.5.1 provides two fixed hardware autofire speeds.

| Reference |  Value | Function |
| --------- | -----: | -------- |
| R13       | 330 kΩ | FAST     |
| R14       | 680 kΩ | SLOW     |

The values were selected through physical gameplay testing.

User-facing switch behaviour:

```text
LEFT  -> SLOW
RIGHT -> FAST
```

These values supersede earlier experimental autofire timing values.

---

# 6. Passive Component Standardization

## 6.1 Resistors

General SMD resistors are standardized on the **YAGEO RC1206FR-07** family wherever practical.

General characteristics:

* 1206 / 3216 metric
* thick film
* ±1 %
* 0.25 W
* SMD

Values used in Rev1.5.1 include:

* 270 Ω
* 330 Ω
* 3.3 kΩ
* 4.7 kΩ
* 10 kΩ
* 100 kΩ
* 330 kΩ
* 680 kΩ

Exact designator-to-MPN assignments are maintained in the Master BOM.

---

## 6.2 Capacitors

### C1

**MPN:** `1206B224K500NT`
**Value:** 220 nF
**Dielectric:** X7R
**Package:** 1206
**JLCPCB/LCSC:** `C1857`

Used as a timing capacitor.

### C2, C3

**Manufacturer:** Samsung Electro-Mechanics
**MPN:** `CL31B104KBCNNNC`
**Value:** 100 nF
**Dielectric:** X7R
**Package:** 1206
**JLCPCB/LCSC:** `C24497`

### VCC-GND-Decoupling1

**Manufacturer:** YAGEO
**MPN:** `CC1206KRX7R8BB104`
**Value:** 100 nF
**Dielectric:** X7R
**Package:** 1206
**JLCPCB/LCSC:** `C527347`

The dedicated VCC-GND decoupling capacitor shall be located close to the relevant IC supply connections.

---

# 7. Overcurrent Protection

**Reference:** F2
**Manufacturer:** Littelfuse
**MPN:** `1206L005/30WR`
**Type:** Resettable PPTC
**Package:** 1206
**JLCPCB/LCSC:** `C3760487`

F2 protects the controller-port +5 V supply path.

The protection value was selected with the available current from the target retro-computer controller interface in mind.

---

# 8. ESD Protection

## 8.1 D4 and D5 — DB9 Signal Protection

**References:** D4, D5
**Manufacturer:** TECH PUBLIC
**MPN:** `PESD5V0S4UD`
**JLCPCB/LCSC:** `C2987082`
**Function:** Quad-line 5 V ESD protection
**Package:** SC-74-6 / SOT-23-6 compatible

KiCad footprint:

```text
Package_TO_SOT_SMD:SC-74-6_1.55x2.9mm_P0.95mm
```

These devices protect externally accessible controller signal lines.

The production-selected device pinout and topology were verified against the PCB implementation.

---

## 8.2 D6 — +5 V Protection

**Reference:** D6
**Manufacturer:** TECH PUBLIC
**MPN:** `TPE0562BC3`
**JLCPCB/LCSC:** `C2841389`
**Function:** 5 V bidirectional ESD/TVS protection
**Package:** SOT-323 / SC-70

KiCad footprint:

```text
Package_TO_SOT_SMD:SOT-323_SC-70
```

Validated Rev1.5.1 connection:

```text
Pin 1 -> protected +5 V rail
Pin 2 -> NC
Pin 3 -> GND
```

The production-selected TPE0562BC3 differs internally from the originally evaluated PESD6V0L2UU device.

It is therefore treated as a specifically validated Rev1.5.1 protection component rather than as an uncontrolled generic substitution.

**Validation status: PASS**

---

# 9. LED System

## 9.1 D1 — Power Indicator

**Reference:** D1
**Manufacturer:** Bivar
**MPN:** `3RD-F`
**Type:** 3 mm red THT LED

Current-limiting resistor:

```text
R_LED1 = 4.7 kΩ
```

Alternative approved LED colours or devices, where applicable, are documented in `ALTERNATE_PARTS.md`.

---

## 9.2 D7 — Autofire Status Indicator

**Reference:** D7
**Manufacturer:** Bivar
**MPN:** `3BC-3-F`
**Type:** 3 mm red/green dual-colour LED
**Configuration:** Common cathode

Validated pinout:

```text
Pin 1 -> RED anode
Pin 2 -> Common cathode -> GND
Pin 3 -> GREEN anode
```

Associated current-limiting resistors:

```text
R22 = 270 Ω
R23 = 330 Ω
```

The common-cathode configuration is required by the Rev1.5.1 LED-driver topology.

**Validation status: PASS**

---

## 9.3 D8–D15 — Key Backlight

**References:** D8–D15
**Manufacturer:** XINGLIGHT
**MPN:** `XL-2012WWC`
**Package:** 0805
**Colour:** Warm white
**JLCPCB/LCSC:** `C965820`

Quantity:

```text
8 per controller
```

Each LED uses an individual 3.3 kΩ current-limiting resistor:

```text
R24–R31 = 3.3 kΩ
```

The deliberately low LED current provides subtle key illumination rather than high-intensity decorative lighting.

---

# 10. Backlight Control

**Reference:** U3
**Manufacturer:** C&K
**MPN:** `PCM12SMTR`
**Type:** SMD slide switch
**PCB side:** Bottom

U3 enables or disables the key-backlight supply.

The component is located on the bottom side of the PCB and may be manually assembled depending on the selected manufacturing process.

---

# 11. Gameplay Switches

Revision 1.5.1 uses eight MX-compatible mechanical switches.

Preferred fitted switch:

**Gateron KS-8 Yellow**

Quantity:

```text
8 per controller
```

The mechanical switches are replaceable and are not soldered directly to the PCB.

---

# 12. MX Hot-Swap Sockets

**References:** SW1–SW8
**Manufacturer:** Kaihua / Kailh
**MPN:** `CPG151101S11`

Quantity:

```text
8 per controller
```

PCB side:

```text
Bottom
```

KiCad footprint:

```text
PCM_Switch_Keyboard_Hotswap_Kailh:SW_Hotswap_Kailh_MX
```

The sockets allow compatible MX-style mechanical switches to be replaced without soldering.

The hot-swap sockets and mechanical switches are separate physical BOM items.

---

# 13. Autofire Control Switches

Revision 1.5.1 uses two different E-Switch devices.

## SW_AUTO1 — Autofire Enable

**Manufacturer:** E-Switch
**MPN:** `100SP1T1B4M2QE`
**Assembly:** THT

Function:

```text
Autofire OFF / ON
```

## SW_SPEED1 — Autofire Speed

**Manufacturer:** E-Switch
**MPN:** `100SP3T1B1M2QEH`
**Type:** SPDT ON-OFF-ON
**Assembly:** THT

Function:

```text
LEFT  -> SLOW
RIGHT -> FAST
```

These are intentionally separate BOM items and shall not be treated as interchangeable solely because they belong to the same switch family.

---

# 14. DB9 Controller Cable

The controller uses a molded female DB9 controller cable with flying leads.

The PCB-side conductors are soldered directly to the J1 pads.

Cable conductors from a new supplier or production batch shall not be identified solely by insulation colour.

The first cable from each new batch should be continuity-tested against the required DB9 pinout before production assembly.

Detailed assembly instructions may be maintained separately under the project assembly documentation.

---

# 15. J1 Cable Interface

J1 consists of PCB solder pads rather than a separately procured connector.

Master BOM classification:

```text
PCB FEATURE / DNP
```

J1 therefore has no independent procurement MPN.

The DB9 cable is soldered directly to these PCB pads.

---

# 16. Assembly Classification

The Master BOM distinguishes between:

### Top SMD

Components intended for top-side surface-mount assembly.

### Bottom SMD

Includes:

* U3 backlight switch
* SW1–SW8 Kailh hot-swap sockets

These components may be manually installed depending on the manufacturing configuration.

### THT

Includes components such as:

* D1
* D2
* D7
* SW_AUTO1
* SW_SPEED1

### Mechanical / Manual

Includes the eight replaceable mechanical MX switches.

### Cable / Manual

Includes the external DB9 controller cable.

### PCB Feature / DNP

Includes J1 PCB solder-pad structures.

---

# 17. Manufacturing Data Policy

The files in this directory form the **Master engineering dataset**.

Manufacturing-house-specific files may be derived from them.

For example, a JLCPCB assembly BOM/CPL may intentionally exclude:

* THT components
* bottom-side manually assembled components
* mechanical switches
* external cables
* DNP PCB features

Such manufacturing subsets shall not replace or redefine the Master BOM.

---

# 18. Production Validation

Before production release, the Rev1.5.1 hardware shall satisfy the following checks:

* schematic ERC passes
* PCB DRC passes
* Gerber output reviewed
* drill files reviewed
* component footprints verified
* D4/D5 orientation and topology verified
* D6 orientation and topology verified
* D7 pinout verified
* D8–D15 LED polarity verified
* MMBT3904 symbol-to-footprint mapping verified
* 2N7002 symbol-to-footprint mapping verified
* U1 orientation verified
* U2 orientation verified
* DB9 cable pin mapping verified
* +5 V and GND continuity verified
* no VCC-GND short circuit
* autofire OFF verified
* autofire SLOW verified
* autofire FAST verified
* FIRE1 verified
* FIRE2 verified
* UP/DOWN/LEFT/RIGHT verified
* red/green autofire indication verified
* key backlight verified
* backlight ON/OFF control verified

---

# 19. Traceability

Component identity should be traced in the following order:

```text
Reference Designator
        ↓
Master BOM
        ↓
Manufacturer Part Number (MPN)
        ↓
DATASHEET_INDEX.md
        ↓
Manufacturer Datasheet
```

Where a JLCPCB/LCSC component is used for production assembly, its corresponding part number is additionally recorded in the Master BOM.

The **manufacturer part number remains the primary component identity**.

---

# 20. Document Authority

For Rev1.5.1:

**Component identity and procurement data**

→ `WASDPad_Rev1.5.1_FULL_MASTER_BOM.csv`

**Component placement data**

→ `WASDPad_Rev1.5.1_FULL_MASTER_CPL.csv`

**Datasheet references**

→ `DATASHEET_INDEX.md`

**Approved/evaluated substitutions**

→ `ALTERNATE_PARTS.md`

**Supplier and procurement guidance**

→ `PROCUREMENT_NOTES.md`

This README provides the human-readable overview of those engineering records.

---

# 21. Release Status

**Hardware Revision:** WASDPad+ Rev1.5.1
**BOM Documentation Version:** 1.0
**Status:** Production Release Candidate

The Rev1.5.1 component selection and PCB manufacturing dataset are complete.

Final promotion to **Production Approved** should follow successful assembly and full functional validation of the Rev1.5.1 production hardware.

---

# 22. Version History

| Document Version | Date           | Status                           | Changes                                                                                                                                                                                                                          |
| ---------------- | -------------- | -------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 0.1              | Not recorded   | Draft                            | Initial Revision 1.5 BOM structure                                                                                                                                                                                               |
| 0.5              | Not recorded   | Draft                            | Initial component grouping and candidate selection                                                                                                                                                                               |
| 0.8              | Not recorded   | Engineering Review               | Protection, timer, logic, hot-swap and LED component selection                                                                                                                                                                   |
| 0.9              | 2026-08-18     | Pre-Release Validated            | Consolidated pre-production component selections                                                                                                                                                                                 |
| **1.0**          | **2026-08-29** | **Production Release Candidate** | Updated to Rev1.5.1 Master BOM/CPL; production-selected TLC555, ESD/TVS devices and capacitors; added key backlight system and U3; corrected autofire switch MPNs; added manufacturing classification and datasheet traceability |
