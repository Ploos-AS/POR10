# M1.3 executable KiCad gate

The next qualification evidence must come from KiCad itself, not from hand-authored syntax review.

CI now invokes KiCad CLI against the local footprint before the root schematic is present. When `por10-m1-rf.kicad_sch` lands, ERC and PDF export automatically become mandatory.

## Pass evidence

- workflow uses an identified KiCad version
- project-local footprint is accepted by KiCad CLI
- root schematic is accepted by KiCad
- ERC exits zero
- schematic PDF is generated
- manual reference-design review is recorded

Until those conditions are met, M1.3 remains ACTIVE.
