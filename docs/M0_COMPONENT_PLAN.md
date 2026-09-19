# POR10 M0 Component Plan

This document freezes component *classes* for M0 while deliberately leaving RF-sensitive selections open for M1 measurement.

## Core controller

**ESP32-S3 module**, preferably a module rather than bare SoC for the first board revision.

Requirements:
- native USB support
- Wi-Fi + Bluetooth
- sufficient flash/PSRAM for UI, databases and networking
- mature ESP-IDF support
- module antenna option and, if practical, an external-antenna variant

Using a certified module reduces RF/layout risk and assembly difficulty.

## Receiver

**Si4732/Si4735-class receiver** for RF implementation v1.

M1 must qualify the exact device/source and firmware feature set before production lock. The design must not assume that every sourced variant has identical SSB/RDS behaviour.

## Display

2.4–2.8 inch SPI IPS, non-touch.

Selection criteria:
- widely available controller
- documented interface
- low enough digital/RF noise
- readable at reduced refresh rate
- controllable backlight

Final controller/panel is not frozen until noise and mechanical testing.

## Controls

- incremental tuning encoder with push switch
- separate volume encoder/control
- 4–6 physical function buttons
- physical power control

Prefer replaceable, mechanically supported controls over tiny board-only UI parts.

## Storage

microSD over SPI. Shared SPI is acceptable if chip-select, bus loading and RF-noise behaviour qualify.

## Audio

Component classes:
- receiver audio output/interface
- low-noise headphone path
- small speaker amplifier
- front-facing speaker
- 3.5 mm headphone jack
- line/audio output

M3 selects the exact amplifier architecture after receiver output levels and noise are measured.

## Power

- USB-C 5 V input
- Li-ion charger suitable for one replaceable 18650-class cell
- battery protection
- battery/system measurement
- low-noise system rails
- explicit power switching

Switching converters must be evaluated for receiver interference. Linear regulation should be used selectively where its noise advantage justifies dissipation.

## RF front-end classes

Not frozen before M1:
- ESD/input protection
- antenna selection
- switchable attenuator
- preselector/filter bank
- matching
- optional LNA
- ferrite MW/LW path

No LNA is mandatory merely for headline sensitivity. Strong-signal behaviour matters.

## Optional / DNP candidates

- RTC
- dedicated fuel gauge
- temperature sensor
- GPS connector/module support
- extra RF gain stage
- expanded filter population
- external Wi-Fi antenna connector variant

## Procurement rule

Prefer parts with multiple distributors or practical second sources. Avoid making POR10 dependent on obscure display modules, connectors or mechanically unique parts where a standard footprint can be used.
