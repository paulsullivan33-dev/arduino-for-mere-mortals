# Serial

Your Arduino has no screen. **Serial** is how it talks to your
computer — for debugging, for logging sensor data, for everything.
Learn this early; it makes every later chapter easier.

## The basics

```cpp
void setup() {
  Serial.begin(9600);        // open the serial port at 9600 baud
  Serial.println("Hello!");  // print a line
}

void loop() {
  Serial.print("Reading: ");
  Serial.println(analogRead(A0));
  delay(500);
}
```

Upload, then open Tools → Serial Monitor. Set the baud rate dropdown
to **9600** to match `Serial.begin(9600)` — mismatched baud rates
produce gibberish, the classic serial symptom.

**Check:** The monitor shows `Hello!` once, then `Reading: 512`
(or whatever A0 sees) every half second.

## print() vs println()

- `Serial.print(x)` — prints with no line ending.
- `Serial.println(x)` — prints *plus* a newline.

Combine them to build readable lines: `print("Temp: ")` then
`println(temp)` gives `Temp: 23.5` on one line.

## Baud rate

**Baud** is symbols per second — roughly bits per second here.
9600 is the traditional default; 115200 is common for faster data.
Both ends must agree. Higher is faster but more error-prone over
long wires; for USB debugging it barely matters.

## Reading from the computer

Serial goes both ways — your computer can send commands *to* the
Arduino:

```cpp
void setup() {
  Serial.begin(9600);
  pinMode(LED_BUILTIN, OUTPUT);
  Serial.println("Type 1 for ON, 0 for OFF");
}

void loop() {
  if (Serial.available() > 0) {       // any incoming data?
    char cmd = Serial.read();         // read one character
    if (cmd == '1') {
      digitalWrite(LED_BUILTIN, HIGH);
      Serial.println("LED on");
    } else if (cmd == '0') {
      digitalWrite(LED_BUILTIN, LOW);
      Serial.println("LED off");
    }
  }
}
```

Type `1` in the Serial Monitor's input bar, press Send — the LED
lights. You've built a remote control.

**Careful:** The Serial Monitor's line-ending dropdown (bottom
right) appends invisible characters. With "Newline" selected, typing
`1` sends `'1'` *plus* `'\n'` — your sketch reads the `1`, then the
`\n` hits the `else` branch harmlessly here, but in stricter parsing
it causes phantom inputs. Set it to "No line ending" when it matters.

## The plotter

Tools → Serial Plotter graphs numbers in real time — one value per
`println`. Point a sensor at things and watch the waveform. It's the
fastest way to "see" what a sensor sees.

**Next:** [Sensors](sensors.md)
