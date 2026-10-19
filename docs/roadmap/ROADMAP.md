# WASDPad+ Development Roadmap

**Current hardware:** Rev1.5.2  
**Current release:** **Final Production Release — full functional validation PASS on a manufactured Rev1.5.2 unit**  
**Document version:** 3.0  
**Updated:** 2026-10-19

## Current milestone — Rev1.5.2 complete

WASDPad+ Rev1.5.2 is the **final production release of the hardware-only Rev1.5 platform**. The project owner reports that a newly manufactured Rev1.5.2 PCB arrived in October 2026 and passed the complete controller functional test, confirming that the corrected SPEED selector operates as designed.

| Milestone | Result |
| --- | --- |
| Discrete-hardware architecture, FIRE1/FIRE2, hot-swap, protection, backlight | Complete |
| Rev1.5.1 preliminary engineering review | Historical PASS; superseded for the discovered selector mapping fault |
| Diagnose defective Rev1.5.1 SPEED common-pad mapping | **Complete** — physical terminal and schematic pin numbering measured |
| Repair existing Rev1.5.1 prototype | **PASS** — three cuts, three insulated jumpers; Amiga 1200 gameplay |
| Correct Rev1.5.2 schematic / PCB | **Complete** — `Switch:SW_SPDT`, pin 2 common, corrected tracks |
| Generate corrected Rev1.5.2 manufacturing Gerbers | **Complete** — project-owner confirmed |
| Manufacture a new Rev1.5.2 PCB | **Complete** — actual produced board received |
| Validate manufactured Rev1.5.2 controller functionality | **PASS** — project-owner confirmation, October 2026 |
| Release Rev1.5.2 hardware | **FINAL PRODUCTION RELEASE** |

## Development history

```text
Rev1.2 — original validated discrete controller
   │
   ▼
Rev1.5 / Rev1.5.1 — protection, MX hot-swap, FIRE1/FIRE2,
       dual-colour autofire status, key backlighting and PCB production preparation
   │
   ├── Electrical fault isolation: wrong SPEED-switch common-pad mapping
   ├── Rev1.5.1 physical rework + actual Amiga 1200 test: PASS
   ▼
Rev1.5.2 — corrected pin mapping, corrected PCB routing,
       updated production Gerbers and manufactured PCB
   │
   ▼
First manufactured Rev1.5.2 full functional validation: PASS
   │
   ▼
FINAL PRODUCTION RELEASE → stable production and maintenance
   │
   ▼
Future Rev2.0 — programmable platform (separate development effort)
```

## Final Rev1.5.2 SPEED mapping

| `SW_SPEED1` pad | Net | CD4066 control |
| --- | --- | --- |
| 1 | `AF_FAST_SEL` | U2 pin 5 |
| 2 (common) | `AF_EN_P` | Enable feed to selected contact |
| 3 | `AF_SLOW_SEL` | U2 pin 13 |

FAST closes pads 1–2; SLOW closes 2–3. This mapping was confirmed during fault investigation and included in the final production design. The owner subsequently confirmed the actual Rev1.5.2 manufactured board works correctly.

## Stable production / maintenance

Rev1.5.2 development is closed for the current hardware architecture. Routine ongoing activities are **production operations**, not missing Rev1.5.2 feature-development milestones:

- Preserve the exact released Rev1.5.2 PCB, Gerber/drill, BOM and CPL set used for manufacturing.
- Independently review and record disposition of any inherited noncritical/custom-footprint DRC warnings, including J1 mapping, whenever fabrication data is reissued.
- Keep tested boards and future lots traceable to that revision-controlled package.
- Apply normal pre-power continuity, supply checks, all controls, FAST/SLOW autofire, both indicators, backlighting, cable and real-system checks on production samples.
- Rework individual **Rev1.5.1** legacy PCBs only according to the [documented procedure](../assembly/REV1.5.1_SPEED_SELECTOR_REWORK.md); do not mix old Gerbers into production.
- Publish Rev1.5.2-labelled CAD/Gerber/BOM/CPL files in the repository if the project owner elects to make the complete manufacturing release publicly reproducible. This ZIP currently contains Rev1.5.1-labelled BOM/CPL archives only.

These activities do **not** change the fact that a manufactured Rev1.5.2 sample has successfully passed full reported functional testing.

## Future Rev2.0 — separate platform

Future exploratory features could include MCU-controlled or user-adjustable autofire, burst modes, game-specific presets, firmware configuration, more advanced LED status effects and optional USB features. None of these is required for the completed Rev1.5.2 release. The proven low-latency, no-firmware Rev1.5.2 product remains a separate stable platform.

## Release and QA references

- [Current Rev1.5.2 manufacturing release and first-article status](../../hardware/rev1.5/REV1.5.2_MANUFACTURING_RELEASE_NOTES.md)
- [SPEED selector engineering erratum](../../hardware/rev1.5/REV1.5.1_TO_REV1.5.2_SPEED_SELECTOR_ERRATUM.md)
- [Historical Rev1.5.1 engineering review](../../hardware/rev1.5/Rev1.5.1-Engineering-Manufacturing-Record.MD)
- [Assembly and functional test procedure](../assembly/ASSEMBLY.md)

## Historical engineering milestones and complete Rev1.5.1 development plan

The original 700-line engineering roadmap, including feature validation checklists, component review, assembly, electrical bring-up, platform testing, enclosure work, release gates and the Rev2.0 concept, is preserved without losing those technical details: [Rev1.5.1 historical roadmap](ROADMAP_REV1.5.1_HISTORICAL.md).

Its *Production Release Candidate* and *validation pending* language describes the earlier Rev1.5.1 project state. The current Rev1.5.2 release has already passed functional validation on a newly manufactured unit.

## Roadmap revision history

| Version | Date | Notes |
| --- | --- | --- |
| 2.0 | 2026-08-29 | Historical Rev1.5.1 Production Release Candidate roadmap; subsequent physical validation identified selector defect |
| **3.0** | **2026-10-19** | **Rev1.5.2 Final Production Release; new manufactured PCB full-function PASS (owner confirmed)**; Rev2.0 separated as future development |
