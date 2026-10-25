# Arduino for Mere Mortals

An Arduino is a tiny, cheap computer with one job: interacting with
the physical world. It reads sensors, blinks lights, spins motors —
no operating system, no screen, no distractions. If you've ever
wanted software to *touch* something real, this is the on-ramp.

No CS degree required. No electronics background assumed. Ideas
first, then circuits you can build on a $30 board.

## What this guide covers

- **What Arduino is** — microcontrollers vs. the computer on your desk
- **The board** — a tour of the Arduino Uno: pins, power, and the
  reset button
- **Getting set up** — the IDE, picking your board and port
- **Your first sketch** — Blink, the "hello world" of hardware
- **How sketches work** — `setup()`, `loop()`, and the shape of every
  program
- **Digital I/O** — LEDs, buttons, and reading the real world as
  on/off
- **Analog** — reading knobs and sensors, faking analog output with
  PWM
- **Serial** — talking to your computer for debugging
- **Sensors** — temperature/humidity and ultrasonic distance
- **Libraries** — other people's code, installed in two clicks
- **Power and wiring** — breadboards, resistors, and the limits that
  keep the magic smoke inside
- **Troubleshooting** — the errors everyone hits

## What it doesn't cover

Circuit design theory, surface-mount soldering, wireless (WiFi /
Bluetooth boards like the ESP32 get a mention, not a chapter), or
the Arduino Uno Q's bigger siblings in depth. This guide is about
understanding and *using* an Arduino, not electrical engineering.

## How to use this guide

Every sketch compiles — each was verified with `arduino-cli`
against the Arduino Uno target before shipping. **Check:** blocks
show what success looks like. **Careful:** marks anything that can
damage hardware (mostly in [Power and Wiring](power-and-wiring.md)).

You don't need the physical board to read this guide, but you'll
want one to *feel* it. A starter kit (Uno, breadboard, LEDs,
resistors, buttons, a sensor or two) is the price of a pizza.

## Chapters

1. [What Arduino Is](what-arduino-is.md)
2. [The Board](the-board.md)
3. [Getting Set Up](getting-set-up.md)
4. [Your First Sketch](first-sketch.md)
5. [How Sketches Work](how-sketches-work.md)
6. [Digital I/O](digital-io.md)
7. [Analog](analog.md)
8. [Serial](serial.md)
9. [Sensors](sensors.md)
10. [Libraries](libraries.md)
11. [Power and Wiring](power-and-wiring.md)
12. [Troubleshooting](troubleshooting.md)
13. [Glossary](glossary.md)

*Written to the [nine-point writing standard](criteria.md) shared by
every guide in this series.*

---

## Part of the series

This guide is one of the [For Mere Mortals](https://paulsullivan33-dev.github.io/mere-mortals/) guides: plain-language guides to the tools programmers and makers use.

Related guides:

- [PlatformIO for Mere Mortals](https://paulsullivan33-dev.github.io/platformio-for-mere-mortals/)
- [Soldering & Basic Electronics for Mere Mortals](https://paulsullivan33-dev.github.io/soldering-for-mere-mortals/)
- [ESPHome for Mere Mortals](https://paulsullivan33-dev.github.io/esphome-for-mere-mortals/)

## License

The writing in this guide is licensed under [CC BY 4.0](https://github.com/paulsullivan33-dev/arduino-for-mere-mortals/blob/main/LICENSE). Code examples and lab scripts are licensed under the [MIT License](https://github.com/paulsullivan33-dev/arduino-for-mere-mortals/blob/main/LICENSE-CODE).
