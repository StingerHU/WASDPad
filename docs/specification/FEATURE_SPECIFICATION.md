# WASDPad+ Rev 1.5 — Feature Specification

**Document Version:** 1.2  
**Hardware Revision:** Rev 1.5  
**Status:** Engineering Validation  
**Last Updated:** 2026-08-19

---

## 1. Purpose

This document defines the functional features and expected user-visible behaviour of **WASDPad+ Rev 1.5**.

Rev 1.5 is a fully hardware-based controller. It requires no microcontroller, firmware, driver or configuration software.

Detailed hardware implementation is documented separately in:

```text
hardware/rev1.5/README.md
docs/architecture/System_architecture.md
```

---

## 2. Feature Summary

Rev 1.5 provides:

- four independent digital directions
- FIRE1
- FIRE2
- hardware autofire for FIRE1
- dedicated autofire OFF / ON control
- SLOW / FAST autofire selection
- power indication
- dual-colour autofire indication
- eight MX-compatible hot-swap gameplay switches
- electrical protection
- direct DE-9 joystick interface

---

## 3. Directional Controls

The controller provides four independent digital directions:

```text
UP
DOWN
LEFT
RIGHT
```

Each direction uses its own physical switch and electrical signal path.

Rev 1.5 does not implement software scanning or SOCD filtering.

Multiple directions may therefore be physically activated simultaneously.

---

## 4. FIRE Controls

### FIRE1

FIRE1 is the primary action button:

```text
DE-9 pin 6
```

It supports both:

- manual FIRE operation
- hardware autofire

With autofire disabled, FIRE1 behaves as a normal joystick FIRE button.

### FIRE2

FIRE2 is an independent secondary action button:

```text
DE-9 pin 9 / POTX
```

FIRE2 is manually controlled and does not use autofire in Rev 1.5.

FIRE2 functionality depends on host-system and software support.

---

## 5. Hardware Autofire

Rev 1.5 provides hardware-generated autofire for FIRE1.

Autofire requires no firmware or software.

Two separate controls are provided:

```text
AUTO:
OFF / ON

SPEED:
SLOW / FAST
```

When AUTO is OFF, FIRE1 operates normally.

When AUTO is ON, holding FIRE1 generates repeated FIRE pulses at the selected speed.

Releasing FIRE1 stops autofire.

---

## 6. Autofire Speed

Rev 1.5 provides two fixed autofire speeds.

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

The autofire rate is not continuously adjustable in Rev 1.5.

---

## 7. Status Indication

Rev 1.5 uses two separate LEDs.

### Power LED

D1 indicates that the controller is powered.

A 3 mm THT LED is used.

Production variants may use:

- Red
- Blue
- White

### Autofire LED

D7 is a red/green dual-colour status LED.

Primary device:

**Bivar 3BC-3-F**

Configuration:

**Common Cathode**

It provides visual feedback for the autofire system.

The final colour-to-state mapping shall be confirmed on the complete Rev 1.5 prototype.

---

## 8. Gameplay Switches

Rev 1.5 uses eight MX-compatible hot-swap gameplay switches.

Default switch:

**Gateron KS-8 Yellow**

Hot-swap socket:

**Kailh / Kaihua CPG151101S11**

Compatible MX-style switches may be substituted when their mechanical compatibility is confirmed.

Gameplay switches can be replaced without soldering them directly to the PCB.

---

## 9. Electrical Protection

Rev 1.5 includes protection for the controller and host interface.

The protection architecture includes:

- resettable +5 V overcurrent protection
- signal-line ESD protection
- +5 V ESD protection
- local supply decoupling

Primary devices are documented in the Rev 1.5 hardware documentation and BOM.

These protection features operate automatically and require no user configuration.

---

## 10. DE-9 Interface

Rev 1.5 uses a classic DE-9 joystick connection.

| Pin | Function |
|---:|---|
| 1 | UP |
| 2 | DOWN |
| 3 | LEFT |
| 4 | RIGHT |
| 5 | Auxiliary / unused by current Rev 1.5 cable assembly |
| 6 | FIRE1 |
| 7 | +5 V |
| 8 | GND |
| 9 | FIRE2 / POTX |

DE-9 pin number is the authoritative electrical reference.

Cable wire colours are not authoritative because they may vary between cable batches.

---

## 11. Target Platforms

Primary Rev 1.5 targets are:

- Commodore 64
- Commodore 128
- Commodore Amiga

Other systems using Atari-style DE-9 joystick interfaces may also be compatible.

Connector shape alone does not guarantee electrical compatibility.

---

## 12. Startup and Latency

Rev 1.5 has no software startup process.

After valid power is applied, the controller is immediately operational.

There is no:

- boot process
- firmware initialization
- pairing
- calibration
- software configuration
- input polling loop

Normal input latency is therefore determined by the mechanical switches and hardware signal paths rather than software processing.

---

## 13. Serviceability

The Rev 1.5 design emphasizes practical serviceability.

The eight gameplay switches are hot-swappable and can be replaced without soldering.

Other internal components may require normal electronic repair or soldering.

The enclosure is developed separately by **Dester3D** and shall provide suitable access and mechanical compatibility with the final Rev 1.5 hardware.

---

## 14. Rev 1.5 Functional Validation

Before Rev 1.5 is considered validated, the completed controller shall demonstrate correct operation of:

```text
Power indication

UP
DOWN
LEFT
RIGHT

FIRE1
FIRE2

Autofire OFF
Autofire SLOW
Autofire FAST

Autofire status indication
```

It shall also confirm:

- correct LEFT = SLOW / RIGHT = FAST behaviour
- FIRE1 release stops autofire
- FIRE2 remains independent
- all gameplay switches operate correctly
- no unintended joystick input activation occurs

Successful functional operation is the primary Rev 1.5 acceptance criterion.

---

## 15. Rev 1.5 Scope

Rev 1.5 intentionally does **not** include:

- microcontroller control
- firmware
- continuously adjustable autofire
- burst mode
- programmable debounce
- profiles
- macros
- USB HID
- USB configuration
- wireless operation
- programmable RGB effects

These are not missing Rev 1.5 features.

They belong to possible future programmable hardware revisions.

---

## 16. Future Rev 2.0

Rev 2.0 is planned as a separate programmable WASDPad+ platform.

Potential future functionality includes:

- adjustable FAST autofire
- burst mode
- firmware-controlled behaviour
- configurable debounce
- game profiles
- persistent configuration
- programmable status indication
- USB configuration/update
- optional USB HID

Rev 2.0 functionality shall remain separate from Rev 1.5 requirements.

---

## 17. Related Documentation

Current supporting documentation:

```text
hardware/rev1.5/
├── README.md
└── bom/
    ├── README.md
    ├── wasdpad+v1.5.csv
    ├── ALTERNATE_PARTS.md
    └── PROCUREMENT_NOTES.md

docs/
├── architecture/
│   └── System_architecture.md
├── assembly/
│   └── CABLE_ASSEMBLY.md
└── roadmap/
    └── ROADMAP.md
```

The authoritative component list is:

```text
hardware/rev1.5/bom/wasdpad+v1.5.csv
```

Documentation should remain compact and avoid duplicating information already maintained in another authoritative file.

---

## 18. Version History

| Version | Date | Changes |
|---|---|---|
| 1.0 | Not recorded | Initial Rev 1.5 feature specification |
| 1.1 | 2026-08-18 | Expanded feature definitions, validation criteria and Rev 1.5 / Rev 2.0 separation |
| **1.2** | **2026-08-19** | Simplified and consolidated specification; removed obsolete Project Specification and production-test references, removed detailed acceptance matrices and duplicated hardware information, and aligned documentation references with the current repository structure |

---

**WASDPad+ Rev 1.5 — Feature Specification**
