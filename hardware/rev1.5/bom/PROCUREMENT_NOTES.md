# WASDPad+ Revision 1.5.1

## Procurement and Component Sourcing Notes

**Document Version:** 1.0
**Hardware Revision:** Rev1.5.1
**Status:** Production Release Candidate
**Last Updated:** 2026-08-29

---

# 1. Purpose

This document defines the procurement, sourcing, supplier-control and component-lifecycle policy for **WASDPad+ Hardware Revision 1.5.1**.

The authoritative production component list is:

`WASDPad_Rev1.5.1_FULL_MASTER_BOM.csv`

This document supplements the Master BOM with sourcing and procurement rules.

It does not redefine component identity.

If information in this document conflicts with the Master BOM, the **Master BOM takes precedence**.

---

# 2. Related Documents

The Rev1.5.1 procurement documentation consists of:

```text
WASDPad_Rev1.5.1_FULL_MASTER_BOM.csv
WASDPad_Rev1.5.1_FULL_MASTER_CPL.csv
DATASHEET_INDEX.md
ALTERNATE_PARTS.md
PROCUREMENT_NOTES.md
```

Document responsibilities:

| Document             | Purpose                                          |
| -------------------- | ------------------------------------------------ |
| Master BOM           | Authoritative component identity and MPN         |
| Master CPL           | Component placement and assembly information     |
| DATASHEET_INDEX.md   | Manufacturer datasheets and technical references |
| ALTERNATE_PARTS.md   | Approved, validated and candidate substitutions  |
| PROCUREMENT_NOTES.md | Supplier, sourcing and lifecycle policy          |

---

# 3. General Procurement Principles

Components should preferably be:

* sourced from recognized manufacturers
* sourced from authorized or traceable distributors
* active and not obsolete
* suitable for long-term production
* available in prototype quantities
* available in production quantities
* supplied with manufacturer identification
* supplied with an identifiable MPN
* supported by a manufacturer datasheet
* compatible with the validated PCB footprint
* compatible with the intended assembly process
* RoHS compliant where applicable
* supported by compliance documentation where reasonably available

For production batches, traceability is preferred over obtaining the absolute lowest component price.

---

# 4. Preferred Procurement Sources

Preferred sources include recognized distributors and manufacturing supply chains such as:

* Mouser
* DigiKey
* Farnell / element14
* TME
* RS
* LCSC
* JLCPCB Parts

Direct manufacturer sourcing may also be used where appropriate.

Other suppliers may be used provided that:

* manufacturer identity is known
* exact MPN is known
* component authenticity is reasonably traceable
* the supplied device matches the approved specification

---

# 5. Marketplace Components

Marketplace-only sourcing should be avoided for:

* ESD protection devices
* TVS devices
* resettable fuses
* integrated circuits
* MOSFETs
* transistors
* safety/protection-related components

unless component authenticity and specification can be verified.

Marketplace sourcing may be acceptable for lower-risk mechanical items where electrical safety and signal integrity are not affected, but mechanical compatibility shall still be verified.

---

# 6. Production Component Identity

Every production component should be identified primarily by:

```text
Manufacturer
+
Manufacturer Part Number (MPN)
```

Supplier-specific identifiers such as:

* LCSC number
* JLCPCB part number
* DigiKey number
* Mouser number
* Farnell number

are secondary sourcing identifiers.

A supplier part number shall not replace the manufacturer MPN as the engineering component identity.

---

# 7. JLCPCB / LCSC Components

Rev1.5.1 uses several components selected from the JLCPCB/LCSC production ecosystem.

Where a JLCPCB/LCSC component is specified, the Master BOM records the corresponding supplier part number.

Examples include production-selected:

* TLC555 timer
* CD4066 CMOS switch
* MOSFETs
* NPN transistors
* ESD protection devices
* TVS protection
* PTC protection
* resistors
* capacitors
* key-backlight LEDs

The JLCPCB/LCSC part number should be treated as a **manufacturing sourcing reference**, not as the fundamental engineering identity of the component.

The manufacturer MPN remains authoritative.

---

# 8. Assembly-House Substitutions

An assembly house may propose an alternate component because of:

* stock shortage
* extended lead time
* minimum order quantity
* lifecycle change
* temporary unavailability
* supplier consolidation

Such a substitution is **not automatically approved**.

Before accepting an assembly-house substitute, verify the proposed MPN against:

`ALTERNATE_PARTS.md`

If the proposed part is not already approved, perform the required engineering review before assembly.

Protection devices and pin-sensitive semiconductors require explicit verification.

---

# 9. Integrated Circuits

## U1 — Autofire Timer

Production component:

**Texas Instruments `TLC555CDR`**

The production timer shall use CMOS 555 technology.

Any substitute must be verified for:

* +5 V operation
* standard 555 pinout
* SOIC-8 footprint compatibility
* supply current
* timing behaviour
* output characteristics

Classic bipolar NE555-family devices shall not be substituted without explicit electrical validation.

The earlier Renesas/Intersil `ICM7555CBAZ` remains documented as a validated legacy alternative in `ALTERNATE_PARTS.md`.

---

## U2 — Bilateral CMOS Switch

Production component:

**Texas Instruments `CD4066BM96`**

Any substitution requires verification of:

* operating voltage
* package
* pinout
* ON resistance
* switching behaviour

Do not assume all 4066-family variants are identical.

---

# 10. Protection Components

Protection components require controlled sourcing.

The production design uses protection on:

* externally accessible DB9 signal lines
* +5 V supply path
* +5 V overcurrent path

Counterfeit or unverified protection devices shall not be used.

---

## D4 / D5 — DB9 ESD Protection

Production component:

**TECH PUBLIC `PESD5V0S4UD`**

JLCPCB/LCSC:

`C2987082`

The selected device has been validated for the Rev1.5.1 PCB topology.

When sourcing an alternate, verify:

* exact package
* working voltage
* ESD rating
* internal topology
* common-anode arrangement
* exact pin mapping

A visually identical six-pin ESD array shall not automatically be considered compatible.

---

## D6 — +5 V ESD / TVS Protection

Production component:

**TECH PUBLIC `TPE0562BC3`**

JLCPCB/LCSC:

`C2841389`

This component was specifically validated for the Rev1.5.1 implementation.

The internal topology differs from the earlier protection device evaluated during development.

Therefore D6 substitutions require explicit verification of:

* internal TVS topology
* bidirectional/unidirectional behaviour
* pin mapping
* working voltage
* breakdown voltage
* clamping voltage
* package

D6 shall not be substituted based solely on package and voltage rating.

---

## F2 — Resettable PTC

Production component:

**Littelfuse `1206L005/30WR`**

Any replacement shall be verified for:

* hold current
* trip current
* maximum voltage
* resistance
* trip behaviour
* 1206 footprint

The controller-port power source has limited available current, therefore significantly different PTC characteristics may affect normal controller operation.

---

# 11. MOSFETs and Transistors

## Q1–Q7

Production component:

**onsemi `2N7002LT1G`**

Any alternate shall be checked for:

* SOT-23 package
* pinout
* gate threshold
* drain-source voltage
* drain current
* ON resistance
* leakage
* package orientation

The generic `2N7002` family name alone is not sufficient for production approval.

---

## Q8 / Q9

Production component:

**onsemi `MMBT3904LT1G`**

Any replacement shall be checked for:

* SOT-23 package
* pinout
* collector current
* VCE rating
* gain
* package orientation

Different SOT-23 transistor families may use different pin assignments.

---

# 12. Resistors

Rev1.5.1 primarily standardizes SMD resistors on the:

**YAGEO `RC1206FR-07` family**

Typical production characteristics:

* 1206
* thick film
* ±1 %
* 0.25 W

This standardization simplifies:

* procurement
* assembly
* stock management
* replacement
* traceability

Equivalent resistors from recognized manufacturers may be considered according to `ALTERNATE_PARTS.md`.

---

## Timing Resistors

Special control applies to:

```text
R13 = 330 kΩ FAST
R14 = 680 kΩ SLOW
```

These values define the validated Rev1.5.1 autofire timing behaviour.

They shall not be changed because of stock availability without engineering approval.

A different manufacturer may be considered if the electrical specification remains equivalent.

---

# 13. Capacitors

## C1 — Timing Capacitor

Production component:

**Walsin `1206B224K500NT`**

Nominal specification:

* 220 nF
* 50 V
* X7R
* 1206

C1 is timing-sensitive.

Substitution shall preserve nominal capacitance, dielectric behaviour and appropriate tolerance.

---

## C2 / C3

Production component:

**Samsung Electro-Mechanics `CL31B104KBCNNNC`**

Nominal specification:

* 100 nF
* 50 V
* X7R
* 1206

Equivalent quality MLCCs may be considered after specification verification.

---

## VCC-GND Decoupling

Production component:

**YAGEO `CC1206KRX7R8BB104`**

Nominal specification:

* 100 nF
* X7R
* 1206

The replacement shall remain suitable for local high-frequency supply decoupling.

---

# 14. LEDs

LED procurement shall consider more than nominal colour.

Verify:

* package
* polarity
* forward voltage
* brightness
* viewing angle
* colour
* colour temperature where applicable
* lead/pad orientation

---

## D1 — Power LED

Production component:

**Bivar `3RD-F`**

D1 is a 3 mm red THT LED.

Alternative colours should be treated as intentional product variants rather than uncontrolled procurement substitutions.

---

## D7 — Autofire Status LED

Production component:

**Bivar `3BC-3-F`**

Required configuration:

**Red/green, common cathode**

Required pinout:

```text
Pin 1 = Red anode
Pin 2 = Common cathode
Pin 3 = Green anode
```

A common-anode device shall not be substituted.

Exact pinout must be verified before procurement of an alternate MPN.

---

## D8–D15 — Key Backlight

Production component:

**XINGLIGHT `XL-2012WWC`**

JLCPCB/LCSC:

`C965820`

Characteristics include:

* 0805 package
* warm-white output
* approximately 2500–3100 K colour temperature

The backlight circuit intentionally operates at relatively low LED current.

A substitute should therefore be evaluated for brightness **at the actual Rev1.5.1 operating current**, not only at the manufacturer's nominal test current.

A very high-efficiency alternate may noticeably change the intended appearance.

---

# 15. Autofire Toggle Switches

Two different E-Switch MPNs are used.

They shall not be combined into one generic procurement line.

---

## SW_AUTO1

Production component:

**E-Switch `100SP1T1B4M2QE`**

Function:

**Autofire ON/OFF**

---

## SW_SPEED1

Production component:

**E-Switch `100SP3T1B1M2QEH`**

Function:

**Autofire SLOW/FAST selection**

The switch topology and mechanical dimensions must be maintained when sourcing alternatives.

---

# 16. Backlight Control Switch

## U3

Production component:

**C&K `PCM12SMTR`**

PCB side:

**Bottom**

U3 is mechanically significant because its actuator must remain accessible in the assembled controller.

A substitute must therefore be verified for:

* PCB footprint
* pad geometry
* switch function
* actuator position
* actuator height
* body dimensions
* enclosure clearance

Electrical compatibility alone is insufficient.

Depending on the manufacturing process, U3 may be manually installed rather than included in automated PCB assembly.

---

# 17. Kailh Hot-Swap Sockets

## SW1–SW8

Production component:

**Kailh / Kaihua `CPG151101S11`**

Quantity:

**8 per controller**

PCB side:

**Bottom**

The socket is mechanically critical.

Any alternate requires verification of:

* PCB pad geometry
* switch-pin contact location
* body dimensions
* PCB thickness compatibility
* retention
* MX-switch compatibility
* enclosure clearance

Hot-swap sockets from different manufacturers shall not automatically be considered footprint-compatible.

---

# 18. Mechanical Key Switches

Production fitted switch:

**Gateron KS-8 Yellow**

Quantity:

**8 per controller**

The mechanical switches are replaceable and are not permanently soldered to the PCB.

The Kailh hot-swap architecture permits compatible MX-style switches to be installed by the user.

Alternative switches may affect:

* actuation force
* travel
* sound
* tactile feel
* gameplay feel

These are normally user-experience differences rather than electrical differences.

However, physical compatibility with the Kailh socket and enclosure must still be verified.

---

# 19. THT Small-Signal Diode

## D2

Production component:

**1N4148**

Package:

**DO-35 THT**

The exact semiconductor manufacturer may vary if a generic 1N4148 is procured.

For controlled production, the supplier/manufacturer should be recorded per production lot where practical.

SMD variants such as 1N4148W are not mechanically interchangeable with the existing PCB footprint.

---

# 20. DB9 Controller Cable

The Master BOM currently specifies:

**DB9F molded 9-wire cable**

with flying leads.

The exact cable manufacturer/MPN is not yet frozen.

The cable is therefore a **supplier-controlled production item**.

Required characteristics include:

* female DB9 connector
* nine conductors
* suitable conductor gauge
* flexible cable construction
* adequate insulation
* molded strain relief
* mechanically reliable connector
* suitable cable length
* reliable solderability of flying leads

The unused controller pin does not remove the requirement for the specified physical cable construction.

---

# 21. Cable Batch Verification

Cable conductor colours shall **never** be treated as an authoritative pin-numbering system.

When:

* changing supplier
* changing cable MPN
* receiving a new production batch where construction may have changed

the first sample should be continuity-tested.

Verify each relevant DB9 pin against the corresponding flying lead before production assembly.

A simple documented cable test fixture is recommended for larger production runs.

---

# 22. J1 PCB Interface

J1 is a PCB feature rather than a procured connector.

Classification:

**PCB Feature / DNP**

The DB9 cable flying leads are soldered directly to the J1 PCB pads.

No component procurement is required for J1 itself.

---

# 23. Manual vs Automated Assembly

The Master BOM identifies the intended assembly class.

Components may be classified as:

* Top SMD
* Bottom SMD
* THT
* Mechanical / Manual
* Cable / Manual
* PCB Feature / DNP

The manufacturing process does not have to populate all components automatically.

For example, a production run may use automated assembly for top-side SMD components while manually installing:

* bottom-side hot-swap sockets
* U3
* THT LEDs
* THT diode
* toggle switches
* mechanical key switches
* DB9 cable

The **Master BOM shall still contain all components**, regardless of the assembly method.

---

# 24. Production Lot Traceability

For production batches, the following should be retained where practical:

* PCB revision
* BOM revision
* Master BOM file
* Master CPL file
* PCB manufacturer
* assembly manufacturer
* assembly order number
* assembly date
* production quantity
* component substitutions
* approved substitution records
* cable supplier
* cable batch
* manually sourced critical-component supplier
* manufacturing issues or deviations

For small production runs, this information may be stored in a simple release or production record.

---

# 25. Compliance Documentation

Where available, retain manufacturer or supplier documentation for:

* RoHS
* REACH
* material compliance
* manufacturer declarations
* component safety information where relevant

Component-level compliance documents support product traceability but **do not by themselves establish compliance of the complete WASDPad+ product**.

Product-level regulatory requirements shall be evaluated separately where applicable.

---

# 26. Datasheet Control

Datasheet references are maintained in:

`DATASHEET_INDEX.md`

For critical components, the preferred documentation source is:

1. component manufacturer
2. authorized distributor
3. assembly-house component database where the exact production component is supplied through that system

Datasheets from unidentified third-party mirrors should be avoided where an authoritative source exists.

The exact MPN in the Master BOM shall be used when selecting the applicable datasheet.

---

# 27. Lifecycle Management

The production component set should periodically be reviewed for:

* Active
* NRND / Not Recommended for New Designs
* EOL / End of Life
* Obsolete
* extended lead time
* chronic stock shortage
* manufacturer acquisition or product migration

A component should not automatically be replaced simply because a cheaper or more readily available part exists.

Where replacement becomes necessary:

1. identify the exact proposed MPN
2. obtain its datasheet
3. evaluate it according to `ALTERNATE_PARTS.md`
4. perform functional validation where required
5. update the Master BOM if selected for production
6. update `DATASHEET_INDEX.md`
7. update `ALTERNATE_PARTS.md`
8. record the change in the hardware revision/release documentation

---

# 28. High-Risk Procurement Changes

The following changes require explicit engineering approval:

* U1 timer family change
* U2 analog-switch family change
* D4/D5 protection-device change
* D6 protection-device change
* F2 PTC characteristic change
* MOSFET family or pinout change
* Q8/Q9 transistor pinout change
* D7 common-cathode architecture change
* R13 or R14 value change
* C1 value or dielectric change
* hot-swap socket manufacturer/type change
* toggle-switch topology change
* cable pin mapping change

These components directly influence functionality, protection, timing or mechanical compatibility.

---

# 29. Incoming Component Verification

For manually procured production components, incoming inspection should include as appropriate:

* manufacturer marking
* MPN / package label
* quantity
* visible package damage
* pin/lead damage
* moisture-sensitive packaging where relevant
* correct component value
* polarity
* mechanical dimensions
* supplier identity

For critical components, the received part should be compared against the applicable datasheet before first production use.

---

# 30. Procurement Change Control

A sourcing change does **not** necessarily require a hardware revision if:

* the MPN remains unchanged, or
* the replacement is already documented as an Approved Alternate and does not change product behaviour

A hardware/documentation review is required when a replacement changes:

* electrical behaviour
* timing
* protection topology
* PCB footprint
* pinout
* mechanical fit
* user-visible behaviour
* assembly process in a material way

Any production-primary MPN change shall be reflected in the Master BOM.

---

# 31. Documentation Authority

Procurement decisions shall follow this hierarchy:

```text
Production Component Identity
        ↓
WASDPad_Rev1.5.1_FULL_MASTER_BOM.csv

Technical Specification
        ↓
DATASHEET_INDEX.md
        ↓
Manufacturer Datasheet

Substitution Approval
        ↓
ALTERNATE_PARTS.md

Supplier and Lifecycle Policy
        ↓
PROCUREMENT_NOTES.md
```

Supplier availability shall never override a technical incompatibility.

---

# 32. Procurement Release Checklist

Before ordering components for a production batch:

* [ ] Confirm PCB revision is Rev1.5.1
* [ ] Use the current Master BOM
* [ ] Confirm production quantity
* [ ] Check availability of critical MPNs
* [ ] Check lifecycle status where practical
* [ ] Confirm assembly-house part mappings
* [ ] Review any proposed substitutions
* [ ] Verify D4/D5 exact MPN
* [ ] Verify D6 exact MPN
* [ ] Verify U1 exact MPN
* [ ] Verify U2 exact MPN
* [ ] Verify F2 exact MPN
* [ ] Verify D7 common-cathode configuration
* [ ] Verify Kailh socket MPN
* [ ] Verify SW_AUTO1 and SW_SPEED1 separately
* [ ] Verify cable source and pin mapping
* [ ] Record approved deviations
* [ ] Retain production order records

---

# 33. Version History

| Version | Date           | Status                           | Changes                                                                                                                                                                                                                                                                              |
| ------- | -------------- | -------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 0.1     | Not recorded   | Draft                            | Initial sourcing and procurement guidelines                                                                                                                                                                                                                                          |
| **1.0** | **2026-08-29** | **Production Release Candidate** | Rebuilt against Rev1.5.1 Master BOM; added production MPN sourcing rules, protection-component controls, JLCPCB/LCSC sourcing policy, assembly-house substitution control, cable batch verification, lifecycle management, production traceability and procurement release checklist |
