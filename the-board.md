# The Board

A tour of the Arduino Uno R3 — the blue board with the silver USB
port. Everything has a label; here's what the labels mean.

## The headline features

- **USB port** — connects to your computer. Uploads programs *and*
  powers the board. One cable does everything while you're learning.
- **Reset button** — restarts your program from the beginning. Your
  best friend during debugging.
- **Power jack / Vin pin** — for running without USB (7–12V
  recommended into the jack).
- **The main chip** — the ATmega328P microcontroller, the brains.
  (On official Unos it's the long black chip you can actually pop
  out and replace.)

## The pins: where wires go

Pins are the numbered holes along the edges. They fall into groups:

| Group | Pins | What they do |
|-------|------|--------------|
| Digital | 0–13 | Read/write on/off signals. Pins 3, 5, 6, 9, 10, 11 (marked `~`) also do PWM "analog" output |
| Analog in | A0–A5 | Read varying voltages (sensors, knobs) |
| Power | 5V, 3.3V, GND | Power your circuits. **GND** (ground) is the reference everything measures against |
| Special | TX/RX (0,1), SDA/SCL, etc. | Serial and sensor buses — later chapters |

**The built-in LED** is on pin 13 (marked `L` on the board). Your
first program blinks it — no wiring needed.

## Three rules of pins

1. **Never connect 5V directly to GND.** That's a short circuit —
   the board will get hot and unhappy. (Resistors exist to prevent
   exactly this.)
2. **Digital pins handle ~20mA each, 200mA total.** An LED is fine.
   A motor is not — motors get their own power and a transistor or
   driver board. (More in [Power and Wiring](power-and-wiring.md).)
3. **Pins 0 and 1 are shared with USB serial.** If uploads fail
   mysteriously, disconnect whatever's wired to pins 0/1 first.

## Clones vs. official boards

Official Unos cost ~$25; clones cost ~$10 and work identically for
learning. The one gotcha: some clones use a different USB-serial
chip (CH340 instead of the official one) and need a driver on some
systems. If your computer doesn't see the board, that's the first
thing to check — see [Troubleshooting](troubleshooting.md).

**Next:** [Getting Set Up](getting-set-up.md)
