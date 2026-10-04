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
- `Lórien` → `Lorien`
- `Glo´in` → `Gloin`
- `Nazgûl` → `Nazgul`

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
