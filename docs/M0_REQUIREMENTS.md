# M0 Requirements

## Product definition
POR10 (Ploos Open Radio 10) is a portable, receive-only, open-hardware communications receiver. It must work as a complete radio with networking disabled.

## Reception
- target LW/MW/SW: ~150 kHz–30 MHz
- target FM: ~64–108 MHz
- AM/FM and USB/LSB where supported by the selected Si473x implementation
- fine tuning appropriate for SSB/CW listening
- FM RDS where supported
- external antenna input plus practical portable antenna support
- RF input protection
- switchable attenuation
- filter/preselector strategy
- optional LNA only where measurements justify it
- separate ferrite-path support for MW/LW is desirable

## User interface
- 2.4–2.8 inch non-touch IPS
- dedicated tuning encoder
- dedicated volume control/encoder
- physical function buttons
- encoder acceleration
- readable daylight and very-low-light operation
- no touch dependency

## Audio
- internal front-facing speaker
- 3.5 mm headphone output
- line/audio output
- mute and software volume control
- audio recording to microSD is an advanced feature

## Power
- USB-C power/programming
- replaceable 18650-class battery concept
- charging and battery protection
- battery state measurement
- physical power control
- power design must minimize receiver interference

## Storage and time
- microSD
- persistent settings/memories
- UTC-oriented clock support
- RTC should be evaluated against BOM/power cost
- NTP may set time when networking is enabled but cannot be required

## RF quiet / DX mode
POR10 shall treat self-generated RF noise as a first-class design concern. A DX/RF-quiet mode should be able to disable Wi-Fi/Bluetooth and unnecessary digital activity, reduce display/MCU activity where useful, and select receiver/front-end settings appropriate for weak-signal listening.

## Advanced receiver functions
Planned software capabilities include:
- configurable band/range/memory scanning
- RSSI/SNR thresholding and activity logging
- pseudo spectrum/band-scope and waterfall based on receiver sweeps
- SWL logbook
- audio and scheduled recording
- offline frequency/station database
- profiles such as Broadcast, MW DX, SWL, Amateur and Utility
- sunrise/sunset and optional propagation-oriented views

Any station identification inferred from frequency/time databases must be presented as a candidate, not as confirmed identification.

## Engineering mode
Expose useful receiver and system state such as frequency, mode, bandwidth, RSSI, SNR, AGC-related state where available, BFO offset, battery state and subsystem diagnostics. Hardware shall provide documented test points where practical.

## Local control architecture
Radio core functionality must not depend on integrations. A stable internal/local control layer should support:
- USB serial control
- local network API/event interface
- local web UI
- MQTT
- future CAT compatibility where practical

## Home Assistant
Home Assistant integration is planned through MQTT and MQTT Discovery. Candidate entities include frequency, mode, bandwidth, volume, mute, preset, RSSI, SNR and battery state.

## Prometheus
An optional local metrics endpoint should expose useful telemetry such as uptime, frequency/mode, RSSI/SNR, battery/power state, Wi-Fi state, scan/tuning counters and subsystem errors. Avoid high-cardinality labels.

## Privacy and networking
- Wi-Fi and Bluetooth are optional and user-controlled
- core radio operation is offline-first
- no mandatory account or cloud service
- integrations are opt-in
- RF-quiet mode must be able to stop radios/services that can create interference

## Expansion
Provide documented access, where electrically practical, to I2C, SPI, UART, GPIO, power and relevant audio/control signals. The architecture should permit future RF modules without replacing the whole UI/controller platform.

## Cost constraints
- target BOM <= EUR 60
- stretch <= EUR 50
- > EUR 75 before enclosure/battery/shipping requires redesign review
- spend first on RF integrity, power integrity, controls and usable audio
- optional features should use DNP footprints/modules where sensible

## Licensing
Hardware, PCB, mechanical design and HDL/gateware use CERN-OHL-P-2.0. Firmware/software use MIT unless inherited licensing requires otherwise.

## M0 exit criteria
M0 is complete when the high-level architecture, v1 scope, RF strategy, major interfaces, cost envelope and initial component classes are documented sufficiently to begin RF prototyping without prematurely freezing an unmeasured RF implementation.
