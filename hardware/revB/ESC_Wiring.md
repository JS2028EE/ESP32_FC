# Reference ESC and functional harness map

Reference: Holybro Tekko32 F4 4in1 50A AM32, SKU31102, product page https://holybro.com/products/tekko32-f4-4in1-50a-esc . The manufacturer lists 4-6S input, DShot150/300/600/1200, analog current sensing, no BEC and 30.5 mm mounting. Use a **4S battery** as the initial reference combination; this ESC is not a 3S recommendation. Recheck the purchased board revision and its supplied pin map.

Use the included ESC pigtail and terminate it in a correctly numbered 2.54 mm female housing for FC J5. The connectors are different sizes. Wire by the manufacturer's signal labels, not by cable color or an assumed left-to-right plug order. The pin-map image is on the product page. Connector_Pin_Map.csv describes the actual FC pad coordinates from the component side.

| FC J5 pin | Connect to the ESC signal labeled |
|---|---|
| 1 | GND |
| 2 | BAT/VBAT positive, only if this is the single FC power feed |
| 3 | S1 / motor control 1 |
| 4 | S2 / motor control 2 |
| 5 | S3 / motor control 3 |
| 6 | S4 / motor control 4 |
| 7 | CUR / analog current output (0-5 V maximum) |
| 8 | Leave disconnected for initial bring-up; telemetry only breaks out to J9 |

Alternatively power the FC separately at J2 from the same battery branch and leave J5 pin 2 unconnected. Never parallel separate supplies. The main battery/XT60 and motor phase wires connect directly to the ESC, not through this flight controller. Install the ESC's supplied bulk capacitor at its power pads according to the ESC manufacturer. The FC's C27 is not a substitute for that ESC capacitor.

The FC sends 3.3 V, output-only motor signals. Start unidirectional DShot300, then qualify DShot600 with a scope and the actual ESC; do not enable bidirectional DShot. Validate the purchased ESC's signal input compatibility during bench bring-up before connecting motors. The ESC's 50 A rating is not a recommendation for any unspecified motor or propeller.

For current sensing, the published Betaflight scale depends on PCB revision (V1.5-V1.7:168; V1.8:110; V1.9/V1.9T:120). Source: https://docs.holybro.com/esc/current-sensor-scale . This custom board adds a 2:1 analog divider, so firmware must account for that divider and calibrate against a meter; do not copy a Betaflight scale unchanged.

After wiring, check continuity end-to-end on every signal and verify neither BAT nor motor phase pads reach an MCU/signal pin. Test first with a current-limited supply and propellers removed. Use firmware motor numbering/orientation calibration before any flight.
