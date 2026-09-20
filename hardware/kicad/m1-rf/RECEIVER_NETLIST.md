# POR10 M1.3 Receiver Sheet — Capture Netlist

This is the reviewed logical netlist for the first KiCad receiver sheet. It is intentionally text-first so the eventual KiCad schematic can be checked mechanically and visually against a stable source of truth.

Authoritative reference: Skyworks/Silicon Labs **Si4730/31/34/35-D60**, Rev. 1.2, section 2.2 (SSOP Typical Application Schematic).

## U1 — Si4735-D60, 24-pin SSOP

| Pin | Name | M1 connection |
|---:|---|---|
| 1 | DOUT/[LIN] | optional digital-audio breakout; otherwise DNP |
| 2 | DFS/[RIN] | optional digital-audio breakout; otherwise DNP |
| 3 | GPO3/[DCLK] | optional breakout / crystal topology |
| 4 | GPO2/[INT] | controller/test header |
| 5 | GPO1 | test pad |
| 6 | NC | **NO CONNECT — FLOAT** |
| 7 | NC | **NO CONNECT — FLOAT** |
| 8 | FMI | net `FMI_IN` |
| 9 | RFGND | GND plane |
| 10 | NC/unused | **GND per manufacturer note** |
| 11 | NC/unused | **GND per manufacturer note** |
| 12 | AMI | net `AMI_IN` |
| 13 | GND | GND plane |
| 14 | GND | GND plane |
| 15 | RSTB | `RX_RESET_N` |
| 16 | SENB | `RX_SEN` |
| 17 | SCLK | `RX_SCL` |
| 18 | SDIO | `RX_SDA` |
| 19 | RCLK | `RX_RCLK` |
| 20 | VD | `RX_VD` |
| 21 | VA | `RX_VA` |
| 22 | DBYP | `RX_DBYP` |
| 23 | ROUT/[DOUT] | `RX_AUDIO_R` |
| 24 | LOUT/[DFS] | `RX_AUDIO_L` |

## Mandatory local networks

### Analog supply

`RX_VA -> U1.21`

Place the manufacturer-specified VA bypass capacitor physically close to the receiver. Exact value is copied from the selected datasheet revision during graphical capture/BOM freeze.

### Digital supply

`RX_VD -> U1.20`

Place the manufacturer-specified VD bypass capacitor physically close to U1.20.

### DBYP

`U1.22 -> manufacturer DBYP bypass network -> GND`

Do not repurpose DBYP.

### Ground

U1.9, U1.13 and U1.14 go directly to the PCB ground plane. U1.10 and U1.11 also go to GND as explicitly required by the SSOP application notes. U1.6 and U1.7 remain floating.

## RF sheet ports

- `FMI_IN` -> U1.8
- `AMI_IN` -> U1.12
- `GND`

FMI/AMI sheet-port placement should permit the receiver to sit physically close to the antenna circuitry on PCB.

## Control sheet ports

- `RX_RESET_N`
- `RX_SEN`
- `RX_SCL`
- `RX_SDA`
- `RX_GPO1`
- `RX_GPO2_INT`
- `RX_GPO3`

## Clock

`RX_RCLK -> U1.19`

The D60 reference schematic permits an external RCLK or an optional crystal topology involving GPO3/RCLK. POR10 M1 keeps the topology selectable until the exact crystal/reference implementation is frozen.

## Audio sheet ports

- `RX_AUDIO_L` <- U1.24
- `RX_AUDIO_R` <- U1.23

Final loading/coupling belongs on the audio/control sheet and must follow the selected analog-audio configuration.

## ERC intent

- pins 6/7: explicit no-connect markers
- pins 10/11: grounded, **not** no-connect
- RF inputs: input/passive electrical type as appropriate
- supply pins: powered through explicit power entry / PWR_FLAG only where KiCad requires it
- multifunction digital/audio pins: symbol types chosen to avoid hiding real conflicts

## Capture review

- [x] 24-pin map checked against manufacturer Rev. 1.2 typical application
- [x] FMI/AMI pins checked
- [x] floating-vs-grounded NC distinction checked
- [x] VA/VD ranges identified in manufacturer schematic
- [x] receiver-sheet logical nets defined
- [ ] exact bypass values transcribed
- [ ] clock implementation frozen
- [ ] exact SSOP land pattern checked
- [ ] graphical KiCad schematic captured
- [ ] ERC clean/reviewed

**M1.3 remains ACTIVE until the graphical KiCad schematic and ERC review exist.**
