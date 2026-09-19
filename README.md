# POR10

**Ploos Open Radio 10** — an open-hardware, maker-friendly portable communications receiver.

POR10 takes the compact Si473x receiver idea further: better RF engineering, better controls, repairability, documentation, extensibility and a useful offline-first software platform.

## M0 baseline

- ESP32-S3 controller
- Si4732/Si4735-class RF implementation for v1
- target LW/MW/SW coverage: ~150 kHz–30 MHz
- target FM coverage: ~64–108 MHz
- AM/FM/USB/LSB where supported
- CW-oriented fine tuning/UI
- RDS
- 2.4–2.8 inch non-touch IPS
- tuning + volume encoders and physical buttons
- speaker, 3.5 mm headphones and line/audio out
- USB-C, replaceable 18650-class battery architecture
- microSD
- Wi-Fi/Bluetooth, fully optional
- documented expansion/test interfaces
- receive-only v1

## Design priorities

1. Maker friendly first
2. Good RF behaviour and usability
3. Repairability and documentation
4. Sensible component availability
5. Cost control
6. Compact size

Target BOM: **<= EUR 60**. Stretch target: **<= EUR 50**. A design exceeding **EUR 75** before enclosure/battery/shipping triggers a cost review.

## Feature layers

**Core Radio** — completely useful offline.

**Advanced Receiver** — scanning, logging, recording, profiles, DX tools, engineering/diagnostic views.

**Connected / Experimental** — local API, web UI, MQTT/Home Assistant, Prometheus, optional online data and future RF modules. Network features must remain opt-in.

## Licensing

Hardware/PCB/mechanical/HDL: **CERN-OHL-P-2.0**. Firmware/software: **MIT**, except inherited components that require another license.

## Status

**M0 — Architecture & requirements: active.**

See [ROADMAP.md](ROADMAP.md) and [docs/M0_REQUIREMENTS.md](docs/M0_REQUIREMENTS.md).
