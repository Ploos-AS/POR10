# POR10 RF Interface Specification — M0

## Scope
Defines the boundary between POR10's RF subsystem and the controller/platform. It intentionally does not freeze an unmeasured front-end topology.

## RF inputs

### External antenna
- connector target: SMA female
- intended for external receiving antennas
- input protection required
- external DC must not be assumed
- a future bias-tee is out of v1 scope unless separately protected and qualified

### Portable/telescopic antenna
A mechanically practical telescopic antenna is required for portable use. Sharing the external path is acceptable if switching/matching remains understandable and robust.

### MW/LW ferrite
Provide an architectural path for a ferrite rod antenna. Exact winding/matching and active/passive implementation are M1 decisions.

## Controllable RF states

The controller architecture shall budget control for:
- attenuation bypass/state(s)
- preselector/filter selection where implemented
- LNA enable/bypass where implemented
- antenna/path selection where implemented

A safe deterministic default state is required at boot.

## Receiver abstraction

Firmware above the device driver should operate on capabilities rather than assuming one exact chip revision. Candidate capabilities:
- tune frequency
- mode
- bandwidth
- seek
- RSSI
- SNR
- RDS
- SSB/BFO-related controls where available

Unsupported capabilities must fail cleanly rather than being emulated misleadingly.

## RF quiet contract

The RF subsystem and platform shall permit a low-noise operating state. Network radios, display activity, SD writes and power-converter behaviour are platform variables to characterize in M1/M8.

## PCB implications

- physical separation of RF and high-speed digital sections
- short RF paths
- continuous/intentional grounding strategy
- controlled return paths
- test points that do not unnecessarily compromise RF nodes
- keep display/SD clocks and switch-mode power nodes away from antenna/receiver sections
- allow bypass/DNP options for experimental front-end stages on early revisions

## Safety / robustness

POR10 is a receiver, not a measurement instrument or lightning protector. Documentation must state that external antennas require appropriate installation practices and disconnection/protection for hazardous conditions. The PCB input protection is for realistic receiver abuse/ESD mitigation, not lightning survival.
