Document Version: 1.0
Last Updated: 2026-07-17
Status: Draft

# WASDPad Project Specification

This document defines the technical vision, engineering requirements and long-term direction of the WASDPad project.

All hardware, firmware and mechanical development shall follow the principles described in this specification.

---

# 1. Project Overview

WASDPad is an open hardware joystick controller designed for classic home computers and gaming systems using digital joystick interfaces.

The project combines the reliability and simplicity of classic hardware with modern engineering practices, providing a premium gaming experience while remaining faithful to the original platforms.

The WASDPad project is intended to be fully documented, maintainable and continuously developed through multiple hardware and firmware revisions.

---

# 2. Project Goals

The primary objectives of the project are:

- Provide an excellent gaming experience
- Minimize input latency
- Achieve high long-term reliability
- Ensure easy servicing and repair
- Support long product lifetime
- Maintain simple assembly and manufacturing
- Follow open hardware principles
- Produce comprehensive documentation
- Enable future expansion without breaking compatibility

---

# 3. Target Platforms

Primary supported systems:

- Commodore 64
- Commodore 128
- Commodore VIC-20
- Commodore Plus/4 (adapter)
- Commodore C16 (adapter)
- Commodore C116 (adapter)
- Commodore Amiga 500 / 600 / 1200
- Atari ST
- Videoton TVC (adapter)

Future compatibility may include additional systems using digital joystick interfaces.

---

# 4. Hardware Requirements

The hardware shall:

- Operate from a standard 5V joystick port
- Maintain compatibility with original joystick signalling
- Use high-quality mechanical switches
- Support switch replacement without soldering (Rev 1.5 and later)
- Provide ESD protection on signal lines
- Include resettable overcurrent protection
- Use MOSFET output drivers where appropriate
- Be easy to assemble and service
- Be suitable for small-scale manufacturing

---

# 5. Mechanical Requirements

The enclosure shall:

- Be fully 3D printable
- Require no glue during assembly
- Be assembled using screws
- Allow easy maintenance
- Support hot-swappable switches
- Provide ergonomic hand positioning
- Be robust enough for intensive gameplay

---

# 6. Firmware Requirements

Future firmware shall provide:

- Adjustable autofire
- Burst mode
- Multiple game profiles
- Configurable debounce parameters
- Persistent user settings
- Firmware updates via USB
- Modular software architecture
- Reliable operation
- Fast startup
- Minimal processing latency

---

# 7. Functional Requirements

## Direction Control

- Four independent digital directions
- Accurate and responsive operation
- No unintended simultaneous activation

## FIRE Buttons

- Dual FIRE buttons
- Identical electrical behaviour
- Low latency

## Autofire

The autofire system shall support:

- Adjustable timing
- Stable pulse generation
- Multiple operating modes

## Burst Mode

The burst system shall allow controlled shot sequences with configurable timing.

## Game Profiles

Game profiles shall allow different timing parameters to be stored for individual games.

Typical configurable parameters include:

- Autofire frequency
- Pulse width
- Burst timing
- Debounce timing
- LED indication

## User Feedback

Visual indication shall clearly display:

- Operating mode
- Active profile
- Error conditions
- Firmware status

---

# 8. Hardware Architecture

The hardware shall remain modular.

Major functional blocks include:

- Input subsystem
- Protection subsystem
- Processing subsystem
- Output subsystem
- User indication subsystem

Future revisions may replace discrete logic with programmable controllers while preserving external compatibility.

---

# 9. Software Architecture

Firmware should be divided into independent modules.

Typical modules include:

- Input Manager
- Debounce Engine
- Game Profile Manager
- Autofire Engine
- Burst Controller
- LED Manager
- Configuration Manager
- Output Driver

Each module should remain independent and maintainable.

---

# 10. User Experience

The user should experience:

- Instant operation
- Predictable behaviour
- Fast response
- Simple configuration
- Reliable gameplay

No configuration software should be required for normal operation.

---

# 11. Design Principles

The WASDPad project follows these engineering principles:

- Reliability before complexity
- Compatibility before innovation
- Every released revision must remain fully usable
- New functionality shall not reduce stability
- Hardware and firmware shall remain maintainable
- Good documentation is part of the product
- Design decisions should be technically justified

---

# 12. Future Expansion

Possible future developments include:

- RP2040-based architecture
- USB configuration utility
- Community game profile library
- Firmware profile editor
- Optional USB HID mode
- Expansion connector
- OLED status display

Future features shall remain consistent with the overall design philosophy.

---

# 13. Revision Strategy

The project follows an evolutionary development model.

Each revision shall represent a complete, stable and manufacturable product.

Current development roadmap:

- Prototype
- Revision 1.0
- Revision 1.1
- Revision 1.2 (Production Ready)
- Revision 1.5 (Enhanced Hardware)
- Revision 2.0 (RP2040 Platform)

---

# 14. Out of Scope

The following features are intentionally excluded unless future project goals change:

- Internal rechargeable battery
- Wireless operation
- Cloud connectivity
- Mobile applications
- Internet connectivity
- Decorative RGB lighting effects
- Features that compromise compatibility with classic hardware

---

# 15. Documentation Policy

All significant hardware, firmware and mechanical changes shall be documented.

Project documentation consists of:

- README
- Project Specification
- Roadmap
- Changelog
- Hardware documentation
- Firmware documentation
- Manufacturing documentation
- Assembly guide
- User manual

Documentation is considered an integral part of the WASDPad project and shall evolve together with the product.
