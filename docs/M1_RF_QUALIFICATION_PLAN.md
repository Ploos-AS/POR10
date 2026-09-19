# POR10 M1 RF Qualification Plan

## Purpose
M1 converts the M0 RF concept into measured evidence. No filter bank, LNA or antenna-path choice is considered final until it improves the receiver in repeatable tests.

## Prototype under test

Candidate signal chain:

```text
external antenna
  -> input protection
  -> selectable attenuation
  -> preselection/filtering
  -> optional LNA
  -> matching
  -> Si473x

MW/LW ferrite path
  -> matching / optional low-noise stage
  -> Si473x
```

Build the prototype so that attenuation, filters, gain stages and matching networks can be bypassed or exchanged.

## Test equipment

Preferred:
- calibrated or characterized RF signal generator
- step attenuator or known attenuation
- oscilloscope
- DMM
- 50 ohm terminations/adapters
- second receiver or SDR for interference observation
- PC for automated logging

Useful but optional:
- spectrum analyzer
- VNA
- RF power meter
- near-field probes

Tests must record equipment/model, settings and limitations. Hobby-grade instruments are acceptable when their uncertainty is documented.

## Qualification matrix

Test representative points across:
- LW
- MW
- lower SW/HF
- mid HF
- upper HF near 30 MHz
- FM band

For each applicable point record:
- frequency
- mode/bandwidth
- injected level
- RSSI/SNR reported by receiver
- intelligibility/detection result
- front-end state
- power/network/display state

## Q1 — Baseline receiver
Measure the simplest safe Si473x path first. Establish a reference before adding gain or filtering.

PASS: repeatable reception/control and a documented baseline dataset.

## Q2 — Input protection
Verify that the selected protection network does not introduce unacceptable loss/capacitance across intended bands.

PASS: protection retained unless measurements show material degradation requiring redesign.

## Q3 — Attenuator
Evaluate at least bypass plus one useful attenuation state. Prefer simple, predictable values.

PASS: attenuation is repeatable and materially improves operation with strong input signals without excessive complexity.

## Q4 — Preselector/filter strategy
Compare bypass with candidate filtering. Test both weak-signal loss and strong out-of-band interferers.

PASS: selected filtering demonstrates a measurable benefit. Avoid an elaborate filter bank if a simpler network performs adequately.

## Q5 — LNA decision
Compare no-LNA and candidate LNA states.

PASS criterion is not “more RSSI.” An LNA is adopted only if weak-signal usability improves without unacceptable overload, noise, instability, power use or BOM impact. DNP/bypass must remain possible where practical.

## Q6 — Strong-signal behaviour
Inject/receive a wanted weak signal while introducing a strong nearby or out-of-band signal where equipment permits.

Record desensitization, false responses and recovery with attenuator/filter/LNA combinations.

## Q7 — Antenna paths
Qualify:
- external SMA path
- telescopic antenna concept/path where applicable
- ferrite MW/LW path prototype

Document matching assumptions and grounding/counterpoise behaviour.

## Q8 — Self-generated interference
Compare receiver noise/spurs with:
- Wi-Fi/Bluetooth off/on
- display normal/reduced activity
- USB connected/disconnected
- SD idle/activity
- candidate power-converter states
- CPU/network idle/load where practical

This produces the first evidence for DX/RF-quiet mode and PCB partitioning.

## Q9 — Repeatability
Repeat a reduced matrix after power cycles and configuration changes.

PASS: no unexplained state-dependent behaviour that invalidates earlier measurements.

## Required artifacts

- schematic of RF prototype
- BOM with exact tested parts
- photographs/layout notes
- test equipment inventory
- raw results in CSV/JSON where practical
- summarized qualification report
- explicit PASS/FAIL/DEFER for Q1–Q9
- decisions and rejected alternatives

## M1 exit criterion

M1 passes when POR10 has a measured RF architecture sufficient to begin controller/UI integration without hiding unresolved receiver-critical assumptions. Deferred items must have a reason and owner milestone.
