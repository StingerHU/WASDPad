# WASDPad+ Documentation

**Current hardware:** **Rev1.5.2**  
**Release:** **Final Production Release — manufactured board functionally validated**  
**Document version:** 2.0  
**Updated:** 2026-10-19

WASDPad+ Rev1.5.2 is the final discrete-hardware release. The project owner confirms that a **newly manufactured Rev1.5.2 PCB** has been received and **all controller functions operate correctly**, including the corrected FAST/SLOW autofire selector. The previous Rev1.5.1 defect was identified, reworked on an existing board and then fixed in the final Rev1.5.2 schematic, PCB and Gerber fabrication outputs.

Rev1.5.1 records remain available to document engineering history; they are **not** the current fabrication baseline. Start with the [project overview](../README.md).

## Read this first

| Subject | Document | Scope |
| --- | --- | --- |
| Current release and validation | [Rev1.5.2 manufacturing release record](../hardware/rev1.5/REV1.5.2_MANUFACTURING_RELEASE_NOTES.md) | Final PCB revision, tested manufactured unit and scope of evidence |
| Features | [Feature specification](specification/FEATURE_SPECIFICATION.md) | Current Rev1.5.2 operation and interfaces |
| Design | [System architecture](architecture/System_architecture.md) | Discrete-hardware functional blocks and correct SPEED pin mapping |
| Hardware | [Rev1.5 hardware overview](../hardware/rev1.5/README.md) | Rev1.5.2 release, design history and manufacturing references |
| Assembly and cable wiring | [Assembly procedure](assembly/ASSEMBLY.md) | Manufacturing, DE-9 cable assembly, inspection and functional checks |
| Next developments | [Roadmap](roadmap/ROADMAP.md) | Completed Rev1.5.2 milestone and future Rev2.0 |

## Rev1.5.1 fault analysis and repair history

The first Rev1.5.1 SPEED selector had the wrong schematic-to-footprint common-terminal mapping. It was measured and corrected on one physical Rev1.5.1 board with three copper cuts and three insulated jumpers. The repaired board passed Amiga 1200 gameplay testing. The fix was carried through to the Rev1.5.2 production schematic/PCB and validated again on newly manufactured Rev1.5.2 hardware.

- [Engineering erratum: Rev1.5.1 → Rev1.5.2](../hardware/rev1.5/REV1.5.1_TO_REV1.5.2_SPEED_SELECTOR_ERRATUM.md)
- [Legacy Rev1.5.1 rework guide and photographs](assembly/REV1.5.1_SPEED_SELECTOR_REWORK.md)
- [Historical Rev1.5.1 engineering and manufacturing review](../hardware/rev1.5/Rev1.5.1-Engineering-Manufacturing-Record.MD)

## Detailed historical engineering records (preserved, not current manufacturing instructions)

The original detailed Rev1.5.1 development records are preserved as **historical snapshots** instead of being discarded when the current Rev1.5.2 release pages were streamlined:

- [Full Rev1.5.1 documentation index and document authority/reading order](README_REV1.5.1_HISTORICAL.md)
- [Detailed Rev1.5.1 roadmap, engineering and validation checklist](roadmap/ROADMAP_REV1.5.1_HISTORICAL.md)
- [Original Rev1.5.1 feature specification and acceptance criteria](specification/FEATURE_SPECIFICATION_REV1.5.1_HISTORICAL.md)
- [Original Rev1.5.1 architecture and engineering history](architecture/System_architecture_REV1.5.1_HISTORICAL.md)
- [Original Rev1.5.1 hardware directory and revision-control policy](../hardware/README_REV1.5.1_HISTORICAL.md)

**Do not mistake historical “pending”, “candidate”, or pre-physical PASS entries for the current release.** Rev1.5.2 is the final, manufactured and functionally validated hardware release.

## Manufacturing data and release traceability

The owner confirms that Rev1.5.2 PCB artwork and Gerbers were updated, and a fabricated Rev1.5.2 sample passed full reported functionality. **This GitHub export does not include the matching Rev1.5.2 KiCad source, Gerber/drill set or Rev1.5.2-labelled BOM/CPL**; therefore the export cannot independently reproduce/verify the exact manufacturing dataset used for the tested sample.

The following currently present CSV/Markdown records are **historical Rev1.5.1 baselines**. Do not silently relabel them Rev1.5.2 or use them to fabricate a Rev1.5.2 batch without confirming revision equivalence against the actual production release:

- [Rev1.5.1 Master BOM](../hardware/rev1.5/bom/WASDPad_Rev1.5.1_FULL_MASTER_BOM.csv)
- [Rev1.5.1 Master CPL](../hardware/rev1.5/bom/WASDPad_Rev1.5.1_FULL_MASTER_CPL.csv)
- [Rev1.5.1 BOM documentation](../hardware/rev1.5/bom/README.md)
- [Rev1.5.1 datasheet index](../hardware/rev1.5/datasheets/WASDPad_Rev1.5.1_DATASHEET_INDEX.md)
- [Rev1.5.1 approved alternate parts](../hardware/rev1.5/bom/ALTERNATE_PARTS.md)
- [Rev1.5.1 procurement notes](../hardware/rev1.5/bom/PROCUREMENT_NOTES.md)

**Current release authority:** [Rev1.5.2 manufacturing notes](../hardware/rev1.5/REV1.5.2_MANUFACTURING_RELEASE_NOTES.md), the actual matching Rev1.5.2 fabrication data held by the project owner, and the recorded first-article functional result. Every future manufacturing lot requires normal revision control and per-unit/batch quality checks.

## Additional project documentation

- [Mechanical enclosure overview](../enclosure/README.md)
- [Licensing and intended usage](legal/LICENSES.md)
- [Branding and trademarks](legal/TRADEMARKS.md)
- [Hardware landing page](../hardware/README.md)

## Revision and document history

| Date | Hardware | Documentation milestone |
| --- | --- | --- |
| 2026-08-29 | Rev1.5.1 | Original engineering review and Production Release Candidate records completed; subsequently identified SPEED mapping error |
| 2026-10-16 | Rev1.5.1 → Rev1.5.2 | Physical fault measured; legacy board repaired and tested; production schematic/PCB and Gerbers corrected |
| 2026-10-19 | **Rev1.5.2** | Owner confirms **manufactured Rev1.5.2 sample PASSED full functional validation**; project documentation updated to **Final Production Release** |

**Scope of PASS:** The project-owner-reported complete controller functionality of the manufactured Rev1.5.2 example. This does not establish independent regulatory approval, an external laboratory test report or automatic acceptance of untested future units.
