# Validation - Rev B prototype

Checked with KiCad 10.0.7 on 2026-10-15.

- PCB DRC: 0 reported violations; 0 unrouted/unconnected items; 0 schematic-parity discrepancies.
- Schematic ERC: 0 reported violations across all five sheets.
- Independently compared 329 schematic pin-to-net assignments against matching PCB pads, including new USB detector and input capacitor.
- 103 schematic/wire-connection references, four board-only mounting holes, four copper layers. Every BOM row has a selected MPN or explicit wire-connection designation. All assigned footprint library files resolve.
- 1470 track segments, 194 routed vias; no signal tracks on the layer-2 ground plane.
- Verified the new fuse lands against the manufacturer dimensions; verified new capacitor polarization/net assignment. These are design-file checks, not inspection of manufactured parts.
- Exported 11 Gerber layers, separate PTH/NPTH Excellon files and maps. Independently checked outline dimensions 70 x65 mm, four USB plated routed slots, six NPTH holes including the four M3 mounts, and nonempty files.
- Placement CSV contains 102 entries; J2 is a manual wire connection and is excluded. Placement is informational because the requested order is bare boards.
- Re-rendered and visually checked all five schematic pages, the assembly drawing and the partial 3D preview. The assembly-only drawing copy adds leaders and removes duplicate internal labels without changing the manufacturing board.
- Compared chosen geometry with the published JLCPCB capability page and recorded JLC04161H-3313 stackup. This does not represent manufacturer DFM acceptance or an impedance guarantee.

No DRC/ERC exclusions were added to hide findings. ERC default ignored check categories and DRC default severities are visible in the JSON reports. Final rules include 0.15 mm copper width/clearance, 0.20 mm minimum drill, 0.45 mm minimum via diameter, 0.10 mm solder-mask web and 1.0/0.15 mm printed text size/stroke. The 15 references not fitting silkscreen remain on the assembly layer.

## Release boundary

Prepared for a small bare-board **prototype** fabrication run following Order_Instructions.md and the manufacturer's ordinary DFM acceptance. No physical PCB has been built or tested. Regulator stability, capacitor effective capacitance across actual bias/temperature, load-step/thermal behavior, input surge/fault coordination, USB interoperability/impedance, sensor noise and actual ESC signal compatibility still require bench validation. No firmware or flight/failsafe validation has been performed. These files are not a flight-qualified or production-qualified design.

Datasheet-derived choices and references are recorded in README.md / Sources.md. Use Assembly_and_Bringup.md after assembly and ESC_Wiring.md when selecting/building the harness. The reference Holybro ESC needs 4S-6S, although the FC input supports 3S-6S.
