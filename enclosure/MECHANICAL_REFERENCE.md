# WASDPad+ Rev1.5.2 - Mechanical Measurements and Validation

**Source:** Four privately provided STL models for the finalized rigid enclosure and flexible accessories  
**Measurement date:** 2026-10-19  
**Unit interpretation:** Millimetres (STL files do not natively declare units)  
**Method:** Triangle-mesh bounding boxes and mesh-integrity checks

This page publishes selected **derived dimensions and technical metadata only**. It does not distribute any of the private STL geometry, source CAD or production-ready print files.

## 1. Part envelopes (STL XYZ dimensions)

| Model component | X (mm) | Y (mm) | Z (mm) | Notes |
| --- | ---: | ---: | ---: | --- |
| Upper housing | **221.75** | **91.15** | **19.40** | Final rigid upper shell |
| Lower base | **221.75** | **91.15** | **12.20** | Final rigid lower shell |
| TPU wrist rest | **251.84** | **128.50** | **15.00** | Optional soft accessory |
| Circular rubber pad | **7.97** | **7.99** | **2.50** | Auxiliary model; final quantity/material not confirmed |

All values are rounded to **0.01 mm** from the maximum minus minimum XYZ coordinates of the mesh vertices. The source geometry is not necessarily equivalent to an approved tolerance drawing or a physical part measurement.

- The two rigid shell models share an **approximately 221.75 x 91.15 mm** footprint when interpreted in their own coordinates.
- Individual Z extents are **not** the assembled-case thickness. Mating/overlapping regions and assembly positioning must be accounted for.
- The wrist-rest model's bounding rectangle is **not** an assembled-controller footprint without a verified assembly transformation.
- The actual fit and alignment of printed parts depend on print material, shrinkage, slicing and post-processing.

![Illustrated mesh bounding envelopes](images/wasdpad_dimensions_overview.png)

## 2. Model-integrity observations

The supplied STL meshes were inspected programmatically as individual geometric objects.

| Model component | Watertight | Consistent face winding | Mesh bodies | Enclosed solid mesh volume (cm3) |
| --- | --- | --- | ---: | ---: |
| Upper housing | Yes | Yes | 1 | **72.32** |
| Lower base | Yes | Yes | 1 | **47.42** |
| TPU wrist rest | Yes | Yes | 1 | **400.44** |
| Circular rubber pad | Yes | Yes | 1 | **0.11** |

The enclosed mesh volumes describe each modeled **solid**, not the filament consumed by a sliced print. Infill, shell counts, supports, brim, material density and other slicer settings affect actual material usage and printed mass. A watertight mesh also does **not** prove printability on every machine or mechanical compatibility of separately positioned models.

## 3. Design and fit features

| Feature | Source / observed status | Verification boundary |
| --- | --- | --- |
| Six enclosure revisions | Project-owner design history | Final geometry described as sixth iteration |
| Two rigid enclosure parts | Supplied separate models and renders | Upper shell + lower base |
| PCB mounting and switch alignment | Project-owner physical test fit | Reported correct and secure |
| Snap-fit connection | Project-owner confirmation | Finalized design intent; no published force rating |
| Five M3 screw positions | Project-owner confirmation, render features | Screw length, head, insert/engagement and torque not determined |
| Integrated DB9 cable retainer | Project-owner confirmation | Intended to divert cable loads away from solder joints; no measured pull force |
| Brand-label area underneath | Project-owner confirmation | Actual label size and layout not specified |
| Three-point wrist-rest mounting | Project-owner physical fit check | Stable, comfortable; long-term cycling not qualified |
| Rubber-pad installation | Small round STL model supplied | Exact attachment, quantity and material not confirmed |

## 4. Manufacturing status and limitations

The **rigid enclosure is final** and physically accepted for PCB fit, while the **TPU wrist rest is near-final** after successful practical fitting. This page intentionally does **not** assign an IK rating, drop resistance number, impact energy, exact assembled height, thermal rating or tensile load rating.

The supplied models do not establish which TPU wrist-rest profile is validated on which printer, nor do they prescribe layer height, nozzle diameter, print orientation, support strategy, screw length or tightening torque. Any production drawing or new revision should retain the distinction between **STL-derived data** and **physical validation evidence**.

For approved non-default slicer recommendations and final handling checks, see [Printing and Mechanical Assembly](PRINTING_AND_ASSEMBLY.md).

## 5. Items requiring confirmation before a controlled mechanical production handoff

- [ ] Confirm exact M3 fastener specification and installation method for the chosen printed build.
- [ ] Confirm final physical assembled height if a product external-dimension specification is required.
- [ ] Confirm material, intended location and quantity for the circular rubber-pad element.
- [ ] Confirm model-specific Bambu Studio profiles and printable-area clearance for **X1C, X2D and H2S**.
- [ ] Confirm approved TPU-specific slicer settings and any repeated-attachment endurance checks.
- [ ] Record any required label dimensions and artwork outside this public geometric overview.

These open documentation details do **not** reverse the project's reported acceptance of the finalized rigid housing and fully functional Rev1.5.2 electronics.

## Publication boundary

This reference includes no raw STL vertices, topology export, printable model, original CAD file, schematic, PCB layout or Gerber file. The corresponding manufacturing sources are reserved for **Commodore**.

**Mechanical design credit:** Dester3D / Sándor Sebesi.
