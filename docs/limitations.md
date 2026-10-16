# Limitations and readiness

Rev B has never been built or flown. Zero reported ERC/DRC violations means the saved design passes the configured checks; it does not establish correct regulator behavior, assembly yield, electromagnetic compatibility, reliable software or safe flight.

| Area | Current boundary / remaining work |
|---|---|
| Firmware | None supplied; drivers, estimators, control, receiver protocol, calibration and output timing must be developed. |
| Power | Stability, load steps, startup, brownout, efficiency, thermal performance and input surge/fault coordination remain unmeasured. Capacitor effective capacitance requires bias/temperature review. |
| Motor control | 3.3 V output-only buffer; actual ESC acceptance and timing need bench tests. Bidirectional DShot is unsupported. |
| Failsafes | Reset and the J4 strap disable outputs. There is no independent hardware watchdog to disable outputs when software freezes with ARM high. |
| Sensors | Axis orientation, offsets, vibration, noise, filtering and pressure-port exposure need assembly-specific validation. |
| USB | Full-speed 12 Mbps, battery-powered data only. No measured impedance, compliance or interoperability results. |
| Mechanical | 70 × 65 mm board is larger than many commercial FCs; offset mounting and antenna/capacitor protrusions need a frame fit check. Preview has missing 3D bodies. |
| Environment | No qualified board operating temperature, vibration, water resistance or EMI immunity. The N8R8 module ambient ceiling is 65 °C. |
| Peripherals | No receiver, GPS, ESC, motors, battery, magnetometer or VTX supply included. External UART logic must be compatible with 3.3 V. |
| Manufacturing | Standard DFM acceptance and assembly inspection remain necessary. No production yield or service-life data. |

Keep propellers removed during electrical and ESC tests. Proceed through [staged bring-up](../hardware/revB/Assembly_and_Bringup.md), then measured firmware and failsafe validation before any flight evaluation. This repository does not claim certification or compatibility with an unspecified airframe, motor or propeller.
