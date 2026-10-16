# Change log

## Rev B — design snapshot checked 2026-10-15

- Replaced the USB VBUS divider with an isolated Q3 detector and MCU-rail pull-up; sense is active low.
- Selected a properly specified 2410 Littelfuse FC branch fuse, low-gate-voltage MOSFETs, sourced input ceramics and a real 47 µF/50 V radial damping capacitor.
- Changed the battery divider to VIN_PROT/16 and shortened regulator critical routes.
- Recorded the four-layer stack and rerouted the USB ESD-to-resistor sections over ground without vias.
- Completed purchasing part numbers, connector pad map, assembly drawing, fabrication exports and saved checks.

## GitHub documentation — 2026-10-16

Published the Rev B design with architecture, power, connections, procurement, manufacturing, firmware requirements, limitations, sources and contribution guidance. Normalized the exported netlist source path and regenerated a public checksum manifest. No electrical redesign or new physical validation was performed during documentation publication.

## Rev A — superseded

Earlier prototype packages are not the current fabrication source. Use Rev B consistently; do not mix its BOM or fuse footprint with Rev A manufacturing files.
