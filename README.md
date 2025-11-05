![logo de la Wild Code SChool en exemple](Ressources/logo_WCS.jpg)

## Sommaire 

- [🎯 Présentation du projet](#presentation-du-projet)
- [📜 Introduction](#introduction)
- [👥 Membres du groupe par sprint](#membres-du-groupe-par-sprint)
- [⚙️ Choix Techniques](#choix-techniques)
- [🧗Difficultés rencontrées](#difficultes-rencontrees)
- [💡 Solutions trouvées](#solutions-trouvees)
- [🚀 Améliorations possibles](#ameliorations-possibles)

# 🎯 Présentation du projet

## Projet 1 — Service d’Agrégation de Flux RSS
Ce projet vise à déployer deux agrégateurs RSS sur serveurs Windows et Linux.

**Contexte :**  
Dans le cadre de notre formation **TSSR (Technicien Supérieur Systèmes et Réseaux)** à la Wild Code School, nous devons mettre en place un service permettant de **regrouper et de consulter automatiquement des flux RSS** depuis plusieurs sources d’actualités.

**Objectif final :**  
Créer deux serveurs (Windows et Linux) capables d’agréger, d’actualiser et d’afficher des flux RSS consultables depuis des postes clients, tout en automatisant la mise à jour et le tri des flux.

# 📜 Introduction

Un **flux RSS** est un fichier XML contenant la liste des dernières publications d’un site web.  
Un **agrégateur RSS** est une application qui regroupe automatiquement ces flux pour permettre une lecture centralisée.

Notre projet consiste à :
- Installer **FreshRSS** sur un serveur Windows (SRVWIN01),
- Installer **Tiny Tiny RSS (TT-RSS)** sur un serveur Linux (SRVLX01),
- Permettre la **consultation depuis deux postes clients** (WIN01 et UBU01),
- Automatiser la **mise à jour des flux RSS** sur chaque serveur,
- Créer des **règles automatiques** (filtrage, étiquettes, marquage automatique). (Optionnelle)



# 👥 Membres du groupe par sprint

**Sprint 1**

| Membre   | Rôle       | Missions |
| -------- | ---------- | -------- |
| Safiullah | Product Owner  | Gestion client, Mise en place du serveur Windows, Connection flux RSS et création des bdd, Créations des machines clientes (windows et linux) |
| Matthias | Scrum Master | Organisation, coordination, rédaction du README & INSTALL, Mise en place du serveur Linux, Connection flux RSS et création des bdd |

**Sprint 2**

| Membre   | Rôle       | Missions |
| -------- | ---------- | -------- |
| Matthias | PO         | -        |
| Safiullah | SM         | -        |

# ⚙️ Choix techniques

## **Matériel & environnement**

| Élément | Description |
|----------|--------------|
| Hyperviseur | VirtualBox |
| Nombre total de machines | 4 |
| Réseau Client windows | Interne — 172.16.10.10/24 |
| Réseau Client Linux | Interne - 172.16.10.20/24 |
| Réseau Serveur Windows | Interne - 172.16.10.5/24 |
| Réseau Serveur Linux | Internet - 172.16.10.6/24 |
| Accès Internet | Activé sur tous les serveurs |
| Pare-feux | Désactivés pour les tests |
| Résolution par nom | Fichier `hosts`|

### 🪟 Serveur Windows (SRVWIN01)

- **Système :** Windows Server 2022  
- **Logiciel :** FreshRSS  
- **Serveur Web :** IIS (ou WAMP)  
- **Base de données :** SQLite / MariaDB  
- **Automatisation :** Planificateur de tâches Windows

### 🐧 Serveur Linux (SRVLX01)
- **Système :** Debian 12  
- **Logiciel :** Tiny Tiny RSS (TT-RSS)  
- **Serveur Web :** Apache2 + PHP + MariaDB  
- **Automatisation :** cron job / systemd timer  

### 💻 Clients (WIN01 et UBU01)
- Accès via navigateur (Firefox / Edge)
- Test de lecteurs de bureau : *QuiteRSS*, *Fluent Reader*, *Feedbro*

# 🧗 Difficultés rencontrées

# 💡 Solutions trouvées

# 🚀 Améliorations possibles
