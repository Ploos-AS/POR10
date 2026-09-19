# POR10 Roadmap

## M0 — Architecture & requirements
Freeze scope, cost envelope, interfaces, RF strategy, power/audio/UI architecture, feature layers, mechanical direction and licensing. Define observability and automation interfaces early without making networking a dependency.

## M1 — RF prototype
Qualification plan: `docs/M1_RF_QUALIFICATION_PLAN.md`.

Characterize Si473x receiver path, antenna protection/switching/matching, attenuation, optional LNA and filter/preselector strategy.

## M2 — Controller & UI prototype
ESP32-S3, IPS display, encoders/buttons, receiver control, tuning and minimal standalone UI.

## M3 — Audio & power
Speaker/headphone/line audio, USB-C, battery charging/protection/fuel measurement and noise qualification.

## M4 — Integrated PCB
Integrated KiCad design with strong RF/digital partitioning, test points and practical modularity.

## M5 — Core firmware & UI
Offline radio UI, memories, band plans, seek/scan, RDS, profiles, persistent configuration and SD support.

## M6 — Advanced receiver features
Smart scanning, signal/activity logging, SWL logbook, audio recording and scheduled recording, pseudo band-scope/waterfall, UTC tools, sunrise/sunset, engineering mode and DX/RF-quiet mode.

## M7 — Mechanical design
Maker-friendly enclosure/front panel, controls, speaker, antennas and connector placement.

## M8 — RF & system qualification
Sensitivity, strong-signal behaviour, internally generated noise, RF-quiet effectiveness, audio/power behaviour, battery runtime, thermal and EMC-oriented checks.

## M9 — Connected integrations
Local REST/WebSocket-style API/event interface, USB serial control, local web UI, MQTT, Home Assistant MQTT Discovery, Prometheus metrics and optional NTP/database updates. All networking is opt-in.

## M10 — Open-hardware release
Manufacturing outputs, BOM, assembly/troubleshooting/service docs, firmware release and reproducible release package.

## M11 — Platform expansion
Alternative RF boards/front-ends, experimental SDR receiver options, optional GPS/location module and community expansion hardware.

### Future / exploratory
Propagation/grayline views, richer offline frequency databases, CAT compatibility where practical and additional automation integrations.
