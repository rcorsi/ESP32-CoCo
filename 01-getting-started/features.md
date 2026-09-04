# Features

## Capability matrix

| Feature | Status | Notes |
|---|---|---|
| CoCo 3 emulation | Confirmed | Emulates a CoCo 3 with 2 MB of RAM, backward compatible with CoCo 1 and CoCo 2 software. There is no separate CoCo 1 or CoCo 2 mode. See [hardware-specs.md](hardware-specs.md). |
| Selectable CPU core (MC6809 / HD6309) | Confirmed (firmware V1.0.8+) | See [overview.md](overview.md#what-it-emulates) |
| DSK (floppy) loading | Confirmed | see [disk-menu.md](../02-menus-and-shortcuts/disk-menu.md) |
| Cassette loading | Confirmed | Virtual `.WAV` playback from SD card (all boards), or a real cassette deck via the CAS/CTL jacks (V1.3 only) — see [cassette-menu.md](../02-menus-and-shortcuts/cassette-menu.md) |
| Cartridge / ROM pak emulation | Not supported yet — planned for a future firmware update | Not the same thing as the Xternal ROM feature below, which is for RSDOS boot ROM variants, not Program Pak ROMs |
| Hi-Res Interface & CoCo Mouse | Not supported | No current plan to support it, but possible in a future update |
| Xternal ROM (custom RSDOS boot ROM) | Confirmed (firmware V1.0.8+) | Boot from a custom 8K RSDOS ROM variant on the SD card instead of the built-in ROM. Not intended for Program Pak/cartridge ROM dumps — see [menu-navigation.md](../02-menus-and-shortcuts/menu-navigation.md) |
| Joystick support | Confirmed | 2× USB Low Speed ports in Soft USB mode (default), or 1 joystick in Native USB mode (firmware V1.0.8+); analog + digital — see [joysticks-and-controllers.md](../03-compatible-hardware/joysticks-and-controllers.md) and [joystick-menu.md](../02-menus-and-shortcuts/joystick-menu.md) |
| Keyboard support | Confirmed | USB Low Speed (1.5 Mbps) only in Soft USB mode; Native USB mode (firmware V1.0.8+) may support more — see [keyboards.md](../03-compatible-hardware/keyboards.md) |
| SD card storage | Confirmed | FAT32 required |
| On-screen menu / OSD | Confirmed | see [menu-navigation.md](../02-menus-and-shortcuts/menu-navigation.md) |
| Save states | Confirmed (firmware V1.04+) | F3 save / F4 load, 36 slots (0–9, A–Z) |
| Screenshot capture | Confirmed (firmware V1.04+) | F9 saves incremental `PICTUREXXXX.BMP` to SD card root |
| Artifact mode toggle | Confirmed (firmware V1.0.2+) | F10 toggles BLUE-RED / RED-BLUE artifact colors |
| Vsync enable/disable | Confirmed (firmware V1.0.2+) | improves compatibility with Twilight Terminal, reduces flicker |
| RS-232 PAK hardware serial | Confirmed (firmware V1.0.2+) | see [modem-menu.md](../02-menus-and-shortcuts/modem-menu.md) |
| WiFi / Telnet BBS bridge | Confirmed (firmware V1.0.2+) | see [modem-menu.md](../02-menus-and-shortcuts/modem-menu.md) |
| Firmware updates | Confirmed | flashed from SD card via F12 menu; signed `.EFW` format as of V1.0.8 (was `.FLH`) — see [firmware-upgrade-menu.md](../02-menus-and-shortcuts/firmware-upgrade-menu.md) |
