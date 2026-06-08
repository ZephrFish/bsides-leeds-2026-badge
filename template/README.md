# Firmware template

A starting point for writing your own badge firmware.

## Start your own

1. Copy an existing folder as your base, e.g. `cp -r ../original-firmware ../yourhandle`
   (or `../zephrfish`), and rename the folder to your handle.
2. Edit `yourhandle/firmware.ino`.
3. Open a PR. CI compiles every author folder automatically and tells you how
   much of the badge's flash you've used (the limit is 8192 bytes, and it is
   tight), so you'll know straight away if your build fits.

## Writing an animation ("free function")

Each animation is a plain free function: it receives the frame counter `step`
and returns how many milliseconds to wait before the next frame. Light some
LEDs, call `show()`, return a delay:

```cpp
uint8_t myMode(uint16_t step)
{
  setAllLeds(0, 0, 0);                                  // clear all LEDs
  ledStrip.setPixelColor(step % NUM_LEDS, 20, 0, 30);   // one purple LED, moving
  ledStrip.show();
  return 100;                                           // 100 ms until next frame
}
```

Then add it to the `runAnimationMode(mode, step)` switch as the next free `case`:

```cpp
case 14:
  return myMode(step);
```

## Handy helpers

| Helper | Does |
|--------|------|
| `setAllLeds(r, g, b)` | set every LED to one colour |
| `ledStrip.setPixelColor(i, r, g, b)` | set LED `i` (0..NUM_LEDS-1) |
| `ledStrip.show()` | push the buffer to the LEDs |
| `NUM_LEDS` / `LEDS_PER_EYE` | 18 total / 9 per eye |

Keep brightness low (single digits up to ~30 per channel) - 18 LEDs at full
white pulls a lot of current from a coin cell.

Have fun, and keep it cosmetic - the rest of the badge is for everyone to figure
out for themselves.
