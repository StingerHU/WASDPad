# WASDPad+ Rev1.5.2 - Enclosure and Ergonomics

**Mechanical design:** Dester3D / Sándor Sebesi  
**Compatible electronics:** WASDPad+ Rev1.5.2  
**Rigid enclosure:** FINAL - sixth design iteration, physical fit accepted  
**Optional TPU wrist rest:** Experimental / near-final; three-point fit and comfort evaluated  
**Document revision:** 2.1 (2026-10-19)

![WASDPad+ Rev1.5.2 enclosure presentation based on original design renders](images/wasdpad_enclosure_showcase.jpg)

The WASDPad+ enclosure is a custom, FDM-printable mechanical system developed alongside the Rev1.5 controller electronics. After **six design iterations**, the two-piece rigid housing was finalized for the **Rev1.5.2** board. The design emphasizes a precise PCB fit, secure board retention, cable strain relief, robust construction, and a customizable retro-inspired appearance.

The rigid enclosure is **complete and physically fit-checked**. The separately printed soft wrist rest is functionally comfortable and stable in reported use, but remains an **experimental / near-final accessory** pending longer-term evaluation.

## Mechanical system at a glance

| Feature | Specification or status |
| --- | --- |
| Main enclosure | **Two parts:** upper housing and lower base |
| Design maturity | **Finalized after six iterations** |
| PCB fit | Precisely matched to Rev1.5.2; physically verified by project owner |
| Closure | Snap-fit, with **five optional M3 screw locations** |
| Cable protection | Dedicated retainer / strain-relief feature for the selected factory DB9 cable |
| Product label | Reserved branding / identification area on the underside |
| Appearance | Multicolour-capable; virtually any desired PLA colour combination |
| Rigid materials | Bambu Lab PLA Galaxy, PLA Basic, PLA Matte, PLA Glow |
| Optional wrist rest | Black **Bambu Lab TPU 85A**, three-point mechanical attachment |
| Small auxiliary part | A separate rubber-pad geometry exists; quantity and placement require confirmation |

## Dimensions measured from supplied STL geometry

These values are **individual part bounding boxes**, extracted from the supplied triangle meshes with dimensions interpreted in **millimetres**. They are not toleranced manufacturing drawings.

| Part | X (mm) | Y (mm) | Z (mm) |
| --- | ---: | ---: | ---: |
| Upper housing | **221.75** | **91.15** | **19.40** |
| Lower base | **221.75** | **91.15** | **12.20** |
| TPU wrist rest | **251.84** | **128.50** | **15.00** |
| Small rubber pad | **7.97** | **7.99** | **2.50** |

The two rigid pieces share an approximately **221.75 x 91.15 mm** maximum XY outline. The total assembled height **must not** be calculated by adding the two STL Z extents; the parts have mating/overlapping geometry and are stored in their own model coordinate systems. The assembled enclosure and wrist rest also require a verified assembly orientation before a combined footprint can be stated.

![STL-derived part size overview, showing outer envelope silhouettes](images/wasdpad_dimensions_overview.png)

See [Mechanical Dimensions and Validation](MECHANICAL_REFERENCE.md) for measurement methodology and interpretation limits.

## Final two-piece housing

### Upper housing

The upper part forms the visible controller surface, incorporates the mechanical switch cut-outs, and carries the integrated WASDPad+ graphic. The colour scheme shown in the renders is illustrative: the final geometry can be produced with different filament colour combinations.

![Upper housing exterior](images/wasdpad_top_exterior.jpg)

### Lower base

The lower section supports the populated PCB, provides enclosure mating and fastening features, accommodates the DB9 cable route, and incorporates connection features for the optional wrist rest. An underside area is provided for a manufacturer or brand identification label.

![Lower base interior showing its support geometry](images/wasdpad_bottom_interior.jpg)

### PCB retention and fastening

The case was repeatedly refined until the project owner confirmed that the **Rev1.5.2 PCB seats correctly and remains firmly held in position**, with the gameplay controls properly aligned to their openings.

The two rigid parts are designed to **snap together**. Five **M3 screw positions** offer additional fastening if desired. The actual screw length, screw type, installation method and torque are not specified by the STL geometry alone and must be checked against the printed parts.

### Integrated DB9 cable strain relief

The enclosure has a purpose-made retaining clip at the factory cable exit, close to the soldered cable-harness termination. The selected cable fits this retaining geometry.

During normal handling and accidental pulling, this feature is intended to route mechanical load into the **housing** rather than into the **PCB solder joints**. It reduces the risk of wire movement and a cable pull damaging the termination. No standardized pull-force rating or destructive pull test is claimed.

## Optional black TPU wrist rest

The ergonomic wrist rest is a separate, soft component intended for printing with **Bambu Lab TPU 85A**, in black.

Unlike a loose desk pad, it connects to **three matching attachment locations** on the lower enclosure. The project owner reports that the fitted wrist rest stays aligned, does not wobble, does not shift or slide away during use, and provides a comfortable wrist-contact surface.

Its rounded upper face carries subtle WASDPad branding. The model is **mechanically mature and physically fit-checked**, but its classification remains **experimental / near-final** until extended-use and repeated-attachment durability assessment has been completed.

![TPU wrist rest upper contact surface](images/wasdpad_wrist_rest_top.jpg)

### Small rubber pad

A separate small circular pad geometry was supplied along with the housing and wrist-rest models. Its nominal maximum dimensions are approximately **7.97 x 7.99 x 2.50 mm**. Exact material, intended quantity, and final fitted location have **not** been confirmed from the supplied information and are not asserted as verified here.

## 3D printing overview

**Project-designated printer models:** Bambu Lab **X1C**, **X2D**, and **H2S** (as supplied by the project; profile compatibility should be confirmed for each actual machine).

**Rigid filament options:** Bambu Lab **PLA Galaxy**, **PLA Basic**, **PLA Matte**, and **PLA Glow**. The colours and surface finishes can be mixed and customized independently of the finalized mechanical geometry.

**Soft accessory:** Bambu Lab **TPU 85A**, black, printed as a separate job using a suitable TPU-specific profile.

The documented non-default Bambu Studio settings (for the **rigid housing**, not automatically for TPU) and the mechanical assembly checklist are available in [Printing and Assembly](PRINTING_AND_ASSEMBLY.md).

## Documentation and design views

- [Printing and Mechanical Assembly](PRINTING_AND_ASSEMBLY.md) - materials, Bambu Studio settings, assembly sequence and checks.
- [Render Gallery](GALLERY.md) - six correctly identified exterior/interior and wrist-rest render views.
- [Mechanical Dimensions and Validation](MECHANICAL_REFERENCE.md) - STL-derived measurements, mesh checks and remaining verification items.
- [Rev1.5.2 electrical hardware release record](../hardware/rev1.5/REV1.5.2_MANUFACTURING_RELEASE_NOTES.md) - independent of the mechanical enclosure design.
- [Controller assembly and functional testing](../docs/assembly/ASSEMBLY.md) - electrical and cable verification.

## Validation and publication boundary

**Confirmed by the project owner:** six enclosure iterations; finalized rigid housing; physically accepted PCB positioning; secure snap-fit concept; five M3 positions; integrated cable retainer; stable and comfortable three-point wrist-rest fit.

**Not claimed:** quantified drop/impact certification, standardized cable pull-force rating, measured enclosure tolerances, long-term TPU wear performance, or approval of all possible filament/printer combinations.

The **STL / printable geometry and original mechanical CAD files are intentionally private** and reserved for delivery to **Commodore**, together with the separate private schematic, PCB and Gerber manufacturing files. This public directory contains only textual documentation, derived measurements and design images; it is **not a printable or complete hardware fabrication package**.

**Mechanical modelling and enclosure design credit:** **Dester3D / Sándor Sebesi**.
