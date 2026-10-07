# Core Audio HAL driver

This directory builds the Intel x86_64 Core Audio HAL driver, the NS6 Status app, and the CoreMIDI bridge for macOS Catalina 10.15 and later.

The HAL device exposes four 44.1 kHz Float32 output channels. Channels 1–2 feed Master and channels 3–4 feed Headphones. Core Audio clients can request the buffer frame size they use; the driver reports the active stream period to the Status app. The USB worker handles packed 24-bit samples, device feedback, whole-frame packet scheduling, queue management, and transfer recovery.

The code is based on the ARM64 driver and is being ported to Intel. Cross-compilation does not prove the USB transport works on an Intel Mac. Hardware validation on Catalina and newer is still required. Audio capture is not implemented.

## Build and tests

```sh
make clean
make all ARCH=x86_64 MACOSX_DEPLOYMENT_TARGET=10.15 VERSION=0.1.0
make test
```

Build an installer with `make package` after validating the build. The package installs `NumarkNS6Intel.driver`, **Numark NS6 Status (Intel)**, and the Intel MIDI bridge. It restarts Core Audio during installation.
