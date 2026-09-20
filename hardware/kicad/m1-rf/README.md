# POR10 M1 RF KiCad Design

This directory is the hardware-design workspace for the POR10 M1 receiver prototype.

## Capture status

**M1.3: capture preparation complete; schematic capture active.**

The verified Si4735-D60 SSOP pin map is maintained in:

`../../rf/SI4735_D60_SSOP_PINMAP.md`

The capture rules and review gates are in:

`../../rf/M1_3_SCHEMATIC_SPEC.md`

## Sheet plan

| Sheet | Purpose |
|---|---|
| `receiver` | Si4735-D60, mandatory bypass/reference circuitry |
| `rf_inputs` | separate FMI and AMI prototype paths |
| `control_audio` | I2C/reset/GPO and analog audio breakout |
| `power_test` | clean prototype power entry and measurement points |

## Baseline population

M1 Q1 must remain deliberately minimal:
- Si4735-D60 SSOP
- mandatory reference/bypass parts
- separate FM and AM-family inputs
- control header
- analog audio breakout
- measurement points

Not populated in Q1:
- LNA
- automatic antenna switch
- filter bank
- final speaker amplifier
- final battery/power converter

## Capture rule

No unverified component value is promoted from a placeholder to a production value merely to make ERC pass. Every datasheet-derived value must be traceable in the review record.
