# Power and Wiring

This is the chapter that keeps the magic smoke inside the chips.
Read it before wiring anything beyond an LED.

## The breadboard

The white plastic board with holes: **solderless breadboard**. Holes
in each half-row of 5 are connected underneath; the long outer rails
(usually marked red/blue) run the full length for power. Components
push in, no soldering.

**The #1 breadboard mistake:** the center groove splits the board —
rows don't connect *across* the gap. A wire that "should" connect
but crosses the groove connects to nothing.

## The resistor: your current limiter

Resistors are read by colored bands. For LEDs with 5V, **220Ω**
(red-red-brown) is the standard choice:

- 5V ÷ 220Ω ≈ 23mA — hmm, that's the *unloaded* math; the LED drops
  ~2V itself, so real current is ~(5−2)/220 ≈ 14mA. Safely under the
  pin's ~20mA limit either way.

You don't need to memorize the bands — phone apps and web
calculators decode them. You need to know *that every LED gets one*.

## Power limits (the numbers that matter)

| Limit | Value | Meaning |
|-------|-------|---------|
| Per digital pin | ~20mA | One LED: fine. A motor: no. |
| All pins combined | ~200mA | The chip's total budget |
| 5V pin output | ~500mA (USB) | Powers small sensors/displays |
| Board input (jack) | 7–12V recommended | The regulator wastes the rest as heat |

**Careful — the motor rule:** Motors (even tiny ones) draw
hundreds of mA and generate voltage spikes when they stop. **Never
power a motor from an Arduino pin.** Use a separate power supply and
a transistor or motor-driver board (L293D, L298N); the Arduino only
sends the *signal*. Wiring a motor straight to a pin is the fastest
way to kill a board.

**Careful — the short rule:** 5V straight to GND with no load is a
short circuit. The board's polyfuse *usually* saves it, but "usually"
is doing heavy lifting — double-check power wiring before plugging
in USB.

## Powering projects without USB

- **7–12V into the barrel jack** — the onboard regulator makes 5V.
  Above 12V the regulator overheats.
- **5V into the 5V pin** — bypasses the regulator (efficient, but no
  protection — get the polarity right).
- **Batteries** — a 9V battery works but dies fast (low capacity);
  4×AA or a USB power bank lasts far longer.

## Wiring checklist (before power-on)

1. 5V and GND go where they should — no swaps.
2. Every LED has its resistor.
3. No bare wire ends touching each other.
4. Pins 0/1 free if you're about to upload.
5. Unplug USB while rewiring — live rewiring slips, slips short.

**Next:** [Troubleshooting](troubleshooting.md)
