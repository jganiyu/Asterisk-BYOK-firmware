# Artifacts

## Firmware

`firmware/asterisk-byok-toggle-v6-circumflex-vowels-20261004.uf2`

- Board target: Asterisk
- Purpose: firmware-only BYOK compatibility update
- Preserves existing Javelin dictionary/data payload
- SHA256: `80efaebfd4cc03833b379f9082f655445e3892265c229d88e17c483bff4b799e`

## Toggle Dictionary

`dictionaries/javelin-toggles.json`

Includes:

- `SAOEUTSDZ/PWOBG` -> `{:set_ascii_output:on}`
- `SAO*EUTSDZ/PWOBG` -> `{:set_ascii_output:off}`
- Placeholder specialty-dictionary examples:
  - `SAOEUTSDZ/1` / `SAO*EUTSDZ/1`
  - `SAOEUTSDZ/2` / `SAO*EUTSDZ/2`

Replace `example-specialty-dictionary-1.json` and `example-specialty-dictionary-2.json` with your own dictionary filenames, or remove those entries if you only need BYOK character mode switching.

SHA256: `30b96a9ef79edfe1676ad464e0489fc3dc427953e6457d363c97dfe431deaf71`

## Companion Q&A

[Asterisk-BYOK Firmware Q&A](https://chatgpt.com/s/cx_6ac27267032081919be05cf355a41701)
