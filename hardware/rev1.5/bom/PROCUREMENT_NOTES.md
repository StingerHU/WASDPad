# WASDPad Revision 1.5
## Procurement Notes

Document Version: 0.1

Status: Draft

This document contains sourcing, availability and manufacturing notes for Revision 1.5 components.

---

# General Procurement Principles

Components should preferably be:

- Available from multiple suppliers
- Active and not marked obsolete
- Suitable for long-term production
- Available in small quantities
- Available in production quantities
- Supplied by recognized manufacturers
- Compatible with manual assembly
- Compatible with automated assembly where practical

---

# Preferred Suppliers

Potential suppliers include:

- Mouser
- DigiKey
- Farnell
- TME
- RS
- LCSC

Marketplace-only components should be avoided for safety-critical or protection-related functions unless authenticity can be verified.

---

# Component Categories

## Protection Components

PTC and ESD protection components should be purchased from recognized distributors.

Counterfeit or unverified protection components shall not be used.

## ICM7555 Timer

The selected timer shall be a CMOS 7555-compatible device.

Bipolar NE555 variants shall not be substituted without electrical validation because of their different supply current and switching characteristics.

## MOSFETs

MOSFET substitutions require verification of:

- Pinout
- Gate threshold
- On-resistance
- Leakage current
- Package orientation

## Mechanical Switches

MX-compatible does not always guarantee identical mechanical dimensions.

The following shall be verified:

- Contact pin location
- Plastic alignment pins
- Plate compatibility
- Hot-swap socket compatibility
- Enclosure clearance

## LEDs

LED electrical characteristics shall be checked together with:

- Series resistor values
- Brightness
- Viewing angle
- Polarity
- Package orientation

---

# Lifecycle Management

The BOM should record:

- Manufacturer part number
- Supplier part number
- Lifecycle status
- Approved alternates
- Last verification date

Parts marked obsolete or not recommended for new designs shall be replaced before production release.
