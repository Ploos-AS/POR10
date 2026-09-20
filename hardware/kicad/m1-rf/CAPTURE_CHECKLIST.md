# M1.3 KiCad Capture Checklist

## U1 symbol
- [ ] 24 pins present
- [ ] pin numbers match verified pin map
- [ ] pin 6/7 marked NC and left floating
- [ ] pin 10/11 grounded per SSOP application guidance
- [ ] FMI pin 8
- [ ] RFGND pin 9
- [ ] AMI pin 12
- [ ] RST/SEN/SCLK/SDIO pins 15–18
- [ ] RCLK pin 19
- [ ] VD/VA/DBYP pins 20–22
- [ ] ROUT/LOUT pins 23/24

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
- [ ] VA limits verified
- [ ] VD limits verified
- [ ] DBYP network verified
- [ ] local bypass values verified
- [ ] RCLK/crystal topology verified
- [ ] clean-supply test points

## Review
- [ ] reference-design cross-check
- [ ] exact SSOP footprint cross-check
- [ ] ERC
- [ ] ERC exceptions documented
- [ ] schematic PDF/export reviewed visually
- [ ] M1 Q1 population variant documented

M1.3 is PASS only when all mandatory items are checked.
