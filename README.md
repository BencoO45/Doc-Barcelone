# 📚 Documentations Réseau & Systèmes

Ce dépôt regroupe l’ensemble des **documentations techniques** que j’ai réalisées durant mes années de **BTS SIO** (option SISR).

Les documents abordent principalement des thématiques liées à :
- l’**administration systèmes**
- les **services réseau**
- la **sécurité**
- les **infrastructures informatiques**

Chaque documentation s’appuie sur des **cas pratiques**, des **configurations réelles** et des **explications détaillées**, dans une logique pédagogique et professionnelle.

---

## ⚠️ Avertissement

> Les configurations présentées dans ces documents sont fournies à titre **d’exemple pédagogique**.  
> Avant toute mise en production, il est indispensable d’**adapter les paramètres** à votre **contexte**, votre **architecture réseau** et vos **contraintes de sécurité**.

---

## 📂 Contenu du dépôt

- 🌐 **DNS** – Résolution de noms, serveurs récursifs, sécurité DNS  
- 📡 **DHCP** – Attribution automatique des adresses IP  
- 🏢 **Active Directory** – Gestion des domaines, utilisateurs et GPO  
- 🔐 **Sécurité** – Bonnes pratiques, filtrage, durcissement  
- 🖥️ **Systèmes** – Administration Linux & Windows Server

---

## 🎯 Objectifs

- Consolider mes compétences en **administration réseau et systèmes**
- Produire une documentation **claire, structurée et réutilisable**
- Servir de **support de révision** et de **référence technique**

## DNS

Cette section regroupe l’ensemble des documentations liées au **Domain Name System (DNS)**.

Le DNS est un service fondamental des réseaux informatiques, permettant la **résolution des noms de domaine en adresses IP**.  
Il joue un rôle clé en termes de **disponibilité**, de **performances** et de **sécurité**.

Les documents présents ici couvrent notamment :
- le fonctionnement du DNS
- la configuration de serveurs DNS (récursifs et/ou internes)
- les bonnes pratiques de sécurité
- des cas pratiques sous Linux et Windows

> ⚠️ **Important**  
> Pensez toujours à adapter les configurations DNS à votre environnement (adressage IP, VLAN, politiques de sécurité).

## DHCP

Cette section est dédiée au **Dynamic Host Configuration Protocol (DHCP)**.

Le DHCP permet d’attribuer automatiquement les paramètres réseau aux machines clientes (adresse IP, passerelle, DNS, etc.), facilitant ainsi la gestion des réseaux, notamment en environnement professionnel.

Les documentations incluent :
- le fonctionnement du protocole DHCP
- l’installation et la configuration de serveurs DHCP
- la gestion des pools, réservations et options
- des scénarios pratiques et courants

> ⚠️ **Important**  
> Toute configuration DHCP doit être pensée en fonction du plan d’adressage et de l’architecture réseau existante.

## Active Directory

Cette section regroupe les documentations liées à **Active Directory** et à la gestion des environnements Windows Server.

Active Directory est un service centralisé permettant la **gestion des utilisateurs**, des **ordinateurs**, des **groupes** et des **stratégies de sécurité** au sein d’un domaine.

Les documents abordent :
- l’installation et la configuration d’un domaine
- la gestion des utilisateurs et des groupes
- les stratégies de groupe (GPO)
- les bonnes pratiques d’administration

> ⚠️ **Important**  
> Les configurations Active Directory doivent être adaptées à la taille de l’entreprise, au nombre d’utilisateurs et aux exigences de sécurité.

# Charte de documentation technique

## 1. Structure recommandée
- Introduction
- Rappels théoriques (si nécessaire)
- Installation
- Configuration
- Tests de fonctionnement
- Conclusion

## 2. Conventions d’écriture
- Langage clair, professionnel et pédagogique
- Pas de langage SMS
- Verbes à l’infinitif pour les actions
- Titres courts et explicites

## 3. Commandes
- Toujours dans des blocs ```bash
- Une commande = une ligne si possible
- Explication hors du bloc de code

## 4. Actions graphiques (GUI)
- Utiliser des listes numérotées ou à puces
- Ne jamais les mettre dans des blocs de code

## 5. Mise en valeur
- ⚠️ pour les avertissements
- ℹ️ pour les informations
- ✅ pour les validations ou résultats attendus
