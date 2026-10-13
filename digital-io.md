# Digital I/O

**Digital** means two states: HIGH (5V, on, 1) or LOW (0V, off, 0).
No in-between. Buttons, motion sensors, and LEDs live in this world.

## Output: lighting an LED

Wire: Uno pin 13 → 220Ω resistor → LED long leg (+); LED short leg
(−) → GND. (The built-in LED needs no wiring, but wiring your own
teaches the circuit.)

```cpp
void setup() {
  pinMode(13, OUTPUT);
}

void loop() {
  digitalWrite(13, HIGH);   // LED on
  delay(500);
  digitalWrite(13, LOW);    // LED off
  delay(500);
}
```

**Why the resistor?** An LED without one draws as much current as it
can — briefly very bright, then dead, possibly taking the pin with
it. The 220Ω resistor limits current to ~15mA, safely under the
pin's ~20mA limit. **No LED without a resistor** (except the
built-in one — it has its own).

## Input: reading a button

Wire: button between pin 2 and GND. No extra resistor needed — we
use the chip's built-in one:

```cpp
const int BUTTON_PIN = 2;
const int LED_PIN = 13;

void setup() {
  pinMode(BUTTON_PIN, INPUT_PULLUP);
  pinMode(LED_PIN, OUTPUT);
}

void loop() {
  int buttonState = digitalRead(BUTTON_PIN);
  if (buttonState == LOW) {
    digitalWrite(LED_PIN, HIGH);  // pressed → LED on
  } else {
    digitalWrite(LED_PIN, LOW);
  }
}
```

**Why does pressed read LOW?** `INPUT_PULLUP` connects the pin
internally to 5V through a resistor, so it reads HIGH when idle.
Pressing the button connects it to GND, dragging it LOW. Backwards
from intuition, but it means the button needs no external parts —
one wire to GND and you're done.

## Debouncing: buttons lie

A button press isn't one clean on/off — the metal contacts bounce,
producing a burst of rapid on/off flickers over a few milliseconds.
Your loop runs fast enough to see each bounce as separate presses.
For "LED follows button" you won't notice; for "count presses" you
must.

The simple fix: after seeing a change, ignore further changes for
~50ms:

```cpp
const int BUTTON_PIN = 2;
int pressCount = 0;
int lastState = HIGH;
unsigned long lastDebounceTime = 0;

void setup() {
  pinMode(BUTTON_PIN, INPUT_PULLUP);
  Serial.begin(9600);
}

void loop() {
  int reading = digitalRead(BUTTON_PIN);
  if (reading != lastState) {
    lastDebounceTime = millis();
  }
  if ((millis() - lastDebounceTime) > 50) {
    if (reading == LOW && lastState == HIGH) {
      pressCount++;
      Serial.print("Presses: ");
      Serial.println(pressCount);
    }
  }
  lastState = reading;
}
```

(Uses `Serial` — covered properly in [Serial](serial.md). For now:
it prints the count to your computer.)

## digitalRead / digitalWrite cheat sheet

| Call | Does |
|------|------|
| `pinMode(pin, OUTPUT)` | Pin will drive HIGH/LOW |
| `pinMode(pin, INPUT)` | Pin reads external signal (needs external resistor) |
| `pinMode(pin, INPUT_PULLUP)` | Pin reads, idle = HIGH |
| `digitalWrite(pin, HIGH/LOW)` | Set output |
| `digitalRead(pin)` | Returns HIGH or LOW |

**Next:** [Analog](analog.md)
