---
title: Configuration MySQL pour les fonctionnalités d’activation
seo-title: Configuration MySQL pour les fonctionnalités d’activation
description: Connexion de votre serveur MySQL
seo-description: Connexion de votre serveur MySQL
uuid: e02d9404-de75-4fdb-896c-ea3f64f980a3
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 9222bc93-c231-4ac8-aa28-30d784a4ca3b
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '1093'
ht-degree: 4%

---


# Configuration MySQL pour les fonctionnalités d’activation {#mysql-configuration-for-enablement-features}

MySQL est une base de données relationnelle principalement utilisée pour le suivi SCORM et les données de rapports pour les ressources d’activation. Il contient des tableaux pour d’autres fonctionnalités telles que le suivi de la mise en pause/reprise de la vidéo.

Ces instructions décrivent comment se connecter au serveur MySQL, établir la base de données d’activation et renseigner la base de données avec les données initiales.

## Conditions requises {#requirements}

Avant de configurer la fonction d’activation de MySQL pour les communautés, veillez à

* Installez [MySQL Server](https://dev.mysql.com/downloads/mysql/) Community Server version 5.6 :
   * La version 5.7 n’est pas prise en charge pour SCORM.
   * Peut être le même serveur que l’instance d’AEM d’auteur.
* Sur toutes les instances AEM, installez le pilote [JDBC officiel pour MySQL](deploy-communities.md#jdbc-driver-for-mysql).
* Installez [MySQL Workbench](https://dev.mysql.com/downloads/tools/workbench/).
* Sur toutes les instances AEM, installez le package [](enablement.md#scorm)SCORM.

## Installation de MySQL {#installing-mysql}

MySQL doit être téléchargé et installé selon les instructions du système d’exploitation de cible.

### Noms de table en minuscules {#lower-case-table-names}

SQL n&#39;étant pas sensible à la casse, pour les systèmes d&#39;exploitation sensibles à la casse, il est nécessaire d&#39;inclure un paramètre permettant d&#39;abaisser la casse de tous les noms de table.

Par exemple, pour spécifier tous les noms de table en minuscules sur un système d’exploitation Linux :

* Modifier le fichier `/etc/my.cnf`
* Dans la `[mysqld]` section, ajoutez la ligne suivante : `lower_case_table_names = 1`

### Jeu de caractères UTF8 {#utf-character-set}

Pour une meilleure prise en charge multilingue, il est nécessaire d&#39;utiliser le jeu de caractères UTF8.

Modifiez MySQL pour qu’UTF8 soit utilisé comme jeu de caractères :
* mysql > SET NAMES &#39;utf8&#39;;

Remplacez la base de données MySQL par défaut par UTF8 :
* Modifier le fichier `/etc/my.cnf`
* Dans la `[client]` section, ajoutez : `default-character-set=utf8`
* Dans la `[mysqld]` section, ajoutez : `character-set-server=utf8`

## Installation de MySQL Workbench {#installing-mysql-workbench}

MySQL Workbench fournit une interface utilisateur pour exécuter des scripts SQL qui installent le schéma et les données initiales.

MySQL Workbench doit être téléchargé et installé selon les instructions du système d’exploitation de cible.

## Connexion d&#39;activation {#enablement-connection}

Lorsque MySQL Workbench est lancé pour la première fois, sauf s’il est déjà utilisé à d’autres fins, il n’affiche pas encore de connexions :

![mysqlconnection](assets/mysqlconnection.png)

### Nouveaux paramètres de connexion {#new-connection-settings}

1. Sélectionnez l&#39;icône &quot;+&quot; à droite de `MySQL Connections`.
1. Dans la boîte de dialogue `Setup New Connection`, saisissez les valeurs appropriées pour votre plateforme à des fins de démonstration, avec l’instance d’AEM auteur et MySQL sur le même serveur :
   * Nom de la connexion: `Enablement`
   * Méthode de connexion : `Standard (TCP/IP)`
   * Nom d’hôte: `127.0.0.1`
   * Nom d’utilisateur: `root`
   * Mot de passe: `no password by default`
   * Schéma par défaut : `leave blank`
1. Sélectionnez `Test Connection` pour vérifier la connexion au service MySQL en cours d’exécution.

**Notes**:
* Le port par défaut est `3306`.
* Le nom `Connection Name` choisi est entré en tant que `datasource` nom dans la configuration [](#configure-jdbc-connections)JDBC OSGi.

#### Connexion réussie {#successful-connection}

![mysqlconnection1](assets/mysqlconnection1.png)

#### Nouvelle connexion d&#39;activation {#new-enablement-connection}

![mysqlconnection2](assets/mysqlconnection2.png)

## Configuration de la base de données {#database-setup}

Lors de l’ouverture de la nouvelle connexion d’activation, vous constatez qu’il existe un schéma de test et des comptes d’utilisateurs par défaut.

![configuration de base de données](assets/database-setup.png)

### Obtention des scripts SQL {#obtain-sql-scripts}

Les scripts SQL sont obtenus à l’aide du CRXDE Lite sur l’instance d’auteur. Le package [](deploy-communities.md#scorm) SCORM doit être installé :

1. Accédez au CRXDE Lite :
   * For example, [http://localhost:4502/crx/de](http://localhost:4502/crx/de)
1. Développez le `/libs/social/config/scorm/` dossier
1. Téléchargement `database_scormengine.sql`
1. Téléchargement `database_scorm_integration.sql`

![sqlscripts](assets/sqlscripts.png)

Une méthode de téléchargement du schéma consiste à :

* Sélectionnez le `jcr:content` noeud du fichier sql.
* Notez que la valeur de la `jcr:data` propriété est un lien de vue.
* Sélectionnez le lien de la vue pour enregistrer les données dans un fichier local.

### Créer une base de données SCORM {#create-scorm-database}

La base de données SCORM d&#39;activation à créer est la suivante :

* name: `ScormEngineDB`
* créé à partir de scripts :
   * schéma: `database_scormengine.sql`
   * data: `database_scorm_integration.sql`
Suivez les étapes ci-dessous (
[open](#step-open-sql-file), [execute](#step-execute-sql-script)) pour installer chaque script [](#obtain-sql-scripts) SQL. [Actualisez](#refresh) si nécessaire pour voir les résultats de l’exécution du script.

Veillez à installer le schéma avant d’installer les données.

>[!CAUTION]
>
>Si le nom de la base de données est modifié, veillez à le spécifier correctement dans :
>
>* [Configuration JDBC](#configure-jdbc-connections)
>* [Configuration SCORM](#configure-scorm)


#### Étape 1 : ouvrir le fichier SQL {#step-open-sql-file}

Dans MySQL Workbench

* Dans le menu déroulant Fichier
* Sélectionner `Open SQL Script ...`
* Dans cet ordre, sélectionnez l&#39;une des options suivantes :
   1. `database_scormengine.sql`
   1. `database_scorm_integration.sql`

![scrom-database](assets/scrom-database.png)

#### Étape 2 : exécuter un script SQL {#step-execute-sql-script}

Dans la fenêtre Workbench du fichier ouvert à l’étape 1, sélectionnez le fichier `lightening (flash) icon` à exécuter.

Notez que l’exécution du `database_scormengine.sql` script destiné à créer la base de données SCORM peut prendre une minute.

![scrom-database1](assets/scrom-database1.png)

#### Actualiser {#refresh}

Une fois les scripts exécutés, il est nécessaire d’actualiser la `SCHEMAS` section de la `Navigator` pour afficher la nouvelle base de données. Utilisez l’icône Actualiser à droite de &quot;SCHÉMAS&quot; :

![scrom-database2](assets/scrom-database2.png)

#### Résultat : scormenginedb {#result-scormenginedb}

Une fois les SCHÉMAS installés et actualisés, ils `scormenginedb` seront visibles.

![scrom-database3](assets/scrom-database3.png)

## Configuration des connexions JDBC {#configure-jdbc-connections}

La configuration OSGi pour le pool **de connexions JDBC** Day Commons permet de configurer le pilote JDBC MySQL.

Toutes les instances d’AEM de publication et d’auteur doivent pointer vers le même serveur MySQL.

Lorsque MySQL s’exécute sur un serveur différent de AEM, le nom d’hôte du serveur doit être spécifié à la place de &quot;localhost&quot; dans le connecteur JDBC (qui renseigne la configuration de [ScormEngine](#configurescormengineservice) ).

* Sur chaque instance d’AEM d’auteur et de publication
* Connecté avec des droits d’administrateur
* Access the [web console](../../help/sites-deploying/configuring-osgi.md)
   * For example, [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)
* Localisez la variable `Day Commons JDBC Connections Pool`
* Sélectionnez l&#39; `+` icône permettant de créer une configuration

   ![jdbcconnection1](assets/jdbcconnection1.png)

* Saisissez les valeurs suivantes :
   * **[!UICONTROL Classe]** de pilote JDBC : `com.mysql.jdbc.Driver`
   * **URIJ** de connexion DBC : `jdbc:mysql://localhost:3306/aem63reporting` spécifiez le serveur à la place de localhost si le serveur MySQL n’est pas identique au serveur AEM &quot;this&quot;.
   * **[!UICONTROL Nom d&#39;utilisateur]**: Racine ou saisissez le nom d’utilisateur configuré pour le serveur MySQL, si ce n’est &quot;root&quot;.
   * **[!UICONTROL Mot de passe]**: Effacez ce champ si aucun mot de passe n’est défini pour MySQL, sinon saisissez le mot de passe configuré pour le nom d’utilisateur MySQL.
   * **[!UICONTROL Nom]** de la source de données : Nom saisi pour la connexion [](#new-connection-settings)MySQL, par exemple &quot;activation&quot;.
* Sélectionnez **[!UICONTROL Enregistrer]**.

## Configurer Scorm {#configure-scorm}

### Service AEM Communities ScormEngine {#aem-communities-scormengine-service}

La configuration OSGi pour le service **ScormEngine** AEM Communities configure SCORM pour l’utilisation du serveur MySQL par une communauté d’activation.

Cette configuration est présente lorsque le package [](deploy-communities.md#scorm-package) SCORM est installé.

Toutes les instances de publication et d’auteur pointent vers le même serveur MySQL.

Lorsque MySQL s’exécute sur un serveur différent de AEM, le nom d’hôte du serveur doit être spécifié à la place de &quot;localhost&quot; dans le service ScormEngine, qui est généralement renseigné à partir de la configuration de connexion [](#configure-jdbc-connections) JDBC.

* Sur chaque instance d’AEM d’auteur et de publication
* Connecté avec des droits d’administrateur
* Access the [web console](../../help/sites-deploying/configuring-osgi.md)
   * For example, [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)
* Localisez la variable `AEM Communities ScormEngine Service`
* Sélectionner l’icône de modification

   ![chlimage_1-337](assets/chlimage_1-337.png)

* Vérifiez que les valeurs de paramètre suivantes sont cohérentes avec la configuration de la connexion [](#configurejdbcconnectionspool) JDBC :
   * **[!UICONTROL URI]** de connexion JDBC : `jdbc:mysql://localhost:3306/ScormEngineDB` *ScormEngineDB* est le nom de base de données par défaut dans les scripts SQL.
   * **[!UICONTROL Nom d&#39;utilisateur]**: Racine ou saisissez le nom d’utilisateur configuré pour le serveur MySQL, si ce n’est &quot;root&quot;
   * **[!UICONTROL Mot de passe]**: Effacez ce champ si aucun mot de passe n’est défini pour MySQL, sinon saisissez le mot de passe configuré pour le nom d’utilisateur MySQL.
* Concernant le paramètre suivant :
   * **[!UICONTROL Scorm User Password]**: NE PAS MODIFIER

      Pour un usage interne uniquement : Il est destiné à un utilisateur de service spécial utilisé par AEM Communities pour communiquer avec le moteur de score.
* Sélectionnez **[!UICONTROL Enregistrer]**

### Filtre CSRF Granit Adobe {#adobe-granite-csrf-filter}

Pour que les cours d’activation fonctionnent correctement dans tous les navigateurs, il est nécessaire d’ajouter Mozilla en tant qu’agent utilisateur qui n’est pas contrôlé par le filtre CSRF.

* Connectez-vous à l’instance de publication AEM avec les droits d’administrateur.
* Access the [web console](../../help/sites-deploying/configuring-osgi.md)
   * For example, [http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr)
* Localisez `Adobe Granite CSRF Filter`.
* Sélectionnez l’icône Modifier.

   ![jdbcconnection2](assets/jdbcconnection2.png)

* Sélectionnez l’ `[+]` icône permettant d’ajouter un agent utilisateur sécurisé.
* Enter `Mozilla/*`.
* Sélectionnez **[!UICONTROL Enregistrer]**.

