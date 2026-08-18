# WASDPad Revision 1.5

## Approved Alternate Parts

**Document Version:** 0.9
**Hardware Revision:** 1.5
**Status:** Engineering Validation
**Last Updated:** 2026-08-18

---

# 1. Purpose

This document defines the alternate-component strategy for **WASDPad Hardware Revision 1.5**.

The primary BOM remains the authoritative source for production components.

Alternate components listed here may be used only when they meet the electrical, mechanical and manufacturing requirements of the primary component.

An alternate part is not considered approved solely because it has:

* the same generic component name
* the same package name
* similar electrical ratings
* the same nominal value

Pinout, footprint, polarity, mechanical dimensions, lifecycle status and system behaviour must also be verified.

---

# 2. Alternate-Part Status Definitions

| Status           | Meaning                                                          |
| ---------------- | ---------------------------------------------------------------- |
| Approved         | Fully compatible for the defined use case                        |
| Approved Variant | Approved configuration option rather than a technical substitute |
| Candidate        | Likely compatible but requires validation                        |
| Conditional      | May be used only if specified requirements are met               |
| Not Approved     | Shall not be used without redesign or engineering review         |

---

# 3. General Approval Requirements

Before an alternate component is used in production, verify:

* electrical function
* nominal value
* voltage and current rating
* tolerance
* package
* footprint
* pin numbering
* polarity
* operating temperature range
* lifecycle status
* availability
* mechanical clearance
* interaction with surrounding components

For semiconductors and protection devices, the manufacturer datasheet must be checked directly.

---

# 4. Autofire Timer

## Primary Component

**Renesas ICM7555CBAZ**

Function:

* CMOS 555 timer
* SOIC-8
* low supply current
* hardware autofire oscillator

## Alternate Strategy

Other CMOS 7555-compatible timers may be considered only if they are electrically and pin compatible.

Potential families include:

* TLC555 CMOS variants
* LMC555 CMOS variants
* other ICM7555-compatible devices

### Requirements

An alternate timer must provide:

* standard 555 pinout
* operation at approximately 5 V
* CMOS implementation
* low supply current
* compatible trigger and threshold levels
* compatible output behaviour
* compatible reset input
* compatible SOIC-8 footprint

### Restriction

Classic bipolar **NE555** devices are **not approved as drop-in production replacements** without electrical validation.

Their significantly higher supply current and different switching behaviour may affect:

* joystick-port current consumption
* timing behaviour
* supply noise
* PTC selection

**Status:** Conditional

---

# 5. CMOS Bilateral Switch

## Primary Component

**Texas Instruments CD4066BM96**

## Alternate Strategy

A compatible CD4066B-family quad bilateral CMOS switch may be used if:

* VDD range includes 5 V
* pinout matches the current schematic
* SOIC-14 mechanical footprint is compatible
* control-input thresholds are compatible
* ON resistance is acceptable for the signal path

Possible manufacturers may include:

* Texas Instruments
* onsemi
* Nexperia
* STMicroelectronics
* other established logic manufacturers

Exact manufacturer part numbers shall be validated before production substitution.

**Status:** Conditional

---

# 6. 2N7002 MOSFETs

## Primary Component

**onsemi 2N7002**

Used throughout the FIRE and autofire logic.

## Alternate Strategy

2N7002 devices from established manufacturers are generally acceptable if the following are verified:

```text
Pin 1 = Gate
Pin 2 = Source
Pin 3 = Drain
```

Additional requirements:

* N-channel MOSFET
* SOT-23
* suitable operation with approximately 5 V gate drive
* low leakage
* adequate drain-current capability
* adequate VDS rating

Potential manufacturers include:

* onsemi
* Nexperia
* Diodes Incorporated
* Vishay
* Infineon
* ROHM

### Critical Requirement

Do not approve an alternate solely from the `2N7002` generic name.

The manufacturer datasheet pinout must be checked against the KiCad symbol and footprint.

**Status:** Conditional / manufacturer-specific validation required

---

# 7. MMBT3904 NPN Transistors

## Primary Component

**MMBT3904 family, SOT-23**

Used for the dual-colour autofire LED driver stages.

Validated mapping:

```text
Pin 1 = Base
Pin 2 = Emitter
Pin 3 = Collector
```

## Alternate Strategy

MMBT3904 devices from established manufacturers may be used if the pinout is identical.

Potential manufacturers include:

* onsemi
* Nexperia
* Diodes Incorporated
* Central Semiconductor
* ROHM

Electrical requirements:

* NPN transistor
* SOT-23
* sufficient gain at the LED operating current
* suitable VCE rating
* compatible pinout

**Status:** Conditional / pinout verification required

---

# 8. General Resistors

## Primary Series

**YAGEO RC1206FR-07**

Specification:

* 1206
* thick film
* ±1 %
* 0.25 W

## Alternate Strategy

Equivalent resistors from reputable manufacturers may be substituted freely if all of the following match or exceed the primary specification:

* correct resistance
* 1206 package
* ±1 % tolerance or better
* ≥0.25 W rating

Potential manufacturers:

* Vishay
* Panasonic
* KOA Speer
* Bourns
* Stackpole
* TE Connectivity

### Critical Timing Values

Extra care shall be taken with:

* R13 = 330 kΩ FAST
* R14 = 680 kΩ SLOW

The resistance value shall not be changed as a procurement substitute.

**Status:** Approved by specification

---

# 9. Capacitors

## 9.1 100 nF Parts

Primary:

**KEMET C1206C104J3RACAUTO**

Used for:

* C2
* C3
* VCC-GND decoupling

Minimum alternate specification:

* 100 nF
* 1206
* X7R
* ≥16 VDC
* ±10 % or better

For C3, tighter tolerance is preferred because it affects autofire timing.

Preferred tolerance:

**±5 %**

Potential manufacturers:

* KEMET
* Murata
* TDK
* Samsung Electro-Mechanics
* Yageo
* Vishay

**Status:** Approved by specification

---

## 9.2 C1 — 220 nF

Primary:

**KEMET C1206S224J3RACAUTO**

Minimum alternate specification:

* 220 nF
* 1206
* X7R
* ≥16 VDC
* ±10 % or better

Preferred:

* 25 V
* ±5 %

**Status:** Approved by specification

---

# 10. PTC Overcurrent Protection

## Primary Component

**Littelfuse 1206L005/30WR**

Specification:

* 50 mA hold current
* 150 mA trip current
* 30 V maximum voltage
* 1206

## Alternate Strategy

An alternate PPTC may be considered if it provides:

* approximately 50 mA hold current
* trip current appropriate for joystick-port protection
* 1206 footprint compatibility
* low enough cold resistance to avoid excessive voltage drop
* voltage rating comfortably above 5 V

Potential manufacturers:

* Littelfuse
* Bourns
* Bel Fuse
* Eaton

### Restriction

A significantly higher hold-current device shall not be substituted automatically.

The 50 mA selection is intentionally related to the limited current capability of classic joystick ports.

**Status:** Conditional

---

# 11. D4 / D5 Signal ESD Arrays

## Primary Component

**Nexperia PESD5V0S4UD**

Package:

**SOT457 / SC-74**

KiCad footprint:

```text
Package_TO_SOT_SMD:SC-74-6_1.55x2.9mm_P0.95mm
```

## Alternate Strategy

An alternate device must provide:

* at least four protected lines
* compatibility with 5 V digital signals
* suitable IEC 61000-4-2 protection
* low leakage
* suitable capacitance
* compatible six-pin package and pad geometry
* matching internal topology or a corresponding schematic redesign

### Candidate Families

Possible alternatives may exist from:

* STMicroelectronics
* onsemi
* Littelfuse
* Semtech

### Important Restriction

Bidirectional and unidirectional protection arrays are not automatically interchangeable.

Pinout and internal topology must be verified.

**Status:** Conditional

---

# 12. D6 +5 V ESD Protection

## Primary Component

**Nexperia PESD6V0L2UU**

Package:

**SOT-323 / SC-70**

Validated implementation:

```text
Pin 1 -> protected +5 V rail
Pin 2 -> NC
Pin 3 -> GND
```

## Alternate Strategy

An alternate device must be suitable for protecting an approximately 5 V supply and provide:

* compatible standoff voltage
* compatible clamping behaviour
* SOT-323 / SC-70 or PCB-compatible package
* correct diode orientation

The current schematic intentionally uses only one of the two internal protection channels.

### Critical Requirement

Any replacement must be checked against the actual schematic connection.

**Status:** Conditional

---

# 13. Dual-Colour Autofire LED

## Primary Component

**Bivar 3BC-3-F**

Specification:

* 3 mm THT
* Red / Green
* common cathode
* three pins

Validated pinout:

```text
Pin 1 -> RED anode
Pin 2 -> Common cathode
Pin 3 -> GREEN anode
```

## Alternate Strategy

A replacement may be used only if it is:

* 3 mm THT
* three-pin
* common cathode
* mechanically compatible with `LED_THT:LED_D3.0mm-3`
* compatible with the R22 / R23 driver network

### Critical Restriction

**Common-anode LEDs are NOT drop-in alternatives.**

For example:

```text
Bivar 3BC-3-CA-F
```

is not approved because it requires a different driver topology.

**Status:** Primary approved; alternatives require explicit pinout validation

---

# 14. Power LED D1

The power LED is intentionally configurable.

## Approved Variants

The supported customer-selectable colours are:

* Red
* Blue
* White

All variants shall use:

* 3 mm THT package
* two-pin LED
* footprint `LED_THT:LED_D3.0mm`
* R_LED1 = 4.7 kΩ

### Current Approved Example Parts

#### Red

**Bivar 3RDL-S**

#### Blue

**Bivar 3BWD-S**

#### White

**LITEON LTW-420D7**

These are treated as **Approved Variants**, not substitutes requiring a hardware revision.

Brightness may vary between colours because R_LED1 remains fixed.

**Status:** Approved Variant

---

# 15. MX Hot-Swap Sockets

## Primary Component

**Kailh / Kaihua CPG151101S11**

KiCad footprint:

```text
PCM_Switch_Keyboard_Hotswap_Kailh:SW_Hotswap_Kailh_MX
```

## Alternate Strategy

Other MX hot-swap sockets shall not be treated as drop-in replacements unless:

* PCB pad geometry matches
* switch contact geometry matches
* mechanical retention is compatible
* enclosure and switch height remain valid

A socket from another manufacturer may require a different PCB footprint.

**Status:** Primary approved; alternatives require PCB-level validation

---

# 16. Mechanical Gameplay Switches

## Primary Component

**Gateron KS-8 Yellow**

Quantity:

**8 per controller**

The switches are installed in the Kailh hot-swap sockets.

## Alternate Strategy

The controller may use other MX-compatible mechanical switches.

Potential compatible families include:

* Cherry MX
* Gateron MX
* Kailh MX
* TTC MX

Approval criteria:

* MX contact geometry
* compatible switch-pin dimensions
* compatible hot-swap socket engagement
* compatible switch height
* compatible enclosure clearance

### User Preference

Different switch feel is intentionally supported.

Linear, tactile or clicky switches may be used if mechanically compatible.

**Status:** Approved by mechanical compatibility

---

# 17. Autofire Toggle Switches

## Primary Component

**E-Switch 100SP1T1B4M2QE**

Used for:

* SW_AUTO1
* SW_SPEED1

## Alternate Strategy

These switches are mechanically integrated into the PCB and enclosure.

Any replacement must match:

* pin spacing
* mounting geometry
* actuator dimensions
* body size
* electrical function
* enclosure opening

### Important Rev 1.5 Note

The two switch positions intentionally use different KiCad footprint / symbol mappings due to the validated physical layout.

The existing mapping shall not be changed merely to standardize library names.

**Status:** Primary approved; alternates require mechanical validation

---

# 18. Controller Cable

## Primary Supplier Type

Generic Sega Mega Drive / Genesis 2 style controller cable.

Current supplier reference:

```text
AliExpress Item ID: 1005009578092300
```

Configuration:

* molded DB9 female connector
* nine internal conductors
* flying leads on PCB side

## Alternate Strategy

A different cable may be used if:

* connector is DB9 female
* mechanical fit is acceptable
* sufficient cable length is provided
* all required conductors exist
* conductor quality is acceptable

### Mandatory Requirement

Wire colour is **not** part of the electrical specification.

Every new supplier or production batch must have its DB9-pin-to-wire mapping checked using a continuity meter.

Refer to:

```text
docs/assembly/CABLE_ASSEMBLY.md
```

**Status:** Approved by batch validation

---

# 19. J1 PCB Cable Pads

J1 is not a procurement component.

It is a PCB feature implemented using:

```text
Connector_Wire:SolderWirePad_1x01_SMD_1.5x3mm
```

There is therefore no alternate purchased part.

**Status:** Not applicable

---

# 20. PCB and Footprints

Alternate components must not force an unreviewed PCB footprint change.

If an alternate requires:

* different pad dimensions
* different pin pitch
* different pin numbering
* different package geometry

the component must be treated as a design change rather than a normal BOM substitution.

Such a change requires:

1. schematic review
2. footprint review
3. PCB DRC
4. manufacturing review
5. prototype validation

---

# 21. Procurement Priority

When selecting between primary and alternate components, preference shall be given in this order:

1. Primary approved BOM component
2. Approved variant
3. Previously validated equivalent
4. Candidate from a recognized manufacturer
5. New alternate requiring engineering validation

Marketplace-only substitutes shall not be used for protection components or semiconductors unless authenticity is known.

---

# 22. No-Substitution Components

The following characteristics shall not be changed without engineering review:

* R13 = 330 kΩ FAST timing
* R14 = 680 kΩ SLOW timing
* D7 common-cathode configuration
* D6 protection polarity/topology
* PTC current class
* MX hot-swap footprint
* toggle-switch mechanical geometry

---

# 23. Version History

| Document Version | Date           | Status                     | Changes                                                                                                                                                                                                               |
| ---------------- | -------------- | -------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 0.1              | Not recorded   | Draft                      | Initial placeholder alternate-part document                                                                                                                                                                           |
| 0.3              | Not recorded   | Draft                      | Initial generic substitution guidance                                                                                                                                                                                 |
| **0.9**          | **2026-08-18** | **Engineering Validation** | Updated with actual Rev 1.5 primary components, D1 colour variants, MX-switch strategy, semiconductor replacement rules, ESD restrictions, PTC requirements, cable batch strategy and validated no-substitution rules |

---

# 24. Next Version

The next planned version is:

**1.0**

It may be released when the complete Revision 1.5 prototype has passed full electrical, functional, mechanical and manufacturing validation.
