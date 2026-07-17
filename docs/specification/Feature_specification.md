# WASDPad Feature Specification
## Revision 1.5

Document Version: 1.0

Status: Draft

---

# Purpose

This document defines the functional behaviour of the WASDPad Revision 1.5 controller.

It specifies how the controller behaves from the user's perspective, independently of the underlying hardware implementation.

---

# Feature Summary

Revision 1.5 provides the following user-visible features:

- Digital joystick control
- Dual FIRE buttons
- Hardware autofire
- OFF / SLOW / FAST operating modes
- Status LED indication
- Hot-swappable switches
- Standard DB9 compatibility

---

# 1. Digital Direction Control

## Description

The controller provides four independent digital directions.

Supported directions:

- UP
- DOWN
- LEFT
- RIGHT

## Behaviour

Each direction operates immediately when the corresponding switch is pressed.

No software configuration is required.

Direction inputs are always active.

---

# 2. FIRE Buttons

## Description

The controller provides two physical FIRE buttons.

FIRE1

Primary action button.

Supports:

- Direct operation
- Autofire

FIRE2

Secondary action button.

Supports:

- Direct operation only

Autofire is intentionally not applied to FIRE2.

---

# 3. Autofire

## Purpose

Autofire repeatedly generates FIRE1 pulses while the FIRE1 button remains pressed.

The feature is intended for games requiring rapid repeated button presses.

---

## Available Modes

OFF

Autofire disabled.

FIRE1 behaves as a normal push button.

---

SLOW

Lower pulse frequency intended for games requiring moderate firing speed.

---

FAST

Higher pulse frequency intended for action games.

---

## Behaviour

Autofire only operates while FIRE1 is physically held.

Releasing FIRE1 immediately stops pulse generation.

Changing the operating mode takes effect immediately.

---

# 4. Operating Mode Selection

The controller provides a dedicated hardware selector.

Available positions:

- OFF
- SLOW
- FAST

The selected mode remains active until changed by the user.

---

# 5. Status LED

## Purpose

Provide immediate visual feedback.

Revision 1.5 supports:

- Power indication
- Autofire mode indication

Future revisions may extend the available indications.

---

# 6. Hot-Swap Switches

Revision 1.5 introduces replaceable Cherry MX compatible switches.

Users may replace switches without soldering.

Compatible switch families include:

- Cherry MX
- Gateron
- Kailh
- TTC
- Outemu (MX compatible versions)

---

# 7. Mechanical Serviceability

The enclosure is designed to allow:

- Easy opening
- Switch replacement
- PCB replacement
- Cable replacement

No destructive disassembly is required.

---

# 8. Electrical Protection

The controller includes protection against common electrical hazards.

The user is not required to configure or maintain these protection features.

Protection includes:

- Resettable overcurrent protection
- Electrostatic discharge protection

---

# 9. Compatibility

Revision 1.5 is electrically compatible with standard digital joystick interfaces.

Supported systems include:

- Commodore 64
- Commodore 128
- VIC-20
- Plus/4 (adapter)
- C16 (adapter)
- C116 (adapter)
- Commodore Amiga
- Atari ST
- Videoton TVC (adapter)

---

# 10. Startup Behaviour

No startup procedure is required.

The controller becomes operational immediately after connection.

No calibration is necessary.

No initialization sequence is visible to the user.

---

# 11. User Configuration

Revision 1.5 intentionally minimizes user configuration.

The available configuration options are limited to:

- Autofire mode selection

No software tools are required.

No firmware updates are required.

No external configuration utility is required.

---

# 12. Reliability Requirements

The controller is intended for long-term operation.

Expected characteristics:

- Stable timing
- Reliable switch operation
- Consistent electrical behaviour
- Low maintenance requirements

---

# 13. Limitations

Revision 1.5 intentionally excludes:

- USB interface
- Firmware updates
- User profiles
- Adjustable timing
- Burst mode
- Macro functions
- Wireless operation
- RGB lighting effects

These features are reserved for future hardware revisions.

---

# Feature Philosophy

Revision 1.5 intentionally remains a hardware controller.

The design prioritizes:

- Simplicity
- Reliability
- Low latency
- Predictable behaviour
- Easy maintenance

Every feature included in Revision 1.5 has been selected to improve the gaming experience without increasing operational complexity.
