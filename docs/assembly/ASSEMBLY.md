# WASDPad+ Rev1.5.2 — Assembly and Manufacturing Procedure

**Document Version:** 2.0  
**Hardware Revision:** Rev1.5.2  
**Status:** Final Production Release — manufactured Rev1.5.2 functionally validated  
**Last Updated:** 2026-10-19

---

## 1. Purpose

This document defines the manufacturing, PCB assembly, manual soldering, cable assembly and final verification procedure for **WASDPad+ Rev1.5.2**.

It replaces the earlier cable-only assembly document and expands the scope to the complete released-hardware assembly and acceptance process.

The document covers:

- PCB manufacturing
- automated SMT assembly
- solder materials
- manually assembled SMD parts
- THT assembly
- Kailh hot-swap socket installation
- mechanical switch installation
- DE-9 cable assembly
- incoming inspection
- electrical bring-up
- final functional verification
- production traceability

The authoritative component and placement records are:

- `hardware/rev1.5/bom/WASDPad_Rev1.5.1_FULL_MASTER_BOM.csv`
- `hardware/rev1.5/bom/WASDPad_Rev1.5.1_FULL_MASTER_CPL.csv`

The CSV files currently in this repository are **Rev1.5.1-labelled historical BOM/CPL references**, not independently verified Rev1.5.2 release exports. For Rev1.5.2 manufacturing, the matching final-revision BOM/CPL and Gerber package used for the successful production build take precedence. See the [release record](../../hardware/rev1.5/REV1.5.2_MANUFACTURING_RELEASE_NOTES.md).

---

# 2. Current Manufacturing Model

The released Rev1.5.2 manufacturing model uses a mixed automated/manual assembly process.

```text
PCB fabrication
      │
      ▼
JLCPCB top-side SMT assembly
      │
      ▼
Incoming visual inspection
      │
      ▼
Manual bottom-side SMD assembly
      │
      ▼
Manual THT assembly
      │
      ▼
Manual cable assembly
      │
      ▼
Mechanical switch installation
      │
      ▼
Electrical bring-up
      │
      ▼
Functional validation
      │
      ▼
Final enclosure assembly
```

The earlier Rev1.5.1 production-candidate fabrication/SMT work was documented with **JLCPCB**. For subsequent Rev1.5.2 production lots, record the actual fabricator, SMT population scope and revision-matched production data for that lot.

---

# 3. Assembly Classification

Rev1.5.2 components are divided into the following manufacturing classes.

## 3.1 Factory-Assembled Top-Side SMD

The majority of top-side SMD electronics are populated by JLCPCB.

This includes, as applicable:

- integrated circuits
- MOSFETs
- transistors
- ESD / TVS protection devices
- resettable PTC
- SMD resistors
- SMD capacitors
- key-backlight LEDs
- other production-approved top-side SMD parts listed in the JLCPCB assembly BOM/CPL

The JLCPCB assembly BOM/CPL is a manufacturing subset of the Master BOM/CPL.

---

## 3.2 Manual Bottom-Side SMD

Bottom-side parts are not part of the current automated top-side SMT assembly process.

These are installed manually.

Current manual bottom-side SMD parts include:

- `U3` — C&K `PCM12SMTR` backlight switch
- `SW1–SW8` — Kailh / Kaihua `CPG151101S11` MX hot-swap sockets

These parts require careful alignment because they are mechanically significant to the final enclosure and gameplay-switch geometry.

---

## 3.3 Manual Through-Hole Assembly

Through-hole components are installed and soldered manually.

Current THT assembly includes:

- `D1` — power LED
- `D2` — 1N4148 diode
- `D7` — red/green dual-colour autofire status LED
- `SW_AUTO1` — autofire ON/OFF switch
- `SW_SPEED1` — autofire SLOW/FAST selector

THT components shall be installed only after the factory-assembled SMD board has passed incoming inspection.

---

## 3.4 Mechanical / Manual Assembly

Mechanical gameplay switches are installed after electrical PCB assembly.

Current production-fitted switch:

**Gateron KS-8 Yellow**

Quantity:

**8**

These switches are inserted into the Kailh hot-swap sockets and are not soldered directly to the PCB.

---

## 3.5 Cable / Manual Assembly

The molded female DE-9 controller cable is soldered manually to the PCB J1 interface pads.

The cable assembly is considered part of final controller assembly, not automated PCBA.

---

# 4. PCB Manufacturing

The Rev1.5.2 PCB manufacturing package is generated from the frozen Rev1.5.2 final-release PCB design.

Required manufacturing outputs include:

- F.Cu
- B.Cu
- F.Mask
- B.Mask
- F.Silkscreen
- B.Silkscreen
- F.Paste
- B.Paste
- Edge.Cuts
- plated-through-hole drill data
- non-plated-through-hole drill data
- Gerber job information where applicable

The production Gerbers and drill data shall be generated only from the approved Rev1.5.2 final-release PCB design.

Before placing a manufacturing order:

- confirm Rev1.5.2 PCB revision
- run final DRC
- refill all copper zones
- confirm board outline
- verify PTH and NPTH data
- verify solder-mask openings
- verify paste layers
- verify mounting holes
- verify J1 cable pads
- verify switch/socket geometry
- verify U3 bottom-side placement

---

# 5. PCB Surface Finish and Lead-Free Requirement

Rev1.5.2 production is intended to use a **lead-free manufacturing process**.

The PCB manufacturing order shall therefore use a lead-free-compatible surface finish.

Acceptable lead-free production finishes may include, depending on the manufacturing order:

- Lead-Free HASL
- ENIG

The actual surface finish used for a production batch shall be recorded with the manufacturing order.

Lead-containing HASL shall not be selected for normal Rev1.5.2 production unless explicitly approved as a controlled exception.

---

# 6. SMT Soldering Material

All automated SMT assembly for Rev1.5.2 shall use **lead-free solder paste**.

For a JLCPCB production order (if applicable to the actual released manufacturing order):

- solder paste is applied as part of the factory SMT process
- components are machine-placed
- the board is reflow soldered
- the project requires a lead-free assembly configuration

JLCPCB normally uses no-clean solder paste in its assembly process.

The exact solder-paste alloy and temperature profile used for a particular manufacturing order shall follow the selected JLCPCB process and component requirements.

The project does not depend on a proprietary solder-paste alloy, but the process shall remain lead-free unless a documented engineering exception is approved.

---

# 7. Manual Soldering Material

All manual Rev1.5.2 soldering shall also use **lead-free solder material**.

This includes:

- THT soldering
- U3 manual SMD soldering
- Kailh hot-swap socket soldering
- DE-9 cable soldering
- approved rework

Recommended characteristics:

- electronics-grade lead-free solder
- suitable flux system
- controlled soldering temperature
- good wetting on the selected PCB finish
- no corrosive flux residues

If a no-clean flux system is used, visible or mechanically problematic residues shall still be removed where necessary.

The exact solder-wire manufacturer, alloy and flux type used for a production batch should be recorded in the production log when controlled traceability is required.

---

# 8. JLCPCB Automated SMT Assembly

The original Rev1.5.1 production-candidate top-side SMT population was documented with **JLCPCB**. The actual Rev1.5.2 production order determines the applicable assembly-house details.

Assembly data is derived from:

- approved Gerber data
- manufacturing BOM
- manufacturing CPL / pick-and-place data

The JLCPCB BOM/CPL may intentionally exclude:

- THT components
- U3 bottom-side switch
- Kailh hot-swap sockets
- mechanical Gateron switches
- external DE-9 cable
- PCB features / DNP items

This does not mean the omitted components are absent from the current released Rev1.5.2 assembly dataset.

---

# 9. JLCPCB Component Orientation Verification

Before approving an SMT assembly order, the graphical placement preview shall be reviewed.

Critical orientation-sensitive components include:

- U1
- U2
- D4
- D5
- D6
- Q1–Q9
- D8–D15

The final Rev1.5.2 assembly CPL shall retain all orientation corrections confirmed applicable to the released design, including those carried forward from earlier Rev1.5.1 engineering.

Particular attention shall be paid to:

- IC pin 1
- SOT-23 pin mapping
- ESD-array orientation
- TVS-device orientation
- LED polarity

A BOM match alone is not sufficient to approve assembly.

---

# 10. Factory Assembly Limitations

The external PCB assembly process shall not be treated as final product validation.

The assembled boards must still undergo project-level incoming inspection and electrical testing.

In particular:

- automated assembly does not guarantee functional operation of every board
- placement data must be verified before ordering
- component substitutions require engineering approval
- boards must be inspected after receipt
- a power-on test shall not be assumed to have been performed by the assembly manufacturer

The Rev1.5.2 project performs its own electrical bring-up and functional validation after assembly.

---

# 11. Incoming PCB/PCBA Inspection

Immediately after receiving the factory-manufactured boards, perform a visual inspection before manual assembly.

Check:

- correct PCB revision
- correct board outline
- no visible PCB damage
- no delamination
- no major solder-mask defects
- no damaged pads
- no damaged plated holes
- no obviously missing top-side SMD components
- no visibly shifted SMD components
- no obvious solder bridges
- no tombstoned passive components
- correct IC orientation
- correct protection-device orientation
- correct transistor/MOSFET orientation
- correct backlight LED orientation
- correct board quantity

Any suspicious board shall be separated from the normal assembly batch until reviewed.

---

# 12. Pre-Manual-Assembly Electrical Check

Before installing manually soldered parts:

1. Inspect the +5 V and GND areas.
2. Measure resistance between +5 V and GND.
3. Confirm that there is no hard short circuit.
4. Verify continuity of key ground paths where appropriate.
5. Inspect factory-populated protection components.
6. Inspect U1 and U2 orientation.
7. Inspect D4/D5/D6 orientation.

Do not proceed to full assembly if a short circuit or obvious factory assembly error is found.

---

# 13. Manual Bottom-Side SMD Assembly

## 13.1 U3 — Backlight Switch

Reference:

`U3`

MPN:

`PCM12SMTR`

PCB side:

`Bottom`

U3 shall be manually soldered in the final Rev1.5.2 assembly process.

Assembly requirements:

- verify correct bottom-side orientation
- align the switch body squarely with the PCB
- ensure the actuator remains mechanically accessible
- avoid excessive solder that could interfere with movement
- verify all intended pads are wetted
- inspect for solder bridges
- verify switch movement after soldering

After soldering, confirm electrically:

```text
Backlight OFF -> BACKLIGHT_5V disconnected
Backlight ON  -> BACKLIGHT_5V supplied
```

---

## 13.2 Kailh Hot-Swap Sockets

References:

`SW1–SW8`

MPN:

`CPG151101S11`

PCB side:

`Bottom`

The hot-swap sockets shall be installed manually.

Because the sockets define the mechanical relationship between the PCB and the gameplay switches, alignment is critical.

Assembly requirements:

- place each socket flat against the PCB
- verify socket orientation
- verify contact openings align with the MX switch-pin locations
- solder both electrical/mechanical pads securely
- avoid excessive solder entering the socket
- do not deform the plastic housing with prolonged heat
- inspect every socket after soldering

After cooling, verify:

- socket is mechanically secure
- socket remains flat
- no solder interferes with switch insertion
- switch pins enter without abnormal force

---

# 14. Manual THT Assembly

THT components are soldered manually using lead-free solder.

Recommended assembly sequence:

1. D2 — small-signal diode
2. D1 — power LED
3. D7 — dual-colour status LED
4. SW_AUTO1 — autofire ON/OFF
5. SW_SPEED1 — speed selector

The exact sequence may be modified for fixture access, but polarity/orientation checks shall be preserved.

---

# 15. D2 Installation

Reference:

`D2`

Type:

`1N4148`

Package:

DO-35 THT

D2 is polarity-sensitive.

Before soldering:

- identify the cathode band
- compare against PCB marking
- confirm correct orientation

After soldering:

- trim leads safely
- inspect joint wetting
- verify no bridge exists to adjacent copper or pads

---

# 16. D1 Power LED Installation

Reference:

`D1`

Production MPN:

`3RD-F`

D1 is polarity-sensitive.

Before soldering:

- confirm anode/cathode orientation
- confirm final LED height
- confirm enclosure visibility

The LED shall be mechanically aligned before final soldering.

---

# 17. D7 Dual-Colour LED Installation

Reference:

`D7`

Production MPN:

`3BC-3-F`

Validated pinout:

```text
Pin 1 = Red anode
Pin 2 = Common cathode
Pin 3 = Green anode
```

D7 orientation is critical.

Before soldering:

- identify the physical LED orientation
- confirm common cathode pin 2
- compare against PCB footprint
- confirm LED body height for enclosure fit

After assembly, both colour channels shall be functionally tested.

---

# 18. Autofire Toggle Switch Installation

## SW_AUTO1

MPN:

`100SP1T1B4M2QE`

Function:

Autofire OFF / ON

## SW_SPEED1

MPN:

`100SP3T1B1M2QEH`

Function:

SLOW / FAST selection

Before soldering:

- confirm correct switch MPN at each position
- confirm mechanical orientation
- ensure body sits squarely against the intended mounting geometry
- confirm enclosure clearance

**Rev1.5.2 SPEED selector pad mapping is mandatory:** the real selector's centre **pad 2 is common**; connect **pad 1 to `AF_FAST_SEL`**, **pad 2 to `AF_EN_P`**, and **pad 3 to `AF_SLOW_SEL`**. The switch closes **1–2 for FAST** and **2–3 for SLOW**. The schematic uses `Switch:SW_SPDT`; the old Rev1.5.1 `SW_SP3T` common mapping is incorrect and must not be used when preparing Gerbers.

Do not interchange SW_AUTO1 and SW_SPEED1. Always verify actual pad continuity with a meter on an unpowered unit before accepting unfamiliar or substituted switch parts.

---

# 19. DE-9 Cable Assembly

The currently approved cable architecture uses:

- molded DE-9 female connector
- 9 internal conductors
- flying leads at the PCB side
- direct solder connection to J1
- 8 active conductors
- DB9 pin 5 unused

The cable is soldered manually after PCB assembly.

---

# 20. DE-9 Pinout

| DB9 Pin | Function |
|---:|---|
| 1 | UP |
| 2 | DOWN |
| 3 | LEFT |
| 4 | RIGHT |
| 5 | Not used |
| 6 | FIRE1 |
| 7 | +5 V |
| 8 | GND |
| 9 | FIRE2 / POTX |

The DB9 pin number is authoritative.

Wire colour is not authoritative.

---

# 21. Validated Cable Batch Mapping

The following colour mapping was physically verified for the originally validated cable batch.

| Wire Color | DB9 Pin | Function | J1 Pad |
|---|---:|---|---:|
| Red | 1 | UP | 1 |
| Black | 2 | DOWN | 2 |
| Grey | 3 | LEFT | 3 |
| Orange | 4 | RIGHT | 4 |
| Brown | 5 | Not used | NC |
| Green | 6 | FIRE1 | 6 |
| White | 7 | +5 V | 7 |
| Blue | 8 | GND | 8 |
| Yellow | 9 | FIRE2 / POTX | 9 |

This colour mapping is valid only for the cable batch that was physically verified.

---

# 22. Mandatory Cable Batch Verification

## DO NOT RELY ON WIRE COLOUR ALONE

Generic controller cables may be manufactured by different factories or changed without notice.

A visually identical cable may contain a different internal colour assignment.

Therefore:

**The first cable from every new supplier or production batch MUST be continuity-tested before production assembly.**

Verify continuity from every DB9 contact to its corresponding flying lead.

If any colour differs from the previously validated mapping:

**STOP ASSEMBLY.**

Document the complete measured pin-to-wire mapping for that batch before continuing.

---

# 23. J1 PCB Connection

The cable wires are soldered directly to J1 PCB pads.

The intended mapping is:

```text
DB9 pin 1 -> J1 pad 1
DB9 pin 2 -> J1 pad 2
DB9 pin 3 -> J1 pad 3
DB9 pin 4 -> J1 pad 4
DB9 pin 5 -> NC
DB9 pin 6 -> J1 pad 6
DB9 pin 7 -> J1 pad 7
DB9 pin 8 -> J1 pad 8
DB9 pin 9 -> J1 pad 9
```

J1 pad 5 is intentionally unused.

---

# 24. Unused Pin 5 Conductor

DB9 pin 5 is not used by Rev1.5.2.

The corresponding cable conductor shall:

1. not be soldered to the PCB
2. be cut to a safe length
3. have no exposed conductor capable of contacting PCB copper or enclosure hardware
4. be individually insulated if necessary

Do not connect DB9 pin 5 to:

- GND
- +5 V
- FIRE
- any direction input
- any other PCB node

---

# 25. Cable Soldering Requirements

The DE-9 cable shall be soldered using lead-free solder.

Before soldering:

- strip only the required conductor length
- twist stranded conductors where applicable
- pre-tin only when appropriate for the cable and pad geometry
- verify each wire against the measured batch mapping
- provide mechanical strain relief through the enclosure design

During soldering:

- avoid excessive conductor heating
- ensure full pad wetting
- avoid excessive solder buildup
- avoid stray wire strands
- inspect for bridges between adjacent J1 pads

After soldering:

- perform continuity verification
- inspect mechanical strain
- confirm no exposed pin-5 conductor remains

---

# 26. Mechanical Switch Installation

After the Kailh sockets are soldered and inspected, install the eight Gateron KS-8 Yellow switches.

Before installation:

- inspect switch pins
- straighten bent pins
- verify the socket is aligned
- ensure the switch body matches the enclosure geometry

During insertion:

- align both electrical switch pins with the Kailh socket
- press vertically
- do not force a misaligned switch

After installation:

- verify switch sits fully seated
- verify no switch rocks excessively
- actuate every switch manually

---

# 27. Flux and Cleaning

The project uses lead-free soldering materials.

Factory SMT assembly may use no-clean solder paste.

Manual soldering should preferably use electronics-grade no-clean flux/solder unless another approved process is documented.

Cleaning requirements:

- remove loose flux contamination
- remove conductive or corrosive residues
- clean areas where residue could interfere with switch movement or mechanical contact
- do not allow solvent to enter mechanical switches or hot-swap sockets unless the cleaning agent is proven compatible

Cosmetic no-clean residue may remain where it does not affect reliability, inspection or mechanical operation.

---

# 28. Rework

Rework shall be minimized.

If rework is required:

- use lead-free-compatible soldering materials
- protect adjacent plastic parts from overheating
- avoid excessive pad heating
- avoid repeated reflow cycles where possible
- inspect the repaired joint under magnification where appropriate
- repeat relevant continuity/function tests after rework

Critical rework on protection devices or ICs shall be documented in the production record.

---

# 29. ESD Handling During Assembly

Although the completed controller includes ESD protection at its external interface, unassembled semiconductor components and partially assembled boards shall still be handled using appropriate ESD precautions.

Recommended:

- grounded ESD work surface
- grounded wrist strap where appropriate
- ESD-safe component storage
- avoid unnecessary handling of IC pins/pads
- store unfinished PCBAs in antistatic packaging

The presence of onboard ESD protection does not replace normal electronics assembly ESD discipline.

---

# 30. Final Electrical Inspection Before Power

Before connecting the assembled controller to a Commodore or other host system:

- inspect every manual solder joint
- inspect all J1 cable pads
- inspect U3
- inspect all Kailh sockets
- inspect D1, D2 and D7 polarity
- inspect toggle-switch soldering
- verify no loose wire strands
- verify no solder debris
- verify no obvious bridges

Mandatory measurements:

```text
DB9 pin 7 -> J1 pad 7 -> +5 V
DB9 pin 8 -> J1 pad 8 -> GND
```

There must be **no hard short circuit between +5 V and GND**.

---

# 31. Final Cable Continuity Verification

After cable soldering, verify:

1. DB9 pin 1 -> J1 pad 1
2. DB9 pin 2 -> J1 pad 2
3. DB9 pin 3 -> J1 pad 3
4. DB9 pin 4 -> J1 pad 4
5. DB9 pin 5 -> not connected
6. DB9 pin 6 -> J1 pad 6
7. DB9 pin 7 -> J1 pad 7
8. DB9 pin 8 -> J1 pad 8
9. DB9 pin 9 -> J1 pad 9
10. no short exists between +5 V and GND
11. unused pin-5 conductor is safely insulated
12. no adjacent J1 pad is accidentally bridged

---

# 32. Initial Power-Up

The first power-up of any newly assembled unit shall be controlled.

Recommended sequence:

1. verify +5 V / GND resistance
2. verify cable mapping
3. connect to a current-limited test supply or suitable protected test setup where available
4. verify expected supply voltage
5. observe current consumption
6. check for abnormal heating
7. verify power LED
8. disconnect immediately if unexpected current or heating is observed

Only after passing basic bring-up should the unit be connected to representative vintage computer hardware.

---

# 33. Functional Acceptance Test

Every newly assembled production unit shall verify:

- UP
- DOWN
- LEFT
- RIGHT
- FIRE1 LEFT
- FIRE1 RIGHT
- FIRE2 LEFT
- FIRE2 RIGHT
- autofire OFF
- autofire SLOW
- autofire FAST
- LEFT selector position = SLOW
- RIGHT selector position = FAST
- red/green autofire indication
- power indication
- all eight backlight LEDs
- backlight ON/OFF operation
- hot-swap socket retention
- mechanical switch actuation
- DE-9 cable continuity
- no abnormal heating

A unit failing any mandatory function shall not be classified as production-accepted until repaired and retested.

---

# 34. Real-System Validation

Newly assembled production units shall be validated on representative original hardware.

Primary targets include:

- Commodore 64
- Commodore 128 where applicable
- Commodore Amiga

Testing should include:

- basic movement
- FIRE1
- FIRE2 where supported
- autofire gameplay
- repeated autofire mode switching
- extended gameplay
- backlight operation
- cable movement / strain behaviour

---

# 35. Enclosure Assembly

Final enclosure assembly is performed after electrical PCB validation.

Before closing the enclosure, verify:

- PCB sits correctly in mechanical mounts
- all gameplay switches align with enclosure openings
- toggle switches remain accessible
- D1 and D7 remain visible
- U3 remains accessible from the intended opening
- cable strain relief is correctly seated
- no wire is trapped or pinched
- no PCB component contacts the enclosure unexpectedly
- switches actuate freely

Do not force the enclosure closed against mechanical interference.

---

# 36. Production Traceability

For each production batch, record where practical:

- hardware revision
- PCB manufacturing order number
- PCB manufacturer
- SMT assembly provider
- assembly order number
- board quantity
- surface finish
- automated solder process
- manual solder material
- manual assembly date
- component substitutions
- cable supplier/batch
- assembler or assembly station
- rework performed
- final validation result

JLCPCB was the documented Rev1.5.1 PCB and SMT provider. For Rev1.5.2 production builds, record the actual PCB fabricator and assembly provider from the applicable order; do not infer them from the Rev1.5.1 records.

---

# 37. Lead-Free Production Policy

Rev1.5.2 is intended to use a lead-free assembly process from PCB finish through final manual soldering.

Project requirement:

```text
PCB finish          -> Lead-free compatible
Factory SMT paste   -> Lead-free
Manual SMD solder   -> Lead-free
Manual THT solder   -> Lead-free
Cable soldering     -> Lead-free
Approved rework     -> Lead-free
```

Any deviation from this policy shall be documented and explicitly approved.

Component-level RoHS declarations and supplier certificates are maintained separately from this assembly procedure.

---

# 38. Manufacturing Documentation

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

All `Rev1.5.1`-named files are historical references. The current **Rev1.5.2** release is functionally validated on manufactured hardware, but its complete Gerber/drill/CAD/BOM/CPL output set is not attached to this repository snapshot. Obtain that revision-matched production dataset for a new manufacturing order.

---

# 39. External Manufacturing References

Previously documented PCB and SMT provider for the Rev1.5.1 production-candidate build:

**JLCPCB**

The actual manufacturer/SMT scope for the completed Rev1.5.2 build is not independently established by the public repository export. Record it from the project owner’s production order.

Relevant public manufacturing references:

- PCB Assembly Capabilities: https://jlcpcb.com/capabilities/pcb-assembly-capabilities
- RoHS and Lead-Free Compliance: https://jlcpcb.com/help/article/rohs-and-lead-free-compliance
- Solder Paste Guidance: https://jlcpcb.com/blog/solder-paste-guide-for-pcb-assembly
- Assembly Service Terms: https://jlcpcb.com/help/article/terms-and-conditions-of-jlcpcb-assembly-service

These references describe the manufacturer's general capabilities and process information.

For Rev1.5.2 production, use the *actual matching Rev1.5.2* BOM/CPL and fabrication order. The archived `Rev1.5.1`-named CSV files in this ZIP are not self-certifying as Rev1.5.2 outputs.

---

# 40. Production Approval Boundary

**The manufactured Rev1.5.2 controller has passed its complete reported functional test**, per project-owner confirmation (October 2026). It is the **Final Production Release** revision. This procedure remains applicable for **routine quality assurance of subsequent production lots**; those units must not be assumed tested merely because the first article passed.

The historical Rev1.5.1 preliminary review is [preserved separately](../../hardware/rev1.5/Rev1.5.1-Engineering-Manufacturing-Record.MD). The [Rev1.5.2 manufacturing record](../../hardware/rev1.5/REV1.5.2_MANUFACTURING_RELEASE_NOTES.md) is the current release authority.

---

# 41. Revision History

| Version | Date | Status | Changes |
|---|---|---|---|
| 0.x | Earlier Rev1.5 development | Draft | Cable-only assembly documentation and validated DE-9 cable mapping |
| **1.0** | **2026-08-29** | **Historical Production Release Candidate** | Expanded to complete Rev1.5.1 manufacturing and assembly procedure; added JLCPCB factory SMT process, lead-free soldering policy, manual bottom-side SMD assembly, THT assembly, Kailh socket installation, cable assembly, incoming inspection, bring-up, functional acceptance, enclosure assembly and production traceability |
| **2.0** | **2026-10-19** | **Final Production Release — fabricated unit functional PASS** | Correct Rev1.5.2 selector mapping and first-article result; previous revision records are historical. |

---

# 42. Document Status

**Project:** WASDPad+  
**Hardware Revision:** **Rev1.5.2**  
**Document:** Assembly and Manufacturing Procedure  
**Document Version:** **2.0**  
**Status:** **FINAL PRODUCTION RELEASE — newly fabricated Rev1.5.2 functional PASS**

The earlier Rev1.5.1 production-candidate procedure remains represented in the version history; its incomplete physical validation is no longer the release status of the current Rev1.5.2 design.
