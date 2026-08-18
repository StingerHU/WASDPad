# WASDPad Revision 1.5

## Procurement Notes

**Document Version:** 0.9
**Hardware Revision:** 1.5
**Status:** Engineering Validation
**Last Updated:** 2026-08-18

---

# 1. Purpose

This document contains compact sourcing and procurement guidance for WASDPad Revision 1.5.

The authoritative component list remains:

```text
hardware/rev1.5/bom/BOM.csv
```

Approved alternates are maintained in:

```text
hardware/rev1.5/bom/ALTERNATE_PARTS.md
```

---

# 2. Preferred Suppliers

Preferred distributors for semiconductors, protection devices and precision passives:

* Mouser
* DigiKey
* Farnell
* TME
* RS
* LCSC, where manufacturer authenticity is clear

Marketplace sourcing may be used for non-critical mechanical items, but should be avoided for:

* ESD protection
* PPTC devices
* timer ICs
* logic ICs
* MOSFETs
* transistors

---

# 3. Protection Components

The following protection components are production-preferred:

* F2 — Littelfuse `1206L005/30WR`
* D4/D5 — Nexperia `PESD5V0S4UD`
* D6 — Nexperia `PESD6V0L2UU`

These components should be purchased from recognized distributors.

The PTC current class shall not be increased without engineering review.

---

# 4. Core ICs

Primary active components:

* U1 — Renesas `ICM7555CBAZ`
* U2 — Texas Instruments `CD4066BM96`

For new procurement, active lifecycle ordering codes should be preferred over obsolete or legacy variants.

Do not substitute a bipolar NE555 for the ICM7555 without validation.

---

# 5. Resistors and Capacitors

Resistors are standardized on the YAGEO `RC1206FR-07` family where practical.

Key fixed timing values:

```text
R13 = 330 kΩ FAST
R14 = 680 kΩ SLOW
```

These values are functionally validated and must not be changed as a normal procurement substitution.

Preferred capacitor families:

* KEMET `C1206C104J3RACAUTO` — 100 nF
* KEMET `C1206S224J3RACAUTO` — 220 nF

Equivalent X7R parts may be used according to `ALTERNATE_PARTS.md`.

---

# 6. MX Switch System

Primary hot-swap socket:

**Kailh / Kaihua `CPG151101S11`**

Primary gameplay switch:

**Gateron KS-8 Yellow**

Other MX-compatible switches may be used only if mechanical compatibility with the Kailh socket and enclosure is confirmed.

Socket footprint compatibility must not be assumed between different hot-swap socket manufacturers.

---

# 7. LEDs

## D1 Power LED

D1 is customer-selectable:

* Red
* Blue
* White

Approved variants are maintained in `ALTERNATE_PARTS.md`.

## D7 Autofire LED

Primary component:

**Bivar `3BC-3-F`**

The common-cathode configuration is mandatory for the current Rev 1.5 schematic.

Common-anode versions are not drop-in substitutes.

---

# 8. Toggle Switches

Primary physical switch:

**E-Switch `100SP1T1B4M2QE`**

Used for both:

* Autofire OFF / ON
* SLOW / FAST selection

The current KiCad mappings are intentionally retained because they match the validated physical orientation.

Do not standardize or replace the footprints solely for naming consistency.

---

# 9. Controller Cable

Current approved supplier type:

**Generic Sega Mega Drive / Genesis 2 style DB9 female cable**

Current supplier reference:

```text
AliExpress Item ID: 1005009578092300
```

This is an acceptable marketplace-sourced assembly item.

However, wire colours are **not considered a controlled specification**.

For every new supplier batch:

1. verify DB9 pin-to-wire continuity on the first cable
2. confirm +5 V and GND assignments
3. update batch instructions if colour mapping differs

Detailed procedure:

```text
docs/assembly/CABLE_ASSEMBLY.md
```

---

# 10. Lifecycle and Availability

For production-preferred parts, verify:

* active lifecycle status
* manufacturer authenticity
* package availability
* minimum order quantity
* lead time
* second-source availability where practical

Protection devices and core ICs should not rely on a single marketplace source.

---

# 11. Assembly-Specific Procurement Notes

The ICM7555 SOIC-8 package requires controlled solder paste application.

Excess or incompletely reflowed paste has caused supply shorts during prototype assembly.

For production assembly:

* use controlled paste quantity
* inspect U1 after reflow
* verify +5 V-to-GND resistance before power-up

---

# 12. Procurement Priority

Preferred order of use:

1. Primary BOM component
2. Approved alternate
3. Approved variant
4. Engineering-reviewed substitute

Do not use an unverified substitute in production-critical positions.

---

# 13. Version History

| Version | Date           | Status                     | Changes                                                                                                                                                                                            |
| ------- | -------------- | -------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 0.1     | Not recorded   | Draft                      | Initial procurement guidance                                                                                                                                                                       |
| **0.9** | **2026-08-18** | **Engineering Validation** | Updated with finalized Rev 1.5 protection parts, active IC ordering codes, resistor/capacitor standardization, switch/socket strategy, LED variants, cable batch rules and assembly sourcing notes |

---

# 14. Next Version

The next planned version is:

**1.0**

Target milestone:

**Rev 1.5 prototype successfully manufactured and fully validated.**
