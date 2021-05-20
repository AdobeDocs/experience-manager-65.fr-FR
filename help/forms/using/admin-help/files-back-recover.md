---
title: Fichiers à sauvegarder et à récupérer
seo-title: Fichiers à sauvegarder et à récupérer
description: Ce document décrit les fichiers d’application et de données à sauvegarder.
seo-description: Ce document décrit les fichiers d’application et de données à sauvegarder.
uuid: ba04adb9-675a-48f2-ad52-39c1266e423b
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 6f9a294d-24bd-4e4b-b929-2809f5e6cef9
exl-id: d2dd381d-a7d2-4fec-a8ba-7ca037fd9dc1
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2187'
ht-degree: 89%

---

# Fichiers à sauvegarder et à récupérer {#files-to-back-up-and-recover}

Les fichiers d’application et de données à sauvegarder sont décrits en détail dans les sections suivantes.

Considérez les points suivants concernant la sauvegarde et la récupération :

* La base de données doit être sauvegardée avant le stockage global de document et le référentiel AEM.
* Si vous devez mettre les noeuds en grappe dans un environnement organisé en grappe pour la sauvegarde, assurez-vous que les noeuds secondaires sont fermés avant le noeud Principal. Dans le cas contraire, une incohérence peut survenir dans la grappe ou le serveur. En outre, le noeud Principal doit être rendu actif avant tout noeud secondaire.
* Pour l’opération de restauration d’une grappe, le serveur d’applications doit être arrêté pour chaque nœud de la grappe.

## Répertoire de stockage global de documents {#global-document-storage-directory}

Le répertoire de stockage global de documents est utilisé pour stocker les fichiers de longue durée utilisés dans un processus. La durée de vie de ces fichiers est destinée à couvrir un ou plusieurs lancements d’un système AEM Forms et peut être de plusieurs jours, voire de plusieurs années. Les fichiers de longue durée peuvent être des PDF, des stratégies ou des modèles de formulaires. Les fichiers de longue durée jouent un rôle capital la plupart des déploiements d’AEM. Si certains d’entre eux sont perdus ou corrompus, le serveur Forms peut devenir instable.

Les documents d’entrée pour un appel de travaux asynchrones sont également stockés dans le répertoire de stockage global de documents et doivent être disponibles pour traiter les demandes. Il est donc important que vous preniez en compte la fiabilité du système de fichiers hébergeant le répertoire de stockage global de documents et que vous utilisiez une technologie RAID (Redundant Array of Independent Disks) ou toute autre technologie appropriée pour répondre à vos besoins en termes de niveau de qualité et de service.

L’emplacement du répertoire de stockage global de documents est défini lors de l’installation d’AEM forms, ou ultérieurement à l’aide d’Administration Console. Outre la possibilité de conserver le répertoire de stockage global de documents à un emplacement de haute disponibilité, vous pouvez également activer le stockage de base de données pour les documents. Voir [Options de sauvegarde dans le cas de l’utilisation de la base de données pour le stockage de documents](files-back-recover.md#backup-options-when-database-is-used-for-document-storage).

### Emplacement du répertoire de stockage global de documents  {#gds-location}

Si vous ne définissez pas le paramètre d’emplacement lors de l’installation, l’emplacement par défaut utilisé est un sous-répertoire de l’emplacement d’installation du serveur d’applications. Vous devez sauvegarder le répertoire suivant de votre serveur d’applications :

* (JBoss) `[appserver root]/server/'server'/svcnative/DocumentStorage`
* (WebLo gic) `[appserverdomain]/'server'/adobe/AEMformsserver/DocumentStorage`
* (WebSphere) `[appserver root]/installedApps/adobe/'server'/DocumentStorage`

Si vous avez installé le répertoire de stockage global de documents à un emplacement autre que celui par défaut, vous pouvez le définir comme suit :

* Connectez-vous à Administration Console et cliquez sur Paramètres > Paramètres de Core System > Configurations.
* Notez l’emplacement indiqué dans la zone Répertoire de stockage global de documents.

Dans un environnement organisé en grappe, le répertoire de stockage global de documents correspond généralement à un répertoire partagé sur le réseau et est accessible en lecture/écriture sur chaque nœud de la grappe.

L’emplacement du répertoire de stockage global de documents peut être modifié lors d’une récupération, si l’emplacement d’origine n’est plus disponible (voir [Modification de l’emplacement du stockage global de documents durant la récupération](/help/forms/using/admin-help/recovering-aem-forms-data.md#changing-the-gds-location-during-recovery)).

### Options de sauvegarde dans le cas de l’utilisation de la base de données pour le stockage de documents  {#backup-options-when-database-is-used-for-document-storage}

Vous pouvez activer le stockage de documents AEM Forms dans la base de données AEM Forms à l’aide d’Administration Console. Cette option conserve tous les documents persistants dans la base de données ; AEM Forms a tout de même besoin du répertoire de stockage global de documents reposant sur le système de fichiers car il est utilisé pour le stockage des fichiers et ressources permanents et temporaires associés aux sessions et aux appels d’AEM Forms.

Lorsque vous sélectionnez l’option « Activer le stockage de documents dans la base de données » dans les paramètres de Core System dans Administration Console ou à l’aide du gestionnaire de configuration, AEM Forms n’autorise pas les modes de sauvegarde d’instantané et de sauvegarde de restauration. Par conséquent, vous n’avez pas besoin de gérer les modes de sauvegarde à l’aide d’AEM Forms. Si vous utilisez cette option, sauvegardez le répertoire de stockage global de documents uniquement après avoir activé cette option. Lors de la récupération d’AEM Forms à partir d’une sauvegarde, il n’est pas nécessaire de renommer le répertoire de sauvegarde du stockage global de documents ni de restaurer ce dernier.

## Référentiel AEM  {#aem-repository}

Le référentiel AEM (crx-repository) est créé si crx-repository est configuré lors de l’installation d’AEM Forms. Le processus d’installation d’AEM Forms détermine l’emplacement du répertoire crx-repository. Le référentiel de sauvegarde et de restauration AEM est requis, de même que la base de données et le stockage global de documents pour des données AEM Forms cohérentes dans AEM Forms. Le référentiel AEM contient des données pour la solution Correspondence Management, Forms Manager et l’espace de travail AEM Forms.

### Solution Correspondence Management {#correspondence-management-solution}

La solution Correspondence Management centralise et gère la création, l’assemblage et la livraison de correspondances sécurisées, personnalisées et interactives. Elle permet de générer rapidement une correspondance à partir de contenus prévalidés et personnalisés dans le cadre d’un processus simplifié allant de la création à l’archivage. Par conséquent, vos clients obtiennent des communications opportunes, précises, pratiques, sécurisées et pertinentes. Votre entreprise optimise la valeur des interactions avec la clientèle et réduit les coûts et les risques à l’aide d’un processus favorisant aisance, vitesse et productivité.

Une configuration simple de la solution Correspondence Management comprend une instance d’auteur et une instance de publication sur la même machine ou sur des machines différentes.

### Gestionnaire des formulaires  {#forms-manager}

Forms Manager simplifie le processus de mise à jour, de gestion et de retrait de formulaires.

### Espace de travail AEM Forms {#html-workspace}

L’espace de travail AEM Forms dispose des mêmes fonctionnalités que le Flex Workspace existant (obsolète pour AEM Forms on JEE) et ajoute de nouvelles fonctionnalités pour étendre et intégrer Workspace et le rendre plus convivial.

>[!NOTE]
>
>Flex Workspace est obsolète pour la version d’AEM Forms.

Il permet la gestion des tâches sur les clients sans Flash Player et Adobe Reader. Il facilite le rendu de formulaires HTML, en plus des formulaires PDF et Flex.

## Base de données des formulaires AEM  {#aem-forms-database}

La base de données AEM Forms stocke le contenu (artefacts de formulaire, configurations de service, état de traitement et références de base de données) dans les fichiers du répertoire de stockage global de documents et du répertoire racine de stockage de contenu (pour Content Services). Les sauvegardes de la base de données peuvent être exécutées en temps réel, sans interruption de service. La récupération s’effectue quant à elle à un moment spécifique ou suite à un changement précis. Cette section explique de quelle façon configurer votre base de données pour qu’elle puisse être sauvegardée en temps réel.

Dans un système AEM Forms correctement configuré, l’administrateur système et l’administrateur de la base de données peuvent facilement travailler ensemble pour récupérer le système dans un état connu cohérent.

Pour sauvegarder la base de données en temps réel, vous devez utiliser le mode instantané ou configurer votre base de données pour qu’elle s’exécute dans le mode de consignation spécifié. Ainsi, les fichiers de données de la base de données peuvent-ils être sauvegardés pendant que la base de données est ouverte et disponible pour utilisation. De plus, dans ces modes, la base de données conserve ses journaux de restauration et de transaction.

>[!NOTE]
>
>Adobe® LiveCycle® Content Services ES (obsolète) est un système de gestion de contenu installé avec LiveCycle. Il permet aux utilisateurs de concevoir, gérer, surveiller et optimiser des processus pour des intervenants humains. La prise en charge de Content Services (obsolète) s’est terminée le 31/12/2014. Consultez le[ Document sur le cycle de vie des produits Adobe](https://www.adobe.com/support/products/enterprise/eol/eol_matrix.html). Pour en savoir plus sur la configuration de Content Services (obsolète), voir [Administration de Content Services](https://help.adobe.com/en_US/livecycle/9.0/admin_contentservices.pdf).

### DB2 {#db2}

Configurez votre base de données DB2 pour qu’elle s’exécute en mode de consignation en archives.

>[!NOTE]
>
>Si votre environnement AEM Forms a été mis à niveau depuis une version précédente d’AEM Forms et utilise DB2, la sauvegarde en ligne n’est pas prise en charge. Dans ce cas, vous devez fermer AEM Forms et procéder à une sauvegarde hors ligne. Les futures versions d’AEM Forms prendront en charge les sauvegardes en ligne pour les clients effectuant une mise à niveau.

IBM propose une suite d’outils et des systèmes d’aide permettant aux administrateurs de base de données de gérer leurs sauvegardes et récupérations :

* IBM DB2 Archive Log Accelerator (voir [IBM DB2 Archive Log Accelerator for z/OS User’s Guide](https://publib.boulder.ibm.com/infocenter/dzichelp/v2r2/topic/com.ibm.db2tools.alc.doc.ug/alcugb20.pdf?noframes=true)).
* IBM DB2 Data Archive Expert (voir [IBM DB2 Data Archive Expert User’s Guide and Reference](https://publib.boulder.ibm.com/infocenter/mptoolic/v1r0/topic/com.ibm.db2tools.aeu.doc.ug/ahxugb13.pdf?noframes=true)).

DB2 possède des capacités intégrées permettant de sauvegarder une base de données vers Tivoli Storage Manager. A l’aide de Tivoli Storage Manager, les sauvegardes DB2 peuvent être stockées sur d’autres supports et disques durs locaux.

Pour plus de détails sur la sauvegarde et la récupération des bases de données DB2, voir [Developing a backup and recovery strategy for DB2](https://publib.boulder.ibm.com/infocenter/db2luw/v9/index.jsp?topic=/com.ibm.db2.udb.admin.doc/doc/c0005945.htm).

### Oracle {#oracle}

Utilisez des sauvegardes de type instantané ou configurez votre base de données Oracle pour qu’elle s’exécute en mode de consignation en archives (voir le document [Oracle Backup: An Introduction](https://www.databasedesign-resource.com/oracle-backup.md).) Pour plus d’informations sur la sauvegarde et la récupération de votre base de données Oracle, visitez les sites Web suivants :

[Oracle Backup and Recovery :](https://www.oracle.com/technetwork/database/features/availability/br-overview-097160.html) explique en détail les concepts de sauvegarde et de récupération, les techniques les plus couramment employées pour utiliser Recovery Manager (RMAN) à des fins de sauvegarde, de récupération et de génération de rapports, de même que la planification d’une stratégie de sauvegarde et de récupération.

[Oracle Database Backup and Recovery User’s Guide :](https://download.oracle.com/docs/cd/E11882_01/backup.112/e10642.pdf) fournit des informations détaillées sur l’architecture RMAN, les concepts et les mécanismes de sauvegarde et de récupération, des techniques de récupération avancées telles que les fonctions de récupération instantanée et de flashback de base de données, de même que le réglage des performances de sauvegarde et de récupération. Il couvre également les opérations de sauvegarde et de récupération gérées par l’utilisateur, à l’aide d’installations de système d’exploitation hôte au lieu de RMAN. Ce volume est essentiel pour la sauvegarde et la récupération de déploiements de base de données plus sophistiqués et pour les scénarios de récupération avancés.

[Oracle Database Backup and Recovery Reference :](https://download.oracle.com/docs/cd/E11882_01/backup.112/e10643.pdf) présente des informations complètes sur la syntaxe et la sémantique de toutes les commandes RMAN et décrit les vues de base de données disponibles pour générer des rapports sur les activités de sauvegarde et de récupération.

### SQL Server  {#sql-server}

Utilisez des sauvegardes de type instantané ou configurez votre base de données SQL Server pour qu’elle s’exécute en mode de consignation de transactions.

SQL Server propose également deux outils de sauvegarde et de récupération :

* SQL Server Management Studio (interface utilisateur graphique)
* T-SQL (ligne de commande)

Pour plus d’informations, voir [Sauvegarde et restauration](https://msdn.microsoft.com/en-us/library/ms187048(v=SQL.90).aspx).

### MySQL {#mysql}

Utilisez MySQLAdmin ou modifiez les fichiers INI dans Windows pour configurer votre base de données MySQL pour qu’elle s’exécute en mode de consignation binaire (Voir [Connexion binaire MySQL](https://dev.mysql.com/doc/refman/5.1/en/binary-log.html)). Un outil de sauvegarde à chaud pour MySQL est également disponible à partir du logiciel InnoBase (Voir [Sauvegarde à chaud avec Innobase](https://www.innodb.com/hot-backup/features.md)).

>[!NOTE]
>
>le mode de connexion binaire par défaut pour MySQL est Instruction ; il est incompatible avec les tables utilisées par Content Services (obsolète). L’utilisation de la connexion binaire dans ce mode par défaut fait échouer Content Services (obsolète). Si votre système inclut Content Services (obsolète), utilisez le mode de connexion mixte. Pour activer la connexion mixte, ajoutez l’argument suivant au fichier my.ini :  `binlog_format=mixed log-bin=logname`

Vous pouvez utiliser l’utilitaire mysqldump pour effectuer la sauvegarde intégrale de la base de données. Les sauvegardes intégrales sont nécessaires, mais ne sont pas toujours pratiques. Elles génèrent des fichiers de sauvegarde volumineux et leur exécution prend du temps. Pour effectuer une sauvegarde incrémentielle, veillez à démarrer le serveur avec l’option - `log-bin` comme décrit dans la section précédente. A chaque fois que le serveur MySQL redémarre, il cesse d’écrire dans le journal binaire courant, en crée un nouveau, qui devient dès lors le nouveau journal binaire courant. Vous pouvez forcer un commutateur manuellement à l’aide de la commande `FLUSH LOGS SQL`. Après la première sauvegarde intégrale, les sauvegardes incrémentielles suivantes sont effectuées en utilisant l’utilitaire mysqladmin avec la commande `flush-logs`, qui crée le fichier journal suivant.

Voir [Résumé de la stratégie de sauvegarde](https://dev.mysql.com/doc/refman/5.5/en/backup-strategy-summary.html).

```text
binlog_format=mixed
log-bin=logname
```

## Répertoire racine de stockage de contenu (Content Services uniquement)  {#content-storage-root-directory-content-services-only}

Le répertoire racine de stockage de contenu contient le référentiel Content Services (obsolète) dans lequel sont stockés tous les documents, artefacts et index. L’arborescence du répertoire racine de stockage de contenu doit être sauvegardée. Cette section décrit de quelle façon déterminer l’emplacement du répertoire racine de stockage de contenu pour les environnements autonomes et organisés en grappe.

### Emplacement racine de stockage de contenu (environnement autonome)  {#content-storage-root-location-stand-alone-environment}

Le répertoire racine de stockage de contenu est créé à l’installation de Content Services (obsolète). Le processus d’installation d’AEM Forms détermine l’emplacement du répertoire racine de stockage de contenu.

L’emplacement par défaut du répertoire racine de stockage de contenu est `[aem-forms root]/lccs_data`.

Sauvegardez les répertoires suivants situés dans le répertoire racine de stockage de contenu :

/audit.contentstore

/contentstore

/contentstore.deleted

/backup-lucene-indexes

Si le répertoire /backup-lucene-indexes est absent, sauvegardez le répertoire /lucene-indexes (également situé dans le répertoire racine de stockage de contenu). Si le répertoire /backup-lucene-indexes existe, ne sauvegardez pas le répertoire /lucene-indexes car cela pourrait générer des erreurs.

### Emplacement racine de stockage de contenu (environnement organisé en grappes)  {#content-storage-root-location-clustered-environment}

Lors de l’installation de Content Services (obsolète) dans un environnement organisé en grappe, le répertoire racine de stockage de contenu se divise en deux répertoires distincts :

**Répertoire racine de stockage de contenu :** répertoire réseau partagé habituellement accessible en mode lecture/écriture pour tous les nœuds de la grappe.

**Répertoire racine d’index :** répertoire créé sur chaque nœud de la grappe et ayant toujours les mêmes chemin et nom.

L’emplacement par défaut du répertoire racine de stockage de contenu est `[GDS root]/lccs_data`, où `[GDS root]` est l’emplacement décrit dans [Emplacement du répertoire de stockage global de documents](files-back-recover.md#gds-location). Sauvegardez les répertoires suivants situés dans le répertoire racine de stockage de contenu :

/audit.contentstore

/contentstore

/contentstore.deleted

/backup-lucene-indexes

Si le répertoire /backup-lucene-indexes est absent, sauvegardez le répertoire /lucene-indexes (également situé dans le répertoire racine de stockage de contenu). Si le répertoire /backup-lucene-indexes existe, ne sauvegardez pas le répertoire /lucene-indexes car cela pourrait générer des erreurs.

L’emplacement par défaut du répertoire racine d’index est `[aem-forms root]/lucene-indexes` sur chaque noeud.

## Polices personnalisées {#customer-installed-fonts}

Sauvegardez séparément les polices supplémentaires éventuellement installées dans votre environnement AEM Forms. Sauvegardez tous les répertoires de polices Adobe et de polices personnalisées tel qu’indiqué dans Administration Console sous Paramètres > Core System > Configurations. Assurez-vous de sauvegarder l’intégralité du répertoire de polices.

>[!NOTE]
>
>Par défaut, les polices Adobe installées avec AEM forms se trouvent dans le répertoire `[aem-forms root]/fonts`.

Si vous réinitialisez le système d’exploitation sur l’ordinateur hôte et que vous souhaitez utiliser des polices du précédent système d’exploitation, le contenu du répertoire des polices système doit également être sauvegardé. (Pour plus d’instructions, reportez-vous à la documentation de votre système d’exploitation).
