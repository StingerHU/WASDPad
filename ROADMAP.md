# WASDPad Roadmap

This document describes the evolution and long-term development plan of the WASDPad project.

---

# Project Vision

WASDPad aims to become a premium open hardware joystick controller for Commodore 64, Amiga and other compatible retro computer systems.

The project combines modern engineering practices with the simplicity, reliability and responsiveness required by classic gaming hardware.

## Core Principles

- Excellent gaming experience
- High reliability
- Serviceability
- Long-term maintainability
- Open hardware philosophy
- Community-driven development

---

# Development Philosophy

WASDPad follows an evolutionary development model.

Every hardware revision must represent a complete, stable and manufacturable product. New features are introduced only after the previous revision has been fully validated.

This approach ensures that every released revision can be manufactured, assembled and used without depending on future development.

---

# Project History

## Prototype

The initial prototype validated the overall concept of a keyboard-style joystick controller.

Objectives:

- Validate the WASD layout
- Test Cherry MX switches
- Verify Commodore-compatible joystick signalling
- Evaluate ergonomics
- Test the autofire concept

**Status:** ✔ Completed

---

## Revision 1.0

First functional PCB.

Main achievements:

- Complete joystick interface
- Autofire implementation
- Dual FIRE buttons
- Initial PCB validation

**Status:** ✔ Completed

---

## Revision 1.1

Electrical refinement.

Main improvements:

- PCB corrections
- Routing optimisation
- Improved signal integrity
- Component placement optimisation

**Status:** ✔ Completed

---

## Revision 1.2

First production-ready hardware platform.

Revision 1.2 represents the first fully validated version of the WASDPad hardware.

It provides the complete intended functionality of the original design and serves as the baseline for all future development.

### Features

- Cherry MX mechanical switches
- Dual FIRE buttons
- ICM7555-based autofire
- OFF / SLOW / FAST autofire modes
- Status LEDs
- MOSFET output drivers
- Commodore / Amiga compatible DB9 interface
- Fully tested PCB
- Production-ready design

**Status:** ✔ Production Ready

---

# Revision 1.5

Enhanced hardware platform.

Revision 1.5 builds upon the proven Revision 1.2 hardware without changing its core architecture.

The objective is to improve reliability, serviceability and manufacturability while maintaining full compatibility.

## Hardware

- [ ] Cherry MX hot-swap sockets
- [ ] ESD protection
- [ ] Resettable PTC fuse
- [ ] RGB / bi-colour status LED
- [ ] PCB optimisation
- [ ] Silkscreen improvements

## Documentation

- [ ] Updated schematic
- [ ] Updated BOM
- [ ] Assembly guide
- [ ] Manufacturing notes
- [ ] Test procedure

**Status:** Planned

---

# Revision 2.0

Next-generation architecture.

Revision 2.0 is the first major redesign of the WASDPad platform.

The existing discrete logic will be replaced by an RP2040-Zero microcontroller while preserving compatibility with classic joystick interfaces.

## Hardware

- [ ] RP2040-Zero
- [ ] USB-C firmware updates
- [ ] RGB status LED
- [ ] Analog trimmer input
- [ ] Modular firmware architecture

## Firmware

- [ ] Adjustable autofire
- [ ] Burst mode
- [ ] Multiple game profiles
- [ ] Configurable debounce profiles
- [ ] Persistent settings stored in flash
- [ ] Startup profile selection
- [ ] Firmware update over USB

## Planned Game Profile Support

Examples include configurable profiles for games with different timing characteristics.

Examples:

- Wizard of Wor
- Summer Games
- Track & Field
- Decathlon
- Daley Thompson's Super-Test

Each profile may define:

- Autofire timing
- Pulse width
- Burst behaviour
- Debounce parameters
- LED indication

**Status:** Concept

---

# Future Development

Possible future extensions.

## Hardware

- [ ] OLED status display
- [ ] Expansion connector
- [ ] Additional configurable buttons

## Software

- [ ] PC configuration utility
- [ ] Profile editor
- [ ] Firmware updater
- [ ] Community profile library
- [ ] USB HID mode (optional)

---

# Current Project Status

| Hardware | Status |
|----------|--------|
| Prototype | Completed |
| Revision 1.0 | Completed |
| Revision 1.1 | Completed |
| Revision 1.2 | Production Ready |
| Revision 1.5 | Planned |
| Revision 2.0 | Concept |

Current development target:

**Revision 1.5**

Long-term development target:

**Revision 2.0**
