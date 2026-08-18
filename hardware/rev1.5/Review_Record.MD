# WASDPad+ Rev 1.5 — Schematic Final Validation Review

**Hardware Revision:** Rev 1.5  
**Review Date:** 2026-08-19  
**Status:** PASS — Release Candidate

This review covers the complete Rev 1.5 schematic after the previous component, BOM, pinout and footprint validation.

---

## 1. Power and Protection

- [x] DE-9 +5 V and GND paths reviewed
- [x] F2 resettable PTC placement reviewed
- [x] D4/D5 signal ESD protection reviewed
- [x] D6 +5 V ESD topology reviewed
- [x] D6: Pin 1 = protected +5 V, Pin 2 = NC, Pin 3 = GND
- [x] Supply decoupling present

**Result:** PASS

---

## 2. Direction Controls

- [x] UP signal path reviewed
- [x] DOWN signal path reviewed
- [x] LEFT signal path reviewed
- [x] RIGHT signal path reviewed
- [x] Independent direction paths retained
- [x] Series resistors present

**Result:** PASS

---

## 3. FIRE1 / FIRE2

- [x] FIRE1 manual path reviewed
- [x] FIRE1 autofire path reviewed
- [x] FIRE1 gating / inversion stages reviewed
- [x] FIRE2 independent signal path reviewed
- [x] No FIRE2 autofire introduced

**Result:** PASS

---

## 4. Autofire Circuit

- [x] ICM7555 timer block reviewed
- [x] CD4066 switching block reviewed
- [x] AUTO OFF / ON control reviewed
- [x] SLOW / FAST selector reviewed
- [x] FAST: R13 = 330 kΩ
- [x] SLOW: R14 = 680 kΩ
- [x] LEFT = SLOW / RIGHT = FAST
- [x] Relevant pull-up / pull-down networks reviewed

**Result:** PASS

---

## 5. Indicators

- [x] D1 power LED circuit reviewed
- [x] D7 dual-colour autofire LED circuit reviewed
- [x] D7 common-cathode topology confirmed
- [x] Q1/Q2 MMBT3904 LED driver stages reviewed
- [x] R22 / R23 current-limiting resistors present

**Result:** PASS

---

## 6. General Schematic Review

- [x] Major signal paths reviewed
- [x] Power connections reviewed
- [x] Ground connections reviewed
- [x] Intentional NC pins marked
- [x] No obvious floating control nodes identified
- [x] No new schematic conflicts identified
- [x] Complete schematic remains consistent with previously validated BOM/component decisions

**Result:** PASS

---

## Final Result

**Rev 1.5 schematic validation: PASS**

No new electrical or schematic issue requiring a design change was identified during the final full-sheet review.

Previously completed BOM, manufacturer pinout and footprint validations were **not unnecessarily repeated** during this review.

The Rev 1.5 schematic can be treated as a **Release Candidate**, subject to normal final ERC, PCB/DRC and manufacturing-output checks.

---

**Reviewed schematic:** WASDPad+ Rev 1.5  
**Validation status:** PASS / RELEASE CANDIDATE
