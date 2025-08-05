### Firewall & Fail2ban (nftables)

Der Server wurde mit `nftables` abgesichert. Zusätzlich schützt `Fail2ban` vor Brute-Force-Angriffen auf den SSH-Dienst.

---

#### nftables Firewall-Regeln

Es wurde ein minimales Regelset erstellt, das nur die benötigten Ports freigibt:

- UDP **51820** für WireGuard
- TCP **[Portnummer]** für den gehärteten SSH-Zugang
- Alle anderen eingehenden Verbindungen werden blockiert
- NAT / Masquerading für VPN-Clients aktiviert

---

#### 📄 Beispielkonfiguration `/etc/nftables.conf`:

```bash
#!/usr/sbin/nft -f

flush ruleset

table inet filter {
  chain input {
    type filter hook input priority 0;

    # Akzeptiere bereits etablierte Verbindungen
    ct state established,related accept

    # SSH-Zugang (Port wurde geändert)
    tcp dport [Portnummer] accept

    # WireGuard
    udp dport 51820 accept

    # Lokales Interface erlauben (z. B. für interne Kommunikation)
    iif "lo" accept

    # Alles andere blockieren
    counter drop
  }

  chain forward {
    type filter hook forward priority 0;
    policy drop;
  }

  chain output {
    type filter hook output priority 0;
    policy accept;
  }
}

table ip nat {
  chain postrouting {
    type nat hook postrouting priority 100;

    # VPN NAT (z. B. für Subnetz 10.0.1.0/24 über eth0 ins Internet)
    ip saddr 10.0.1.0/24 oifname "eth0" masquerade
  }
}
```

#### nftables aktivieren

```bash
sudo systemctl enable nftables
sudo systemctl start nftables
```

---

### Fail2ban – Schutz vor SSH-Brute-Force-Angriffen
Fail2ban scannt die Authentifizierungs-Logs und blockiert IPs mit zu vielen fehlgeschlagenen Anmeldeversuchen.

###### Installation:

```bash
sudo apt install fail2ban
```

Beispielkonfiguration /etc/fail2ban/jail.local:


```bash
[sshd]
enabled  = true
port     = [Portnummer]
logpath  = /var/log/auth.log
maxretry = 5
bantime  = 1h
```

##### Fail2ban aktivieren und starten:

```bash
sudo systemctl enable fail2ban
sudo systemctl start fail2ban
```

##### Status anzeigen:

```bash
sudo fail2ban-client status sshd
```
