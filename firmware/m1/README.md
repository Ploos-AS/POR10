# M1 RF Prototype Firmware

M1 firmware exists to qualify hardware, not to prototype the final POR10 UI.

## Minimum functions

- initialize selected Si473x receiver
- set frequency
- set mode/bandwidth where supported
- report frequency
- report RSSI
- report SNR
- expose repeatable serial commands suitable for scripted measurements

## Suggested serial surface

```text
INFO
FREQ <Hz>
MODE <AM|FM|USB|LSB>
BW <value>
STATUS
RSSI
SNR
```

Exact command syntax may change before implementation. Machine-readable output should be available (CSV or JSON lines) so M1 measurements can be logged without screen scraping.

## RF-quiet experiments

The controller harness should eventually support explicit test states for Wi-Fi/Bluetooth and CPU/display activity. M1.1 itself should start with unnecessary radios disabled.

## Rule

Do not build application/UI architecture into this harness. Keep it deterministic and disposable enough to serve RF qualification.
