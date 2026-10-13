# How Sketches Work

A sketch is C++ with training wheels. You don't need to learn C++
first — you need about ten ideas, and you'll pick up the rest from
examples.

## The non-negotiables

```cpp
void setup() {
  // runs once
}

void loop() {
  // runs forever
}
```

Every sketch has these two functions. Miss one and it won't
compile. `//` starts a comment — ignored by the compiler, read by
humans. Comment generously; future-you won't remember why.

**Statements end with `;`** — every single one. Forgetting it is
the #1 compile error, and the error message points at the *next*
line, which confuses everyone exactly once:

```cpp
digitalWrite(LED_BUILTIN, HIGH)   // missing ; — error reported on the NEXT line
delay(1000);
```

## Variables

```cpp
int blinkCount = 0;          // whole numbers
float voltage = 3.3;         // decimals
bool ledOn = true;           // true/false
char letter = 'A';           // single character (single quotes)
String message = "hello";    // text (double quotes, capital S)
```

On the Uno, an `int` holds -32,768 to 32,767. Count past that and it
*wraps around* — a classic bug source. Need bigger? `long`
(-2 billion to 2 billion). With 2 KB of RAM, you think about this
more than on a PC — but for beginner projects, `int` is almost
always right.

**Careful:** `String` (capital S) is convenient but fragments the
Uno's tiny memory over time, eventually crashing long-running
programs. Fine for learning; for devices that run months, C-style
strings (`char msg[] = "hello";`) are the grown-up choice.

## if, for, while — the usual suspects

```cpp
if (buttonPressed) {
  digitalWrite(LED_BUILTIN, HIGH);
} else {
  digitalWrite(LED_BUILTIN, LOW);
}

for (int i = 0; i < 10; i++) {
  // do something 10 times
}
```

If you've seen any programming language, this is familiar. If not:
`if` chooses, `for` repeats a counted number of times, `while`
repeats until something changes. Curly braces `{}` group statements
together.

## delay() and its problem

`delay()` freezes *everything* — no button reads, no sensor checks —
until the time passes. Fine for blinking; terrible for responsive
projects. The grown-up pattern is `millis()` (milliseconds since
power-on) — "is it time yet?" instead of "wait here":

```cpp
unsigned long previousMillis = 0;
const long interval = 1000;

void setup() {
  pinMode(LED_BUILTIN, OUTPUT);
}

void loop() {
  unsigned long currentMillis = millis();
  if (currentMillis - previousMillis >= interval) {
    previousMillis = currentMillis;
    digitalWrite(LED_BUILTIN, !digitalRead(LED_BUILTIN));  // toggle
  }
  // other code runs freely here — nothing is blocked
}
```

This is the famous "Blink Without Delay" example (File → Examples →
02.Digital → BlinkWithoutDelay). Learn it when `delay()` starts
annoying you — roughly your third project.

**Next:** [Digital I/O](digital-io.md)
