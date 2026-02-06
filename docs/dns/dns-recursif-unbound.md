# Installation d’un serveur DNS récursif sous Debian 12 (Unbound)

## **Introduction**

Dans ce tutoriel, nous allons apprendre à installer et configurer un **serveur DNS récursif** sous **Linux**, en utilisant une machine sous **Debian 12**.

Le **DNS (Domain Name System)** est un service essentiel permettant de traduire les noms de domaine en adresses IP.  
Dans une entreprise, mettre en place un serveur DNS récursif interne permet d’avoir plus de **contrôle**, de **sécurité** et de **performances**.

---

## **Rappels sur le DNS**

### **Types d’enregistrements DNS principaux**

- **NS (Name Server)** : définit les serveurs DNS faisant autorité sur une zone.
- **A** : associe un nom de domaine à une adresse IPv4.
- **AAAA** : associe un nom de domaine à une adresse IPv6.
- **CNAME (Canonical Name)** : alias pointant vers un autre nom de domaine.
- **MX** : définit les serveurs de messagerie d’un domaine (avec priorité).
- **TXT** : enregistrement textuel (SPF, vérifications, etc.).

---

## **Avantages et inconvénients d’un DNS récursif interne**

### **Avantages**

- Amélioration des performances grâce au cache local
- Réduction de la dépendance aux DNS publics (Google, Cloudflare…)
- Sécurité renforcée (filtrage possible des requêtes)
- Contrôle et journalisation des requêtes DNS
- Continuité locale même en cas de panne Internet

### **Inconvénients**

- Complexité de gestion et de maintenance
- Consommation de ressources (CPU, mémoire)
- Point de défaillance unique sans redondance
- Risque d’erreurs de configuration
- Surveillance nécessaire contre les abus DNS

---

## **Installation et configuration du service Unbound**
### **Installation du service**

Mettre à jour le système et installer **Unbound** :

```bash
sudo apt update && sudo apt upgrade
```

Installez le service de journalisation RSYSLOG à la place de journalctl !
Cela permmettra de disposer de fichiers de log clairs au format texte situés dans /var/log

```bash
sudo apt install rsyslog
```


Vérifier la version installée :

```bash
sudo unbound -V
```

Sauvegarde et configuration des fichiers

La configuration d’Unbound se trouve dans :

```bash
/etc/unbound/unbound.conf
```

Avant modification, il est recommandé de sauvegarder le fichier :

```bash
sudo cp /etc/unbound/unbound.conf /etc/unbound/unbound.conf.bak
```

Exemple de configuration Unbound <br>
Ajouter la directive suivante dans le fichier de configuration Unbound :

```bash

include-toplevel: "/etc/unbound/unbound.conf.d/*.conf"


server:
  interface: 172.16.51.100
  interface: 127.0.0.1

  access-control: 172.16.1.0/24 allow
  access-control: 172.16.2.0/24 allow
  access-control: 172.16.3.0/24 allow
  access-control: 172.16.4.0/24 allow
  access-control: 172.16.0.0/24 allow
  access-control: 127.0.0.0/8 allow
  access-control: 0.0.0.0/0 refuse

  hide-version: yes
  hide-identity: yes
  do-ip4: yes
  verbosity: 3
```

### Ce que fait cette configuration

✅ **Contrôle d’accès**
- Autorise uniquement les réseaux internes définis (VLAN)

✅ **Sécurité**
- Bloque toutes les requêtes DNS externes
- Masque l’identité et la version du serveur DNS

✅ **Durcissement**
- Réduit la surface d’attaque du service DNS




Démarrage du service Unbound

Démarrer le service :

```bash
sudo systemctl start unbound
```
Vérifier son état :

```bash
sudo systemctl status unbound
```
Configuration des clients

### Configuration sous Windows

1. Ouvrir le **Panneau de configuration**
2. Aller dans **Réseau et Internet → Centre Réseau et partage**
3. Cliquer sur **Modifier les paramètres de la carte**
4. Clic droit sur la carte réseau → **Propriétés**
5. Sélectionner **IPv4** → **Propriétés**
6. Cocher **Utiliser l’adresse de serveur DNS suivante**
7. Entrer l’IP du serveur DNS interne
8. Valider avec **OK**


Configuration sous Linux

Éditer le fichier de résolution DNS :

```bash
sudo nano /etc/resolv.conf
```

### Configuration du résolveur DNS

Ajouter ou modifier la ligne suivante dans le fichier :

```bash
nameserver 192.168.1.1
```
    ℹ️ Remarque
    Remplacer 192.168.1.1 par l’adresse IP de votre serveur DNS interne.


---

## 🔍 Test de fonctionnement


Le bon fonctionnement du serveur DNS peut être vérifié de plusieurs manières :

- 🔎 **Test de résolution de noms**
  - `ping google.com`
  - `nslookup google.com`

- 📡 **Analyse réseau**
  - Observation des requêtes DNS via **Wireshark**
---
## **Conclusion**

Mettre en place un serveur DNS récursif interne avec Unbound est une solution efficace pour améliorer les performances et renforcer le contrôle des requêtes DNS dans une entreprise.

Même si cela demande plus de travail en termes d’installation et de maintenance, les bénéfices en sécurité, indépendance et maîtrise du réseau sont significatifs.
C’est donc un choix pertinent pour une infrastructure professionnelle.