# Fiche de procédure n°6 : Fail2Ban (Protection DoS)

## Objectif
Protéger un serveur (ex : DNS récursif) contre les attaques DoS en bloquant automatiquement les IP suspectes.

## Installation
```
sudo apt update
sudo apt install fail2ban -y
`Activation`
sudo systemctl enable fail2ban
sudo systemctl start fail2ban
```

Configuration

Fichier :

/etc/fail2ban/jail.local

Exemple :

```
[DEFAULT]
bantime = 600
findtime = 600
maxretry = 10

[named]
enabled = true
port = 53
logpath = /var/log/syslog
```
Pour Vérification
```
sudo fail2ban-client status
```
Résultat
Les IP suspectes sont automatiquement bloquées via le pare-feu.