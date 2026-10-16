# ESP32-S3 flight-controller bench prototype - Rev B

This is the current editable KiCad 10 project for a 70 x 65 mm, four-layer controller, with an ESP32-S3-WROOM-1-N8R8, BMI088 SPI IMU, BMP280 barometer and a separate 4-in-1 ESC. The FC supply accepts a 3S-6S LiPo (9-25.2 V). Motor current stays on the ESC.

**Order status: prepared for a small bare-board prototype run to Order_Instructions.md.** This is an unbuilt design, not validated flight hardware. KiCad checks and the source/PCB audit pass. The manufacturer still must accept the uploaded fabrication data and requested stackup through its normal DFM process. Physical regulator, USB, sensor and flight validation cannot be completed in software. No flight firmware is included.

Use the Rev B ZIP and Gerbers. The earlier Rev A packages are superseded for this build.

## Open the design

Extract the entire project ZIP. Open ESP32_FC.kicad_pro, then ESP32_FC.kicad_sch or ESP32_FC.kicad_pcb. Keep all five schematic files and FC_Prototype.pretty together. In PCB Editor, Alt+3 opens the native 3D Viewer using installed KiCad 10 model libraries. A separate STEP assembly is not bundled. Some bodies are absent in the preview, including the USB connector and the new fuse; model availability does not affect the fabrication data. PCB_Preview.png is a partial 3D illustration, not an exact assembly envelope check.

## What changed

- Added Q3 and R46: USB VBUS now drives an isolated MOSFET gate. GPIO16 is pulled to the MCU's own 3.3 V rail and reads LOW when USB VBUS is present. USB cannot feed the MCU rail through the previous VBUS sense divider. USB remains data-only; battery power is required.
- Added C27, a real 47uF/50V Panasonic radial electrolytic for input damping. C6/C7 are sourced 2.2uF/100V ceramic bypass capacitors, replacing the unsourced 47uF/50V ceramic requirement.
- Selected Littelfuse 0476001.MR, 1 A, with a documented 10 kA interrupt rating at 86 VDC. Its 2410 lands follow the manufacturer drawing; do not fit the old 1206 fuse. This protects the FC branch, not the motor circuit.
- Selected DMN2056U-7 MOSFETs, with on-resistance specified at low gate voltage, for output gating, buzzer and USB detection.
- Changed R21 to 150k. Battery ADC is VIN_PROT/16; 25.2 V at the protected input gives 1.575 V. Calibrate the diode drop and ADC gain in firmware.
- Shortened regulator bootstrap, bypass and feedback routes; connected C8 directly to U3 VIN/PGND. Recorded a JLC04161H-3313 four-layer stackup.
- Rerouted USB D+/D- from ESD protection to the series resistors on the front layer over the uninterrupted ground plane, removing four vias. Those two sections measure 12.960 and 12.945 mm. USB is full speed, 12 Mbps; this is not 480 Mbps USB high speed. Impedance is not a measured/certified result.
- Completed the BOM with selected component numbers, provided a grouped shopping list and a coordinate-based connector map. Stock/price and authorized distributor availability should be checked when buying; substitutions require matching the actual package and electrical characteristics.
- Applied 1.0 mm text height and 0.15 mm text stroke to printed references. 88 references fit on silkscreen; others remain on the assembly layer. Use Assembly_Top.pdf for placement.

## Processor pin assignment


| Function | ESP32-S3 GPIO | Notes |
|---|---|---|
| Battery ADC | 1 | ADC1; senses protected input after D1 |
| ESC current ADC | 2 | ADC1; 2:1 divider, 0-5 V analog input only |
| Motor 1 / 2 / 3 / 4 | 4 / 5 / 6 / 15 | Through U8 and 33-ohm series resistors |
| Gyro / accel data-ready | 7 / 8 | BMI088 INT3 / INT1 |
| Gyro / accel CS | 9 / 10 | Active low; external 10k pull-ups |
| IMU MOSI / SCK / MISO | 11 / 12 / 13 | Separate from the flash/PSRAM interface |
| USB VBUS sense | 16 | Active-low, isolated by Q3 |
| Receiver TX / RX | 17 / 18 | Flight-controller perspective; remapped UART1 |
| USB D- / D+ | 19 / 20 | 22-ohm series termination and USBLC6 protection |
| Arm output | 21 | HIGH enables motor buffers; LOW disables |
| I2C SDA / SCL | 38 / 39 | 4.7k pull-ups to sensor rail |
| Status LED | 40 | HIGH turns LED on |
| Auxiliary GPIO | 41 | Exposed on J9 |
| Active buzzer | 42 | Drives Q2; external 5 V active buzzer <=30 mA |
| Debug TX / RX | 43 / 44 | UART0; includes boot messages |
| GPS TX / RX | 47 / 48 | Remapped UART2 |
| Boot / voltage straps | 0 / 45 / 46 | Boot pull-up, GPIO45/46 pull-downs |

GPIO3 and GPIO14 are unused. GPIO35/36/37 are reserved. Critical sensor buffers and control code should use internal SRAM; do not depend on PSRAM access latency for the real-time loop. A reasonable initial firmware target is a 1 kHz gyro-triggered loop, subject to measured worst-case latency. Hardware peripherals should generate motor timing. Radio operation, flash writes, USB, and navigation tasks must be qualified for scheduling interference.


## Connectors and ESC

Connector_Pin_Map.csv gives every numbered header pad and its location as viewed from the component side, with the antenna at the top. It is the definitive pad-to-net map. J5 uses 2.54 mm headers, not the 1 mm connector fitted to commercial ESCs. A custom harness is required.

| Connector | Pins in numeric order |
|---|---|
| J2 | battery+, GND; FC branch supply only |
| J3 | GND, sensor 3.3V, SDA, SCL |
| J4 | ARM_GATE, GND; short to force outputs disabled |
| J5 | GND, battery+, motor1, motor2, motor3, motor4, analog current, telemetry breakout |
| J6 | GND, 5V, FC RX, FC TX; receiver |
| J7 | GND, 5V, FC RX, FC TX; GPS |
| J8 | GND, digital 3.3V, FC RX0, FC TX0; debug |
| J9 | GND, digital 3.3V, GPIO41, telemetry breakout |
| J10 | 5V, buzzer low-side drain |

J2 and J5 battery pins are the same node. Use only one FC battery feed. Receiver/GPS supply is 5 V but all MCU serial logic is 3.3 V. Do not connect independently powered serial devices or a 5 V UART adapter without checking powered-off and logic-voltage compatibility. J5 analog current accepts 0-5 V and divides it by two. Telemetry is only a passive breakout to J9, not a configured MCU UART.

The reference ESC is Holybro Tekko32 F4 4in1 50A AM32, SKU31102; see ESC_Wiring.md. It supports **4S-6S**, so use a 4S pack for that reference combination. The FC itself retains its 3S-6S input range; using 3S requires an ESC explicitly rated for 3S. This recommendation does not establish motor/propeller compatibility; motor current requirements must be matched separately.

## Power and firmware limits

The 5 V regulator is rated 1 A; it supplies all downstream rails and peripherals. Initial allocations: digital 3.3 V <=0.70 A, sensor 3.3 V <=0.05 A, external 5 V <=0.25 A including buzzer. They correspond to about 0.84 A from 5 V at 85% digital-buck efficiency. These are design allocations, not measured continuous ratings. Begin bench tests with smaller loads and verify temperature and transients before approaching them. No VTX/air-unit supply is provided. External active buzzer <=30 mA.

The N8R8 module is specified by Espressif for ambient temperatures up to 65 C, which is lower than the 85 C rating of several passive parts. No board temperature operating range is qualified. Avoid inductors heating the sensors/module. Use the barometer without blocking its pressure port.

Q1 and U8 disable motor outputs during MCU reset. J4 is a physical disable strap. A frozen MCU that leaves ARM asserted is not stopped by independent watchdog hardware: firmware must configure watchdog reset, receiver timeout, arming checks, brownout handling and motor timing. Start with unidirectional DShot300 for ESC bring-up; bidirectional DShot is unsupported through U8. No stock Betaflight/PX4/ArduPilot binary is assumed to work on this custom ESP32 board.

## Before applying power

Follow Assembly_and_Bringup.md. Solder paste and hot-air/reflow are required for the LGA sensors and exposed-pad regulator. Observe component moisture/reflow limits. All components mount on the front; C27 and headers are soldered after reflow. The 6.3 mm diameter C27 body is 11.2 mm tall. Inspect soldering and check resistance to ground before using a current-limited bench supply. Fit the kill strap; leave ESC, motors, receiver and GPS disconnected initially.

## References

See Sources.md for manufacturer documents used for this revision, Order_Instructions.md for fabrication settings and Validation.md for the actual checks and their limits.
