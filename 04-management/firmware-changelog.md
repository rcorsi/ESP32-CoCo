# Firmware Changelog

Version history for ESP32-COCO device firmware. For how to actually flash a firmware file, see [firmware-upgrade-menu.md](../02-menus-and-shortcuts/firmware-upgrade-menu.md).

> Ordering note: versions are listed newest-first based on feature accumulation (V1.04 includes capabilities not present in V1.0.2's notes). TODO: confirm exact version numbering/order and whether "V1.04" is shorthand for "V1.0.4", plus fill in any versions between/before/after these.
> **Current published firmware: V1.0.8** — https://github.com/mast4rbug/ESP32-CoCo/releases/tag/Firmware
> **As of V1.0.8, firmware is universal across board revisions** — a single build now supports both V1.2 and V1.3, with the board revision selected in the Firmware menu instead of being baked into separate per-board files. See [Revisions](../01-getting-started/hardware-specs.md#revisions).
> **File format changed from `.FLH` to `.EFW`** as of V1.0.8 — see the V1.0.8 entry below for the required two-stage update process, and [firmware-upgrade-menu.md](../02-menus-and-shortcuts/firmware-upgrade-menu.md) for the full flashing procedure.
> **V1.05 existed but was never published** — superseded by V1.06.
> **Cross-flashing was safe for V1.06 and earlier** (any `.FLH` version could be loaded on either board revision without damage). This still applies for the V1.0.8 transition step — see below — but going forward, firmware is universal, so the question no longer applies.

## V1.0.8 — Universal firmware (all board revisions)

Release: https://github.com/mast4rbug/ESP32-CoCo/releases/tag/Firmware

Major release. Highlights:

- **Selectable CPU core**: the emulator can now run either the **Motorola MC6809** or the **Hitachi HD6309** processor, selectable from the emulator menu. The selected core is prepared at startup (rather than checked on every instruction/timer tick) for better performance. The HD6309 implementation also received execution optimizations, and the MC6809 build's compiler optimization settings were corrected.
- **New "Xternal ROM" menu**: boot from the built-in ROM, or a custom 8192-byte ROM file stored in a `ROM` folder on the SD card. The selected source and filename are remembered in the config. **Intended use is swapping in different 8K RSDOS ROM variants — not for loading ROMs extracted from CoCo Program Paks/cartridges.** Some 8K Program Pak ROM dumps have reportedly worked anyway, but that's not a supported or guaranteed use case.
- **Joystick menu redesigned** around two USB modes:
  - **Native USB mode** (new — uses the ESP32's built-in USB host instead of the software "Soft USB" stack): supports at most **2 USB devices at once — one keyboard and one joystick**. Since only one joystick can be connected at a time, the **S** key now swaps that joystick between the CoCo's left and right joystick ports (works even mid-game) instead of needing two separate USB ports/configs.
  - **Soft USB mode** (the original mode): keeps its own independent joystick configuration and does not show the Native USB swap option.
  - Hardware revision 1.3 keeps the optional physical CoCo joystick interface option; revision 1.2 automatically hides menu options for hardware it doesn't have.
  - See [Native USB hardware setup](../03-compatible-hardware/joysticks-and-controllers.md#native-usb-mode-firmware-v108) for the hub + splitter cable needed to use Native USB mode.
- **Cassette menu**: boards with the physical cassette port can now select Virtual Tape or the physical port directly from the cassette menu; boards without that hardware stay in Virtual Tape mode automatically.
- **Board revision (1.2 / 1.3) is now selectable from the Firmware menu** and saved to the ESP32's non-volatile storage — the menu and available features then adjust automatically for the selected revision.
- **New signed/encoded `.EFW` firmware file format.** The updater validates the file's signature, format, and contents before touching the flash — invalid or incompatible files are rejected before installation starts.
- Fixed a garbage line that could appear at the bottom of the display when artifact colors were disabled.
- Improved PIA register behavior.
- Fixed the GIME vertical-border FIRQ status to correctly identify the interrupt source.
- General stability work across menus, Native USB support, joystick handling, and firmware configuration.

**Important — file format transition and two-stage update:** after this update, the old `.FLH` format is no longer accepted for future updates — it's replaced by the signed `.EFW` format, which the device validates before flashing. Archive old `.FLH` files for older/unupdated units only; don't use them for any update after this one.

Updating to V1.0.8 is a **two-stage process**:

1. Install the **transition firmware** using the old `.FLH` format (this is still how existing units take the first step). The device restarts.
2. Install the **second firmware** using the new `.EFW` format. This second stage adds the board-revision (1.2/1.3) selection to the Firmware menu.

If you stop after stage 1 and skip stage 2, the unit keeps working normally — a V1.2 board will just show a few menu options meant only for V1.3 hardware. Those are harmless but non-functional on V1.2. After both stages are done, all future updates must use `.EFW` files.

See [firmware-upgrade-menu.md](../02-menus-and-shortcuts/firmware-upgrade-menu.md) for the step-by-step flashing procedure.

## V1.06 — Board Revision V1.2 and V1.3 (separate builds)

Release: https://github.com/mast4rbug/ESP32-CoCo/releases/tag/1.06

- **CoCo 3 emulation now runs at full speed** (previously ~80% speed).
- Fixed a minor Timer bug (FF93).
- Added support for the new game port of **Montezuma's Revenge** (ported by Lee Perkins).

## V1.04 — Board Revision V1.2

- Added hardware and software revision display in the menu.
- Added **F9** to save a screenshot — saved to SD card root as incremental `PICTUREXXXX.BMP`.
- Added **Save State** (F3) and **Load State** (F4) — save/load game or work progress, or use for fast-loading. 36 slots available (0–9, A–Z).
- Added Disk menu option to create a new, formatted `.DSK` file.
- Added Disk menu **FORMAT** option to format an existing `.DSK` file.
- Added **DEL** key to remove/eject a disk from any drive (0–3).

## V1.0.2 — Board Revision V1.2

File: `CC3-BOARDV1-2-FW1-0-2.FLH`
Download: https://drive.google.com/file/d/1Avexaa-GsFraal4dFbb2e44r8fiGZH3m/view

**Flashing instructions:** copy the file to the root of the SD card, then flash it via the Flash Firmware menu (**F12**).

**Changes:**

- Fixed file corruption issue when saving to disk.
- Fixed screen centering (was shifted too far right).
- Fixed display bug when loading from cassette.
- Added **F10** to toggle between artifact modes (BLUE-RED / RED-BLUE).
- Added Vsync enable/disable (better compatibility with Twilight Terminal, less flickering).
- Added RS-232-PAK modem support via the hardware serial port.
- Added RS-232-PAK ↔ WiFi bridge for Telnet BBS connections.
- Added **F11** to exit data mode and return to command mode (WiFi mode only).
- Fixed various minor bugs.

See [modem-menu.md](../02-menus-and-shortcuts/modem-menu.md) for full detail on the RS-232/WiFi features this version introduced.

## Earlier versions

- TODO: no earlier firmware versions documented yet.
