# Firmware Upgrade Menu

## Checking your current version

- Firmware V1.04+ added hardware and software revision display in the on-device menu.

## Update methods

- **SD card flash file**, via an on-device menu — no separate USB/serial flashing tool needed for routine updates.
- **As of firmware V1.0.8, the file format changed from `.FLH` to a signed/encoded `.EFW` format.** The updater validates the `.EFW` file's signature, format, and contents before writing to flash, rejecting invalid or incompatible files up front. Older `.FLH` files are no longer accepted once a unit is running V1.0.8 or later — keep them only for units you don't plan to update further.
- Pre-V1.0.8 firmware files were named like `CC3-BOARDV1-2-FW1-0-2.FLH` (board revision + firmware version encoded in the filename) and were board-revision-specific. From V1.0.8 onward, firmware is universal across board revisions — the board revision (1.2/1.3) is selected in the Firmware menu instead.

## Step-by-step update

**Routine update (already on V1.0.8 or later):**

1. Download the `.EFW` firmware file (see [firmware-changelog.md](../04-management/firmware-changelog.md) for the current release).
2. Copy the file to the **root of the SD card**.
3. On the device, press **F12** to open the **on-screen menu**, then **F** for the Firmware Upgrade menu (see [menu-navigation.md](menu-navigation.md)).
4. Select the **Flash Firmware** option from that menu and flash the new firmware.

**One-time transition to V1.0.8 (if you're still on V1.06 or earlier):** this requires two stages, since the old `.FLH`-based units can't jump straight to a `.EFW` file. See the [V1.0.8 entry in firmware-changelog.md](../04-management/firmware-changelog.md) for the full two-stage process — in short: flash the `.FLH` transition firmware first (same steps as above, old format), let the device restart, then flash the `.EFW` second-stage firmware (same steps, new format). The second stage is what adds the board-revision selector to the Firmware menu; skipping it isn't harmful, it just leaves a few non-functional V1.3-only menu options visible on V1.2 boards.

## Release notes / changelog

- Full firmware version history, download links, and per-version release notes: [firmware-changelog.md](../04-management/firmware-changelog.md)
- Track documentation (this repo) changes separately in [../CHANGELOG.md](../CHANGELOG.md)

## Rollback

- No manual rollback should normally be needed. The ESP32 has a **dual-firmware (A/B) setup**, and if an update fails, it automatically falls back to loading the previous firmware — this self-healing is designed to hold even if power is interrupted mid-flash.

## Risks

- Under normal use, bricking risk is very low thanks to the dual-firmware fallback described in [Rollback](#rollback) above. This isn't an absolute guarantee, though — it protects against a failed or interrupted update, not against a device that's been physically tampered with (e.g. modified flash storage/bootloader) or otherwise compromised outside normal operation.
- Known-fixed-in-V1.0.2: a file corruption issue when saving to disk existed in earlier firmware — update if you're on an older version.
