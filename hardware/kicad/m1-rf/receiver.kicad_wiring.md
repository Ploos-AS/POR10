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
