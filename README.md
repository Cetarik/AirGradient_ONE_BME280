# AirGradient Arduino Library for ESP8266 (Wemos D1 MINI) and ESP32 (ESP32-C3 Mini)

This is the code for the AirGradient open-source indoor and outdoor air quality monitors using ESP8266 and ESP32-C3 microcontrollers.

More information about the air quality monitors and kits:

- **Indoor Monitor**: https://www.airgradient.com/indoor/
- **Outdoor Monitor**: https://www.airgradient.com/outdoor/

---

## BME280 Integration (Custom Extension)

The goal of this modification was to resolve the issue of unrealistic temperature and humidity readings and to additionally gain access to **barometric pressure measurements**.

For this purpose, the **BME280 sensor** was integrated.

The BME280 integration is implemented on a completely separated level compared to the original measurements.

### Design Principles

- Temperature and humidity values from the **PMS5003T** remain unchanged.
- PMS5003T values are still used for **PM and S8 compensation**.
- Temperature, humidity, and pressure from the **BME280** are published as **separate JSON and MQTT fields**.
- These additional values are **not sent to the AirGradient Cloud**.
- They **do not appear in Home Assistant** when using the official AirGradient HA integration.

This ensures full backward compatibility with the original firmware behavior.

---

## Physical Connection

- The **PicoBlade IO connector** directly on the AirGradient PCB was used.
- Communication is handled via standard **I2C**.
- A small hole was drilled next to the PMS5003T sensor.
- The hole placement was carefully chosen so that it does **not interfere with the PM measurement chamber**.

> **Important:**  
> The sensor must be placed in shade and protected from direct sunlight.  
> Direct sunlight can heat the enclosure and significantly distort temperature readings.

---

## Library Requirements

To use the BME280 sensor, you must install the following libraries via the **Arduino IDE Library Manager**:

- **Adafruit BME280**
- **Adafruit BusIO**

These are two separate libraries.

The **Adafruit BME280** library depends on **Adafruit BusIO**, so both must be installed.

Always install them directly from the official Arduino IDE Library Manager to avoid compatibility issues.

---

## Supported Sensor Modules

This library supports the following sensor modules:

- Plantower PMS5003
- Plantower PMS5003T
- SenseAir S8
- Sensirion SGP41
- Sensirion SHT40
- Adafruit BME280

---

## Important Information

Make sure you have exactly the versions of libraries and boards installed as described in the comment section of the example files.

If you have an older version of the AirGradient PCB not mentioned in the example files, please downgrade this library to **version 2.4.15** to support legacy boards.

---

## Release Process

Releases published on GitHub are **not immediately deployed to all devices in the market**.

Each release first goes through internal testing, including limited deployments in select locations to verify stability and functionality.

If the tests pass, the firmware becomes available for:

- **FOTA (Firmware Over-The-Air) updates** from the AirGradient dashboard
- **Manual flashing** via https://www.airgradient.com/documentation/firmwares/

Each GitHub release note will include the planned rollout date for wider availability.

---

## Help & Support

If you have any questions or problems, visit:

https://forum.airgradient.com/

---

## Development

See:

- /docs/howto-compile.md

for details about how to customize the firmware and flash it to your device.

---

## Over The Air (OTA) Updates

See:

- /docs/ota-updates.md

for details about how AirGradient monitors receive OTA updates.

---

## API Documentation

- Local server API documentation:
  /docs/local-server.md

- AirGradient Cloud server API documentation:
  https://api.airgradient.com/public/docs/api/v1/

---

## Integrated Libraries

The following libraries have been integrated into this library for ease of use:

- Adafruit NeoPixel
- Adafruit SH110X
- Adafruit SSD1306 Wemos Mini OLED
- Adafruit GFX Library
- Sensirion Gas Index Algorithm
- Sensirion Core
- Sensirion I2C SGP41
- Sensirion I2C SHT
- WiFiManager
- Arduino_JSON
- PubSubClient

---

## License

**CC BY-SA 4.0 Attribution-ShareAlike 4.0 International License**
