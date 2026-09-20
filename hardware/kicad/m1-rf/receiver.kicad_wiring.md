# Receiver sheet wiring — M1.3

This file is the exact wiring manifest used to build and review `receiver.kicad_sch`.

## U1 Si4735-D60

- 8 FMI -> hierarchical/net label FMI_IN
- 9 RFGND -> GND
- 10 unused -> GND
- 11 unused -> GND
- 12 AMI -> AMI_IN
- 13 GND -> GND
- 14 GND -> GND
- 15 RST -> RX_RESET_N
- 16 SEN -> RX_SEN
- 17 SCLK -> RX_SCL
- 18 SDIO -> RX_SDA
- 19 RCLK -> crystal/reference network
- 20 VD -> RX_VD
- 21 VA -> RX_VA
- 22 DBYP -> C1/reference bypass network
- 23 ROUT -> RX_AUDIO_R
- 24 LOUT -> RX_AUDIO_L
- 6/7 -> explicit no-connect

## Reference parts

- C1 22 nF, manufacturer bypass/reference network
- C4 100 nF, VD bypass
- X1 32.768 kHz
- C5/C6 22 pF C0G, crystal load
- C2/C3 are placed on RF-input sheet, not receiver core

## Clock selection

Crystal is baseline. External RCLK must remain possible through a DNP/selection position; do not directly drive RCLK while the crystal topology is populated.

## Supply labels

RX_VA and RX_VD remain separate named rails during M1 even when fed from a common clean bench source.


## Supply bypass implementation block

Capture the following as the next self-contained graphical block before clock/control/RF:

| Ref | From | To | Value | Placement intent |
|---|---|---|---|---|
| C1 | RX_DBYP / U1.22 | GND | 22 nF | immediately adjacent to receiver DBYP region |
| C4 | RX_VD / U1.20 | GND | 100 nF | immediately adjacent to VD |
| TP_DBYP | RX_DBYP | probe | test point | short stub only |
| TP_VD | RX_VD | probe | test point | short stub only |
| TP_VA | RX_VA | probe | test point | short stub only |

Do not connect RX_DBYP to RX_VA. C1 is a DBYP-to-ground bypass. RX_VA remains a separately supplied rail.

### ERC staging

After C1/C4 are graphically captured:
1. run KiCad parser/export,
2. run ERC,
3. compare against the 29-violation baseline from commit `60c8e2d`,
4. investigate every new violation; do not add blanket exclusions,
5. only then proceed to X1/C5/C6.
