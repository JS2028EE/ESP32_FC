# Connections and wiring

The [connector CSV](../hardware/revB/Connector_Pin_Map.csv) is the definitive numbered-pad/net/coordinate map, viewed from the component side with the antenna at the top. Confirm pin 1 on the actual board; cable colors and physical plug order are not reliable substitutes.

| Connector | Numbered pins, in order | Purpose |
|---|---|---|
| J1 | USB-C USB 2.0 contacts | Native USB; data only, external board power required |
| J2 | 1 VBAT_RAW; 2 GND | FC battery branch |
| J3 | 1 GND; 2 sensor 3.3 V; 3 SDA; 4 SCL | Sensor I2C expansion |
| J4 | 1 ARM_GATE; 2 GND | Short to force motor outputs disabled |
| J5 | 1 GND; 2 VBAT_RAW; 3 M1; 4 M2; 5 M3; 6 M4; 7 analog current; 8 telemetry | Custom ESC harness |
| J6 | 1 GND; 2 5 V; 3 FC RX; 4 FC TX | Receiver |
| J7 | 1 GND; 2 5 V; 3 FC RX; 4 FC TX | GPS |
| J8 | 1 GND; 2 digital 3.3 V; 3 FC RX0; 4 FC TX0 | UART0 debug |
| J9 | 1 GND; 2 digital 3.3 V; 3 GPIO41; 4 ESC telemetry | Auxiliary breakout |
| J10 | 1 5 V; 2 buzzer switched ground | 5 V active buzzer, at most 30 mA |

TX/RX names use the flight-controller perspective: a peripheral TX connects to FC RX. Receiver/GPS supply is 5 V but serial logic is 3.3 V; the ports are not 5 V tolerant. Check powered-off behavior before attaching independently powered equipment. J9 telemetry is a passive breakout, not a wired MCU UART input.

J2 positive and J5 pin 2 are the same net. Use one FC power feed. Main battery and motor phase wires go directly to the ESC. Read the complete [ESC functional harness map](../hardware/revB/ESC_Wiring.md) before building a cable. The reference ESC's 1 mm connector does not mate with this board's 2.54 mm header. Start with J5 telemetry disconnected and unidirectional DShot300.

The [hardware overview](../hardware/revB/README.md#processor-pin-assignment) lists every GPIO assignment. Battery ADC GPIO1 measures VIN_PROT/16; current ADC GPIO2 measures half the external 0–5 V current signal. USB presence on GPIO16 is active LOW. ARM GPIO21 HIGH enables the buffer; J4 overrides it by pulling the gate low. Boot GPIO0 and GPIO45/46 strap states must be preserved.
