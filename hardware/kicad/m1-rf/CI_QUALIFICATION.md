# KiCad CI qualification

POR10 hardware source is checked with KiCad CLI in GitHub Actions.

## Current gates

- report KiCad version
- ensure the project-local Si4735 footprint exists
- run schematic ERC with `--exit-code-violations` when the root schematic exists
- export the schematic to PDF as visual-review evidence
- run PCB DRC when a board exists
- upload generated reports/PDF as workflow artifacts

## Qualification rule

A green workflow without a `.kicad_sch` does **not** mean M1.3 PASS; conditional steps intentionally allow the infrastructure to land before the graphical schematic.

Once `por10-m1-rf.kicad_sch` exists, ERC becomes a mandatory CI gate automatically.

M1.3 PASS additionally requires manual comparison of the exported PDF against the manufacturer reference design and the repository capture checklist.
