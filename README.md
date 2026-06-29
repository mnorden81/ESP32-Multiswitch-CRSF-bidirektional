# ESP32-MultiSwitch v0.27

RC-gesteuerter 8-Kanal-Schalter für ESP32 mit Web-Interface.

## Änderungen v0.27

- **CRSF Parser-Fix**: Doppelschreiben des CRC-Bytes im RX-Parser entfernt
- **CRSF Init-Fix**: `init_crsf()` verwendet nun den übergebenen Serial-Port
- **CRSF API-Fix**: `send_command()` korrekt als Klassenmethode implementiert
- **Web-API robuster**: JSON-Strings werden sicher escaped, Eingaben werden valider geparst/validiert
- **NVS-Schreibschutz**: Konfigurationsänderungen werden gebündelt gespeichert (Debounce), Flush vor Neustart
- **Versionskonsistenz**: Firmware, Web-UI und README auf `v0.27` vereinheitlicht

## Pin-Belegung

| GPIO | Funktion |
|------|----------|
| 13 | WiFi-Pin (LOW = AP aktiv) |
| 16 | SBUS RX / CRSF RX |
| 17 | CRSF TX |
| 18–27 | Ausgänge 1–8 |
| 2 | Status-LED |

## Bibliotheken

- Bolder Flight Systems SBUS 8.1.4
- CRSF_ESP32 (https://github.com/Ziege-One/CRSF_ESP32)

## RC-System Werte

| Wert | System |
|------|--------|
| 0 | FrSky (SBUS) |
| 1 | FlySky (SBUS) |
| 2 | ELRS normiert (SBUS) |
| 3 | HoTT (SBUS) |
| 4 | CRSF (ELRS/TBS) |

## Web-Interface

IP: `192.168.1.1` (Standard)  
SSID: `MultiSwitch` / Passwort: `123456789`

### API-Endpunkte

| Methode | Pfad | Beschreibung |
|---------|------|--------------|
| GET | `/api/status` | Aktueller Status (Ausgänge, Kanäle, MWprop) |
| GET/POST | `/api/config` | Konfiguration lesen/schreiben |
| POST | `/api/switch` | Ausgang manuell schalten / freigeben |
| POST | `/api/reset` | Werkseinstellungen |
