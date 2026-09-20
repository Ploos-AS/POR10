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


## M1.3 supply/bypass capture decision

The receiver supply/bypass topology is now frozen for the next graphical capture step:

- U1.20 VD = `RX_VD`; C4 = 100 nF from RX_VD to GND, placed close to VD.
- U1.21 VA = `RX_VA`; VA remains a distinct external supply rail.
- U1.22 DBYP = `RX_DBYP`; C1 = 22 nF from RX_DBYP to GND, placed close to the receiver.
- RX_VA, RX_VD and RX_DBYP must not be shorted together merely to silence ERC.
- Ground pins remain tied to the common low-impedance ground plane per the M1 architecture.

The actual C1/C4 KiCad symbols and wiring remain a capture task; this decision record prevents ambiguous VA/DBYP interpretation during that edit.


## Corrected U1 coordinate qualification

Commit `00ffd3d` corrected the placed-symbol coordinate mapping against the actual KiCad symbol geometry. CI run 35491987560 parsed the schematic normally and ERC decreased to 27 violations. The corrected power/bypass endpoints are U1.20 VD at (139.70,93.98), U1.21 VA at (139.70,91.44), and U1.22 DBYP at (139.70,88.90). C4 is routed from VD to its 100 nF bypass and C1 from DBYP to its 22 nF bypass. Ground pins 9/10/11/13/14 were likewise remapped to their actual endpoints. This supersedes the earlier coordinate assumptions. Remaining ERC findings are expected capture work and must be reduced incrementally; no blanket ERC waivers.

Next capture gate: 32.768 kHz reference clock X1/C5/C6 on U1.19 RCLK, with the external-RCLK alternative retained as DNP.


## X1 transplant qualification

Commit `ce7c57c` uses a complete KiCad-generated Device:Crystal definition and instance donor rather than a hand-authored crystal structure. CI run 35494261292 successfully parsed and executed ERC with X1 present; the result is **27 violations**, with no KiCad segmentation fault. This validates the transplant method. X1 is currently an unconnected 32.768 kHz placeholder at the RCLK region; electrical wiring and C5/C6 remain the next clock-capture steps.
