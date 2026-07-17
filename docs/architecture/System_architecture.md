# WASDPad System Architecture
## Revision 1.5

Document Version: 1.0

Status: Draft

---

# Purpose

This document describes the functional architecture of the WASDPad Revision 1.5 hardware.

Revision 1.5 is based on the proven Revision 1.2 platform and introduces improvements in reliability, serviceability and manufacturability without changing the fundamental operating principles.

This document intentionally excludes the future RP2040-based architecture, which will be documented separately.

---

# System Overview

The WASDPad Rev1.5 consists of the following functional blocks:

- Power Input
- Power Protection
- User Inputs
- Autofire Logic
- Mode Selection
- Status Indicators
- Output Drivers
- DB9 Interface

```

---
# Functional Block Diagram

```text
                    DB9 Connector
                         │
          +5V            │           GND
           │             │            │
           └──────┬──────┘            │
                  │                   │
           PTC Protection             │
                  │                   │
           Power Distribution         │
                  │                   │
      ┌───────────┼───────────┐       │
      │           │           │       │
      ▼           ▼           ▼       │
Input Switches  Autofire   Status LEDs│
      │         Logic         │       │
      └───────────┬───────────┘       │
                  │                   │
                  ▼                   │
            Output Drivers            │
                  │                   │
                  ▼                   │
           DB9 Signal Lines───────────┘
```


# Functional Blocks

## 1. Power Input

Provides operating voltage from the host computer joystick port.

Responsibilities:

- Receive +5V
- Distribute power
- Maintain low current consumption

---

## 2. Power Protection

Protects the controller against accidental overcurrent.

Components

- Resettable PTC fuse

Future revisions may introduce additional protection if required.

---

## 3. User Inputs

Mechanical switches provide the joystick inputs.

Signals:

- UP
- DOWN
- LEFT
- RIGHT
- FIRE1
- FIRE2

Revision 1.5 introduces:

- Cherry MX hot-swap sockets

---

## 4. Autofire Logic

Hardware implementation based on the ICM7555 timer.

Responsibilities:

- Stable timing
- OFF / SLOW / FAST operation
- Independent from software

---

## 5. Mode Selection

The user selects the desired autofire operating mode.

Modes:

- OFF
- SLOW
- FAST

Mode selection remains purely hardware based.

---

## 6. Status Indicators

Visual feedback for operating mode.

Revision 1.5 introduces:

- RGB or bi-colour LED

Purpose:

- Power indication
- Autofire mode indication

---

## 7. Output Drivers

MOSFET output stages isolate the timing circuitry from the joystick interface.

Responsibilities:

- Signal switching
- Electrical robustness
- Reliable operation

---

## 8. ESD Protection

New in Revision 1.5.

Signal protection located close to the DB9 connector.

Protected lines:

- UP
- DOWN
- LEFT
- RIGHT
- FIRE1
- FIRE2

Purpose:

- Increase robustness
- Reduce risk of electrostatic damage

---

## 9. DB9 Interface

Standard digital joystick interface.

Compatible systems include:

- Commodore 64
- Commodore 128
- VIC-20
- Plus/4 (adapter)
- C16 (adapter)
- C116 (adapter)
- Commodore Amiga
- Atari ST
- TVC (adapter)

---

# Design Principles

Revision 1.5 intentionally preserves the successful hardware architecture introduced in Revision 1.2.

Only improvements that increase:

- reliability
- maintainability
- manufacturability
- serviceability

are introduced.

No user-visible behavioural changes are planned.

---

# Future Migration

Revision 1.5 serves as the reference platform for the future RP2040-based Revision 2.0.

The following functional blocks are expected to remain largely unchanged:

- Power Protection
- ESD Protection
- User Inputs
- Output Drivers
- DB9 Interface

The following blocks will be replaced:

- Autofire Logic
- Mode Selection
- Status Indicator Control

These functions will later be implemented in firmware.

---

# Current Status

Revision 1.5 Architecture

Status: In Design
