# DHT11 Sensor

The DHT11 is a low-cost digital sensor used to measure temperature and humidity. It's widely used in various applications due to its simplicity and reliability.

## Features

- **Temperature Range**: 0 to 50°C (32 to 122°F) with ±2°C accuracy.
- **Humidity Range**: 20 to 90% RH (Relative Humidity) with ±5% accuracy.
- **Operating Voltage**: 3 to 5V.
- **Low Power Consumption**: Ideal for battery-powered devices.
- **Communication Protocol**: Digital single-wire.

## Pin Configuration

1. **VCC**: Power supply (3-5V).
2. **Data**: Serial data output.
3. **NC (Not Connected)**: No connection.
4. **GND**: Ground.

## How It Works

The DHT11 sensor uses a capacitive humidity sensor and a thermistor to measure the surrounding air and outputs a digital signal on the data pin. It communicates with a microcontroller using a single-wire protocol, making it easy to interface with.

## Interfacing with a Microcontroller

To interface the DHT11 with a microcontroller like an Arduino, follow these steps:

### Connections

- Connect the VCC pin to the 5V pin on the Arduino.
- Connect the GND pin to the GND on the Arduino.
- Connect the Data pin to a digital I/O pin on the Arduino (e.g., pin 2).

### Library

- Install the DHT library in the Arduino IDE. You can find it in the Library Manager or download it from GitHub.

### Code

```cpp
#include "DHT.h"

#define DHTPIN 2     // Digital pin connected to the DHT sensor
#define DHTTYPE DHT11   // DHT11

DHT dht(DHTPIN, DHTTYPE);

void setup() {
  Serial.begin(9600);
  dht.begin();
}

void loop() {
  delay(2000);  // Wait a few seconds between measurements
  float h = dht.readHumidity();
  float t = dht.readTemperature();

  if (isnan(h) || isnan(t)) {
    Serial.println("Failed to read from DHT sensor!");
    return;
  }

  Serial.print("Humidity: ");
  Serial.print(h);
  Serial.print(" %\t");
  Serial.print("Temperature: ");
  Serial.print(t);
  Serial.println(" *C ");
}
