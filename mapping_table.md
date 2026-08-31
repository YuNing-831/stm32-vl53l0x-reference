# KiCad -> Altium Mapping Table

This mapping table lists the KiCad symbol/footprint names used in the repository and recommended Altium footprint names (or footprint parameters) to map to after importing the KiCad project into Altium Designer 26. It also includes verification notes you should check in Altium after import.

IMPORTANT: Altium will import KiCad schematic symbols and footprints but will not automatically match to your organization's component libraries. Use this table to speed up mapping; verify pad sizes, pitches and orientation before releasing to CAM.

---

## Recommended mapping (KiCad name -> Altium suggestion / notes)

- U1: `STM32F103VCT6` (KiCad symbol: `STM32F103VCT6`, footprint: `LQFP100:STM32F103VCT6`)
  - Altium suggested footprint: `LQFP-100_14x14mm_P0.5mm` or your company's LQFP100 footprint.
  - Verify: body size (mm), lead pitch 0.5 mm, pad shape (rect vs rounded), thermal pad and exposed pad if present.
  - Pad count: 100. Confirm pin numbering mapping (KiCad -> Altium) after import.

- U2: `TPS62172` (KiCad footprint placeholder: `SOT-23-6:TPS62172`)
  - Altium suggested footprint: `SOT-23-6` or `SON-6` as per actual package used (verify package variant in TPS62172 datasheet).
  - Verify: pad pitch, exposed thermal pad presence/size. Map the regulator pin ordering per datasheet.

- L1: Inductor (if shown) — KiCad generic footprint (e.g., `Inductor_SMD`) → Altium: `L_SMD_1210` or `L_SMD_0805` depending on chosen part.
  - Verify current rating and DCR; choose footprint accordingly.

- C (decoupling): KiCad `C_0603` / `C_0805` → Altium `CAP-0603` / `CAP-0805` (X5R/X7R family)
  - Typical capacitors: 0.1 µF (0603) and 22 µF (0805/1206). Verify footprint pad dimensions for reflow.

- R (resistors): KiCad `R_0603` → Altium `RES-0603` (or your library's 0603 resistor footprint)
  - I2C pullups: 4.7k (0603). XSHUT pullup: 10k (0603).

- J1: `DC_JACK_2.1mm` → Altium: `DC01-2.1` or vendor-specific power jack footprint
  - Verify hole sizes and mounting pads for through-hole jack.

- J2: `VL53_J2_1x6` (KiCad footprint: `PinHeader:PinHeader_1x6_P2.54mm`) → Altium: `PinHeader_1x6_P2.54mm_Horizontal` or `Header-1x6_2.54mm`
  - Verify pin numbering (1..6) and orientation; include silkscreen marker for pin 1.

- SWD header: `SWD_HDR (2x5 2.54mm)` → Altium: `HDR-2X5_2.54mm` or `SWD_10pin`
  - Verify orientation and that NRST and VCC (3.3V) pins are present as in debug cable.

- TP: Testpoints (TP_3V3, TP_GND, TP_SDA, TP_SCL, TP_XSHUT)
  - Map to Altium testpoint footprints: `TP_PAD_1mm` or `TP_3MM_LOOP` depending on test method.

- LED + resistor: KiCad `LED_0805` / `R_0603` → Altium `LED_0805` / `RES-0603`
  - Verify LED polarity marking and silkscreen.

- Crystal: `X1 8MHz HC49` → Altium `Crystal_HC49` or preferred SMD alternative (if using SMD 8MHz resonator use corresponding footprint)
  - If using SMD resonator (no through-hole), map to resonator footprint.

- Power flag / net labels:
  - KiCad power nets (3V3_NET, GND, VIN_9V) will import as nets into Altium. Mark 3V3 as Power Port in Altium and ensure net naming consistency.

---

## Verification checklist after import into Altium

1. Footprint physical dimensions: for MCU (LQFP100) and power regulator (SOT-23-6) verify pad size, body outline, and courtyard against manufacturer datasheet.
2. Pin mapping: open each critical device (MCU, regulator) and cross-check pin numbers to ensure schematic symbol pin ordering matches footprint pins. Reassign mapping if necessary.
3. Pad shapes and solder mask: check exposed pads and mask openings (especially for thermal pad under regulator or MCU).
4. SWD and connector orientation: confirm header pin 1 location and silkscreen marker correctness.
5. Testpoint accessibility: ensure TP placement is not blocked by large components or mechanical features.
6. DRC rules: run design rule check and correct any clearance or net connectivity issues.
7. Power nets: verify decoupling caps are connected to the correct VDD pins and close to pads.

---

## Suggested Altium libraries to create (if none exist)

- `MCU_LQFP100` — LQFP100 footprint with correct pad sizes and courtyard
- `Regulators_SOT23-6` — TPS62172 footprint variant(s)
- `Connectors_2.54mm` — 1x6, 2x5 headers
- `Passive_0603_0805` — resistor/capacitor footprints
- `Testpoints` — pad or loop style footprints

If you want, I can populate the repository with a CSV mapping table of the KiCad symbols to specific Altium library names (example entries). Reply “Add CSV mapping” and I will commit a mapping file that you can use to perform bulk mapping in Altium post-import.

---

Notes
- These recommendations assume common footprints; if your PCB house or assembly process uses different pad sizes or preferred packages, choose those in Altium and update mappings accordingly.
- For the MCU LQFP100 and regulator, always cross-check with the manufacturer's mechanical drawings.

If this table looks good, reply “Commit mapping” and I will add this file to the repository (mapping_table.md already will be committed). If you want the CSV version or an expanded per-pin mapping for the MCU, request “Add CSV mapping” or “Add MCU pin map”.