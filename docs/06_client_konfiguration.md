### Client Konfigurationen auf dem Server

Damit sich neue Clients mit dem Wireguard Server verbinden können, müssen diese zunächst in der wg0.conf hinzugefügt werden.


Hierfür gibt es 2 Varianten.

##### 1. Mit Docker

```bash
docker exec -it wireguard /app/add-peer client2
```

##### 2. Manuell

Einträge in der wg0.conf vornehmen (Beispiel):

```bash
# Client2
[Peer]
PublicKey  = 4wXUQna8RVJKgryxHs+7HronfEcmnsIJjqNCuhm4wS8=
AllowedIPs = 10.0.1.20/32
```
---

### Client Konfigurationen auf dem Client (unter Linux)

Um sich mit dem Wireguard-Server verbinden zu können, muss Wireguard auf dem Client installiert werden:

(hier am Beispiel für eine Debian-Distribution)

```bash
sudo apt install wireguard
```

Anschließend wird bspw. eine wg0.conf mit folgendem Inhalt angelegt:

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
