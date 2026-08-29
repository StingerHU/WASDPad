# WASDPad+ Rev1.5.1 --- Datasheet Index

Central datasheet and manufacturer-reference index for the WASDPad+
Rev1.5.1 hardware release.

> **Scope:** PCB-mounted electronic and electromechanical components
> used by the Rev1.5.1 design.\
> **Rule:** Manufacturer documentation is preferred. Where a stable
> direct manufacturer PDF was not available, the official
> manufacturer/JLCPCB product page containing the datasheet download is
> linked instead.\
> **Revision:** 2026-08-29

------------------------------------------------------------------------

## 1. Integrated Circuits

### U1 --- CMOS timer

-   **Manufacturer:** Texas Instruments
-   **MPN:** `TLC555CDR`
-   **Function:** CMOS 555 timer / autofire oscillator
-   **Datasheet:** https://www.ti.com/lit/ds/symlink/tlc555.pdf
-   **Product page:** https://www.ti.com/product/TLC555

### U2 --- Quad bilateral switch

-   **Manufacturer:** Texas Instruments
-   **MPN:** `CD4066BM96`
-   **Function:** Quad bilateral CMOS switch / autofire speed selection
-   **Datasheet / product page:**
    https://www.ti.com/product/CD4066B/part-details/CD4066BM96

------------------------------------------------------------------------

## 2. Protection Devices

### D4, D5 --- Quad ESD protection arrays

-   **Manufacturer:** TECH PUBLIC
-   **MPN:** `PESD5V0S4UD`
-   **JLCPCB:** `C2987082`
-   **Package:** SOT-23-6
-   **Function:** 5 V quad-line ESD protection
-   **Datasheet / JLCPCB product page:**
    https://jlcpcb.com/partdetail/TECHPUBLIC-PESD5V0S4UD/C2987082

### D6 --- ESD / TVS protection

-   **Manufacturer:** TECH PUBLIC
-   **MPN:** `TPE0562BC3`
-   **JLCPCB:** `C2841389`
-   **Package:** SOT-323
-   **Function:** 5 V bidirectional ESD / TVS protection
-   **Datasheet / JLCPCB product page:**
    https://jlcpcb.com/partdetail/TECHPUBLIC-TPE0562BC3/C2841389

### F2 --- Resettable PTC fuse

-   **Manufacturer:** Littelfuse
-   **MPN:** `1206L005/30WR`
-   **Series:** 1206L
-   **Function:** +5 V input overcurrent protection
-   **Datasheet:**
    https://www.littelfuse.com/assetdocs/resettable-ptcs-1206l-datasheet

------------------------------------------------------------------------

## 3. Transistors / MOSFETs

### Q1--Q7 --- N-channel MOSFET

-   **Manufacturer:** onsemi
-   **MPN:** `2N7002LT1G`
-   **Package:** SOT-23
-   **Function:** Logic switching / autofire and fire-line control
-   **Datasheet:** https://www.onsemi.com/pdf/datasheet/2n7002l-d.pdf

### Q8, Q9 --- NPN transistor

-   **Manufacturer:** onsemi
-   **MPN:** `MMBT3904LT1G`
-   **Package:** SOT-23
-   **Function:** Red/green status LED drivers
-   **Datasheet:**
    https://www.onsemi.com/pdf/datasheet/mmbt3904lt1-d.pdf

------------------------------------------------------------------------

## 4. Switches and Sockets

### U3 --- Backlight slide switch

-   **Manufacturer:** C&K
-   **MPN:** `PCM12SMTR`
-   **Type:** SPDT SMD slide switch
-   **Function:** Key-backlight enable / disable
-   **Manufacturer/distributor datasheet page:**
    https://eu.mouser.com/en/ProductDetail/CK/PCM12SMTR

### SW1--SW8 --- MX hot-swap sockets

-   **Manufacturer:** Kailh / Kaihua Electronics
-   **MPN:** `CPG151101S11`
-   **Type:** MX-compatible PCB hot-swap socket
-   **Function:** Replaceable Cherry MX / Gateron-compatible key
    switches
-   **Manufacturer reference:**
    https://www.kailhswitch.com/info/kailh-pcb-socket-for-switch-37972215.html
-   **JLCPCB datasheet page:**
    https://jlcpcb.com/partdetail/Kailh-CPG151101S11/C2803348
-   **New-generation related drawing/specification:**
    https://www.kailh.com/product/Ms/rcb/CPG151101S11-16.pdf

### SW_AUTO1 --- Autofire enable switch

-   **Manufacturer:** E-Switch
-   **MPN:** `100SP1T1B4M2QE`
-   **Series:** 100 Series miniature toggle
-   **Function:** Autofire ON/OFF
-   **Manufacturer series / datasheet page:**
    https://www.e-switch.com/product/100-series-miniature-toggle-switch/
-   **Part-specific datasheet page:**
    https://eu.mouser.com/en/ProductDetail/E-Switch/100SP1T1B4M2QE

### SW_SPEED1 --- Autofire speed selector

-   **Manufacturer:** E-Switch
-   **MPN:** `100SP3T1B1M2QEH`
-   **Series:** 100 Series miniature toggle
-   **Type:** SPDT, ON-OFF-ON
-   **Function:** Autofire speed selection
-   **Manufacturer series / datasheet page:**
    https://www.e-switch.com/product/100-series-miniature-toggle-switch/
-   **Part-specific datasheet page:**
    https://www.digikey.com/en/products/detail/e-switch/100SP3T1B1M2QEH/378846

------------------------------------------------------------------------

## 5. LEDs / Optoelectronics

### D1 --- Red 3 mm status LED

-   **Manufacturer:** Bivar
-   **MPN:** `3RD-F`
-   **Type:** 3 mm THT red diffused LED
-   **Datasheet page:**
    https://www.digikey.com/en/products/detail/bivar-inc/3RD-F/3088822

### D7 --- Red/green bi-color status LED

-   **Manufacturer:** Bivar
-   **MPN:** `3BC-3-F`
-   **Type:** 3 mm THT red/green bi-color LED
-   **Function:** Autofire speed/status indication
-   **Product / datasheet page:** https://www.bivar.com/product/3bc-3-f/

### D8--D15 --- Key-backlight LEDs

-   **Manufacturer:** XINGLIGHT
-   **MPN:** `XL-2012WWC`
-   **JLCPCB:** `C965820`
-   **Package:** 0805
-   **Color:** Warm white, 2500--3100 K
-   **Function:** Mechanical-key backlight
-   **Datasheet / JLCPCB product page:**
    https://jlcpcb.com/partdetail/XINGLIGHT-XL2012WWC/C965820

------------------------------------------------------------------------

## 6. Diodes

### D2 --- Small-signal switching diode

-   **MPN:** `1N4148`
-   **Package used:** DO-35 THT
-   **Function:** Autofire / timing logic diode
-   **Note:** `1N4148` is an industry-standard generic part number and
    may be sourced from multiple qualified manufacturers. The actual
    procurement manufacturer should be recorded per production lot.
-   **Reference datasheet (onsemi):**
    https://www.onsemi.com/pdf/datasheet/1n914-d.pdf

------------------------------------------------------------------------

## 7. Capacitors

### C1 --- Timing capacitor

-   **Manufacturer:** Walsin
-   **MPN:** `1206B224K500NT`
-   **Value:** 220 nF
-   **Package:** 1206
-   **Dielectric:** X7R
-   **Rated voltage:** 50 V
-   **Function:** TLC555 autofire timing
-   **Distributor / datasheet search reference:**
    https://www.lcsc.com/search?q=1206B224K500NT

### C2, C3 --- 100 nF capacitors

-   **Manufacturer:** Samsung Electro-Mechanics
-   **MPN:** `CL31B104KBCNNNC`
-   **Value:** 100 nF
-   **Package:** 1206
-   **Dielectric:** X7R
-   **Rated voltage:** 50 V
-   **Manufacturer datasheet / product page:**
    https://product.samsungsem.com/mlcc/CL31B104KBCNNN.do

### VCC-GND-Decoupling1 --- Supply decoupling

-   **Manufacturer:** YAGEO
-   **MPN:** `CC1206KRX7R8BB104`
-   **Value:** 100 nF
-   **Package:** 1206
-   **Dielectric:** X7R
-   **Function:** VCC--GND local decoupling
-   **Manufacturer specsheet:**
    https://www.yageogroup.com/download/specsheet/CC1206KRX7R8BB104

------------------------------------------------------------------------

## 8. Resistors

All listed resistors are **YAGEO RC series, 1206, thick-film, ±1%, 0.25
W** unless otherwise stated.

### 10 kΩ

-   **MPN:** `RC1206FR-0710KL`
-   **Manufacturer specsheet:**
    https://yageogroup.com/component-documentation/download/specsheet/RC1206FR-0710KL

### 330 Ω

-   **MPN:** `RC1206FR-07330RL`
-   **Datasheet page:**
    https://www.digikey.com/en/products/detail/yageo/RC1206FR-07330RL/728822

### 100 kΩ

-   **MPN:** `RC1206FR-07100KL`
-   **Manufacturer specsheet:**
    https://www.yageogroup.com/component-documentation/download/specsheet/RC1206FR-07100KL

### 330 kΩ

-   **MPN:** `RC1206FR-07330KL`
-   **Datasheet page:**
    https://www.digikey.com/en/products/detail/yageo/RC1206FR-07330KL/728823

### 680 kΩ

-   **MPN:** `RC1206FR-07680KL`
-   **Datasheet page:**
    https://www.digikey.com/en/products/detail/yageo/RC1206FR-07680KL/729065

### 270 Ω

-   **MPN:** `RC1206FR-07270RL`
-   **Datasheet page:**
    https://www.digikey.com/en/products/detail/yageo/RC1206FR-07270RL/728734

### 3.3 kΩ

-   **MPN:** `RC1206FR-073K3L`
-   **Datasheet page:**
    https://www.digikey.com/en/products/detail/yageo/RC1206FR-073K3L/731713

### 4.7 kΩ

-   **MPN:** `RC1206FR-074K7L`
-   **Datasheet page:**
    https://www.digikey.com/en/products/detail/yageo/RC1206FR-074K7L/728887

------------------------------------------------------------------------

## 9. Mechanical Key Switches

### Mechanical switches --- 8 positions

-   **Manufacturer:** Gateron
-   **Selected type:** `Gateron KS-8 Yellow`
-   **Interface:** MX-compatible
-   **Installation:** Plugged into Kailh `CPG151101S11` hot-swap sockets
-   **Note:** The hot-swap architecture permits compatible Cherry MX /
    Gateron MX-style switch replacement. The exact fitted
    mechanical-switch variant is therefore a replaceable
    user-serviceable component rather than a permanently soldered
    electrical component.
-   **Manufacturer:** https://www.gateron.com/

------------------------------------------------------------------------

## 10. External Cable / PCB Interface

### DB9 controller cable

-   **Type:** Molded female DB9 cable with flying leads
-   **PCB interface:** J1 solder pads
-   **Note:** This is a procurement/mechanical item rather than an
    active electronic component. The exact cable manufacturer/MPN should
    be recorded in the production BOM once the production cable supplier
    is frozen.

### J1

-   **Type:** PCB solder-pad interface
-   **Status:** PCB feature / DNP
-   **Datasheet:** Not applicable.

------------------------------------------------------------------------

## 11. Documentation and Traceability Notes

1.  This index is intended to accompany the **WASDPad+ Rev1.5.1 Master
    BOM**.
2.  The **MPN in the Master BOM remains the authoritative component
    identity**.
3.  JLCPCB links are used where the selected production component is a
    JLCPCB-stocked replacement and its datasheet is distributed through
    the JLCPCB component database.
4.  Distributor links are used only where they provide stable access to
    the manufacturer's datasheet for the exact MPN.
5.  For compliance review, RoHS/REACH declarations and certificates
    should be stored separately from this datasheet index.
6.  Generic components such as `1N4148`, the DB9 cable, and replaceable
    mechanical key switches require production-lot supplier traceability
    if a specific manufacturer is not frozen in the Master BOM.
7.  This document does **not** by itself constitute product-level CE,
    RoHS, REACH, EMC, safety, or Commodore approval/certification.

------------------------------------------------------------------------

**Project:** WASDPad+\
**Hardware revision:** Rev1.5.1\
**Document:** Datasheet Index\
**Last updated:** 2026-08-29
