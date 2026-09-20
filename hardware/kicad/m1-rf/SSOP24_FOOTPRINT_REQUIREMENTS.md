# POR10 M1.3 — Si4735-D60 SSOP-24 Footprint Requirements

## Package

U1 uses the Si4735-D60 **24-pin SSOP** package.

Manufacturer package drawing: 24-pin SSOP, nominal **0.025 in / 0.635 mm lead pitch**.

## Capture/PCB policy

Prefer a standard KiCad SSOP-24 footprint only when its geometry has been checked against the manufacturer package drawing. Do not select a footprint merely because the pin count and pitch match.

Candidate KiCad class:

`Package_SO:SSOP-24_5.3x8.2mm_P0.65mm`

is **not automatically acceptable** because the common library part uses 0.65 mm pitch while the device drawing specifies 0.025 in (0.635 mm). POR10 must not silently substitute the pitch.

## Required custom footprint

Create/verify a POR10-local footprint:

`POR10:SSOP-24_Si4735-D60_P0.635mm`

Requirements:
- 24 gull-wing pads
- 0.635 mm pitch
- pin 1 marker
- courtyard based on actual maximum package/lead envelope
- fab outline from manufacturer dimensions
- silkscreen clear of pads
- sufficient hand-rework access for M1
- no exposed thermal pad
- pad dimensions derived from an IPC/manufacturer-compatible land pattern, not guessed from body size

## Pin orientation

Pin numbering must follow the package drawing and U1 symbol:
- pin 1 at manufacturer pin-1 corner
- counter-clockwise numbering around package
- pins 1–12 on one side, 13–24 returning on the opposite side as shown by the package convention/drawing

A printed assembly drawing must make pin 1 unmistakable.

## Qualification

Before PCB fabrication:
- [ ] package pitch checked: 0.635 mm
- [ ] body dimensions checked against exact manufacturer drawing
- [ ] lead span checked
- [ ] lead width/length checked
- [ ] pad geometry independently reviewed
- [ ] pin-1 orientation cross-checked against schematic
- [ ] courtyard clearance checked
- [ ] 1:1 print/PDF physical sanity check
- [ ] KiCad DRC clean

## Decision

**Do not use an approximately matching 0.65 mm library footprint.**

M1 prioritizes correctness and reworkability over avoiding a project-local footprint.

## Status

Package family and exact pitch are frozen. Final pad geometry remains a PCB-capture task and must be checked against the manufacturer's mechanical drawing before M1.3 PASS.


## Manufacturer mechanical drawing verification

Verified against Skyworks Si4730/31/34/35-D60 Rev. 1.2, section 7.2 / Table 16:

- package standard: JEDEC MO-137, variation AE
- A: max 1.75 mm
- A1: 0.10–0.25 mm
- lead width b: 0.20–0.30 mm
- lead thickness c: 0.10–0.25 mm
- body length D: 8.65 mm BSC
- overall lead span E: 6.00 mm BSC
- body width E1: 3.90 mm BSC
- lead pitch e: 0.635 mm BSC
- lead length L: 0.40–1.27 mm
- L2: 0.25 mm BSC
- lead angle: 0–8 degrees

These dimensions supersede the provisional body geometry previously used in the local footprint.

### Land-pattern policy

The manufacturer drawing specifies the component package envelope, not a complete POR10 solder-land recommendation. Pad geometry therefore remains derived design work. For M1 we will use a conservative hand-rework-friendly land pattern and require a 1:1 print + DRC + assembly review before fabrication.

**Mechanical package dimensions: VERIFIED.**
