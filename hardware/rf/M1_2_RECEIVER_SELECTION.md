# POR10 M1.2 Receiver Selection

## Decision

**Baseline receiver: Silicon Labs Si4735-D60 family.**

Preferred prototype package: **Si4735-D60-GU / -GUR, 24-pin SSOP**, subject to genuine-part availability.

The QFN -GM/-GMR remains electrically relevant for a later compact production revision, but the SSOP is preferred for early POR10 RF prototypes because it is substantially easier to inspect, probe and rework.

## Why Si4735-D60

The D60 Si4735 is an AM/FM/SW/LW broadcast receiver with RDS/RBDS support. Its documented native ranges include:
- LW 153–279 kHz
- MW 520–1710 kHz
- SW 2.3–26.1 MHz
- FM 64–108 MHz

The part exposes separate FMI and AMI antenna inputs, analog audio, digital audio capability, RSSI/AGC-related receiver functions and 2/3-wire control.

## Important POR10 correction

The earlier M0 target of approximately **150 kHz–30 MHz** is a *platform/product aspiration*, not a guaranteed native Si4735-D60 tuning specification.

For M1, the baseline must be qualified against the device's documented ranges. Any extension toward 30 MHz, gaps between documented broadcast ranges, or SSB behaviour supplied through patch firmware must be treated as an experimental capability and qualified separately.

POR10 documentation must not imply native coverage or SSB support that has not been demonstrated on the exact receiver/firmware combination.

## Package choice

### M1 prototype — SSOP
Advantages:
- 0.635 mm pitch, hand-rework friendly relative to QFN
- pins accessible for probing
- easier prototype inspection
- simpler fault isolation

Tradeoff: larger board area and higher documented receive current than the QFN variant in available D60 documentation/distributor data.

### Later option — QFN
20-pin 3 x 3 mm QFN is suitable for a compact integrated board after the RF design is qualified. It is not necessary to accept its rework/debug penalty in M1.

## Electrical baseline

Use the manufacturer's typical application as the starting reference, not hobby-module schematics.

Key constraints:
- VA and VD are separate supply domains; follow exact selected-package datasheet limits.
- place supply bypass capacitors at the relevant pins
- all grounds connect to a low-impedance ground plane
- keep FMI/AMI paths as short as practical
- expose RESET and I2C/control access
- follow the manufacturer's antenna/layout guidance before inventing matching networks

## Antenna interfaces

Si4735-D60 provides separate FM and AM antenna inputs. POR10's external SMA/telescopic/ferrite architecture therefore needs an intentional routing strategy rather than treating the receiver as one generic 50-ohm input.

M1 will characterize:
- FMI path for FM
- AMI path for LW/MW/SW
- practical external-antenna coupling
- ferrite-loop implementation
- any switching needed to make POR10's user-facing antenna arrangement coherent

## RDS

Si4735 is selected over non-RDS family variants because RDS is a POR10 v1 requirement.

## SSB

SSB is **not considered a native D60 baseline capability for qualification**. Community Si47xx projects commonly use downloadable patch mechanisms on compatible revisions, but POR10 must separately record the exact patch provenance, licensing, receiver revision and measured behaviour before USB/LSB can be claimed.

This is an explicit M1 qualification item.

## Supply / clock / control

Final values and clock topology must be copied from the exact selected revision's datasheet/application guidance during schematic capture.

For M1.2:
- control: I2C preferred
- external controller: ESP32-S3 development board
- unnecessary ESP32 radios disabled during baseline RF tests
- crystal/reference-clock choice remains open until schematic review
- analog audio is sufficient for first receive qualification

## Procurement risk

Si473x parts are widely encountered through modules and secondary channels. M1 must record supplier, marking, package and observed revision/firmware identification. Unknown/counterfeit/re-marked parts must not silently become the POR10 production baseline.

## M1.2 result

**PASS for schematic baseline selection, conditional on sourced-part verification.**

Next: create the first KiCad schematic around the SSOP Si4735-D60 reference circuit with explicit FMI/AMI paths, bypassable RF experiments, control header and test points.
