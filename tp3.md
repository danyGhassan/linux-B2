# TP3 Sécu : Linux Hardening

## 1. Guides CIS

### 🌞 Suivre un guide CIS

- la section 2.1
```
fait
```

- les sections 3.1 3.2 et 3.3
```
fait
```

- toute la section 5.2 Configure SSH Server
```
fait
```
- au moins 10 points dans la section 6.1 System File Permissions
```
j'ai fais les 10 premiers
```
- au moins 10 points ailleur sur un truc que vous trouvez utile

```
6.2.3 Ensure all groups in /etc/passwd exist in /etc/group
4.3.4 Ensure users must provide password for escalation
4.3.5 Ensure re-authentication for privilege escalation is not
disabled globally
4.3.6 Ensure sudo authentication timeout is configured correctly
4.5.2.4 Ensure root password is set (Automated)
```

## 2. Conf SSH

### 🌞 Chiffrement fort côté serveur

## 4. DoT

### 🌞 Configurer la machine pour qu'elle fasse du DoT

```
sudo dnf install epel-release -y


-installez systemd-resolved sur la machine pour ça
sudo dnf install systemd-resolved -y

sudo systemctl enable systemd-resolved

sudo systemctl start systemd-resolved

sudo systemctl restart systemd-resolved

sudo cat /etc/systemd/resolved.conf 
DNS=1.1.1.1
Domains=~
DNSSEC=yes
DNSOverTLS=yes


sudo ln -sf /run/systemd/resolve/stub-resolv.conf /etc/resolv.conf
```

### 🌞 Prouvez que les requêtes DNS effectuées par la machine...

- quand on fait un dig ynov.com on voit en bas quel serveur a répondu

```
[dany@localhost ~]$ dig ynov.com

; <<>> DiG 9.16.23-RH <<>> ynov.com
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 33443
;; flags: qr rd ra; QUERY: 1, ANSWER: 3, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 65494
;; QUESTION SECTION:
;ynov.com.			IN	A

;; ANSWER SECTION:
ynov.com.		300	IN	A	104.26.11.233
ynov.com.		300	IN	A	172.67.74.226
ynov.com.		300	IN	A	104.26.10.233

;; Query time: 335 msec
;; SERVER: 127.0.0.53#53(127.0.0.53)
;; WHEN: Sat Jan 18 20:52:03 CET 2025
;; MSG SIZE  rcvd: 85

```

[capture Wireshark](/DoT.pcap)
