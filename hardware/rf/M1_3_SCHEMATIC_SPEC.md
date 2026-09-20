# POR10 M1.3 Schematic Capture Specification

## Status

**M1.3 schematic specification: READY FOR CAPTURE**

This is the authoritative capture checklist for the first Si4735-D60 SSOP RF prototype. Values that depend on the exact D60 datasheet/reference design are intentionally marked **VERIFY** rather than guessed.

## Sheets

The first KiCad project should use these logical sheets:

1. `receiver.kicad_sch` — Si4735-D60 and local decoupling/reference components
2. `rf_inputs.kicad_sch` — FMI/AMI antenna paths and experiment footprints
3. `control_audio.kicad_sch` — controller header, RESET, audio breakout
4. `power_test.kicad_sch` — prototype rails and test points

## U1 — receiver

Target: Si4735-D60-GU/GUR, 24-pin SSOP.

Before assigning pin numbers, verify every symbol pin against the exact Silicon Labs D60 SSOP datasheet. Do not reuse a community symbol without review.

Symbol must expose by function:
- FMI
- AMI
- analog supply domain
- digital supply domain
- grounds
- RESET
- control bus pins
- reference clock/crystal pins
- analog audio L/R
- any GPO/interrupt/digital-audio pins present on the selected package

Pin numbers: **VERIFY FROM DATASHEET DURING CAPTURE**.

## RF inputs

### FM path

```text
J1 SMA_FM
 -> ESD footprint
 -> 0R bypass / optional coupling-matching network
 -> TP_FMI
 -> U1 FMI
```

### AM/LW/MW/SW path

```text
J2 SMA_AM
 -> ESD footprint
 -> 0R bypass / configurable RLC matching positions
 -> TP_AMI
 -> U1 AMI
```

### Ferrite experiment header

Provide a two-pin or suitable experiment connector near the AMI network so a ferrite rod winding/coupling network can be evaluated without modifying the receiver section.

M1.3 uses separate FM and AM-family connectors deliberately. User-facing antenna consolidation/switching comes only after M1 measurements.

## Protection / matching footprints

Every experimental series path must have a known bypass state.

Use footprints allowing:
- series 0R / capacitor / inductor
- shunt capacitor/inductor positions where appropriate
- ESD device populated vs bypass comparison

Do not claim a 50-ohm match to Si4735 antenna pins unless measurement/reference documentation supports it.

## Supplies

Create separately named analog and digital receiver rails even if the prototype later derives both from the same clean source.

For each supply pin/domain:
- local high-frequency decoupling at U1
- bulk/local reservoir where reference design recommends it
- supply test point
- optional series bead/0R experiment position if useful

All exact values and permitted voltage ranges: **VERIFY against selected D60 documentation**.

## Grounding

- one intentional low-impedance ground system/plane for prototype PCB
- identify RF and digital probe ground points by location/function, not by splitting the board into uncontrolled isolated grounds
- no long return path through controller headers
- place RF ground vias close to RF/protection components

## Clock/reference

Provide the manufacturer-supported reference-clock/crystal topology.

M1.3 must not invent crystal values. Capture:
- crystal/reference component footprint(s)
- any load components required by the exact reference circuit
- optional external-reference injection/test option only if it can be added without degrading normal operation

Exact topology/values: **VERIFY**.

## Control header J_CTRL

Expose:
- GND
- required receiver supply/reference as appropriate
- SDA
- SCL
- RESET
- optional GPO/interrupt/status signal(s)

Use I2C for POR10 M1 baseline.

Pull-up population must be configurable because the ESP32-S3 development harness may already provide or require a chosen pull-up arrangement.

## Audio breakout

Expose analog L/R outputs according to the datasheet's required loading/coupling.

M1.3 provides:
- TP_AUDIO_L
- TP_AUDIO_R
- nearby GND
- connector/header for external listening/test amplifier

No final speaker amplifier is part of M1.3.

## Test points

Required:
- TP_FMI
- TP_AMI
- TP_VA
- TP_VD
- TP_GND_RF
- TP_GND_CTRL
- TP_RESET
- TP_SDA
- TP_SCL
- TP_AUDIO_L
- TP_AUDIO_R

Test structures on FMI/AMI must minimize RF stubs.

## DNP philosophy

Mark experimental parts clearly:
- `DNP_BASELINE`
- `POP_BASELINE`
- `ALT_VALUE`

The schematic notes must make the Q1 baseline population unambiguous.

## Baseline population

Q1 baseline should contain only:
- U1 and mandatory reference components
- mandatory decoupling/reference clock
- control connection
- audio breakout
- SMA inputs
- minimum safe coupling/matching required by manufacturer guidance
- bypass links

No LNA. No filter bank. No automatic antenna switch.

## ERC / review gates

M1.3 is not PASS merely because KiCad ERC is clean.

Required review:
1. every U1 pin name/number checked against exact D60 SSOP datasheet
2. supply limits checked
3. clock network checked
4. FMI/AMI reference networks checked
5. audio loading checked
6. RESET/control levels checked for ESP32-S3 compatibility
7. all DNP/bypass states reviewed
8. ERC clean or every exception documented

## Output

Expected KiCad tree:

```text
hardware/kicad/m1-rf/
  por10-m1-rf.kicad_pro
  por10-m1-rf.kicad_sch
  receiver.kicad_sch
  rf_inputs.kicad_sch
  control_audio.kicad_sch
  power_test.kicad_sch
```

## Exit criterion

M1.3 PASS requires a real reviewed KiCad schematic, not this specification alone.
