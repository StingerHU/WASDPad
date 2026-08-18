# WASDPad+ Firmware

**Document Version:** 0.9  
**Current Hardware Revision:** Rev 1.5  
**Status:** Reserved for Future Development  
**Last Updated:** 2026-08-18

---

# 1. Purpose

This directory is reserved for firmware associated with future programmable revisions of the **WASDPad+** controller.

The current hardware revision, **Rev 1.5**, does **not** use firmware.

---

# 2. Rev 1.5

WASDPad+ Rev 1.5 is a fully hardware-based controller.

Normal operation requires no:

- microcontroller
- firmware
- bootloader
- USB stack
- host driver
- configuration software
- programmable logic

Directional inputs, FIRE controls and autofire are implemented entirely in hardware.

The Rev 1.5 autofire system is based on:

- ICM7555 CMOS timer
- CD4066 CMOS switching
- discrete MOSFET/transistor circuitry
- passive timing components

Therefore:

```text
firmware/
```

being empty of firmware source code for Rev 1.5 is **intentional**.

---

# 3. Rev 1.5 Firmware Requirements

There are none.

Rev 1.5 shall remain operational without any programmable device or software component.

Firmware functionality shall not be introduced into Rev 1.5 without a formal hardware-revision decision.

---

# 4. Future Rev 2.0

Firmware development is planned for a future programmable hardware architecture, currently referred to as:

**WASDPad+ Rev 2.0**

Potential Rev 2.0 functionality may include:

- microcontroller-based control
- firmware-controlled autofire
- adjustable autofire rate
- burst mode
- configurable debounce
- game-specific profiles
- persistent configuration
- programmable status indication
- USB firmware update
- optional USB HID support

These are future concepts and are **not Rev 1.5 features**.

---

# 5. Planned Firmware Structure

When active Rev 2.0 firmware development begins, this directory may evolve into a structure similar to:

```text
firmware/
├── README.md
├── src/
├── include/
├── config/
├── tests/
└── tools/
```

The final structure shall be defined when the programmable hardware architecture is finalized.

---

# 6. Revision Separation

Firmware shall always identify the hardware revision it targets.

Firmware intended for a future programmable revision shall not be documented or distributed as compatible with Rev 1.5.

Conceptually:

```text
Rev 1.5
Hardware-only
No firmware

Rev 2.0
Programmable architecture
Firmware planned
```

This separation prevents future firmware documentation from creating ambiguity about Rev 1.5 requirements.

---

# 7. Related Documentation

Current Rev 1.5 documentation:

```text
README.md
docs/README.md
docs/architecture/System_architecture.md
docs/specification/PROJECT_SPECIFICATION.md
docs/specification/FEATURE_SPECIFICATION.md
docs/roadmap/ROADMAP.md
hardware/README.md
hardware/rev1.5/README.md
```

---

# 8. Version History

| Version | Date | Status | Changes |
|---|---|---|---|
| 0.1 | Not recorded | Placeholder | Initial firmware directory placeholder |
| **0.9** | **2026-08-18** | **Reserved** | Clarified that Rev 1.5 intentionally contains no firmware; reserved directory for future programmable revisions; documented Rev 1.5 / Rev 2.0 architectural separation |

---

# 9. Next Version

No firmware release is currently planned for Rev 1.5.

This document should be updated when active development of a programmable WASDPad+ hardware revision begins.

---

**Rev 1.5: Hardware Only — No Firmware Required**
