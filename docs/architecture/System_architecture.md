# WASDPad+ System Architecture

## Hardware Revision 1.5.1

**Document Version:** 2.0
**Hardware Revision:** Rev1.5.1
**Status:** Production Release Candidate
**Last Updated:** 2026-08-29

---

# 1. Purpose

This document describes the functional and electrical architecture of **WASDPad+ Hardware Revision 1.5.1**.

Revision 1.5.1 is the production-oriented evolution of the proven discrete-hardware WASDPad architecture.

The design retains the fundamental principles of the earlier platform:

* direct digital joystick signalling
* hardware-only input processing
* no microcontroller
* no firmware
* no software dependency
* deterministic operation
* minimal input latency

Revision 1.5.1 extends the architecture primarily in the areas of:

* electrical protection
* serviceability
* mechanical switch replacement
* status indication
* key illumination
* PCB robustness
* manufacturability

Future programmable WASDPad hardware generations are outside the scope of this document.

---

# 2. Architectural Goals

The Rev1.5.1 architecture is designed around the following priorities:

1. **Low latency**
   User inputs should reach the host through direct hardware paths without software scanning or protocol conversion.

2. **Deterministic behaviour**
   Controller behaviour must not depend on firmware execution, polling intervals or operating-system timing.

3. **Retro-hardware compatibility**
   Electrical behaviour should remain appropriate for traditional digital joystick interfaces.

4. **Low host-port loading**
   The controller must operate within the practical limitations of vintage computer joystick-port power sources.

5. **Electrical robustness**
   External signal and supply connections require appropriate ESD and overcurrent protection.

6. **Serviceability**
   Gameplay switches should be replaceable without PCB soldering.

7. **Manufacturability**
   The architecture should support repeatable PCB production and mixed automated/manual assembly.

8. **Maintainability**
   Functional blocks should remain understandable and repairable using conventional electronic components.

---

# 3. System Overview

WASDPad+ Rev1.5.1 consists of the following principal functional blocks:

* Host / DB9 Interface
* +5 V Power Input
* Power Protection
* Power Distribution and Decoupling
* ESD Protection
* Mechanical User Inputs
* FIRE1 / FIRE2 Signal Logic
* Autofire Timing Generator
* Autofire Mode Selection
* Output Switching
* Autofire Status Indication
* Key Backlighting
* Backlight Control

The system is entirely hardware-driven.

---

# 4. High-Level Functional Architecture

```text
                         HOST COMPUTER
                     DIGITAL JOYSTICK PORT
                              │
          ┌───────────────────┴───────────────────┐
          │                                       │
         +5 V                                    GND
          │                                       │
          ▼                                       │
    ┌─────────────┐                               │
    │ PTC Current │                               │
    │ Protection  │                               │
    └──────┬──────┘                               │
           │                                      │
           ▼                                      │
    ┌─────────────┐                               │
    │ +5 V ESD /  │                               │
    │ TVS Protect │                               │
    └──────┬──────┘                               │
           │                                      │
           ▼                                      │
    ┌──────────────────┐                          │
    │ Power Distribution│                         │
    │   + Decoupling    │                         │
    └──────┬───────────┘                          │
           │                                      │
      ┌────┼───────────────┬──────────────┐       │
      │    │               │              │       │
      ▼    ▼               ▼              ▼       │
   Inputs Autofire      Status LED      Backlight │
          Logic          Drivers          System  │
      │    │               │              │       │
      └────┴───────┬───────┘              │       │
                   │                      │       │
                   ▼                      │       │
             Output Switching             │       │
                   │                      │       │
                   ▼                      │       │
             Protected Signal Lines       │       │
                   │                      │       │
                   └──────────┬───────────┘       │
                              ▼                   │
                         DB9 INTERFACE─────────────┘
```

---

# 5. Signal Architecture

The controller uses traditional digital joystick signal lines.

Primary logical signals are:

```text
UP
DOWN
LEFT
RIGHT
FIRE1
FIRE2
```

These signals are fundamentally independent.

No matrix scanning is used.

No multiplexed digital communication protocol is used.

No firmware polling is used.

This preserves the electrical behaviour expected from conventional retro-computer joystick hardware.

---

# 6. Direction Input Architecture

The four directional controls are:

```text
UP
DOWN
LEFT
RIGHT
```

Each direction uses an independent mechanical switch path.

The architecture does not implement software or hardware SOCD filtering.

Therefore electrically simultaneous combinations remain possible, including:

```text
UP + DOWN
LEFT + RIGHT
```

Whether such combinations have meaningful behaviour depends on the connected host hardware and software.

---

# 7. Mechanical Input System

Rev1.5.1 uses MX-compatible mechanical switches for gameplay controls.

The controller provides eight physical gameplay switch positions:

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

The duplicated FIRE1 and FIRE2 controls provide an ambidextrous button arrangement.

---

# 8. Hot-Swap Architecture

Mechanical switches are not permanently soldered to the PCB.

Each gameplay switch is installed through an MX-compatible hot-swap socket.

Production architecture:

```text
Mechanical MX Switch
        │
        ▼
Kailh Hot-Swap Socket
        │
        ▼
       PCB
        │
        ▼
Input / Fire Logic
```

This architecture separates the mechanical wear component from the PCB.

Advantages include:

* switch replacement without soldering
* switch-feel customization
* improved serviceability
* reduced PCB rework
* longer practical controller service life

The production socket is the Kailh/Kaihua `CPG151101S11`.

The production-fitted switch is the Gateron KS-8 Yellow.

Other mechanically compatible MX-family switches may be used subject to physical compatibility.

---

# 9. FIRE1 Architecture

FIRE1 is the primary action signal.

Two physical FIRE1 switches are connected into the same logical FIRE1 function:

```text
FIRE1 LEFT ──┐
             ├──► FIRE1 Manual Logic ──┐
FIRE1 RIGHT ─┘                          │
                                        ├──► FIRE1 Output
Autofire Generator ─► Mode Control ─────┘
```

The FIRE1 output can therefore originate from:

* manual button activation
* hardware-generated autofire pulses

Autofire affects FIRE1 only.

When autofire is disabled, FIRE1 operates as a conventional manual fire signal.

---

# 10. FIRE2 Architecture

FIRE2 is an independent secondary fire signal.

Two physical switches provide the FIRE2 input:

```text
FIRE2 LEFT ──┐
             ├──► FIRE2 Logic ──► FIRE2 Output
FIRE2 RIGHT ─┘
```

FIRE2 does not pass through the autofire timing system.

There is no FIRE2 autofire in Rev1.5.1.

Host-system and software support is required for meaningful use of the second fire signal.

---

# 11. Autofire Architecture

Autofire is implemented entirely in hardware.

The timing source is a CMOS 555 timer.

Production device:

**Texas Instruments TLC555CDR**

The functional architecture is:

```text
                Timing Network
                     │
                     ▼
              ┌─────────────┐
              │   TLC555    │
              │ Oscillator  │
              └──────┬──────┘
                     │
                     ▼
              Autofire Pulse
                     │
                     ▼
               Mode Switching
                     │
                     ▼
                FIRE1 Logic
                     │
                     ▼
                FIRE1 Output
```

No processor or firmware participates in pulse generation.

---

# 12. Autofire Timing

Rev1.5.1 provides two fixed autofire rates.

The timing network uses:

```text
FAST = 330 kΩ
SLOW = 680 kΩ
```

These values form part of the validated Rev1.5.1 gameplay configuration.

The architecture deliberately uses fixed hardware timing rather than continuously variable user adjustment.

This provides:

* predictable behaviour
* repeatability between units
* simplified operation
* reduced accidental misconfiguration

---

# 13. Autofire Mode Selection

Two physical controls manage the autofire system.

## Autofire Enable

Provides:

```text
OFF
ON
```

## Speed Selection

Provides:

```text
SLOW
FAST
```

Functional architecture:

```text
                 ┌──────────────┐
                 │ Autofire ON  │
                 │    / OFF     │
                 └──────┬───────┘
                        │
Timing Generator ───────┼──────► FIRE1 Logic
                        │
                 ┌──────┴───────┐
                 │ SLOW / FAST  │
                 │   Selection  │
                 └──────────────┘
```

All mode selection remains hardware-based.

---

# 14. Analog Switching

A CMOS bilateral-switch IC is used in the autofire control architecture.

Production device:

**Texas Instruments CD4066BM96**

The CD4066 provides controlled switching of the relevant autofire timing paths.

This avoids introducing programmable logic while allowing clean hardware mode selection.

---

# 15. Output Switching Architecture

The controller uses MOSFET switching stages where required by the FIRE/autofire logic.

Production device family:

**2N7002 N-channel MOSFET**

Functional purpose:

* logic switching
* signal control
* isolation between timing circuitry and host-facing fire signals
* predictable low-current operation

The MOSFET stages preserve the behaviour expected from conventional joystick switching rather than actively driving logic-high levels into the host.

---

# 16. Host Interface Philosophy

The controller is designed to behave as closely as practical to a conventional passive digital joystick from the perspective of the host.

The architecture therefore emphasizes **signal assertion by switching toward ground**, rather than actively sourcing logic levels onto host signal lines.

This is particularly important when interfacing modern controller electronics with vintage computer hardware.

---

# 17. Power Architecture

Operating power is obtained from the host joystick interface.

The +5 V path is divided into the following functional stages:

```text
Host +5 V
    │
    ▼
Resettable PTC
    │
    ▼
+5 V ESD / TVS Protection
    │
    ▼
Protected +5 V Rail
    │
    ├──► Logic
    ├──► Autofire
    ├──► Status Indicators
    └──► Backlight System
```

The design intentionally maintains low overall power consumption.

---

# 18. Overcurrent Protection

The +5 V input includes a resettable PTC.

Production device:

**Littelfuse 1206L005/30WR**

Purpose:

* limit fault current
* reduce risk from accidental short circuits
* protect the host joystick-port supply
* provide automatically resettable protection

The PTC is located upstream of the controller's powered circuitry.

---

# 19. +5 V ESD / TVS Protection

The protected +5 V rail includes dedicated transient protection.

Production device:

**TPE0562BC3**

Functional connection:

```text
Protected +5 V ─── TVS ─── GND
```

The selected device topology and PCB connection were explicitly validated for Rev1.5.1.

This protection supplements the PTC:

* the PTC addresses sustained overcurrent conditions
* the TVS addresses short-duration transient events

The two devices therefore perform different protective functions.

---

# 20. Signal-Line ESD Protection

Externally accessible digital signal lines are protected against electrostatic discharge.

Protection is implemented using multi-line ESD arrays positioned in the host-interface signal paths.

Production device family:

**PESD5V0S4UD**

Protected functional signals include:

```text
UP
DOWN
LEFT
RIGHT
FIRE1
FIRE2
```

The protection architecture is intended to reduce the risk of ESD damage during:

* controller connection
* disconnection
* handling
* normal user interaction

The ESD devices do not participate in normal joystick logic.

---

# 21. Power Distribution and Decoupling

The protected +5 V rail supplies the active circuitry.

Local decoupling is provided using ceramic capacitors.

The architecture includes:

* local IC decoupling
* VCC-to-GND high-frequency bypassing
* ground copper zones
* ground stitching vias

These measures reduce:

* supply noise
* local switching disturbances
* ground impedance

while maintaining a simple two-layer PCB architecture.

---

# 22. Ground Architecture

Ground is distributed using copper zones on both PCB layers.

```text
F.Cu GND Zone
      │
      │ Stitching Vias
      ▼
B.Cu GND Zone
```

Ground stitching vias provide low-impedance connections between the two planes.

Additional stitching was introduced during Rev1.5.1 PCB validation where required to improve ground continuity.

---

# 23. Autofire Status Architecture

Autofire status is indicated using a dual-colour LED.

Production architecture:

```text
Autofire State
      │
      ├──► SLOW Driver ──► LED Channel
      │
      └──► FAST Driver ──► LED Channel
```

The indicator uses:

* one red/green dual-colour LED
* common-cathode topology
* two transistor driver stages
* independent current-limiting resistors

Production LED:

**Bivar 3BC-3-F**

Driver devices:

**MMBT3904 NPN transistors**

This architecture isolates the indicator load from the autofire control logic.

---

# 24. Power Indication

A separate LED provides controller power indication.

This indicator is independent from the dual-colour autofire status system.

Functional separation:

```text
POWER LED
    │
    └──► Controller powered

AUTOFIRE LED
    │
    └──► Autofire operating state / speed
```

This prevents ambiguity between power status and gameplay mode indication.

---

# 25. Key Backlight Architecture

Rev1.5.1 introduces independent key illumination.

Eight warm-white SMD LEDs are positioned beneath the gameplay switches.

```text
Protected +5 V
      │
      ▼
Backlight Switch
      │
      ▼
BACKLIGHT_5V
      │
      ├──► R ─► LED 1
      ├──► R ─► LED 2
      ├──► R ─► LED 3
      ├──► R ─► LED 4
      ├──► R ─► LED 5
      ├──► R ─► LED 6
      ├──► R ─► LED 7
      └──► R ─► LED 8
```

Each LED has an independent current-limiting resistor.

Production LED family:

**XINGLIGHT XL-2012WWC**

The LEDs are intentionally operated at relatively low current.

The design goal is subtle illumination rather than high-brightness decorative lighting.

---

# 26. Backlight Control

Backlighting has a dedicated hardware ON/OFF control.

Production switch:

**C&K PCM12SMTR**

The switch is physically located on the bottom side of the PCB.

The backlight subsystem is independent from:

* direction inputs
* FIRE inputs
* autofire timing
* autofire status indication

Disabling the backlight therefore has no effect on gameplay functionality.

---

# 27. Functional Independence

One of the central Rev1.5.1 design principles is separation between functional subsystems.

```text
                    ┌──► Direction Inputs
                    │
Mechanical Inputs ──┼──► FIRE1
                    │
                    └──► FIRE2


Autofire System ─────────► FIRE1 only

Status System ───────────► Visual feedback only

Backlight System ────────► Illumination only

Protection System ───────► Electrical robustness
```

A failure or disablement of a non-essential visual subsystem should not intentionally disable the fundamental manual controller inputs.

---

# 28. Latency Architecture

Rev1.5.1 contains no digital processing pipeline between a manual switch and the corresponding host input.

There is no:

* USB polling
* Bluetooth transmission
* firmware debounce loop
* software input scanning
* operating-system processing
* protocol conversion

For manual direction and fire inputs, latency is therefore dominated by:

* mechanical switch behaviour
* transistor/MOSFET switching propagation where present
* host-system input detection

Electronic propagation delay within the controller is negligible relative to human input timescales and the host computer's frame timing.

---

# 29. PCB Architecture

Rev1.5.1 uses a two-layer PCB.

Primary characteristics include:

* F.Cu signal and component routing
* B.Cu routing
* GND zones on both layers
* GND stitching vias
* top-side SMD electronics
* selected bottom-side components
* THT user-interface components
* bottom-mounted hot-swap sockets
* direct cable solder pads

The architecture supports a mixed manufacturing process.

---

# 30. Assembly Architecture

The hardware is divided into assembly classes.

## Automated SMD Assembly

Primarily:

* ICs
* MOSFETs
* transistors
* protection devices
* resistors
* capacitors
* SMD backlight LEDs

## Bottom-Side / Manual Assembly

Primarily:

* MX hot-swap sockets
* backlight control switch

## Through-Hole Assembly

Includes:

* power/status LEDs where applicable
* small-signal diode
* autofire control switches

## Mechanical Assembly

Includes:

* MX mechanical switches
* enclosure components

## Cable Assembly

The DB9 cable is soldered directly to dedicated PCB pads.

---

# 31. DB9 Interface

The host connection uses the classic DB9 / DE-9 digital joystick interface architecture.

Primary functional connections are:

```text
UP
DOWN
LEFT
RIGHT
FIRE1
FIRE2
+5 V
GND
```

The exact availability and interpretation of FIRE2 varies between host platforms and software.

---

# 32. Platform Compatibility

The underlying architecture is intended for systems using compatible digital joystick signalling.

Relevant platform families include:

* Commodore 64
* Commodore 128
* VIC-20
* Commodore Amiga
* Atari-compatible digital joystick interfaces
* additional compatible systems through appropriate adapters

Adapters may be required where the physical connector or pinout differs.

Electrical compatibility must be verified separately for each officially supported platform.

A mechanically compatible connector alone does not establish electrical compatibility.

---

# 33. Plus/4 Family

Commodore Plus/4-family systems use a different physical joystick connector.

Compatibility therefore requires an adapter.

The adapter maps the WASDPad digital joystick signals to the appropriate Plus/4-family connector.

The Rev1.5.1 controller itself does not require firmware or protocol conversion for this purpose.

---

# 34. Design Boundaries

Rev1.5.1 intentionally does **not** implement:

* programmable profiles
* firmware configuration
* USB
* Bluetooth
* macros
* software-defined autofire
* programmable burst patterns
* per-game profiles
* MCU-based input processing

These functions are outside the architectural scope of the discrete Rev1.5.1 platform.

---

# 35. Failure-Mode Philosophy

The architecture is designed so that optional visual features remain separated from core gameplay functions.

Examples:

* backlight failure should not intentionally disable gameplay inputs
* power-indicator failure should not disable controller operation
* autofire status-indicator failure should not disable manual FIRE1
* autofire can be disabled while retaining manual FIRE1 operation

Protection-device failure modes remain dependent on the nature of the electrical event and are not assumed to be fail-safe.

---

# 36. Serviceability

Rev1.5.1 improves serviceability through:

* hot-swappable gameplay switches
* conventional discrete components
* identifiable component MPNs
* documented footprints
* documented datasheets
* replaceable mechanical controls
* no firmware dependency
* no programmed device required for basic operation

The architecture can therefore be diagnosed using conventional electronic test equipment.

---

# 37. Manufacturing Traceability

The system architecture is supported by a controlled manufacturing dataset.

Authoritative records include:

```text
hardware/rev1.5/
├── README.md
├── Review_Record.MD
└── bom/
    ├── README.md
    ├── WASDPad_Rev1.5.1_FULL_MASTER_BOM.csv
    ├── WASDPad_Rev1.5.1_FULL_MASTER_CPL.csv
    ├── DATASHEET_INDEX.md
    ├── ALTERNATE_PARTS.md
    └── PROCUREMENT_NOTES.md
```

The Master BOM defines production component identity.

The Master CPL defines component placement.

---

# 38. Engineering Validation Status

The Rev1.5.1 architecture has completed its pre-production engineering review.

| Area                            | Status  |
| ------------------------------- | ------- |
| Functional architecture         | PASS    |
| Schematic                       | PASS    |
| ERC                             | PASS    |
| PCB layout                      | PASS    |
| DRC                             | PASS    |
| Protection topology             | PASS    |
| Critical component pinouts      | PASS    |
| PCB assembly orientation review | PASS    |
| Gerber generation               | PASS    |
| Master BOM                      | PASS    |
| Master CPL                      | PASS    |
| Manufacturing documentation     | PASS    |
| Physical Rev1.5.1 validation    | PENDING |

The hardware is therefore classified as:

**Production Release Candidate**

---

# 39. Production Validation Boundary

The architecture and manufacturing dataset are considered complete for production-candidate manufacture.

Final Production Approved status requires validation of the manufactured Rev1.5.1 hardware.

Physical validation includes:

* power integrity
* current consumption
* all direction inputs
* FIRE1
* FIRE2
* autofire OFF
* autofire SLOW
* autofire FAST
* status indication
* key backlighting
* backlight switching
* hot-swap socket operation
* DB9 cable mapping
* representative host-system operation
* extended gameplay testing

The detailed validation gate is maintained in:

`hardware/rev1.5/Review_Record.MD`

---

# 40. Future Architecture

Rev1.5.1 represents the mature discrete-hardware architecture of WASDPad+.

A future programmable generation may replace selected hardware blocks with MCU-controlled functions.

A conceptual future architecture may replace:

```text
Current Rev1.5.1
----------------
CMOS Autofire Timer
Hardware Mode Selection
Discrete Status Control

            │
            ▼

Future Programmable Generation
------------------------------
MCU Timing
Programmable Modes
Firmware-Controlled Indicators
Game-Specific Behaviour
```

However, the following concepts are expected to remain valuable:

* protected host interface
* ESD protection
* replaceable mechanical switches
* hot-swap sockets
* low-latency input architecture
* serviceability
* robust power distribution

The future programmable architecture shall be documented separately and shall not redefine the Rev1.5.1 hardware specification.

---

# 41. Architectural Summary

WASDPad+ Rev1.5.1 is a:

**hardware-only, low-latency, serviceable digital retro-computer controller architecture with protected host interfaces, replaceable MX-style gameplay switches, hardware autofire, independent visual indication and optional key backlighting.**

Its principal signal philosophy is:

```text
PLAYER
   │
   ▼
MECHANICAL SWITCH
   │
   ▼
DISCRETE HARDWARE
   │
   ▼
PROTECTED HOST SIGNAL
   │
   ▼
RETRO COMPUTER
```

There is no firmware or software layer between the player and the host interface.

---

# 42. Document Status

**Architecture:** Frozen for Rev1.5.1 Production Release Candidate
**Engineering Review:** PASS
**Physical Hardware Validation:** PENDING
**Production Approval:** PENDING

Architecture changes after this point require controlled engineering review and corresponding documentation updates.

---

# 43. Revision History

| Document Version | Date                       | Hardware Revision | Status                           | Description                                                                                                                                                                                                                                                                                            |
| ---------------- | -------------------------- | ----------------- | -------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 1.0              | Earlier Rev1.5 development | Rev1.5            | Draft                            | Initial functional architecture; early PTC, hot-swap, ICM7555 and ESD concepts                                                                                                                                                                                                                         |
| **2.0**          | **2026-08-29**             | **Rev1.5.1**      | **Production Release Candidate** | Architecture finalized against production hardware; added complete protection architecture, TLC555 autofire, FIRE1/FIRE2 separation, hot-swap system, dual-colour status architecture, key backlighting, ground architecture, assembly model, validation boundary and manufacturing-document hierarchy |
