# 📘 GUIDE UTILISATEUR — Projet 1 : Service d’Agrégation de Flux RSS

## Sommaire

1. [Connexion et utilisation de base](#1-connexion-et-utilisation-de-base)
2. [Utilisation avancée (règles, filtres, étiquettes)](#2-utilisation-avancée-règles-filtres-étiquettes)
3. [Automatisation de la mise à jour](#3-automatisation-de-la-mise-à-jour)
4. [FAQ / Problèmes fréquents](#4-faq--problèmes-fréquents)
5. [Astuces et bonnes pratiques](#5-astuces-et-bonnes-pratiques)

# 1. Connexion et utilisation de base

## 1.1 Se connecter à FreshRSS
### 🔹 Adresse d’accès :
http://172.16.10.5/freshrss/
### 🔹 Étapes :
1. Ouvrir un navigateur web (Edge, Firefox ou Chrome).  
2. Entrer l’adresse du serveur FreshRSS ci-dessus.  
3. L’écran d’accueil de FreshRSS s’affiche.  
   **SCREEN**
4. Saisir vos identifiants :
   - **Nom d’utilisateur :** admin  
   - **Mot de passe :** (fourni par l’administrateur)
5. Cliquer sur **Connexion**.

### 🔹 Interface principale :
Une fois connecté, vous accédez :
- à la liste des flux RSS dans la colonne de gauche,  
- au nombre d’articles non lus,  
- et à la zone de lecture à droite.  
**SCREEN**
## 1.2 Se connecter à Tiny Tiny RSS (serveur Linux)
## 1.3 Ajouter le flux FreshRSS sur FluentReader et NewsFlash
Les clients **Windows (Fluent Reader)** et **Ubuntu (NewsFlash)** permettent de consulter les flux à distance via l’API Google Reader.

### 🪟 Sous Windows — Fluent Reader

1. Ouvrez **Fluent Reader** depuis le menu Démarrer.  
2. Allez dans **Settings → Accounts → Add Account**.  
3. Choisissez **Google Reader API**.  
   **SCREEN**
4. Remplissez les champs :
   - **Nom d’affichage :** Serveur FreshRSS  
   - **URL du serveur :** `http://172.16.10.5/freshrss/api/greader.php`  
   - **Nom d’utilisateur :** admin  
   - **Mot de passe :** (mot de passe FreshRSS)
5. Cliquez sur **Connect**.  
6. Vos flux apparaissent automatiquement dans la colonne de gauche.  
   **SCREEN**


---

### 🐧 Sous Ubuntu — NewsFlash

1. Lancez **NewsFlash** depuis le menu Applications.  
2. Sur la page d’accueil, cliquez sur **Add Account**.  
3. Sélectionnez **FreshRSS**.  
   **SCREEN**
4. Renseignez :
   - **Nom d’affichage :** Serveur FreshRSS  
   - **URL du serveur :** `http://172.16.10.5/freshrss/api/greader.php`  
   - **Nom d’utilisateur :** admin  
   - **Mot de passe :** (mot de passe FreshRSS)
5. Cliquez sur **Connect**.  
6. Les flux se synchronisent automatiquement.  
   **SCREEN**


# 2. Utilisation avancée (règles, filtres, étiquettes)
1. Depuis FreshRSS, ouvrez le menu **Catégories**.  
2. Cliquez sur **+ Ajouter une catégorie**.  
3. Entrez un nom (ex. *Veille Tech*, *Cybersécurité*).  
4. Glissez les flux souhaités dans la catégorie correspondante.  
   **SCREEN**

Les catégories sont synchronisées automatiquement avec vos clients.

# 3. Automatisation de la mise à jour

# 4. FAQ / Problèmes fréquents
| Problème                                    | Cause probable                     | Solution                                                 |
| ------------------------------------------- | ---------------------------------- | -------------------------------------------------------- |
| **Erreur cURL 60** lors de l’ajout de flux  | Certificats SSL manquants          | Télécharger `cacert.pem` et le déclarer dans `php.ini`   |
| Impossible de se connecter au flux de FreshRSS | API Google Reader désactivée       | Activer l’API dans les paramètres FreshRSS               |
| “Connection refused” sur Fluent Reader      | Carte réseau désactivée sur la VM  | Réactiver la connexion dans les paramètres réseau Ubuntu |                  |
| Erreur PDO sur Debian                       | Modules PHP manquants              | Installer `php-xml`, `php-intl`, `php-curl`              |

# 5. Astuces et bonnes pratiques
- Sauvegardez régulièrement la base de données MariaDB / PostgreSQL.
- Créez des catégories claires pour vos flux (Tech, Cyber, Réseaux…).
- Testez chaque flux dans un navigateur avant de l’ajouter.
- En cas de changement d’adresse IP du serveur, mettez à jour vos clients Fluent Reader et NewsFlash.