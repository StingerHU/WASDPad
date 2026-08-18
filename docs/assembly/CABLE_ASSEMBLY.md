# WASDPad+ Rev 1.5 — DB9 Cable Assembly

## Purpose

This document defines the cable assembly and verification procedure for the
WASDPad+ Rev 1.5 controller.

The currently approved cable is a generic Sega Mega Drive / Genesis 2 style
controller cable with:

- Molded DB9 female connector
- 9 internal conductors
- Flying leads on the PCB side
- Direct solder connection to the WASDPad+ PCB
- 8 conductors used
- DB9 pin 5 unused

Current supplier reference:

- Supplier: AliExpress
- Item ID: `1005009578092300`
- Product URL:
  `https://www.aliexpress.com/item/1005009578092300.html`

> IMPORTANT:
> The wire colors documented below are valid for the cable batch that was
> physically verified during development of WASDPad+ Rev 1.5.
>
> Wire colors MUST NOT be assumed to be identical between different
> production batches or suppliers.


## DB9 Connector Pinout

The WASDPad+ uses the following DB9 signals:

| DB9 Pin | Function |
|--------:|----------|
| 1 | UP |
| 2 | DOWN |
| 3 | LEFT |
| 4 | RIGHT |
| 5 | Not used |
| 6 | FIRE1 |
| 7 | +5V |
| 8 | GND |
| 9 | FIRE2 / POTX |


## Validated Cable Color Mapping

The following mapping was measured on the currently approved cable batch.

| Wire Color | DB9 Pin | Function | WASDPad+ J1 Pad |
|------------|---------:|----------|----------------:|
| Red | 1 | UP | 1 |
| Black | 2 | DOWN | 2 |
| Grey | 3 | LEFT | 3 |
| Orange | 4 | RIGHT | 4 |
| Brown | 5 | Not used | NC |
| Green | 6 | FIRE1 | 6 |
| White | 7 | +5V | 7 |
| Blue | 8 | GND | 8 |
| Yellow | 9 | FIRE2 / POTX | 9 |

The WASDPad+ PCB therefore intentionally does not use J1 pad 5.


## PCB Connection

The cable wires are soldered directly to the J1 solder pads on the PCB.

J1 uses:

`Connector_Wire:SolderWirePad_1x01_SMD_1.5x3mm`

The numbering has intentionally been kept identical to the DB9 connector
numbering wherever possible:

    DB9 pin 1 -> J1 pad 1
    DB9 pin 2 -> J1 pad 2
    DB9 pin 3 -> J1 pad 3
    DB9 pin 4 -> J1 pad 4
    DB9 pin 5 -> NC
    DB9 pin 6 -> J1 pad 6
    DB9 pin 7 -> J1 pad 7
    DB9 pin 8 -> J1 pad 8
    DB9 pin 9 -> J1 pad 9


## Unused Pin 5 Wire

DB9 pin 5 is not used by WASDPad+ Rev 1.5.

On the currently validated cable this conductor is BROWN.

The unused conductor must:

1. NOT be soldered to the PCB.
2. Be cut to a safe length.
3. Have no exposed conductor capable of contacting the PCB or enclosure.
4. Be individually insulated if necessary.

Do not connect DB9 pin 5 to GND, +5V or any other WASDPad+ signal.


## Mandatory New-Batch Verification

### DO NOT RELY ON WIRE COLOR ALONE

Generic controller cables may be manufactured by different factories or
changed without notice.

A cable that looks externally identical may use a different internal wire
color assignment.

Therefore:

**The first cable from every new supplier batch MUST be verified with a
multimeter before production assembly begins.**

Perform a continuity test between every DB9 contact and its corresponding
wire.


## Required Continuity Test

Verify all nine conductors:

| DB9 Pin | Expected Color* | Expected Function |
|--------:|-----------------|-------------------|
| 1 | Red | UP |
| 2 | Black | DOWN |
| 3 | Grey | LEFT |
| 4 | Orange | RIGHT |
| 5 | Brown | NC |
| 6 | Green | FIRE1 |
| 7 | White | +5V |
| 8 | Blue | GND |
| 9 | Yellow | FIRE2 / POTX |

`* Expected Color` refers only to the currently validated supplier batch.

If ANY wire color differs:

**STOP ASSEMBLY.**

Measure the complete DB9 pin-to-wire mapping and update the production
instructions for that cable batch before continuing.


## Critical Power Verification

Before connecting an assembled controller to a Commodore computer, verify:

    DB9 pin 7 -> J1 pad 7 -> +5V
    DB9 pin 8 -> J1 pad 8 -> GND

There must be NO continuity between +5V and GND.

This check is mandatory because an incorrectly wired power conductor could
damage the controller or the connected computer.


## Final Assembly Verification

After soldering the cable to the PCB:

1. Inspect all J1 solder joints.
2. Check for solder bridges.
3. Verify DB9 pin 1 -> J1 pad 1.
4. Verify DB9 pin 2 -> J1 pad 2.
5. Verify DB9 pin 3 -> J1 pad 3.
6. Verify DB9 pin 4 -> J1 pad 4.
7. Verify DB9 pin 5 is NOT connected.
8. Verify DB9 pin 6 -> J1 pad 6.
9. Verify DB9 pin 7 -> J1 pad 7.
10. Verify DB9 pin 8 -> J1 pad 8.
11. Verify DB9 pin 9 -> J1 pad 9.
12. Verify no short circuit exists between +5V and GND.
13. Verify the unused pin-5 conductor is safely insulated.


## Production Rule

A cable supplier part number or product listing does NOT by itself qualify a
cable batch for production.

Production approval requires:

- Mechanical compatibility
- DB9 female connector
- Nine conductors
- Verified pin-to-wire mapping
- Verified +5V and GND assignment
- Successful continuity test
- No shorts between adjacent DB9 pins or PCB pads

Once verified, the measured color mapping may be used for the remainder of
that specific production batch.


## Revision

Document applies to:

**WASDPad+ Rev 1.5**

Cable mapping initially validated using the generic AliExpress
Mega Drive / Genesis 2 style controller cable listed above.
