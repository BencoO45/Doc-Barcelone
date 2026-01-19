# Installation et configuration d’un serveur DHCP sous Debian 12 (KEA)

## Présentation

Ce document décrit l’installation et la configuration d’un serveur **DHCP** sous **Debian 12** à l’aide de la solution **ISC KEA DHCP Server**.

### Prérequis

- Une machine Debian avec une **adresse IP statique**  
  Exemple : `192.168.14.99/24`
- Aucun autre serveur DHCP actif sur le réseau (éviter les conflits)
- Une machine cliente (Debian, Ubuntu, Windows…) **sans configuration IP**
- Une connexion Internet pour installer les paquets

---

## Installation du serveur DHCP KEA

Avant toute chose, mettre à jour le système et installer le serveur DHCP KEA :

```bash
sudo apt-get update
sudo apt-get install kea-dhcp4-server

Vérifier l’état du service :

sudo systemctl status kea-dhcp4-server

Le service utilise le fichier de configuration suivant :

/etc/kea/kea-dhcp4.conf

Configuration du serveur DHCP KEA
Identifier l’interface réseau

Afficher la configuration réseau afin d’identifier le nom de l’interface :

ip a

Dans cet exemple, l’interface utilisée est ens33.
Préparer le fichier de configuration

Renommer le fichier de configuration par défaut afin de repartir sur une base propre :

sudo mv /etc/kea/kea-dhcp4.conf /etc/kea/kea-dhcp4.conf.bkp

Créer et éditer le nouveau fichier :

sudo nano /etc/kea/kea-dhcp4.conf

Configuration globale du serveur DHCP

Ajouter la configuration suivante :

{
  "Dhcp4": {
    "interfaces-config": {
      "interfaces": [ "ens33" ]
    },

    "valid-lifetime": 691200,
    "renew-timer": 345600,
    "rebind-timer": 604800,

    "authoritative": true,

    "lease-database": {
      "type": "memfile",
      "persist": true,
      "name": "/var/lib/kea/kea-leases4.csv",
      "lfc-interval": 3600
    }
  }
}

Création d’une étendue DHCP

Pour distribuer des adresses IP sur le réseau 192.168.2.0/24, ajouter une étendue DHCP :

{
  "Dhcp4": {
    "interfaces-config": {
      "interfaces": [ "ens33" ]
    },

    "valid-lifetime": 691200,
    "renew-timer": 345600,
    "rebind-timer": 604800,

    "authoritative": true,

    "lease-database": {
      "type": "memfile",
      "persist": true,
      "name": "/var/lib/kea/kea-leases4.csv",
      "lfc-interval": 3600
    },

    "subnet4": [
      {
        "subnet": "192.168.2.0/24",
        "pools": [
          { "pool": "192.168.2.1 - 192.168.2.125" }
        ],
        "option-data": [
          {
            "name": "domain-name-servers",
            "data": "8.8.8.8"
          },
          {
            "name": "domain-search",
            "data": "local.epoka2.lan"
          },
          {
            "name": "routers",
            "data": "192.168.2.126"
          }
        ]
      }
    ]
  }
}

Explication des options

    domain-name-servers : serveur DNS distribué aux clients

    domain-search : domaine de recherche local

    routers : passerelle par défaut

    pools : plage d’adresses IP attribuées aux clients

⚠️ Attention à la syntaxe JSON :
chaque élément doit se terminer par une virgule, sauf le dernier.
Redémarrage et vérification du service

Redémarrer le serveur DHCP :

sudo systemctl restart kea-dhcp4-server.service

Si le service ne démarre pas, consulter les logs :

sudo journalctl -xe | grep -e kea

Une erreur de syntaxe dans le fichier de configuration peut empêcher le démarrage du service.
Test de fonctionnement

Configurer un poste client pour qu’il obtienne automatiquement une adresse IP via DHCP.

Si le poste reçoit :

    une adresse IP

    une passerelle

    un serveur DNS

👉 alors le serveur DHCP est fonctionnel.
Conclusion

Le serveur DHCP KEA est désormais opérationnel sous Debian 12 et prêt à distribuer automatiquement les paramètres réseau aux clients.
