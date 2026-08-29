# WASDPad+ Rev1.5.1 — Feature Specification

**Document Version:** 2.0  
**Hardware Revision:** Rev1.5.1  
**Status:** Production Release Candidate  
**Last Updated:** 2026-08-29

---

## 1. Purpose

This document defines the functional features and expected user-visible behaviour of **WASDPad+ Rev1.5.1**.

Rev1.5.1 is a fully hardware-based controller.

It requires:

- no microcontroller
- no firmware
- no driver
- no configuration software
- no operating-system support
- no digital protocol conversion

The controller is designed around direct digital joystick signalling for retro-computer platforms.

Detailed implementation information is maintained separately in:

- `hardware/rev1.5/README.md`
- `hardware/rev1.5/Review_Record.MD`
- `docs/architecture/System_architecture.md`
- `hardware/rev1.5/bom/`

---

## 2. Feature Summary

Rev1.5.1 provides:

- four independent digital direction inputs
- FIRE1
- FIRE2
- hardware autofire for FIRE1
- dedicated autofire OFF / ON control
- fixed SLOW / FAST autofire selection
- power indication
- dual-colour autofire status indication
- eight MX-compatible hot-swappable gameplay switches
- warm-white key backlighting
- dedicated backlight ON / OFF control
- resettable +5 V overcurrent protection
- signal-line ESD protection
- +5 V ESD / TVS protection
- local supply decoupling
- dual-layer GND planes with stitching vias
- direct DE-9 joystick interface
- serviceable mechanical architecture
- no firmware or software dependency

---

## 3. Directional Controls

The controller provides four independent digital directions:

```text
UP
DOWN
LEFT
RIGHT
```

Each direction uses:

- its own physical gameplay switch
- its own electrical signal path
- direct hardware signalling

Rev1.5.1 does not implement:

- software scanning
- firmware debounce
- SOCD filtering
- input remapping

Multiple directions may therefore be physically activated simultaneously.

Examples include:

```text
UP + DOWN
LEFT + RIGHT
```

The connected host hardware and software determine the resulting behaviour.

---

## 4. FIRE Controls

### 4.1 FIRE1

FIRE1 is the primary action input.

DE-9 connection:

```text
Pin 6
```

FIRE1 supports:

- manual FIRE operation
- hardware autofire

Two physical FIRE1 switches are provided:

```text
FIRE1 LEFT
FIRE1 RIGHT
```

Both operate the same logical FIRE1 function.

With autofire disabled, FIRE1 behaves as a normal digital joystick fire button.

### 4.2 FIRE2

FIRE2 is an independent secondary action input.

DE-9 connection:

```text
Pin 9 / POTX
```

Two physical FIRE2 switches are provided:

```text
FIRE2 LEFT
FIRE2 RIGHT
```

FIRE2:

- is manually controlled
- is independent from FIRE1
- does not use autofire in Rev1.5.1

FIRE2 functionality depends on host-system and software support.

---

## 5. Gameplay Switch Layout

Rev1.5.1 provides eight gameplay switch positions:

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

The duplicated FIRE1 and FIRE2 controls provide an ambidextrous control layout.

The gameplay switch architecture is electrically direct and does not use a keyboard matrix.

---

## 6. Hot-Swap Mechanical Switches

All eight gameplay switches are installed using MX-compatible hot-swap sockets.

Production socket:

**Kailh / Kaihua `CPG151101S11`**

Production-fitted mechanical switch:

**Gateron KS-8 Yellow**

The switches can be replaced without soldering them directly to the PCB.

Compatible MX-style switches may be substituted when mechanical compatibility is confirmed.

This allows:

- switch replacement
- user preference changes
- easier servicing
- reduced PCB rework

---

## 7. Hardware Autofire

Rev1.5.1 provides hardware-generated autofire for FIRE1.

The autofire system uses a CMOS 555 timer.

Production device:

**Texas Instruments `TLC555CDR`**

Autofire requires:

- no firmware
- no software
- no microcontroller
- no external configuration

Two independent controls are provided:

```text
AUTO:
OFF / ON

SPEED:
SLOW / FAST
```

When AUTO is OFF:

- FIRE1 operates normally

When AUTO is ON:

- holding FIRE1 generates repeated FIRE pulses
- the selected SLOW / FAST mode determines the pulse rate
- releasing FIRE1 stops autofire

Autofire applies only to FIRE1.

---

## 8. Autofire Speed

Rev1.5.1 provides two fixed autofire speeds.

| Mode | Timing Resistor |
|---|---:|
| FAST | 330 kΩ |
| SLOW | 680 kΩ |

Implementation:

```text
R13 = 330 kΩ -> FAST
R14 = 680 kΩ -> SLOW
```

The values were selected through physical gameplay testing.

Validated physical selector orientation:

```text
LEFT  -> SLOW
RIGHT -> FAST
```

The autofire rate is not continuously adjustable in Rev1.5.1.

This is intentional.

Fixed hardware timing provides:

- repeatability
- predictable gameplay behaviour
- reduced accidental misconfiguration
- consistent units

---

## 9. Autofire Mode Switching

Autofire mode selection is performed using discrete hardware.

Production switching IC:

**Texas Instruments `CD4066BM96`**

The CD4066 provides hardware switching between the autofire timing paths.

No programmable logic is involved.

---

## 10. Autofire Status Indication

Rev1.5.1 uses a dedicated red/green dual-colour LED.

Reference:

```text
D7
```

Production device:

**Bivar `3BC-3-F`**

Configuration:

```text
Common Cathode
```

Validated pinout:

```text
Pin 1 = Red anode
Pin 2 = Common cathode
Pin 3 = Green anode
```

The LED provides visual feedback for the selected autofire state / speed.

Driver stages use:

**MMBT3904 NPN transistors**

References:

```text
Q8
Q9
```

Associated LED resistors:

```text
R22 = 270 Ω
R23 = 330 Ω
```

The dual-colour LED replaces the earlier separate autofire indicator concept.

---

## 11. Power Indication

Reference:

```text
D1
```

D1 indicates that the controller is powered.

Production type:

**3 mm red THT LED**

Production MPN:

**Bivar `3RD-F`**

Current-limiting resistor:

```text
R_LED1 = 4.7 kΩ
```

Power indication is functionally independent from the autofire status LED.

---

## 12. Key Backlighting

Rev1.5.1 adds backlighting beneath all eight gameplay switches.

References:

```text
D8–D15
```

Production device:

**XINGLIGHT `XL-2012WWC`**

Package:

```text
0805
```

Colour:

```text
Warm white
```

Each LED has its own current-limiting resistor.

References:

```text
R24–R31
```

Value:

```text
3.3 kΩ
```

The LEDs are intentionally operated at relatively low current.

The intended visual effect is:

- subtle
- even
- non-distracting
- suitable for illuminated keycaps

The backlight is not intended as a high-brightness decorative lighting system.

---

## 13. Backlight Control

The key backlight has a dedicated hardware ON / OFF control.

Reference:

```text
U3
```

Production device:

**C&K `PCM12SMTR`**

PCB side:

```text
Bottom
```

The switch controls a dedicated backlight supply rail:

```text
BACKLIGHT_5V
```

Backlight control is independent from:

- direction inputs
- FIRE1
- FIRE2
- autofire timing
- power indication
- autofire status indication

Disabling the backlight does not affect gameplay functionality.

---

## 14. Electrical Protection

Rev1.5.1 includes several protection stages for the controller and connected retro-computer hardware.

The protection architecture includes:

- resettable +5 V overcurrent protection
- signal-line ESD protection
- +5 V ESD / TVS protection
- local supply decoupling
- dual-layer GND distribution

These protection features operate automatically.

No user configuration is required.

---

## 15. +5 V Overcurrent Protection

Reference:

```text
F2
```

Production device:

**Littelfuse `1206L005/30WR`**

The resettable PPTC protects the host joystick-port +5 V supply against sustained overcurrent conditions.

The device automatically resets after the fault condition is removed and the device cools.

---

## 16. Signal-Line ESD Protection

References:

```text
D4
D5
```

Production device:

**TECH PUBLIC `PESD5V0S4UD`**

These devices provide ESD protection for externally accessible controller signal lines.

The protection devices are transparent during normal controller operation.

Their function is to reduce the risk of damage caused by electrostatic discharge during:

- handling
- connection
- disconnection
- normal use

---

## 17. +5 V ESD / TVS Protection

Reference:

```text
D6
```

Production device:

**TECH PUBLIC `TPE0562BC3`**

The device protects the +5 V supply path against transient events.

Validated Rev1.5.1 connection:

```text
Pin 1 -> protected +5 V
Pin 2 -> NC
Pin 3 -> GND
```

The production-selected device was explicitly reviewed for:

- package
- pinout
- topology
- working voltage
- PCB connection

---

## 18. Power Distribution and Decoupling

Rev1.5.1 includes local ceramic decoupling and PCB ground planes.

Key functions include:

- stabilizing the +5 V supply
- reducing local switching noise
- lowering ground impedance
- improving power integrity

The PCB uses GND copper zones on both layers.

The planes are connected using stitching vias.

---

## 19. DE-9 Interface

Rev1.5.1 uses the classic DE-9 digital joystick interface.

| Pin | Function |
|---|---|
| 1 | UP |
| 2 | DOWN |
| 3 | LEFT |
| 4 | RIGHT |
| 5 | Auxiliary / unused by current Rev1.5.1 cable assembly |
| 6 | FIRE1 |
| 7 | +5 V |
| 8 | GND |
| 9 | FIRE2 / POTX |

The DE-9 pin number is the authoritative electrical reference.

Cable wire colours are not authoritative because conductor colours may vary between cable batches.

---

## 20. Cable Interface

The controller uses a molded female DE-9 cable with flying leads.

The cable is soldered directly to PCB pads.

The PCB interface is designated:

```text
J1
```

J1 is a PCB feature rather than a separately procured connector.

A cable from a new supplier or production batch should be continuity-tested before production assembly.

---

## 21. Target Platforms

Primary Rev1.5.1 targets include:

- Commodore 64
- Commodore 128
- Commodore Amiga

Other systems using electrically compatible Atari-style digital joystick interfaces may also be supported.

Connector shape alone does not guarantee electrical compatibility.

Platform compatibility must be verified before being considered officially supported.

---

## 22. FIRE2 Platform Support

FIRE2 uses the second-fire / POTX-capable line.

The hardware provides the signal electrically.

Actual functionality depends on:

- host hardware
- software
- game support
- platform-specific joystick implementation

FIRE2 support shall therefore not be assumed solely because the connector provides pin 9.

---

## 23. Plus/4 Family Compatibility

Commodore Plus/4-family systems use a different physical joystick connector.

Compatibility requires an adapter.

The adapter performs electrical pin mapping only.

No protocol conversion or firmware is required.

---

## 24. Startup Behaviour

Rev1.5.1 has no software startup process.

After valid power is applied, the controller is immediately operational.

There is no:

- boot process
- firmware initialization
- pairing
- calibration
- configuration loading
- software initialization
- input polling loop

---

## 25. Input Latency

Manual input latency is determined primarily by:

- mechanical switch behaviour
- discrete transistor / MOSFET propagation
- host-system input detection

There is no firmware or software processing pipeline inside the controller.

Electronic propagation delay inside the controller is negligible relative to:

- human reaction times
- mechanical switch timing
- retro-computer frame timing

---

## 26. Serviceability

Rev1.5.1 emphasizes practical serviceability.

The gameplay switches are hot-swappable and can be replaced without soldering.

Other serviceable elements include:

- conventional discrete components
- documented component MPNs
- documented footprints
- documented datasheets
- standard SMD passives
- replaceable external cable

No programmed component is required for basic controller operation.

---

## 27. Assembly Model

Rev1.5.1 uses a mixed assembly process.

### Top SMD

Includes most:

- ICs
- MOSFETs
- transistors
- resistors
- capacitors
- ESD protection devices
- backlight LEDs

### Bottom SMD / Manual

Includes:

- U3
- SW1–SW8 Kailh hot-swap sockets

### THT

Includes:

- D1
- D2
- D7
- SW_AUTO1
- SW_SPEED1

### Mechanical / Manual

Includes:

- eight MX mechanical switches

### Cable / Manual

Includes:

- DE-9 controller cable

---

## 28. Manufacturing Documentation

The authoritative Rev1.5.1 manufacturing documentation is located under:

```text
hardware/rev1.5/bom/
```

Primary files:

```text
WASDPad_Rev1.5.1_FULL_MASTER_BOM.csv
WASDPad_Rev1.5.1_FULL_MASTER_CPL.csv
DATASHEET_INDEX.md
ALTERNATE_PARTS.md
PROCUREMENT_NOTES.md
```

The Master BOM is authoritative for component identity.

The Master CPL is authoritative for placement data.

---

## 29. Feature Validation Status

The Rev1.5.1 feature set has completed pre-production engineering review.

| Feature | Status |
|---|---|
| Direction controls | Engineering PASS |
| FIRE1 | Engineering PASS |
| FIRE2 | Engineering PASS |
| Hardware autofire | Engineering PASS |
| SLOW / FAST selection | Engineering PASS |
| Power indication | Engineering PASS |
| Dual-colour autofire indication | Engineering PASS |
| Hot-swap switch architecture | Engineering PASS |
| Signal ESD protection | Engineering PASS |
| +5 V overcurrent protection | Engineering PASS |
| +5 V ESD / TVS protection | Engineering PASS |
| Key backlighting | Engineering PASS |
| Backlight control | Engineering PASS |
| PCB layout | PASS |
| ERC | PASS |
| DRC | PASS |
| Gerber generation | PASS |
| Master BOM | Complete |
| Master CPL | Complete |
| Physical Rev1.5.1 validation | Pending |

The hardware is therefore classified as:

**Production Release Candidate**

---

## 30. Physical Functional Validation

Before Rev1.5.1 is considered **Production Approved**, the completed production-candidate controller shall demonstrate correct operation of:

```text
Power indication

UP
DOWN
LEFT
RIGHT

FIRE1 LEFT
FIRE1 RIGHT

FIRE2 LEFT
FIRE2 RIGHT

Autofire OFF
Autofire SLOW
Autofire FAST

Dual-colour autofire indication

D8–D15 key backlighting
Backlight ON / OFF
```

Additional checks include:

- correct LEFT = SLOW / RIGHT = FAST behaviour
- FIRE1 release stops autofire
- FIRE2 remains independent
- all gameplay switches operate correctly
- no unintended joystick input activation occurs
- no +5 V / GND short circuit
- no abnormal heating
- hot-swap sockets retain switches correctly
- mechanical switches can be replaced
- cable mapping is correct

Successful physical operation is the final Rev1.5.1 acceptance criterion.

---

## 31. Real-System Validation

The production-candidate controller should be validated on representative original hardware.

Planned targets include:

- Commodore 64
- Commodore 128 where applicable
- Commodore Amiga

Validation should include:

- basic joystick operation
- FIRE1
- FIRE2 where supported
- autofire gameplay
- extended gameplay
- repeated mode changes
- key backlight operation
- mechanical switch use

---

## 32. Rev1.5.1 Scope

Rev1.5.1 intentionally does not include:

- microcontroller control
- firmware
- continuously adjustable autofire
- burst mode
- programmable debounce
- user profiles
- macros
- USB HID
- USB configuration
- wireless operation
- programmable RGB effects
- game-specific programmable logic

These are not missing Rev1.5.1 features.

They belong to possible future programmable hardware revisions.

---

## 33. Future Rev2.0

Rev2.0 is planned as a separate programmable WASDPad+ platform.

Potential future functionality may include:

- adjustable autofire
- burst-fire modes
- firmware-controlled behaviour
- configurable debounce
- game profiles
- persistent configuration
- programmable status indication
- USB configuration
- firmware update capability
- optional USB HID functionality

An MCU platform such as the RP2040 family may be evaluated.

Rev2.0 functionality shall remain separate from Rev1.5.1 requirements.

---

## 34. Feature Freeze

The Rev1.5.1 feature set is frozen for the production candidate.

No additional Rev1.5.1 features should be introduced before physical production validation.

Changes affecting:

- functionality
- timing
- PCB topology
- connector behaviour
- protection architecture
- mechanical compatibility
- assembly process

require explicit engineering review.

---

## 35. Related Documentation

Current supporting documentation:

```text
hardware/
├── README.md
└── rev1.5/
    ├── README.md
    ├── Review_Record.MD
    └── bom/
        ├── README.md
        ├── WASDPad_Rev1.5.1_FULL_MASTER_BOM.csv
        ├── WASDPad_Rev1.5.1_FULL_MASTER_CPL.csv
        ├── DATASHEET_INDEX.md
        ├── ALTERNATE_PARTS.md
        └── PROCUREMENT_NOTES.md

docs/
├── architecture/
│   └── System_architecture.md
├── assembly/
│   └── CABLE_ASSEMBLY.md
├── roadmap/
│   └── ROADMAP.md
└── specification/
    └── FEATURE_SPECIFICATION.md
```

Authoritative production component list:

```text
hardware/rev1.5/bom/WASDPad_Rev1.5.1_FULL_MASTER_BOM.csv
```

Authoritative placement data:

```text
hardware/rev1.5/bom/WASDPad_Rev1.5.1_FULL_MASTER_CPL.csv
```

Engineering review:

```text
hardware/rev1.5/Review_Record.MD
```

---

## 36. Documentation Authority

For Rev1.5.1:

**Feature behaviour**

→ `FEATURE_SPECIFICATION.md`

**System architecture**

→ `System_architecture.md`

**Production component identity**

→ `WASDPad_Rev1.5.1_FULL_MASTER_BOM.csv`

**Placement data**

→ `WASDPad_Rev1.5.1_FULL_MASTER_CPL.csv`

**Datasheets**

→ `DATASHEET_INDEX.md`

**Component substitutions**

→ `ALTERNATE_PARTS.md`

**Procurement**

→ `PROCUREMENT_NOTES.md`

**Engineering release status**

→ `Review_Record.MD`

---

## 37. Release Status

**Hardware Revision:** WASDPad+ Rev1.5.1  
**Feature Specification Version:** 2.0  
**Status:** Production Release Candidate

The Rev1.5.1 feature set is complete and frozen.

Engineering validation of the design and manufacturing dataset is complete.

Final promotion to:

**Production Approved**

requires successful physical validation of manufactured Rev1.5.1 hardware.

---

## 38. Version History

| Version | Date | Changes |
|---|---|---|
| 1.0 | Not recorded | Initial Rev1.5 feature specification |
| 1.1 | 2026-08-18 | Expanded feature definitions, validation criteria and Rev1.5 / Rev2.0 separation |
| 1.2 | 2026-08-19 | Simplified and consolidated specification; removed obsolete Project Specification and duplicated hardware information |
| **2.0** | **2026-08-29** | Updated to Rev1.5.1 Production Release Candidate; added final production autofire architecture, hot-swap system, ESD/PTC protection, dual-colour status indication, key backlighting, U3 backlight control, manufacturing structure, Master BOM/CPL references, physical validation gate and feature freeze |

---

**WASDPad+ Rev1.5.1 — Feature Specification**  
**Status: Production Release Candidate**
