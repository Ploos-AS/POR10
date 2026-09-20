# POR10 M1.3 Capture Gate

## Result

**UNBLOCKED — authoritative-manufacturer datasheet content located via preserved/mirrored copies.**

The Si4730/31/34/35-D60 datasheet (Silicon Laboratories Rev. 1.1 and later Skyworks Rev. 1.2 publication) provides the 24-pin SSOP pin assignment and SSOP typical application schematic required by M1.3.

## Verified SSOP pin map

| Pin | Signal |
|---:|---|
| 1 | DOUT/[LIN] |
| 2 | DFS/[RIN] |
| 3 | GPO3/[DCLK] |
| 4 | GPO2/[INT] |
| 5 | GPO1 |
| 6 | NC — leave floating |
| 7 | NC — leave floating |
| 8 | FMI |
| 9 | RFGND |
| 10 | NC/unused — tie to GND per typical application notes |
| 11 | NC/unused — tie to GND per typical application notes |
| 12 | AMI |
| 13 | GND |
| 14 | GND |
| 15 | RST |
| 16 | SEN |
| 17 | SCLK |
| 18 | SDIO |
| 19 | RCLK |
| 20 | VD |
| 21 | VA |
| 22 | DBYP |
| 23 | ROUT/[DOUT] |
| 24 | LOUT/[DFS] |

## Verified reference constraints

- SSOP VA: 2.0–5.5 V in the D60 typical-application documentation.
- VD: 1.62–3.6 V.
- FMI pin 8 is the FM antenna interface.
- AMI pin 12 is the AM/SW/LW interface.
- RFGND pin 9 connects to PCB ground plane.
- pins 6/7 are true no-connects and are left floating.
- pins 10/11 are unused and are tied to GND in the manufacturer's SSOP application notes.
- local bypassing belongs close to VA/VD.
- all grounds connect directly to the PCB ground plane.
- the receiver should be close to the antenna interfaces with short FMI/AMI traces.

## Source record

Authoritative document identity:
- Silicon Laboratories, *Si4730/31/34/35-D60 Broadcast AM/FM/SW/LW Radio Receiver*, Rev. 1.1 (2011) / later Skyworks publication Rev. 1.2 (2021).
- historical Silicon Labs document path: `/documents/public/data-sheets/Si4730-31-34-35-D60.pdf`

The repository records document identity rather than redistributing the vendor PDF.

## Next gate

M1.3 may now proceed to KiCad capture. Exact passive values, crystal/reference implementation and package land pattern must still be transcribed/reviewed from the same exact revision during capture.

**Status: UNBLOCKED / CAPTURE AUTHORIZED.**
