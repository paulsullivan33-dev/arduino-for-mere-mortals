# Libraries

A **library** is someone else's code, packaged so you can use it
without understanding its insides. The DHT sensor library from the
last chapter is one; there are thousands — for displays, motors,
WiFi, cryptography, everything.

## Installing

Sketch → Include Library → Manage Libraries. Search, click Install.
That's it — the IDE downloads it into your sketchbook's `libraries`
folder.

With arduino-cli:

```bash
arduino-cli lib search "DHT sensor"
arduino-cli lib install "DHT sensor library"
```

**Check:** After installing, File → Examples shows a new section
named after the library, full of working example sketches. **Start
there** — library examples are tested by the author and are the
fastest way to learn the API.

## Using one

```cpp
#include <DHT.h>   // the #include makes the library available
```

The angle brackets mean "a installed library" (vs. quotes for your
own files). After including, you get the library's objects and
functions — `DHT dht(...)`, `dht.readTemperature()` — as if you'd
written them.

## When libraries fight

- **Missing dependency:** the installer usually offers to install
  them — accept. If a sketch fails with "No such file or directory"
  on an `#include`, a dependency is missing.
- **Duplicate libraries:** two versions installed (one manual, one
  via manager). The compiler warns "Multiple libraries were found"
  and picks one — possibly the wrong one. Remove the duplicate from
  the sketchbook's `libraries` folder.
- **Wrong architecture:** some libraries only work on certain chips
  (ESP32-only WiFi code won't compile for the Uno). The library
  manager shows architectures — check before depending on one.

## Writing your own (later)

You won't need this for a while, but the shape is simple: a `.h`
file declaring things, a `.cpp` file defining them, in a folder
under `libraries/`. When you find yourself copying the same sensor
code into a third sketch, that's the moment.

**Next:** [Power and Wiring](power-and-wiring.md)
