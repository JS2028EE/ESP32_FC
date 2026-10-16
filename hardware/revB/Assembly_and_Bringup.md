# Rev B assembly and first power-up

This plan is for bench validation of the first prototypes. It is not a record of tests already performed. No flight firmware or powered hardware test results are included.

## Assemble

1. Use BOM.csv / Shopping_List.csv and Assembly_Top.pdf together. Do not substitute similarly named packages without comparing dimensions and pin numbering. U8 must be SN74LVC125APWR, not an LS125. Q1-Q3 are DMN2056U-7 despite the compatible generic transistor drawing. Fit R21=150k and the new 2410 fuse.
2. Reflow the front-side SMD components with a front stencil. The BMI088/BMP280 have pads underneath; U3 requires a soldered ground/thermal pad. Follow each component's moisture and reflow instructions. Do not cover the barometer pressure port with flux, conformal coating or tape.
3. Inspect the sensor LGA joints and regulator thermal-pad soldering with appropriate inspection equipment; electrical continuity alone does not prove every hidden joint is sound. Inspect USB contacts for bridges.
4. Solder headers and C27 after reflow. C27 pin 1 is positive VIN_PROT; pin 2 is ground/negative. The stripe on the capacitor marks negative. D1/D2 cathode bars, LED polarity and Q/IC pin 1 must match the assembly drawing and component datasheets.
5. Use insulating M3 standoffs/washer diameters <=7 mm, keeping copper/antenna clear of the frame. Fix C27 mechanically if vibration is expected, without blocking the pressure sensor.

## Power rails first

1. With no supply, check for solder bridges and unexpectedly low resistance from VIN_PROT, 5 V, digital 3.3 V and sensor 3.3 V to GND. Capacitors will charge during the measurement, so a resistance reading alone is not a complete acceptance test.
2. Fit J4's kill strap. Leave USB, ESC, receiver, GPS and buzzer disconnected. For staged assembly, first verify the regulator sections before fitting the processor/sensors; no-load regulator testing can use a low current limit.
3. Use a current-limited bench supply at J2, correct polarity. With all parts fitted, begin at 12 V and about 0.15 A current limit. If it limits or repeatedly resets, disconnect and investigate before raising the limit; do not substitute a LiPo to force startup. The ESP32 may require more current during startup/radio bursts, so a current-limit event is not by itself proof of a short.
4. Check approximately 5.03 V, digital 3.3 V and sensor 3.3 V at the corresponding connector/capacitor pads. Investigate rails outside device operating limits before proceeding. Scope startup, ripple and overshoot. Use short probe grounds. Check for heating.
5. With controlled dummy loads, gradually exercise the documented power allocations and input range (9-25.2 V) while measuring rail transients and temperatures. Qualify the 6S hot-plug/transient behavior separately with suitable equipment; these files do not establish surge immunity. Reverse-polarity/fault tests require a deliberately current-limited setup, not a direct battery short.

## Controller and interfaces

1. Connect USB after the rails pass. For download, hold BOOT, tap RESET, release BOOT. USB is data-only and needs board power. Verify GPIO16 LOW with USB present, HIGH when absent. Check USB enumeration and attach/detach over repeated power cycles. UART0 on J8 is an alternative 3.3 V programming/debug interface; never feed 5 V logic into it.
2. Use a diagnostic firmware build to check the exact module's flash/PSRAM configuration. Do not use GPIO35/36/37. Confirm brownout and watchdog reset behavior and ensure GPIO21 stays LOW until deliberate arming.
3. Read BMI088 accel ID 0x1E and gyro ID 0x0F; BMP280 ID 0x58. Follow Bosch's SPI-selection, startup and dummy-byte rules. Record the actual package-to-airframe axes and calibrate the sensors. A forward marking alone does not configure firmware axes.
4. Calibrate battery ADC: protected input = ADC pin voltage x16; correct the series-diode drop for battery voltage. Current ADC voltage = ESC current-output voltage /2. Use a meter/reference load to calibrate both channels.
5. Check motor outputs with a logic analyzer while the ESC is disconnected. They must remain LOW during reset, boot, watchdog recovery and kill-strap assertion. Validate pulse timing at the connectors and deliberately exercise lost-receiver/failsafe cases. A frozen MCU with ARM high needs watchdog reset; there is no independent external watchdog.
6. Remove the kill strap only for deliberate motor tests. Connect the checked ESC harness; keep propellers removed. Qualify DShot300 and later DShot600, motor order/direction, sensor axes, receiver timeout and emergency shutdown. Test radio/USB/flash operations for timing interference. No propeller-on test should precede those checks.

Log voltages, ripple, load, temperature, sensor IDs, firmware version and failures. Flight evaluation is a separate controlled hardware/firmware validation step, not part of bare-board fabrication acceptance.
