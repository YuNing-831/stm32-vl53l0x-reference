# stm32-vl53l0x-reference

Reference design: STM32F103VCT6 + GY-VL53L0X distance sensor

This repository contains the design notes, schematic sketch, BOM and import instructions to bring the design into Altium Designer 26. It documents the decisions you confirmed:

- Input: 9V DC
- Power conversion: TPS62172 (production-grade SMD synchronous buck, 2A)
- MCU: STM32F103VCT6 (LQFP100)
- Sensor: GY-VL53L0X module (6-pin connector)
- No expansion interfaces reserved

Files in this repository (initial upload):
- README.md (this file)
- schematic_sketch.txt (text version of the schematic and nets)
- BOM_minimal.csv (minimal BOM with recommended parts)
- design_notes.md (layout and implementation notes)
- altium_import_guide.md (step-by-step import + mapping tips for Altium 26)

Next step:
I will now (immediately) generate the full KiCad project (KiCad 7 format) containing:
- Hierarchical schematic (.kicad_sch)
- Schematic symbols folder (.kicad_sym)
- PCB outline / component placement (.kicad_pcb)
- High-resolution schematic PNG export
- BOM CSV (updated)

When the KiCad project files are ready I will upload them into this repository in a separate commit. After that you can follow README instructions to import the KiCad project into Altium Designer 26 using the Import Wizard.

If you want me to upload the KiCad project directly into this repo now, reply "Proceed KiCad upload". Otherwise I'll prepare the KiCad files and upload them in the next message.
