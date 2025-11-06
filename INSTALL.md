## Sommaire

# * Mon guide détaillé : Installer FreshRSS sur Windows Server avec WAMP et MariaDB *

* Je vais vous expliquer toutes les étapes que j’ai suivies pour installer FreshRSS sur Windows Server 2022, 


## 1. Préparer le serveur

Avant de toucher à WAMP ou FreshRSS, j’ai dû m’assurer que mon serveur avait tous les prérequis nécessaires.

1.1 Installer Microsoft Visual C++ Redistributables

WAMP a besoin de plusieurs versions de Visual C++ pour fonctionner correctement.

Je suis allé sur le site  https://wampserver.aviatechno.net/ pour télécharger les packages x86 et x64 de 2008 à 2022.
J’ai installé chaque version une par une.

Après l’installation, j’ai redémarré mon serveur pour que tout soit pris en compte.

## 2. Installer WAMP Server
### 2.1 Télécharger WAMP

J’ai téléchargé WAMP depuis le site: https://wampserver.aviatechno.net/ -> download-wampserver-64bits

J’ai choisi la version 64 bits car mon Windows Server est 64 bits.

## 2.2 Installer WAMP

J’ai lancé le fichier d'instalation (.exe)

⚠️ Astuce : si l’icône est orange ou rouge, je vérifie que Visual C++ est bien installé et que le port 80 n’est pas occupé par une autre application (Skype, IIS…).

J’ai accepté toutes les étapes de l’assistant.

J’ai choisi le dossier par défaut : C:\wamp64\

À la fin, j’ai coché l’option pour démarrer WAMP automatiquement.

Une fois lancé, l’icône de WAMP est devenue verte, ce qui signifie que :

Apache fonctionne

PHP fonctionne

MariaDB fonctionne


## 3. Configurer MariaDB

### 3.1 Accéder à phpMyAdmin

Je clique sur l’icône WAMP bar de tache à adroite → phpMyAdmin

L’URL s’ouvre automatiquement : http://localhost/phpmyadmin

Je me connecte avec l’utilisateur root (mot de passe vide par défaut).

### 3.2 Créer la base de données FreshRSS

Dans phpMyAdmin, je clique sur Nouvelle base de données.

Je nomme ma base : freshrss

Je choisis l’interclassement : utf8mb4_general_ci

Je clique sur Créer

### 3.3 Créer un utilisateur dédié

Je vais dans Comptes d’utilisateurs → Ajouter un compte utilisateur

Je remplis :

Nom d’utilisateur : freshrss

Hôte : localhost

Mot de passe : un mot de passe sécurisé

Je coche Donner tous les privilèges sur la base freshrss

Je clique sur Exécuter

⚠️ Astuce : Toujours créer un utilisateur dédié pour FreshRSS, plutôt que d’utiliser root. Cela sécurise la base.

### 4. Télécharger et préparer FreshRSS
4.1 Télécharger FreshRSS 
Je vais sur GitHub :https://github.com/FreshRSS/FreshRSS/releases/tag/1.27.1


Je télécharge la dernière version stable au format ZIP.

### 4.2 Extraire les fichiers

Je décompresse le ZIP.C:\wamp64\www\

Je renomme le dossier en FreshRSS.

## 5. Créer et configurer l’alias Apache pour FreshRSS via WampServer

### 5.1 — Donner les permissions Windows sur le dossier FreshRSS  
Avant de créer l’alias, je m’assure que le dossier de l’application FreshRSS est accessible en lecture/écriture par le serveur Apache.

- Je vais dans `C:\wamp64\www\FreshRSS\`  
- Clic droit sur le dossier → Propriétés → Onglet **Sécurité**  
- Je sélectionne un utilisateur ou j’ajoute **Everyone**  
- Je coche toutes les cases **Autoriser** (Lecture & exécution, Lecture, Écriture)  
- Je clique sur **Appliquer**, puis **OK**  
- Je m’assure que cela s’applique aux sous‑dossiers (p/, data/, config/)

### 5.2 — Créer l’alias via l’interface WampServer  
- Je clique sur l’icône WampServer dans la barre des tâches  
- Dans le menu, je vais à :  
Apache → Alias directories → Add an alias

- Une fenêtre s’ouvre :  
- **Alias name** : `freshrss`  
  (cela donne l’URL `http://localhost/freshrss/`)  
- **Directory path** : `C:/wamp64/www/FreshRSS/p/`  
  (c’est le chemin où j’ai placé l’application)  
- Je clique sur **OK** pour créer l’alias.

### 5.3 — Modifier le fichier d’alias pour l’accès réseau  
- WampServer crée automatiquement un fichier dans :  

C:\wamp64\alias\FreshRSS ou myalias_1

- J’ouvre ce fichier avec le Bloc‑notes  
- Je vérifie/modifie le contenu pour qu’il ressemble à :  

**(Alias /freshrss "C:/wamp64/www/FreshRSS/p/"
<Directory "C:/wamp64/www/FreshRSS/p/">
Options +Indexes +FollowSymLinks +MultiViews
AllowOverride All
Require all granted
</Directory>)**

- Je m’assure que la ligne `Require all granted` est présente (et non `Require local`)

### 5.4 — Redémarrer tous les services WampServer  
- Je clique sur l’icône WampServer → **Restart All Services**  
- Je vérifie que l’icône passe au **vert**

### 5.5 — Tester l’alias  
- Depuis le serveur : ouvrir `http://localhost/freshrss/`  
- Depuis une machine du réseau ou VM : ouvrir `http://IP_du_serveur/freshrss/`  
- Si la page s’affiche, l’alias fonctionne correctement  
- Astuce : créer un fichier `test.txt` dans `C:/wamp64/www/FreshRSS/p/` pour tester l’accès depuis une autre machine

---


Je sauvegarde et je redémarre tous les services WAMP.

⚠️ Astuce : La ligne Require all granted permet aux VM et autres machines du réseau d’accéder à FreshRSS. Sans ça, l’accès est limité au serveur local.

6. Lancer l’installation dans le navigateur

J’ouvre : http://localhost/freshrss/

L’assistant d’installation apparaît avec plusieurs étapes : langue, vérification système, configuration base de données, création admin.

## 7. Configurer FreshRSS
### Étape 1 : Langue
Je sélectionne Français

### Étape 2 : Vérifications système
Tous les modules doivent être en vert.
Si un module est rouge, je vais dans WAMP → PHP → PHP extensions et j’active :

curl
mbstring
openssl
pdo_mysql
Puis je redémarre WAMP.

### Étape 3 : Base de données
Champ	Ce que je remplis
Type de base	MySQL / MariaDB
Hôte	localhost
Utilisateur	freshrss
Mot de passe	mon mot de passe
Base de données	freshrss
Préfixe des tables	freshrss_

Je clique sur Test connection, puis Next si tout fonctionne.

Je clique sur Install pour finaliser.

8. Ajouter des flux RSS
Ajouter une catégorie

Dans FreshRSS → Add a category

Nom : Actualités → je clique sur Add

Ajouter un flux

Dans Add a feed :

URL du flux : https://rss.nytimes.com/services/xml/rss/nyt/HomePage.xml

Catégorie : Actualités

Je clique sur Add

⚠️ Astuce : Si le flux apparaît en rouge, je vérifie la connexion Internet et les extensions PHP curl et openssl.

9. Accès depuis les VM

Depuis la VM : http://IP_du_serveur/freshrss/

Si ça ne fonctionne pas :

Vérifier le pare-feu Windows

Vérifier le fichier d’alias (Require all granted)

Redémarrer WAMP

## 10. Problèmes fréquents
Problème	Cause probable	Solution
Page 404	Mauvais alias	Vérifier freshrss.conf
Page blanche	Extension PHP manquante	Activer mbstring, json, pdo_mysql
Flux rouge	URL invalide ou pas d’accès Internet	Vérifier la connexion et activer curl + openssl
VM ne peut pas accéder	Require local	Mettre Require all granted
WAMP ne démarre pas	Visual C++ manquant	Réinstaller tous les redistribuables Visual C++
11. Vérification finale

WAMP vert

Accès à http://localhost/freshrss/ OK
VM peuvent accéder via l’IP du serveur Ok 

Flux RSS affichés non pas encore 





## 13. Liens officiels 

Visual C++ Redistributables : https://wampserver.aviatechno.net/ -> télécharger pulusier version de Visual C++
Téléchargement WAMP : https://wampserver.aviatechno.net/ -> download-wampserver-64bits
Téléchargement FreshRSS : https://github.com/FreshRSS/FreshRSS/releases/tag/1.27.1


