## Test und Validierung

#### 1. Schritt: WireGuard starten

Am Beispiel Debian/Ubuntu, mit der Voraussetzung dass alle Einträge zu Peers und Interface in die wg0.conf geschrieben wurden:

```bash
sudo wg-quick up wg0.conf
```

Anschließend den Status prüfen

```bash
sudo wg show
```

-> Hier sollten nun u.a. übertragene Datenmengen und der Zeitpunkt des letzten Handshakes angezeigt werden.


#### 2. Für weitere Tests hat man noch folgende Möglichkeiten:

IP Adresse prüfen:

```bash
ip a
```
oder

```bash
ipconfig
```
Die IP sollte nun derjenigen entsprechen, welche in der wg0.conf im Client als auch auf dem Server für den Client bestimmt wurde.
Prüfen der öffentlichen IP über Dienste wie https://ipinfo.io (sollte Server-IP anzeigen).

Ping-Test:

Server vom Client aus anpingen (ping [VPN-IP des Servers])
Client vom Server aus anpingen (ping [VPN-IP des Clients])

Routing testen:

Prüfen, ob der gesamte Traffic (oder gewählte IP-Bereiche) über VPN läuft (z. B. traceroute / tracert)
