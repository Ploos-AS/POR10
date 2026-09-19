# POR10 M0 Interface and Pin Budget

This is a logical budget, not yet a final ESP32-S3 GPIO assignment.

| Function | Interface / signals | Notes |
|---|---|---|
| Si473x control | I2C + reset/interrupt as needed | dedicated control bus preferred |
| Display | SPI + CS/DC/RST/backlight | evaluate shared SPI carefully |
| microSD | SPI + CS + card detect optional | may share bus if qualified |
| Tuning encoder | A/B + switch | interrupt-capable GPIO |
| Volume encoder | A/B + switch | GPIO |
| Function keys | 4–6 inputs | matrix/expander only if useful |
| Audio control | GPIO/I2C as selected | exact M3 architecture TBD |
| Battery/power | ADC/I2C + status GPIO | charger/fuel measurement |
| USB | native USB D+/D- | reserve correct native pins |
| RF control | GPIO/I2C/SPI | attenuator/filter/LNA switching |
| Expansion | I2C, SPI, UART, GPIO | documented maker header/pads |
| Debug | UART/JTAG/test pads | must remain accessible |

## Rules

- Do not assign boot/strapping-sensitive pins casually.
- Keep high-speed display/SD routing away from sensitive RF sections.
- Reserve enough GPIO for RF switching before spending pins on convenience features.
- Prefer I/O expanders for slow UI signals only if pin pressure justifies their BOM/complexity.
- Expansion pins are a budgeted feature, not leftovers.
- Provide labelled ground and power beside expansion signals.
- Final pin map follows selected ESP32-S3 module and schematic review.
