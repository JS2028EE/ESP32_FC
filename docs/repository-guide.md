# Repository guide and reproducibility

| Location | Contents |
|---|---|
| `hardware/revB/ESP32_FC.kicad_pro` | KiCad 10 project and design-rule settings |
| `hardware/revB/*.kicad_sch` | Root plus Power, Sensors, Interfaces and Auxiliary sheets |
| `hardware/revB/ESP32_FC.kicad_pcb` | Authoritative editable PCB |
| `hardware/revB/FC_Prototype.pretty/`, `fp-lib-table` | Four local footprints and project-relative library table |
| `hardware/revB/Fabrication/` | Gerbers, drills, maps and job file |
| `hardware/revB/*.csv` | BOM, procurement, placement and connector maps |
| `hardware/revB/*RC.json`, `Design_Audit.json` | Saved validation snapshots |
| `hardware/revB/*.pdf` | Schematic and assembly drawings |
| `downloads/` | Uploadable fabrication archive |
| `docs/` | Project-level explanation and development requirements |
| `SHA256SUMS.json` | SHA-256 of every published file except this manifest |

The hardware folder retains its original local documentation so its internal relative links continue to work. The root README is the public documentation index. The exported netlist's source path has been normalized to avoid including a workstation username; electrical contents are retained. Editor preferences, lock files, backups and obsolete Rev A packages are excluded.

The saved files were checked with KiCad 10.0.7. To reproduce after an edit: open all sheets, run ERC, update the PCB from the schematic, refill zones, run DRC/parity and inspect the board. Re-export Gerbers and separate PTH/NPTH drills with the recorded stack/settings; verify outline, slots and layer count. Regenerate PDFs/BOM/placement outputs and update the checksums and fabrication archive. Compare net connectivity independently for power, straps, sensors, USB and every connector.

The committed reports document the supplied snapshot; GitHub does not run KiCad checks automatically. The original audit-generation scripts and a firmware build system are not included. Opening and saving in another KiCad version can change library references, rules or formatting; review changes rather than treating a successful open as a fresh validation.
