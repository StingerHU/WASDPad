# WASDPad+ System Architecture

## Hardware Revision 1.5.2

**Document Version:** 3.0
**Hardware Revision:** Rev1.5.2
**Status:** Final Production Release — fabricated Rev1.5.2 functional PASS
**Last Updated:** 2026-10-19

---

# 1. Purpose

This document describes the functional and electrical architecture of **WASDPad+ Hardware Revision 1.5.2**.

Revision 1.5.2 is the final, physically validated hardware-only production release based on the Rev1.5.1 generation. A newly fabricated Rev1.5.2 board passed complete reported functionality in October 2026 (project-owner confirmation).

The design retains the fundamental principles of the earlier platform:

* direct digital joystick signalling
* hardware-only input processing
* no microcontroller
* no firmware
* no software dependency
* deterministic operation
* minimal input latency

The Rev1.5 hardware generation (introduced in Rev1.5.1, carried into Rev1.5.2) includes:

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

The Rev1.5.2 architecture is designed around the following priorities:

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

WASDPad+ Rev1.5.2 consists of the following principal functional blocks:

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

Rev1.5.2 uses MX-compatible mechanical switches for gameplay controls.

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

There is no FIRE2 autofire in Rev1.5.2.

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

Rev1.5.2 provides two fixed autofire rates.

The timing network uses:

```text
FAST = 330 kΩ
SLOW = 680 kΩ
```

These values form part of the validated Rev1.5.2 gameplay configuration.

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

**Rev1.5.2 SPEED selector physical pin assignment (final):** the actual three-terminal selector closes **pads 1–2 in FAST** and **pads 2–3 in SLOW**. The schematic now uses `Switch:SW_SPDT`, with **pin 2 as common**. The physical `SW_SPEED1` pads are routed as:

| Physical pad | Rev1.5.2 net | Hardware destination |
| --- | --- | --- |
| 1 | `AF_FAST_SEL` | CD4066 U2 pin 5 |
| 2 (common) | `AF_EN_P` | Selected FAST/SLOW feed |
| 3 | `AF_SLOW_SEL` | CD4066 U2 pin 13 |

This fixes the original Rev1.5.1 symbol/footprint mapping error. The Rev1.5.2 board has subsequently been manufactured and functionally validated. See the [design erratum](../../hardware/rev1.5/REV1.5.1_TO_REV1.5.2_SPEED_SELECTOR_ERRATUM.md).

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

The selected TVS topology and PCB connection were reviewed during Rev1.5.1 engineering and carried forward into the Rev1.5.2 design. The new Rev1.5.2 unit passed the project-owner-reported full functional test; this statement does not claim a separate new component-level TVS test log.

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

Additional stitching was introduced during Rev1.5.1 PCB engineering and carried forward into the Rev1.5.2 layout where applicable.

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

The Rev1.5 generation introduced independent key illumination.

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

One of the central Rev1.5.2 design principles is separation between functional subsystems.

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

Rev1.5.2 contains no digital processing pipeline between a manual switch and the corresponding host input.

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

Rev1.5.2 uses a two-layer PCB.

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

The Rev1.5.2 controller itself does not require firmware or protocol conversion for this purpose.

---

# 34. Design Boundaries

Rev1.5.2 intentionally does **not** implement:

* programmable profiles
* firmware configuration
* USB
* Bluetooth
* macros
* software-defined autofire
* programmable burst patterns
* per-game profiles
* MCU-based input processing

These functions are outside the architectural scope of the discrete Rev1.5.2 platform.

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

Rev1.5.2 improves serviceability through:

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

**Rev1.5.2 is the released and physically functionally validated hardware.** The owner has confirmed that the production schematic/PCB and Gerbers include the SPEED fix and were used to manufacture a working Rev1.5.2 board. The current repository snapshot does **not** include the matching complete Rev1.5.2 KiCad/Gerber/drill/BOM/CPL bundle; the following BOM and CPL records are historical Rev1.5.1 references only:

```text
hardware/rev1.5/
├── README.md
├── REV1.5.2_MANUFACTURING_RELEASE_NOTES.md
├── Rev1.5.1-Engineering-Manufacturing-Record.MD
├── datasheets/WASDPad_Rev1.5.1_DATASHEET_INDEX.md
└── bom/
    ├── README.md
    ├── WASDPad_Rev1.5.1_FULL_MASTER_BOM.csv
    ├── WASDPad_Rev1.5.1_FULL_MASTER_CPL.csv
    ├── ALTERNATE_PARTS.md
    └── PROCUREMENT_NOTES.md
```

For a new Rev1.5.2 production order, use the revision-matched actual release data, not unmodified historical Rev1.5.1 Gerbers or unverified Rev1.5.1 BOM/CPL exports.

---

# 38. Engineering Validation Status

The Rev1.5.1 engineering review initially recorded PASS before its physical SPEED-selector common-pin error was discovered. The failure was reproduced and electrically traced to the `SW_SP3T` symbol's pin-3 common not matching the physical switch's pin-2 common. A Rev1.5.1 example was reworked and passed Amiga 1200 gameplay. **The exact correction was implemented in Rev1.5.2, and a newly manufactured Rev1.5.2 controller has now passed complete reported functional testing (project-owner confirmation, October 2026).**

| Stage | Result |
| --- | --- |
| Original Rev1.5.1 pre-production review | Historical PASS; superseded for SPEED common-pad assignment |
| Rev1.5.1 electrical fault investigation | Confirmed pin 2 common, switch closure and incorrect nets |
| Physical Rev1.5.1 patch and Amiga 1200 test | PASS on one reworked unit |
| Rev1.5.2 schematic / PCB fix | Completed; correct `SW_SPDT` common pin 2 and PCB pad routing |
| Rev1.5.2 pre-fabrication ERC / DRC | Previously reported: ERC 0 errors/0 warnings; DRC 0 errors/0 unconnected, 46 custom/J1 warnings noted |
| Rev1.5.2 fabrication Gerbers | Regenerated and used for production (owner confirmed) |
| **Manufactured Rev1.5.2 board — all reported functions** | **PASS (owner confirmed, October 2026)** |
| **Current release** | **FINAL PRODUCTION RELEASE** |

This section records user-reported first-article functional acceptance, not independently supplied electrical logs, regulatory compliance or acceptance of future untested batches. [Manufacturing/validation detail](../../hardware/rev1.5/REV1.5.2_MANUFACTURING_RELEASE_NOTES.md).

---

# 39. Production Validation Boundary

**The Rev1.5.2 design-validation milestone is closed.** A physical Rev1.5.2 production PCB has already passed all reported controller functionality tests, confirming that the SPEED selector defect was fixed in manufactured hardware.

The repeatable acceptance checklist for later builds covers power checks, DB9 pinout, all directions, FIRE1/FIRE2, AUTO OFF/ON and SLOW/FAST operation, indicator LEDs, key backlight, hot-swap sockets, mechanical fit and representative host operation. This is normal lot/unit quality control, not unfinished product development.

The engineering chronology is preserved in the [Rev1.5.1 historical engineering record](../../hardware/rev1.5/Rev1.5.1-Engineering-Manufacturing-Record.MD) and [Rev1.5.2 release record](../../hardware/rev1.5/REV1.5.2_MANUFACTURING_RELEASE_NOTES.md).

---

# 40. Future Architecture

Rev1.5.2 completes the discrete-hardware production platform. A separate future Rev2.0 generation may explore programmable functions without altering the established release.

```text
Rev1.5.2 — FINAL PRODUCTION RELEASE
Hardware CMOS 555 / CD4066 autofire
Direct joystick signalling / no firmware
               │
               ▼
Future Rev2.0 (concept only)
MCU timing / configurable modes
Programmable indicators / game-specific profiles
```

The protection philosophy, hot-swap controls, low-latency signalling and serviceable hardware interface remain useful architectural principles for any future platform.

---

# 41. Architectural Summary

**WASDPad+ Rev1.5.2** is a functionally validated, production-released, hardware-only digital retro-computer controller with a protected host interface, replaceable MX-compatible switches, independent FIRE1/FIRE2 buttons, hardware FAST/SLOW autofire, power/status LEDs and optional independent key backlighting.

The physical SPEED selector has **pad 2 as common**; the final Rev1.5.2 schematic/PCB correctly implements the observed contact mapping. Full functionality of a newly manufactured Rev1.5.2 board was confirmed by the project owner in October 2026. There is no firmware or software layer between the player and the host interface.

---

# 42. Document Status

**Architecture:** Rev1.5.2 — final hardware-only platform  
**Final manufacturing design:** corrected schematic/PCB and updated Gerbers (owner confirmed)  
**Newly manufactured Rev1.5.2 hardware validation:** **PASS — full reported functionality**  
**Production release:** **FINAL PRODUCTION RELEASE**  
**Document version:** 3.0 (2026-10-19)

The Rev1.5.1 review record remains in the repository as a historical artifact, not as the present release status.

---

## Historical Rev1.5.1 architecture snapshot

The earlier complete Rev1.5.1 system architecture, including its original architecture diagrams and validation boundaries, is preserved as a [historical system architecture snapshot](System_architecture_REV1.5.1_HISTORICAL.md). Its date-specific “Production Release Candidate” and “Physical Validation: PENDING” statements are historical, not the final Rev1.5.2 status.

---

# 43. Revision History

| Document Version | Date | Hardware Revision | Status | Description |
| --- | --- | --- | --- | --- |
| 1.0 | Earlier | Rev1.5 | Draft | Initial protected discrete-controller architecture |
| 2.0 | 2026-08-29 | Rev1.5.1 | Historical Production Release Candidate | Production-oriented architecture, hot-swap, protection, key backlight, BOM/CPL, etc.; later SPEED mapping defect discovered on a physical board |
| **3.0** | **2026-10-19** | **Rev1.5.2** | **FINAL PRODUCTION RELEASE — manufactured functional PASS** | Corrected SPEED-switch common pin mapping and revised production artwork; new fabricated board fully function-tested, per project owner |
