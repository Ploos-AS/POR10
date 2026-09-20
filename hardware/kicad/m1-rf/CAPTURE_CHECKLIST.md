# M1.3 KiCad Capture Checklist

## U1 symbol
- [x] 24 pins present
- [x] pin numbers match verified pin map
- [x] pin 6/7 marked NC and left floating
- [x] pin 10/11 represented distinctly for grounding per SSOP application guidance
- [x] FMI pin 8
- [x] RFGND pin 9
- [x] AMI pin 12
- [x] RST/SEN/SCLK/SDIO pins 15–18
- [x] RCLK pin 19
- [x] VD/VA/DBYP pins 20–22
- [x] ROUT/LOUT pins 23/24

## RF
- [ ] dedicated FM input connector
- [ ] dedicated AM/LW/MW/SW input connector
- [ ] ferrite experiment connector
- [ ] bypassable protection footprints
- [ ] configurable matching footprints
- [ ] short FMI/AMI routes planned
- [ ] RF probing does not create excessive stubs

## Control
- [ ] I2C header
- [ ] reset
- [ ] optional GPO/INT access
- [ ] configurable pull-ups
- [ ] controller ground return is explicit

## Audio
- [ ] analog L/R breakout
- [ ] nearby ground
- [ ] required loading/coupling verified before values frozen

## Power / clock
- [x] VA limits verified
- [x] VD limits verified
- [ ] DBYP network captured graphically
- [x] local bypass values verified
- [x] RCLK/crystal topology selected for M1
- [ ] clean-supply test points

## Review
- [x] reference-design pin-map cross-check
- [x] exact SSOP package dimensions cross-checked
- [ ] physical footprint 1:1 check against sourced device
- [ ] ERC
- [ ] ERC exceptions documented
- [ ] schematic PDF/export reviewed visually
- [ ] M1 Q1 population variant documented

M1.3 is PASS only when all mandatory items are checked.
