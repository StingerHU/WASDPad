# WASDPad+ Rev1.5.1 to Rev1.5.2 — SPEED Selector Engineering Erratum

**Document revision:** 1.2  
**Date:** 2026-10-16  
**Affected design:** WASDPad+ Rev1.5.1, original fabricated PCBs requiring correction  
**Corrected design:** WASDPad+ Rev1.5.2 (`wasdpad+v1.5.2-fixed`)  
**Classification:** Functional design defect / incorrect schematic-symbol-to-physical-switch pin mapping  
**Status:** **Root cause measured and confirmed; Rev1.5.1 rework validated; Rev1.5.2 schematic, final PCB layout and corresponding series-production Gerber outputs corrected/updated; newly manufactured Rev1.5.2 hardware fully functionally validated (owner confirmed).** One physically reworked Rev1.5.1 board passed full reported Amiga 1200 gameplay testing. The Gerber regeneration is reported by the project owner; no Gerber archive was supplied for independent review in this documentation update. A **newly manufactured Rev1.5.2 PCB has since passed full reported controller functionality testing**, as confirmed by the project owner in October 2026.

> **Manufacturing release notice:** **Rev1.5.2 is the corrected series-production design baseline, with the final PCB model and fabrication Gerbers updated to include the SPEED selector fix (project-owner confirmation).** Do **not** manufacture unmodified Rev1.5.1 Gerbers. Existing Rev1.5.1 boards can be retained following the documented three-cut/three-jumper patch and individual electrical/functional tests. The historical Rev1.5.1 PASS review remains a record of the earlier review, not approval of unmodified Rev1.5.1 stock. See the [rework guide](../../docs/assembly/REV1.5.1_SPEED_SELECTOR_REWORK.md) and [Rev1.5.2 production release notes](REV1.5.2_MANUFACTURING_RELEASE_NOTES.md).

## 1. Discovery and symptoms

Physical debugging of a Rev1.5.1 assembled prototype found that the `SW_SPEED1` FAST position failed to operate: the red FAST status LED remained off and the ICM7555 oscillator output was essentially static (approximately 4.78 V DC at U1 pin 3). The SLOW position appeared functional, but energized the `AF_FAST_SEL` control path rather than the intended `AF_SLOW_SEL` path.

Measurements established the following facts:

- On the **physical three-terminal toggle switch**, pad 2 is the common contact.
- The physical switch closes **pads 1–2 in FAST** and **pads 2–3 in SLOW** (corresponding to the tested installed actuator positions).
- The Rev1.5.1 KiCad symbol was `Switch:SW_SP3T`, whose schematic common contact is **pin 3**.
- The custom three-pad PCB footprint retained its **physical pad 2** as the common contact. KiCad maps pins to pads **by number**, not by visual position or physical switching behavior.
- Rev1.5.1 therefore placed the positive autofire-enable signal, `AF_EN_P`, on physical pad 3 instead of pad 2.

The physical switch itself was not faulty. A schematic/footprint/part-function pin mapping error caused the defect.

## 2. Root cause: wrong network assignment on Rev1.5.1

**Viewed from the PCB component/front side**, with the SPEED footprint numbered 1–2–3 from left to right:

| Physical pad | Incorrect Rev1.5.1 PCB net | Required Rev1.5.2 net | Correct function |
| --- | --- | --- | --- |
| 1 (left) | `AF_SLOW_SEL` | `AF_FAST_SEL` | FAST selection; CD4066 U2 pin 5 |
| 2 (center, actual common) | `AF_FAST_SEL` | `AF_EN_P` | Common autofire enable; R12 pad 2 net |
| 3 (right) | `AF_EN_P` | `AF_SLOW_SEL` | SLOW selection; CD4066 U2 pin 13 |

In the unmodified Rev1.5.1 board, FAST physically connects pads 1 and 2, joining the two 100 kΩ pull-down control networks without bringing `AF_EN_P` to either. Both relevant CD4066 control inputs stay LOW, preventing the selected timing path from operating. SLOW connects pads 2 and 3 and inadvertently feeds `AF_EN_P` to `AF_FAST_SEL`, explaining why only that switch position oscillated.

## 3. Corrected Rev1.5.2 design

The electrical symbol for `SW_SPEED1` has been changed to **`Switch:SW_SPDT`**, which uses schematic pin **2** as the common contact. The existing custom mechanical footprint (`ToggleSwitches:SW_100SP3T1B1M2QEH`) and mounting location were retained. The three connections were reassigned as shown above.

Expected switch logic:

| Selected mode | Physical contacts closed | Asserted control | CD4066 control pin |
| --- | --- | --- | --- |
| FAST | 1–2 | `AF_FAST_SEL` | U2 pin 5 |
| SLOW | 2–3 | `AF_SLOW_SEL` | U2 pin 13 |

The normal AUTO ON/OFF switch is a separate design and is not implicated by this SPEED-selector defect.

The corrected schematic passed KiCad ERC with **0 errors / 0 warnings**. After schematic-to-PCB synchronization and rerouting, the corrected PCB reported **0 DRC errors and 0 unconnected pads**, with **46 warnings** associated with custom/auxiliary footprints and J1 mapping. These warnings require separate final-release review; a clean ERC/DRC run alone does **not** verify the physical switch common pin.

**Production design update:** The final Rev1.5.2 schematic and `wasdpad+v1.5.2-fixed.kicad_pcb` incorporate the corrected `SW_SPEED1` physical pad assignment; PCB routing was updated to match. **The corresponding fabrication Gerber outputs were regenerated/updated for the intended series-production run**, as confirmed by the project owner. Thus the identified Rev1.5.1 SPEED common-pad mapping defect is corrected in the **manufacturing-source design**, not merely bypassed on the repaired prototype.

This documentation review did **not** receive or independently parse the regenerated Gerber archive. Manufacturing handoff must use Gerbers exported from the corrected Rev1.5.2 PCB, never archived Rev1.5.1 fabrication files. Gerber-level plot and drill verification remains a normal release check, not a claim that the design fix is unfinished. See [Rev1.5.2 manufacturing release notes](REV1.5.2_MANUFACTURING_RELEASE_NOTES.md).

**Validation boundary:** the actual Rev1.5.1 hardware patch is proven by physical measurements and Amiga 1200 gameplay. The corrected Rev1.5.2 design and Gerber update remove the known layout defect, and **a newly manufactured Rev1.5.2 unit has now passed full reported functional acceptance** (project-owner confirmation, October 2026). Instrumented per-pin logs were not supplied for independent review.

## 4. Rev1.5.1 physical rework and verification

The validated patch strategy leaves the soldered SPEED switch in place:

1. Isolate the three old F.Cu connections by three precise copper trace cuts at verified accessible locations.
2. Route three fine insulated patch wires on the PCB rear side from the through-hole SPEED switch pads to the corresponding **correct** nets.
3. Where necessary, carefully remove a small patch of solder mask from a suitable B.Cu trace and solder the insulated jumper to exposed copper.
4. Perform power-off continuity and isolation measurements, check +5 V-to-GND for a short, then power up with a current-limited 5 V supply.
5. Test all operating modes on a real host before cleaning and applying UV-curable solder mask / protective lacquer.

**Do not** cut or scrape a PCB solely from a generic photograph: confirm the PCB revision, the copper layer and each source/target net before work. Exact visual references and a verified measurement checklist are in [the Rev1.5.1 rework procedure](../../docs/assembly/REV1.5.1_SPEED_SELECTOR_REWORK.md).

## 5. Observed validation results (one patched Rev1.5.1 prototype)

The following are actual bench and gameplay observations, **not theoretical predictions**:

| Test | Observed outcome |
| --- | --- |
| Old SLOW connection isolated from pad 1 (FAST selector position) | OL / open |
| New SLOW path, SW_SPEED1 pad 3 to U2 pin 13 | Continuity |
| New FAST path, SW_SPEED1 pad 1 to U2 pin 5 | Continuity |
| New enable path, SW_SPEED1 pad 2 to R12 pad 2 | Continuity |
| Old enable path isolated from pad 3 (FAST position) | OL / open |
| Old FAST path isolated from pad 2 (SLOW position) | OL / open |
| U2 pin 14 (+5 V) to pin 7 (GND), power off | No sustained continuity beep |
| Bench supply at 5 V in FAST | CV regulation; power LED on; red FAST indicator operating |
| ICM7555 U1 pin 3 with FAST selected | Approximately 2.199 V DC average |
| ICM7555 U1 pin 3 with SLOW selected | Approximately 2.2 V DC average |
| Real host validation | All reported controller functions passed during gameplay on **Amiga 1200** |

**Measurement interpretation:** a DC voltmeter reading of about 2.2 V on a switching output does not by itself measure or prove oscillation frequency. FAST/SLOW behavior was instead functionally checked during real gameplay. No instrumented Hz measurement is claimed.

**Timing components on the patched unit:** `R13 = 330 kΩ`, `R14 = 680 kΩ`. These are installed component values; do not confuse them with direct, independent end-to-end timing resistance in every CD4066 switch configuration.

## 6. Resolution and manufacturing release status

The corrective action was carried through **both branches of the project**:

| Deliverable / evidence | Status and evidence |
| --- | --- |
| Failure reproduced and root cause identified | **Completed:** switch contact pairs and CD4066 control levels measured; original symbol/footprint pin mapping mismatch identified. |
| Existing Rev1.5.1 PCB rework | **Completed and validated for one assembled board:** three cuts and three insulated rear-side jumpers; continuity/isolation/short checks passed. |
| Real-world rework verification | **Completed for the reworked board:** all reported functions passed during Amiga 1200 gameplay, including both autofire settings. |
| Rev1.5.2 schematic | **Corrected:** `Switch:SW_SPDT`, common pin/pad 2; ERC 0 errors / 0 warnings. |
| Rev1.5.2 PCB layout | **Corrected and saved:** pad 1 FAST, pad 2 ENABLE, pad 3 SLOW; DRC 0 errors / 0 unconnected pads (46 existing warnings require release awareness). |
| Rev1.5.2 manufacturing Gerbers | **Updated for series production, project-owner confirmed:** regenerated from the corrected board. Archive not independently supplied/inspected in this documentation pass. |
| **Newly fabricated Rev1.5.2 board acceptance** | **PASS:** a newly manufactured Rev1.5.2 unit passed full reported controller functionality, including SPEED selection (project-owner confirmed, October 2026). |

At discovery there were **four assembled Rev1.5.1 boards and six additional fabricated bare boards**. As of this report **one** patched unit has a recorded full Amiga 1200 functional test. The patch is repeatable, but this document does not claim that the other nine have already been reworked or verified.

**Manufacturing baseline:** **use the corrected Rev1.5.2 PCB and its updated Rev1.5.2 Gerbers** for series production. Do not release unmodified Rev1.5.1 fabrication outputs. The SPEED-selector correction is now also **confirmed functional on an actually manufactured Rev1.5.2 board**, not just expected from the artwork. Confirm that the fabrication output set matches the final PCB, perform standard fabrication-output/J1-footprint review, and retain the now-confirmed first-article functional PASS together with the standard acceptance records for subsequent produced units.

The 46 recorded DRC warnings concern custom/auxiliary footprints and J1 mapping; they are not evidence of a remaining SPEED-selector failure. Their disposition must nevertheless be recorded separately before an unconditional fabrication QA sign-off. Preserve the historical Rev1.5.1 engineering review together with this post-validation erratum.

## 7. Preventive action: mandatory common-pin verification

For **every mechanical selector** prior to design freeze:

1. Identify the physical common terminal from the manufacturer's data and/or measure it on an unpowered sample.
2. Measure the pair of contacts closed in every lever position.
3. Verify correspondence between schematic pin number, footprint pad number and actual physical terminal—not merely schematic-to-PCB connectivity.
4. Confirm control-level polarity and resulting functional path at each switch position.
5. Perform a physical prototype smoke test and gameplay/functional test before assigning production-approved status.

**Lesson learned:** Passing ERC and DRC cannot detect an incorrect physical common terminal if the schematic and PCB consistently use the wrong pin numbering. The defect was diagnosed on a real Rev1.5.1 assembly, fixed on existing hardware **and** corrected in the definitive Rev1.5.2 board plus its series-production Gerber outputs.

---

**Related documents:** [Rev1.5.1 Rework Procedure](../../docs/assembly/REV1.5.1_SPEED_SELECTOR_REWORK.md) · [Rev1.5.2 Manufacturing Release Notes](REV1.5.2_MANUFACTURING_RELEASE_NOTES.md) · [Historical Engineering Review](Rev1.5.1-Engineering-Manufacturing-Record.MD) · [Development Roadmap](../../docs/roadmap/ROADMAP.md).
