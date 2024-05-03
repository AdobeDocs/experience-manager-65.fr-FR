---
title: Stratégie de sauvegarde et de restauration dans un environnement organisé en grappes
description: Si votre déploiement d’AEM Forms stocke les données personnalisées supplémentaires dans une base de données différente, vous devez mettre en place une stratégie de sauvegarde pour ces données veillant à ce qu’elles soient synchronisées avec les données AEM Forms.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 98c96349-f253-475f-b646-352269814a38
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '1396'
ht-degree: 100%

---

# Stratégie de sauvegarde et de restauration dans un environnement organisé en grappes {#strategy-for-backup-and-restore-in-a-clustered-environment}

>[!NOTE]
>
>Si votre déploiement d’AEM forms stocke les données personnalisées supplémentaires dans une base de données différente, vous devez mettre en place une stratégie de sauvegarde pour ces données veillant à ce qu’elles soient synchronisées avec les données AEM forms. En outre, l’application doit être conçue de manière à pouvoir faire face à un scénario où les bases de données supplémentaires se désynchronisent. Il est vivement recommandé d’effectuer toute opération de base de données dans le contexte d’une transaction afin de maintenir un état cohérent.

Vous devez sauvegarder les éléments suivants du système de formulaires d’AEM pour garantir une récupération en cas d’erreur :

* la base de données utilisée par les formulaires d’AEM ;
* le répertoire de stockage global de documents qui contient des données de longue durée et d’autres documents persistants ;
* la base de données d’AEM (crx-repositery).

>[!NOTE]
>
>Vous devez sauvegarder toutes les autres données utilisées par la configuration de vos formulaires d’AEM, telles que les polices du client ou de la cliente, les données des connecteurs, etc.

## Sauvegarder un environnement organisé en cluster {#back-up-a-clustered-environment}

Cette rubrique présente les stratégies suivantes pour sauvegarder tout environnement organisé en grappes d’AEM Forms :

* Sauvegarder hors connexion avec temps d’interruption
* Sauvegarder hors connexion sans temps d’interruption (sauvegarde d’un nœud secondaire qui est arrêté)
* Sauvegarder en ligne sans temps d’interruption, mais avec un retard de réponse
* Sauvegarder le fichier de propriétés Bootstrap

### Sauvegarder hors connexion avec temps d’interruption {#offline-backup-with-downtime}

1. Arrêtez l’ensemble du cluster et des services associés (voir [Démarrage et arrêt des services](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services)).
1. Sur n’importe quel nœud, sauvegardez la base de données, le répertoire de stockage global de documents et les connecteurs (voir [Fichiers à sauvegarder et à récupérer](/help/forms/using/admin-help/files-back-recover.md#files-to-back-up-and-recover)).
1. Pour sauvegarder le référentiel AEM hors connexion, procédez comme suit :

   1. Pour chaque nœud du cluster, sauvegardez le fichier contenant l’ID du nœud du cluster.
   1. Sauvegardez tous les fichiers de tout nœud secondaire du cluster, notamment les sous-répertoires.
   1. Sauvegardez l’identifiant du référentiel/système de chaque nœud de la grappe séparément.

   Pour obtenir des instructions détaillées, voir [Sauvegarde et restauration](https://helpx.adobe.com/fr/experience-manager/kb/CRXBackupAndRestoreProcedure.html).

1. Sauvegardez toutes les autres données, telles que les polices du client ou de la cliente.
1. Redémarrez le cluster.

### Sauvegarder hors connexion sans temps d’interruption {#offline-backup-with-no-downtime}

1. Passez en mode de sauvegarde de restauration (voir [Activation des modes de sauvegarde](/help/forms/using/admin-help/backing-aem-forms-data.md#entering-the-backup-modes)).

   Quittez le mode de sauvegarde de restauration après une récupération.

1. Concernant AEM, arrêtez l’un des nœuds secondaires du cluster (voir [Démarrage et arrêt des services](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services)).
1. Sur n’importe quel nœud, sauvegardez la base de données, le répertoire de stockage global de documents et les connecteurs (voir [Fichiers à sauvegarder et à récupérer](/help/forms/using/admin-help/files-back-recover.md#files-to-back-up-and-recover)).
1. Pour sauvegarder le référentiel AEM hors connexion, procédez comme suit :

   1. Pour chaque nœud du cluster, sauvegardez le fichier contenant l’ID du nœud du cluster.
   1. Sauvegardez tous les fichiers de tout nœud secondaire du cluster, notamment les sous-répertoires.
   1. Sauvegardez le fichier repository/system.id de chaque nœud de la grappe séparément.

   Pour obtenir des instructions détaillées, voir [Sauvegarde et restauration](https://helpx.adobe.com/fr/experience-manager/kb/CRXBackupAndRestoreProcedure.html).

1. Sauvegardez toutes les autres données, telles que les polices du client ou de la cliente.
1. Redémarrez le cluster.

### Sauvegarder en ligne sans temps d’interruption, mais avec un retard de réponse {#online-backup-with-no-downtime-but-delay-in-response}

1. Passez en mode de sauvegarde de restauration (voir [Activation des modes de sauvegarde](/help/forms/using/admin-help/backing-aem-forms-data.md#entering-the-backup-modes)).

   Quittez le mode de sauvegarde de restauration après une récupération.

1. Concernant AEM, arrêtez l’un des nœuds secondaires du cluster (voir [Démarrage et arrêt des services](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services)).
1. Sur n’importe quel nœud, sauvegardez la base de données, le répertoire de stockage global de documents et les connecteurs (voir [Fichiers à sauvegarder et à récupérer](/help/forms/using/admin-help/files-back-recover.md#files-to-back-up-and-recover)).
1. Pour sauvegarder le référentiel AEM en ligne, procédez comme suit :

   1. Pour chaque nœud du cluster, sauvegardez le fichier contenant le fichier cluster_node.id.
   1. Sauvegardez le fichier repository/system.id de chaque nœud de la grappe séparément.
   1. Sur n’importe quel nœud secondaire, réalisez une sauvegarde en ligne du référentiel (pour connaître les étapes détaillées, reportez-vous à la section Sauvegarde en ligne).

1. Sauvegardez toutes les autres données, telles que les polices du client ou de la cliente.
1. Redémarrez le cluster.

### Sauvegarder le fichier de propriétés Bootstrap {#back-up-the-bootstrap-properties-file}

Lorsque nous créons un cluster AEM, un fichier de propriétés est créé dans le serveur d’applications pour tous les nœuds secondaires. Nous recommandons de sauvegarder le fichier de propriétés Bootstrap. Le fichier se trouve à l’emplacement suivant sur votre serveur d’applications :

* JBoss® : dans le répertoire BIN.
* WebLogic : dans le répertoire du domaine.
* WebSphere® : dans le répertoire des profils.

Sauvegardez le fichier en cas de reprise après sinistre du nœud secondaire AEM et replacez-le à l’emplacement indiqué sur le serveur d’applications, en cas de restauration.

## Récupération dans un environnement en cluster {#recovery-in-a-clustered-environment}

En cas de panne de l’ensemble du cluster ou d’un seul nœud, restaurez-le à l’aide de la sauvegarde.

Pour la récupération d’un seul nœud, arrêtez le nœud et exécutez la procédure de récupération pour un seul nœud.

En cas de panne de l’ensemble du cluster en raison de problèmes tels que le crash de la base de données, procédez comme suit. La restauration dépend de la méthode de sauvegarde utilisée.

### Restaurer un seul nœud {#restoring-a-single-node}

1. Arrêtez le nœud corrompu.

   >[!NOTE]
   >
   >Si le nœud corrompu est un nœud principal AEM, arrêtez le nœud de l’intégralité du cluster.

1. Recréez le système physique à partir d’une image système.
1. Appliquez les correctifs ou les mises à jour à AEM Forms qui ont été appliqués depuis que l’image a été créée. Ces informations ont été enregistrées pendant la procédure de sauvegarde. AEM Forms doit être restauré au même niveau de correctif que lors de la sauvegarde du système.
1. (*Facultatif*) Si tous les autres nœuds fonctionnent correctement, il est possible que le référentiel AEM soit également corrompu. Dans ce cas, un message de désynchronisation du référentiel s’affiche dans le fichier error.log du référentiel AEM.

   Pour restaurer le référentiel, procédez comme suit.

   >[!NOTE]
   >
   >Si une sauvegarde compressée de crx-repository a été effectuée en ligne, décompressez-la à n’importe quel emplacement et suivez le processus de restauration hors ligne.

   1. Supprimez les répertoires du référentiel, partagé, de version et des espaces de travail dans le répertoire clusterNode du nœud.
   1. Restaurez la sauvegarde du nœud du cluster (y compris les sous-répertoires) sur le nœud.
   1. Supprimez le fichier clusterNode/revision.log sur le nœud.
   1. Supprimez le fichier .lock sur le nœud, le cas échéant.
   1. Supprimez le fichier repository/system.id sur le nœud, le cas échéant.
   1. Supprimez les fichiers &amp;ast;&amp;ast;/listener.properties sur le nœud, le cas échéant.
   1. Restaurez le fichier repository/cluster_node.id pour chaque nœud du cluster.

>[!NOTE]
>
>Tenez compte des points suivants :

* Si le nœud en échec était un nœud principal AEM, copiez tout le contenu du dossier du référentiel secondaire (crx-repository\crx.0000 où 0000 peut être n’importe quels chiffres) dans le dossier du référentiel crx-repository\ et supprimez le dossier du référentiel secondaire.
* Avant de redémarrer tout nœud du cluster, assurez-vous que vous supprimez du nœud principal le fichier /clustered.txt du référentiel.
* Assurez-vous de démarrer le nœud principal en premier et, lorsqu’il a complètement démarré, démarrez les autres nœuds.

### Restaurer l’ensemble du cluster {#restoring-the-entire-cluster}

1. Arrêtez tous les nœuds du cluster.
1. Recréez le système physique à partir d’une image système.
1. Appliquez les correctifs ou les mises à jour à AEM Forms qui ont été appliqués depuis que l’image a été créée. Ces informations ont été enregistrées à l’étape 1 de la procédure de sauvegarde. AEM Forms doit être restauré au même niveau de correctif que lors de la sauvegarde du système.
1. Restaurez la base de données, le répertoire de stockage global de documents et les connecteurs.
1. Procédez comme suit pour récupérer le référentiel AEM hors ligne :

   >[!NOTE]
   >
   >Si une sauvegarde compressée de crx-repository a été effectuée en ligne, décompressez-la à n’importe quel emplacement et suivez le processus de restauration hors ligne.

   1. Sur tous les nœuds du cluster, supprimez les répertoires du référentiel, partagé, de version et des espaces de travail dans le répertoire clusterNode.
   1. Supprimez tous les fichiers et répertoires du répertoire partagé.
   1. Restaurez la sauvegarde du nœud du cluster (y compris les sous-répertoires) sur un nœud du cluster.
   1. Copiez tous les fichiers du nœud du cluster restauré dans tous les autres nœuds du cluster. Une fois cette opération terminée, tous les nœuds du cluster contiennent les mêmes données.
   1. Supprimez le fichier clusterNode/revision.log sur tous les nœuds du cluster.
   1. Supprimez le fichier .lock sur tous les nœuds du cluster, le cas échéant.
   1. Supprimez le fichier repository/system.id tous les nœuds du cluster, le cas échéant.
   1. Supprimez les fichiers &amp;ast;&amp;ast;/listener.properties sur tous les nœuds de la grappe, le cas échéant.
   1. Restaurez le fichier repository/cluster_node.id pour chaque nœud du cluster.

>[!NOTE]
>
>Tenez compte des points suivants :

* Si le nœud en panne était un nœud maître AEM, copiez tout le contenu du dossier du référentiel esclave (au format crx-repository\crx.0000 où 0000 peut être n’importe quel nombre) au dossier du référentiel crx-repository\.
* Avant de redémarrer tout nœud du cluster, assurez-vous que vous supprimez du nœud principal le fichier /clustered.txt du référentiel.
* Assurez-vous de démarrer le nœud principal en premier et, lorsqu’il a complètement démarré, démarrez les autres nœuds.

## Sauvegarde et restauration du nœud d’éditeur de la solution Correspondence Management {#back-up-and-restore-correspondence-management-solution-publish-node}

Le nœud d’éditeur ne dispose pas d’une relation maître-esclave dans un environnement organisé en grappes. Vous pouvez sauvegarder n’importe quel nœud de l’éditeur en suivant la procédure de [Sauvegarde et restauration](https://helpx.adobe.com/fr/experience-manager/kb/CRXBackupAndRestoreProcedure.html).

### Récupérer un seul nœud de l’éditeur {#recover-a-single-publisher-node}

1. Arrêtez le nœud à récupérer et n’effectuez aucune opération de publication tant que le nœud n’a pas redémarré.
1. Restaurez le nœud de publication en suivant la procédure de [Restauration de la sauvegarde](https://helpx.adobe.com/fr/experience-manager/kb/CRXBackupAndRestoreProcedure.html).

### Récupérer un cluster {#recover-a-cluster}

1. Arrêtez le cluster.
1. Restaurez le nœud de publication en suivant la procédure de [Restauration de la sauvegarde](https://helpx.adobe.com/fr/experience-manager/kb/CRXBackupAndRestoreProcedure.html).
1. Démarrez le nœud principal, puis le nœud secondaire du cluster de création.
