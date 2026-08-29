# WASDPad+ Rev1.5.1 — Assembly and Manufacturing Procedure

**Document Version:** 1.0  
**Hardware Revision:** Rev1.5.1  
**Status:** Production Release Candidate  
**Last Updated:** 2026-08-29

---

## 1. Purpose

This document defines the manufacturing, PCB assembly, manual soldering, cable assembly and final verification procedure for **WASDPad+ Rev1.5.1**.

It replaces the earlier cable-only assembly document and expands the scope to the complete production-candidate assembly process.

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

If this document conflicts with the Master BOM or Master CPL, the Master BOM/CPL shall take precedence for component identity and placement.

---

# 2. Current Manufacturing Model

The current Rev1.5.1 production-candidate manufacturing model uses a mixed automated/manual assembly process.

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

The first Rev1.5.1 production-candidate PCBs are manufactured and partially assembled by **JLCPCB**.

---

# 3. Assembly Classification

Rev1.5.1 components are divided into the following manufacturing classes.

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

The Rev1.5.1 PCB manufacturing package is generated from the frozen production-candidate PCB design.

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

The production-candidate Gerbers and drill data shall be generated only from the approved Rev1.5.1 PCB design.

Before placing a manufacturing order:

- confirm Rev1.5.1 PCB revision
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

Rev1.5.1 production is intended to use a **lead-free manufacturing process**.

The PCB manufacturing order shall therefore use a lead-free-compatible surface finish.

Acceptable lead-free production finishes may include, depending on the manufacturing order:

- Lead-Free HASL
- ENIG

The actual surface finish used for a production batch shall be recorded with the manufacturing order.

Lead-containing HASL shall not be selected for normal Rev1.5.1 production unless explicitly approved as a controlled exception.

---

# 6. SMT Soldering Material

All automated SMT assembly for Rev1.5.1 shall use **lead-free solder paste**.

For the current JLCPCB prototype/production-candidate assembly:

- solder paste is applied as part of the factory SMT process
- components are machine-placed
- the board is reflow soldered
- the project requires a lead-free assembly configuration

JLCPCB normally uses no-clean solder paste in its assembly process.

The exact solder-paste alloy and temperature profile used for a particular manufacturing order shall follow the selected JLCPCB process and component requirements.

The project does not depend on a proprietary solder-paste alloy, but the process shall remain lead-free unless a documented engineering exception is approved.

---

# 7. Manual Soldering Material

All manual Rev1.5.1 soldering shall also use **lead-free solder material**.

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

The current Rev1.5.1 prototype/production-candidate top-side SMT population is performed by **JLCPCB**.

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

This does not mean those components are absent from the full Rev1.5.1 Master BOM.

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

Previously validated Rev1.5.1 assembly orientation corrections shall be retained in the production assembly CPL.

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

The Rev1.5.1 project performs its own electrical bring-up and functional validation after assembly.

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

U3 shall be manually soldered in the final Rev1.5.1 assembly process.

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

Do not interchange SW_AUTO1 and SW_SPEED1.

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

DB9 pin 5 is not used by Rev1.5.1.

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

The first power-up of a newly assembled production-candidate unit shall be controlled.

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

Every production-candidate unit shall verify:

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

Production-candidate units shall be validated on representative original hardware.

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

For Rev1.5.1 production-candidate builds, JLCPCB is the current PCB manufacturer and top-side SMT assembly provider.

---

# 37. Lead-Free Production Policy

Rev1.5.1 is intended to use a lead-free assembly process from PCB finish through final manual soldering.

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

Relevant manufacturing documents include:

```text
hardware/rev1.5/
├── README.md
├── Review_Record.MD
├── datasheets/
│   └── WASDPad_Rev1.5.1_DATASHEET_INDEX.md
└── bom/
    ├── README.md
    ├── WASDPad_Rev1.5.1_FULL_MASTER_BOM.csv
    ├── WASDPad_Rev1.5.1_FULL_MASTER_CPL.csv
    ├── ALTERNATE_PARTS.md
    └── PROCUREMENT_NOTES.md
```

This assembly document defines how those engineering records are translated into a physical controller.

---

# 39. External Manufacturing References

Current PCB and SMT production provider:

**JLCPCB**

Relevant public manufacturing references:

- PCB Assembly Capabilities: https://jlcpcb.com/capabilities/pcb-assembly-capabilities
- RoHS and Lead-Free Compliance: https://jlcpcb.com/help/article/rohs-and-lead-free-compliance
- Solder Paste Guidance: https://jlcpcb.com/blog/solder-paste-guide-for-pcb-assembly
- Assembly Service Terms: https://jlcpcb.com/help/article/terms-and-conditions-of-jlcpcb-assembly-service

These references describe the manufacturer's general capabilities and process information.

The Rev1.5.1 Master BOM/CPL and production order remain authoritative for the actual WASDPad+ manufacturing configuration.

---

# 40. Production Approval Boundary

This document defines the assembly process for the **Production Release Candidate**.

Following successful assembly and validation, the hardware may be promoted to:

**Production Approved**

only after completion of the formal physical validation gate documented in:

`hardware/rev1.5/Review_Record.MD`

---

# 41. Revision History

| Version | Date | Status | Changes |
|---|---|---|---|
| 0.x | Earlier Rev1.5 development | Draft | Cable-only assembly documentation and validated DE-9 cable mapping |
| **1.0** | **2026-08-29** | **Production Release Candidate** | Expanded to complete Rev1.5.1 manufacturing and assembly procedure; added JLCPCB factory SMT process, lead-free soldering policy, manual bottom-side SMD assembly, THT assembly, Kailh socket installation, cable assembly, incoming inspection, bring-up, functional acceptance, enclosure assembly and production traceability |

---

# 42. Document Status

**Project:** WASDPad+  
**Hardware Revision:** Rev1.5.1  
**Document:** Assembly and Manufacturing Procedure  
**Document Version:** 1.0  
**Status:** Production Release Candidate

This document supersedes the earlier cable-only Rev1.5 assembly procedure.
