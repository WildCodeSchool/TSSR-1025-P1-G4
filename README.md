#  Projet 1 Service d’Agrégation de Flux RSS

## Sommaire 

- [ Présentation du projet](#présentation-du-projet)
- [ Introduction](#introduction)
- [ Membres du groupe par sprint](#membres-du-groupe-par-sprint)
- [ Choix techniques](#choix-techniques)
- [ Difficultés rencontrées](#difficultés-rencontrées)
- [ Solutions trouvées](#solutions-trouvées)
- [ Améliorations possibles](#améliorations-possibles)

---

# Présentation du projet

## Projet 1 Service d’Agrégation de Flux RSS

Ce projet vise à déployer deux agrégateurs RSS sur serveurs **Windows** et **Linux**,  
et à permettre la consultation et la mise à jour automatique des flux depuis des postes clients.

**Contexte :**  
Dans le cadre de la formation **TSSR (Technicien Supérieur Systèmes et Réseaux)** à la Wild Code School,  
l’objectif est de concevoir une infrastructure simple permettant de **centraliser des flux RSS**,  
de les rendre accessibles depuis plusieurs machines, et d’automatiser leur mise à jour.

**Objectif final :**  
- Créer deux serveurs (Windows et Linux) capables d’agréger et de diffuser des flux RSS,  
- Permettre la consultation depuis les clients (Windows et Ubuntu),  
- Automatiser la mise à jour des flux, 
- (Optionnel) Créer des **règles automatiques** (étiquettes, marquage).

---

# Introduction

Un **flux RSS** est un fichier XML listant les dernières publications d’un site web.  
Un **agrégateur RSS** regroupe ces flux pour offrir une lecture centralisée et simplifiée.

## Objectifs techniques
- Installer **FreshRSS** sur un serveur Windows (SRVWIN01)  
- Installer **Tiny Tiny RSS (TT-RSS)** sur un serveur Linux (SRVLX01)  
- Permettre la consultation depuis les postes clients : WIN01 et UBU01  
- Automatiser les mises à jour sur chaque serveur  
- Tester des lecteurs RSS clients : **Fluent Reader** et **NewsFlash**  
- Mettre en place la synchronisation entre clients et serveur  

---

# Membres du groupe par sprint

## Sprint 1 Installation & configuration

| Membre | Rôle | Missions principales |
|--------|------|----------------------|
| **Safiullah** | Product Owner | Installation et configuration de FreshRSS (Windows Server), création des clients (Windows & Ubuntu), gestion réseau |
| **Matthias** | Scrum Master | Installation et configuration de TT-RSS (Debian), documentation (`README`, `INSTALL`, `USER_GUIDE`), coordination et suivi GitHub |

## Sprint 2 Automatisation & documentation

| Membre | Rôle | Missions principales |
|--------|------|----------------------|
| **Matthias** | Product Owner | Gestion avec le client, correction des problèmes de flux sur FreshRSS, installation et configuration des logiciels de bureau client |
| **Safiullah** | Scrum Master | Gestion du planning, correction des problèmes sur le serveur Debian documentation prèparation (Guide Install TTRSS, FreshRSS |

---

# Choix techniques

## **Matériel & environnement**

| Élément | Description |
|----------|--------------|
| Hyperviseur | VirtualBox |
| Nombre total de machines | 4 |
| Réseau interne | 172.16.10.0/24 |
| SRVWIN01 | Windows Server 2022 — IP 172.16.10.5 |
| SRVLX01 | Debian 13 — IP 172.16.10.6 |
| WIN01 | Client Windows — IP 172.16.10.10 |
| UBU01 | Client Ubuntu — IP 172.16.10.20 |
| Accès Internet | Activé pour les serveurs |
| Résolution de noms | Fichier `hosts` |
| Pare-feux | Désactivés pour les tests |

---

### Serveur Windows (SRVWIN01)
- **Système :** Windows Server 2022  
- **Logiciel :** FreshRSS  
- **Serveur web :** WAMP (Apache2 + MariaDB + PHP)  
- **Base de données :** MariaDB  
- **Automatisation :** Potentiellement le "Planificateur de tâches Windows"

### Serveur Linux (SRVLX01)
- **Système :** Debian 13  
- **Logiciel :** Tiny Tiny RSS (TT-RSS)  
- **Serveur web :** LAMP (Apache2 + PHP + MariaDB)  
- **Base de données :** PostgreSQL  
- **Automatisation :** Potentiellement "Cron job / systemd timer"  

### Clients (WIN01 et UBU01)
- **Windows :** Fluent Reader  
- **Ubuntu :** NewsFlash  
- Test de la connexion directe au serveur FreshRSS via `/api/greader.php`  

---

# Difficultés rencontrées

### Côté Windows FreshRSS
- Mauvaise lecture des flux RSS au départ (erreur cURL).  
- API Google Reader non activée (empêchait la synchronisation avec NewsFlash).  

### Côté Debian TT_RSS
- Problème : DNS Résolution réseau
- Erreur **PDO** lors de l’installation (connexion SQL échouée).
- Dépendances PHP manquantes (`php-xml`, `php-intl`, `php-curl`).  
- Blocages prolongés sans test sur un autre environnement (Ubuntu).  
- Nouvelle version de TT-RSS n’est pas compatible avec MariaDB/MySQL → passage vers **PostgreSQL

### Côté clients (UBU01)
- Aucune connexion entre Fluent Reader et FreshRSS.  
- Problème de reconnaissance Unicode UTF-8 avec Fluent Reader.  

---

# Solutions trouvées

| Problème | Solution mise en place |
|-----------|-----------------------|
| Problème  DNS  | Édition de `/etc/resolv.conf` pour ajouter des serveurs DNS valides |
| Erreur PDO sur Debian | Installation des modules PHP manquants et mise en place d’une autre base de données PostgreSQL |
| API FreshRSS inactive | Activation manuelle de “l’API Google Reader” dans les paramètres |
| Flux RSS — erreur cURL | Installation du fichier `cacert.pem` manquant dans le dossier `C:/wamp64/bin/php/php8.3.14/extras/ssl/` |
| Blocages techniques prolongés | Échange des rôles entre les membres pour croiser les compétences |

---

# Améliorations possibles

- Conteneuriser FreshRSS et TT_RSS avec Docker.  
- Centraliser les flux sur un seul serveur mutualisé.  
