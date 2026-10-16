# Mechanical design, fabrication and assembly

The PCB is 70 × 65 mm, four layers, nominal 1.6 mm FR-4. Four 3.2 mm NPTH mounting holes form an offset 30.5 mm square. Relative to board top-left, their centers are (34.75,24.75), (65.25,24.75), (34.75,55.25) and (65.25,55.25) mm. Copper exclusions extend 3.5 mm around each center; check washers/standoffs against the 7 mm keepout diameter.

The antenna overhangs the top by about 6.3 mm. Keep conductive frame parts and carbon fiber away from it. C27 is 6.3 mm diameter and 11.2 mm tall; headers and connectors add further height. The bare-board outline is not the assembled envelope. The partial preview lacks some bodies and no STEP assembly is bundled.

Use [Order_Instructions.md](../hardware/revB/Order_Instructions.md) as the fabrication specification and [PCB_Notes.md](../hardware/revB/PCB_Notes.md) for layout details. The requested stack is JLC04161H-3313: 1 oz outer / 0.5 oz inner copper, with layer 2 as ground and layer 3 predominantly digital 3.3 V. Nominal finished thickness is 1.6 mm. The recorded stack has 0.0994 mm 3313 prepreg on each side of a 1.265 mm core. A different manufacturer's substitution requires stack and USB geometry review.

Prototype settings include ENIG, green solder mask, white legend, 0.15 mm track/clearance, 0.20 mm minimum drill and 0.45 mm minimum via diameter. The Gerber package includes 11 layers, a job file and separate PTH/NPTH Excellon drills. There are four plated USB slots and six NPTH holes. Manufacturer DFM acceptance is still required; no controlled-impedance coupon or compliance measurement is included.

This is a bare-board order, normally a small initial batch. A front-side 0.1 mm stencil is optional. LGA sensors and exposed-pad regulators require appropriate paste, hot air/reflow and inspection. Install the radial capacitor and headers after reflow. Follow the [assembly procedure](../hardware/revB/Assembly_and_Bringup.md) and [top assembly PDF](../hardware/revB/Assembly_Top.pdf). The placement CSV is informational, not a reviewed turnkey assembly order. Fifteen references remain on the assembly layer because they do not fit the silkscreen.

Fabrication and shipping prices vary by configuration, address and date. Obtain a live manufacturer quote using the actual ZIP and ordering specification; no supplier quote or delivery commitment is included here.
