## Sommaire

1. [Prérequis technique](#prerequis-technique)
2. [Installation sur le serveur](#installation-sur-le-serveur)
3. [Installation sur le client](#installation-sur-le-client)
4. [FAQ](#faq)

# 1. Prérequis techniques
<span id="prerequis-techniques"></span>

# 2. Installation sur le serveur
<span id="installation-sur-le-serveur"></span>

# 3. Installation sur le client
<span id="installation-sur-le-client"></span>
## Installation et gestion de Fluent Reader sur Ubuntu

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

# 4. FAQ
<span id="faq"></span> 