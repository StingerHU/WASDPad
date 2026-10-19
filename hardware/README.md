# WASDPad+ Hardware

**Current production release:** **Rev1.5.2 — Final Production Release**  
**Manufactured first article:** **FULL FUNCTIONAL PASS** (project-owner confirmation, October 2026)  
**Architecture:** Direct retro joystick interface; no MCU, firmware or OS driver.

Rev1.5.2 is the definitive hardware-only version of WASDPad+. It retains MX-compatible hot-swappable keys, dual FIRE1/FIRE2 controls, CMOS 555 autofire, SLOW/FAST selection, ESD and PPTC power protection, dual-colour status indication and independent warm-white backlighting.

## Released design and physical confirmation

The original Rev1.5.1 hardware had a SPEED selector mapping error: the physical common contact is pin/pad 2, not pin 3 as the previous schematic symbol implied. The engineering team measured the fault, reworked one legacy panel and passed an Amiga 1200 gameplay test. The Rev1.5.2 schematic and PCB were corrected; corresponding Gerber outputs were regenerated and used to manufacture new Rev1.5.2 hardware (project-owner report). The newly fabricated Rev1.5.2 unit subsequently **passed complete functional testing**.

[Final Rev1.5.2 manufacturing and validation record](rev1.5/REV1.5.2_MANUFACTURING_RELEASE_NOTES.md)

## Hardware repository index

| Document | Role |
| --- | --- |
| [Rev1.5.2 hardware overview](rev1.5/README.md) | Final hardware revision and functional baseline |
| [Rev1.5.2 manufacturing release notes](rev1.5/REV1.5.2_MANUFACTURING_RELEASE_NOTES.md) | Corrected design, manufactured-sample PASS and revision QA |
| [Rev1.5.1 → Rev1.5.2 erratum](rev1.5/REV1.5.1_TO_REV1.5.2_SPEED_SELECTOR_ERRATUM.md) | Physical measurements and root cause |
| [Rev1.5.1 engineering review](rev1.5/Rev1.5.1-Engineering-Manufacturing-Record.MD) | Historical pre-production assessment, superseded for SPEED |
| [Rev1.5.1 rework guide](../docs/assembly/REV1.5.1_SPEED_SELECTOR_REWORK.md) | Salvage of existing legacy boards |
| [Current assembly and acceptance procedure](../docs/assembly/ASSEMBLY.md) | Hardware assembly, DE-9 cable wiring and final test |

## Historical manufacturing reference files

The ZIP contains the following Rev1.5.1-named production planning files. They are preserved for traceability and **not represented as a new Rev1.5.2 manufacturing dataset**:

- [Rev1.5.1 BOM](rev1.5/bom/WASDPad_Rev1.5.1_FULL_MASTER_BOM.csv)
- [Rev1.5.1 CPL](rev1.5/bom/WASDPad_Rev1.5.1_FULL_MASTER_CPL.csv)
- [Rev1.5.1 BOM and sourcing notes](rev1.5/bom/README.md)
- [Rev1.5.1 datasheet references](rev1.5/datasheets/WASDPad_Rev1.5.1_DATASHEET_INDEX.md)

The matching **Rev1.5.2 KiCad source, fabrication Gerber/drill outputs and revision-specific BOM/CPL are not in this repository export**. Their absence here does not mean the physical board was not manufactured: the owner confirms it was produced and fully function-tested. The public repository is not itself a complete independently auditable Rev1.5.2 fabrication archive until those files are published.

## Revision control

- **Rev1.2:** validated initial discrete-hardware platform.
- **Rev1.5.1:** extended protection, hot-swap and backlight features; physical validation found a SPEED common-pin mapping error. Pre-correction fabrication files are obsolete.
- **Rev1.5.2:** corrected production board and Gerbers; a newly manufactured board passed functional validation. **Current final release.**
- **Future Rev2.0:** separate, potentially programmable platform. Not needed to complete Rev1.5.2.

Before manufacturing subsequent Rev1.5.2 lots, verify the complete revision-matched source, fabrication and assembly output bundle; perform normal lot and unit acceptance checks. Do not combine historic Rev1.5.1 Gerbers with later revision data.
