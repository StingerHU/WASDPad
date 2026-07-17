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

- Cherry MX compatible hot-swap sockets
- Resettable PTC protection
- ESD protection on external signal lines
- Improved status indication
- PCB routing improvements
- Improved serviceability
- Updated manufacturing documentation

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

Compatibility with additional digital joystick systems may be added in future revisions.

---

# Repository Structure

```text
WASDPad/
│
├── docs/
│   ├── architecture/
│   │   └── System_Architecture.md
│   │
│   ├── specification/
│   │   ├── Project_Specification.md
│   │   └── Feature_Specification.md
│   │
│   ├── roadmap/
│   │   └── ROADMAP.md
│   │
│   └── legal/
│       ├── LICENSES.md
│       └── TRADEMARKS.md
│
├── hardware/
│   └── rev1.5/
│       ├── README.md
│       └── bom/
│           ├── BOM.csv
│           ├── BOM.md
│           ├── ALTERNATE_PARTS.md
│           └── PROCUREMENT_NOTES.md
│
├── firmware/
├── enclosure/
├── images/
│
└── README.md
```

---

# Documentation

## Architecture

- `docs/architecture/System_Architecture.md`

Defines the functional architecture of the Revision 1.5 hardware platform.

---

## Specifications

- `docs/specification/Project_Specification.md`

Defines the long-term technical vision, engineering principles and design goals of the WASDPad project.

- `docs/specification/Feature_Specification.md`

Defines the user-visible behaviour and functionality of the Revision 1.5 hardware.

---

## Roadmap

- `docs/roadmap/ROADMAP.md`

Describes the project's development history, current milestone and future hardware revisions.

---

## Hardware

- `hardware/rev1.5/README.md`

Overview of the Revision 1.5 hardware platform.

- `hardware/rev1.5/bom/BOM.md`

Human-readable Bill of Materials.

- `hardware/rev1.5/bom/BOM.csv`

Machine-readable Bill of Materials.

- `hardware/rev1.5/bom/ALTERNATE_PARTS.md`

Approved and candidate replacement components.

- `hardware/rev1.5/bom/PROCUREMENT_NOTES.md`

Component sourcing, availability and lifecycle notes.

---

## Legal

- `docs/legal/LICENSES.md`

Planned licensing model for hardware, firmware, enclosure and documentation.

- `docs/legal/TRADEMARKS.md`

Trademark ownership and permitted trademark usage.

---

# Development Philosophy

The WASDPad project follows several core engineering principles:

- Reliability before complexity
- Compatibility before innovation
- Low latency by design
- Serviceable hardware
- Long-term maintainability
- Complete documentation
- Evolution through validated hardware revisions

Every released hardware revision shall represent a complete, stable and manufacturable product.

---

# Revision History

| Revision | Description | Status |
| :--- | :--- | :--- |
| Prototype | Initial proof of concept | ✔ Completed |
| Revision 1.0 | First functional PCB | ✔ Completed |
| Revision 1.1 | Electrical refinement | ✔ Completed |
| Revision 1.2 | Production-ready hardware platform | ✔ Released |
| Revision 1.5 | Enhanced hardware platform | 🚧 In Development |
| Revision 2.0 | RP2040 programmable platform | Planned |

---

# Current Development Focus

The current Revision 1.5 development cycle consists of:

1. Complete the Revision 1.5 Bill of Materials.
2. Select all new protection components.
3. Update the schematic.
4. Update the PCB layout.
5. Manufacture the first Revision 1.5 prototype.
6. Validate electrical, mechanical and functional performance.
7. Prepare manufacturing and assembly documentation.
8. Release Revision 1.5.

---

# Future Development

Revision 2.0 is planned as the first programmable WASDPad platform while maintaining compatibility with existing joystick interfaces.

Planned capabilities include:

- RP2040-based architecture
- Firmware-controlled autofire
- Adjustable timing
- Burst mode
- Game profiles
- Persistent configuration
- USB firmware updates
- Optional USB HID support

Development of Revision 2.0 will begin after Revision 1.5 has been completed and validated.

---

# Licensing

The project is currently under private development.

Hardware, firmware, enclosure and documentation may be released under different open-source licenses in future revisions.

See `docs/legal/LICENSES.md` for details.

---

# Trademark Notice

All product names and trademarks remain the property of their respective owners.

The Commodore **C=** logo is used only where explicit permission has been granted.

See `docs/legal/TRADEMARKS.md` for additional information.

---

# Current Milestone

**Revision 1.5 — Bill of Materials**
