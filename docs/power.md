# Power design and protection

The FC accepts 9–25.2 V (3S–6S LiPo) at one battery feed. The chosen reference ESC requires 4S–6S, making 4S the initial reference combination. Battery power passes through the FC branch fuse, Schottky reverse-polarity diode and protected-input network. The 5 V buck supplies the digital 3.3 V buck, sensor LDO and external 5 V loads.

| Rail/load | Initial allocation | Qualification |
|---|---|---|
| Digital 3.3 V | ≤0.70 A | Includes MCU and digital loads |
| Sensor 3.3 V | ≤0.05 A | LDO powered from 5 V, enabled by digital rail |
| External 5 V | ≤0.25 A | Includes buzzer ≤30 mA |
| Upstream 5 V buck | 1 A part rating | All downstream loads share this limit |

These allocations imply about 0.84 A from 5 V at an assumed 85% digital-buck efficiency. They are not measured continuous ratings. The AP63203's 2 A device rating does not bypass the upstream 1 A limit. Measure temperatures and transients at increasing loads before accepting any limit. No motor or VTX supply is provided.

F1 is a 1 A Littelfuse 476 with a published 10 kA interrupt rating at 86 VDC. It protects only the FC branch. D1 is a 100 V Schottky device; D2 has a 28 V standoff rating. Their presence does not establish complete LiPo fault or surge coordination. C6/C7 provide 100 V ceramic bypass, C8 directly bypasses the regulator input, and C27 supplies 47 µF/50 V input damping. Install the ESC manufacturer's bulk capacitor separately at the ESC pads.

Battery measurement is after D1: GPIO1 sees VIN_PROT/16, or 1.575 V at a protected input of 25.2 V. Calibrate diode drop and ADC gain. The ESC current input is limited to 0–5 V and divided by two; calibrate it against measured current rather than copying an unmodified Betaflight scale.

USB cannot power or charge the board. Q3 senses USB VBUS through its gate, with the MCU input pulled up to its own rail; USB presence reads LOW. Begin first power-up with the kill strap fitted and a current-limited bench supply, following the [bring-up procedure](../hardware/revB/Assembly_and_Bringup.md).
