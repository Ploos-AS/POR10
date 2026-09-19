# POR10 M0 BOM Target

This is a design-cost envelope, not a supplier quote.

| Subsystem | Target EUR |
|---|---:|
| ESP32-S3 module | 5–8 |
| Si473x receiver | 5–10 |
| IPS display | 5–9 |
| RF protection/filtering/matching/optional gain | 5–10 |
| audio path + speaker | 3–6 |
| USB-C, charging, protection, regulation, measurement | 4–7 |
| encoders/buttons/connectors | 4–7 |
| microSD + storage support | 1–2 |
| PCB allocation at small quantity | 4–8 |
| miscellaneous passives/mechanical PCB parts | 4–7 |
| **planning range** | **40–74** |

## Cost gates

- Stretch target: <= EUR 50
- Nominal target: <= EUR 60
- Cost review: EUR 60–75
- Redesign threshold: > EUR 75 before enclosure, cell and shipping

## Cost philosophy

Do not cut the parts that make POR10 a good receiver: RF integrity, power integrity, controls and usable audio have priority.

Features that are inexpensive in firmware should not drive hardware complexity. Optional hardware should use DNP footprints or modules when practical.

## Not included yet

- enclosure
- battery cell
- antenna/telescopic hardware where not PCB-mounted
- shipping/tax
- assembly labour
- programming/test fixture
- retail margin

M1–M3 replace these planning figures with sourced component candidates and measured requirements.
