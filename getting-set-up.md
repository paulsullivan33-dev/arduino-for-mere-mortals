# Getting Set Up

You need two things: the Arduino software, and telling it which
board and port you have.

## Install the IDE

Download the **Arduino IDE** (version 2.x) from
[arduino.cc](https://www.arduino.cc/en/software) for your system and
install it like any program. It's free and open-source.

Prefer the command line? `arduino-cli` does everything the IDE does:

```bash
arduino-cli core update-index
arduino-cli core install arduino:avr
```

(Every sketch in this guide was verified with `arduino-cli`
compiling for the Uno.)

## Select your board and port

1. Plug the Uno into your computer with a USB cable.
   (**Careful:** some cheap USB cables are charge-only — no data
   wires. If the board powers on but no port appears, try another
   cable before anything else.)
2. In the IDE: Tools → Board → "Arduino Uno".
3. Tools → Port → pick the port that appeared when you plugged in
   (on Windows it's `COM3` or similar; Mac/Linux show
   `/dev/tty.usbmodem...` or `/dev/ttyUSB0`).

**Check:** Tools → Port shows a port *only while the board is
plugged in*. Unplug, watch it disappear, plug back in — that's how
you identify the right one when several are listed.

With arduino-cli:

```bash
arduino-cli board list
```

**Check:** Your board appears with its port and name.

## The sketchbook

The IDE stores your programs ("sketches") in a **sketchbook**
folder (Documents/Arduino by default). Libraries you install also
live there. Know where it is — you'll visit it when installing
libraries manually.

**Next:** [Your First Sketch](first-sketch.md)
