---
title: Stratégie de sauvegarde et de restauration dans un environnement organisé en grappes
seo-title: Strategy for backup and restore in a clustered environment
description: Si votre déploiement d’AEM Forms stocke les données personnalisées supplémentaires dans une base de données différente, vous devez mettre en place une stratégie de sauvegarde pour ces données veillant à ce qu’elles soient synchronisées avec les données AEM Forms.
seo-description: If your AEM forms implementation stores additional custom data in a different database, you must implement a strategy to back up this data ensuring that it remains in sync with the AEM forms data.
uuid: c29b989c-30ed-4a8e-bab8-9b7746291a33
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: c332985b-4556-4056-961a-fce2356da88d
exl-id: 98c96349-f253-475f-b646-352269814a38
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '1476'
ht-degree: 100%

---

# Stratégie de sauvegarde et de restauration dans un environnement organisé en grappes {#strategy-for-backup-and-restore-in-a-clustered-environment}

>[!NOTE]
>
>Si votre déploiement d’AEM forms stocke les données personnalisées supplémentaires dans une base de données différente, vous devez mettre en place une stratégie de sauvegarde pour ces données veillant à ce qu’elles soient synchronisées avec les données AEM forms. De plus, vous devez concevoir l’application de sorte à ce qu’elle puisse gérer un scénario dans lequel les bases de données supplémentaires se désynchronisent. Il est fortement recommandé d’effectuer toutes les opérations de base de données dans le contexte d’une transaction pour veiller à sa cohérence.

Vous devez sauvegarder les éléments suivants du système AEM Forms pour récupérer d’une erreur :

* Base de données utilisée par AEM Forms
* le stockage global de document qui contient des données anciennes et autres documents persistants ;
* la base de données AEM (crx-repository).

>[!NOTE]
>
>Vous devez sauvegarder toutes les autres données qui sont utilisées par votre configuration d’AEM Forms, telles que les polices du client, les données des connecteurs, etc.

## Sauvegarde d’un environnement organisé en grappes {#back-up-a-clustered-environment}

Cette rubrique présente les stratégies suivantes pour sauvegarder tout environnement organisé en grappes d’AEM Forms :

* Sauvegarde hors connexion avec temps d’interruption
* Sauvegarder hors connexion sans temps d’interruption (sauvegarde d’un nœud secondaire qui est arrêté)
* Sauvegarde en ligne sans temps d’interruption, mais un retard de réponse
* Sauvegarde du fichier de propriétés de démarrage

### Sauvegarde hors connexion avec temps d’interruption {#offline-backup-with-downtime}

1. Arrêtez l’ensemble de la grappe et des services connexes. (Voir la section [Démarrage et arrêt des services](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services).)
1. Sur n’importe quel nœud, sauvegardez la base de données, le stockage global de documents et les connecteurs. (Voir [Fichiers à sauvegarder et à récupérer](/help/forms/using/admin-help/files-back-recover.md#files-to-back-up-and-recover).)
1. Effectuez les étapes suivantes pour sauvegarder le référentiel AEM hors ligne :

   1. Pour chaque nœud de la grappe, sauvegarder le fichier qui contient l’identifiant du nœud de la grappe.
   1. Sauvegardez tous les fichiers de tout nœud secondaire du cluster, notamment les sous-répertoires.
   1. Sauvegardez l’identifiant du référentiel/système de chaque nœud de la grappe séparément.

   Pour les étapes détaillées, voir [Sauvegarde et restauration](https://docs.adobe.com/docs/fr/crx/current/administering/backup_and_restore.html).

1. Le cas échéant, sauvegardez toutes les autres données, telles que les polices du client.
1. Redémarrez la grappe.

### Sauvegarde hors connexion sans temps d’interruption {#offline-backup-with-no-downtime}

1. Passez en mode de sauvegarde restauration. (Voir [Passage en mode de sauvegarde](/help/forms/using/admin-help/backing-aem-forms-data.md#entering-the-backup-modes).)

   Notez qu’il est nécessaire de quitter le mode de sauvegarde restauration après une restauration.

1. Arrêtez l’un des nœuds secondaires du cluster par rapport à AEM. (Voir la section [Démarrage et arrêt des services](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services).)
1. Sur n’importe quel nœud, sauvegardez la base de données, le stockage global de documents et les connecteurs. (Voir [Fichiers à sauvegarder et à récupérer](/help/forms/using/admin-help/files-back-recover.md#files-to-back-up-and-recover).)
1. Effectuez les étapes suivantes pour sauvegarder le référentiel AEM hors ligne :

   1. Pour chaque nœud de la grappe, sauvegarder le fichier qui contient l’identifiant du nœud de la grappe.
   1. Sauvegardez tous les fichiers de tout nœud secondaire du cluster, notamment les sous-répertoires.
   1. Sauvegardez le fichier repository/system.id de chaque nœud de la grappe séparément.

   Pour les étapes détaillées, voir [Sauvegarde et restauration](https://docs.adobe.com/docs/fr/crx/current/administering/backup_and_restore.html).

1. Le cas échéant, sauvegardez toutes les autres données, telles que les polices du client.
1. Redémarrez la grappe.

### Sauvegarde en ligne sans temps d’interruption, mais un retard de réponse {#online-backup-with-no-downtime-but-delay-in-response}

1. Passez en mode de sauvegarde restauration. (Voir [Passage en mode de sauvegarde](/help/forms/using/admin-help/backing-aem-forms-data.md#entering-the-backup-modes).)

   Notez qu’il est nécessaire de quitter le mode de sauvegarde restauration après une restauration.

1. Arrêtez l’un des nœuds secondaires du cluster par rapport à AEM. (Voir la section [Démarrage et arrêt des services](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services).)
1. Sur n’importe quel nœud, sauvegardez la base de données, le stockage global de documents et les connecteurs. (Voir [Fichiers à sauvegarder et à récupérer](/help/forms/using/admin-help/files-back-recover.md#files-to-back-up-and-recover).)
1. Effectuez les étapes suivantes pour sauvegarder le référentiel AEM en ligne :

   1. Pour chaque nœud de la grappe, sauvegardez le fichier qui contient le cluster_node.id.
   1. Sauvegardez le fichier repository/system.id de chaque nœud de la grappe séparément.
   1. Sur n’importe quel nœud secondaire, réalisez une sauvegarde en ligne du référentiel (pour connaître les étapes détaillées, reportez-vous à la section Sauvegarde en ligne).

1. Le cas échéant, sauvegardez toutes les autres données, telles que les polices du client.
1. Redémarrez la grappe.

### Sauvegarde du fichier de propriétés de démarrage {#back-up-the-bootstrap-properties-file}

Lorsque nous créons un cluster AEM, un fichier de propriétés est créé dans le serveur d’applications pour tous les nœuds secondaires. Il est conseillé de sauvegarder le fichier de propriétés de démarrage. Vous pouvez trouver le fichier à l’emplacement suivant sur votre serveur d’applications :

* JBoss : dans le répertoire BIN
* WebLogic : dans le répertoire de domaine
* WebSphere : dans le répertoire de profil

Vous devez sauvegarder le fichier en cas de scénario de récupération après catastrophe du nœud secondaire AEM et le replacer à l’emplacement indiqué sur le serveur d’applications, en cas de restauration.

## Récupération dans un environnement organisé en grappes {#recovery-in-a-clustered-environment}

Dans le cas d’un échec de l’ensemble de la grappe ou d’un seul nœud, vous devez le restaurer à l’aide de la sauvegarde.

Pour la récupération d’un nœud unique, il vous suffit d’arrêter le nœud et d’exécuter la procédure de récupération pour un nœud unique.

Dans le cas d’un échec de l’ensemble de la grappe en raison d’échecs tels qu’une panne de base de données, vous devez effectuer les étapes suivantes. La restauration dépend de la méthode de sauvegarde utilisée.

### Restauration d’un nœud unique {#restoring-a-single-node}

1. Arrêtez le nœud corrompu.

   >[!NOTE]
   >
   >Si le nœud corrompu est un nœud principal AEM, arrêtez le nœud de l’intégralité du cluster.

1. Recréez le système physique à partir d’une image système.
1. Appliquez à AEM Forms les correctifs et mises à jour qui ont été appliqués depuis que l’image a été réalisée. Cette information a été mentionnée durant la procédure de sauvegarde. AEM Forms doit être récupéré au même niveau de correctif auquel il se trouvait lors de la sauvegarde du système.
1. (*Facultatif*) Si tous les autres nœuds fonctionnent, il est possible que le référentiel AEM soit également corrompu. Dans ce cas, vous verrez un message de non-synchronisation du référentiel dans le fichier error.log du référentiel AEM.

   Pour restaurer le référentiel, effectuez les étapes suivantes.

   >[!NOTE]
   >
   >Si une sauvegarde compressée de crx-repository a été réalisée en ligne, décompressez-la à l’emplacement qui vous convient et suivez le processus de restauration hors ligne.

   1. Supprimez le répertoire partagé et les répertoires du référentiel, de version et des espaces de travail dans le répertoire clusterNode du nœud.
   1. Restaurez la sauvegarde du nœud de la grappe (notamment les sous-répertoires) pour le nœud.
   1. Supprimez le fichier clusterNode/revision.log sur le nœud.
   1. Supprimez le fichier .lock sur le nœud, le cas échéant.
   1. Supprimez le fichier repository/system.id sur le nœud, le cas échéant.
   1. Supprimez les fichiers &amp;ast;&amp;ast;/listener.properties sur le nœud, le cas échéant.
   1. Restaurez le fichier repository/cluster_node.id pour les nœuds individuels de la grappe.

>[!NOTE]
>
>Examinez les points suivants :

* Si le nœud en échec était un nœud principal AEM, copiez tout le contenu du dossier du référentiel secondaire (crx-repository\crx.0000 où 0000 peut être n’importe quels chiffres) dans le dossier du référentiel crx-repository\ et supprimez le dossier du référentiel secondaire.
* Avant de redémarrer tout nœud du cluster, assurez-vous que vous supprimez du nœud principal le fichier /clustered.txt du référentiel.
* Assurez-vous que le nœud principal est démarré en premier, et lorsqu’il est complètement démarré, démarrez les autres nœuds.

### Restauration de l’ensemble de la grappe {#restoring-the-entire-cluster}

1. Arrêtez tous les nœuds de la grappe.
1. Recréez le système physique à partir d’une image système.
1. Appliquez à AEM Forms les correctifs et mises à jour qui ont été appliqués depuis que l’image a été réalisée. Cette information a été mentionnée dans l’étape 1 de la procédure de sauvegarde. AEM Forms doit être récupéré au même niveau de correctif auquel il se trouvait lors de la sauvegarde du système.
1. Restaurez la base de données, le stockage global de documents et les connecteurs.
1. Effectuez les opérations suivantes pour récupérer le référentiel AEM hors ligne :

   >[!NOTE]
   >
   >Si une sauvegarde compressée de crx-repository a été réalisée en ligne, décompressez-la à l’emplacement qui vous convient et suivez le processus de restauration hors ligne.

   1. Sur tous les nœuds de la grappe, supprimez le répertoire partagé, et les répertoires du référentiel, de version et des espaces de travail dans le répertoire clusterNode.
   1. Supprimez tous les fichiers et répertoires dans le répertoire partagé.
   1. Restaurez la sauvegarde du nœud de la grappe (notamment les sous-répertoires) sur un nœud de la grappe.
   1. Copiez tous les fichiers du nœud restauré de la grappe sur tous les autres nœuds de la grappe. Une fois cette opération effectuée, chaque nœud de la grappe contient les mêmes données.
   1. Supprimez le fichier clusterNode/revision.log sur tous les nœuds de la grappe.
   1. Supprimez le fichier .lock sur tous les nœuds de la grappe, le cas échéant.
   1. Supprimez le fichier repository/system.id sur tous les nœuds de la grappe, le cas échéant.
   1. Supprimez les fichiers &amp;ast;&amp;ast;/listener.properties sur tous les nœuds de la grappe, le cas échéant.
   1. Restaurez le fichier repository/cluster_node.id pour les nœuds individuels de la grappe.

>[!NOTE]
>
>Examinez les points suivants :

* Si le nœud en panne était un nœud maître AEM, copiez tout le contenu du dossier du référentiel esclave (au format crx-repository\crx.0000 où 0000 peut être n’importe quel nombre) au dossier du référentiel crx-repository\.
* Avant de redémarrer tout nœud du cluster, assurez-vous que vous supprimez du nœud principal le fichier /clustered.txt du référentiel.
* Assurez-vous que le nœud principal est démarré en premier, et lorsqu’il est complètement démarré, démarrez les autres nœuds.

## Sauvegarde et restauration du nœud d’éditeur de la solution Correspondence Management {#back-up-and-restore-correspondence-management-solution-publish-node}

Le nœud d’éditeur ne dispose pas d’une relation maître-esclave dans un environnement organisé en grappes. Vous pouvez réaliser une sauvegarde de tout nœud d’éditeur en suivant le document [Sauvegarde et restauration](https://docs.adobe.com/docs/fr/crx/current/administering/backup_and_restore.html).

### Récupération d’un seul nœud d’éditeur {#recover-a-single-publisher-node}

1. Arrêtez le nœud qui doit être récupéré et ne réalisez aucune activité de publication avant que le nœud fonctionne à nouveau.
1. Restaurez le nœud de publication à l’aide de [Restauration de la sauvegarde](https://docs.adobe.com/docs/fr/crx/current/administering/backup_and_restore.html#Restoring the Backup).

### Récupération d’une grappe {#recover-a-cluster}

1. Arrêtez la grappe.
1. Restaurez le nœud de publication à l’aide de [Restauration de la sauvegarde](https://docs.adobe.com/docs/fr/crx/current/administering/backup_and_restore.html#Restoring the Backup).
1. Démarrez le nœud maître, puis le nœud esclave de la grappe d’éditeur.
