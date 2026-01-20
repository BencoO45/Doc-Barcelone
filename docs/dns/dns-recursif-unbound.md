# Installation d’un serveur DNS récursif sous Debian 12 (Unbound)

## Introduction

Dans ce tutoriel, nous allons apprendre à installer et configurer un **serveur DNS récursif** sous **Linux**, en utilisant une machine sous **Debian 12**.

Le **DNS (Domain Name System)** est un service essentiel permettant de traduire les noms de domaine en adresses IP.  
Dans une entreprise, mettre en place un serveur DNS récursif interne permet d’avoir plus de **contrôle**, de **sécurité** et de **performances**.

---

## Rappels sur le DNS

### Types d’enregistrements DNS principaux

- **NS (Name Server)** : définit les serveurs DNS faisant autorité sur une zone.
- **A** : associe un nom de domaine à une adresse IPv4.
- **AAAA** : associe un nom de domaine à une adresse IPv6.
- **CNAME (Canonical Name)** : alias pointant vers un autre nom de domaine.
- **MX** : définit les serveurs de messagerie d’un domaine (avec priorité).
- **TXT** : enregistrement textuel (SPF, vérifications, etc.).

---

## Avantages et inconvénients d’un DNS récursif interne

### Avantages

- Amélioration des performances grâce au cache local
- Réduction de la dépendance aux DNS publics (Google, Cloudflare…)
- Sécurité renforcée (filtrage possible des requêtes)
- Contrôle et journalisation des requêtes DNS
- Continuité locale même en cas de panne Internet

### Inconvénients

- Complexité de gestion et de maintenance
- Consommation de ressources (CPU, mémoire)
- Point de défaillance unique sans redondance
- Risque d’erreurs de configuration
- Surveillance nécessaire contre les abus DNS

---

## Installation et configuration du service Unbound

### Installation du service

Mettre à jour le système et installer **Unbound** :

```bash
sudo apt update
sudo apt install unbound

Vérifier la version installée :

sudo unbound -V

Sauvegarde et configuration des fichiers

La configuration d’Unbound se trouve dans :

/etc/unbound/unbound.conf

Avant modification, il est recommandé de sauvegarder le fichier :

sudo cp /etc/unbound/unbound.conf /etc/unbound/unbound.conf.bak

Exemple de configuration Unbound

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

Cette configuration permet :

    d’autoriser uniquement certains réseaux (VLAN)

    de bloquer les requêtes externes

    de masquer les informations du serveur DNS

Démarrage du service Unbound

Démarrer le service :

sudo systemctl start unbound

Vérifier son état :

sudo systemctl status unbound

Configuration des clients
Configuration sous Windows

    Ouvrir le Panneau de configuration

    Aller dans Réseau et Internet > Centre Réseau et partage

    Cliquer sur Modifier les paramètres de la carte

    Clic droit sur la carte réseau → Propriétés

    Sélectionner IPv4 → Propriétés

    Cocher Utiliser l’adresse de serveur DNS suivante

    Entrer l’IP du serveur DNS interne

    Valider avec OK

Configuration sous Linux

Éditer le fichier de résolution DNS :

sudo nano /etc/resolv.conf

Ajouter ou modifier la ligne :

nameserver 192.168.1.1

(Remplacer par l’adresse IP de ton serveur DNS interne)
Test de fonctionnement

Le bon fonctionnement peut être vérifié :

    en testant la résolution de noms (ping, nslookup)

    ou via Wireshark pour analyser les trames DNS sur le réseau

Conclusion

Mettre en place un serveur DNS récursif interne avec Unbound est une solution efficace pour améliorer les performances et renforcer le contrôle des requêtes DNS dans une entreprise.

Même si cela demande plus de travail en termes d’installation et de maintenance, les bénéfices en sécurité, indépendance et maîtrise du réseau sont significatifs.
C’est donc un choix pertinent pour une infrastructure professionnelle.