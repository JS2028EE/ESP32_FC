# Components and procurement

Use the [per-reference BOM](../hardware/revB/BOM.csv) for values, packages and selected part numbers. The [shopping list](../hardware/revB/Shopping_List.csv) groups 43 purchasing entries covering 102 fitted parts. The 103rd schematic entry, J2, is a manual wire connection. Four mounting holes are board-only objects. Buy assembly spares, especially for small passives and sensors.

| Function | Selected component |
|---|---|
| MCU/module | ESP32-S3-WROOM-1-N8R8 |
| Inertial sensor | Bosch BMI088 |
| Barometer | Bosch BMP280 |
| Battery-to-5 V regulator | TI LMR36510ADDAR, 65 V / 1 A, 400 kHz |
| Digital 3.3 V regulator | Diodes AP63203WU-7 |
| Sensor 3.3 V regulator | TI TLV75533PDBVR |
| Motor-output buffer | TI SN74LVC125APWR |
| MOSFETs Q1/Q2/Q3 | Diodes DMN2056U-7, SOT-23 G1/S2/D3 |
| FC branch fuse F1 | Littelfuse 0476001.MR, 1 A, 2410 |
| Reverse polarity diode D1 | SS310-13-F |
| Input TVS D2 | SMBJ28A-13-F |
| Input damping capacitor C27 | Panasonic EEUFR1H470, 47 µF / 50 V radial |
| 5 V inductor L1 | Bourns SRP6060FA-220M, 22 µH |
| Digital buck inductor L2 | Bourns SRP5030T-4R7M, 4.7 µH |

The complete BOM controls procurement; this table is an orientation guide. Verify exact suffix, dimensions, land pattern, pinout, voltage rating, DC-bias capacitance, temperature behavior and regulator requirements before substituting. A nominal capacitance match alone is insufficient. F1 must fit the new 2410 lands; the old Rev A 1206 fuse is unsuitable.

The external reference ESC is Holybro Tekko32 F4 4in1 50A AM32, SKU31102. It requires 4S–6S and a custom harness. Select motors/propellers against their actual current and voltage requirements; the ESC's advertised 50 A rating does not select a motor automatically. Receiver, GPS, active buzzer, battery, frame, wiring and mounting hardware are separate purchases.

Stock, prices and distributor authenticity have not been guaranteed. Manufacturer source links are collected in [Sources.md](../hardware/revB/Sources.md). No assembled-PCB purchase is specified: this project assumes bare boards and user assembly with hot air/reflow equipment.
