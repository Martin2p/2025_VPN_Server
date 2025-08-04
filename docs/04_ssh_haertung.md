### SSH Härtung

Folgende Maßnahmen wurden zur Absicherung des SSH-Zugangs auf dem VPN-Server umgesetzt:

-  **SSH-Standardport geändert**  
  → z. B. von Port `22` auf `.......` 

-  **Login per Passwort deaktiviert**  
  → Nur noch Anmeldung mit SSH-Schlüsseln erlaubt (`PasswordAuthentication no`)

-  **Nur Public-Key-Authentifizierung aktiviert**  
  → Schlüssel befinden sich im `~/.ssh/authorized_keys` des Ziel-Users

-  **Root-Login deaktiviert**  
  → Direktes Einloggen als `root` via SSH ist nicht erlaubt (`PermitRootLogin no`)

-  **Fail2ban installiert**  
  → Schutz vor Brute-Force-Angriffen durch temporäres Sperren fehlgeschlagener Loginversuche

-  **Firewall-Regeln angepasst**  
  → Nur der neue SSH-Port ist per `NFTables`

-  **Port-Knocking (optional, nicht aktiv)**  
  → Möglichkeit für zukünftige Härtung (z. B. mit `knockd`)

---

### Beispielkonfiguration in `/etc/ssh/sshd_config`:

```ini
Port ......
PermitRootLogin no
PasswordAuthentication no
ChallengeResponseAuthentication no
UsePAM yes
AllowUsers deinuser
