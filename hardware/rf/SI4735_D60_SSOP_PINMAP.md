# Si4735-D60 SSOP Verified Pin Map

Authoritative device family document: Silicon Laboratories Si4730/31/34/35-D60, Rev. 1.1; cross-checked against later Skyworks Rev. 1.2 publication.

| Pin | Net/function | POR10 M1.3 treatment |
|---:|---|---|
| 1 | DOUT/[LIN] | expose/test; DNP if unused |
| 2 | DFS/[RIN] | expose/test; DNP if unused |
| 3 | GPO3/[DCLK] | expose/test as needed |
| 4 | GPO2/[INT] | optional controller status/INT |
| 5 | GPO1 | optional test |
| 6 | NC | leave floating |
| 7 | NC | leave floating |
| 8 | FMI | FM RF path |
| 9 | RFGND | ground plane |
| 10 | unused NC | tie GND per application note |
| 11 | unused NC | tie GND per application note |
| 12 | AMI | AM/SW/LW RF path |
| 13 | GND | ground plane |
| 14 | GND | ground plane |
| 15 | RST | controller/reset |
| 16 | SEN | serial-enable/interface configuration |
| 17 | SCLK | I2C/control clock role per selected interface |
| 18 | SDIO | I2C/control data role per selected interface |
| 19 | RCLK | reference clock/crystal network |
| 20 | VD | digital/I/O supply |
| 21 | VA | analog supply |
| 22 | DBYP | bypass capacitor per reference circuit |
| 23 | ROUT/[DOUT] | analog right / alternate digital out |
| 24 | LOUT/[DFS] | analog left / alternate digital function |

## Capture warning

Do not confuse pins 6/7 with 10/11: the manufacturer's SSOP application notes explicitly distinguish the former as leave-floating NCs and the latter as unused pins tied to GND.

This table removes the pin-number blocker only. Passive values and package geometry remain subject to exact-datasheet capture review.
