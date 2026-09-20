# M1.3 schematic capture status

## Completed

- [x] manufacturer D60 pin map verified
- [x] manufacturer reference values recorded
- [x] SSOP mechanical package dimensions verified
- [x] project-local 0.635 mm footprint created
- [x] project-local U1 symbol created
- [x] library tables created
- [x] receiver wiring manifest frozen
- [x] sheet partition frozen

## Pending executable KiCad validation

- [ ] graphical `.kicad_sch` parsed by KiCad
- [ ] ERC run
- [x] footprint library parsed by KiCad 9.0.9 in GitHub Actions (run 35488973246, commit `e8c5f20`)
- [ ] DRC/footprint checks
- [ ] schematic visual review

## CI evidence

- KiCad: 9.0.9
- Workflow run: 35488973246
- Commit: `e8c5f204d3a7481298e4aba4c339bf395f7baf21`
- Result: PASS for project-local footprint-library parsing
- This does not yet qualify the physical 1:1 land pattern or M1.3 as a whole.

## Important

The repository now contains enough design information to reproduce the receiver sheet without inventing connectivity. M1.3 remains **ACTIVE**, because a hand-written KiCad S-expression that has not been opened by KiCad is not treated as a qualified schematic.

The next implementation step must use KiCad itself (GUI or CLI) to create/normalize the schematic and run ERC. Qualification evidence should include the KiCad version and ERC output.


## First populated-schematic ERC — run 35490529239

Commit `fdd28098bc9d835d92d48b8d58fbe7a248cab37c` removed the KiCad crash and produced the first real ERC report with U1 placed.

Result: **35 errors, 0 warnings**. These are expected connectivity errors from the intentionally unconnected receiver symbol, not parser failures.

Breakdown:
- unconnected signal/control/audio/RF pins,
- undriven FMI/AMI/RCLK/SCLK/SEN/RST inputs,
- undriven VA/VD/RFGND/GND power pins,
- unconnected DBYP.

This establishes the next capture order: ground and supply/DBYP first, then 32.768 kHz clock, control, RF and audio. Do not waive these ERC errors globally; remove them by actual schematic connectivity or explicit intentional no-connect treatment.
