# Sensors

Sensors are why Arduinos exist. Two classics cover most beginner
needs: temperature/humidity and distance.

## Temperature and humidity: DHT22

The DHT22 (blue, ~$5) reports temperature and humidity over a single
digital pin. Install the library first — Sketch → Include Library →
Manage Libraries, search "DHT sensor library" (Adafruit), Install
(it will offer the Adafruit Unified Sensor dependency — accept).

Wire: VCC → 5V, GND → GND, data pin → digital pin 2.

```cpp
#include <DHT.h>

#define DHT_PIN 2
#define DHT_TYPE DHT22

DHT dht(DHT_PIN, DHT_TYPE);

void setup() {
  Serial.begin(9600);
  dht.begin();
}

void loop() {
  float humidity = dht.readHumidity();
  float tempC = dht.readTemperature();

  if (isnan(humidity) || isnan(tempC)) {
    Serial.println("Sensor read failed — check wiring");
  } else {
    Serial.print("Temp: ");
    Serial.print(tempC);
    Serial.print(" C, Humidity: ");
    Serial.print(humidity);
    Serial.println(" %");
  }
  delay(2000);   // DHT22 needs ~2s between reads
}
```

**Honest limits:** ±0.5°C accuracy, slow (one reading per 2
seconds), and the cheap DHT11 sibling is worse (±2°C — skip it if
you can). Fine for room monitoring; not for science.

## Distance: HC-SR04 ultrasonic

The HC-SR04 (~$3) measures distance with sound: it pings, listens
for the echo, and times it. No library needed.

Wire: VCC → 5V, GND → GND, Trig → pin 9, Echo → pin 10.

```cpp
const int TRIG_PIN = 9;
const int ECHO_PIN = 10;

void setup() {
  Serial.begin(9600);
  pinMode(TRIG_PIN, OUTPUT);
  pinMode(ECHO_PIN, INPUT);
}

void loop() {
  digitalWrite(TRIG_PIN, LOW);
  delayMicroseconds(2);
  digitalWrite(TRIG_PIN, HIGH);
  delayMicroseconds(10);
  digitalWrite(TRIG_PIN, LOW);

  long duration = pulseIn(ECHO_PIN, HIGH);   // echo time, microseconds
  float distanceCm = duration * 0.0343 / 2;  // sound: 343 m/s, round trip

  Serial.print("Distance: ");
  Serial.print(distanceCm);
  Serial.println(" cm");
  delay(200);
}
```

`pulseIn()` waits for the pin to go HIGH and measures how long it
stays there — the echo's round-trip time. Divide by 2 (there and
back), multiply by the speed of sound.

**Check:** Hold your hand in front of the sensor and move it — the
numbers track your hand, roughly 2cm to 400cm.

**Honest limits:** Soft fabrics absorb the ping, angled surfaces
deflect it, and two sensors in one room confuse each other. It's a
parking sensor, not lidar.

## The pattern

Both sensors follow the same shape you'll reuse forever:

1. Include the library (if any).
2. Configure in `setup()`.
3. Read in `loop()`, check for failure, print or act on the value.

New sensor, same dance.

**Next:** [Libraries](libraries.md)
