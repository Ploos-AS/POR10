# POR10 M1.1 RF Baseline Design

## Goal

Build the simplest useful, measurable Si473x receiver reference path. M1.1 is deliberately **not** the final POR10 RF front-end. It establishes the baseline against which protection, attenuation, filtering and gain are judged.

## Baseline topology

```text
J1 SMA RX
   |
   +-- ESD/protection footprint (bypassable)
   |
   +-- configurable matching / DC-block footprint
   |
   +-- RF test / injection node
   |
   +-- Si473x antenna input

Si473x
   +-- I2C control header
   +-- RESET
   +-- audio outputs / test points
   +-- supply test point
   +-- ground test points
```

For the first prototype, every non-essential RF network must have a zero-ohm/bypass configuration.

## Design rules

- Receive only. No TX path and no antenna bias voltage.
- SMA female is the controlled external-input reference.
- Keep the RF trace short and isolated from digital clocks.
- Provide ground immediately beside RF probing points.
- Do not populate an LNA in the baseline.
- Do not hide unknowns behind an elaborate filter bank.
- Protection is physically provisioned but must be bypassable so insertion effects can be measured.
- Matching footprints should permit practical R/L/C experimentation without PCB rework.
- Use explicit net names and documented test points.
- Early prototype should favour hand rework and measurement over minimum board area.

## Test points

Minimum:
- TP_RF_IN — after connector/protection boundary as appropriate
- TP_RX_SUPPLY
- TP_GND_RF
- TP_GND_DIG
- TP_AUDIO_L
- TP_AUDIO_R
- I2C access
- RESET access

Avoid adding large stubs directly to sensitive RF nets merely to create convenient test points.

## Control interface

M1.1 may use an external ESP32-S3 development board or equivalent controller rather than waiting for the POR10 mainboard.

Required signals:
- 3V3/GND as appropriate to selected receiver implementation
- I2C SDA/SCL
- RESET
- optional receiver interrupt/status signal if the selected implementation benefits from it

The prototype controller must be electrically quiet enough that controller noise can be distinguished from receiver behaviour.

## Audio

M1.1 does not qualify the final POR10 audio amplifier. Expose receiver audio safely for measurement/listening using the selected receiver implementation's documented output requirements.

## Power

Start from a known clean bench supply/regulator arrangement. Power-converter qualification belongs later. Record voltage and current during tests.

## Variants to compare

A — minimum/bypass path

B — protection populated

C — matching candidate(s)

Later M1 substeps add attenuator, filters/preselector and optional LNA to the measured A/B reference.

## Deliverables

- KiCad RF prototype schematic
- exact receiver part/module documented
- exact prototype BOM
- assembly notes
- controller hookup
- baseline firmware/tool
- Q1 results
- raw measurement log

## Exit criterion

M1.1 passes when a repeatable receiver baseline exists across representative bands and the result can be reproduced from repository documentation.
