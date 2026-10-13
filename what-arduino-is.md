# What Arduino Is

**The one-sentence version:** Arduino is a tiny computer designed to
interact with physical things — lights, buttons, sensors, motors —
programmed in a simplified form of C++.

## Microcontroller vs. your computer

Your laptop is a general-purpose machine: it runs an operating
system, juggles dozens of programs, and has gigabytes of memory. A
**microcontroller** is the opposite philosophy — one chip containing
a processor, a little memory, and input/output pins, running *one*
program, forever, with no operating system at all.

| | Your computer | Arduino Uno |
|---|---|---|
| Processor | GHz, multiple cores | 16 MHz, one core |
| Memory | Gigabytes | 2 KB of RAM (yes, KB) |
| Storage | SSD, terabytes | 32 KB for your program |
| Operating system | Windows/macOS/Linux | None — your program *is* the OS |
| Power | Watts | Milliwatts (runs months on a battery) |
| Price | Hundreds+ | ~$25 (clones less) |

The Uno's specs look like a joke until you realize what it's *for*.
Reading a temperature sensor every second doesn't need gigahertz —
it needs to be cheap, reliable, and sip power. Your thermostat,
microwave, and car have dozens of microcontrollers in them right now.

## What "Arduino" actually refers to

Three things share the name, which confuses beginners:

1. **The boards** — physical hardware (Uno, Nano, Mega, and newer
   ones like the Uno Q with far more power).
2. **The IDE** — the free programming software.
3. **The ecosystem** — the language (simplified C++), the libraries,
   and the enormous community. This is the real product: whatever
   you want to build, someone has built something like it and shared
   the code.

This guide uses the **Arduino Uno** (the classic R3) for examples —
it's the most documented board on earth. The ideas transfer to every
other board; pin numbers and specs differ.

## Why not just use a Raspberry Pi?

A Pi is a full Linux computer — more power, but it boots an OS, can
corrupt its SD card if power is yanked, and idles at watts. An
Arduino starts instantly, tolerates power cuts, and sips power. Rule
of thumb: **Pi when you need an operating system** (networking,
video, complex software); **Arduino when you need to touch the
physical world** simply and reliably. Many projects use both.

## What Arduino is not

- **Not a replacement for your computer.** 2 KB of RAM is not a
  challenge to overcome; it's the design.
- **Not only for experts.** The whole point of Arduino (since 2005)
  was making microcontrollers accessible to artists and beginners.
- **Not precision equipment.** Its analog readings are 10-bit
  (0–1023), its clock drifts — fine for hobbyist sensing, not for
  lab instruments.

**Next:** [The Board](the-board.md)
