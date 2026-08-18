# WASDPad Revision 1.5

## Bill of Materials

**Document Version:** 0.9
**Hardware Revision:** 1.5
**Status:** Pre-Release / Component Selection Complete
**Last Updated:** 2026-08-18

---

# 1. Purpose

This directory contains the Bill of Materials and component-selection documentation for **WASDPad Hardware Revision 1.5**.

Revision 1.5 is based on the validated Revision 1.2 hardware architecture and introduces improvements in:

* electrical protection
* serviceability
* switch replacement
* status indication
* component standardization
* manufacturing documentation

The fundamental operating principle remains fully hardware-based.

Revision 1.5 does not require a microcontroller or firmware.

---

# 2. BOM Files

The BOM directory contains:

```text
hardware/rev1.5/bom/
│
├── README.md
├── BOM.csv
├── ALTERNATE_PARTS.md
└── PROCUREMENT_NOTES.md
```

## `BOM.csv`

The authoritative engineering Bill of Materials.

It contains:

* reference designators
* quantities
* electrical values
* footprints
* manufacturer information
* manufacturer part numbers
* datasheet references
* component descriptions
* mechanical and assembly items

The CSV file shall be treated as the primary component database for Revision 1.5.

## `ALTERNATE_PARTS.md`

Contains approved or candidate replacement components.

An alternate component shall only be used after electrical, mechanical and pinout compatibility has been verified.

## `PROCUREMENT_NOTES.md`

Contains sourcing, lifecycle and supplier-specific information that does not belong in the schematic itself.

---

# 3. Revision 1.5 Component Selection Status

The primary component-selection phase for Revision 1.5 is substantially complete.

| Component Group            | Status                                               |
| -------------------------- | ---------------------------------------------------- |
| Autofire timer             | Approved                                             |
| CMOS switching logic       | Approved                                             |
| MOSFET logic stages        | Approved                                             |
| Autofire timing resistors  | Approved and physically tested                       |
| General resistors          | Approved                                             |
| Timing capacitors          | Approved                                             |
| Supply decoupling          | Approved                                             |
| PTC overcurrent protection | Approved                                             |
| DB9 signal ESD protection  | Approved                                             |
| +5 V ESD protection        | Approved                                             |
| MX hot-swap sockets        | Approved                                             |
| Mechanical switches        | Approved                                             |
| Dual-colour status LED     | Approved                                             |
| Power LED variants         | Approved concept / colour selectable                 |
| Toggle switches            | Approved / physically validated                      |
| Controller cable           | Approved supplier type / batch verification required |
| PCB solder pads            | PCB feature / no procurement item                    |

---

# 4. Core Active Components

## 4.1 Autofire Timer

**Reference:** U1
**Manufacturer:** Renesas Electronics
**MPN:** `ICM7555CBAZ`
**Function:** CMOS general-purpose timer
**Package:** SOIC-8
**KiCad Footprint:**

```text
Package_SO:SOIC-8_3.9x4.9mm_P1.27mm
```

The ICM7555 provides the hardware autofire oscillator.

This component has been physically validated on working WASDPad hardware.

The CMOS implementation is preferred over bipolar NE555 variants because of its substantially lower supply current.

---

## 4.2 Bilateral Switching Logic

**Reference:** U2
**Manufacturer:** Texas Instruments
**MPN:** `CD4066BM96`
**Function:** Quad bilateral CMOS switch
**Package:** SOIC-14
**KiCad Footprint:**

```text
Package_SO:SO-14_3.9x8.65mm_P1.27mm
```

The active `CD4066BM96` ordering code is preferred over obsolete or legacy `CD4066BM` sourcing.

---

## 4.3 MOSFET Logic

The FIRE and autofire logic uses **2N7002 N-channel MOSFETs**.

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

The symbol, footprint and device pinout use:

```text
Pin 1 = Gate
Pin 2 = Source
Pin 3 = Drain
```

---

## 4.4 Autofire Status Drivers

The dual-colour status LED is driven by MMBT3904 NPN transistors.

The verified pin assignment is:

```text
Pin 1 = Base
Pin 2 = Emitter
Pin 3 = Collector
```

This mapping has been checked against:

* the selected transistor datasheet
* the KiCad symbol
* the KiCad footprint

---

# 5. Autofire Timing

Revision 1.5 uses two fixed hardware autofire speeds.

The final values were selected through physical gameplay testing.

| Reference |  Value | Function | SMD Marking |
| --------- | -----: | -------- | ----------- |
| R13       | 330 kΩ | FAST     | `334`       |
| R14       | 680 kΩ | SLOW     | `684`       |

The physical toggle behaviour is:

```text
Switch LEFT  -> SLOW
Switch RIGHT -> FAST
```

The 680 kΩ SLOW value provides an approximately half-speed subjective firing rate compared with FAST and produces a clearly distinguishable operating mode during gameplay.

These values supersede all earlier experimental autofire resistor values.

---

# 6. Resistors

General resistors are standardized on the:

**YAGEO RC1206FR-07**

series wherever practical.

General specification:

* 1206 / 3216 metric
* thick film
* ±1 %
* 0.25 W
* SMT

Approved values include:

|  Value | Typical SMD Code |
| -----: | ---------------: |
|  270 Ω |            `271` |
|  330 Ω |            `331` |
| 4.7 kΩ |            `472` |
|  10 kΩ |            `103` |
| 100 kΩ |            `104` |
| 330 kΩ |            `334` |
| 680 kΩ |            `684` |

Examples of approved YAGEO part numbers include:

```text
RC1206FR-07270RL
RC1206FR-07330RL
RC1206FR-074K7L
RC1206FR-0710KL
RC1206FR-07100KL
RC1206FR-07330KL
RC1206FR-07680KL
```

---

# 7. Capacitors

## 7.1 C1 — FIRE1 Timing

**Value:** 220 nF
**Manufacturer:** KEMET
**MPN:** `C1206S224J3RACAUTO`

Specification:

* 220 nF
* 25 VDC
* X7R
* ±5 %
* 1206
* SMT

---

## 7.2 C2, C3 and Supply Decoupling

Primary component:

**Manufacturer:** KEMET
**MPN:** `C1206C104J3RACAUTO`

Specification:

* 100 nF
* 25 VDC
* X7R
* ±5 %
* 1206
* SMT

These parts are used for:

* ICM7555 control-pin filtering
* autofire timing
* VCC-GND supply decoupling

The dedicated supply-decoupling capacitor shall be placed physically close to the ICM7555 VDD and GND connections.

---

# 8. Overcurrent Protection

Revision 1.5 introduces resettable supply protection.

**Reference:** F2
**Manufacturer:** Littelfuse
**MPN:** `1206L005/30WR`

Specification:

* resettable PPTC
* 50 mA hold current
* 150 mA trip current
* 30 V maximum voltage
* 1206 package

The 50 mA hold-current selection was chosen with the Commodore 64 control-port +5 V current specification in mind.

---

# 9. ESD Protection

## 9.1 D4 and D5 — DB9 Signal Protection

**Component:** `PESD5V0S4UD`
**Manufacturer:** Nexperia
**Function:** Quadruple unidirectional ESD protection array
**Package:** SOT457 / SC-74

KiCad footprint:

```text
Package_TO_SOT_SMD:SC-74-6_1.55x2.9mm_P0.95mm
```

These devices protect externally accessible digital joystick signal lines.

---

## 9.2 D6 — +5 V Protection

**Component:** `PESD6V0L2UU`
**Manufacturer:** Nexperia
**Package:** SOT-323 / SC-70

KiCad footprint:

```text
Package_TO_SOT_SMD:SOT-323_SC-70
```

Validated schematic connection:

```text
Pin 1 -> protected +5 V rail
Pin 2 -> NC
Pin 3 -> GND
```

The device contains two protection channels; Revision 1.5 intentionally uses one channel for the +5 V supply rail.

### Validation Status

**PASS**

The symbol, internal topology and schematic connection have been checked against the Nexperia datasheet.

---

# 10. Status LEDs

## 10.1 D1 — Power Indicator

D1 is a 3 mm through-hole power indicator LED.

KiCad footprint:

```text
LED_THT:LED_D3.0mm
```

The customer may select:

* Red
* Blue
* White

The current-limiting resistor is:

```text
R_LED1 = 4.7 kΩ
```

Approved LED variants shall be maintained in `ALTERNATE_PARTS.md`.

---

## 10.2 D7 — Autofire Status Indicator

**Manufacturer:** Bivar
**MPN:** `3BC-3-F`
**Type:** 3 mm dual-colour Red/Green LED
**Configuration:** Common cathode

KiCad footprint:

```text
LED_THT:LED_D3.0mm-3
```

Validated pinout:

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

The common-cathode version is required by the current Revision 1.5 LED-driver topology.

### Validation Status

**PASS**

The LED datasheet pinout has been checked against the KiCad symbol and footprint mapping.

---

# 11. Gameplay Switches

Revision 1.5 uses eight MX-compatible mechanical switches:

* UP
* DOWN
* LEFT
* RIGHT
* FIRE buttons

The preferred mechanical switch is:

**Gateron KS-8 Yellow**

Quantity:

```text
8 per controller
```

The switches are installed without soldering into hot-swap sockets.

---

# 12. MX Hot-Swap Sockets

**Manufacturer:** Kaihua / Kailh
**MPN:** `CPG151101S11`

Quantity:

```text
8 per controller
```

KiCad footprint:

```text
PCM_Switch_Keyboard_Hotswap_Kailh:SW_Hotswap_Kailh_MX
```

The sockets allow compatible Cherry MX-style switches to be replaced without PCB soldering.

The hot-swap socket is a separate physical BOM item from the mechanical switch itself.

---

# 13. Autofire Toggle Switches

Both autofire control functions use the same physical E-Switch device:

**Manufacturer:** E-Switch
**MPN:** `100SP1T1B4M2QE`

Functions:

* Autofire OFF / ON
* Autofire SLOW / FAST

Revision 1.5 intentionally uses different KiCad symbol/footprint mappings for the two positions because the validated schematic and PCB were adapted to the physical switch orientation.

The current working mappings shall not be altered solely to make their KiCad names identical.

Validated user behaviour:

```text
Autofire selector:
OFF / ON

Speed selector:
LEFT  -> SLOW
RIGHT -> FAST
```

---

# 14. DB9 Cable

The controller uses a generic molded DB9 female controller cable with flying leads.

Current approved supplier item:

```text
AliExpress Item ID: 1005009578092300
```

The PCB-side conductors are soldered directly to the J1 pads.

Detailed assembly and verification instructions are maintained in:

```text
docs/assembly/CABLE_ASSEMBLY.md
```

Wire colours shall not be trusted automatically for new supplier batches.

The first cable from every new batch must be verified by continuity measurement.

---

# 15. J1 Cable Pads

J1 consists of PCB solder pads rather than a separately procured connector.

KiCad footprint:

```text
Connector_Wire:SolderWirePad_1x01_SMD_1.5x3mm
```

J1 is therefore:

```text
DNP / no procurement item
```

The DB9 pin numbering is intentionally kept aligned with the J1 pad numbering wherever possible.

---

# 16. Assembly Notes

## ICM7555 Soldering

Particular care shall be taken when soldering U1.

During prototype assembly, excess or incompletely reflowed solder paste beneath the SOIC-8 package caused:

* VCC-GND short circuits
* collapsed supply voltage
* incorrect autofire operation

After soldering U1:

1. visually inspect all pins
2. clean excess flux and paste
3. measure resistance between +5 V and GND before first power-up
4. verify that no low-resistance short circuit exists

---

# 17. Production Validation Requirements

Before Revision 1.5 is released for production, the following shall be verified:

* schematic ERC passes
* PCB DRC passes
* D4/D5 footprint and routing verified
* D6 pinout and protection topology verified
* D7 pinout and common-cathode configuration verified
* MMBT3904 symbol-to-footprint mapping verified
* 2N7002 symbol-to-footprint mapping verified
* DB9 cable pin mapping verified
* +5 V and GND continuity verified
* no VCC-GND short circuit
* autofire OFF operation verified
* autofire SLOW operation verified
* autofire FAST operation verified
* FIRE1 and FIRE2 verified
* all four directional inputs verified
* both LED indication states verified

---

# 18. BOM Release Status

The Revision 1.5 component-selection phase is considered complete.

Current BOM maturity:

**Pre-Release Validated**

The BOM may be promoted to **Version 1.0 / Production Approved** after:

1. final schematic review
2. final PCB review
3. first Revision 1.5 prototype assembly
4. full functional validation
5. manufacturing validation

---

# 19. Version History

| Document Version | Date           | Status                    | Changes                                                                                                                                          |
| ---------------- | -------------- | ------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------ |
| 0.1              | Not recorded   | Draft                     | Initial Revision 1.5 BOM structure                                                                                                               |
| 0.5              | Not recorded   | Draft                     | Initial component grouping and candidate selection                                                                                               |
| 0.8              | Not recorded   | Engineering Review        | Protection, timer, logic, hot-swap and LED component selection                                                                                   |
| **0.9**          | **2026-08-18** | **Pre-Release Validated** | Consolidated component selections, finalized autofire values, protection devices, LEDs, switches, cable assembly references and validation notes |

---

# 20. Next Revision

The next planned document revision is:

**BOM README v1.0**

Target condition:

**Revision 1.5 prototype successfully assembled and fully validated.**
