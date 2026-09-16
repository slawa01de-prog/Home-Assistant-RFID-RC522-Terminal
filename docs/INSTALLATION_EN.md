# Installation – English

## Requirements

- Home Assistant
- ESPHome
- HACS
- HACS frontend component **Button Card**
- optional **card-mod**
- ESP32-C3
- RC522

## 1. ESPHome

Copy `esphome/rfid-rc522.yaml` into ESPHome and add the values from `secrets.example.yaml` to your private ESPHome `secrets.yaml`.

Never commit real credentials.

## 2. Flash

Validate the configuration and install it to the ESP32-C3 over USB or OTA.

## 3. Home Assistant integration

Add the device through the ESPHome integration if it is not discovered automatically. Then open the device integration options and enable **Allow the device to perform Home Assistant actions**. This is required for `homeassistant.tag_scanned`.

## 4. Check entity IDs

Open **Developer Tools → States** and search for `rfid`.

Entity IDs may differ from the examples in this repository. Update the dashboard YAML files when required.

## 5. HACS

Install **Button Card** through HACS. `card-mod` is optional.

Reload the Home Assistant frontend afterwards.

## 6. Dashboard

Create three dashboard sections and paste the YAML from:

- `home-assistant/01-terminal.yaml`
- `home-assistant/02-testconsole.yaml`
- `home-assistant/03-control.yaml`

## 7. Test RFID

Present a tag to the RC522. The UID should appear in ESPHome logs and Home Assistant should receive a tag event.
