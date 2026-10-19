# WASDPad+ Rev1.5.2 — Bill of Materials and Component Documentation

> **CURRENT RELEASE: Rev1.5.2 — FINAL PRODUCTION RELEASE.** A newly manufactured
> Rev1.5.2 controller passed the project owner's reported functional testing
> in October 2026, including the corrected FAST/SLOW selector. **The component
> BOM is unchanged from Rev1.5.1** (project-owner confirmation).
>
> **Publication policy:** The BOM, historical CPL, component datasheets,
> sourcing and compliance references are public. The **KiCad schematic,
> KiCad PCB layout and fabrication Gerber/drill/CAM files** are maintained
> privately and reserved for exclusive delivery to **Commodore**. Their absence
> from this public repository is intentional, not a missing engineering output.

**Document Version:** 2.0  
**Hardware Revision:** Rev1.5.2  
**Hardware Status:** Final Production Release — manufactured functional validation PASS  
**Compliance Evidence:** Research register; outstanding declarations flagged  
**Last Updated:** 2026-10-19

---

## 1. Purpose

This directory documents the **public component, placement-history, sourcing,
regulatory-reference and assembly-classification records** of WASDPad+
Rev1.5.2. The component selection is identical to Rev1.5.1. Rev1.5.2 corrects
the physical SPEED switch common-contact mapping in the schematic and PCB;
it does **not** introduce a BOM/MPN change. See the [release record](../REV1.5.2_MANUFACTURING_RELEASE_NOTES.md)
and the [SPEED selector erratum](../REV1.5.1_TO_REV1.5.2_SPEED_SELECTOR_ERRATUM.md).

The retained hardware platform includes:

* pure hardware directional, FIRE1/FIRE2 and FAST/SLOW autofire control
* resettable +5 V overcurrent, signal ESD and supply rail protection
* MX hot-swap sockets and replaceable mechanical switches
* dual-colour autofire status indication
* warm-white key backlighting and independent illumination control
* standardized passives, MPN traceability, BOM/CPL and datasheet references

**Rev1.5.2 requires no microcontroller, firmware or driver.**

---

## 2. BOM Files and Supporting Documentation

### 2.1 Directory layout

The datasheet and declaration indexes are in the **sibling `datasheets/` folder**, not in `bom/`:

```text
hardware/rev1.5/
├── REV1.5.2_MANUFACTURING_RELEASE_NOTES.md
├── datasheets/
│   ├── WASDPad_Rev1.5.1_DATASHEET_INDEX.md
│   └── WASDPad_Rev1.5.2_Regulatory_Declaration_URL_Index.md
└── bom/
    ├── README.md
    ├── WASDPad_Rev1.5.2_BOM_Compliance_Links.xlsx
    ├── WASDPad_Rev1.5.1_FULL_MASTER_BOM.csv
    ├── WASDPad_Rev1.5.1_FULL_MASTER_CPL.csv
    ├── ALTERNATE_PARTS.md
    └── PROCUREMENT_NOTES.md
```

### 2.2 Current Rev1.5.2 BOM and compliance Excel

**[WASDPad+ Rev1.5.2 BOM with Compliance Links (XLSX)](WASDPad_Rev1.5.2_BOM_Compliance_Links.xlsx)**

The workbook retains the **83 original BOM line items** and adds datasheet,
RoHS, REACH and evidence-quality references. The project owner confirms no
component-list changes between Rev1.5.1 and Rev1.5.2. It contains:

* **README** — purpose, provenance and evidence limitations
* **MPN Compliance** — evidence-source register covering **29 unique MPN entries**
* **BOM 83 rows** — designators, MPNs, quantities, footprints, assembly
  classes and matching compliance-source columns

**Scope:** The workbook is a **public BOM and compliance research register**,
not a signed declaration of conformity and not a complete production PCB
fabrication package. Where evidence is incomplete, the status is marked
pending, provisional or source-limited; such entries are not certified.

### 2.3 Historical Rev1.5.1 Master BOM (CSV)

**[WASDPad_Rev1.5.1_FULL_MASTER_BOM.csv](WASDPad_Rev1.5.1_FULL_MASTER_BOM.csv)**

The original Master BOM is retained unchanged for historical traceability.
It includes reference designators, MPNs, quantities, KiCad footprints,
component descriptions, supplier part numbers, PCB layer and assembly
classification, including SMD, THT, mechanical, cable and DNP/PCB-feature items.

The component identity was carried into Rev1.5.2 without MPN changes.
The Rev1.5.1 CSV itself is **not** a replacement for the controlled Rev1.5.2
fabrication and assembly handoff. If public documents disagree, reconcile
against the owner's approved final-revision component list.

### 2.4 Historical Rev1.5.1 Master CPL (CSV)

**[WASDPad_Rev1.5.1_FULL_MASTER_CPL.csv](WASDPad_Rev1.5.1_FULL_MASTER_CPL.csv)**

The historic placement list covers top/bottom SMD, THT, hot-swap and
manual-installation classes. It is **public** but is **not represented as a
separately verified Rev1.5.2 placement export**. Rev1.5.2 fabrication must
use the revision-matched, controlled production placement dataset.

### 2.5 Datasheets and regulatory evidence

* [Rev1.5.1 Datasheet Index](../datasheets/WASDPad_Rev1.5.1_DATASHEET_INDEX.md) —
  the technical references for the unchanged Rev1.5.2 component list.
* [Rev1.5.2 RoHS/REACH Declaration URL Index](../datasheets/WASDPad_Rev1.5.2_Regulatory_Declaration_URL_Index.md) —
  official manufacturer declarations, product-status pages, distributor
  indicators and items that still require specific supplier evidence.

A datasheet, distributor product badge, manufacturer-status page and signed
MPN-specific declaration are **different evidence classes**. They must not
be conflated when reviewing compliance.

### 2.6 Other documentation

* [ALTERNATE_PARTS.md](ALTERNATE_PARTS.md) — evaluated substitute parts and
  requirements for checking function, pinout, polarity and footprint.
* [PROCUREMENT_NOTES.md](PROCUREMENT_NOTES.md) — sourcing, suppliers,
  lifecycle and purchasing guidance.
* [Rev1.5.2 Manufacturing Release Notes](../REV1.5.2_MANUFACTURING_RELEASE_NOTES.md) —
  release status, speed-switch correction and first-article validation.

---

## 3. Rev1.5.2 Component Status

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

## 4. Core Active Components

### 4.1 Autofire Timer

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

The TLC555CDR remains the production-selected timer for Rev1.5.2; its MPN is unchanged from Rev1.5.1.

It replaces the ICM7555 used during earlier development while preserving the CMOS 555 operating principle and required pin compatibility.

Bipolar NE555-family devices are not preferred because of their higher supply-current characteristics.

---

### 4.2 Bilateral Switching Logic

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

The CD4066 provides hardware switching for the autofire speed-selection circuitry. Rev1.5.2 corrects the SPEED switch common-contact schematic/PCB mapping; no component substitution was required.

---

### 4.3 MOSFET Logic

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

### 4.4 Autofire Status Drivers

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

## 5. Autofire Timing

Rev1.5.2 provides two fixed hardware autofire speeds.

| Reference |  Value | Function |
| --------- | -----: | -------- |
| R13       | 330 kΩ | FAST     |
| R14       | 680 kΩ | SLOW     |

The values were selected through physical gameplay testing and retained for Rev1.5.2.

User-facing switch behaviour:

```text
LEFT  -> SLOW
RIGHT -> FAST
```

These values supersede earlier experimental autofire timing values.

---

## 6. Passive Component Standardization

### 6.1 Resistors

General SMD resistors are standardized on the **YAGEO RC1206FR-07** family wherever practical.

General characteristics:

* 1206 / 3216 metric
* thick film
* ±1 %
* 0.25 W
* SMD

Values used in Rev1.5.2 include:

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

### 6.2 Capacitors

#### C1

**MPN:** `1206B224K500NT`
**Value:** 220 nF
**Dielectric:** X7R
**Package:** 1206
**JLCPCB/LCSC:** `C1857`

Used as a timing capacitor.

#### C2, C3

**Manufacturer:** Samsung Electro-Mechanics
**MPN:** `CL31B104KBCNNNC`
**Value:** 100 nF
**Dielectric:** X7R
**Package:** 1206
**JLCPCB/LCSC:** `C24497`

#### VCC-GND-Decoupling1

**Manufacturer:** YAGEO
**MPN:** `CC1206KRX7R8BB104`
**Value:** 100 nF
**Dielectric:** X7R
**Package:** 1206
**JLCPCB/LCSC:** `C527347`

The dedicated VCC-GND decoupling capacitor shall be located close to the relevant IC supply connections.

---

## 7. Overcurrent Protection

**Reference:** F2
**Manufacturer:** Littelfuse
**MPN:** `1206L005/30WR`
**Type:** Resettable PPTC
**Package:** 1206
**JLCPCB/LCSC:** `C3760487`

F2 protects the controller-port +5 V supply path.

The protection value was selected with the available current from the target retro-computer controller interface in mind.

---

## 8. ESD Protection

### 8.1 D4 and D5 — DB9 Signal Protection

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

### 8.2 D6 — +5 V Protection

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

Protection-device pin mapping originally validated during Rev1.5.1 engineering:

```text
Pin 1 -> protected +5 V rail
Pin 2 -> NC
Pin 3 -> GND
```

The production-selected TPE0562BC3 differs internally from the originally evaluated PESD6V0L2UU device.

It remains the specified protection component for Rev1.5.2 rather than an uncontrolled generic substitution.

**Validation status: PASS**

---

## 9. LED System

### 9.1 D1 — Power Indicator

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

### 9.2 D7 — Autofire Status Indicator

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

The common-cathode configuration is required by the Rev1.5.2 LED-driver topology.

**Validation status: PASS**

---

### 9.3 D8–D15 — Key Backlight

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

## 10. Backlight Control

**Reference:** U3
**Manufacturer:** C&K
**MPN:** `PCM12SMTR`
**Type:** SMD slide switch
**PCB side:** Bottom

U3 enables or disables the key-backlight supply.

The component is located on the bottom side of the PCB and may be manually assembled depending on the selected manufacturing process.

---

## 11. Gameplay Switches

Rev1.5.2 uses eight MX-compatible mechanical switches.

Preferred fitted switch:

**Gateron KS-8 Yellow**

Quantity:

```text
8 per controller
```

The mechanical switches are replaceable and are not soldered directly to the PCB.

---

## 12. MX Hot-Swap Sockets

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

## 13. Autofire Control Switches

Rev1.5.2 uses two different E-Switch devices.

### SW_AUTO1 — Autofire Enable

**Manufacturer:** E-Switch
**MPN:** `100SP1T1B4M2QE`
**Assembly:** THT

Function:

```text
Autofire OFF / ON
```

### SW_SPEED1 — Autofire Speed

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

## 14. DB9 Controller Cable

The controller uses a molded female DB9 controller cable with flying leads.

The PCB-side conductors are soldered directly to the J1 pads.

Cable conductors from a new supplier or production batch shall not be identified solely by insulation colour.

The first cable from each new batch should be continuity-tested against the required DB9 pinout before production assembly.

Detailed assembly instructions may be maintained separately under the project assembly documentation.

---

## 15. J1 Cable Interface

J1 consists of PCB solder pads rather than a separately procured connector.

Master BOM classification:

```text
PCB FEATURE / DNP
```

J1 therefore has no independent procurement MPN.

The DB9 cable is soldered directly to these PCB pads.

---

## 16. Assembly Classification

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

## 17. Public BOM and Private Design-File Policy

WASDPad+ publishes its **component BOM, historical CPL, datasheets, evaluated
alternates, procurement information and compliance evidence references**.

The **schematic source (`.kicad_sch`), PCB layout (`.kicad_pcb`) and fabrication
outputs (Gerber, drill and other CAM data)** are deliberately maintained
outside the public repository and are reserved for **exclusive delivery to
Commodore**. They exist as part of the finished Rev1.5.2 hardware development;
non-public distribution does not imply incomplete engineering.

For production control:

* A public BOM or historical CPL is **not** a complete fabrication package.
* Rev1.5.1 fabrication data shall not be reused as a Rev1.5.2 manufacturing
  source without an explicit revision verification.
* Actual Rev1.5.2 fabrication and assembly must use matching controlled
  final-revision documentation, including the SPEED common-pin correction.
* Assembly-house-specific BOM/CPL subsets may omit manually fitted THT items,
  bottom-side components, mechanical switches, cables and DNP PCB features.
  Such subsets do not change the identity of the approved components.

---

## 18. Hardware Validation and Quality Checks

**Rev1.5.2 — Final Production Release.** The project owner confirmed a
successful complete functional test of an **actually manufactured Rev1.5.2**
controller in October 2026, including both FAST and SLOW autofire settings.
An earlier Rev1.5.1 board was separately repaired and tested as part of
historic corrective action.

The following checklist remains relevant to production acceptance. It is not
an assertion that every check's detailed test log or every future unit's QA
record is published on GitHub:

* final schematic ERC, PCB DRC, Gerber and drill release reviews
* component footprint, mounting orientation and board-revision checks
* D4/D5 signal ESD topology and orientation
* D6 rail-protection topology and orientation
* D7 common-cathode LED pinout and D8–D15 backlight polarity
* MMBT3904/2N7002 pin mappings and U1/U2 orientations
* physical SPEED switch **pad 2 COMMON**, pad 1 FAST, pad 3 SLOW mapping
* cable-to-DB9 continuity testing independent of insulation colour
* +5 V/GND continuity and absence of supply short circuits
* autofire OFF, FAST, SLOW, FIRE1, FIRE2, UP/DOWN/LEFT/RIGHT
* red/green autofire status and backlight ON/OFF control

Future production batches and individual controllers still require routine
incoming, assembly and end-of-line acceptance. Regulatory documentation
verification is a **separate activity** from completed hardware functional
validation, and does not change the Final Production Release designation.

Supporting documents:

* [Rev1.5.2 Manufacturing Release Notes](../REV1.5.2_MANUFACTURING_RELEASE_NOTES.md)
* [SPEED Selector Erratum](../REV1.5.1_TO_REV1.5.2_SPEED_SELECTOR_ERRATUM.md)
* [Assembly and Manufacturing Procedure](../../../docs/assembly/ASSEMBLY.md)

---

## 19. Component and Regulatory Evidence Traceability

```text
Reference Designator
        |
        v
Rev1.5.2 BOM Excel (unchanged Rev1.5.1 component baseline)
        |
        v
Manufacturer Part Number / approved procurement item
        |
        +--> Datasheet Index --> technical specification
        |
        +--> RoHS/REACH Evidence Index --> source URL / evidence class / status
```

Do not treat a manufacturer product-status page, distributor "RoHS" label or
family-wide policy as an exact-MPN signed declaration without verification.
Where only limited evidence is available, its status remains **pending** or
**provisional** until valid current supplier documentation is obtained.

**Specific caveat:** The E-Switch 100 series regulatory source identifies a
RoHS **6(c)** exemption and reports **lead as REACH SVHC above 0.1%** within
its stated scope. It must not be presented as unconditionally lead-free or
SVHC-free. Confirm the applicable version, scope and market requirements
before making a finished-product compliance claim.

Generic descriptions without a fixed supplier/MPN (such as the 1N4148 diode
and DB9 cable) require supplier-specific verification. J1 is a PCB copper
feature, not a purchased component; PCB materials and finishes are covered by
fabrication-process controls rather than an independent J1 part certificate.

**Neither the BOM workbook nor this README is a signed declaration of
conformity or a CE certificate for the finished controller.**

---

## 20. Document Authority

| Subject | Document / disposition |
| --- | --- |
| Final hardware revision | **Rev1.5.2 — Final Production Release**; [manufacturing release notes](../REV1.5.2_MANUFACTURING_RELEASE_NOTES.md) |
| Current public component reference | [Rev1.5.2 BOM + Compliance Excel](WASDPad_Rev1.5.2_BOM_Compliance_Links.xlsx); unchanged component list |
| Historical component baseline | [Rev1.5.1 Master BOM CSV](WASDPad_Rev1.5.1_FULL_MASTER_BOM.csv) |
| Historical placement data | [Rev1.5.1 Master CPL CSV](WASDPad_Rev1.5.1_FULL_MASTER_CPL.csv) |
| Technical datasheets | [Rev1.5.1 Datasheet Index](../datasheets/WASDPad_Rev1.5.1_DATASHEET_INDEX.md); retained component MPNs |
| RoHS/REACH references | [Rev1.5.2 Declaration URL Index](../datasheets/WASDPad_Rev1.5.2_Regulatory_Declaration_URL_Index.md); evidence register, not a certificate |
| Component substitutions | [ALTERNATE_PARTS.md](ALTERNATE_PARTS.md) |
| Supplier and procurement rules | [PROCUREMENT_NOTES.md](PROCUREMENT_NOTES.md) |
| Controlled schematic, PCB, Gerber and drill data | **Private; exclusive handoff to Commodore** |

The project owner's **controlled, final Rev1.5.2 design and matching production
handoff package** is authoritative for PCB fabrication, net connectivity and
revision-specific assembly. Public component records support technical
transparency and sourcing traceability; they do not override the final design.

---

## 21. Release and Compliance Status

**Hardware Revision:** WASDPad+ Rev1.5.2  
**BOM Documentation Version:** 2.0  
**Hardware Status:** **FINAL PRODUCTION RELEASE — manufactured functional validation PASS** (project-owner report, October 2026)  
**BOM Changes from Rev1.5.1:** **None** (project-owner confirmation)  
**Regulatory Evidence Status:** Some exact-MPN declarations remain pending or provisional

Rev1.5.2 implements the verified SPEED switch common-pad correction in the
schematic, PCB and final fabrication outputs. The manufactured controller
has passed the reported complete functional test. The design files and
Gerbers remain private, while BOM and regulatory-document references are
publicly accessible.

---

## 22. Version History

| Document Version | Date | Status | Changes |
| --- | --- | --- | --- |
| 0.1 | Not recorded | Draft | Initial Rev1.5 BOM structure |
| 0.5 | Not recorded | Draft | Candidate component groupings and early selection |
| 0.8 | Not recorded | Engineering Review | Protection, timer, logic, hot-swap and LED part selection |
| 0.9 | 2026-08-18 | Pre-Release Validated | Consolidated pre-production parts |
| **1.0** | **2026-08-29** | **Rev1.5.1 Production Release Candidate (historical)** | Established Rev1.5.1 Master BOM/CPL; selected TLC555, protection parts and capacitors; backlighting/U3, corrected autofire switch MPNs, manufacturing classification and datasheet traceability |
| **2.0** | **2026-10-19** | **Rev1.5.2 Final Production Release** | Updated entire README to manufactured and validated Rev1.5.2 status; linked public BOM/compliance Excel and RoHS/REACH index; clarified historic BOM/CPL provenance and the private schematic/PCB/Gerber distribution policy |
