# Wiring / Verdrahtung

## Verdrahtungsplan

![Verdrahtungsplan](../images/wiring-diagram.svg)

## RC522 → ESP32-C3

| RC522 Pin | ESP32-C3 Pin | Beschreibung |
|---|---|---|
| 3.3V | 3V3 | Versorgung |
| GND | GND | Masse |
| SCK | GPIO9 | SPI Clock |
| MISO | GPIO5 | SPI MISO |
| MOSI | GPIO6 | SPI MOSI |
| SDA / SS | GPIO7 | SPI Chip Select |
| RST | GPIO10 | Reset |

## Zusätzliche Ausgänge

| Funktion | GPIO | Hinweis |
|---|---|---|
| passiver Buzzer + | GPIO8 | RTTTL-Ausgabe |
| passiver Buzzer - | GND | gemeinsame Masse |
| Status-LED Anode | GPIO2 über 220 Ω | optional |
| Status-LED Kathode | GND | gemeinsame Masse |

## Hinweise

- RC522 immer mit **3,3 V** versorgen.
- **Keine 5 V** am RC522 anlegen.
- Bei externer LED immer einen **Vorwiderstand** verwenden.
- Für RTTTL muss ein **passiver Piezo-Buzzer** verwendet werden.
- Falls dein ESP32-C3-Board GPIO2 anderweitig nutzt, `status_led` in der ESPHome-YAML auf einen freien GPIO ändern.

## Benötigte Hardware

![Benötigte Hardware](../images/hardware-overview.svg)
