# WASDPad Revision 1.5
## Bill of Materials

Document Version: 0.1

Status: Draft

The authoritative component list is maintained in:

`BOM.csv`

This document provides a human-readable overview of the main component groups and their selection status.

---

# BOM Status Definitions

## Revision Status

| Status | Meaning |
|---|---|
| Existing | Inherited from Revision 1.2 without functional changes |
| Modified | Existing function with a changed component or implementation |
| New | Introduced in Revision 1.5 |

## Selection Status

| Status | Meaning |
|---|---|
| Approved | Component type and specification accepted |
| Evaluation | Candidate components are under evaluation |
| TBD | Selection has not started or insufficient information is available |

---

# Main Functional Groups

## 1. Autofire Circuit

The Revision 1.5 autofire circuit is inherited from Revision 1.2.

Main components:

- ICM7555 CMOS timer
- SLOW timing resistor: 150 kΩ
- FAST timing resistor: 68 kΩ
- FIRE1 timing capacitor: 220 nF
- FIRE1 gate resistor: 10 kΩ
- 1N4148 switching diode
- Associated MOSFET switching stages

The operating behaviour shall remain compatible with Revision 1.2.

---

## 2. Direction and FIRE Switches

Revision 1.5 supports:

- Four direction switches
- Two FIRE1 switches
- Two FIRE2 switches

All gameplay switches use Cherry MX compatible mechanical switches.

Revision 1.5 introduces hot-swap sockets so switches can be replaced without soldering.

Hot-swap socket selection status:

**Evaluation**

---

## 3. Output Drivers

Joystick signal switching uses N-channel MOSFET output stages.

Current baseline component:

- 2N7002
- SOT-23 package

The final quantity and reference designators shall be imported from the validated Revision 1.2 schematic.

---

## 4. Power Protection

Revision 1.5 introduces a resettable PTC fuse on the joystick-port supply input.

The final PTC shall be selected based on:

- Normal operating current
- Maximum startup current
- Hold current
- Trip current
- Voltage rating
- Cold resistance
- Package size
- Reset behaviour

Selection status:

**Evaluation**

---

## 5. ESD Protection

Revision 1.5 introduces ESD protection for externally accessible joystick signals.

Protected signals are expected to include:

- UP
- DOWN
- LEFT
- RIGHT
- FIRE1
- FIRE2
- Supply input where appropriate

The final implementation may use:

- Individual TVS diodes
- Multi-channel TVS arrays
- A combination of both

Selection status:

**Evaluation**

---

## 6. Status Indication

Revision 1.2 uses separate Power and Autofire indication.

Revision 1.5 may use:

- Two individual LEDs
- One bi-colour LED
- Another simple hardware-controlled indication solution

The indication system shall not require a microcontroller.

Selection status:

**Evaluation**

---

## 7. Connectors and Mechanical Parts

Mechanical components include:

- DB9 joystick connector
- Autofire mode switches
- MX-compatible switches
- Hot-swap sockets
- PCB
- Enclosure
- Fasteners
- Cable and strain relief, where applicable

Exact manufacturer and supplier part numbers shall be added after mechanical compatibility has been verified.

---

# Current BOM Priorities

Component selection shall proceed in the following order:

1. Hot-swap socket
2. Compatible MX switch footprint
3. PTC resettable fuse
4. ESD protection solution
5. Status LED solution
6. DB9 connector
7. Remaining passive component standardization
8. Mechanical hardware
