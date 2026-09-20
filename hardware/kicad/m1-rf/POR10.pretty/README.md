# POR10 local footprint library

## Si4735-D60 SSOP-24

`SSOP-24_Si4735-D60_P0.635mm` targets the verified JEDEC MO-137-AE package: 0.635 mm pitch, 8.65 x 3.90 mm body and 6.00 mm overall lead span.

The M1 prototype uses 1.80 x 0.40 mm pads on x = +/-3.20 mm centers. This is a POR10 hand-rework-oriented engineering land pattern, not a Silicon Labs published PCB land pattern. It gives a 7.30 mm outer copper span and 0.235 mm nominal pad-to-pad gap along each row.

Before fabrication, run KiCad DRC and a 1:1 physical check with an actual sourced Si4735-D60-GU/GUR. Confirm pitch, pin 1, body clearance, solder-mask dams, toe/heel access and sourced package dimensions. Record that check in M1 qualification.