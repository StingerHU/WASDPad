# WASDPad+ Rev1.5.2 — Corrected Series-Production Design Release Notes

**Document revision:** 1.0  
**Date:** 2026-10-16  
**Design baseline:** `wasdpad+v1.5.2-fixed`  
**Intended manufacturing baseline:** corrected Rev1.5.2 PCB layout **and its updated Gerber fabrication outputs**  
**Release statement:** Project owner confirms the final PCB model and corresponding Gerber files were updated for the series-production build. This documentation package did not receive the Gerber archive for independent inspection.  
**First-article status:** A newly fabricated Rev1.5.2 PCB has not yet been reported as physically tested; the first patched Rev1.5.1 board has passed Amiga 1200 functional/gameplay testing.

## 1. Why the production artwork was revised

The original Rev1.5.1 manufacturing PCB incorrectly mapped the SPEED switch's common contact. Measured physical switch behavior established **pad 2** as the actual common, but the previous schematic symbol `Switch:SW_SP3T` used schematic common **pin 3**. The FAST actuator position therefore failed to energize either relevant CD4066 channel. The issue was confirmed by bench measurements and corrected in the Rev1.5.2 schematic and layout.

The rework of an already assembled Rev1.5.1 board was independently checked by continuity/isolation tests, a current-limited 5 V bench test and **successful Amiga 1200 gameplay exercising all reported controller functions**. This provides direct functional evidence that the corrected control mapping works.

## 2. Exact fix incorporated into the production design

| Physical `SW_SPEED1` pad (front/component view) | Corrected net | Destination / logic |
| --- | --- | --- |
| **1 — left** | `AF_FAST_SEL` | CD4066 U2 pin 5; FAST selected via contacts 1–2 |
| **2 — center, COMMON** | `AF_EN_P` | Autofire enable; distributes to selected throw |
| **3 — right** | `AF_SLOW_SEL` | CD4066 U2 pin 13; SLOW selected via contacts 2–3 |

- Schematic symbol changed to **`Switch:SW_SPDT`**, whose common is pin 2.
- Verified custom three-pad footprint and mechanical location retained.
- PCB pad nets and routed F.Cu/B.Cu tracks corrected to match the physical switch.
- **Final Rev1.5.2 Gerber fabrication outputs updated/regenerated from the corrected PCB for series production** (project-owner confirmed).
- Unmodified Rev1.5.1 Gerbers **must not** be used for this production release.

## 3. Completed validation versus first-article acceptance

| Stage | Result / evidence |
| --- | --- |
| Fault diagnosis | **Completed:** physical contact pairs, voltage levels and oscilloscope-independent continuity measurements identified the common-pin discrepancy. |
| Rev1.5.1 physical fix | **Completed:** three copper cuts and three insulated jumper wires on first assembled sample. |
| Rev1.5.1 functional proof | **Passed:** power-off continuity/isolation, CV bench supply and Amiga 1200 real gameplay for all reported controls/FAST/SLOW settings. |
| Rev1.5.2 schematic | **Corrected:** ERC 0 errors / 0 warnings. |
| Rev1.5.2 PCB | **Corrected:** DRC 0 errors, 0 unconnected pads; 46 pre-existing/overridden warnings are separately documented. |
| Rev1.5.2 production Gerbers | **Updated for series manufacture:** per project-owner confirmation. Actual Gerber archive not attached for an independent plot/drill check. |
| First fabricated Rev1.5.2 unit | **Not yet documented as tested:** complete first-article inspection and gameplay test upon receipt. |

**Meaning of “production-ready”:** the known Rev1.5.1 SPEED-selector design defect has been identified, corrected and included in the manufacturing source/outputs. Boards fabricated from the **matching updated Rev1.5.2 Gerbers** are expected to have the correct switching circuitry. As with any PCB release, actual manufacturing quality and first-article function still require acceptance testing; no guaranteed zero-defect lot is claimed.

## 4. Final production handoff and QA record

Before a manufacturing order or batch acceptance, preserve the following evidence against the **same Rev1.5.2 release revision**:

1. Confirm the CAM output set was regenerated **after** the last PCB change. Archive the dated Gerber/drill/outline files next to the Rev1.5.2 project source and identify the release unambiguously.
2. Open the generated copper/mask/silkscreen/outline/drill outputs in an independent Gerber viewer or KiCad GerbView; compare `SW_SPEED1` pad placement and the associated copper routing with the corrected Rev1.5.2 PCB, including B.Cu connections and vias.
3. Ensure no Rev1.5.1 manufacturing output has been mixed into the Rev1.5.2 production archive. Keep previous Gerbers labeled obsolete for new manufacture.
4. Document disposition of **46 recorded warning overrides** (custom/auxiliary footprints and J1 mapping). These were separate from the SPEED-selector fault and must not silently be reclassified as cleared.
5. Perform an incoming first-article continuity/short check and 5 V bench test. On a real Amiga 1200 or comparable approved host, verify directions, FIRE1/FIRE2, AUTO OFF/ON, FAST/SLOW differentiation and both indicators before accepting the series-production assembly run.

## 5. Existing Rev1.5.1 inventory

The earlier fabricated stock can be recovered through the [three-cut / three-jumper rework guide](../../docs/assembly/REV1.5.1_SPEED_SELECTOR_REWORK.md). At the time of finding there were **four assembled and six bare Rev1.5.1 PCBs**. The first modified assembled PCB passed full reported Amiga 1200 gameplay validation; further reworked units need individual acceptance records. This legacy rework is **separate from the corrected Rev1.5.2 manufacturing release**.

---

**See also:** [SPEED Selector Engineering Erratum](REV1.5.1_TO_REV1.5.2_SPEED_SELECTOR_ERRATUM.md) · [Rev1.5.1 Rework Procedure](../../docs/assembly/REV1.5.1_SPEED_SELECTOR_REWORK.md) · [Historical Engineering Review](Review_Record.MD).
