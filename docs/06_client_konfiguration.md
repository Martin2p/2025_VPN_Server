### Client Konfigurationen auf dem Server

Damit sich neue Clients mit dem WireGuard-Server verbinden können, müssen diese zunächst in der "wg0.conf" hinzugefügt werden.


Hierfür gibt es 2 Varianten.

#### 1. Mit Docker

```bash
docker exec -it wireguard /app/add-peer client2
```

#### 2. Manuell

Einträge in der "wg0.conf" auf dem Server vornehmen (Beispiel):

```bash
# Client2
[Peer]
PublicKey  = 4wXUQna8RVJKgryxHs+7HronfEcmnsIJjqNCuhm4wS8=
AllowedIPs = 10.0.1.20/32
```


## Schlüsselerzeugung für den Client 
(nur bei manueller Konfiguration notwendig)

Falls du den Client manuell konfigurierst, musst du zuvor ein Schlüsselpaar erzeugen:

```bash
wg genkey | tee client2_private.key | wg pubkey > client2_public.key
```

client2_private.key ist der private Schlüssel des Clients → kommt in dessen wg0.conf

client2_public.key ist der öffentliche Schlüssel → wird in die wg0.conf auf dem Server eingetragen


-> hierbei handelt es sich um WireGuard Keys, nicht um SSH-Keys!
Diese dienen ausschließlich der VPN-Authentifizierung und haben mit dem SSH-Zugriff nichts zu tun.


---

### Client Konfigurationen auf dem Client (unter Linux)

Um sich mit dem WireGuard-Server verbinden zu können, muss WireGuard auf dem Client installiert werden:

(hier am Beispiel für Debian(Ubuntu)

```bash
sudo apt install wireguard
```

Anschließend wird bspw. eine Datei mit der Bezeichnung "wg0.conf" und folgendem Inhalt angelegt:

```bash
[Interface]
PrivateKey = [privater Key]
Address = 10.0.1.20/24
DNS = 1.1.1.1

# Server
PublicKey = [PublicKey]
AllowedIPs = 0.0.0.0
Endpoint = [Server IP Adresse]
PersistentKeepalive = 25
```

---

### Verbindung vom Client unter Windows

Für Windows-Clients empfiehlt sich die offizielle [WireGuard-App für Windows](https://www.wireguard.com/install/).

Dort kann die zuvor erstellte Konfigurationsdatei (`client2.conf`) einfach über **"Import tunnel(s) from file..."** geladen und aktiviert werden.

> Weitere Details zum Windows-Client findest du ggf. in einer separaten Anleitung.
