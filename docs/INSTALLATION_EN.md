# Installation – English

## Overview

![Installation Flow](../images/installation-flow.svg)

## Requirements

- Home Assistant
- ESPHome
- HACS
- HACS frontend component **Button Card**
- optional **card-mod**
- ESP32-C3
- RC522
- passive piezo buzzer
- optional LED + resistor

## 1. Wire the hardware

Wire the ESP32-C3, RC522, buzzer and LED according to [WIRING.md](WIRING.md).

Important:

- power the RC522 from **3.3 V only**
- connect the LED anode to **GPIO2 via 220 Ω**
- connect the buzzer to **GPIO8** and **GND**

## 2. ESPHome configuration

Copy `esphome/rfid-rc522.yaml` into ESPHome and add the values from `secrets.example.yaml` to your private ESPHome `secrets.yaml`.

Never commit real credentials.

## 3. Flash

Validate the configuration and install it to the ESP32-C3 over USB or OTA.

## 4. Home Assistant integration

Add the device through the ESPHome integration if it is not discovered automatically. Then open the device integration options and enable **Allow the device to perform Home Assistant actions**. This is required for `homeassistant.tag_scanned`.

## 5. Check entity IDs

Open **Developer Tools → States** and search for `rfid`.

Entity IDs may differ from the examples in this repository. Update the dashboard YAML files when required.

## 6. HACS

Install **Button Card** through HACS. `card-mod` is optional.

Reload the Home Assistant frontend afterwards.

## 7. Dashboard

Create three dashboard sections and paste the YAML from:

- `home-assistant/01-terminal.yaml`
- `home-assistant/02-testconsole.yaml`
- `home-assistant/03-control.yaml`

## 8. Test RFID

Present a tag to the RC522. The UID should appear in ESPHome logs and Home Assistant should receive a tag event.

You can then use the tag in **Settings → Tags** for Home Assistant automations.
