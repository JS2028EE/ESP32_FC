# Ordering Rev B bare-board prototypes

Upload **ESP32_FC_RevB_Gerbers.zip**, not a Rev A ZIP, to the PCB manufacturer. The full project ZIP is for editing/review and contains assembly documents as well as manufacturing files. Order a small prototype batch (for example five bare boards), not a production quantity. No order has been placed or paid for.

| Setting | Required selection |
|---|---|
| Material | FR-4 |
| Size | 70 x 65 mm |
| Copper layers | 4 |
| Nominal thickness | 1.6 mm |
| Stackup | JLCPCB JLC04161H-3313, or a manufacturer-confirmed equivalent |
| Outer copper | 1 oz finished |
| Inner copper | 0.5 oz |
| Finish | ENIG, for flat LGA/USB pads |
| Solder mask / legend | Green / white |
| Minimum track / clearance used | 0.15 / 0.15 mm |
| Smallest through drill | 0.20 mm |
| Smallest routed-via land / drill | 0.45 / 0.20 mm |
| Through-via tenting | Both sides where mask permits; do not alter component-pad mask apertures |
| Mounting holes | Four NPTH 3.2 mm holes |
| USB mounting holes | Plated slots; preserve the Excellon routed slots |
| Board outline | Single routed rectangle, no V-scoring or panel rails |
| Assembly service | None; user will solder |
| Optional stencil | Front paste layer, 0.10 mm stainless stencil |

The modeled stack has L1 copper 0.035 mm, 3313 prepreg 0.0994 mm (Er 4.1), L2 copper 0.0152 mm, core 1.265 mm (Er 4.6), L3 copper 0.0152 mm, second 3313 prepreg 0.0994 mm, L4 copper 0.035 mm. Finished nominal thickness includes mask/plating and normal process tolerance. L2 is ground; L3 is 3.3 V plus a few sensor escapes.

Ask the manufacturer to use this stackup and preserve USB routing geometry. The design does not include an impedance coupon or a field-solver report; no certified 90-ohm or USB-compliance result is claimed. If the manufacturer requires a different stackup or copper weight, obtain a revised USB geometry review before accepting that substitution. Do not select two layers or 2 oz outer copper for these files.

The geometry was compared with JLCPCB's published capabilities: 1 oz trace spacing, via diameters/drills, plated slots, ENIG, 1 mm legend and 0.15 mm legend strokes. The manufacturer must still run its normal DFM check on the ZIP. Respond to engineering questions before approving fabrication; a KiCad pass is not an external fabrication acceptance.

The 30.5 mm mounting pattern is offset, not centered. Relative hole coordinates: (34.75,24.75), (65.25,24.75), (34.75,55.25), (65.25,55.25) mm from the top-left. The antenna extends about 6.3 mm above the board. Confirm these dimensions fit the intended frame. Keep metal/carbon away from the antenna.

Gerber contents: four copper layers, two solder-mask layers, two legend layers, front/back paste, outline, PTH and NPTH drills. Paste is for the optional stencil; the manufacturer should not mistake it for copper. Check the online preview shows four copper layers and all holes before paying.

Sources: https://jlcpcb.com/capabilities/pcb-capabilities and https://jlcpcb.com/impedance
