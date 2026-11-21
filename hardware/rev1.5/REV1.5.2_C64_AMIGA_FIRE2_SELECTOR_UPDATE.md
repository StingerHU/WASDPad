# Rev1.5.2 C64 / Amiga FIRE2 Mode Selector — Engineering Update

**Hardware revision:** WASDPad+ **Rev1.5.2** (unchanged)  
**Engineering update:** 2026-11, integrated FIRE2 electrical mode selector  
**Release status:** Completed; project owner reports a manufactured, fully working switch-equipped controller  
**Validation evidence:** Project-owner confirmation; original per-host measurement logs and private KiCad/Gerber outputs are not part of this public repository  
**Earlier build:** The October 2026 Rev1.5.2 sample without the selector also passed its reported functional tests. These are separate hardware configurations within Rev1.5.2.

## Why a selector is necessary

The **second fire button (FIRE2)** is routed to **DE-9 contact 9**, also used for **POTX**. A single fixed electrical polarity is not suitable for both host families:

- **Amiga mode:** the second button is an **active-low** contact. Pressing FIRE2 must pull contact 9 towards **GND**.
- **C64 / C64GS-compatible mode:** the SID **POTX analogue measurement input** must receive a **positive charging path from +5 V** when FIRE2 is pressed. The original GND-only contact does not provide that transition. On a C64 the game must explicitly read the SID potentiometer input and select the intended joystick port; the controller is not a software driver.

The physical DE-9 plug alone does not identify the host's FIRE2 electrical convention. The user chooses the appropriate position on the small underside hardware switch. The selector is **not** needed for FIRE1 or the four direction inputs.

## Implemented hardware

The switch-equipped Rev1.5.2 preserves both FIRE2 mechanical buttons and their common output, but isolates their former GND connection. The new connections are:

| Ref. | Component / net | Connection and purpose |
| --- | --- | --- |
| **SW7, SW8** | Left and right FIRE2 pushbuttons | One side of each goes to **`FIRE2_COMMON`**; the opposite side joins the output path via **R7** |
| **U4** | C&K **`PCM12SMTR`** SPDT slide switch, PCB underside | **Pin 2:** `FIRE2_COMMON` (common); **pin 1:** GND (Amiga); **pin 3:** R32 to protected +5 V (C64) |
| **R32** | **YAGEO `RC1206JR-072K2L`**, **2.2 kΩ ±5%**, SMD **1206** (nominal code `222`; JLCPCB `C137167`) | Series current-limiting resistor in the **C64-only +5 V branch** |
| **R7** | Existing **330 Ω** series resistor | Between the combined FIRE2 button output and **DE-9 pin 9**, retained in both modes |
| **U3** | Existing `PCM12SMTR` backlight control | Separate switch; **unchanged** |

**Functional connection:**

```text
                         U4 SPDT (common pin 2)
    Protected +5 V -- R32 (2k2) -- pin 3 [C64]
                                      \
                                       -- pin 2 -- FIRE2_COMMON -- SW7 --+
                                      /                           SW8 --+-- R7 (330R) -- DE-9 pin 9 / POTX
                         GND -- pin 1 [AMIGA]
```

SW7 and SW8 are normally open and electrically parallel; pressing either joins the selected U4 common voltage path to R7 and the external FIRE2/POTX line. The FIRE2 button contacts are **not** tied directly to the main GND copper zone in the revised layout. The 5 V source is the protected supply rail, **not** `BACKLIGHT_5V`. FIRE1/autofire and backlight control remain independent.

| Mode | U4 closed contacts | FIRE2 released | FIRE2 pressed | Total intentional series resistance |
| --- | --- | --- | --- | --- |
| **AMIGA / active-low** | 1–2 | High impedance | Contact 9 connected to GND through R7 | **330 Ω** |
| **C64 / active-high** | 2–3 | High impedance | Contact 9 connected towards +5 V through R32 and R7 | **2.53 kΩ** |

Using the ideal 5 V supply, the C64 pressed-state short-circuit-current upper bound is approximately **5 V / 2,530 Ω = 1.98 mA**, excluding switch/contact/supply resistance. This is an explanatory upper bound, not a measured SID discharge current or a guaranteed SID read value. The actual SID POTX result depends on the host and measurement timing.

## Usage and compatibility

1. **Disconnect the controller before switching modes.** Select **C64** for the C64's normal joystick ports; select **AMIGA** for Amiga systems that expect active-low FIRE2.
2. On a C64, software must support the second button on SID POTX (`$D419`); mode switching alone cannot give a game an extra input it does not read.
3. A standard **Protovision 4-player user-port adapter** does **not** transport the normal joystick-port POTX FIRE2 channel. A *custom* extended 4P+ interface may be designed for active-low FIRE2 and would use the **AMIGA / GND** switch position, provided its firmware/game reader explicitly supports it. This does not imply compatibility with the standard adapter.
4. The remaining DE-9 signals (directions, FIRE1, +5 V, GND and pin 5) retain their earlier mapping. The backlight selector is independent of the FIRE2 mode switch.
5. Do not connect the controller to a different host based solely on its connector: confirm that host's actual electrical interface first.

## Verification, release, and traceability

- The project owner confirms the selector-equipped **Rev1.5.2** design has been fabricated and that a **final working example exists**; the reported C64/Amiga FIRE2 functional verification is complete. Original per-host SID register captures, board photographs and test sheets were not supplied with this repository ZIP and are **not fabricated here**.
- The October 2026 pre-selector **Rev1.5.2** full-function validation remains a separate historic result. The November selector implementation belongs to the **same Rev1.5.2 revision**, not a new Rev1.6 release.
- For production, use the exact controlled **post-selector Rev1.5.2** PCB/Gerber/CPL/BOM package. Existing Rev1.5.1 documents and the earlier pre-selector BOM cannot substitute for the current build list.
- The public BOM/compliance workbook includes U4 and R32. **R32 is specified as YAGEO `RC1206JR-072K2L` (2.2 kΩ, ±5%, 1206, 0.25 W; JLCPCB `C137167`)**, in line with the other YAGEO resistors already used in the project. [JLCPCB exact-MPN listing](https://jlcpcb.com/partdetail/YAGEO-RC1206JR072K2L/C137167) / [DigiKey corroboration](https://www.digikey.com/en/products/detail/yageo/RC1206JR-072K2L/729239). **Supply-chain evidence note:** this records the confirmed component family and selected orderable 5% reference, not an independent lot-level check of the resistor physically fitted to the tested sample. The YAGEO RC family RoHS source is listed in the BOM; the manufacturer REACH file requires current-document confirmation. A distributor badge is not a signed component-specific declaration.

**Related:** [System architecture](../../docs/architecture/System_architecture.md), [feature specification](../../docs/specification/FEATURE_SPECIFICATION.md), [assembly and validation](../../docs/assembly/ASSEMBLY.md), [manufacturing release record](REV1.5.2_MANUFACTURING_RELEASE_NOTES.md), and [current BOM documentation](bom/README.md).
