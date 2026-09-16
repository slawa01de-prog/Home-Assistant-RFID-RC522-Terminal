# Installation – Deutsch

![Installation in 4 Schritten](../images/installation-flow.svg)

## Voraussetzungen

- Home Assistant
- ESPHome
- HACS
- HACS Frontend-Komponente **Button Card**
- optional **card-mod**
- ESP32-C3
- RC522
- passiver Buzzer
- optional LED + 220–330 Ω Widerstand

## 1. Hardware verdrahten

Verdrahte zuerst RC522, Buzzer und LED gemäß:

![Verdrahtungsplan](../images/wiring-diagram.svg)

Die vollständige Pin-Tabelle steht zusätzlich in [WIRING.md](WIRING.md).

## 2. ESPHome konfigurieren

`esphome/rfid-rc522.yaml` in ESPHome übernehmen.

Danach in deiner privaten `secrets.yaml` folgende Einträge anlegen:

```yaml
wifi_ssid: "MEIN_WLAN"
wifi_password: "MEIN_PASSWORT"
rfid_api_key: "DEIN_ESPHOME_API_KEY"
rfid_ota_password: "DEIN_OTA_PASSWORT"
rfid_fallback_password: "DEIN_FALLBACK_PASSWORT"
```

Keine echten Zugangsdaten in GitHub speichern.

## 3. ESP flashen

ESPHome-Konfiguration validieren und anschließend über USB oder OTA installieren.

## 4. Home Assistant Integration

Nach dem Start sollte Home Assistant das ESPHome-Gerät erkennen. Falls nicht:

**Einstellungen → Geräte & Dienste → Integration hinzufügen → ESPHome**

Danach die ESPHome-Integration des Geräts öffnen, **Konfigurieren** wählen und **„Home-Assistant-Aktionen erlauben“** aktivieren. Das ist für `homeassistant.tag_scanned` erforderlich.

## 5. Entity-IDs prüfen

Unter:

**Entwicklerwerkzeuge → Zustände**

nach `rfid` suchen.

Die Entity-IDs können von den Beispielen im Repository abweichen. Passe dann die drei Dashboard-Dateien an.

## 6. HACS

Über HACS → Frontend installieren:

- Button Card
- optional card-mod

Danach Browser/App vollständig neu laden.

## 7. Dashboard

Im Dashboard drei Abschnitte nebeneinander anlegen:

1. Terminal
2. Testkonsole
3. Steuerung

Je Abschnitt eine manuelle YAML-Karte einfügen und den Inhalt der entsprechenden Datei übernehmen:

- `home-assistant/01-terminal.yaml`
- `home-assistant/02-testconsole.yaml`
- `home-assistant/03-control.yaml`

Beispielansicht:

![RFID Dashboard](../images/dashboard-hero.svg)

## 8. RFID testen

Tag an den RC522 halten. Im ESPHome-Log sollte die UID erscheinen und Home Assistant erhält ein Tag-Ereignis.

Unter **Einstellungen → Tags** kann der Tag anschließend für Automationen verwendet werden.
