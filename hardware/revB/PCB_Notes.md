# Rev B PCB notes

70 x 65 mm nominal, 1.6 mm four-layer FR-4. L1 components/signals/power and ground fill; L2 ground plane with no signal tracks; L3 digital 3.3 V and a few sensor escapes; L4 signals and ground fill. Requested stackup is JLC04161H-3313 with 1 oz outer / 0.5 oz inner copper. See Order_Instructions.md.

Four NPTH 3.2 mm mounting holes on an offset 30.5 mm square: (34.75,24.75), (65.25,24.75), (34.75,55.25), (65.25,55.25) mm relative to top-left. Copper/track/via exclusion radius is 3.5 mm around each. Antenna overhang is about 6.3 mm above the board; assembled envelope exceeds the bare outline. C27 is 6.3 mm diameter and 11.2 mm tall. Verify the entire frame/stack envelope before ordering.

All 103 electrical/wire-connection references are on the front; four extra mounting holes are board-only. Custom local footprints are the module, USB connector and BMP280 with cleared edge silkscreen, plus the new Littelfuse 476 lands. The fuse land dimensions are 1.96 x3.15 mm at +/-2.45 mm; body 6.1 x2.69 mm. Copper/holes of the three original footprints remain based on KiCad libraries.

Minimum copper clearance/width is 0.15 mm. Most vias are 0.6/0.3 mm; selected escapes are 0.45/0.2 mm. The signal rule settings do not represent a regulator power rating. The new direct regulator input, ground and switch routes are reviewed against datasheet layout guidance, but switching stability, thermal limits and EMI must be measured on prototypes.

USB ESD-to-series-resistor sections are now entirely on F.Cu over L2 ground, with no vias and 0.015 mm length difference for those sections. Connector fanout retains short crossover vias. This is a full-speed prototype layout; no impedance coupon, 3D field solver or compliance measurement has been performed. Match the requested stackup and qualify USB on the assembled boards.

88 reference fields fit on silkscreen at 1.0 mm text / 0.15 mm stroke. Use the assembly drawing for the remaining references and all polarity/pin-1 checks. Filled/capped via-in-pad processing is not included in the basic bare-board specification; inspect thermal-pad soldering when hand-reflowing the official exposed-pad footprints.

Fabrication files are for a small unassembled prototype run. The current release has no KiCad errors, unconnected items or parity issues. Manufacturer DFM acceptance, assembly inspection, power/sensor tests and flight firmware/failsafe qualification remain physical validation steps.
