# Joysticks & Controllers

## Connector / interface

- **2× USB ports, USB Low Speed (1.5 Mbps) only in Soft USB mode (the default)** — not Full Speed (12 Mbps, most of USB 1.1) or High Speed (480 Mbps, USB 2.0+). Same constraint as keyboards — see [keyboards.md](keyboards.md#connector--interface) for the technical explanation and a possible ADuM4160-adapter workaround. This rules out most modern USB gamepads, which is why the community compiles confirmed-working controllers (often older/legacy models, or cheap ones from AliExpress) below.
- **As of firmware V1.0.8, an alternative "Native USB" mode exists** — see [below](#native-usb-mode-firmware-v108) — which uses the ESP32's own USB host and should improve compatibility with more USB devices, at the cost of only supporting one keyboard + one joystick at a time (instead of two joystick ports).
- Supports both **analog pads and digital controllers**.
- An **expansion port** on the side of the board accepts an optional joystick module that connects **standard/original CoCo joysticks** directly, bypassing USB entirely — see [hardware-specs.md](../01-getting-started/hardware-specs.md). This module (documented on-device as the "CoCo Port" joystick type) requires **board revision V1.3**.
- TODO: is any digital-to-analog mapping done internally for CoCo-style analog joystick emulation, or is it 1:1 passthrough for analog pads?

## Native USB mode (firmware V1.0.8+)

Firmware V1.0.8 introduced a second USB mode, as an alternative to the original software-emulated "Soft USB" stack:

- **Native USB mode** uses the ESP32-S3's own built-in USB host hardware instead of the Soft USB library. This should improve compatibility with a wider range of USB devices, since it isn't limited by the Soft USB stack's Low Speed (1.5 Mbps)-only restriction the same way — though the exact speed classes it supports haven't been independently confirmed yet.
- **Trade-off: only 2 USB devices total** — one keyboard and one joystick — can be connected at once in Native USB mode. Since only one joystick fits, the Joystick menu's **S** key swaps that single joystick between the CoCo's left and right ports (even mid-game) instead of using two independent ports — see [joystick-menu.md](../02-menus-and-shortcuts/joystick-menu.md#two-usb-modes-firmware-v108).
- **Soft USB mode** (the original, still the default) keeps its own independent per-port joystick configuration and doesn't show the swap option.

**Hardware needed to use Native USB mode** (reported by the doc maintainer, exact part interchangeability not independently verified):

1. A small USB hub — e.g. https://www.amazon.ca/dp/B09TDF9RTX
2. A micro-USB splitter cable **with power bypass** — e.g. https://www.amazon.ca/dp/B083M1S6QT

Connect the hub to the ESP32-COCO's USB port via the power-bypass splitter cable. This lets the hub (and whatever keyboard/joystick are plugged into it) run off the device's own native ESP32-S3 USB host instead of the software-emulated one.

## Known-working (community-sourced)

| Controller                                                               | Source            | Link                                                                                                                                    | Notes                                                                                               |
| ------------------------------------------------------------------------ | ----------------- | --------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------- |
| Unnamed USB joystick                                                     | AliExpress        | https://www.aliexpress.com/item/1005010597048106.html                                                                                   | Reported working. TODO: confirm product name/model — AliExpress listings can change or be delisted. |
| Logitech RumblePad 2                                                     | Legacy/secondhand | P/N 863247-0000 (no link — legacy device, check eBay/thrift)                                                                            | Reported working.                                                                                   |
| Logitech Wingman Action Pad                                              | Legacy/secondhand | Model 963247-0914, also part number G-UB3A (no link — legacy device)                                                                    | Reported working.                                                                                   |
| Rii Game Controller (Retro USB Controller)                               | Amazon            | https://www.amazon.com/dp/B073Z9MKKH                                                                                                    | Reported working.                                                                                   |
| USB SNES-style joypad ("Controller Classic Nintendo Computer Raspberry") | Amazon            | CA: https://www.amazon.ca/-/fr/dp/B075QJKBLV · US: https://www.amazon.com/Controller-Classic-Nintendo-Computer-Raspberry/dp/B075QJKBLV/ | Reported working.                                                                                   |
| Hyperkin "Scout" Premium USB Controller (PC/Mac)                         | Amazon            | https://www.amazon.com/dp/B0798GFM6V                                                                                                    | Reported working.                                                                                   |

## Buying guidance

- When shopping AliExpress/Amazon/secondhand for a compatible controller, older/basic USB gamepads are far more likely to negotiate at USB1 than modern USB2+ controllers — there's no reliable way to tell from a listing alone besides community reports, so treat the table above as the source of truth as it grows.
- A [Joystick Config Editor by Mike Horgan](../05-resources/utilities.md) is available to help set up a controller once connected.
- A [joystick testing .DSK image](../05-resources/media-library.md) from the creator is available to verify a controller works correctly.

## Tested & known-NOT-working

| Controller | Notes |
|---|---|
| TODO | TODO |

## Original CoCo joysticks

- Supported via the optional expansion-port joystick module — see [hardware-specs.md](../01-getting-started/hardware-specs.md). No adapter needed when using that module; not connected via USB.

## Number of ports

- 2 USB Low Speed joystick ports (2-player support via USB), plus the expansion port for original CoCo joysticks.

## See also

- [Joystick Menu](../02-menus-and-shortcuts/joystick-menu.md) — configuring axes/buttons on-device (including the axis-number gotcha)
