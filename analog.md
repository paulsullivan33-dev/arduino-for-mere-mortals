# Analog

The real world isn't on/off — a knob turns gradually, light fades,
temperature drifts. **Analog** handles the in-between.

## Reading analog: analogRead()

The Uno's analog pins (A0–A5) measure voltage from 0 to 5V and
report it as a number from **0 to 1023** (10-bit resolution):

```cpp
void setup() {
  Serial.begin(9600);
}

void loop() {
  int value = analogRead(A0);   // 0 (0V) to 1023 (5V)
  Serial.println(value);
  delay(200);
}
```

Wire a potentiometer (knob): outer legs to 5V and GND, middle wiper
to A0. Turn the knob, watch the numbers sweep 0–1023. That's a
sensor reading — most analog sensors work exactly like this,
presenting a voltage the Arduino measures.

**Volts from the reading:** `volts = reading * 5.0 / 1023.0`. The
`.0`s matter — without them, C++ does integer division and your
0–5V becomes 0–4V of wrongness.

## "Analog" output: PWM

Here's the catch: the Uno has **no true analog output**. It can't
produce 2.5V. Instead, pins marked `~` (3, 5, 6, 9, 10, 11) do
**PWM** — Pulse Width Modulation: they flicker between 0V and 5V
hundreds of times per second, varying how long each pulse stays on.
An LED (or motor) averages the flicker into "dimmer" or "slower":

```cpp
const int LED_PIN = 9;   // a ~ PWM pin

void setup() {
  pinMode(LED_PIN, OUTPUT);
}

void loop() {
  int knob = analogRead(A0);          // 0–1023
  int brightness = map(knob, 0, 1023, 0, 255);
  analogWrite(LED_PIN, brightness);   // 0–255 duty cycle
  delay(10);
}
```

`analogWrite(pin, value)` takes 0 (fully off) to 255 (fully on).
`map()` rescales one range to another — the translator between the
10-bit input world and the 8-bit output world.

**Check:** Turning the potentiometer fades the LED smoothly. If the
LED only snaps on/off, you're on a non-PWM pin — move to one marked
`~`.

**Honest limits:** PWM at ~490Hz flickers visibly on camera and
buzzes audibly through a speaker. It's "analog enough" for LEDs and
motors, not for audio or precision instruments.

## tone(): the bonus sound

Any digital pin can make noise with `tone()`:

```cpp
void setup() {
  tone(8, 440, 500);   // pin 8, 440Hz (A4), for 500ms
  delay(600);
  noTone(8);
}

void loop() {
}
```

Wire a piezo buzzer between pin 8 and GND. It's square-wave harsh,
not musical — but doorbells and alarms don't need fidelity.

**Next:** [Serial](serial.md)
