# POR10 M1.3 — Receiver schematic capture manifest

This file is the exact component/net manifest for the first graphical `receiver.kicad_sch`. It closes ambiguity before serialization into KiCad's schematic format.

## U1

- U1: Si4735-D60-GU/GUR
- Symbol: `POR10:Si4735-D60-SSOP24`
- Footprint: `POR10:SSOP-24_Si4735-D60_P0.635mm`

## Mandatory receiver-local components

| Ref | Value | Baseline | Connection |
|---|---|---|---|
| C1 | 22 nF | POP | manufacturer VA/DBYP reference network |
| C4 | 100 nF | POP | RX_VD to GND, close to U1 |
| X1 | 32.768 kHz | POP | manufacturer crystal topology |
| C5 | 22 pF C0G | POP with X1 | crystal load to GND |
| C6 | 22 pF C0G | POP with X1 | crystal load to GND |

The exact C1 VA/DBYP wiring is copied from the manufacturer graphical reference during schematic capture; this manifest deliberately does not infer connectivity from the BOM label.

## Sheet nets

### RF
- `FMI_IN` -> U1.8
- `AMI_IN` -> U1.12

### Control
- U1.15 -> `RX_RESET_N`
- U1.16 -> `RX_SEN`
- U1.17 -> `RX_SCL`
- U1.18 -> `RX_SDA`
- U1.5 -> `RX_GPO1`
- U1.4 -> `RX_GPO2_INT`
- U1.3 -> `RX_GPO3`

### Clock
- U1.19 -> `RX_RCLK`
- X1/C5/C6 use the manufacturer-supported 32.768 kHz topology.
- External RCLK remains an alternate/DNP test option and must not electrically fight X1.

### Supplies
- U1.20 -> `RX_VD`
- U1.21 -> `RX_VA`
- U1.22 -> `RX_DBYP`
- U1.9, 10, 11, 13, 14 -> GND
- U1.6, 7 -> explicit no-connect; never ground them.

### Audio
- U1.23 -> `RX_AUDIO_R`
- U1.24 -> `RX_AUDIO_L`
- U1.1/2 remain optional multifunction/digital-audio breakout only.

## Receiver-sheet test points

- TP_VA on RX_VA
- TP_VD on RX_VD
- TP_RESET on RX_RESET_N
- optional clock probe point only if its stub/loading is acceptable

FMI/AMI and audio test points belong on their respective sheets so the receiver sheet does not create unnecessary RF stubs.

## ERC intent

Pins 6/7 receive explicit no-connect markers. Pins 10/11 are connected to GND. Power pins are not hidden. No `PWR_FLAG` is added merely to silence ERC; flags belong at the actual prototype power source.

## Capture gate

The graphical schematic must be opened by KiCad and checked for:
1. parser success,
2. zero unintended dangling mandatory pins,
3. U1 footprint association,
4. explicit no-connect on 6/7 only,
5. grounded 9/10/11/13/14,
6. manufacturer-reference check of C1/DBYP and X1 topology,
7. ERC with every exception documented.

This manifest is not itself M1.3 PASS; it is the frozen input to the graphical capture.


## L1 ferrite antenna interface freeze

For M1 qualification, L1 remains an **external replaceable ferrite loopstick**, nominal 180–450 uH. The PCB interface is a two-terminal keyed connector/test interface rather than a fixed PCB inductor. This keeps ferrite material, rod geometry, winding inductance and placement experimentally replaceable during Q7 antenna qualification.

Capture intent:
- pin 1: `AM_FERRITE` -> C3 -> U1.12 AMI
- pin 2: GND
- `TP_AMI` remains accessible on the receiver side
- no assumption that L1 is a generic SMT/through-hole inductor
- connector footprint remains unfrozen until mechanical selection
- optional L2/T1 external-antenna network stays DNP/separate from L1 baseline


## External AM/SW antenna option — L2/T1 gate

The qualified ferrite baseline remains unchanged. M1.3 reserves a separate **DNP experimental external AM/SW antenna branch** for Q7/Q6 measurements:

- input: `AM_EXT` from the external antenna/protection section
- L2: 10–20 uH air-loop / matching element, **DNP baseline**
- T1: 1:5 turns transformer option, **DNP baseline**
- output: selectable coupling to the receiver-side `AM_FERRITE` / AMI path only during experiments
- no permanent parallel loading of the ferrite loopstick in the baseline population
- no claim of 50-ohm AMI impedance
- protection, switching and exact matching values are qualified separately before population

This keeps the manufacturer-reference ferrite path as the known baseline while allowing external long-wire/loop/SW antenna experiments without baking an unverified matching network into M1 hardware.
