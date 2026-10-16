# Firmware development and validation plan

**There is no firmware in this repository.** The hardware is custom and no stock Betaflight, PX4 or ArduPilot binary is assumed to support it. This document records requirements, not completed implementation or measured performance.

1. Establish repeatable flashing, console, reset and boot-strap behavior. Confirm active-low USB detection and leave ARM low by default.
2. Verify rail sensing and calibrate battery/current ADCs with meters. Implement low-voltage and brownout handling.
3. Implement BMI088 SPI access with separate gyro/accelerometer chip selects and data-ready interrupts. Verify identities, axis mapping, calibration, sampling timestamps and dropped-sample handling. Read BMP280 at an appropriate lower rate.
4. Measure scheduling latency before implementing attitude estimation and control. Start with a 1 kHz gyro-driven loop; keep critical code/data in internal SRAM. Qualify interference from wireless, USB, flash writes, navigation and telemetry before enabling them in flight operation.
5. Generate four motor signals with hardware timing. Begin unidirectional DShot300; check signal voltage and timing on the actual ESC, then consider DShot600 only after measurement. Do not enable bidirectional DShot through U8.
6. Implement explicit arming/disarming, receiver freshness checks, invalid sensor handling, watchdog reset, output limits and a defined reset/brownout response. ARM must remain low until all prerequisites pass. Measure time to stop outputs under each failure case.
7. With propellers removed, verify motor numbering/direction and receiver loss behavior. Log worst-case loop time, jitter, overruns, sensor faults and reset reasons. Establish acceptance thresholds before flight tests.

J4 shorts ARM_GATE to ground and forces output disable. It is useful during development but is not an independent watchdog. A stalled MCU that leaves GPIO21 asserted can keep the buffers enabled until a reset or physical disable. Hardware peripherals may continue output during a CPU fault; evaluate that case explicitly.

Flight performance, stabilization quality, radio range, autonomy and recovery behavior are not claims of this hardware release. Track each validation result with the exact firmware commit, board revision, ESC revision, supply, test setup and measurements.
