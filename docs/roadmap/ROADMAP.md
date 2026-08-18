# WASDPad+ Development Roadmap

**Document Version:** 1.0  
**Current Hardware Revision:** Rev 1.5  
**Status:** Pre-Production  
**Last Updated:** 2026-08-19

---

## 1. Current Status

**WASDPad+ Rev 1.5 is functionally complete and approaching production.**

The hardware architecture, component selection, BOM, protection system, hot-swap implementation, autofire design and controller cable strategy have been finalized.

Current focus:

```text
Rev 1.5
Final design review
        ↓
PCB manufacturing
        ↓
Assembly
        ↓
Functional validation
        ↓
Release
```

No additional Rev 1.5 feature development is currently planned.

---

## 2. Rev 1.5 — Completed

The following major development areas are complete:

- controller architecture
- UP / DOWN / LEFT / RIGHT controls
- FIRE1
- FIRE2
- hardware autofire
- autofire OFF / ON control
- SLOW / FAST selection
- final autofire timing values
- power indication
- dual-colour autofire indication
- MX-compatible hot-swap system
- gameplay switch selection
- +5 V overcurrent protection
- signal ESD protection
- +5 V ESD protection
- component selection
- BOM
- alternate-parts strategy
- procurement strategy
- controller cable mapping
- cable assembly documentation

Final autofire values:

```text
FAST -> R13 = 330 kΩ
SLOW -> R14 = 680 kΩ

LEFT  -> SLOW
RIGHT -> FAST
```

---

## 3. Rev 1.5 — Remaining

Only the final release steps remain.

### Final Design Review

- [ ] final schematic review
- [ ] final ERC
- [ ] final PCB review
- [ ] final DRC
- [ ] verify critical component pinouts
- [ ] inspect manufacturing outputs

Special attention remains required for the previously identified D6 and D7 pinout/footprint checks.

### Manufacturing

- [ ] order Rev 1.5 PCB
- [ ] procure remaining production components
- [ ] assemble first complete Rev 1.5 unit

### Validation

- [ ] verify all controller functions
- [ ] confirm SLOW / FAST autofire operation
- [ ] confirm FIRE1 / FIRE2 operation
- [ ] confirm status indication
- [ ] confirm hot-swap operation
- [ ] confirm cable assembly
- [ ] validate final enclosure fit
- [ ] perform real-system gameplay validation

Successful functional operation of the complete controller is the primary acceptance criterion.

---

## 4. Enclosure

The Rev 1.5 enclosure is developed separately by **Dester3D**.

Mechanical design files and enclosure-specific documentation are maintained under:

```text
enclosure/
```

Final enclosure validation will be performed against the production Rev 1.5 PCB and assembled controller.

---

## 5. Rev 1.5 Release

Rev 1.5 can move from **Pre-Production** to **Released** when:

1. the final PCB passes design review,
2. the PCB is successfully manufactured and assembled,
3. the complete controller operates correctly,
4. the enclosure fits and functions correctly,
5. real-system gameplay validation succeeds.

After this milestone, Rev 1.5 should enter maintenance rather than continued feature development.

---

## 6. Future Rev 2.0

Rev 2.0 is a separate future programmable platform.

Potential features currently considered include:

- adjustable FAST autofire
- burst mode
- firmware-controlled behaviour
- configurable debounce
- game profiles
- persistent configuration
- programmable multi-colour status indication
- USB configuration / firmware update
- optional USB HID

These concepts are **not part of Rev 1.5**.

Rev 2.0 development should begin only as a separate hardware and firmware branch after Rev 1.5 has reached a stable release state.

---

## 7. Project Direction

The immediate project priority is:

> **Do not add new Rev 1.5 features. Manufacture and validate the existing design.**

The development sequence is therefore:

```text
NOW
 │
 ├─ Final Rev 1.5 schematic / PCB review
 │
 ├─ PCB manufacturing
 │
 ├─ Assembly
 │
 ├─ Functional + gameplay validation
 │
 └─ Rev 1.5 release
        │
        ▼
     Maintenance
        │
        ▼
Future Rev 2.0 development
```

---

## 8. Version History

| Version | Date | Changes |
|---|---|---|
| 0.x | Not recorded | Initial development roadmap and Rev 1.5 planning |
| **1.0** | **2026-08-19** | Simplified roadmap for Rev 1.5 pre-production state; removed detailed test scenarios and duplicated technical information; marked major Rev 1.5 development areas complete and reduced remaining work to final design review, manufacturing, functional validation and release |

---

**Current milestone: WASDPad+ Rev 1.5 — Ready for Final Review and Manufacturing**
