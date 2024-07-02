
# HACS einrichten 

* Webseite: https://hacs.xyz/

HACS muss einmalig manuell im Container installiert werden:

```
docker compose exec app bash
wget -O - https://get.hacs.xyz | bash -
exit
```

Anschließend muss die Integration HACS hinzugefügt werden.
Eine Anmeldung bei GitHub ist hierbei erforderlich.
Anschließend muss Homeassistant neu gestartet werden.
Wenn das Icon vom HACS Menüentrag fehlt muss der Broser Cache einmal geleert werden.

# Manuell eingerichtete Integrationen / Geräte 

## Sonne 

Nach Installation automatisch vorhanden

* Integration: Sonne 
* Umbenennen in: Sun
* Alle Entitäten aktivieren 

## Wetter 

Nach Installation automatisch vorhanden

* Integration: Forecast von Met.no 
* Name: Home
* Breitengrad, Längengrad, Höhe: <aus configuration.yaml>

## MQTT Broker

* Integration: MQTT 
* Server: Feste IP des MQTT Brokers
* Port: 1883
* Benutzername: Leer 
* Passswort: Leer 
* Umbenennen in: MQTTBroker

## ZHA / SLZB-06 

Der SLZB-06 ist über Netzwerk angeschlossen.

* Radio Type: ZNP
* socket://192.168.0.18:6638

## Homematic CCU3

* In HACS (s. oben) muss zuerst das folgende Repository hinzugefügt werden: 
  * https://github.com/danielperna84/custom_homematic
  * Kategorie: Integrationen
* Anschließend ist die Integration "Homematic(IP) Local" verfügbar und kann heruntergeladen werden
* Der Benutzer Admin in der CCU3 muss ein Paswort gesetzt haben
* In der Firewall Konfiguration der CCU3 muss die IP des Homeassistant-Servers explizit freigegeben werden
* Solange das Webinterface er CUU2 geöffnet ist, sind keine Verbindungen von Homeassistant möglich

* Seite 1:
  * Integration: Homematic(IP) Local
  * Instanzname: HomematicCCU3
  * Host: Feste IP der CCU3
  * Benutzername: Admin
  * Passwort: *****
  * TLS: Nein
  * TLS: Überprüfen: Nein
  * Callback Host: IP Des Docker-Hosts 
  * Callback Port: 12001 
  * JSON-RPC Port: 80
  * Aktiver Sysvar Scan: Ja
  * Sysvar Scan Interval: 30
  * Aktive Systembanachrichtigungen: Ja

* Seite 2:
  * Aktiviere Homematic IP: Ja
  * HmIP-RF Port: 2010
  * Aktiviere Homematic (Bidcos-RF): Ja
  * HM-RF Port: 2001
  * Aktiviere Heizgruppen: Nein
  * Gruppen Port: 9292
  * Gruppen-Plan: /groups
  * Aktiviere Homematic-Wired (Bidcos-Wired): Nein
  * BidCos-Wired Port: 2000
