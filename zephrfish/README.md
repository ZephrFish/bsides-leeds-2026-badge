# ZephrFish firmware

A custom build of the BSides Leeds 2026 "Artie the Owl" badge firmware
(**ATtiny814**, 18× SK6812 RGB LEDs). Built from [`firmware.ino`](firmware.ino);
the unmodified upstream version is in
[`../original-firmware/`](../original-firmware).

> The badge is meant to be explored and reverse-engineered - half the fun is
> working it out yourself. So this README only covers the cosmetic tweaks in
> this build and deliberately doesn't document how the stock badge behaves.
> No spoilers here.

> Want your own? Add a folder named after your handle (e.g. `yourname/`) with a
> `firmware.ino` inside - CI compiles every author folder and reports its flash
> usage automatically.

| File | Description |
|------|-------------|
| `firmware.ino` | Custom firmware source |
| `firmware.hex` | Intel HEX image - flash with megaTinyCore over UPDI |
| `firmware.bin` | Raw binary (8094 bytes) |

Flash footprint: **8094 / 8192 bytes**.

## What this build changes

Purely cosmetic LED tweaks on top of the stock firmware:

- A **ZephrFish Morse** signature shown at power-up - cyan dots, purple dashes.
- An **animated pride rainbow**.
- A **red/blue split** with purple where the two meet.
- A few of the existing idle animations **recoloured** to purple / cyan / orange.

That's it - everything else about the badge is left for you to discover.

## Building

```sh
arduino-cli core install megaTinyCore:megaavr
mkdir -p build/firmware && cp firmware.ino build/firmware/
arduino-cli compile --fqbn megaTinyCore:megaavr:atxy4:chip=814 build/firmware
```

CI rebuilds on every push, reports flash headroom, and attaches the compiled
firmware to the [latest release](../../releases/latest).
