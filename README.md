# bitEngine Hub — EFR32MG24 Zigbee NCP firmware

Zigbee 3.0 coordinator firmware for the **Silicon Labs EFR32MG24** in the
[bitEngine Hub](https://home.bitengine.tech). The MG24 runs Silicon Labs **EmberZNet** as a
Network Co-Processor (NCP) and speaks **EZSP** over UART to the hub's ESP32-C5, which exposes it to
Home Assistant as EZSP-over-TCP on port `6638` (ZHA, Zigbee2MQTT `ember`).

> **Status: pre-release.** Project files and the first release images follow the ESP32-C5
> source release in **November 2026**.

- Host-side firmware (ESP32-C5): [bitengine-hub-firmware](https://github.com/bitEngineTech/bitengine-hub-firmware)
- Hardware: [bitengine-hub-hardware](https://github.com/bitEngineTech/bitengine-hub-hardware)

## What is in this repository

| Path | Contents | License |
|---|---|---|
| `project/` | Simplicity Studio project (`.slcp`), component selection and configuration for the EmberZNet NCP (UART / EZSP) | Apache-2.0 |
| `bootloader/` | Gecko Bootloader project and configuration used on the hub | Apache-2.0 |
| `docs/` | Rebuild and flashing instructions, version history | Apache-2.0 |
| **Releases** | Pre-built `.gbl` images, with EmberZNet and EZSP protocol versions in the release notes | Silicon Labs MSLA (see below) |

## What is *not* in this repository, and why

The Zigbee stack itself — EmberZNet, part of the Silicon Labs SDK — is proprietary to Silicon Labs
and distributed under the
[Silicon Labs Master Software License Agreement](https://www.silabs.com/about-us/legal/master-software-license-agreement)
(MSLA). We cannot relicense or redistribute its source. What we can and do publish:

- the complete **project and configuration** needed to rebuild the NCP image yourself with the
  freely available Silicon Labs SDK (Simplicity Studio);
- the **pre-built images** we ship, so you can reflash or roll back;
- **flashing and update instructions**.

Home Assistant talks to the radio over standard EZSP; no proprietary host-side software is
involved. This is the same model used by other EmberZNet-based coordinators in the Home
Assistant ecosystem.

## Rebuilding the image

1. Install Simplicity Studio 5 and the Simplicity SDK version pinned in `project/README.md`.
2. Import the project from `project/`.
3. Build. The resulting `.gbl` can be flashed as described in `docs/`.

The exact SDK version, component list and build options are recorded with each release so that
a given release image can be reproduced.

## Flashing and updates

- From the hub: the ESP32-C5 updates the MG24 over their UART link using the Gecko Bootloader;
  official images are applied through the hub's updater.
- Direct programming: see the hardware repository for the MG24 programming interface.
- The MG24 remains fully user-flashable — you can build and flash your own NCP image.

Step-by-step instructions will be published with the first release.

## Versions

| Release | EmberZNet | EZSP protocol | Notes |
|---|---|---|---|
| — | — | — | First release with the November 2026 source drop |

## License

Copyright 2026 bitEngine.

The project files, configuration and documentation in this repository are licensed under the
Apache License, Version 2.0 — see [LICENSE](LICENSE).

Pre-built images contain Silicon Labs code and are distributed under the terms of the Silicon
Labs MSLA, for use on Silicon Labs devices only — see [NOTICE](NOTICE).
