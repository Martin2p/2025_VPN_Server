### Server (Host)
- Ubuntu Server 22.04 LTS (x86_64)
- Mind. 1 vCPU, 1 GB RAM, 5–10 GB Speicher
- Öffentliche IPv4-Adresse oder IPv6
- SSH-Zugriff (z. B. via Terminal oder PuTTY)

### Software
- Docker ≥ 24.0
- WireGuard (wird per Container genutzt)
- iptables oder nftables (für NAT und Firewall)
- systemd (Autostart, Netzwerk)
- Optional in Zusammenarbeit mit iptables: `ufw` zur Firewall-Verwaltung

### Client
- WireGuard-Client für Windows, Linux, Android oder iOS
- Konfigurationsdatei oder QR-Code für Verbindung

### Ports
- UDP-Port **51820** muss erreichbar sein (Portfreigabe im Hosting-Panel)
- Optional: SSH-Port für Wartung (z. B. 22)
