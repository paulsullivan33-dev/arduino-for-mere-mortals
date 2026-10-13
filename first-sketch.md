# Your First Sketch

In the IDE: File → Examples → 01.Basics → Blink. This is the "hello
world" of hardware — it blinks the built-in LED on pin 13.

```cpp
void setup() {
  pinMode(LED_BUILTIN, OUTPUT);
}

void loop() {
  digitalWrite(LED_BUILTIN, HIGH);
  delay(1000);
  digitalWrite(LED_BUILTIN, LOW);
  delay(1000);
}
```

Click Upload (the arrow button). The IDE compiles the sketch, sends
it to the board, and the little LED starts blinking — one second on,
one second off.

**Check:** The `L` LED on the board blinks steadily. The IDE's
output panel ends with "Done uploading."

## Line by line

- `void setup()` — runs **once** when the board powers on or resets.
  Configuration goes here. (`void` means "returns nothing" — C++
  vocabulary you'll absorb by osmosis.)
- `pinMode(LED_BUILTIN, OUTPUT)` — set pin 13 as an output.
  `LED_BUILTIN` is a built-in name for 13, so the sketch works on
  boards where the LED is elsewhere.
- `void loop()` — runs **over and over, forever**. This is your
  program's heartbeat.
- `digitalWrite(LED_BUILTIN, HIGH)` — set the pin to 5V (LED on).
  `LOW` means 0V (LED off).
- `delay(1000)` — do nothing for 1000 milliseconds.

That's the whole paradigm: **configure once in `setup()`, then
repeat `loop()` forever.** Nearly every Arduino program you'll ever
write has this shape.

## Experiment (this is the fun part)

Change `delay(1000)` to `delay(100)` and re-upload — fast blink.
Change one of them to make an SOS pattern: three short, three long,
three short. The edit-upload-see cycle takes seconds, which is why
hardware feels so immediate compared to most programming.

**Next:** [How Sketches Work](how-sketches-work.md)
