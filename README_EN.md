# Home Assistant RFID RC522 Terminal

A compact RFID access terminal based on an **ESP32-C3**, **MFRC522/RC522** and **ESPHome**, integrated directly into **Home Assistant**.

The project forwards RFID tags to Home Assistant as tag events and provides buzzer, LED and test functions. The included tablet dashboard uses an animated scan panel and separate sections for terminal status, test actions and controls.

[Deutsche Version](README.md)

![Project Banner](images/dashboard-hero.svg)

> **Security:** Keep API keys, OTA passwords and Wi-Fi credentials in `secrets.yaml`. Never commit real credentials to a public repository.

## Features

- ESP32-C3 + RC522 via SPI
- forwards RFID scans to Home Assistant
- RTTTL buzzer output
- Home Assistant switch to enable/disable buzzer
- optional status LED
- online/offline indication
- test actions for OK, deny, melody and alarm
- animated tablet UI using `custom:button-card`
- compact layout designed to avoid vertical scrolling

## Example graphics

### Wiring diagram

![Wiring Diagram](images/wiring-diagram.svg)

### Required hardware

![Required Hardware](images/hardware-overview.svg)

### Installation flow

![Installation Flow](images/installation-flow.svg)

## Hardware

- ESP32-C3 DevKitM-1 or compatible board
- RC522 RFID module
- passive piezo buzzer
- optional LED with a suitable resistor
- jumper wires
- RFID tag or RFID card

## Wiring

| Signal / module | ESP32-C3 |
|---|---|
| RC522 SDA / SS | GPIO7 |
| RC522 SCK | GPIO9 |
| RC522 MOSI | GPIO6 |
| RC522 MISO | GPIO5 |
| RC522 RST | GPIO10 |
| RC522 3.3V | 3V3 |
| RC522 GND | GND |
| Buzzer + | GPIO8 |
| Buzzer - | GND |
| LED anode | GPIO2 via 220 Ω |
| LED cathode | GND |

**Power the RC522 from 3.3 V only.**

See [docs/WIRING.md](docs/WIRING.md) for the full wiring guide.

## Quick start

1. Add `esphome/rfid-rc522.yaml` to ESPHome.
2. Copy the required values from `esphome/secrets.example.yaml` into your own `secrets.yaml`.
3. Flash the ESP32-C3.
4. Add the ESPHome device to Home Assistant.
5. Enable **Allow the device to perform Home Assistant actions** in the ESPHome integration so `homeassistant.tag_scanned` can work.
6. Install **Button Card** through HACS.
7. Optionally install **card-mod**.
8. Reload the Home Assistant frontend.
9. Add the three YAML cards from `home-assistant/` to three dashboard sections.
10. Adjust entity IDs if Home Assistant generated different names.

See [docs/INSTALLATION_EN.md](docs/INSTALLATION_EN.md) for details.

## Dashboard layout

Recommended tablet arrangement:

```text
┌────────────────────────┐ ┌────────────────────────┐ ┌──────────────────────┐
│ RFID ACCESS TERMINAL   │ │ RFID Test Console      │ │ RFID Controls        │
│ ● SYSTEM ONLINE        │ │ ✓ allowed   ! denied   │ │ Connection Firmware  │
│                        │ │ ♪ Success   🚨 Alarm    │ │ Buzzer      LED      │
│    READY TO SCAN       │ │                        │ │                      │
│   < Scan Animation >   │ │                        │ │                      │
└────────────────────────┘ └────────────────────────┘ └──────────────────────┘
```

## Home Assistant entities

Exact entity IDs depend on your installation. After first startup, open **Developer Tools → States** and search for `rfid`, then adjust the dashboard YAML if needed.

Typical entities are:

```text
binary_sensor.rfid_rc522_status
switch.rfid_rc522_buzzer_ein
switch.rfid_rc522_led_ein
```

## Home Assistant actions

The ESPHome configuration exposes these actions:

```text
esphome.rfid_rc522_rfidreader_tag_ok
esphome.rfid_rc522_rfidreader_tag_ko
esphome.rfid_rc522_play_rtttl
```

## Repository structure

```text
Home-Assistant-RFID-RC522-Terminal/
├── README.md
├── README_EN.md
├── LICENSE
├── esphome/
│   ├── rfid-rc522.yaml
│   └── secrets.example.yaml
├── home-assistant/
│   ├── 01-terminal.yaml
│   ├── 02-testconsole.yaml
│   └── 03-control.yaml
├── docs/
│   ├── INSTALLATION_DE.md
│   ├── INSTALLATION_EN.md
│   ├── WIRING.md
│   └── HACS.md
└── images/
    ├── README.md
    ├── dashboard-hero.svg
    ├── wiring-diagram.svg
    ├── hardware-overview.svg
    └── installation-flow.svg
```

## Roadmap

Planned additions include last tag, last scan timestamp, scan counter, access status, user names, admin mode, alarm mode, relay output and event history.

## Compatibility / syntax

The examples use the current ESPHome `api: actions:` syntax and Home Assistant dashboard `perform-action` syntax.

Official documentation:

- ESPHome Native API: https://esphome.io/components/api/
- ESPHome RC522: https://esphome.io/components/binary_sensor/rc522/
- Home Assistant Dashboard Actions: https://www.home-assistant.io/dashboards/actions/

## License

MIT License. See [LICENSE](LICENSE).
