Altium Designer 26 - Import KiCad project guide

This guide explains how to import the KiCad project into Altium Designer 26 using the Import Wizard.

1. Prepare the KiCad project folder (after I upload the KiCad files): ensure the following files exist at project root:
   - <project>.kicad_pro
   - <project>.kicad_sch (or .kicad_sch files for each sheet)
   - <project>.kicad_pcb
   - sym/ and fp-lib-table if present

2. In Altium Designer 26:
   - File -> Import Wizard
   - Select "KiCad"
   - Point to the .kicad_pro file or the project folder root
   - Follow the wizard, select schematic(s) and PCB to import
   - After import, check the "Component Links" and "Library Mapping" dialog. Map KiCad symbols to Altium schematic components or create new Altium library components.

3. Library/Footprint mapping tips
   - Altium will import symbols but not automatically provide matching footprints from your local libraries. Create a mapping table: KiCad symbol name -> Altium footprint name.
   - Verify pad sizes and pitch especially for SWD header and MCU LQFP100 footprints.

4. Validation
   - After import, run electrical rule check and visually confirm power nets (3V3, GND) and connectors.
   - Re-run design rule checks (DRC) and update footprints as needed.

If you need, after I add the full KiCad project files I will include a recommended mapping table (KiCad symbol -> Altium footprint) for the parts in the BOM.
