# U1 symbol review

The project-local `POR10:Si4735-D60-SSOP24` symbol has now been created.

## Locked properties

- 24 pins
- verified D60 SSOP numbering
- FMI = 8
- RFGND = 9
- AMI = 12
- RST/SEN/SCLK/SDIO = 15–18
- RCLK = 19
- VD/VA/DBYP = 20–22
- ROUT/LOUT = 23/24
- pins 6/7 are explicit NC pins
- pins 10/11 are represented as grounded/unused supply-type pins rather than NC
- footprint association points to the POR10-local 0.635 mm SSOP footprint

## Status

**U1 symbol: CAPTURED.**

The symbol still requires KiCad parser/ERC validation together with the schematic. Electrical pin types may be adjusted if ERC reveals a type that better represents the manufacturer's multifunction behaviour; such changes must not alter numbering or connectivity.
