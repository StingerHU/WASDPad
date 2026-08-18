# WASDPad Hardware

## Revision 1.5

**Document Version:** 0.9
**Hardware Revision:** 1.5
**Status:** Engineering Validation / Pre-Prototype
**Last Updated:** 2026-08-18

---

# 1. Overview

WASDPad Revision 1.5 is the current hardware development revision of the WASDPad controller.

It builds on the validated Revision 1.2 architecture while adding improvements in:

* electrical protection
* switch serviceability
* component standardization
* manufacturing repeatability
* status indication
* production documentation

Revision 1.5 remains a fully hardware-based controller.

No microcontroller or firmware is required for normal operation.

The fundamental joystick signal path remains based on direct digital control compatible with classic Atari-style DE-9 / DB9 joystick interfaces.

---

# 2. Development Goals

Revision 1.5 is intended to refine the existing production-capable hardware rather than replace its basic operating principle.

Primary development goals include:

* retain the proven hardware-only control architecture
* improve electrical protection
* add resettable overcurrent protection
* add ESD protection
* introduce MX hot-swap sockets
* standardize gameplay switches
* improve autofire speed differentiation
* add dual-colour autofire indication
* standardize passive components
* document cable assembly and production verification
* improve manufacturing and test procedures
* prepare the platform for a later Rev 2.0 redesign

---

# 3. Hardware Architecture

Revision 1.5 is divided into the following functional blocks:

```text
                    DB9 Connector
                         |
                    +5V / GND
                         |
                  Power Protection
                         |
                  Power Distribution
                         |
        +----------------+----------------+
        |                |                |
        v                v                v
  Input Switches   Autofire Logic    Status LEDs
        |                |                |
        +-----------+----+----------------+
                    |
              Output Drivers
                    |
              DB9 Signal Lines
```

The controller remains entirely hardware controlled.

---

# 4. Directional Controls

The controller provides four independent digital direction controls:

* UP
* DOWN
* LEFT
* RIGHT

Each direction uses an MX-compatible mechanical switch installed in a hot-swap socket.

The signal behaviour follows the active-low logic expected by classic joystick interfaces.

---

# 5. FIRE Controls

Revision 1.5 provides:

* FIRE1
* FIRE2

FIRE1 supports both:

* normal manual operation
* hardware autofire

FIRE2 remains a direct manual input.

The FIRE logic uses discrete MOSFET switching stages to reproduce the electrical behaviour expected by the target systems.

---

# 6. Autofire System

The autofire generator uses:

**Renesas ICM7555CBAZ**

This is a low-power CMOS implementation of the classic 555 timer architecture.

The oscillator is fully hardware based and requires no firmware.

Two firing speeds are supported.

| Mode | Timing Resistance |
| ---- | ----------------: |
| FAST |            330 kΩ |
| SLOW |            680 kΩ |

The corresponding resistors are:

```text
R13 = 330 kΩ -> FAST
R14 = 680 kΩ -> SLOW
```

The final values were selected through physical gameplay testing.

The SLOW setting provides a clearly distinguishable lower firing rate compared with FAST.

Physical speed-selector behaviour:

```text
LEFT  -> SLOW
RIGHT -> FAST
```

---

# 7. Autofire Enable Control

Autofire can be enabled or disabled using a dedicated toggle switch.

The physical switch used is:

**E-Switch 100SP1T1B4M2QE**

The same physical switch type is also used for the SLOW / FAST selector.

The two controls intentionally use different KiCad symbol / footprint mappings because the schematic and PCB were adapted to the validated physical switch orientation.

These mappings shall not be changed solely to make their KiCad names identical.

---

# 8. Hot-Swap Switch Architecture

Revision 1.5 introduces hot-swappable gameplay switches.

The PCB uses:

**Kailh / Kaihua CPG151101S11**

MX hot-swap sockets.

Quantity:

```text
8 per controller
```

KiCad footprint:

```text
PCM_Switch_Keyboard_Hotswap_Kailh:SW_Hotswap_Kailh_MX
```

The sockets allow compatible MX-style mechanical switches to be replaced without soldering.

---

# 9. Default Mechanical Switch

The default Rev 1.5 switch is:

**Gateron KS-8 Yellow**

Quantity:

```text
8 per controller
```

The Gateron KS-8 Yellow is used as the baseline production switch configuration.

Other MX-compatible switches may be supported where:

* contact geometry is compatible
* mechanical pin spacing is compatible
* the switch fits the Kailh socket
* enclosure clearance is sufficient

---

# 10. Power Protection

Revision 1.5 introduces resettable overcurrent protection on the +5 V supply.

Primary component:

**Littelfuse 1206L005/30WR**

Nominal characteristics:

* 50 mA hold current
* 150 mA trip current
* 30 V maximum voltage
* 1206 package

The selected current rating reflects the limited +5 V current capability of classic joystick ports, including the Commodore 64 control port.

---

# 11. Signal ESD Protection

Externally accessible joystick signal lines are protected using:

**Nexperia PESD5V0S4UD**

Package:

```text
SOT457 / SC-74
```

KiCad footprint:

```text
Package_TO_SOT_SMD:SC-74-6_1.55x2.9mm_P0.95mm
```

The original generic SOT-23-6 footprint was replaced with the more appropriate SC-74 footprint during Rev 1.5 component validation.

---

# 12. +5 V ESD Protection

The +5 V rail is protected using:

**Nexperia PESD6V0L2UU**

Package:

```text
SOT-323 / SC-70
```

KiCad footprint:

```text
Package_TO_SOT_SMD:SOT-323_SC-70
```

The final validated schematic connection is:

```text
Pin 1 -> protected +5 V rail
Pin 2 -> NC
Pin 3 -> GND
```

The component topology and pin mapping have been checked against the Nexperia datasheet.

**Validation Status: PASS**

---

# 13. Power Decoupling

The controller includes dedicated supply decoupling.

Primary decoupling component:

**KEMET C1206C104J3RACAUTO**

Specification:

* 100 nF
* 25 VDC
* X7R
* ±5 %
* 1206

The dedicated VCC-GND decoupling capacitor should be placed physically close to the ICM7555 supply pins.

---

# 14. Timing and Filter Capacitors

## C1

Primary part:

**KEMET C1206S224J3RACAUTO**

Specification:

* 220 nF
* 25 VDC
* X7R
* ±5 %
* 1206

C1 forms part of the FIRE1 timing / shot-gate network.

---

## C2 and C3

Primary part:

**KEMET C1206C104J3RACAUTO**

Specification:

* 100 nF
* 25 VDC
* X7R
* ±5 %
* 1206

C2 is associated with the ICM7555 control network.

C3 is part of the autofire timing network.

---

# 15. Standardized Resistors

Revision 1.5 standardizes most resistors on:

**YAGEO RC1206FR-07**

General specification:

* 1206
* thick film
* ±1 %
* 0.25 W
* SMT

Used values include:

* 270 Ω
* 330 Ω
* 4.7 kΩ
* 10 kΩ
* 100 kΩ
* 330 kΩ
* 680 kΩ

Standardization reduces sourcing complexity and improves production consistency.

---

# 16. Dual-Colour Autofire Indicator

Revision 1.5 uses a dedicated 3 mm dual-colour autofire status LED.

Primary component:

**Bivar 3BC-3-F**

Configuration:

**Common Cathode**

KiCad footprint:

```text
LED_THT:LED_D3.0mm-3
```

Validated pin assignment:

```text
Pin 1 -> RED anode -> R22
Pin 2 -> Common cathode -> GND
Pin 3 -> GREEN anode -> R23
```

Associated resistors:

```text
R22 = 270 Ω
R23 = 330 Ω
```

The common-cathode version is required by the current Rev 1.5 driver topology.

**Validation Status: PASS**

---

# 17. Dual-Colour LED Drivers

The autofire LED channels are driven using MMBT3904 NPN transistors.

Verified pin assignment:

```text
Pin 1 = Base
Pin 2 = Emitter
Pin 3 = Collector
```

The following have been checked for consistency:

* manufacturer datasheet
* KiCad symbol
* KiCad footprint

The Q1/Q2 collector connections are tied to +5 V in the current design.

The emitter outputs drive the LED channels through R22 and R23.

**Validation Status: PASS**

---

# 18. Power LED

Revision 1.5 contains a separate 3 mm THT power indicator.

KiCad footprint:

```text
LED_THT:LED_D3.0mm
```

The power LED colour may be selected according to the requested controller configuration.

Supported variants include:

* Red
* Blue
* White

The series resistor is:

```text
R_LED1 = 4.7 kΩ
```

Approved exact LED variants are maintained separately in the alternate-parts documentation.

---

# 19. Controller Cable

Revision 1.5 currently uses a generic molded DB9 female controller cable with flying leads.

The validated cable is sold as a Sega Mega Drive / Genesis 2 style replacement controller cable.

Current supplier reference:

```text
AliExpress Item ID: 1005009578092300
```

The cable is soldered directly to PCB pads.

Detailed assembly and verification information is maintained in:

```text
docs/assembly/CABLE_ASSEMBLY.md
```

The first cable from every new supplier batch must undergo a complete DB9 pin-to-wire continuity test.

Wire colours must not be assumed to remain identical between production batches.

---

# 20. J1 Cable Interface

J1 is implemented as PCB solder pads rather than a separately procured connector.

KiCad footprint:

```text
Connector_Wire:SolderWirePad_1x01_SMD_1.5x3mm
```

J1 is therefore treated as:

```text
DNP / no procurement item
```

The DB9 numbering is intentionally kept aligned with J1 pad numbering wherever possible.

---

# 21. CMOS Switching Logic

Revision 1.5 uses:

**Texas Instruments CD4066BM96**

Function:

Quad bilateral CMOS switch

Package:

SOIC-14

KiCad footprint:

```text
Package_SO:SO-14_3.9x8.65mm_P1.27mm
```

The active `CD4066BM96` ordering code is preferred for new procurement.

---

# 22. MOSFET Logic

The FIRE and autofire logic uses 2N7002 N-channel MOSFETs.

Primary device family:

```text
2N7002
```

Preferred manufacturer:

```text
onsemi
```

Package:

```text
SOT-23
```

The symbol / footprint mapping follows:

```text
Pin 1 = Gate
Pin 2 = Source
Pin 3 = Drain
```

This pin mapping shall be rechecked during final production validation if the manufacturer is changed.

---

# 23. Assembly Considerations

## ICM7555 Soldering

Special attention must be paid to U1 during assembly.

During prototype construction, incompletely reflowed solder paste beneath the SOIC package caused unintended low-resistance paths between +5 V and GND.

Observed symptoms included:

* collapsed supply voltage
* non-operational LEDs
* controller completely unresponsive
* incorrect or missing autofire operation

After U1 soldering:

1. visually inspect the package
2. clean excess solder paste and flux
3. verify all pins
4. measure +5 V-to-GND resistance before applying power
5. do not connect the controller to a host computer while a low-resistance supply short exists

This procedure shall become part of the Rev 1.5 production test process.

---

# 24. Engineering Validation Completed

The following Rev 1.5 component checks have been completed:

| Check                                   | Status     |
| --------------------------------------- | ---------- |
| Final autofire timing values            | PASS       |
| D4/D5 component and footprint selection | PASS       |
| D6 component pinout / topology          | PASS       |
| D7 common-cathode LED pinout            | PASS       |
| Q1/Q2 MMBT3904 pinout                   | PASS       |
| ICM7555 package selection               | PASS       |
| CD4066 package selection                | PASS       |
| Hot-swap socket selection               | PASS       |
| Default MX switch selection             | PASS       |
| PTC selection                           | PASS       |
| Cable pin mapping                       | PASS       |
| Cable batch validation procedure        | Documented |

---

# 25. Development Status

| Area                        | Status                         |
| --------------------------- | ------------------------------ |
| Hardware architecture       | ✅ Defined                      |
| Feature specification       | ✅ Defined                      |
| Primary component selection | ✅ Complete                     |
| BOM                         | ✅ Pre-Release Validated        |
| Protection components       | ✅ Selected                     |
| Autofire timing             | ✅ Physically Validated         |
| Hot-swap system             | ✅ Defined                      |
| LED system                  | ✅ Defined and Pinout Validated |
| Controller cable            | ✅ Defined and Documented       |
| Schematic                   | 🚧 Engineering Review          |
| PCB layout                  | 🚧 Engineering Review          |
| ERC                         | ⏳ Final Run Pending            |
| DRC                         | ⏳ Final Run Pending            |
| Rev 1.5 prototype           | ⏳ Pending                      |
| Electrical validation       | ⏳ Pending                      |
| Mechanical validation       | ⏳ Pending                      |
| Production release          | ⏳ Pending                      |

---

# 26. Current Development Phase

The primary component-selection phase for Revision 1.5 is complete.

Current work is focused on:

1. final schematic review
2. final symbol / footprint verification
3. PCB layout review
4. ERC validation
5. DRC validation
6. prototype manufacturing
7. electrical validation
8. gameplay testing
9. manufacturing documentation
10. production-release preparation

---

# 27. Production Release Criteria

Revision 1.5 may be considered production-ready only after all of the following have been completed:

* final schematic review
* final PCB review
* clean ERC
* clean DRC
* first Rev 1.5 PCB manufactured
* full controller assembled
* all directional inputs validated
* FIRE1 validated
* FIRE2 validated
* autofire OFF validated
* autofire SLOW validated
* autofire FAST validated
* power LED validated
* dual-colour LED validated
* ESD protection layout verified
* PTC operation verified
* cable assembly verified
* enclosure clearance verified
* hot-swap operation verified
* no excessive supply current
* no +5 V-to-GND short circuit

---

# 28. Relationship to Revision 1.2

Revision 1.5 is an evolutionary development of the validated Revision 1.2 platform.

Revision 1.2 established the fully functional hardware architecture.

Revision 1.5 retains the basic control concept while improving:

* serviceability
* electrical protection
* autofire usability
* manufacturing documentation
* switch replacement
* LED indication
* sourcing consistency
* production validation

---

# 29. Future Revision 2.0

Revision 2.0 is planned as a substantially different platform.

Possible Rev 2.0 features include:

* RP2040-based control
* firmware-controlled autofire
* adjustable autofire timing
* burst mode
* game-specific profiles
* configurable debounce
* persistent configuration
* USB firmware update capability
* optional USB HID support
* programmable LED indication

Rev 2.0 development shall remain separate from the final validation of Rev 1.5.

---

# 30. Documentation

Related documentation includes:

```text
docs/architecture/System_architecture.md
docs/specification/PROJECT_SPECIFICATION.md
docs/specification/FEATURE_SPECIFICATION.md
docs/assembly/CABLE_ASSEMBLY.md
hardware/rev1.5/bom/README.md
hardware/rev1.5/bom/BOM.csv
hardware/rev1.5/bom/ALTERNATE_PARTS.md
hardware/rev1.5/bom/PROCUREMENT_NOTES.md
```

---

# 31. Document Versioning

The hardware revision and documentation revision are independent.

Current state:

```text
Hardware Revision: 1.5
Hardware README:   0.9
BOM README:        0.9
```

Documentation-only corrections do not require a PCB revision increment.

---

# 32. Version History

| Document Version | Date           | Status                     | Changes                                                                                                                                                                                             |
| ---------------- | -------------- | -------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 0.1              | Not recorded   | Initial Draft              | Initial Rev 1.5 hardware overview                                                                                                                                                                   |
| 0.4              | Not recorded   | Planning                   | Rev 1.5 feature and protection planning                                                                                                                                                             |
| 0.6              | Not recorded   | Component Selection        | Hot-swap, PTC and ESD architecture added                                                                                                                                                            |
| 0.8              | Not recorded   | Engineering                | Initial BOM and autofire refinements documented                                                                                                                                                     |
| **0.9**          | **2026-08-18** | **Engineering Validation** | Primary component selection completed; final FAST/SLOW values documented; D6 and D7 pinouts validated; MMBT3904 mapping validated; hot-swap, switches, cable assembly and production checks updated |

---

# 33. Next Documentation Version

The next planned hardware README release is:

**Version 1.0**

Target milestone:

**First complete Rev 1.5 prototype successfully manufactured and fully validated.**

Until that milestone is reached, Revision 1.5 remains:

**Engineering Validation / Pre-Prototype**
