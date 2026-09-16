# Home Assistant RFID RC522 Terminal

Ein kompaktes RFID-Zugangsterminal auf Basis eines **ESP32-C3**, **MFRC522/RC522** und **ESPHome** mit direkter Integration in **Home Assistant**.

Das Projekt stellt RFID-Tags als Home-Assistant-Tag-Ereignisse bereit und bietet zusätzlich Buzzer-, LED- und Testfunktionen. Für das Dashboard gibt es eine tabletfreundliche Oberfläche mit animierter Scan-Anzeige und separaten Bereichen für Terminal, Testkonsole und Steuerung.

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

## Hardware

- ESP32-C3 DevKitM-1 oder kompatibles Board
- RC522 RFID-Modul
- passiver Piezo-Buzzer
- optionale LED mit passendem Vorwiderstand
- Jumper-Kabel

## Verdrahtung

| RC522 | ESP32-C3 |
|---|---|
| SCK | GPIO9 |
| MISO | GPIO5 |
| MOSI | GPIO6 |
| SDA / SS | GPIO7 |
| RST | GPIO10 |
| 3.3 V | 3.3 V |
| GND | GND |

Zusätzlich:

| Funktion | ESP32-C3 |
|---|---|
| Buzzer | GPIO8 |
| Status-LED | GPIO2 |

**RC522 nur mit 3,3 V betreiben.**

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

Die exakten Entity-IDs hängen von deiner Installation ab. Nach dem ersten Start unter

**Entwicklerwerkzeuge → Zustände → nach `rfid` suchen**

prüfen und bei Bedarf die YAML-Karten anpassen.

Typische Entitäten dieses Projekts sind:

```text
binary_sensor.rfid_rc522_status
switch.rfid_rc522_buzzer_ein
switch.rfid_rc522_led_ein
```

Bei älteren Konfigurationen können die IDs anders aussehen.

## Home-Assistant-Aktionen

Die ESPHome-Konfiguration stellt folgende Aktionen bereit:

```text
esphome.rfid_rc522_rfidreader_tag_ok
esphome.rfid_rc522_rfidreader_tag_ko
esphome.rfid_rc522_play_rtttl
```

Auch hier kann der tatsächliche Präfix je nach Gerätename abweichen.

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
    └── README.md
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
