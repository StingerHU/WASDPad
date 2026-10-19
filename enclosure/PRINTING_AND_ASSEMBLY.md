# WASDPad+ Rev1.5.2 - Printing and Mechanical Assembly

**Document revision:** 2.1 (2026-10-19)  
**Rigid housing:** Finalized, sixth iteration  
**TPU wrist rest:** Optional, experimental / near-final

This is a project-oriented build guide for the two-part WASDPad+ housing and its optional TPU wrist rest. It is **not** a complete slicer profile or a substitute for the private mechanical model files.

## Parts and materials

| Item | Quantity | Specification / note |
| --- | ---: | --- |
| Upper housing | 1 | FDM-printed rigid PLA part |
| Lower base | 1 | FDM-printed rigid PLA part |
| Populated Rev1.5.2 PCB | 1 | Final hardware revision; electrical assembly documented separately |
| Selected factory DB9 controller cable | 1 | Must fit the designed strain-relief geometry |
| Optional enclosure fasteners | Up to 5 | **M3** screws; length, head style and engagement must be verified |
| Optional wrist rest | 1 | Black **Bambu Lab TPU 85A**, three-point attachment |
| Auxiliary rubber pad | To confirm | Separate circular geometry; material, quantity and placement not verified |
| Brand/manufacturer label | Optional | Underside label area |

### Printers

- Bambu Lab **X1C**
- Bambu Lab **X2D**
- Bambu Lab **H2S**

These are the project-designated machine names. Check the exact printer model and applicable slicer profile before running a production job.

### Rigid housing filament options

- **Bambu Lab PLA Galaxy**
- **Bambu Lab PLA Basic**
- **Bambu Lab PLA Matte**
- **Bambu Lab PLA Glow**

Any colour combination compatible with the selected print process may be used. The decorated upper housing can use contrasting colours; colour choices do not change the nominal mechanical model.

### Flexible accessory

The wrist rest is intended to be printed separately in **black Bambu Lab TPU 85A**. Use printer/material-specific TPU settings. Confirm the supported material feed path and nozzle requirements with the selected printer. The rigid-housing settings below have **not** been qualified as a TPU preset.

**Build-area check:** The wrist-rest model is approximately **251.84 mm** along its longest STL axis. On machines with a nominal **256 mm** build dimension, this leaves little nominal margin for brim, purge lines or part placement. Confirm the usable area and the complete toolpath in Bambu Studio; machine selection alone does not guarantee that this part will fit.

## Recommended Bambu Studio settings for the rigid housing

The project owner identified these as the **non-default settings worth applying**:

| Bambu Studio parameter | Project-recommended setting |
| --- | --- |
| Seam position | **Back** |
| Wall generator | **Arachne** |
| Wall loops | **3** |
| Bottom shell layers | **5** |
| Bottom paint penetration layers | **5** |
| Sparse infill density | **20%** |
| Sparse infill pattern | **Locked Zag** |

Use these settings for the **PLA upper and lower enclosure parts** as a documented starting point; verify the resulting print against the fitted physical design. **Do not assume they are appropriate for TPU 85A.**

Other parameters, including **nozzle size, layer height, extrusion/bed temperatures, cooling, support usage, print orientation, and PLA Glow nozzle wear considerations**, depend on the chosen printer, filament and tested print profile. Values for these have not been supplied and are deliberately not invented here.

## Before printing

1. Use the **approved sixth-iteration** geometry for both rigid parts. Do not combine revisions.
2. Select printer and filament profiles appropriate to the actual equipment and material batch.
3. Review the top-shell switch openings, mating features, screw locations, PCB supports and DB9 cable retaining clip in the preview.
4. Check that colour painting, support generation and slicing do not damage small snap-fit or wrist-rest engagement features.
5. Print the optional TPU wrist rest as a separate material-specific job.
6. Inspect each part for dimensional and cosmetic issues before fitting electronics.

## Mechanical assembly

### 1. Inspect the printed components

Check the two rigid parts for defects around:

- mating and snap-fit surfaces,
- five M3 fastener locations,
- PCB retaining/support areas,
- switch cut-outs and user-control clearances,
- cable retaining clip and exit opening,
- the wrist-rest connection features,
- and the underside identification area.

For the optional TPU component, inspect all three attachment features and the wrist-contact surface.

### 2. Seat the electronics

1. Identify the correct **Rev1.5.2** PCB and assembled components.
2. Place the PCB in the base against its dedicated locating and support geometry.
3. Confirm a full, stable seating without improvised shims or forcing the board.
4. Confirm mechanical switches can enter the upper-shell openings without side loading.

Electrical soldering, DE-9 pinout verification and functional checks are specified separately in the [controller assembly document](../docs/assembly/ASSEMBLY.md).

### 3. Engage the factory cable strain relief

1. Route the prepared DB9 cable through the designed housing exit.
2. Seat the factory cable into the purpose-built retaining clip beside the termination area.
3. Ensure that cable motion is restrained by the **enclosure geometry**, not the PCB solder joints.
4. Confirm that the cable is not pinched between the two shell halves.
5. Perform a non-destructive normal-handling inspection; do not claim a tested pull-force rating without a controlled test.

### 4. Close the rigid enclosure

1. Align the upper housing and lower base.
2. Engage the snap-fit features evenly, without excessive force.
3. If extra fastening is desired, use the provided **five M3 screw positions**.
4. Select screw length and engagement for the actual printed build; do not assume a nominal M3 diameter determines length or torque.
5. Check the perimeter, switch travel, and access to user controls.

### 5. Attach the optional TPU wrist rest

1. Align the TPU part with the **three matching connection features** in the lower housing.
2. Engage all three points without tearing, twisting or overstretching the TPU.
3. Verify consistent mating and alignment with the controller body.
4. Under normal wrist movement, check for rocking, displacement and separation.
5. Confirm comfortable control access and a natural wrist-contact surface.

The project owner reports that this three-point attachment already fits **securely, without wobble or sliding apart**, and is comfortable in use. Extended wear and repeated attachment have not been formally qualified.

### 6. Rubber pads and branding

A separate small circular rubber-pad model exists, but the final **quantity, installed location, and material** have not been verified. Do not install or specify a fixed number without confirming the production assembly layout.

Apply an identification/brand label in the intended underside location if the chosen build requires one.

## Final mechanical quality checklist

- [ ] Upper and lower shells belong to the finalized sixth iteration
- [ ] Printed surfaces and snap-fit features are intact
- [ ] PCB sits flush and remains securely located
- [ ] Controls are aligned and actuate freely
- [ ] Cable is seated fully in the dedicated retaining feature
- [ ] Cable does not preload or pull directly on soldered joints
- [ ] Snap-fit is completely and evenly engaged
- [ ] All fitted M3 screws have appropriate length and engagement
- [ ] No housing deformation, cracks or trapped conductors
- [ ] Underside branding location is unobstructed
- [ ] Optional wrist rest is engaged at all three points
- [ ] Wrist rest is stable and comfortable under normal handling
- [ ] Any fitted rubber pads match the approved build instructions
- [ ] Final controller electrical and gameplay checks are complete

## Engineering and safety boundaries

The mechanical design is **final** and reported to fit the actual PCB correctly, but this guide does not constitute a laboratory impact qualification, environmental test report or measured cable-force specification. PLA material behaviour can change with heat and printing conditions; choose the print/application environment accordingly.

No printable STL/CAD geometry is distributed with this public document. For measured part envelopes see [Mechanical Reference](MECHANICAL_REFERENCE.md); for component photographs/renders see the [Render Gallery](GALLERY.md).
