# Asterisk-BYOK Firmware

Custom Asterisk/Javelin firmware for using an Asterisk stenography keyboard directly with BYOK while preserving normal laptop/Plover workflows.

> **Start here:** Read the project overview below, then use the companion ChatGPT Q&A task for questions about how this works, how to use it, or what would be needed to adapt the approach for other Javelin keyboards:
>
> [Asterisk-BYOK Firmware Q&A](https://chatgpt.com/s/cx_6ac27267032081919be05cf355a41701)

## Project Overview

This project turned the Asterisk into a self-contained Javelin stenography keyboard that can be used both with BYOK and with a normal laptop setup.

## Firmware

Custom Asterisk/Javelin firmware was built so the device presents translated output as a simple standard USB keyboard. This solved the original BYOK issue where strokes produced unexpected numbers, symbols, or newlines.

A keyboard timing issue was also fixed, where Shift could linger after punctuation and accidentally capitalize following letters.

## Dictionaries

The original dictionary set and priority were preserved. The specialty dictionaries remain off by default, while the main dictionaries and toggle dictionary remain on.

Firmware-only updates were designed to preserve the large dictionary payload already flashed to the Asterisk.

## Simple And Accented Characters

One issue arose after the initial BYOK keyboard fix: BYOK could not handle certain accented or special characters and displayed them as `?`. The solution was to add a switchable output mode. In BYOK mode, unsupported accented or special characters are simplified into plain characters. In normal computer mode, the firmware preserves accented output using Mac-compatible key sequences where needed.

**BYOK mode:**
- Simplifies unsupported characters.
- `Lórien` -> `Lorien`
- `Glo´in` -> `Gloin`
- `Nazgûl` -> `Nazgul`

**Normal computer mode:**
- Preserves accented output.
- Confirmed output: `Gandalf Lórien Glo´in Nazgûl`

**Character mode switching:**
- `SAOEUTSDZ/PWOBG` = BYOK mode on
- `SAO*EUTSDZ/PWOBG` = BYOK mode off

## Javelin/Plover Switching

The Asterisk’s small **BOOTSEL** button, labelled `B`, has two roles:

- Hold `B` while plugging in to enter flash mode.
- Press `B` normally after boot to switch between embedded Javelin output and Plover-compatible HID mode.

## Conclusion

The final setup lets the Asterisk translate onboard, type directly into BYOK as a plain keyboard, preserve accented output on normal computers, and still retain a Plover-compatible mode for laptop workflows.

## Who This Is For

This firmware is intended for **Asterisk users already using Javelin** or users who can first build and flash a normal Javelin Asterisk setup with their own dictionaries.

The custom firmware in this repository is firmware-only. It does not contain your personal dictionaries. It expects the dictionary/data payload to already be installed on the Asterisk through the normal Javelin builder workflow.

## Files

- `firmware/asterisk-byok-toggle-v6-circumflex-vowels-20261004.uf2`  
  Final tested custom Asterisk BYOK firmware.

- `dictionaries/javelin-toggles.json`  
  Toggle dictionary entries for BYOK character mode on/off. The firmware also includes built-in support for these same two mode strokes.

- `docs/firmware-write-up.md`  
  Saved project write-up.

## How To Use This On An Asterisk

### If Your Asterisk Already Has Javelin And Dictionaries Installed

1. Unplug the Asterisk.
2. Hold the small **BOOTSEL** button labelled `B`.
3. While holding `B`, plug the Asterisk into USB.
4. Release `B` when the `RPI-RP2` drive appears.
5. Copy `firmware/asterisk-byok-toggle-v6-circumflex-vowels-20261004.uf2` onto the `RPI-RP2` drive.
6. Wait for the drive to disconnect and the Asterisk to reboot.

Your existing dictionaries should remain in place.

### If You Have Not Installed Javelin Dictionaries Yet

1. Use the original Javelin builder to build a normal Asterisk UF2 with your own dictionaries, dictionary order, and default states.
2. Flash that builder-generated UF2 first.
3. Then flash the custom firmware UF2 from this repository.

The first flash installs your dictionary/data payload. The second flash updates the firmware behavior while preserving that dictionary/data payload.

## Mode Reference

### BYOK Character Mode

- Turn on: `SAOEUTSDZ/PWOBG`
- Turn off: `SAO*EUTSDZ/PWOBG`

BYOK mode converts unsupported accented/special characters to simpler plain text.

### Embedded Javelin vs Plover HID

- Press the Asterisk’s `B` button normally after boot to switch between embedded Javelin output and Plover-compatible HID mode.
- Hold `B` while plugging in to enter flash mode.

## Notes For Other Javelin Keyboards

The core approach should be reusable, but this UF2 is for the Asterisk target. Other Javelin keyboards may need board-specific verification or firmware changes for:

- board target/configuration
- flash layout and dictionary region
- bootloader process
- USB descriptors
- Plover/Javelin mode switching
- available firmware space

For Asterisks using the same board target, this should be close to turnkey: users mainly need their own dictionary payload installed first.

## Checksums

```text
80efaebfd4cc03833b379f9082f655445e3892265c229d88e17c483bff4b799e  firmware/asterisk-byok-toggle-v6-circumflex-vowels-20261004.uf2
b2c17c7b502bb38eb44a074ff9690ac61984a0902ddede79894a3a46db888b19  dictionaries/javelin-toggles.json
```

