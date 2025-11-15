
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

## Présentation

**FreshRSS** est un agrégateur de flux RSS libre et auto-hébergé, permettant de centraliser des actualités depuis plusieurs sources.  
Ce guide décrit la procédure complète d’installation sur **Windows Server 2022**, à l’aide de **WAMP**.

---

## 1. Préparer le serveur Windows

Avant toute installation :
- Connectez-vous avec un compte administrateur.
- Vérifiez les mises à jour Windows.
- Désactivez temporairement le pare-feu Windows Defender si nécessaire pour les tests internes.  

---

### 1.1 Installer Microsoft Visual C++ Redistributables

WAMP requiert plusieurs versions de Visual C++ pour fonctionner correctement.

1. Rendez-vous sur :  
   [https://wampserver.aviatechno.net/](https://wampserver.aviatechno.net/)
2. Téléchargez et installez toutes les versions x86 et x64 (2008 à 2022).  
3. Redémarrez le serveur une fois l’installation terminée.

![Visuall C++ instalation image](https://github.com/WildCodeSchool/TSSR-1025-P1-G4/blob/Safiullah/Ressources/installation%20C%2B%2B.PNG)


---

## 2. Installer WAMP Server

### 2.1 Télécharger WAMP

1. Téléchargez la version 64 bits de WAMP sur :  
   [https://wampserver.aviatechno.net/](https://wampserver.aviatechno.net/)
2. Exécutez le fichier `.exe`.
3. Choisissez le dossier d’installation par défaut :  
   `C:\wamp64\`
4. Acceptez les options proposées et lancez WAMP automatiquement à la fin.

![Wamp instalation image](https://github.com/WildCodeSchool/TSSR-1025-P1-G4/blob/Safiullah/Ressources/wamp%20instalation%20start.PNG)

🧠 *Astuce :*  
Si l’icône WAMP est **orange ou rouge**, vérifiez que :
- Tous les **Visual C++ Redistributables** sont installés.  
- Le **port 80** n’est pas utilisé par un autre service (comme IIS ou Skype).

---

### 2.2 Vérifier WAMP

Lorsque l’icône devient **verte**, les trois services sont actifs :
- Apache ✅  
- PHP ✅  
- MariaDB ✅  

![Wamp vrification](https://github.com/WildCodeSchool/TSSR-1025-P1-G4/blob/Safiullah/Ressources/wamp-verification.jpg)

---

## 3. Configurer MariaDB

### 3.1 Accéder à phpMyAdmin

1. Cliquez sur l’icône WAMP dans la barre des tâches.  
2. Sélectionnez **phpMyAdmin**.  
3. L’interface s’ouvre : [http://localhost/phpmyadmin](http://localhost/phpmyadmin)  
4. Connectez-vous :
   - Utilisateur : `root`
   - Mot de passe : *(laisser vide par défaut)*  

![php-myadim-image](https://github.com/WildCodeSchool/TSSR-1025-P1-G4/blob/Safiullah/Ressources/php-my-adimconfig.jpg)

---

### 3.2 Créer la base de données FreshRSS

1. Cliquez sur **Nouvelle base de données**.  
2. Nommez-la `freshrss`.  
3. Choisissez l’interclassement : `utf8mb4_general_ci`.  
4. Cliquez sur **Créer**.  

![adding-new-basse-forfreshrss](https://github.com/WildCodeSchool/TSSR-1025-P1-G4/blob/Safiullah/Ressources/adding%20newbasse.jpg)

---

### 3.3 Créer un utilisateur dédié

1. Dans **Comptes d’utilisateurs → Ajouter un compte utilisateur**.  
2. Renseignez :
   - Nom d’utilisateur : `freshrss`
   - Hôte : `localhost`
   - Mot de passe : un mot de passe fort  
3. Cochez **Donner tous les privilèges sur la base freshrss**.  
4. Cliquez sur **Exécuter**.  

🧠 *Astuce :*  
Ne jamais utiliser `root` pour les applications. Créez toujours un utilisateur dédié pour plus de sécurité.

![creating-new-user-for-freshrss](https://github.com/WildCodeSchool/TSSR-1025-P1-G4/blob/Safiullah/Ressources/creating-user-mariasql.jpg)

---

## 4. Télécharger et préparer FreshRSS

### 4.1 Télécharger FreshRSS

1. Rendez-vous sur le dépôt officiel :  
   [https://github.com/FreshRSS/FreshRSS/releases](https://github.com/FreshRSS/FreshRSS/releases)
2. Téléchargez la dernière version stable (ZIP).  
3. Extrayez le contenu du ZIP dans :  
   `C:\wamp64\www\`
4. Renommez le dossier en **freshrss** (en minuscules).

![freshrss-downloading-reanaming](https://github.com/WildCodeSchool/TSSR-1025-P1-G4/blob/Safiullah/Ressources/freesrss%20changing%20name%20and%20extract%20to%20wwwfolder.PNG)

---

## 5. Créer et configurer l’alias Apache

### 5.1 Donner les permissions Windows

1. Clic droit sur le dossier :  
   `C:\wamp64\www\freshrss\`
2. Onglet **Sécurité** → **Modifier les autorisations**.  
3. Ajoutez l’utilisateur **Everyone** → cochez **Lecture et exécution**, **Lecture**, **Écriture**.  
4. Appliquez les modifications à tous les sous-dossiers (`p/`, `data/`, `config/`).

![adding-permissions-frss-dr](https://github.com/WildCodeSchool/TSSR-1025-P1-G4/blob/Safiullah/Ressources/permision%20de%20droit%20freshrss-11-15%20222619.jpg)

---

### 5.2 Créer l’alias via WAMP

1. Cliquez sur l’icône WAMP → **Apache → Alias directories → Add an alias**.  
2. Dans la fenêtre :  
   - Alias name : `freshrss`  
   - Directory path : `C:/wamp64/www/freshrss/p/`  
3. Cliquez sur **OK**.

![alias-creating](https://github.com/WildCodeSchool/TSSR-1025-P1-G4/blob/Safiullah/Ressources/configurer%20l'alias.PNG)

---

### 5.3 Modifier l’accès réseau de l’alias

1. Ouvrez le fichier d’alias créé :  
   `C:\wamp64\alias\freshrss.conf`
2. Vérifiez qu’il contient bien :
```
Alias /freshrss "C:/wamp64/www/freshrss/p/  
<Directory "C:/wamp64/www/freshrss/p/">  
Options +Indexes +FollowSymLinks +MultiViews  
AllowOverride All  
Require all granted  
</Directory>`
```

3. Sauvegardez et fermez.

![apache-configuration](https://github.com/WildCodeSchool/TSSR-1025-P1-G4/blob/Safiullah/Ressources/apache%20configuration%20donssier%20myalias.conf-%20require%20all%20granted.PNG)

---

### 5.4 Redémarrer WAMP

Cliquez sur l’icône WAMP → **Restart All Services**.  
L’icône doit devenir **verte**.  

![WAMP-restart](https://github.com/WildCodeSchool/TSSR-1025-P1-G4/blob/Safiullah/Ressources/wamp%20instalation%20start.PNG)

---

## 6. Installer FreshRSS

1. Ouvrez dans votre navigateur :  
`http://localhost/freshrss/`  
2. Suivez l’assistant d’installation.

---

### 6.1 : Langue

Choisissez **Français**, puis cliquez sur **Suivant**.  

---

### 6.2 : Vérification système

Tous les modules doivent apparaître en vert.  
Si certains sont rouges, activez-les dans WAMP → PHP → **PHP Extensions** :  
- `curl`  
- `mbstring`  
- `openssl`  
- `pdo_mysql`  

Puis redémarrez WAMP.  
![fsrr-vrification](https://github.com/WildCodeSchool/TSSR-1025-P1-G4/blob/Safiullah/Ressources/instalation%20freshrss.PNG)

---

### 6.3 : Base de données

Remplissez les champs :  

| Champ              | Valeur             |
| ------------------ | ------------------ |
| Type de base       | MariaDB            |
| Hôte               | localhost          |
| Utilisateur        | freshrss           |
| Mot de passe       | votre_mot_de_passe |
| Base de données    | freshrss           |
| Préfixe des tables | freshrss_          |

Cliquez sur **Valider** → **Installer**.  
![frss-database-configuration](https://github.com/WildCodeSchool/TSSR-1025-P1-G4/blob/Safiullah/Ressources/instalation%20freshrss%20etape%203.PNG)

---

### 6.4 : Compte administrateur

| Champ                      | Exemple                 |
| -------------------------- | ----------------------- |
| Nom d’utilisateur          | admin                   |
| Mot de passe               | votre_mot_de_passe      |
| Méthode d’authentification | Formulaire traditionnel |

Cliquez sur **Installer FreshRSS**.  
![frss-useracoutncreationg](https://github.com/WildCodeSchool/TSSR-1025-P1-G4/blob/Safiullah/Ressources/instalation%20freshrss%20etape%204.PNG)

---

## 7. Correction du problème `cURL error 60` (SSL)

Lors de l’ajout d’un flux HTTPS, FreshRSS peut afficher :  
`cURL error 60: SSL certificate problem: unable to get local issuer certificate`

Ce problème vient de l’absence du fichier de certificats racine (`cacert.pem`) dans PHP.

---

### 7.1 : Télécharger `cacert.pem`

Téléchargez depuis le site officiel :  
👉 [https://curl.se/ca/cacert.pem](https://curl.se/ca/cacert.pem)

Placez le fichier dans :  
`C:\wamp64\bin\php\php8.3.14\extras\ssl\cacert.pem`

> Créez les dossiers `extras\ssl` s’ils n’existent pas.

**SCREEN**

---

### 7.2 : Modifier le fichier `php.ini`

1. Ouvrez `http://localhost/phpinfo.php`.  
2. Repérez la ligne :
	Loaded Configuration File
	→ Copiez le chemin indiqué (souvent dans `apache/bin/php.ini`).
3. Ouvrez ce fichier avec le Bloc-notes.
4. Ajoutez à la fin :
	curl.cainfo = "C:/wamp64/bin/php/php8.3.14/extras/ssl/cacert.pem"
	openssl.cafile = "C:/wamp64/bin/php/php8.3.14/extras/ssl/cacert.pem"
5. Enregistrez, puis redémarrez Apache :
	WAMP → Apache → **Restart Service**

**SCREEN**

---

###  7.3 : Vérification

Retournez sur `phpinfo()` et vérifiez que :

| Directive | Valeur |
|------------|--------|
| `curl.cainfo` | C:/wamp64/bin/php/php8.3.14/extras/ssl/cacert.pem |
| `openssl.cafile` | C:/wamp64/bin/php/php8.3.14/extras/ssl/cacert.pem |

✅ Si c’est le cas, la configuration SSL fonctionne.  
FreshRSS peut maintenant ajouter des flux HTTPS sans erreur.

**SCREEN**

---

## 8. Vérification finale

- WAMP : icône verte ✅  
- Accès à `http://localhost/freshrss/` ✅  
- Accès depuis une VM : `http://172.16.10.5/freshrss/` ✅  
- Ajout de flux HTTPS fonctionnel ✅  
- Aucun message `cURL error 60` dans les logs ✅  

**SCREEN**

---

## 9. Liens utiles

- Visual C++ Redistributables : [https://wampserver.aviatechno.net/](https://wampserver.aviatechno.net/)  
- WAMP Server : [https://wampserver.aviatechno.net/](https://wampserver.aviatechno.net/)  
- FreshRSS (releases) : [https://github.com/FreshRSS/FreshRSS/releases](https://github.com/FreshRSS/FreshRSS/releases)  
- Certificats CA officiels : [https://curl.se/ca/cacert.pem](https://curl.se/ca/cacert.pem)


---

# 3. Installation sur le serveur Linux (TT-RSS)

## Étape 1. Pré-requis

- Debian récente
- Accès root ou sudo
- Apache2
- PHP 8.x avec extensions : pgsql, xml, mbstring, curl, gd, intl
- PostgreSQL
- Accès réseau sortant fonctionnel (DNS et Internet)

---

## Étape  2. Mettre Debian à jour

Exécuter :

`apt update && apt upgrade -y`

---

## Étape  3. Installer les dépendances nécessaires

Installer Apache, PHP et modules requis, ainsi que PostgreSQL :

`apt install apache2 php php-cli php-fpm php-mbstring php-xml php-curl php-gd php-json php-pgsql php-intl git -y`

`apt install postgresql -y`

---

## Étape  4. Correction DNS (si nécessaire)

Si la VM ne résout pas les noms de domaine (ex. git.tt-rss.org) :

Éditer `/etc/resolv.conf` :

`nano /etc/resolv.conf`

Ajouter :

nameserver 1.1.1.1
nameserver 8.8.8.8

Si le fichier se verrouille automatiquement, empêcher sa réécriture :

`chattr -i /etc/resolv.conf`

Vérifier la résolution :

`ping git.tt-rss.org`

---

## Étape 5. Installation de Tiny Tiny RSS

Aller dans le répertoire `/var/www` :

`cd /var/www`

Cloner le dépôt officiel TT-RSS :

`git clone https://git.tt-rss.org/fox/tt-rss.git ttrss`

Attribuer les droits à l’utilisateur web `www-data` :

`chown -R www-data:www-data /var/www/ttrss`

---

## Étape 6. Configuration d’Apache

Créer un VirtualHost pour TT-RSS afin que le serveur web serve correctement l’application.  
Créer le fichier de configuration :  
nano /etc/apache2/sites-available/ttrss.conf
Ajouter le contenu suivant :  
<VirtualHost *:80>  
    ServerName 172.16.10.6  
	DocumentRoot /var/www/ttrss  
	<Directory /var/www/ttrss/>
        AllowOverride All  
		Require all granted  
		</Directory>  
		</VirtualHost>
 
| ServerName          | IP de la VM |    
| DocumentRoot        | répertoire TT-RSS |    
| AllowOverride All   | permet l’usage de .htaccess pour les réécritures d’URL |    
| Require all granted | autorise l’accès à tous les clients |  

Activer le site et le module rewrite :  
a2ensite ttrss.conf  
a2enmod rewrite  
systemctl reload apache2

-----

## Étape 7. Configuration PostgreSQL

7.1 Créer l’utilisateur PostgreSQL    
sudo -u postgres createuser ttrssuser -P    
Définir un mot de passe sécurisé pour ttrssuser.

7.2 Créer la base TT-RSS  
sudo -u postgres createdb -O ttrssuser ttrss

7.3 Attribuer les droits nécessaires  
Se connecter en tant que postgres :  
sudo -i -u postgres    
psql    
Attribuer tous les privilèges :    
ALTER USER ttrssuser WITH SUPERUSER;    
GRANT ALL PRIVILEGES ON DATABASE ttrss TO ttrssuser;    
GRANT ALL PRIVILEGES ON SCHEMA public TO ttrssuser;    
ALTER SCHEMA public OWNER TO ttrssuser;    
\q    
exit    

------

## Étape 8. Initialisation du schéma de base TT-RSS  
Exécuter le schéma SQL fourni par TT-RSS pour créer toutes les tables et fonctions nécessaires :  
sudo -u postgres psql -U ttrssuser -d ttrss -f /var/www/ttrss/sql/pgsql/schema.sql  

------

## Étape 9. Premier lancement et configuration Web  
Ouvrir dans le navigateur :  
http://172.16.10.6  
Configurer l’accès à la base :  
| Base         | ttrss |    
| Utilisateur  | ttrssuser |    
| Mot de passe | celui défini précédemment |    
| Type         | PostgreSQL |    
Changer le mot de passe par défaut du compte admin.  

-----


## Étape 10. Mise à jour du schéma TT-RSS (obligatoire)  
cd /var/www/ttrss  
sudo -u www-data php update.php --update-schema  
Cette étape assure que TT-RSS reconnaît toutes les tables et fonctions.  

-------

## Étape 11. Ajouter des flux RSS  
Dans TT-RSS → Configuration → Flux → Ajouter un flux  
Exemples :  
CERT-FR : https://www.cert.ssi.gouv.fr/feed/  
Korben : https://korben.info/feed  
Organiser les flux dans des catégories.  

-------

## Étape 12. Créer des catégories  
Configuration → Flux → Catégories → Ajouter  
Exemples :  
Cyber  
Actus  
Tech  
Déplacer les flux dans leur catégorie correspondante.  

--------

##  Étape 13. Test de mise à jour manuelle des flux  
Avant d’automatiser avec Cron, tester la récupération des flux :  
cd /var/www/ttrss  
sudo -u www-data php update.php --feeds  
Si aucune erreur n’apparaît, tout fonctionne.  

---------

## Étape 14. Automatisation avec Cron  
Créer un fichier cron :  
nano /etc/cron.d/ttrss  
Ajouter la ligne suivante pour mettre à jour les flux toutes les 15 minutes :  
*/15 * * * * www-data php /var/www/ttrss/update.php --feeds >> /var/log/ttrss_feeds.log 2>&1  
Appliquer les droits corrects :  
chmod 644 /etc/cron.d/ttrss  
systemctl restart cron  
Vérifier les logs :  
tail -n 20 /var/log/ttrss_feeds.log  

---------

## 15. Vérifications finales  
Vérifier Apache : systemctl status apache2  ✅  
Vérifier PostgreSQL : systemctl status postgresql  ✅  
Vérifier que TT-RSS récupère bien des articles via l’interface Web.  ✅  

----------

## Liens utiles
TT-RSS Git : https://git.tt-rss.org/fox/tt-rss.git

CERT-FR feed : https://www.cert.ssi.gouv.fr/feed/

Documentation PostgreSQL : https://www.postgresql.org/docs/

Apache docs : https://httpd.apache.org/docs/

---

# 4. Installation sur les clients

## 4.1 Fluent Reader sur Windows

### Présentation

**Fluent Reader** est un lecteur RSS moderne, open source et multiplateforme.  
Il permet de regrouper plusieurs flux RSS dans une interface claire et rapide, disponible sur **Windows**, **Ubuntu** et **macOS**.  
L’application peut également se connecter à un serveur distant tel que **FreshRSS** via l’API Google Reader.

---

### 1. Vérification de l’environnement

Avant de commencer, assurez-vous que :
- Vous êtes connecté avec un compte administrateur.  
- Votre système est à jour.  

#### Sous Windows
- L’installation se fait depuis le **Microsoft Store** ou via le fichier d’installation `.exe` disponible sur le site officiel.  

---
### 3. Installation sur Windows

1. Ouvrez le **Microsoft Store**.  
    **SCREEN**
2. Recherchez **Fluent Reader**.  
    **SCREEN**
3. Cliquez sur **Obtenir** ou **Installer**.  
    **SCREEN**
4. Une fois l’installation terminée, l’application est disponible dans le menu **Démarrer**.

---
### 4. Lancer Fluent Reader

1. Ouvrez le menu **Démarrer** (Windows)
2. Recherchez **Fluent Reader**.
3. Cliquez pour lancer l’application.
4. L’interface principale s’affiche.  
    **SCREEN**

---

### 5. Connexion à un serveur FreshRSS

Fluent Reader peut se connecter directement à un serveur **FreshRSS** pour récupérer et synchroniser vos flux.

1. Dans le menu principal, ouvrez **Settings → Service**.  
    **SCREEN**
2. Choisissez le type de compte **Google Reader API**.  
    **SCREEN**
3. Remplissez les champs avec les informations de votre serveur FreshRSS :
    |Champ|Description|Exemple|
    |---|---|---|
   |**Adresse**|Adresse de l’API Google Reader|`http://172.16.10.5/freshrss/api/greader.php`|
    |**Pseudo**|Votre identifiant FreshRSS|`admin`|
    |**Mot de passe**|Votre mot de passe FreshRSS|`motdepasse`|
	**SCREEN**
4. Cliquez sur **Connect** pour établir la liaison avec le serveur.
5. Si la connexion réussit, vos flux RSS apparaissent automatiquement dans Fluent Reader.

🧠 _Important :_  
L’URL doit pointer vers **l’API Google Reader** (`/api/greader.php`) et non vers la racine du site FreshRSS.

---

### 6. Vérification de la synchronisation

1. Depuis l’interface de **FreshRSS**, ajoutez un nouveau flux RSS (via le navigateur).
2. Dans **Fluent Reader**, cliquez sur le bouton **Refresh (🔄)** pour actualiser les flux.  
    **SCREEN**
3. Le nouveau flux doit apparaître automatiquement.
4. Marquez un article comme **lu** dans Fluent Reader, puis vérifiez dans FreshRSS : il doit apparaître comme **lu** également.

✅ Si ces deux vérifications fonctionnent, la synchronisation entre le client et le serveur est opérationnelle.

---

## 4.2 NewsFlash sur Ubuntu

### Présentation
**NewsFlash** est un lecteur RSS pour Linux qui permet de centraliser vos flux d’actualités,  
et surtout de se synchroniser directement avec un serveur **FreshRSS**.  
C’est une solution simple, graphique et rapide pour consulter vos flux RSS depuis le client **UBU01**.

---

### 1. Pré-requis

Avant de commencer, assurez-vous que :
- Votre poste **Ubuntu (UBU01)** dispose d’un accès Internet.
- Votre serveur **FreshRSS** est déjà installé et fonctionnel (ex. `http://[ADRESSE_IP_SERVEUR]/freshrss`).
- Vous connaissez vos identifiants de connexion FreshRSS :
  - Nom d’utilisateur  
  - Mot de passe  

---

### 2. Ouvrir le **Centre d’applications Ubuntu**

1. Cliquez sur l’icône **“Centre d’applications”** (sac orange dans la barre de gauche).  
   **SCREEN**
2. Dans la barre de recherche en haut, tapez :  
3. Sélectionnez **NewsFlash** dans les résultats de recherche.  
**SCREEN**

---

### 3. Installation de NewsFlash

1. Cliquez sur le bouton **“Installer”**.  
**SCREEN**
2. Patientez le temps que l’installation se termine (quelques secondes).  
3. Une fois terminée, le bouton devient **“Ouvrir”**.  
4. Cliquez dessus pour lancer directement l’application.

---

### 4. Première ouverture de NewsFlash

1. Lors du premier lancement, NewsFlash vous demande de **choisir une source de flux RSS**.  
**SCREEN**
2. Cliquez sur le bouton **“Add Account”** (ou “Ajouter un service”).  
3. Une liste de services compatibles s’affiche.

---

### 5. Connexion à votre serveur FreshRSS

1. Sélectionnez **FreshRSS** dans la liste des services.  
**SCREEN**
2. Renseignez les champs de connexion :
- **Nom d’affichage :** le nom du compte local (ex. *Serveur FreshRSS*).  
- **URL du serveur :** l’adresse complète du service (ex. `http://[ADRESSE_IP_SERVEUR]/freshrss/api/greader.php`).  
- **Nom d’utilisateur :** votre identifiant FreshRSS.  
- **Mot de passe :** votre mot de passe FreshRSS.
3. Cliquez sur **“Connect”**.  
**SCREEN**
4. NewsFlash vérifie la connexion et importe automatiquement vos flux et dossiers depuis le serveur.

🧠 *Important :*  
L’URL doit pointer vers **l’API Google Reader** de FreshRSS (`/api/greader.php`), sinon la synchronisation échouera.

---

### 6. Consultation de vos flux RSS

1. Une fois connecté, la fenêtre principale s’affiche avec :
- Vos flux RSS importés depuis FreshRSS dans la colonne de gauche.  
- Les articles au centre.  
- Le contenu de l’article sélectionné à droite.  
**SCREEN**

2. Cliquez sur un flux pour afficher les articles récents.  
3. Les articles lus sont automatiquement marqués comme **lus** dans FreshRSS.

🧠 *Synchronisation :*  
Toute action effectuée dans NewsFlash (lecture, marquage, suppression) se synchronise automatiquement avec le serveur FreshRSS.

---

### 7. Rafraîchir les flux

1. Cliquez sur le bouton **🔄 Actualiser** dans la barre supérieure.  
2. Les nouveaux articles apparaissent immédiatement.  
3. Vous pouvez aussi activer la mise à jour automatique dans :

---

# 5. Automatisation de la mise à jour

## Sur Windows (FreshRSS)
## Sur Linux (TT-RSS)
