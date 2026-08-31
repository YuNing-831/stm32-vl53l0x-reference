OrCAD Import Instructions for Altium Designer 26

1) Download the OrCAD .DSN file from this repository: stm32-vl53l0x.orcad.dsn
2) In Altium Designer 26: File -> Import Wizard
3) From the "Select Type of Files to Import" list choose: "Orcad and PADS Designs and Libraries Files" (Orcad Designs (*.DSN))
4) Click Next and point the wizard to the downloaded .dsn file
5) Follow the wizard to import schematic and netlist. After import, Altium will create schematic documents and a PCB document based on the DSN information.
6) Mapping footprints: use the orCAD_mapping.csv in this repo as a reference to map parts to your Altium footprints. In the Import Wizard or in the Component Links panel, map the imported parts to Altium footprints.
7) After mapping, run ERC/DRC and visually inspect critical components: STM32 LQFP100, TPS62172 footprint, power rails and I2C connectors.

Notes & Limitations:
- This DSN is a generated placeholder based on the KiCad netlist and component list. Some attributes (footprint pin mapping, detailed symbol attributes) may not be present; you will likely need to reassign footprints for complex parts (MCU/regulator).
- For best results, use the KiCad project import. Use OrCAD DSN if your Import Wizard does not support KiCad directly.

If you want, I can generate a fuller DSN (with more detailed symbol pin mappings and attributes) — reply "Full DSN" and I will produce a more complete OrCAD export suitable for direct import with fewer manual mapping steps.
