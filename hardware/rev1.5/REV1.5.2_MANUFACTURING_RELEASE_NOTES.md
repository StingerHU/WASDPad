# WASDPad+ Rev1.5.2 — Final Production Release and Validation Record

**Hardware revision:** **Rev1.5.2** (`wasdpad+v1.5.2-fixed` design baseline)  
**Document revision:** 2.0  
**Release documentation updated:** 2026-10-19  
**Release classification:** **FINAL PRODUCTION RELEASE**  
**Manufactured Rev1.5.2 functional acceptance:** **PASS — project-owner confirmation, October 2026**

## 1. Production release outcome

**WASDPad+ Rev1.5.2 is the final, functionally validated discrete-hardware production revision.** The owner reports receiving a newly manufactured Rev1.5.2 PCB in October 2026 and completing a **successful full-function controller test**. In particular, the FAST/SLOW SPEED-selector mapping corrected after the Rev1.5.1 investigation operates as designed. This is **a real manufactured Rev1.5.2 sample**, not solely a patched earlier board or an untested Gerber export.

The owner also confirms that the corrected final PCB design and its matching Gerber fabrication outputs were updated and used for the manufactured revision. The release completes the known Rev1.5.1 fault corrective action.

**Validation attribution:** These physical-first-article results are reported by the project owner. This repository export contains neither the final physical test log, the release Gerber archive nor a Rev1.5.2-labelled BOM/CPL. This document records the reported result; it does not claim independent inspection of unavailable artifacts or certify every untested subsequent unit.

## 2. Root cause and final production correction

The original Rev1.5.1 board used an incorrect common-contact assignment for the physical SPEED toggle. The installed three-terminal switch has **physical pad 2 as common**, while the old `Switch:SW_SP3T` symbol used pin 3 as the schematic common. This resulted in a nonfunctional FAST mode on the unmodified Rev1.5.1 PCB.

The Rev1.5.2 design corrected the schematic to `Switch:SW_SPDT`, retained the custom physical three-pad footprint and fixed all connected PCB routing:

| Physical `SW_SPEED1` pad (front-side reference) | Rev1.5.2 net | Connection / observed contacts |
| --- | --- | --- |
| **1 — FAST throw** | `AF_FAST_SEL` | CD4066 U2 pin 5; FAST closes pads 1–2 |
| **2 — COMMON** | `AF_EN_P` | Autofire enable feed for selected mode |
| **3 — SLOW throw** | `AF_SLOW_SEL` | CD4066 U2 pin 13; SLOW closes pads 2–3 |

The separate AUTO OFF/ON control, mechanical gameplay inputs and FIRE1/FIRE2 architecture were not implicated in this common-pin error.

## 3. Validation and closure record

| Milestone | Actual result / provenance |
| --- | --- |
| Physical Rev1.5.1 fault diagnosis | **Complete:** switching contacts and PCB nets measured; incorrect common contact identified |
| Legacy Rev1.5.1 recovery | **PASS:** three trace cuts + three insulated rear-side jumpers on one assembled unit |
| Patched Rev1.5.1 functional test | **PASS:** continuity/shorts/current-limited 5 V bring-up; all reported functions validated during Amiga 1200 gameplay |
| Rev1.5.2 schematic | **Corrected:** `SW_SPDT` symbol, common pin 2; previously reported ERC 0 errors / 0 warnings |
| Rev1.5.2 PCB | **Corrected:** all three SPEED nets/routing; previously reported DRC 0 errors / 0 unconnected pads |
| Rev1.5.2 manufacturing Gerbers | **Updated and fabricated:** matching new design outputs, project-owner confirmation |
| **Manufactured Rev1.5.2 unit** | **RECEIVED and physically tested**, October 2026, project-owner confirmation |
| **Manufactured Rev1.5.2 controller full functionality** | **PASS** — user confirms the Rev1.5.2 design is fully functional, including the selector fix |
| **Current release** | **FINAL PRODUCTION RELEASE** |

The owner's report of *complete controller functionality* encompasses the design's intended control modes (directions, FIRE1/FIRE2, manual/autofire mode, FAST/SLOW selection, status indication and backlight functionality). It is a global outcome report: per-pin test logs, instrumented frequency and current readings, photographs of the new sample and details of the test host were not included with this repository ZIP and must not be inferred.

## 4. Engineering QA notes and revision control

- **Recorded ERC/DRC results:** The earlier corrected design review recorded ERC 0 errors/0 warnings and DRC 0 errors/0 unconnected pads, with **46 warnings concerning customized footprint/J1 mappings**. These warnings were not reported as remaining SPEED selector functional defects. The corresponding signed/written disposition record is not present in this repository ZIP.
- **Manufacturing source of truth:** The project owner confirms Rev1.5.2 Gerbers were regenerated from the corrected PCB. This archive **does not contain** the final Rev1.5.2 Gerber/drill package, KiCad source, or **Rev1.5.2-labelled** Master BOM/CPL; only older Rev1.5.1-labelled CSV files are present. Do not use the historical file names as proof of the current assembly record.
- **New build traceability:** Retain the exact Rev1.5.2 manufacturing Gerbers, drill files, PCB revision, BOM, CPL and supplier/lot information for future board orders. Reconcile legacy component lists if reusing any part of them.
- **Routine quality control:** A first manufactured sample passed functionality. Later fabricated units still require their own incoming/assembly/end-of-line acceptance checks. This does not mean the current design remains a production candidate.
- **Scope of the release declaration:** Final production hardware release and full reported functional validation; no independent environmental, EMC, safety or regulatory certification is asserted.

## 5. Historical Rev1.5.1 inventory and records

At the time of diagnosis, inventory comprised four assembled and six bare Rev1.5.1 boards. One reworked assembled Rev1.5.1 example is known to have passed an Amiga 1200 gameplay test. Do not assume the remaining legacy examples have been repaired or passed. All **new PCB fabrication must use the corrected Rev1.5.2 release outputs**, never the unmodified Rev1.5.1 Gerbers.

The original pre-production Rev1.5.1 PASS review remains archived as a dated review; it was superseded for SPEED selector mapping by the subsequent measured fault and corrected production release.

## 6. References

- [Rev1.5.1 → Rev1.5.2 measured engineering erratum](REV1.5.1_TO_REV1.5.2_SPEED_SELECTOR_ERRATUM.md)
- [Original Rev1.5.1 engineering and manufacturing review](Rev1.5.1-Engineering-Manufacturing-Record.MD)
- [Legacy Rev1.5.1 three-cut/three-jumper repair](../../docs/assembly/REV1.5.1_SPEED_SELECTOR_REWORK.md)
- [Rev1.5.2 assembly and routine production acceptance](../../docs/assembly/ASSEMBLY.md)
- [Rev1.5.2 final development milestone](../../docs/roadmap/ROADMAP.md)

**Release decision:** **WASDPad+ Rev1.5.2 — FINAL PRODUCTION RELEASE. Manufactured sample fully functionally validated; PASS (project-owner reported, October 2026).**
