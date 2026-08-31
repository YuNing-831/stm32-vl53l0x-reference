Design notes and PCB layout guidance

1. Power supply
- TPS62172 is the selected SMD synchronous buck (2A). Follow TI reference layout for minimal EMI. Place input capacitor (>= 47uF low ESR) close to VIN pin and keep short traces between regulator, inductor and capacitors.
- Provide a solid ground plane. Route the high di/dt loop (switch node, inductor, input and output caps) as compact as possible.
- Add a Ferrite bead or filter if the upstream 9V source is noisy.

2. MCU decoupling and clocks
- Place 0.1uF decoupling capacitors next to each VDD pin. Add a 10uF or 22uF main cap near the MCU power entry.
- If precise timing needed, use external 8MHz crystal with recommended load caps (18pF) per ST datasheet.

3. VL53 placement
- Place the VL53 module away from the switching inductor and noisy traces. If using a bare VL53L0X die (not the module), ensure optical window cutout and shielding per ST optical guide.
- Keep I2C lines short. If they must be longer than ~10 cm, reduce pullup to 2.2k and consider series resistors (22-47 ohm) close to MCU.

4. Connectors and test points
- Expose TP_3V3, TP_GND, TP_SDA, TP_SCL, TP_XSHUT for debugging.
- SWD header (2x5) should be placed at board edge for easy access.

5. EMC considerations
- Keep analog/VDDA area separate and provide quiet routing. If ADC used, add RC filter to ADC inputs.
- If EMI observed, add common-mode choke and additional LC filtering on 3.3V rail to the sensor.
