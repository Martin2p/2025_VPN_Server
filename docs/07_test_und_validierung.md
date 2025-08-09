## Test und Validierung

##### 1. Schritt: WireGuard starten

Am Beispiel Debian/Ubuntu, mit der Voraussetzung dass alle Einträge zu Peers und Interface in die wg0.conf geschrieben wurden:

```bash
sudo wg-quick up wg0.conf
```

Anschließend den Status prüfen

```bash
sudo wg show
```

-> Hier sollten nun u.a. übertragene Datenmengen und der Zeitpunkt des letzten Handshakes angezeigt werden.
