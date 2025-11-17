
# GUIDE UTILISATEUR Projet 1 : Service d’Agrégation de Flux RSS

## Sommaire

1. [Connexion et utilisation de base](#1-connexion-et-utilisation-de-base)
2. [Utilisation avancée (règles, filtres, étiquettes)](#2-utilisation-avancée-règles-filtres-étiquettes)
3. [FAQ Problèmes fréquents](#3-faq-problèmes-fréquents)
4. [Astuces et bonnes pratiques](#4-astuces-et-bonnes-pratiques)

# 1. Connexion et utilisation de base  
## Se connecter à FreshRSS
###  Adresse d’accès :
http://172.16.10.5/freshrss/
###  Étapes 1:
1.1 Ouvrir un navigateur web (Edge, Firefox ou Chrome).  
1.2 Entrer l’adresse du serveur FreshRSS ci-dessus.  
1.3 L’écran d’accueil de FreshRSS s’affiche.  
![page_conect_freshrss](https://github.com/WildCodeSchool/TSSR-1025-P1-G4/blob/main/Ressources/autres/page_conect_freshrss.png)
1.4 Saisir vos identifiants :
   - **Nom d’utilisateur :** admin  
   - **Mot de passe :** (fourni par l’administrateur)
1.5 Cliquer sur **Connexion**.  
### Interface principale :
Une fois connecté, vous accédez :
- à la liste des flux RSS dans la colonne de gauche,  
- au nombre d’articles non lus,  
- et à la zone de lecture à droite.    
![page_conect_freshrss_flux](https://github.com/WildCodeSchool/TSSR-1025-P1-G4/blob/main/Ressources/autres/page_freshrss.png)
  
## Se connecter à Tiny Tiny RSS  
###  Adresse d’accès :  
http://172.16.10.6 
###  Étapes 1:
1.1 Aller dans navigateur (sur poste client)
1.2 Ouvrir un navigateur web (Edge, Firefox ou Chrome).
1.3 la page d’authentification apparaît
1.4 Entrer l’adresse du serveur Tiny Tiny RSS ci-dessus.  
1.5 L’écran d’accueil de FreshRSS s’affiche.  
  ! [page_connect_ttrss(https://github.com/WildCodeSchool/TSSR-1025-P1-G4/blob/main/Ressources/autres/configuration%20page%20ttrss.jpg)
1.6 Saisir vos identifiants :  
   - **Nom d’utilisateur :** admin    
   - **Mot de passe :** (fourni par l’administrateur)
### Interface principale :
Une fois connecté, vous accédez :
- à la liste des flux RSS dans la colonne de gauche, 
- au nombre d’articles non lus,  
- et à la zone de lecture à droite.

----

## Ajouter le flux FreshRSS sur FluentReader et NewsFlash
Sur Les poste clients **Windows (Fluent Reader)** et **Ubuntu (NewsFlash)** permettent de consulter les flux à distance via l’API Google Reader.

### Sous Windows Fluent Reader

###  Étapes 1:
1.1 Ouvrez **Fluent Reader** depuis le menu Démarrer.  
1.2 Allez dans **Settings → Accounts → Add Account**.  
1.3 Choisissez **Google Reader API**.  
![6_api_parametrage](https://github.com/WildCodeSchool/TSSR-1025-P1-G4/blob/main/Ressources/installation_fluentreader/6_api_parametrage.png)
 
1.4 Remplissez les champs :
   - **Nom d’affichage :** Serveur FreshRSS  
   - **URL du serveur :** `http://172.16.10.5/freshrss/api/greader.php`  
   - **Nom d’utilisateur :** admin  
   - **Mot de passe :** (mot de passe FreshRSS)

![7_api_connectes](https://github.com/WildCodeSchool/TSSR-1025-P1-G4/blob/main/Ressources/installation_fluentreader/7_api_connectes.png)
1.5 Cliquez sur **Connect**.  
1.6 Vos flux apparaissent automatiquement dans la colonne de gauche.  


---

### Sous Ubuntu NewsFlash
###  Étapes 1:
1.1 Lancez **NewsFlash** depuis le menu Applications.  
1.2 Sur la page d’accueil, cliquez sur **Add Account**.  
1.3 Sélectionnez **FreshRSS**.    
 ![4_newsflash_servicerss](https://github.com/WildCodeSchool/TSSR-1025-P1-G4/blob/main/Ressources/installation_newsflash/4_newsflash_servicerss.png)
   
1.4 Renseignez :
   - **Nom d’affichage :** Serveur FreshRSS  
   - **URL du serveur :** `http://172.16.10.5/freshrss/api/greader.php`  
   - **Nom d’utilisateur :** admin  
   - **Mot de passe :** (mot de passe FreshRSS)

 ![6_parametre_connection](https://github.com/WildCodeSchool/TSSR-1025-P1-G4/blob/main/Ressources/installation_newsflash/6_parametre_connection.png)
1.5 Cliquez sur **Connect**.  
1.6 Les flux se synchronisent automatiquement.  


# 2. Utilisation avancée (règles, filtres, étiquettes)
###  Étapes 1:
1.1 Depuis FreshRSS, ouvrez le menu **Catégories**.  
1.2 Cliquez sur **+ Ajouter une catégorie**.  
1.3 Entrez un nom (ex. *Veille Tech*, *Cybersécurité*).  
1.4 Glissez les flux souhaités dans la catégorie correspondante.  


Les catégories sont synchronisées automatiquement avec vos clients.

-----

# 3. FAQ Problèmes fréquents

| Problème                                    | Cause probable                     | Solution                                                 |
| ------------------------------------------- | ---------------------------------- | -------------------------------------------------------- |
| Erreur cURL 60 lors de l’ajout de flux      | Certificats SSL manquants          | Télécharger `cacert.pem` et le déclarer dans `php.ini`   |
| Impossible de se connecter au flux de FreshRSS | API Google Reader désactivée       | Activer l’API dans les paramètres FreshRSS               |
| Connection refused sur Fluent Reader      | Carte réseau désactivée sur la VM  | Réactiver la connexion dans les paramètres réseau Ubuntu |                  |
| Erreur PDO sur Debian                       | Modules PHP manquants              | Installer `php-xml`, `php-intl`, `php-curl`              |

# 4. Astuces et bonnes pratiques
- Créez des catégories claires pour vos flux (Tech, Cyber, Réseaux…).
- Testez chaque flux dans un navigateur avant de l’ajouter.

