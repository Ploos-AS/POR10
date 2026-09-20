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
