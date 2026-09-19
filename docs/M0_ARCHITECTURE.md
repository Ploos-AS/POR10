# POR10 M0 System Architecture

## Functional block diagram

```text
 Antennas
    |
    v
 Protection -> Attenuator -> Filter / Preselector -> [optional LNA]
    |                                             |
    +---------------- RF module boundary --------+
                                                  v
                                             Si473x RF
                                                  |
                    +-----------------------------+------------------+
                    | control                                        | audio
                    v                                                v
                ESP32-S3 <---- microSD                         Audio path
               /   |   \                                          /    \
          Display Controls Local API                          Speaker   Phones/Line
               |       |
          Engineering  USB / Wi-Fi / MQTT / Web / Metrics
               |
        diagnostics / logs

 USB-C ---> power/charge/protection ---> system rails ---> replaceable battery
```

## Architectural rules

1. The receiver remains fully operational with Wi-Fi and Bluetooth disabled.
2. RF and noisy digital/power domains are deliberately partitioned.
3. RF-quiet/DX operation is designed into hardware and firmware rather than added later.
4. Integrations consume a common local control/state interface; Home Assistant or Prometheus logic does not enter the radio core.
5. Expansion interfaces are documented and electrically protected where practical.
6. Optional cost/features should prefer DNP footprints or modules rather than multiplying PCB variants.
7. v1 remains receive-only.

## RF module boundary

The first implementation is Si4732/Si4735-class, but the controller/UI platform should not unnecessarily depend on Si473x-specific electrical assumptions. M1 must determine the practical front-end through measurement.

Candidate chain:

```text
SMA/telescopic -> protection -> switchable attenuation -> filtering/preselection
               -> optional LNA -> matching -> receiver

ferrite MW/LW -> matching / optional low-noise stage -> receiver
```

The exact filter bank, LNA and antenna switching implementation is intentionally not frozen in M0.

## Software layering

```text
UI / buttons / encoder
        |
Radio application + state model
        |
Receiver abstraction + services
        |
Drivers / ESP-IDF
        |
Hardware

Application state/events
        |
        +-- USB control
        +-- local Web/API
        +-- MQTT / Home Assistant Discovery
        +-- Prometheus metrics
        +-- logging/recording
```

## RF-quiet mode

DX mode should provide a deterministic path to a quieter receiver state. Candidate actions include disabling Wi-Fi/Bluetooth, suspending network services, lowering display update rate/backlight activity, avoiding unnecessary SD writes, and selecting suitable receiver/front-end settings. M8 measurements decide which actions genuinely improve reception.

## Observability

Prometheus is for operational telemetry, not raw spectrum storage. Long-lived radio observations belong in SD logs/export formats. Metrics should avoid high-cardinality dimensions such as arbitrary frequency values as labels.

## Home Assistant

MQTT Discovery is the preferred first integration because it keeps HA-specific code small and makes the MQTT interface useful to Node-RED and custom automation at the same time.

## Expansion philosophy

Expose useful maker interfaces without turning the PCB into an unprotected development board. Headers/test pads should be clearly labelled and documented. Future RF boards and optional GPS are anticipated, but must not inflate the v1 base BOM unnecessarily.
