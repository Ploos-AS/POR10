# POR10 M1.3 Capture Gate

## Result

**BLOCKED — authoritative Si4735-D60 SSOP pin/reference data not yet captured in-repo.**

M1.3 requires a real KiCad schematic whose receiver symbol, pin numbers, supply limits, clock network, antenna networks and audio connections have been checked against the exact Silicon Labs Si4735-D60 SSOP documentation.

A current search of Silicon Labs' public support/resource pages confirms that Silicon Labs provides CAD/CAE symbols and footprints through its resource system and explicitly requires exported CAD data to be verified against the published datasheet. However, the exact D60 SSOP datasheet/pin table was not reliably retrievable in this qualification step.

## Engineering decision

Do **not** generate a plausible-looking KiCad schematic from third-party pin tables or memory.

That would violate the M1.3 review gate established in `M1_3_SCHEMATIC_SPEC.md`.

## Required unblock evidence

One of:

1. authoritative Silicon Labs Si4735-D60 datasheet/reference-design file containing the 24-pin SSOP pin table and typical application circuit; or
2. authoritative Silicon Labs CAD/CAE package plus the matching published datasheet used for verification.

Store the source identity/version/date in the qualification record. Vendor documents need not be redistributed if licensing prevents it; record source URL/title/hash where appropriate.

## Once unblocked

Capture and review:

- U1 Si4735-D60 SSOP symbol
- exact pin numbering
- FMI path
- AMI path
- VA/VD and decoupling
- GND
- RESET
- I2C/control
- crystal/reference clock
- LOUT/ROUT
- GPO/digital-audio pins where applicable
- bypassable protection/matching footprints
- ferrite experiment connector
- test points

Then run ERC and complete the eight review gates in `M1_3_SCHEMATIC_SPEC.md`.

## Status

M1.3 remains **ACTIVE / BLOCKED ON AUTHORITATIVE DEVICE DATA**.

This is preferable to silently committing an unverified RF schematic.
