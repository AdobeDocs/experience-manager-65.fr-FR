---
title: Configuration MySQL pour DSRP
seo-title: Configuration MySQL pour DSRP
description: Comment se connecter au serveur MySQL et établir la base de données UGC
seo-description: Comment se connecter au serveur MySQL et établir la base de données UGC
uuid: c058cc88-7ca2-4aed-9a36-b080e603f886
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: edc3043c-7ec4-4e4a-b008-95f1784f012e
translation-type: tm+mt
source-git-commit: 29f150215052d61c1e20d25b0c095ea6582e26f7
workflow-type: tm+mt
source-wordcount: '739'
ht-degree: 4%

---


# Configuration MySQL pour DSRP {#mysql-configuration-for-dsrp}

MySQL est une base de données relationnelle qui peut être utilisée pour stocker le contenu généré par l’utilisateur (UGC).

Ces instructions décrivent comment se connecter au serveur MySQL et établir la base de données UGC.

## Conditions requises {#requirements}

* [Pack de fonctionnalités des dernières communautés](deploy-communities.md#latestfeaturepack)
* [Pilote JDBC pour MySQL](deploy-communities.md#jdbc-driver-for-mysql)
* Une base de données relationnelle :

   * [MySQL Server](https://dev.mysql.com/downloads/mysql/) Community Server version 5.6 ou ultérieure

      * Peut s’exécuter sur le même hôte que AEM ou à distance
   * [Outils MySQL](https://dev.mysql.com/downloads/tools/workbench/)


## Installation de MySQL {#installing-mysql}

[MySQL](https://dev.mysql.com/downloads/mysql/) doit être téléchargé et installé selon les instructions du système d’exploitation de cible.

### Noms de table en minuscules {#lower-case-table-names}

SQL n&#39;étant pas sensible à la casse, pour les systèmes d&#39;exploitation sensibles à la casse, il est nécessaire d&#39;inclure un paramètre permettant d&#39;abaisser la casse de tous les noms de table.

Par exemple, pour spécifier tous les noms de table en minuscules sur un système d’exploitation Linux :

* Modifier le fichier `/etc/my.cnf`
* Dans la `[mysqld]` section, ajoutez la ligne suivante :

   `lower_case_table_names = 1`

### Jeu de caractères UTF8 {#utf-character-set}

Pour une meilleure prise en charge multilingue, il est nécessaire d&#39;utiliser le jeu de caractères UTF8.

Modifiez MySQL pour qu’UTF8 soit utilisé comme jeu de caractères :

* mysql > SET NAMES &#39;utf8&#39;;

Remplacez la base de données MySQL par défaut par UTF8 :

* Modifier le fichier `/etc/my.cnf`
* Dans la `[client]` section, ajoutez la ligne suivante :

   `default-character-set=utf8`

* Dans la `[mysqld]` section, ajoutez la ligne suivante :

   `character-set-server=utf8`

## Installation de MySQL Workbench {#installing-mysql-workbench}

MySQL Workbench fournit une interface utilisateur pour exécuter des scripts SQL qui installent le schéma et les données initiales.

MySQL Workbench doit être téléchargé et installé selon les instructions du système d’exploitation de cible.

## Connexion aux communautés {#communities-connection}

Lorsque MySQL Workbench est lancé pour la première fois, sauf s’il est déjà utilisé à d’autres fins, il n’affiche pas encore de connexions :

![chlimage_1-104](assets/chlimage_1-104.png)

### Nouveaux paramètres de connexion {#new-connection-settings}

1. Sélectionnez l’ `+` icône à droite de `MySQL Connections`.
1. Dans la boîte de dialogue `Setup New Connection`, saisissez les valeurs appropriées à votre plateforme.

   A des fins de démonstration, avec l’instance d’AEM d’auteur et MySQL sur le même serveur :

   * Nom de la connexion: `Communities`
   * Méthode de connexion : `Standard (TCP/IP)`
   * Nom d’hôte: `127.0.0.1`
   * Nom d’utilisateur: `root`
   * Mot de passe: `no password by default`
   * Schéma par défaut : `leave blank`

1. Sélectionnez `Test Connection` pour vérifier la connexion au service MySQL en cours d’exécution.

**Notes**:

* Le port par défaut est `3306`
* Le nom de connexion choisi est entré en tant que nom de source de données dans la configuration [JDBC OSGi.](#configurejdbcconnections)

#### Nouvelle connexion aux communautés {#new-communities-connection}

![chlimage_1-105](assets/chlimage_1-105.png)

## Configuration de la base de données {#database-setup}

Ouvrez la connexion Communities pour installer la base de données.

![chlimage_1-106](assets/chlimage_1-106.png)

### Obtention du script SQL {#obtain-the-sql-script}

Le script SQL est obtenu à partir du référentiel AEM :

1. Accéder au CRXDE Lite

   * For example, [http://localhost:4502/crx/de](http://localhost:4502/crx/de)

1. Sélectionnez le dossier /libs/social/config/datastore/dsrp/schéma.
1. Téléchargement `init-schema.sql`

   ![chlimage_1-107](assets/chlimage_1-107.png)

Une méthode de téléchargement du schéma consiste à

* Sélectionner le `jcr:content` noeud du fichier sql
* Notez que la valeur de la `jcr:data` propriété est un lien de vue.

* Sélectionnez le lien de la vue pour enregistrer les données dans un fichier local.

### Création de la base de données DSRP {#create-the-dsrp-database}

Suivez les étapes ci-dessous pour installer la base de données. Le nom par défaut de la base de données est `communities`.

Si le nom de la base de données est modifié dans le script, veillez à le modifier également dans la configuration [](#configurejdbcconnections)JDBC.

#### Étape 1 : ouvrir le fichier SQL {#step-open-sql-file}

Dans MySQL Workbench

* Dans le menu déroulant Fichier
* Sélectionnez le fichier téléchargé `init_schema.sql`

![chlimage_1-108](assets/chlimage_1-108.png)

#### Étape 2 : exécuter un script SQL {#step-execute-sql-script}

Dans la fenêtre Workbench du fichier ouvert à l’étape 1, sélectionnez le fichier `lightening (flash) icon` à exécuter.

Dans l’illustration suivante, le `init_schema.sql` fichier est prêt à être exécuté :

![chlimage_1-109](assets/chlimage_1-109.png)

#### Actualiser {#refresh}

Une fois le script exécuté, il est nécessaire d’actualiser la `SCHEMAS` section de la `Navigator` pour afficher la nouvelle base de données. Utilisez l’icône Actualiser à droite de &quot;SCHÉMAS&quot; :

![chlimage_1-110](assets/chlimage_1-110.png)

## Configuration de la connexion JDBC {#configure-jdbc-connection}

La configuration OSGi pour le pool **de connexions JDBC** Day Commons permet de configurer le pilote JDBC MySQL.

Toutes les instances d’AEM de publication et d’auteur doivent pointer vers le même serveur MySQL.

Lorsque MySQL s’exécute sur un serveur différent de AEM, le nom d’hôte du serveur doit être spécifié à la place de &quot;localhost&quot; dans le connecteur JDBC.

* Sur chaque instance d’AEM d’auteur et de publication.
* Connecté avec des droits d’administrateur.
* Access the [web console](../../help/sites-deploying/configuring-osgi.md).

   * For example, [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)

* Localisez la variable `Day Commons JDBC Connections Pool`
* Sélectionnez l&#39; `+` icône pour créer une nouvelle configuration de connexion.

   ![chlimage_1-111](assets/chlimage_1-111.png)

* Saisissez les valeurs suivantes :

   * **[!UICONTROL Classe]** de pilote JDBC : `com.mysql.jdbc.Driver`
   * **[!UICONTROL URI de connexion JDBC]**: `jdbc:mysql://localhost:3306/communities?characterEncoding=UTF-8`

      Spécifiez le serveur à la place de localhost si le serveur MySQL n’est pas identique à &quot;this&quot; AEM *communautés* de serveurs est le nom de base de données (schéma) par défaut.

   * **[!UICONTROL Nom d&#39;utilisateur]**: `root`

      Ou saisissez le nom d’utilisateur configuré pour le serveur MySQL, si ce n’est &quot;root&quot;.

   * **[!UICONTROL Mot de passe]**:

      Effacez ce champ si aucun mot de passe n’est défini pour MySQL,

      sinon, saisissez le mot de passe configuré pour le nom d’utilisateur MySQL.

   * **[!UICONTROL Nom]** de la source de données : nom saisi pour la connexion [](#new-connection-settings)MySQL, par exemple &quot;communautés&quot;.

* Sélectionnez **[!UICONTROL Enregistrer]**

