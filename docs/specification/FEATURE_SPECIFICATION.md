# WASDPad+ Feature Specification
## Hardware Revision 1.5

**Document Version:** 1.1  
**Hardware Revision:** Rev 1.5  
**Status:** Engineering Specification / Pre-Prototype  
**Last Updated:** 2026-08-18

---

# 1. Purpose

This document defines the functional behaviour and user-visible features of **WASDPad+ Hardware Revision 1.5**.

It specifies what the controller shall do from the user's perspective and provides acceptance criteria for later prototype and production validation.

Implementation details are documented separately in:

```text
docs/architecture/System_architecture.md
docs/specification/PROJECT_SPECIFICATION.md
hardware/rev1.5/README.md
hardware/rev1.5/bom/
```

---

# 2. Feature Status Definitions

| Status | Meaning |
|---|---|
| Defined | Feature behaviour is specified |
| Physically Validated | Behaviour/value has already been tested on existing hardware |
| Validation Pending | Designed for Rev 1.5 but requires validation on the final Rev 1.5 prototype |
| Future | Not part of Rev 1.5 |

---

# 3. Rev 1.5 Feature Summary

| ID | Feature | Status |
|---|---|---|
| F-001 | Digital directional control | Defined |
| F-002 | FIRE1 | Defined |
| F-003 | FIRE2 | Defined |
| F-004 | Hardware autofire | Defined |
| F-005 | Autofire OFF / ON control | Defined |
| F-006 | SLOW / FAST selection | Physically Validated |
| F-007 | Power indication | Defined |
| F-008 | Dual-colour autofire indication | Defined |
| F-009 | MX hot-swap switches | Defined |
| F-010 | Electrical protection | Defined |
| F-011 | Immediate startup | Defined |
| F-012 | Hardware-only operation | Defined |
| F-013 | DB9 controller interface | Defined |
| F-014 | Serviceability | Defined |

Final Rev 1.5 prototype validation remains pending.

---

# 4. F-001 — Digital Directional Control

## Description

The controller provides four independent digital directional controls:

```text
UP
DOWN
LEFT
RIGHT
```

Each direction is controlled by an independent mechanical switch.

No firmware scanning or software interpretation is used.

## Behaviour

Pressing a direction shall immediately activate the corresponding joystick signal.

Releasing the switch shall return that signal to its inactive state.

Multiple direction switches may be physically pressed simultaneously.

Rev 1.5 does not implement firmware-based SOCD filtering or direction arbitration.

## Acceptance Criteria

- UP activates only the intended UP signal.
- DOWN activates only the intended DOWN signal.
- LEFT activates only the intended LEFT signal.
- RIGHT activates only the intended RIGHT signal.
- Releasing a switch clears its corresponding signal.
- One direction shall not unintentionally activate another.
- No software or configuration shall be required.

---

# 5. F-002 — FIRE1

## Description

FIRE1 is the primary action button.

Host interface:

```text
DB9 pin 6
```

FIRE1 supports:

- direct manual firing
- hardware autofire

## Manual Behaviour

With autofire disabled, FIRE1 shall behave as a conventional joystick FIRE button.

Pressing FIRE1 shall activate FIRE1.

Releasing FIRE1 shall immediately deactivate it.

## Acceptance Criteria

With autofire OFF:

- FIRE1 press activates FIRE1.
- FIRE1 release deactivates FIRE1.
- No automatic pulses are generated.
- FIRE2 behaviour is unaffected.

---

# 6. F-003 — FIRE2

## Description

FIRE2 is an independent secondary action button.

Rev 1.5 uses:

```text
DB9 pin 9 / POTX
```

FIRE2 is a direct manual control.

Autofire is intentionally not applied to FIRE2 in Rev 1.5.

## Acceptance Criteria

- FIRE2 activates only while commanded by the FIRE2 switch.
- FIRE1 operation does not unintentionally activate FIRE2.
- Autofire state does not cause automatic FIRE2 pulses.

Host support for FIRE2 / POTX is platform-dependent.

---

# 7. F-004 — Hardware Autofire

## Description

Rev 1.5 provides hardware-generated autofire for FIRE1.

Autofire repeatedly generates FIRE1 activity while the FIRE1 button is held.

The function is implemented entirely in hardware.

It requires:

- no firmware
- no software
- no host configuration

## Behaviour

When autofire is enabled:

```text
FIRE1 held
    |
    v
Repeated FIRE1 pulses
```

When FIRE1 is released, automatic firing shall stop.

## Acceptance Criteria

- Autofire affects FIRE1 only.
- Autofire operates without software.
- FIRE1 must be physically held for continuous autofire operation.
- Releasing FIRE1 stops automatic firing.
- FIRE2 remains independent.

---

# 8. F-005 — Autofire OFF / ON Control

## Description

Autofire enable is controlled by a dedicated physical toggle switch.

Available states:

```text
OFF
ON
```

This switch is independent from the SLOW / FAST selector.

## OFF Behaviour

With autofire OFF:

- automatic FIRE1 pulses are disabled
- FIRE1 remains available as a normal manual button

## ON Behaviour

With autofire ON:

- the hardware autofire circuit becomes available
- the selected SLOW / FAST timing determines the firing rate

## Acceptance Criteria

- OFF disables automatic firing.
- Manual FIRE1 remains functional while OFF.
- ON enables autofire operation.
- Switching OFF shall not leave FIRE1 asserted.
- Autofire enable state shall not affect directional controls or FIRE2.

---

# 9. F-006 — Autofire SLOW / FAST Selection

## Description

A separate physical toggle switch selects one of two fixed autofire speeds.

The Rev 1.5 values are:

| Mode | Timing Resistance |
|---|---:|
| FAST | 330 kΩ |
| SLOW | 680 kΩ |

Implementation references:

```text
R13 = 330 kΩ -> FAST
R14 = 680 kΩ -> SLOW
```

These values were selected through physical gameplay testing.

## Physical Switch Behaviour

The validated switch orientation is:

```text
LEFT  -> SLOW
RIGHT -> FAST
```

## Behaviour

SLOW shall provide a clearly lower firing rate than FAST.

The speed selection is hardware-defined and is not continuously adjustable.

## Acceptance Criteria

- LEFT selects SLOW.
- RIGHT selects FAST.
- SLOW produces a lower autofire frequency than FAST.
- Both settings operate reliably with FIRE1.
- Changing speed requires no restart or software action.

**Status:** Physically Validated

---

# 10. F-007 — Power Indication

## Description

Rev 1.5 provides a dedicated power indicator:

```text
D1
```

D1 is a 3 mm THT LED.

Production colour may be selected as:

- Red
- Blue
- White

The colour is a product configuration option and does not alter controller behaviour.

## Acceptance Criteria

When the controller receives normal operating power:

- D1 shall provide visible power indication.

The indicator shall not materially affect controller operation.

---

# 11. F-008 — Dual-Colour Autofire Indication

## Description

Autofire status is indicated using a separate red/green dual-colour LED:

**Bivar 3BC-3-F**

Electrical configuration:

**Common Cathode**

Validated pin assignment:

```text
Pin 1 -> RED anode
Pin 2 -> Common cathode
Pin 3 -> GREEN anode
```

The two colour channels are independently driven.

## Functional Requirement

The indication shall allow the user to distinguish the relevant autofire operating state/speed visually.

The exact final user-facing colour-to-mode mapping shall match the final validated Rev 1.5 schematic and assembled prototype.

## Acceptance Criteria

- Both LED channels operate independently.
- The displayed state corresponds to the actual autofire state.
- SLOW and FAST shall not produce an ambiguous indication.
- Autofire indication shall not interfere with FIRE operation.

**Final prototype validation:** Pending

---

# 12. F-009 — MX Hot-Swap Switches

## Description

Rev 1.5 uses MX-compatible hot-swappable gameplay switches.

Primary socket:

**Kailh / Kaihua CPG151101S11**

Default gameplay switch:

**Gateron KS-8 Yellow**

Quantity:

```text
8 switches
8 hot-swap sockets
```

## Behaviour

Gameplay switches shall be replaceable without soldering the switch to the PCB.

Other compatible MX-style switches may be used when mechanical compatibility is confirmed.

Potential compatible families include suitable variants from:

- Gateron
- Cherry MX
- Kailh
- TTC
- other mechanically compatible MX-style manufacturers

Compatibility shall not be assumed solely from marketing terminology.

## Acceptance Criteria

- Each switch is securely retained.
- Each installed switch operates electrically.
- Switches can be removed without PCB soldering.
- Replacement does not damage the hot-swap socket during normal use.
- Switch and enclosure clearances are adequate.

---

# 13. F-010 — Electrical Protection

## Description

Rev 1.5 integrates electrical protection without requiring user configuration.

Protection includes:

- resettable +5 V overcurrent protection
- ESD protection for external signal lines
- ESD protection for the +5 V supply
- local supply decoupling

Primary protection architecture includes:

```text
Littelfuse 1206L005/30WR
Nexperia PESD5V0S4UD
Nexperia PESD6V0L2UU
```

## User Behaviour

Protection is automatic.

The user shall not need to:

- configure protection
- reset a fuse manually during normal operation
- install external protection hardware

## Acceptance Criteria

Final prototype validation shall confirm:

- normal controller operation through the protection network
- acceptable supply voltage
- acceptable current consumption
- correct ESD-device topology
- absence of unintended +5 V/GND shorts

---

# 14. F-011 — Immediate Startup

## Description

Rev 1.5 has no software startup process.

After connection to a compatible powered host, the controller shall become operational without user initialization.

## No Startup Requirement

The controller requires no:

- boot process
- calibration
- pairing
- profile loading
- firmware initialization
- configuration utility

## Acceptance Criteria

After valid power is applied:

- directional controls are immediately usable
- FIRE controls are immediately usable
- no user startup procedure is required

---

# 15. F-012 — Hardware-Only Operation

## Description

Rev 1.5 is intentionally a hardware-only controller.

Normal operation requires no:

- microcontroller
- firmware
- USB stack
- host driver
- configuration software
- programmable logic

## User Benefit

This architecture provides:

- deterministic behaviour
- no firmware maintenance
- no software dependency
- immediate operation
- very low processing latency

## Acceptance Criteria

All normal Rev 1.5 gameplay functions shall operate without any programmable device or software component.

---

# 16. F-013 — DB9 Controller Interface

## Description

Rev 1.5 connects to the host using a classic DE-9 / DB9 joystick interface.

Primary mapping:

| Pin | Function |
|---:|---|
| 1 | UP |
| 2 | DOWN |
| 3 | LEFT |
| 4 | RIGHT |
| 5 | Auxiliary / unused by current cable assembly |
| 6 | FIRE1 |
| 7 | +5 V |
| 8 | GND |
| 9 | FIRE2 / POTX |

## Cable Requirement

DB9 pin number is authoritative.

Wire colour is batch-specific and shall not define functionality.

## Acceptance Criteria

- Cable continuity matches the documented DB9 mapping.
- +5 V is correctly connected to pin 7.
- GND is correctly connected to pin 8.
- No unintended cross-connections exist.

Detailed assembly requirements:

```text
docs/assembly/CABLE_ASSEMBLY.md
```

---

# 17. F-014 — Mechanical Serviceability

## Description

Rev 1.5 is designed to improve serviceability compared with permanently soldered controller-switch designs.

The primary user-serviceable components are the eight gameplay switches.

The enclosure and PCB architecture should also permit controlled access for repair or replacement of internal components.

## Requirements

Normal maintenance should not require destructive disassembly.

Hot-swap gameplay-switch replacement shall not require soldering.

Replacement of components such as:

- cable
- PCB
- toggle switches

may require disassembly and soldering.

## Acceptance Criteria

- Enclosure can be opened without intentional destruction.
- Hot-swap switches can be accessed and replaced.
- PCB can be accessed for servicing.
- Cable strain relief can be inspected and serviced.

Final mechanical acceptance depends on the production enclosure.

---

# 18. Compatibility

## Primary Rev 1.5 Targets

The primary development targets are:

- Commodore 64
- Commodore 128
- Commodore Amiga

## Other Platforms

Other Atari-style DE-9 systems may be compatible, but physical connector compatibility alone is insufficient.

Platform-specific validation must consider:

- pin assignment
- +5 V availability
- FIRE2 / POT usage
- auxiliary signals
- electrical behaviour

Systems requiring pin or electrical conversion shall be considered adapter-dependent.

They shall not automatically be described as natively supported.

---

# 19. User Configuration

Rev 1.5 intentionally minimizes configuration.

User-accessible hardware choices are:

```text
Autofire: OFF / ON
Speed:    SLOW / FAST
```

The gameplay switches may also be physically replaced with compatible MX-style switches.

No digital configuration is required.

There is no:

- configuration software
- firmware menu
- profile manager
- USB setup
- calibration utility

---

# 20. Timing and Latency Behaviour

Rev 1.5 introduces no intentional firmware or software latency.

Normal input propagation is determined by:

- mechanical switch behaviour
- discrete circuitry
- CMOS logic propagation
- autofire timing network where applicable

There is no polling interval or firmware input-processing loop.

---

# 21. Reliability Requirements

Rev 1.5 is intended for repeated gameplay use.

Required characteristics include:

- stable autofire timing
- reliable direction switching
- reliable FIRE operation
- consistent electrical behaviour
- secure hot-swap socket operation
- adequate cable strain relief
- predictable switch selection
- protection of the host interface

Final reliability claims require validation on production-representative hardware.

---

# 22. Failure-Safe Behaviour

Where practical, a single feature failure should not create an unsafe host condition.

Particular attention shall be given to:

- +5 V / GND shorts
- incorrect cable wiring
- stuck FIRE outputs
- autofire remaining asserted when disabled
- reversed or incorrect protection devices
- solder bridges

An assembled controller shall be electrically checked before connection to a valuable retro computer.

---

# 23. Rev 1.5 Intentional Limitations

Rev 1.5 intentionally does **not** provide:

- continuously adjustable autofire timing
- burst mode
- game profiles
- macros
- programmable debounce
- USB HID
- USB configuration
- firmware updates
- wireless operation
- programmable RGB effects
- persistent digital settings

These omissions are intentional architectural boundaries rather than missing Rev 1.5 functionality.

---

# 24. Future / Rev 2.0 Features

The following are potential future features and are **not Rev 1.5 requirements**:

| ID | Potential Feature | Rev 1.5 |
|---|---|---|
| FUT-001 | Firmware-controlled autofire | Not included |
| FUT-002 | Adjustable autofire rate | Not included |
| FUT-003 | Burst mode | Not included |
| FUT-004 | Configurable debounce | Not included |
| FUT-005 | Game profiles | Not included |
| FUT-006 | Persistent configuration | Not included |
| FUT-007 | USB firmware update | Not included |
| FUT-008 | Optional USB HID | Not included |
| FUT-009 | Programmable LED behaviour | Not included |
| FUT-010 | Macro functionality | Not included |

These features belong to a potential programmable **Rev 2.0** architecture.

---

# 25. Rev 1.5 Feature Validation Matrix

| Feature | Design Defined | Existing Physical Validation | Final Rev 1.5 Prototype |
|---|:---:|:---:|:---:|
| UP/DOWN/LEFT/RIGHT | ✓ | — | Pending |
| FIRE1 | ✓ | — | Pending |
| FIRE2 | ✓ | — | Pending |
| Autofire OFF | ✓ | — | Pending |
| Autofire ON | ✓ | — | Pending |
| SLOW timing | ✓ | ✓ | Pending |
| FAST timing | ✓ | ✓ | Pending |
| LEFT = SLOW | ✓ | ✓ | Pending |
| RIGHT = FAST | ✓ | ✓ | Pending |
| Power LED | ✓ | — | Pending |
| Dual-colour LED | ✓ | Pinout validated | Pending |
| MX hot-swap | ✓ | — | Pending |
| PTC protection | ✓ | Component selected | Pending |
| Signal ESD | ✓ | Component selected | Pending |
| +5 V ESD | ✓ | Pinout validated | Pending |
| DB9 cable mapping | ✓ | ✓ | Pending |
| Cable batch procedure | ✓ | ✓ | Production use pending |

A feature shall not be marked **Production Validated** until tested on production-representative Rev 1.5 hardware.

---

# 26. Production Test Traceability

The future production test procedure should reference the Feature IDs defined in this document.

Planned document:

```text
docs/testing/PRODUCTION_TEST.md
```

Example:

```text
T-DIR-01  -> F-001 Directional Control
T-FIRE-01 -> F-002 FIRE1
T-FIRE-02 -> F-003 FIRE2
T-AF-01   -> F-004 Hardware Autofire
T-AF-02   -> F-005 Autofire OFF / ON
T-AF-03   -> F-006 SLOW / FAST
T-LED-01  -> F-007 Power Indication
T-LED-02  -> F-008 Autofire Indication
```

This allows production validation to remain traceable to the feature specification.

---

# 27. Feature Philosophy

Rev 1.5 intentionally prioritizes:

- predictable operation
- low latency
- hardware simplicity
- serviceability
- host protection
- clear user feedback
- minimal configuration

Features shall not be added to Rev 1.5 merely because they could technically be implemented.

Functionality requiring a programmable controller belongs to a future architecture unless a formal hardware revision decision is made.

---

# 28. Related Documentation

```text
README.md

docs/
├── README.md
├── architecture/
│   └── System_architecture.md
├── specification/
│   ├── PROJECT_SPECIFICATION.md
│   └── FEATURE_SPECIFICATION.md
└── assembly/
    └── CABLE_ASSEMBLY.md

hardware/rev1.5/
├── README.md
└── bom/
    ├── README.md
    ├── wasdpad+v1.5.csv
    ├── ALTERNATE_PARTS.md
    └── PROCUREMENT_NOTES.md
```

---

# 29. Document Versioning

Feature-specification versions are independent from PCB hardware revisions.

Current state:

```text
Hardware Revision:       Rev 1.5
Feature Specification:   v1.1
```

A documentation clarification does not require a hardware revision.

A change to defined Rev 1.5 behaviour may require engineering review and potentially a new hardware revision.

---

# 30. Version History

| Version | Date | Status | Changes |
|---|---|---|---|
| 1.0 | Not recorded | Draft | Initial Rev 1.5 feature specification covering digital controls, FIRE buttons, autofire, status indication, hot-swap switches, protection and compatibility |
| **1.1** | **2026-08-18** | **Engineering Specification** | Corrected autofire control model to separate OFF/ON and SLOW/FAST switches; added final 330 kΩ / 680 kΩ timing values and physical selector orientation; defined FIRE1/FIRE2 behaviour; updated Kailh/Gateron hot-swap system; separated power and autofire LEDs; added protection, DB9 and serviceability requirements; restricted compatibility claims; added feature IDs, acceptance criteria, validation matrix and Rev 2.0 feature separation |

---

# 31. Next Version

The next feature-specification revision should be created when:

- Rev 1.5 prototype validation changes a feature requirement,
- a user-visible Rev 1.5 behaviour is modified, or
- additional acceptance criteria are formally defined.

Successful Rev 1.5 prototype validation may result in a minor revision updating validation status without changing the feature definitions.

A major version increment should be reserved for substantial feature-set changes.

---

**WASDPad+ Rev 1.5 — Feature Specification**
