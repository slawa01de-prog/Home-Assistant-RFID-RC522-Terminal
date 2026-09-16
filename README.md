# Home Assistant RFID RC522 Terminal

Ein kompaktes RFID-Zugangsterminal auf Basis eines **ESP32-C3**, **MFRC522/RC522** und **ESPHome** mit direkter Integration in **Home Assistant**.

Das Projekt stellt RFID-Tags als Home-Assistant-Tag-Ereignisse bereit und bietet zusätzlich Buzzer-, LED- und Testfunktionen. Für das Dashboard gibt es eine tabletfreundliche Oberfläche mit animierter Scan-Anzeige und separaten Bereichen für Terminal, Testkonsole und Steuerung.

[English version](README_EN.md)

![Projektbanner](images/dashboard-hero.svg)

> **Hinweis:** API-Schlüssel, OTA-Passwörter und WLAN-Zugangsdaten gehören ausschließlich in `secrets.yaml` und niemals in ein öffentliches Repository.

## Funktionen

- ESP32-C3 + RC522 über SPI
- RFID-Tags an Home Assistant senden
- Buzzer über RTTTL
- Buzzer in Home Assistant ein-/ausschaltbar
- optionale Status-LED
- Online-/Offline-Anzeige
- Testaktionen für OK, Fehler, Erfolgsmelodie und Alarmton
- animierte Tablet-GUI mit `custom:button-card`
- kompakte Darstellung ohne vertikales Scrollen auf typischen Tablet-Auflösungen

## Beispielgrafiken

### Verdrahtungsplan

![Verdrahtungsplan](images/wiring-diagram.svg)

### Benötigte Hardware

![Benötigte Hardware](images/hardware-overview.svg)

### Installationsablauf

![Installationsablauf](images/installation-flow.svg)

## Hardware

- ESP32-C3 DevKitM-1 oder kompatibles Board
- RC522 RFID-Modul
- passiver Piezo-Buzzer
- optionale LED mit passendem Vorwiderstand
- Jumper-Kabel
- RFID-Tag oder RFID-Karte

## Verdrahtung

| Signal / Modul | ESP32-C3 |
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
| LED Anode | GPIO2 über 220 Ω |
| LED Kathode | GND |

**RC522 nur mit 3,3 V betreiben.**

Ausführliche Verdrahtung: [docs/WIRING.md](docs/WIRING.md)

## Installation

1. ESPHome in Home Assistant installieren bzw. verwenden.
2. `esphome/rfid-rc522.yaml` in ESPHome übernehmen.
3. Werte aus `esphome/secrets.example.yaml` in deine eigene `secrets.yaml` übertragen.
4. Firmware auf den ESP32-C3 installieren.
5. Das ESPHome-Gerät in Home Assistant hinzufügen.
6. In der ESPHome-Integration für das Gerät **„Home-Assistant-Aktionen erlauben“** aktivieren, damit `homeassistant.tag_scanned` funktionieren kann.
7. Über HACS die **Button Card** installieren.
8. Optional **card-mod** installieren.
9. Browser/App vollständig neu laden.
10. Die drei Dashboard-Karten aus `home-assistant/` in drei Dashboard-Abschnitte einfügen.
11. Falls deine Entity-IDs abweichen, diese in den Karten anpassen.

Ausführlicher: [docs/INSTALLATION_DE.md](docs/INSTALLATION_DE.md)

## Dashboard-Aufbau

Empfohlene Tablet-Anordnung:

```text
┌────────────────────────┐ ┌────────────────────────┐ ┌──────────────────────┐
│ RFID ACCESS TERMINAL   │ │ RFID Testkonsole       │ │ RFID Steuerung       │
│ ● SYSTEM ONLINE        │ │ ✓ erlaubt   ! gesperrt │ │ Verbindung Firmware  │
│                        │ │ ♪ Erfolg    🚨 Alarm    │ │ Buzzer      LED      │
│    READY TO SCAN       │ │                        │ │                      │
│   < Scan-Animation >   │ │                        │ │                      │
└────────────────────────┘ └────────────────────────┘ └──────────────────────┘
```

## Home-Assistant-Entitäten

Die exakten Entity-IDs hängen von deiner Installation ab. Nach dem ersten Start unter **Entwicklerwerkzeuge → Zustände → nach `rfid` suchen** prüfen und bei Bedarf die YAML-Karten anpassen.

Typische Entitäten dieses Projekts sind:

```text
binary_sensor.rfid_rc522_status
switch.rfid_rc522_buzzer_ein
switch.rfid_rc522_led_ein
```

## Home-Assistant-Aktionen

Die ESPHome-Konfiguration stellt folgende Aktionen bereit:

```text
esphome.rfid_rc522_rfidreader_tag_ok
esphome.rfid_rc522_rfidreader_tag_ko
esphome.rfid_rc522_play_rtttl
```

## Verzeichnisstruktur

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

Geplant sind unter anderem:

- letzter RFID-Tag
- letzte Scan-Zeit
- Scan-Zähler
- Zugriff erlaubt / verweigert
- Benutzername statt reiner UID
- Admin-Modus
- Alarm-Modus
- Relais-/Türöffner-Ausgang
- Ereignis-Historie
- Benachrichtigungen bei unbekannten Tags

## Kompatibilität / verwendete Syntax

Die Beispielkonfiguration verwendet die aktuelle ESPHome-Syntax `api: actions:` sowie die aktuelle Home-Assistant-Dashboard-Aktion `perform-action`.

Offizielle Dokumentation:

- ESPHome Native API: https://esphome.io/components/api/
- ESPHome RC522: https://esphome.io/components/binary_sensor/rc522/
- Home Assistant Dashboard Actions: https://www.home-assistant.io/dashboards/actions/

## Lizenz

MIT License. Siehe [LICENSE](LICENSE).
