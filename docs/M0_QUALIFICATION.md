# POR10 M0 Closure Review

**Result: PASS**

M0 establishes a sufficient architectural baseline to begin M1 RF prototyping without pretending that unmeasured RF choices are final.

## Exit criteria review

| Criterion | Evidence | Result |
|---|---|---|
| Product scope and v1 boundary | README, M0 requirements | PASS |
| Receive-only v1 defined | README, M0 requirements | PASS |
| Band/mode targets defined | M0 requirements | PASS |
| High-level architecture | M0 architecture | PASS |
| RF subsystem boundary | M0 RF interface | PASS |
| RF-sensitive choices intentionally deferred to measurement | M0 component plan, M1 qualification plan | PASS |
| Controller/display/control classes | M0 component plan | PASS |
| Logical GPIO/interface budget | M0 pin budget | PASS |
| Audio/power direction | M0 requirements/component plan | PASS |
| Offline-first/network-optional rule | M0 architecture/requirements | PASS |
| Home Assistant/MQTT and Prometheus architecture | M0 architecture/requirements | PASS |
| DX/RF-quiet concept | M0 architecture/requirements | PASS |
| Expansion philosophy | M0 architecture/RF interface | PASS |
| Cost envelope | M0 BOM target | PASS |
| Licensing policy | README/M0 requirements | PASS |
| M1 qualification gates | M1 RF qualification plan | PASS |

## Decisions frozen for M1

- Project/model: POR10 — Ploos Open Radio 10
- maker-friendly, repairable open hardware
- ESP32-S3-class controller platform
- Si4732/Si4735-class first receiver implementation
- receive-only v1
- physical controls and non-touch IPS
- external antenna plus portable antenna support
- MW/LW ferrite path in architecture
- USB-C, replaceable single-cell 18650-class power concept
- microSD
- optional Wi-Fi/Bluetooth; radio remains complete offline
- common local state/control layer for integrations
- MQTT/Home Assistant Discovery and Prometheus are planned integrations
- target BOM <= EUR 60; > EUR 75 triggers redesign review

## Deliberately not frozen

These require measurement/prototyping:
- exact Si473x sourcing/variant
- exact display module/controller
- protection network values
- attenuator topology/value(s)
- preselector/filter topology
- LNA inclusion/topology
- ferrite matching
- final power-regulator topology
- final audio amplifier/headphone implementation
- exact GPIO map
- PCB dimensions/enclosure

These are not M0 failures; freezing them now would violate the measurement-first design strategy.

## M1 entry condition

**SATISFIED.**

Proceed to RF prototype design and Q1 baseline receiver qualification using `docs/M1_RF_QUALIFICATION_PLAN.md`.

## M0 conclusion

**M0 PASS — architecture and requirements baseline complete.**
