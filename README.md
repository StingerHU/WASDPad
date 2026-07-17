# WASDPad

An open hardware joystick controller for classic home computers.

WASDPad combines the reliability of classic digital joystick interfaces with modern engineering practices, high-quality mechanical switches and a serviceable hardware design.

The current development focuses on **Hardware Revision 1.5**, an enhanced version of the validated Revision 1.2 platform.

---

# Project Status

| Area | Status |
| :--- | :--- |
| Product Definition | ✔ Complete |
| Documentation | ✔ In Progress |
| Rev1.5 Architecture | ✔ Defined |
| Rev1.5 Feature Specification | ✔ Defined |
| Rev1.5 BOM | 🚧 In Progress |
| Rev1.5 Schematic | Planned |
| Rev1.5 PCB Layout | Planned |
| Rev1.5 Prototype | Planned |
| Rev2.0 Platform | Future |

---

# Current Features

Revision 1.5 is a fully hardware-based joystick controller featuring:

- Four digital direction inputs
- Dual FIRE1 buttons
- Dual FIRE2 buttons
- Hardware autofire
- OFF / SLOW / FAST autofire modes
- ICM7555-based timing circuit
- MOSFET output switching
- Cherry MX compatible switches
- Standard DB9 joystick interface

Planned improvements over Revision 1.2 include:

- Cherry MX hot-swap sockets
- Resettable PTC protection
- ESD protection
- Improved status indication
- PCB routing improvements
- Improved serviceability

---

# Supported Platforms

Native support:

- Commodore 64
- Commodore 128
- Commodore VIC-20
- Commodore Amiga
- Atari ST

Supported through adapters:

- Commodore Plus/4
- Commodore C16
- Commodore C116
- Videoton TVC

---

# Repository Structure

```text
WASDPad/
│
├── docs/
│   ├── architecture/
│   ├── specification/
│   ├── roadmap/
│   └── legal/
│
├── hardware/
│   └── rev1.5/
│       └── bom/
│
├── firmware/
├── enclosure/
├── images/
│
├── ROADMAP.md
├── LICENSES.md
├── TRADEMARKS.md
└── README.md
```

---

# Documentation

## Architecture

- `docs/architecture/System_Architecture.md`

Functional architecture of the Revision 1.5 hardware.

## Specifications

- `docs/specification/Project_Specification.md`

Project goals, engineering principles and long-term vision.

- `docs/specification/Feature_Specification.md`

Functional behaviour of Revision 1.5.

## Hardware

- `hardware/rev1.5/README.md`

Revision 1.5 hardware overview.

- `hardware/rev1.5/bom/BOM.md`

Human-readable Bill of Materials.

- `hardware/rev1.5/bom/BOM.csv`

Machine-readable BOM.

- `hardware/rev1.5/bom/ALTERNATE_PARTS.md`

Approved replacement parts.

- `hardware/rev1.5/bom/PROCUREMENT_NOTES.md`

Component sourcing and lifecycle notes.

## Legal

- `LICENSES.md`

Planned licensing model.

- `TRADEMARKS.md`

Trademark information.

---

# Development Philosophy

The WASDPad project follows several core engineering principles:

- Reliability before complexity
- Compatibility before innovation
- Low latency by design
- Serviceable hardware
- Complete documentation
- Evolution through validated hardware revisions

Every released revision shall represent a complete, stable and manufacturable product.

---

# Revision History

| Revision | Description | Status |
| :--- | :--- | :--- |
| Prototype | Initial proof of concept | ✔ Completed |
| Revision 1.0 | First functional PCB | ✔ Completed |
| Revision 1.1 | Electrical refinement | ✔ Completed |
| Revision 1.2 | Production-ready hardware | ✔ Released |
| Revision 1.5 | Enhanced hardware platform | 🚧 In Development |
| Revision 2.0 | RP2040-based platform | Planned |

---

# Current Development Focus

The current development cycle consists of:

1. Complete the Revision 1.5 Bill of Materials.
2. Select all new protection components.
3. Update the schematic.
4. Redesign the PCB.
5. Manufacture the first Revision 1.5 prototype.
6. Validate hardware and mechanics.
7. Prepare production documentation.

---

# Future Development

Revision 2.0 will introduce a programmable RP2040-based architecture while preserving compatibility with existing joystick interfaces.

Planned capabilities include:

- Firmware-controlled autofire
- Adjustable timing
- Burst mode
- Game profiles
- USB firmware updates
- Persistent configuration
- Optional USB HID support

---

# Licensing

The project is currently under private development.

Hardware, firmware, enclosure and documentation may be released under different open-source licenses in the future.

See `LICENSES.md` for details.

---

# Trademark Notice

All trademarks remain the property of their respective owners.

The Commodore **C=** logo is used only where explicit permission has been granted.

See `TRADEMARKS.md` for additional information.

---

# Current Milestone

**Revision 1.5 — Bill of Materials**
