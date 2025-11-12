# 🧰 INSTALLATION — Projet 1 : Service d’Agrégation de Flux RSS

## Sommaire

1. [Prérequis techniques](#1-prérequis-techniques)
2. [Installation sur le serveur Windows (FreshRSS)](#2-installation-sur-le-serveur-windows-freshrss)
3. [Installation sur le serveur Linux (TT-RSS)](#3-installation-sur-le-serveur-linux-tt-rss)
4. [Installation sur les clients](#4-installation-sur-les-clients)
5. [Automatisation de la mise à jour](#5-automatisation-de-la-mise-à-jour)
6. [FAQ / Dépannage](#6-faq--dépannage)

# 1. Prérequis techniques

### Matériel et environnement

| Élément | Description |
|----------|-------------|
| Hyperviseur | VirtualBox |
| Nombre de machines | 4 (2 serveurs + 2 clients) |
| Réseau Client windows | NAT — 172.16.10.10/24 |
| Réseau Client Linux | NAT - 172.16.10.20/24 |
| Réseau Serveur Windows | NAT - 172.16.10.5/24 |
| Réseau Serveur Linux | NAT - 172.16.10.6/24 |
| Accès Internet | Activé sur les serveurs |
| Pare-feux | Désactivés pour les tests |
| Résolution de noms | Fichier `hosts` ou DNS local |

### Comptes et identifiants

| Machine | Nom | Identifiant | Mot de passe |
|----------|-----|--------------|---------------|
| SRVWIN01 | Serveur Windows | Administrateur | (à définir) |
| SRVLX01 | Serveur Linux | root / utilisateur | (à définir) |
| WIN01 | Client Windows | utilisateur local | (à définir) |
| UBU01 | Client Linux | utilisateur local | (à définir) |

### Logiciels nécessaires

- FreshRSS
- Tiny Tiny RSS
- WAMP
- LAMP
- Visual C++
- ... 

---

# 2. Installation sur le serveur Windows (FreshRSS)

## Étape 1 -

---

# 3. Installation sur le serveur Linux (TT-RSS)

## Étape 1 — 

---

# 4. Installation sur les clients

## Installation et gestion de Fluent Reader sur Ubuntu et Windows.

Présentation **Fluent Reader** est un lecteur RSS moderne, open source et multiplateforme.   Il permet de regrouper plusieurs flux RSS dans une interface claire et rapide, disponible sur **Ubuntu**, **Windows** et **macOS**.  ---  

### 1. Vérification de l’environnement  Avant de commencer : 

- Vous êtes connecté avec un compte **sudo**. - Le système est à jour : 
```bash sudo apt update && sudo apt upgrade -y```

🧠 Note :_ sous Windows, l’installation se fait via le **Microsoft Store** ou le **setup officiel (.exe)

---
### 2. Accéder au Centre d’applications Ubuntu

1. Ouvrir le **Centre d’applications** (icône orange sur la barre latérale).
2. Cliquer sur **Explorer**.
3. Dans la barre de recherche, saisir :
    `Fluent Reader`
4. Sélectionner l’application dans la liste des résultats.  
---
### 3. Installation de Fluent Reader

1. Depuis la fiche de l’application :
	- Vérifier la version (ex. `0.7.4`)
	- Vérifier le **canal** : `latest/beta`
	- Licence : **BSD-3-Clause**

2. Cliquer sur **Installer**.  
3. Attendre la fin du téléchargement (~63 Mo).
4. Une fois installée, l’application apparaît dans le menu **Applications**.

💡 _Alternative ligne de commande :_

`sudo snap install fluent-reader`

---
### 4. Lancer Fluent Reader

1. Ouvrir le menu **Afficher les applications** (neuf points en bas à gauche).
2. Rechercher **Fluent Reader** et lancer le programme.
3. L’interface principale s’affiche :  

---
### 5. Ajouter un flux RSS

1. Ouvrir l’onglet **Sources**.
2. Dans la section **Add Source**, saisir l’URL du flux de votre choix :
    ex :`https://www.lemonde.fr/rss/en_continu.xml`
3. Cliquer sur **Add**.  
4. Le flux apparaît désormais dans la liste.

🧠 _Astuce :_ tester le lien dans un navigateur si le flux ne s’affiche pas (vérifier certificat HTTPS ou disponibilité).

---
### 6. Créer des groupes de flux

1. Ouvrir l’onglet **Groups**.
2. Dans le champ **Create Group**, saisir un nom (ex. `IT`).
3. Cliquer sur **Create**.
4. Sélectionner un flux existant et l’ajouter à ce groupe.  

🧠 _Bonnes pratiques :_
- Créez des groupes par thématique : _Tech_, _Sécurité_, _Linux_…
- Cela facilite la lecture et la veille quotidienne.

---
### 7. Supprimer un flux RSS

1. Allez dans l’onglet **Sources**.
2. Sélectionnez le flux que vous souhaitez supprimer.  
3. En bas de la fenêtre, cliquez sur le bouton **Delete source** (rouge).  
4. Confirmez la suppression.

🧠 _Note :_
- Cela supprime également les articles associés à ce flux.
- Vous pouvez ensuite le réimporter via “Add Source” si besoin.

---
### 8. Paramètres et préférences

|Menu|Fonction principale|
|---|---|
|**Sources**|Gestion et ajout de flux|
|**Groups**|Organisation thématique|
|**Rules**|Filtres automatiques|
|**Service**|Connexion à un serveur distant (FreshRSS, TT-RSS, etc.)|
|**Preferences**|Mode sombre, fréquence d’actualisation, affichage|

💡 _Exemple :_  
Pour forcer l’affichage complet des articles → **Preferences → RSS full text**

---
### 9. Désinstallation de Fluent Reader

Sous Ubuntu :
`sudo snap remove fluent-reader`

Sous Windows :
- Ouvrir _Applications et fonctionnalités_
- Rechercher _Fluent Reader_
- Cliquer sur _Désinstaller_

---

# 5. Automatisation de la mise à jour

## Sur Windows (FreshRSS)
## Sur Linux (TT-RSS)
