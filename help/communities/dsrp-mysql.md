---
title: Configuration MySQL pour DSRP
seo-title: MySQL Configuration for DSRP
description: Comment se connecter au serveur MySQL et établir la base de données UGC
seo-description: How to connect to the MySQL server and establish the UGC database
uuid: c058cc88-7ca2-4aed-9a36-b080e603f886
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: edc3043c-7ec4-4e4a-b008-95f1784f012e
role: Admin
exl-id: eafb60be-2963-4ac9-8618-50fd9bc6fe6c
source-git-commit: 1807919078996b1cf1cbd1f2d90c3b14cb660e2c
workflow-type: tm+mt
source-wordcount: '726'
ht-degree: 3%

---

# Configuration MySQL pour DSRP {#mysql-configuration-for-dsrp}

MySQL est une base de données relationnelle qui peut être utilisée pour stocker le contenu généré par l’utilisateur.

Ces instructions décrivent comment se connecter au serveur MySQL et établir la base de données UGC.

## Conditions requises {#requirements}

* [Pack de fonctionnalités des dernières communautés](deploy-communities.md#latestfeaturepack)
* [Pilote JDBC pour MySQL](deploy-communities.md#jdbc-driver-for-mysql)
* Une base de données relationnelle :

   * [Serveur MySQL](https://dev.mysql.com/downloads/mysql/) Community Server version 5.6 ou ultérieure

      * Peut s’exécuter sur le même hôte que AEM ou à distance

   * [Workbench MySQL ](https://dev.mysql.com/downloads/tools/workbench/)

## Installation de MySQL {#installing-mysql}

[MySQL](https://dev.mysql.com/downloads/mysql/) doit être téléchargé et installé selon les instructions du système d’exploitation cible.

### Noms de table en minuscules {#lower-case-table-names}

Comme SQL n’est pas sensible à la casse, pour les systèmes d’exploitation sensibles à la casse, il est nécessaire d’inclure un paramètre permettant de réduire la casse de tous les noms de table.

Par exemple, pour spécifier tous les noms de table en minuscules sur un système d’exploitation Linux :

* Modifier le fichier `/etc/my.cnf`
* Dans le `[mysqld]` , ajoutez la ligne suivante :

  `lower_case_table_names = 1`

### Jeu de caractères UTF8 {#utf-character-set}

Pour offrir une meilleure prise en charge multilingue, il est nécessaire d&#39;utiliser le jeu de caractères UTF8.

Modifiez MySQL pour que UTF8 soit son jeu de caractères :

* mysql > SET NAMES &#39;utf8&#39;;

Remplacez la base de données MySQL par défaut par UTF8 :

* Modifier le fichier `/etc/my.cnf`
* Dans le `[client]` , ajoutez la ligne suivante :

  `default-character-set=utf8`

* Dans le `[mysqld]` , ajoutez la ligne suivante :

  `character-set-server=utf8`

## Installation de MySQL Workbench {#installing-mysql-workbench}

MySQL Workbench fournit une interface utilisateur pour exécuter des scripts SQL qui installent le schéma et les données initiales.

MySQL Workbench doit être téléchargé et installé selon les instructions du système d’exploitation cible.

## Connexion aux communautés {#communities-connection}

Lorsque MySQL Workbench est lancé pour la première fois, sauf s’il est déjà utilisé à d’autres fins, il n’affiche pas encore de connexions :

![mysqlconnection](assets/mysqlconnection.png)

### Nouveaux paramètres de connexion {#new-connection-settings}

1. Sélectionnez la variable `+` à droite de `MySQL Connections`.
1. Dans la boîte de dialogue `Setup New Connection`, saisissez les valeurs appropriées à votre plateforme.

   À des fins de démonstration, avec l’instance d’AEM de création et MySQL sur le même serveur :

   * Connection Name : `Communities`
   * Méthode de connexion : `Standard (TCP/IP)`
   * Nom d’hôte : `127.0.0.1`
   * Nom d’utilisateur : `root`.
   * Mot de passe : `no password by default`.
   * Schéma par défaut : `leave blank`

1. Sélectionner `Test Connection` pour vérifier la connexion au service MySQL en cours d’exécution

**Remarques**:

* Le port par défaut est `3306`
* Le nom de connexion choisi est saisi en tant que nom de la source de données dans [Configuration OSGi JDBC](#configurejdbcconnections)

#### Nouvelle connexion aux communautés {#new-communities-connection}

![connection-communauté](assets/community-connection.png)

## Configuration de la base de données {#database-setup}

Ouvrez la connexion Communities pour installer la base de données.

![install-database](assets/install-database.png)

### Obtention du script SQL {#obtain-the-sql-script}

Le script SQL est obtenu à partir du référentiel AEM :

1. Accéder à CRXDE Lite

   * Par exemple : [http://localhost:4502/crx/de](http://localhost:4502/crx/de)

1. Sélectionnez le dossier /libs/social/config/datastore/dsrp/schema .
1. Télécharger `init-schema.sql`

   ![database-schema-crxde](assets/database-schema-crxde.png)

Une méthode de téléchargement du schéma consiste à :

* Sélectionnez la variable `jcr:content` noeud du fichier sql
* Notez la valeur de la variable `jcr:data` est un lien d’affichage

* Sélectionnez le lien d&#39;affichage pour enregistrer les données dans un fichier local.

### Création de la base de données DSRP {#create-the-dsrp-database}

Pour installer la base de données, procédez comme suit. Le nom par défaut de la base de données est `communities`.

Si le nom de la base de données est modifié dans le script, veillez également à le modifier dans la variable [Configuration JDBC](#configurejdbcconnections).

#### Étape 1 : ouverture du fichier SQL {#step-open-sql-file}

Dans MySQL Workbench

* Dans le menu déroulant Fichier , sélectionnez la variable **[!UICONTROL Open SQL Script]** option
* Sélectionner le téléchargé `init_schema.sql` script

![select-sql-script](assets/select-sql-script.png)

#### Étape 2 : exécution du script SQL {#step-execute-sql-script}

Dans la fenêtre Workbench du fichier ouvert à l’étape 1, sélectionnez l’option `lightening (flash) icon` pour exécuter le script.

Dans l’image suivante, la variable `init_schema.sql` est prêt à être exécuté :

![execute-sql-script](assets/execute-sql-script.png)

#### Actualiser {#refresh}

Une fois le script exécuté, il est nécessaire d&#39;actualiser la variable `SCHEMAS` de la `Navigator` pour voir la nouvelle base de données. Utilisez l’icône d’actualisation à droite de &quot;SCHEMAS&quot; :

![refresh-schema](assets/refresh-schema.png)

## Configuration de la connexion JDBC {#configure-jdbc-connection}

Configuration OSGi pour **Pool de connexions JDBC Day Commons** configure le pilote JDBC MySQL.

Toutes les instances d’AEM de publication et de création doivent pointer vers le même serveur MySQL.

Lorsque MySQL s’exécute sur un serveur différent de l’AEM, le nom d’hôte du serveur doit être spécifié à la place de &quot;localhost&quot; dans le connecteur JDBC.

* Sur chaque instance d’AEM de création et de publication.
* Connecté avec les privilèges d’administrateur.
* Accédez au [console web](../../help/sites-deploying/configuring-osgi.md).

   * Par exemple : [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)

* Recherchez la variable `Day Commons JDBC Connections Pool`
* Sélectionnez la variable `+` pour créer une configuration de connexion.

  ![configure-jdbc-connection](assets/configure-jdbc-connection.png)

* Saisissez les valeurs suivantes :

   * **[!UICONTROL Classe de pilote JDBC]**: `com.mysql.jdbc.Driver`
   * **[!UICONTROL URI de connexion JDBC]**: `jdbc:mysql://localhost:3306/communities?characterEncoding=UTF-8`

     Spécifiez le serveur à la place de localhost si le serveur MySQL n’est pas identique à &quot;this&quot; AEM serveur *communities* est le nom par défaut de la base (schéma).

   * **[!UICONTROL Nom d’utilisateur]**: `root`

     Ou saisissez le nom d’utilisateur configuré pour le serveur MySQL, si ce n’est &quot;root&quot;.

   * **[!UICONTROL Password]**:

     Effacez ce champ si aucun mot de passe n’est défini pour MySQL,

     sinon, saisissez le mot de passe configuré pour le nom d’utilisateur MySQL.

   * **[!UICONTROL Nom de la source de données]**: nom saisi pour la variable [Connexion MySQL](#new-connection-settings), par exemple, &quot;communautés&quot;.

* Sélectionnez **[!UICONTROL Enregistrer]**.
