# WASDPad+ Revision 1.5.1

## Approved Alternate Parts

**Document Version:** 1.0
**Hardware Revision:** Rev1.5.1
**Status:** Production Release Candidate
**Last Updated:** 2026-08-29

---

# 1. Purpose

This document defines the component-substitution policy and records approved, validated, legacy and candidate alternate components for **WASDPad+ Hardware Revision 1.5.1**.

The authoritative production component identity is maintained in:

`WASDPad_Rev1.5.1_FULL_MASTER_BOM.csv`

This document does not replace the Master BOM.

Its purpose is to define which components may be substituted and which technical checks are required before an alternate component may be used.

---

# 2. General Substitution Policy

A component shall not be considered interchangeable solely because it has:

* the same generic component name
* the same nominal electrical value
* a visually similar package
* a similar manufacturer description
* the same number of pins
* the same general function

Before an alternate component is approved, all relevant electrical, mechanical and functional characteristics shall be verified.

At minimum:

* electrical ratings
* operating voltage
* current capability
* power rating
* tolerance
* temperature range
* package
* footprint
* pin numbering
* pinout
* polarity
* mechanical dimensions
* functional behaviour
* timing behaviour where applicable
* protection topology where applicable
* availability from a recognized supplier

No alternate part may introduce measurable degradation in:

* controller compatibility
* input latency
* autofire timing stability
* signal integrity
* protection level
* mechanical reliability

---

# 3. Status Definitions

Alternate components are classified using the following status levels.

| Status                 | Meaning                                                                                              |
| ---------------------- | ---------------------------------------------------------------------------------------------------- |
| **Production Primary** | Component specified by the current Rev1.5.1 Master BOM                                               |
| **Approved Alternate** | Electrically, mechanically and functionally verified as a replacement                                |
| **Legacy Validated**   | Component used or validated during earlier WASDPad development and considered technically compatible |
| **Candidate**          | Potential replacement requiring verification before production use                                   |
| **Not Approved**       | Component known to be unsuitable or not permitted without redesign                                   |
| **Not Evaluated**      | No compatibility determination has been made                                                         |

The Master BOM always defines the **Production Primary** component.

---

# 4. Integrated Circuits

## 4.1 U1 — CMOS Autofire Timer

### Production Primary

**Texas Instruments `TLC555CDR`**

Requirements for any alternate:

* CMOS 555 architecture
* compatible SOIC-8 footprint
* standard 555 pinout
* reliable operation from +5 V
* astable-mode compatibility
* compatible timing behaviour with the existing R/C network
* no significant increase in controller-port current consumption

### Legacy Validated Alternate

**Renesas / Intersil `ICM7555CBAZ`**

Status:

**Legacy Validated**

The ICM7555 was used during earlier WASDPad development and implements the same CMOS 555 operating principle.

It remains a technically suitable alternate subject to availability and package/pinout verification.

### Generic TLC555 / LMC555 / CMOS 555 Families

Status:

**Candidate**

A generic CMOS 555 shall not automatically be substituted.

The exact manufacturer MPN must be verified for:

* operating voltage
* supply current
* output characteristics
* package
* pinout
* timing behaviour

### Bipolar NE555 Family

Status:

**Not Approved as Drop-In Production Alternate**

Classic bipolar NE555 devices are not preferred because of their significantly higher supply-current characteristics.

Use would require explicit electrical review.

---

## 4.2 U2 — Quad Bilateral CMOS Switch

### Production Primary

**Texas Instruments `CD4066BM96`**

Any alternate must provide:

* CD4066-compatible functionality
* +5 V operation
* compatible SOIC-14 package
* identical pinout
* suitable ON resistance
* suitable switching characteristics

### Other CD4066B-Compatible Devices

Status:

**Candidate**

Possible manufacturers may include other established semiconductor vendors.

The exact MPN must be validated before production use.

HC4066-family devices shall not automatically be treated as equivalent to CD4066B without electrical review.

---

# 5. MOSFETs and Transistors

## 5.1 Q1–Q7 — N-Channel MOSFET

### Production Primary

**onsemi `2N7002LT1G`**

Requirements for an alternate:

* N-channel enhancement MOSFET
* compatible operation at the available gate voltage
* SOT-23 footprint compatibility
* correct pin mapping
* adequate VDS rating
* adequate ID rating
* sufficiently low leakage
* suitable logic switching behaviour

### Generic 2N7002

Status:

**Candidate**

`2N7002` is a generic device family and manufacturer pinout/package details must be checked.

A substitute shall not be approved based only on the `2N7002` name.

Particularly verify:

```text
Pin 1 = Gate
Pin 2 = Source
Pin 3 = Drain
```

against the actual selected manufacturer datasheet and PCB footprint.

---

## 5.2 Q8–Q9 — NPN Status LED Drivers

### Production Primary

**onsemi `MMBT3904LT1G`**

Requirements for an alternate:

* NPN bipolar transistor
* SOT-23 footprint compatibility
* suitable collector current
* suitable VCE rating
* compatible gain characteristics
* correct pin mapping

Required Rev1.5.1 mapping:

```text
Pin 1 = Base
Pin 2 = Emitter
Pin 3 = Collector
```

### Generic MMBT3904

Status:

**Candidate**

The exact manufacturer datasheet must be checked before substitution.

---

# 6. Protection Components

Protection components require stricter substitution control than ordinary passive components.

A replacement shall not be approved solely from:

* working voltage
* package name
* ESD rating
* number of protected channels

The **internal protection topology and pin mapping must also be verified**.

---

## 6.1 D4 / D5 — DB9 Signal ESD Protection

### Production Primary

**TECH PUBLIC `PESD5V0S4UD`**

JLCPCB/LCSC:

`C2987082`

Package:

SC-74-6 / SOT-23-6 compatible

Validated topology/pin mapping:

```text
Pin 1 = K1
Pin 2 = Common Anode
Pin 3 = K2
Pin 4 = K3
Pin 5 = Common Anode
Pin 6 = K4
```

Status:

**Production Primary / Validated**

### Nexperia `PESD5V0S4UD,115`

Status:

**Legacy Validated Alternate**

This device formed the basis of the original protection design.

Before substitution, verify the exact ordering suffix, package and datasheet pinout.

### Other Quad-Line 5 V ESD Arrays

Status:

**Candidate**

Required checks:

* working voltage
* breakdown voltage
* clamping behaviour
* capacitance
* ESD rating
* number of channels
* package
* common-anode topology
* exact pin mapping

A topology mismatch is grounds for rejection even if the electrical ratings appear similar.

---

## 6.2 D6 — +5 V ESD / TVS Protection

### Production Primary

**TECH PUBLIC `TPE0562BC3`**

JLCPCB/LCSC:

`C2841389`

Package:

SOT-323 / SC-70

Validated Rev1.5.1 PCB connection:

```text
Pin 1 = Protected +5 V rail
Pin 2 = NC
Pin 3 = GND
```

Status:

**Production Primary / Specifically Validated**

The TPE0562BC3 is a bidirectional protection device and its internal topology differs from the device originally evaluated during Rev1.5 development.

It shall therefore be treated as a specifically validated Rev1.5.1 component.

### Nexperia `PESD6V0L2UU,115`

Status:

**Legacy Design Reference — Not Automatic Drop-In**

This device was evaluated during the original protection design.

Because its internal topology differs from the current production-selected TPE0562BC3, it shall **not** be treated as an uncontrolled interchangeable replacement.

Any return to this device requires verification against the actual Rev1.5.1 schematic and PCB connection.

### Other 5 V TVS / ESD Devices

Status:

**Candidate**

Required verification:

* unidirectional/bidirectional topology
* pin mapping
* working voltage
* breakdown voltage
* clamping voltage
* surge/ESD capability
* package
* PCB connection

---

# 7. Resettable Fuse

## F2 — +5 V Input Protection

### Production Primary

**Littelfuse `1206L005/30WR`**

Requirements for an alternate:

* resettable PPTC technology
* 1206 footprint compatibility
* comparable hold current
* comparable trip current
* suitable maximum voltage
* suitable trip characteristics
* suitable resistance
* appropriate behaviour with the retro-computer controller-port +5 V supply

### Other 1206 PPTC Devices

Status:

**Candidate**

A replacement must be selected from electrical characteristics rather than package and current marking alone.

---

# 8. Diodes

## D2 — Small-Signal Switching Diode

### Production Primary

**`1N4148` THT**

Package:

DO-35

Status:

**Production Primary**

Because `1N4148` is an industry-standard generic designation, qualified manufacturer versions may be used provided that the electrical ratings and physical package are compatible.

### `1N4148W`

Status:

**Not a Direct PCB Alternate**

The 1N4148W is commonly supplied in an SMD package.

It may be electrically suitable but is **not footprint-compatible** with the Rev1.5.1 THT DO-35 position.

Using it would require PCB or assembly adaptation.

---

# 9. Capacitors

## 9.1 C1 — Autofire Timing Capacitor

### Production Primary

**Walsin `1206B224K500NT`**

Nominal specification:

* 220 nF
* 50 V
* X7R
* ±10 %
* 1206

Any alternate shall maintain:

* 220 nF nominal capacitance
* X7R or electrically suitable stable dielectric
* compatible tolerance
* voltage rating ≥ required circuit voltage
* 1206 footprint

Because C1 influences autofire timing, large tolerance or dielectric changes are not permitted without timing verification.

### Earlier KEMET Timing Capacitor

Status:

**Legacy Validated Alternate**

An electrically equivalent 220 nF / 1206 / X7R KEMET device used during development may remain acceptable provided the exact MPN, tolerance and voltage rating are verified.

---

## 9.2 C2 / C3 — 100 nF Capacitors

### Production Primary

**Samsung Electro-Mechanics `CL31B104KBCNNNC`**

Specification:

* 100 nF
* 50 V
* X7R
* 1206

### Equivalent 100 nF X7R 1206 MLCC

Status:

**Candidate**

Requirements:

* 100 nF
* X7R
* 1206
* suitable tolerance
* voltage rating safely above +5 V

---

## 9.3 VCC-GND-Decoupling1

### Production Primary

**YAGEO `CC1206KRX7R8BB104`**

Specification:

* 100 nF
* X7R
* 1206

### Equivalent 100 nF X7R 1206 MLCC

Status:

**Candidate**

Any replacement shall provide suitable high-frequency local decoupling performance.

---

# 10. Resistors

## Production Primary Family

**YAGEO `RC1206FR-07` series**

The Rev1.5.1 Master BOM standardizes SMD resistors on this family wherever practical.

Typical characteristics:

* 1206
* thick film
* ±1 %
* 0.25 W

Production values include:

* 270 Ω
* 330 Ω
* 3.3 kΩ
* 4.7 kΩ
* 10 kΩ
* 100 kΩ
* 330 kΩ
* 680 kΩ

### Equivalent 1206 Resistors

Status:

**Candidate / Generally Acceptable After Verification**

An alternate resistor shall match:

* nominal resistance
* footprint
* tolerance equal to or better than required
* power rating equal to or greater than required
* suitable voltage rating

### Timing Resistors R13 / R14

Additional restriction applies.

```text
R13 = 330 kΩ FAST
R14 = 680 kΩ SLOW
```

These values are part of the validated autofire behaviour.

Alternate values shall **not** be substituted without gameplay and timing validation.

---

# 11. Status LEDs

## 11.1 D1 — Power LED

### Production Primary

**Bivar `3RD-F`**

Type:

3 mm red THT LED

Status:

**Production Primary**

Other colours or compatible 3 mm THT LEDs may be technically possible, but forward voltage, polarity, mechanical dimensions and resulting brightness with `R_LED1 = 4.7 kΩ` shall be verified.

### Alternative Colour LEDs

Status:

**Candidate / Cosmetic Variant**

A colour change is considered a product variant rather than an uncontrolled component substitution.

---

## 11.2 D7 — Dual-Colour Autofire Status LED

### Production Primary

**Bivar `3BC-3-F`**

Type:

3 mm red/green bi-colour THT LED

Required configuration:

**Common cathode**

Required pinout:

```text
Pin 1 = Red anode
Pin 2 = Common cathode
Pin 3 = Green anode
```

Status:

**Production Primary / Validated**

### Other 3 mm Red/Green Bi-Colour LEDs

Status:

**Candidate**

Any replacement must be verified for:

* common-cathode architecture
* exact pin numbering
* physical lead spacing
* body diameter
* red forward voltage
* green forward voltage
* brightness
* viewing angle

A common-anode LED is **not** a drop-in replacement.

---

# 12. Key Backlight LEDs

## D8–D15

### Production Primary

**XINGLIGHT `XL-2012WWC`**

JLCPCB/LCSC:

`C965820`

Specification:

* 0805
* warm white
* approximately 2500–3100 K
* wide viewing angle

Status:

**Production Primary**

The Rev1.5.1 circuit intentionally operates these LEDs at a low current through individual 3.3 kΩ resistors to produce subtle backlighting.

### Other 0805 White / Warm-White LEDs

Status:

**Candidate**

Required verification:

* 0805 footprint
* polarity / pad orientation
* forward voltage
* brightness at low current
* colour temperature
* viewing angle

A significantly higher-efficiency LED may alter the intended visual appearance even if electrically compatible.

---

# 13. Backlight Switch

## U3

### Production Primary

**C&K `PCM12SMTR`**

Type:

SMD slide switch

PCB side:

Bottom

Status:

**Production Primary**

An alternate must match:

* switching function
* contact arrangement
* PCB footprint
* pad geometry
* actuator direction
* actuator height
* mechanical accessibility through the enclosure

Mechanical compatibility with the enclosure is mandatory.

---

# 14. Autofire Control Switches

## 14.1 SW_AUTO1 — Autofire ON/OFF

### Production Primary

**E-Switch `100SP1T1B4M2QE`**

Status:

**Production Primary / Validated**

Any alternate must match:

* electrical switching function
* THT footprint
* pin spacing
* body dimensions
* actuator dimensions
* mounting geometry
* enclosure clearance

---

## 14.2 SW_SPEED1 — Autofire Speed Selector

### Production Primary

**E-Switch `100SP3T1B1M2QEH`**

Type:

SPDT ON-OFF-ON

Status:

**Production Primary / Validated**

Function:

```text
LEFT  = SLOW
RIGHT = FAST
```

An alternate must reproduce the required switching behaviour and mechanical footprint.

`SW_AUTO1` and `SW_SPEED1` use different MPNs and shall not be treated as interchangeable.

---

# 15. MX Hot-Swap Sockets

## SW1–SW8

### Production Primary

**Kailh / Kaihua `CPG151101S11`**

Type:

MX-compatible PCB hot-swap socket

PCB side:

Bottom

Quantity:

8

Status:

**Production Primary**

An alternate hot-swap socket must be verified for:

* PCB footprint
* pad geometry
* switch-pin contact position
* retention force
* PCB thickness compatibility
* mechanical switch compatibility
* enclosure clearance

Hot-swap sockets from another manufacturer shall not be assumed mechanically interchangeable.

---

# 16. Mechanical Key Switches

## Production Fitted Switch

**Gateron KS-8 Yellow**

Status:

**Production Primary / Replaceable Mechanical Component**

The mechanical key switches are user-replaceable through the Kailh hot-swap sockets.

Because they are not permanently soldered to the PCB, a broader range of compatible MX-style switches may be used.

---

## Cherry MX-Compatible Switches

Status:

**Approved Mechanical Family Subject to Fit**

Compatible Cherry MX switches may be used provided that:

* switch pin geometry matches
* center post geometry is compatible
* switch body clears the enclosure
* keycap interface is compatible
* Kailh socket insertion does not require excessive force

---

## Other Gateron MX-Compatible Switches

Status:

**Approved Mechanical Family Subject to Fit**

Different Gateron MX-compatible switch types may be used as user-selectable variants.

Switch force and feel are user-experience parameters rather than electrical compatibility parameters.

---

## Kailh MX-Compatible Mechanical Switches

Status:

**Candidate / Mechanical Verification Required**

Do not confuse **Kailh mechanical switches** with the production-selected **Kailh CPG151101S11 hot-swap socket**.

Exact switch geometry must be checked.

---

## TTC MX-Compatible Mechanical Switches

Status:

**Candidate**

Mechanical fit must be verified.

---

## Outemu MX-Compatible Mechanical Switches

Status:

**Candidate**

Outemu switch-pin dimensions may differ from other MX-style switches.

Socket compatibility must be verified before approval.

---

# 17. DB9 Controller Cable

## Production Requirement

The Rev1.5.1 Master BOM specifies a molded female DB9 controller cable with nine flying leads.

The exact production cable supplier/MPN may vary until a permanent supplier is frozen.

Status:

**Supplier-Controlled Component**

Any replacement cable must be verified for:

* female DB9 connector
* correct number of conductors
* adequate conductor gauge
* adequate insulation
* suitable cable flexibility
* strain relief
* connector mechanical quality
* continuity
* pin-to-wire mapping

Wire insulation colour shall not be assumed to identify DB9 pin numbers.

The first cable from each new supplier or production batch should be continuity-tested.

---

# 18. PCB Interface J1

J1 is a PCB solder-pad interface and is not a separately purchased component.

Status:

**PCB Feature / DNP**

No alternate component is applicable.

---

# 19. Components Requiring Special Approval

The following component classes shall **not** be substituted without explicit engineering review:

1. D4 / D5 ESD protection arrays
2. D6 +5 V ESD/TVS protection
3. U1 autofire timer
4. U2 bilateral switch
5. Q1–Q7 MOSFETs where pin mapping differs
6. Q8/Q9 transistors where pin mapping differs
7. D7 dual-colour status LED
8. F2 resettable fuse
9. R13 / R14 autofire timing resistors
10. U3 where mechanical dimensions differ
11. SW_AUTO1 / SW_SPEED1 where switching topology differs
12. Kailh hot-swap sockets where PCB geometry differs

---

# 20. Alternate-Part Approval Procedure

Before a new alternate MPN is added to this document:

1. Obtain the manufacturer datasheet.
2. Record manufacturer and exact MPN.
3. Compare electrical specifications against the Production Primary.
4. Compare package and physical dimensions.
5. Verify pin numbering and pinout.
6. Verify PCB footprint compatibility.
7. Verify polarity where applicable.
8. Verify internal topology for protection devices.
9. Verify mechanical fit for switches, sockets and LEDs.
10. Update the Master BOM only if the alternate becomes the new production-selected component.
11. Update `DATASHEET_INDEX.md`.
12. Perform functional testing where the component can influence timing, latency, protection or user interaction.
13. Record the approval status in this document.

---

# 21. Manufacturing Substitutions

PCB assembly suppliers may propose component substitutions because of:

* stock shortages
* minimum order quantities
* lifecycle changes
* supplier changes
* extended lead times

A manufacturing-house substitution is **not automatically approved**.

The proposed MPN shall be evaluated using the rules in this document before assembly.

For ordinary passive components, verification may be straightforward.

For:

* semiconductors
* ESD/TVS devices
* switches
* LEDs
* hot-swap sockets
* timing components

explicit engineering review is required.

---

# 22. Documentation Authority

The following document hierarchy applies:

```text
Production component identity
        ↓
WASDPad_Rev1.5.1_FULL_MASTER_BOM.csv

Component placement
        ↓
WASDPad_Rev1.5.1_FULL_MASTER_CPL.csv

Datasheets
        ↓
DATASHEET_INDEX.md

Approved substitutions
        ↓
ALTERNATE_PARTS.md

Supplier / sourcing information
        ↓
PROCUREMENT_NOTES.md
```

If an alternate listed here becomes the standard production component, the **Master BOM must be updated first**.

---

# 23. Version History

| Version | Date           | Status                           | Changes                                                                                                                                                                                                                                                                                 |
| ------- | -------------- | -------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 0.1     | Not recorded   | Draft                            | Initial alternate-part policy and candidate mechanical switches                                                                                                                                                                                                                         |
| **1.0** | **2026-08-29** | **Production Release Candidate** | Rebuilt against Rev1.5.1 Master BOM; TLC555 established as production timer; production ESD/TVS devices documented; capacitors, transistors, LEDs, backlight system, switches and hot-swap sockets added; mechanical-switch policy expanded; substitution approval procedure formalized |
