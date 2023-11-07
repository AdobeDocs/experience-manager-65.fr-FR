---
title: Fichiers à sauvegarder et à récupérer
description: Ce document décrit l’application et les fichiers de données à sauvegarder.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: d2dd381d-a7d2-4fec-a8ba-7ca037fd9dc1
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '2065'
ht-degree: 16%

---

# Fichiers à sauvegarder et à récupérer {#files-to-back-up-and-recover}

L’application et les fichiers de données à sauvegarder sont décrits plus en détail dans les sections suivantes.

Tenez compte des points suivants concernant la sauvegarde et la récupération :

* La base de données doit être sauvegardée avant le stockage global de documents et le référentiel AEM.
* Si vous avez besoin de faire descendre les nœuds dans un environnement organisé en grappes pour la sauvegarde, assurez-vous que les nœuds secondaires sont fermés avant le nœud principal. Dans le cas contraire, une incohérence peut survenir dans la grappe ou le serveur. En outre, le nœud principal doit être rendu actif avant tout nœud secondaire.
* Pour l’opération de restauration d’une grappe, le serveur d’applications doit être arrêté pour chaque noeud de la grappe.

## Répertoire de stockage global de documents {#global-document-storage-directory}

Le répertoire de stockage global de documents est utilisé pour stocker les fichiers de longue durée utilisés dans un processus. La durée de vie des fichiers de longue durée est destinée à couvrir un ou plusieurs lancements d’un système d’AEM forms et peut s’étendre sur plusieurs jours, voire plusieurs années. Ces fichiers de longue durée peuvent inclure des PDF, des stratégies et des modèles de formulaire. Les fichiers de longue durée sont une partie essentielle de l’état global de nombreux déploiements d’AEM forms. Si certains ou tous les documents de longue durée sont perdus ou corrompus, le serveur Forms peut devenir instable.

Les documents d’entrée pour un appel de tâche asynchrone sont également stockés dans le répertoire de stockage global de documents et doivent être disponibles pour traiter les demandes. Par conséquent, il est important de tenir compte de la fiabilité du système de fichiers qui héberge le répertoire de stockage global de documents et d’utiliser un ensemble redondant de disques indépendants (RAID) ou d’autres technologies adaptées à vos besoins en termes de qualité et de niveau de service.

L’emplacement du répertoire de stockage global de documents est déterminé pendant le processus d’installation d’AEM forms ou ultérieurement à l’aide d’Administration Console. En plus de conserver un emplacement de haute disponibilité pour le stockage global de documents, vous pouvez également activer le stockage de base de données pour les documents. Voir [Options de sauvegarde lors de l’utilisation de la base de données pour le stockage de documents](files-back-recover.md#backup-options-when-database-is-used-for-document-storage).

### Emplacement du répertoire de stockage global de documents {#gds-location}

Si vous laissez le paramètre d’emplacement vide lors de l’installation, l’emplacement par défaut est un répertoire sous l’installation du serveur d’applications. Vous devez sauvegarder le répertoire suivant pour votre serveur d’applications :

* (JBoss) `[appserver root]/server/'server'/svcnative/DocumentStorage`
* (WebLo gic) `[appserverdomain]/'server'/adobe/AEMformsserver/DocumentStorage`
* (WebSphere) `[appserver root]/installedApps/adobe/'server'/DocumentStorage`

Si vous avez remplacé le répertoire de stockage global de documents par un autre emplacement que celui par défaut, vous pouvez le déterminer comme suit :

* Connectez-vous à Administration Console et cliquez sur Paramètres > Paramètres de Core System > Configurations.
* Enregistrez l’emplacement spécifié dans la zone Répertoire de stockage global de documents.

Dans un environnement organisé en grappe, le répertoire de stockage global de documents pointe généralement vers un répertoire partagé sur le réseau et est accessible en lecture/écriture pour chaque noeud de la grappe.

L’emplacement du répertoire de stockage global de documents peut être modifié lors d’une récupération si l’emplacement d’origine n’est plus disponible. (Voir [Modification de l’emplacement du répertoire de stockage global de documents pendant la récupération](/help/forms/using/admin-help/recovering-aem-forms-data.md#changing-the-gds-location-during-recovery).)

### Options de sauvegarde lors de l’utilisation de la base de données pour le stockage de documents {#backup-options-when-database-is-used-for-document-storage}

Vous pouvez activer le stockage de documents d’AEM forms dans la base de données d’AEM forms à l’aide de la console d’administration. Même si cette option conserve tous les documents persistants dans la base de données, AEM forms a toujours besoin du répertoire de stockage global de documents basé sur le système de fichiers, car il est utilisé pour stocker les fichiers et ressources permanents et temporaires liés aux sessions et aux appels d’AEM forms.

Lorsque vous sélectionnez l’option « Activer le stockage de documents dans la base de données » dans les paramètres de Core System dans Administration Console ou à l’aide du gestionnaire de configuration, AEM Forms n’autorise pas les modes de sauvegarde d’instantané et de sauvegarde de restauration. Par conséquent, vous n’avez pas besoin de gérer les modes de sauvegarde à l’aide d’AEM forms. Si vous utilisez cette option, sauvegardez le répertoire de stockage global de documents une seule fois après avoir activé l’option. Lorsque vous récupérez AEM forms à partir d’une sauvegarde, il n’est pas nécessaire de renommer le répertoire de sauvegarde du répertoire de stockage global de documents ni de restaurer ce dernier.

## Référentiel AEM {#aem-repository}

AEM référentiel (crx-repository) est créé si crx-repository est configuré lors de l’installation d’AEM forms. L’emplacement du répertoire crx-repository est déterminé pendant le processus d’installation d’AEM forms. AEM sauvegarde et restauration du référentiel sont requises, ainsi que la base de données et le répertoire de stockage global de documents, pour que les données d’AEM forms dans les formulaires soient cohérentes. AEM référentiel contient des données pour la solution Correspondence Management, Forms Manager et AEM Forms Workspace.

### Solution Correspondence Management {#correspondence-management-solution}

La solution Correspondence Management centralise et gère la création, l’assemblage et la diffusion de correspondances sécurisées, personnalisées et interactives. Il vous permet d’assembler rapidement une correspondance à partir de contenu prévalidé et personnalisé dans un processus simplifié allant de la création à l’archivage. Par conséquent, vos clients reçoivent une communication opportune, précise, pratique, sécurisée et pertinente. Votre entreprise optimise la valeur des interactions client et réduit les coûts et les risques grâce à un processus simplifié pour faciliter, accélérer et accroître la productivité.

Une configuration simple de la solution Correspondence Management comprend une instance d’auteur et une instance de publication sur le même ordinateur ou sur différents ordinateurs.

### gestionnaire de formulaires {#forms-manager}

Forms Manager simplifie le processus de mise à jour, de gestion et de retrait des formulaires.

### Espace de travail AEM Forms {#html-workspace}

AEM Forms Workspace correspond aux fonctionnalités de Flex Workspace (obsolète pour AEM forms on JEE) et ajoute de nouvelles fonctionnalités pour étendre et intégrer Workspace et le rendre plus convivial.

>[!NOTE]
>
>L’espace de travail Flex est obsolète pour la version d’AEM Forms.

Il permet la gestion des tâches sur les clients sans Flash Player ni Adobe Reader. Il facilite le rendu de Forms HTML, en plus des PDF forms et des formulaires Flex.

## AEM base de données forms {#aem-forms-database}

La base de données d’AEM forms stocke du contenu tel que des artefacts de formulaire, des configurations de service, un état de traitement et des références de base de données dans les fichiers du répertoire de stockage global de documents et du répertoire racine de stockage de contenu (pour Content Services). Les sauvegardes de la base de données peuvent être effectuées en temps réel sans interruption de service, et la récupération peut être effectuée à un moment précis ou à un changement particulier. Cette section décrit comment configurer votre base de données pour qu’elle puisse être sauvegardée en temps réel.

Sur un système d’AEM forms correctement configuré, l’administrateur système et l’administrateur de base de données peuvent facilement collaborer pour récupérer le système dans un état connu et cohérent.

Pour sauvegarder la base de données en temps réel, vous devez utiliser le mode instantané ou configurer votre base de données pour qu’elle s’exécute dans le mode de journalisation spécifié. Cela permet de sauvegarder vos fichiers de base de données tant que la base de données est ouverte et disponible à l’utilisation. En outre, la base de données conserve ses logs de restauration et de transaction lorsqu’elle s’exécute dans ces modes.

>[!NOTE]
>
>Adobe® LiveCycle® Content Services ES (obsolète) est un système de gestion de contenu installé avec LiveCycle. Il permet aux utilisateurs de concevoir, gérer, surveiller et optimiser des processus pour des intervenants humains. La prise en charge de Content Services (obsolète) prend fin le 12/31/2014. Consultez le[ Document sur le cycle de vie des produits Adobe](https://www.adobe.com/fr/support/products/enterprise/eol/eol_matrix.html).

### DB2 {#db2}

Configurez votre base de données DB2 pour qu’elle s’exécute en mode de consignation des archives.

>[!NOTE]
>
Si votre environnement d’AEM forms a été mis à niveau à partir d’une version précédente d’AEM forms et utilise DB2, la sauvegarde en ligne n’est pas prise en charge. Dans ce cas, vous devez arrêter AEM forms et effectuer une sauvegarde hors ligne. Les futures versions d’AEM forms prendront en charge la sauvegarde en ligne pour les clients effectuant la mise à niveau.

IBM dispose d’une suite d’outils et de systèmes d’aide pour aider les administrateurs de base de données à gérer leurs tâches de sauvegarde et de récupération :

* Accélérateur de journaux d’archives IBM DB2
* Expert en archivage de données IBM DB2

DB2 dispose de fonctionnalités intégrées pour sauvegarder une base de données dans Tivoli Storage Manager. En utilisant Tivoli Storage Manager, les sauvegardes DB2 peuvent être stockées sur d’autres supports ou sur le disque dur local.

### Oracle {#oracle}

Utilisez des sauvegardes instantanées ou configurez votre base de données Oracle pour qu’elle s’exécute en mode de consignation d’archivage. (Voir [Sauvegarde d’Oracle : Introduction](https://www.databasedesign-resource.com/oracle-backup.md).) Pour plus d’informations sur la sauvegarde et la récupération de votre base de données Oracle, consultez les sites suivants :

[Sauvegarde et récupération des Oracles :](https://www.oracle.com/technetwork/database/features/availability/br-overview-097160.html) Décrit les concepts de sauvegarde et de récupération, ainsi que les techniques les plus courantes pour utiliser Recovery Manager (RMAN) à des fins de sauvegarde, de récupération et de création de rapports plus en détail, et fournit des informations supplémentaires sur la planification d’une stratégie de sauvegarde et de récupération.

[Oracle de la sauvegarde et de la récupération de la base de données Guide de l’utilisateur :](https://download.oracle.com/docs/cd/E11882_01/backup.112/e10642.pdf) Fournit des informations détaillées sur l’architecture RMAN, les concepts et les mécanismes de sauvegarde et de récupération, des techniques de récupération avancées telles que la récupération instantanée et les fonctionnalités de flashback de base de données, ainsi que l’optimisation des performances de sauvegarde et de récupération. Il couvre également la sauvegarde et la récupération gérées par l’utilisateur, à l’aide des installations du système d’exploitation hôte au lieu de RMAN. Ce volume est essentiel pour la sauvegarde et la récupération de déploiements de base de données plus sophistiqués et pour les scénarios de récupération avancés.

[Référence sur la sauvegarde et la récupération de la base de données Oracle :](https://download.oracle.com/docs/cd/E11882_01/backup.112/e10643.pdf) Fournit des informations complètes sur la syntaxe et la sémantique de toutes les commandes RMAN et décrit les vues de base de données disponibles pour la création de rapports sur les activités de sauvegarde et de récupération.

### SQL Server {#sql-server}

Utilisez des sauvegardes de type instantané ou configurez votre base de données SQL Server pour qu’elle s’exécute en mode journal de transaction.

SQL Server fournit également deux outils de sauvegarde et de récupération :

* SQL Server Management Studio (GUI)
* T-SQL (ligne de commande)

Pour plus d’informations, voir [Sauvegarder et restaurer](https://msdn.microsoft.com/fr-fr/library/ms187048(v=SQL.90).aspx).

### MySQL {#mysql}

Utilisez MySQLAdmin ou modifiez les fichiers INI dans Windows pour configurer votre base de données MySQL afin qu’elle s’exécute en mode de journalisation binaire. (Voir [Journalisation binaire MySQL](https://dev.mysql.com/doc/refman/5.1/fr/binary-log.html).) Un outil de sauvegarde à chaud pour MySQL est également disponible à partir du logiciel InnoBase. (Voir [Sauvegarde à chaud Innobase](https://www.innodb.com/hot-backup/features.md).)

>[!NOTE]
>
Le mode de connexion binaire par défaut pour MySQL est &quot;Statement&quot;, qui est incompatible avec les tables utilisées par Content Services (obsolète). L’utilisation de la connexion binaire dans ce mode par défaut entraîne l’échec de Content Services (obsolète). Si votre système inclut Content Services (obsolète), utilisez le mode de journalisation &quot;mixte&quot;. Pour activer la journalisation &quot;mixte&quot;, ajoutez l’argument suivant au fichier my.ini : `binlog_format=mixed log-bin=logname`

Vous pouvez utiliser l’utilitaire mysqldump pour obtenir la sauvegarde complète de la base de données. Des sauvegardes complètes sont requises, mais elles ne sont pas toujours pratiques. Ils produisent des fichiers de sauvegarde volumineux et prennent du temps à générer. Pour exécuter une sauvegarde incrémentielle, veillez à démarrer le serveur avec l’option `log-bin`, comme décrit dans la section précédente. A chaque fois que le serveur MySQL redémarre, il cesse d’écrire dans le journal binaire courant, en crée un nouveau, qui devient dès lors le nouveau journal binaire courant. Vous pouvez forcer un basculement manuel avec la commande `FLUSH LOGS SQL`. Après la première sauvegarde intégrale, les sauvegardes incrémentielles suivantes sont effectuées en utilisant l’utilitaire mysqladmin avec la commande `flush-logs`, qui crée le fichier journal suivant.

Voir [Résumé de la stratégie de sauvegarde](https://dev.mysql.com/doc/refman/5.5/fr/backup-strategy-summary.html).

```text
binlog_format=mixed
log-bin=logname
```

## Répertoire racine de stockage de contenu (Content Services uniquement) {#content-storage-root-directory-content-services-only}

Le répertoire racine de stockage de contenu contient le référentiel Content Services (obsolète) dans lequel sont stockés tous les documents, artefacts et index. L’arborescence du répertoire racine de stockage de contenu doit être sauvegardée. Cette section décrit comment déterminer l’emplacement du répertoire racine de stockage de contenu pour les environnements autonomes et organisés en grappe.

### Emplacement racine de stockage de contenu (environnement autonome) {#content-storage-root-location-stand-alone-environment}

Le répertoire racine de stockage de contenu est créé lorsque Content Services (obsolète) est installé. L’emplacement du répertoire racine de stockage de contenu est déterminé pendant le processus d’installation d’AEM forms.

L’emplacement par défaut du répertoire racine de stockage de contenu est `[aem-forms root]/lccs_data`.

Sauvegardez les répertoires suivants dans le répertoire racine de stockage de contenu :

/audit.contentstore

/contentstore

/contentstore.deleted

/backup-lucene-indexes

Si le répertoire /backup-lucene-indexes n’est pas présent, sauvegardez le répertoire /lucene-indexes, également dans le répertoire racine de stockage de contenu. Si le répertoire /backup-lucene-indexes existe, ne sauvegardez pas le répertoire /lucene-indexes, car cela peut entraîner des erreurs.

### Emplacement racine de stockage de contenu (environnement en grappe) {#content-storage-root-location-clustered-environment}

Lorsque vous installez Content Services (obsolète) dans un environnement en grappe, le répertoire racine de stockage de contenu est divisé en deux répertoires distincts :

**Répertoire racine de stockage de contenu :** En règle générale, un répertoire réseau partagé en lecture/écriture est accessible pour tous les noeuds de la grappe.

**Répertoire racine de l’index :** Répertoire créé sur chaque noeud de la grappe, avec toujours le même chemin et le même nom de répertoire.

L’emplacement par défaut du répertoire racine de stockage de contenu est `[GDS root]/lccs_data`, où `[GDS root]` correspond à l’emplacement décrit à la [section GDS (stockage global de documents)](files-back-recover.md#gds-location). Sauvegardez les répertoires suivants dans le répertoire racine de stockage de contenu :

/audit.contentstore

/contentstore

/contentstore.deleted

/backup-lucene-indexes

Si le répertoire /backup-lucene-indexes n’est pas présent, sauvegardez le répertoire /lucene-indexes, également dans le répertoire racine de stockage de contenu. Si le répertoire /backup-lucene-indexes existe, ne sauvegardez pas le répertoire /lucene-indexes, car cela peut entraîner des erreurs.

L’emplacement par défaut du répertoire racine d’index est `[aem-forms root]/lucene-indexes` sur chaque nœud.

## Polices personnalisées {#customer-installed-fonts}

Si vous avez installé des polices supplémentaires dans votre environnement de AEM forms, vous devez les sauvegarder séparément. Sauvegardez tous les répertoires de polices d’Adobe et de polices du client spécifiés dans Administration Console sous Paramètres > Core System > Configurations. Assurez-vous de sauvegarder l’intégralité du répertoire des polices.

>[!NOTE]
>
Par défaut, les polices Adobe installées avec AEM forms se trouvent dans la variable `[aem-forms root]/fonts` répertoire .

Si vous réinitialisez le système d’exploitation sur l’ordinateur hôte et que vous souhaitez utiliser des polices du système d’exploitation précédent, le contenu du répertoire des polices système doit également être sauvegardé. (Pour obtenir des instructions spécifiques, consultez la documentation de votre système d’exploitation).
