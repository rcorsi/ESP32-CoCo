# Firmware Changelog

Version history for ESP32-COCO device firmware. For how to actually flash a `.FLH` file, see [firmware-upgrade-menu.md](../02-menus-and-shortcuts/firmware-upgrade-menu.md).

> Ordering note: versions are listed newest-first based on feature accumulation (V1.04 includes capabilities not present in V1.0.2's notes). TODO: confirm exact version numbering/order and whether "V1.04" is shorthand for "V1.0.4", plus fill in any versions between/before/after these.
> **Current published firmware: V1.06**, distributed via GitHub Releases (a shift from the earlier Google Drive links) — https://github.com/mast4rbug/ESP32-CoCo/releases/tag/1.06
> **V1.05 existed but was never published** — superseded by V1.06 below.
> **Firmware now forks per board revision**, as expected — V1.06 ships as separate builds for board V1.2 (no HDMI) and board V1.3 (HDMI + Cassette port). See [hardware-specs.md](../01-getting-started/hardware-specs.md) for the board differences.
> **Cross-flashing is safe.** Any firmware version can be loaded on either board revision — it won't damage the board, you'll just end up with menu options for features that board doesn't physically support.

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
