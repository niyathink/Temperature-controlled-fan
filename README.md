# 🌡️ Temperature Monitoring System with LCD Display and Fan Control

## 📌 Overview

This project is an Arduino-based temperature monitoring system that uses a **DS18B20 temperature sensor** to measure temperature and displays the readings on a 20×4 I2C LCD. It also controls a fan based on the measured temperature.

The LCD displays a custom-designed temperature progress bar along with the minimum, current, and maximum recorded temperatures. The fan speed is controlled using PWM based on temperature.

## ✨ Features

- **Real-Time Temperature Monitoring:** Reads temperature using the DS18B20 sensor.
- **Temperature Progress Bar:** Displays temperature variations on the LCD.
- **Minimum Temperature Tracking:** Records the lowest temperature measured.
- **Maximum Temperature Tracking:** Records the highest temperature measured.
- **Current Temperature Display:** Shows the latest temperature reading.
- **Automatic Fan Speed Control:** Adjusts fan speed using PWM according to the measured temperature.
- **Serial Monitoring:** Sends temperature readings to the Serial Monitor every second.

## 🛠️ Components Required

| Component                  |    Quantity |
| -------------------------- | ----------: |
| Arduino Nano               |           1 |
| DS18B20 Temperature Sensor |           1 |
| 20×4 I2C LCD Display       |           1 |
| DC Fan                     |           1 |
| Transistor                 |           1 |
| 4.7kΩ Pull-up Resistor     |           1 |
| Connecting Wires           | As required |
| Breadboard                 |           1 |

## 🔌 Pin Connections

| Component                                 | Arduino Nano Pin |
| ----------------------------------------- | ---------------- |
| DS18B20 Data                              | Digital Pin 2    |
| LCD SDA                                   | A4               |
| LCD SCL                                   | A5               |
| Fan Control (Transistor Base/Gate Driver) | PWM Pin 3        |

**Additional connections:**

- DS18B20 VCC → 5V
- DS18B20 GND → GND
- Connect a 4.7kΩ pull-up resistor between the DS18B20 data line and 5V.
- LCD VCC → 5V
- LCD GND → GND
- Connect the transistor as a fan driver, with the fan powered by a suitable supply.
- Ensure the Arduino and external fan power supply share a common GND.

**Note:** Use a suitable transistor with an appropriate base resistor (for a BJT) or gate arrangement (for a MOSFET). A flyback diode should be connected across a brushed DC fan to protect the transistor.

## 📚 Libraries Required

Install the following libraries through the Arduino IDE Library Manager:

1. `OneWire`
2. `DallasTemperature`
3. `LiquidCrystal_I2C`
4. `Wire` (included with the Arduino environment)

## ⚙️ Working Principle

1. The DS18B20 sensor measures the surrounding temperature.
2. The Arduino retrieves the temperature reading using the DallasTemperature library.
3. The minimum and maximum temperatures are updated whenever a new reading is obtained.
4. The current temperature is mapped to a position between 0 and 20.
5. The LCD displays a custom progress bar representing the mapped temperature position.
6. The LCD also displays the minimum, current, and maximum temperature readings.
7. The Arduino generates a PWM signal on digital pin 3 to control the fan speed through the transistor.
8. Temperature readings are sent to the Serial Monitor every second.

## 🖥️ LCD Display

The 20×4 LCD displays the following information:

| LCD Row | Display                                    |
| ------- | ------------------------------------------ |
| Row 1   | Temperature progress bar                   |
| Row 2   | Min / Cur / Max labels                     |
| Row 3   | Minimum, current, and maximum temperatures |
| Row 4   | Available for additional information       |

## 📊 Temperature-Based Fan Control

The temperature is mapped to a range of 0–20.

The resulting temperature is converted into a PWM value between 0 and 255:

`PWM = (pos / 20.0) × 255`

This allows the fan speed to vary according to the mapped temperature.

**Note:** The progress bar represents the temperature relative to the minimum and maximum readings recorded since startup, rather than a fixed temperature scale.

---

