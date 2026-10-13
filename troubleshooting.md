# Troubleshooting

## Upload problems

**"No port" / board not detected**

1. Try another USB cable — charge-only cables are the #1 cause.
2. Clone boards with the CH340 USB chip need the CH340 driver
   (search "CH340 driver" + your OS).
3. Try a different USB port; avoid unpowered hubs.

**"avrdude: stk500_recv(): programmer is not responding"**

The classic. Check in order: right board selected (Tools → Board →
Arduino Uno), right port, nothing wired to pins 0/1 (they share the
USB serial lines), then press the reset button and upload again
immediately.

**Upload worked but nothing happens**

- Is the *right* sketch uploaded? (We've all debugged yesterday's
  code.)
- `setup()` runs once — if your configuration is in `loop()` by
  mistake, or vice versa, behavior is bizarre.
- Add `Serial.println()` checkpoints — see [Serial](serial.md).

## Code problems

**Error points at the wrong line**

A missing `;` or `}` is reported where the compiler *noticed*, which
is usually the line *after* the mistake. Look upward.

**"was not declared in this scope"**

Typo in a variable/function name, or a missing `#include`. C++ is
case-sensitive: `ledPin` ≠ `ledpin`.

**"Multiple libraries were found for ..."**

Duplicate library installs — the compiler picks one and tells you
which. Remove the loser from the sketchbook's `libraries` folder.

**Weird numbers from analogRead()**

- Floating pin (nothing connected) reads random noise — that's
  normal, not broken.
- Integer division: `reading * 5 / 1023` does integer math. Use
  `5.0` to force decimals.

**The board resets randomly**

Usually power: USB ports on some hubs/computers sag under load.
Try a direct port or a powered hub. Also check for `String`
fragmentation in long-running sketches (see [How Sketches
Work](how-sketches-work.md)).

## Circuit problems

**LED doesn't light**

1. Resistor in series? (No resistor = dead LED, fast.)
2. LED polarity: long leg toward power, short leg toward GND.
   Backwards LEDs just sit there, silently judging.
3. Is the pin set `OUTPUT` in `setup()`?

**Button reads backwards / randomly**

- Using `INPUT` without an external pull-down resistor? The pin
  floats. Use `INPUT_PULLUP` (see [Digital I/O](digital-io.md)).
- Bouncing? Add the 50ms debounce.

**Sensor gives garbage**

- Wrong baud rate in the Serial Monitor (gibberish text).
- DHT: reads faster than every 2 seconds fail — respect the delay.
- HC-SR04: soft/angled surfaces, or a second sensor pinging nearby.

## The method

1. **Halve the problem.** Blink the built-in LED — board and upload
   work? Then it's your circuit. Doesn't blink? It's the board/cable/
   port.
2. **Serial print everything.** When in doubt, print the variable.
3. **Change one thing.** Rewire *or* re-upload, not both.
4. **Sleep on it.** Hardware bugs hide in plain sight at midnight.

**Next:** [Glossary](glossary.md)
