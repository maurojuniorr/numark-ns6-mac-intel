# Numark NS6 driver for Intel Macs

A community Core Audio and CoreMIDI driver for the original Numark NS6, targeting **Intel Macs (x86_64) running macOS Catalina 10.15 or later**. Numark's original driver provides native support on older macOS releases through Mojave; this separate userspace implementation targets Catalina and later.

This project adapts the protocol and initialization work from [maurojuniorr/numark-ns6-linux](https://github.com/maurojuniorr/numark-ns6-linux) and the macOS implementation in [maurojuniorr/numark-ns6-mac-arm64](https://github.com/maurojuniorr/numark-ns6-mac-arm64). It is an independent community project, not a Numark or Ploytec product.

> **Status: Intel port in progress.** The source is being cross-compiled for x86_64 with Catalina as the deployment target. The audio and MIDI behavior has been developed and tested on Apple Silicon, but this Intel build has not yet been verified on physical Intel hardware or across Catalina-and-later releases. Treat it as experimental until those tests are complete.

## What it provides

- A four-channel, 44.1 kHz Core Audio output device. Channels 1–2 are Master; channels 3–4 are Headphones, allowing DJ software to route them independently.
- CoreMIDI input and output for the NS6 controls and LEDs, coordinated with the audio USB session by a companion bridge.
- A status app showing USB connection, driver and firmware versions, audio format, and the active audio flow's buffer cycle.
- USB feedback-based audio clock scheduling and diagnostics for queue depth, callback timing, transfer health, and recovery.

The implementation follows the device's 44.1 kHz feedback and whole-frame USB packet cadence. Mixxx or another Core Audio client requests its own buffer period; the driver reports the period active in the current stream. Behavior and stability on Intel Macs still need hardware validation.

## Current limits

- **No audio capture input:** the macOS driver exposes output only. The NS6's physical inputs have not been implemented as Core Audio capture channels.
- The installer is unsigned and not notarized; macOS may ask you to approve it.
- Catalina 10.15 is the minimum deployment target. No claim of support below Catalina is made.
- The x86_64 build is not yet validated with real Intel NS6 hardware. Reports should include the Mac model, macOS version, driver build, DJ software, and audio settings.

## Architecture map

Graphify's generated architecture map is checked in under `graphify-out/`: open [`graph.html`](graphify-out/graph.html) for the interactive graph, inspect [`graph.json`](graphify-out/graph.json) for machine-readable nodes and edges, or read [`GRAPH_REPORT.md`](graphify-out/GRAPH_REPORT.md) for community summaries and extraction limitations. This is a snapshot of the current source tree; regenerate it after significant code or documentation changes.

## Build

Install Xcode Command Line Tools, then build the HAL driver, status app, and MIDI bridge:

```sh
cd coreaudio
make clean
make all ARCH=x86_64 MACOSX_DEPLOYMENT_TARGET=10.15 VERSION=0.1.0
make test
```

To create a local installer package:

```sh
make package ARCH=x86_64 MACOSX_DEPLOYMENT_TARGET=10.15 VERSION=0.1.0
```

The package is created under `coreaudio/dist/`. Do not install it on a performance system before testing it on the target Intel Mac. The development USB descriptor probe is separate from the driver and is not included in the package.

## Install and route audio

After installing and restarting Core Audio, select **Numark NS6** in System Settings → Sound → Output or in the DJ application's audio settings. In Mixxx, select the NS6 for audio and its CoreMIDI ports for the controller. Route Master to channels 1–2 and Headphones to channels 3–4.

The package installs an Intel-specific HAL bundle and **Numark NS6 Status (Intel)**, so its identifiers and paths do not collide with the Apple Silicon package. Do not install both distributions on the same Mac unless you are intentionally testing them side by side.

## Project background

The Linux project supplied the early vendor activation, SysEx initialization, initial state, and USB protocol work. The macOS ARM64 project established the Core Audio transport and developed the feedback-driven scheduling used as the basis for this Intel port.

**Acknowledgment — [Gregory Senay](https://github.com/GregorySenay).** His independent NS6 protocol research and hardware-verified findings helped clarify the `0x50`/`0x51`/`0x60` initialization exchange, the `0x81` feedback endpoint, and whole-frame audio packet scheduling. His work informed both the Linux investigation ([PR #4](https://github.com/maurojuniorr/numark-ns6-linux/pull/4)) and the macOS research at [GregorySenay/ns6-macos](https://github.com/GregorySenay/ns6-macos). This repository incorporates those findings through its own implementation.

## Contributing

Testing on Intel Macs running Catalina or later is especially useful. Please report the macOS version, Mac model, driver version, audio application, sample rate, buffer size, and any timestamps associated with audio artifacts or device disconnects. Contributions to code, testing, and documentation are welcome.
