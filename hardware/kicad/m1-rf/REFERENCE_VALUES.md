# POR10 M1.3 — Si4735-D60 Reference Values

Source: Skyworks/Silicon Labs Si4730/31/34/35-D60 datasheet, Rev. 1.2, SSOP typical application and QFN/SSOP BOM.

## Frozen manufacturer reference values

| Ref | Value | Function | M1 baseline |
|---|---|---|---|
| C1 | 22 nF ±20%, Z5U/X7R | supply/DBYP bypass | POP |
| C2 | 1 nF ±20%, Z5U/X7R | FM antenna coupling | POP for manufacturer-reference FM path |
| C3 | 0.47 uF ±20%, Z5U/X7R | coupling in reference antenna network | topology-dependent |
| C4 | 100 nF ±10%, Z5U/X7R | VD supply bypass | POP |
| C5 | 22 pF ±5%, C0G | optional crystal load | POP only with crystal |
| C6 | 22 pF ±5%, C0G | optional crystal load | POP only with crystal |
| C9 | 2–5 pF | optional digital-audio noise mitigation | DNP baseline |
| R1 | 600 ohm | optional digital audio | DNP baseline |
| R2 | 2 kohm | optional digital audio | DNP baseline |
| R3 | 2 kohm | optional digital audio | DNP baseline |
| L1 | 180–450 uH ferrite loop stick | ferrite AM antenna | external experiment |
| L2 | 10–20 uH air loop | optional AM input | DNP baseline |
| T1 | 1:5 turns transformer | optional AM input | DNP baseline |
| X1 | 32.768 kHz crystal | optional crystal oscillator | selected M1 clock candidate |

## Supply limits used for capture

- VA: 2.0–5.5 V
- VD: 1.62–3.6 V

For the POR10 M1 controller interface, no assumption is made that VA and VD must be the same rail. Their final prototype rail assignment is reviewed separately.

## Clock decision for M1

Use the manufacturer's optional **32.768 kHz crystal topology** as the default standalone receiver reference-clock candidate. Keep an external RCLK option available by DNP/selection so clock-induced RF noise can be compared experimentally.

The crystal option uses X1 with C5/C6 = 22 pF per the manufacturer BOM. For the SSOP reference topology, X1 is connected between GPO3/DCLK (pin 3) and RCLK (pin 19), with C5 from the GPO3/X1 node to GND and C6 from the RCLK/X1 node to GND. This topology is enabled by the POWER_UP clock-mode selection; it is not a conventional crystal connected around RCLK alone.

## Clock-topology correction

A prior review incorrectly concluded that the D60 could not use an external 32.768 kHz crystal. The manufacturer datasheet explicitly specifies an onboard crystal oscillator and the SSOP typical application shows the X1/C5/C6 network between GPO3/DCLK and RCLK. M1 therefore retains X1/C5/C6 and recaptures that exact topology rather than replacing it with an external oscillator.

## Important capture note

C1 belongs close to VA/DBYP according to the manufacturer's application schematic and notes; C4 belongs close to VD. Exact connectivity is taken from the graphical typical-application schematic during KiCad capture, not inferred from component names alone.

## AM/SW experimental population matrix

The external AM/SW input is intentionally selectable so the ferrite Q1 baseline is not permanently loaded.

| Mode | R_AM_BYPASS | R_AM_SELECT | L2 | R_AM_L_SELECT | T1 | R_AM_T_SELECT |
|---|---|---|---|---|---|---|
| Ferrite Q1 baseline | POP 0R | DNP | DNP | DNP | DNP | DNP |
| Direct external SMA | POP 0R | POP 0R | DNP | DNP | DNP | DNP |
| External SMA + L2 experiment | POP 0R | DNP | POP 10–20 uH | POP 0R | DNP | DNP |
| External SMA + T1 experiment | POP 0R | DNP | DNP | DNP | POP 1:5 | POP 0R |

Rules:
- `R_AM_SELECT`, `R_AM_L_SELECT`, and `R_AM_T_SELECT` are mutually exclusive receiver-path selectors.
- Populate at most one of those three selectors for an external-antenna experiment.
- `R_AM_BYPASS` is the normal populated input link and is not the receiver-path selector.
- Ferrite Q1 keeps all three external receiver-path selectors DNP.
- L2 and T1 remain experimental DNP parts unless their matching mode is explicitly under test.

## Status

Reference passive values and clock candidate are now **FROZEN FOR M1 CAPTURE**.

Remaining M1.3 capture gate:
- exact SSOP land pattern/dimensions
- graphical KiCad schematic
- ERC
- manual visual/reference-design review
