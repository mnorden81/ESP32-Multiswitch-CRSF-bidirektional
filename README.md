# ESP32-MultiSwitch v0.14

RC-gesteuerter 8-Kanal-Schalter für ESP32 mit Web-Interface.

## Änderungen v0.14

- **MWprop-Unterstützung**: Proportionale PWM-Steuerung über CRSF-MWprop-Kommandos.  
  `pwm_wert[x] = 200..207` → Duty aus `wm_prop_value[channel]`
- **CRSF-Timeout 2000 ms** (vorher 1000 ms) – robuster bei kurzen Unterbrechungen
- **getPwmDuty()** Helfer-Funktion für saubere PWM-Quellenauflösung
- **Debug-Tab** zeigt jetzt MWprop-Kanalwerte live
- NVS-Speicherung konsequent bei allen Konfigurationsänderungen

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

IP: `192.168.4.1` (Standard)  
SSID: `MultiSwitch` / Passwort: `123456789`

### API-Endpunkte

| Methode | Pfad | Beschreibung |
|---------|------|--------------|
| GET | `/api/status` | Aktueller Status (Ausgänge, Kanäle, MWprop) |
| GET/POST | `/api/config` | Konfiguration lesen/schreiben |
| POST | `/api/switch` | Ausgang manuell schalten / freigeben |
| POST | `/api/reset` | Werkseinstellungen |
