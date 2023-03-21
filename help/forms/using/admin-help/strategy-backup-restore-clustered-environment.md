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
source-git-commit: 4fa868f3ae4778d3a637e90b91f7c5909fe5f8aa
workflow-type: tm+mt
source-wordcount: '1416'
ht-degree: 26%

---

# Stratégie de sauvegarde et de restauration dans un environnement organisé en grappes {#strategy-for-backup-and-restore-in-a-clustered-environment}

>[!NOTE]
>
>Si votre déploiement d’AEM forms stocke les données personnalisées supplémentaires dans une base de données différente, vous devez mettre en place une stratégie de sauvegarde pour ces données veillant à ce qu’elles soient synchronisées avec les données AEM forms. En outre, l’application doit être conçue de sorte qu’elle soit suffisamment robuste pour gérer un scénario où les bases de données supplémentaires ne sont pas synchronisées. Il est vivement recommandé d’effectuer toute opération de base de données dans le contexte d’une transaction afin de maintenir un état cohérent.

Vous devez sauvegarder les éléments suivants du système AEM forms pour récupérer d’une erreur :

* Base de données utilisée par AEM forms
* le stockage global de documents qui contient des données de longue durée et d’autres documents persistants ;
* AEM base de données (crx-repository)

>[!NOTE]
>
>Vous devez sauvegarder toutes les autres données utilisées par votre configuration d’AEM forms, telles que les polices du client, les données des connecteurs, etc.

## Sauvegarde d’un environnement organisé en grappes {#back-up-a-clustered-environment}

Cette rubrique présente les stratégies suivantes pour sauvegarder tout environnement organisé en grappes d’AEM Forms :

* Sauvegarde hors ligne avec temps d’interruption
* Sauvegarder hors connexion sans temps d’interruption (sauvegarde d’un nœud secondaire qui est arrêté)
* Sauvegarde en ligne sans temps d’arrêt, mais avec un délai de réponse
* Sauvegarde du fichier de propriétés du Bootstrap

### Sauvegarde hors ligne avec temps d’interruption {#offline-backup-with-downtime}

1. Arrêtez l’ensemble de la grappe et des services associés. (voir [Démarrage et arrêt des services](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services))
1. Sur n’importe quel noeud, sauvegardez la base de données, le répertoire de stockage global de documents et les connecteurs. (voir [Fichiers à sauvegarder et à récupérer](/help/forms/using/admin-help/files-back-recover.md#files-to-back-up-and-recover))
1. Pour sauvegarder AEM référentiel hors ligne, procédez comme suit :

   1. Pour chaque noeud de la grappe, sauvegardez le fichier contenant l’identifiant du noeud de la grappe.
   1. Sauvegardez tous les fichiers de tout nœud secondaire du cluster, notamment les sous-répertoires.
   1. Sauvegardez l’identifiant du référentiel/système de chaque nœud de la grappe séparément.

   Pour obtenir des instructions détaillées, voir [Sauvegarde et restauration](https://helpx.adobe.com/experience-manager/kb/CRXBackupAndRestoreProcedure.html).

1. Sauvegardez toutes les autres données, telles que les polices du client.
1. Redémarrez la grappe.

### Sauvegarde hors ligne sans temps d’arrêt {#offline-backup-with-no-downtime}

1. Passez en mode de sauvegarde restauration. (voir [Passage en mode de sauvegarde](/help/forms/using/admin-help/backing-aem-forms-data.md#entering-the-backup-modes))

   Laissez le mode de sauvegarde restauration après une récupération.

1. Arrêtez l’un des noeuds secondaires de la grappe en ce qui concerne l’AEM. (voir [Démarrage et arrêt des services](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services))
1. Sur n’importe quel noeud, sauvegardez la base de données, le répertoire de stockage global de documents et les connecteurs. (voir [Fichiers à sauvegarder et à récupérer](/help/forms/using/admin-help/files-back-recover.md#files-to-back-up-and-recover))
1. Pour sauvegarder AEM référentiel hors ligne, procédez comme suit :

   1. Pour chaque noeud de la grappe, sauvegardez le fichier contenant l’identifiant du noeud de la grappe.
   1. Sauvegardez tous les fichiers de tout nœud secondaire du cluster, notamment les sous-répertoires.
   1. Sauvegardez le fichier repository/system.id de chaque nœud de la grappe séparément.

   Pour obtenir des instructions détaillées, voir [Sauvegarde et restauration](https://helpx.adobe.com/experience-manager/kb/CRXBackupAndRestoreProcedure.html).

1. Sauvegardez toutes les autres données, telles que les polices du client.
1. Redémarrez la grappe.

### Sauvegarde en ligne sans temps d’arrêt, mais avec un délai de réponse {#online-backup-with-no-downtime-but-delay-in-response}

1. Passez en mode de sauvegarde restauration. (voir [Passage en mode de sauvegarde](/help/forms/using/admin-help/backing-aem-forms-data.md#entering-the-backup-modes))

   Laissez le mode de sauvegarde restauration après une récupération.

1. Arrêtez l’un des noeuds secondaires de la grappe en ce qui concerne l’AEM. (voir [Démarrage et arrêt des services](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services))
1. Sur n’importe quel noeud, sauvegardez la base de données, le répertoire de stockage global de documents et les connecteurs. (voir [Fichiers à sauvegarder et à récupérer](/help/forms/using/admin-help/files-back-recover.md#files-to-back-up-and-recover))
1. Pour sauvegarder AEM référentiel en ligne, procédez comme suit :

   1. Pour chaque noeud de la grappe, sauvegardez le fichier contenant le cluster_node.id.
   1. Sauvegardez le fichier repository/system.id de chaque nœud de la grappe séparément.
   1. Sur n’importe quel nœud secondaire, réalisez une sauvegarde en ligne du référentiel (pour connaître les étapes détaillées, reportez-vous à la section Sauvegarde en ligne).

1. Sauvegardez toutes les autres données, telles que les polices du client.
1. Redémarrez la grappe.

### Sauvegarde du fichier de propriétés du Bootstrap {#back-up-the-bootstrap-properties-file}

Lorsque nous créons un cluster AEM, un fichier de propriétés est créé dans le serveur d’applications pour tous les nœuds secondaires. Il est recommandé de sauvegarder le fichier de propriétés du Bootstrap. Le fichier se trouve à l’emplacement suivant sur votre serveur d’applications :

* JBoss®: dans le répertoire BIN
* WebLogic : dans le répertoire du domaine
* WebSphere®: dans le répertoire des profils

Sauvegardez le fichier pour le scénario de reprise sur sinistre du noeud secondaire AEM et remplacez-le à l’emplacement spécifié sur le serveur d’applications, le cas échéant.

## Récupération dans un environnement organisé en grappes {#recovery-in-a-clustered-environment}

En cas d’échec de l’ensemble de la grappe ou d’un seul noeud, restaurez-le à l’aide de la sauvegarde.

Pour une récupération de noeud unique, arrêtez le noeud unique et exécutez la procédure de récupération de noeud unique.

Si l’ensemble de la grappe échoue en raison d’échecs tels que le blocage de la base de données, procédez comme suit. La restauration dépend de la méthode de sauvegarde utilisée.

### Restauration d’un seul noeud {#restoring-a-single-node}

1. Arrêtez le noeud corrompu.

   >[!NOTE]
   >
   >Si le nœud corrompu est un nœud principal AEM, arrêtez le nœud de l’intégralité du cluster.

1. Recréez le système physique à partir d’une image système.
1. Appliquez des correctifs ou des mises à jour aux formulaires AEM qui ont été appliqués depuis que l’image a été créée. Ces informations ont été enregistrées pendant la procédure de sauvegarde. AEM les formulaires doivent être récupérés au même niveau de correctif que lors de la sauvegarde du système.
1. (*Facultatif*) Si tous les autres noeuds fonctionnent correctement, il est possible que le référentiel AEM soit également corrompu. Dans ce cas, un message de désynchronisation du référentiel s’affiche dans le fichier error.log du référentiel AEM.

   Pour restaurer le référentiel, procédez comme suit.

   >[!NOTE]
   >
   >Si une sauvegarde compressée de référentiel crx a été effectuée en ligne, décompressez-la à n’importe quel emplacement et suivez le processus de restauration hors ligne.

   1. Supprimez les répertoires du référentiel, partagés, de version et des espaces de travail dans le répertoire clusterNode du noeud.
   1. Restaurez la sauvegarde du noeud de la grappe (y compris les sous-répertoires) sur le noeud .
   1. Supprimez le fichier clusterNode/revision.log sur le noeud .
   1. Supprimez le fichier .lock sur le noeud, le cas échéant.
   1. Supprimez le fichier repository/system.id sur le noeud, le cas échéant.
   1. Supprimez les fichiers &amp;ast;&amp;ast;/listener.properties sur le nœud, le cas échéant.
   1. Restaurez repository/cluster_node.id pour chaque noeud de la grappe.

>[!NOTE]
>
>Tenez compte des points suivants :

* Si le nœud en échec était un nœud principal AEM, copiez tout le contenu du dossier du référentiel secondaire (crx-repository\crx.0000 où 0000 peut être n’importe quels chiffres) dans le dossier du référentiel crx-repository\ et supprimez le dossier du référentiel secondaire.
* Avant de redémarrer tout nœud du cluster, assurez-vous que vous supprimez du nœud principal le fichier /clustered.txt du référentiel.
* Assurez-vous que le noeud Principal est démarré en premier et qu’une fois qu’il est démarré, démarrez d’autres noeuds.

### Restauration de l’ensemble de la grappe {#restoring-the-entire-cluster}

1. Arrêtez tous les noeuds de la grappe.
1. Recréez le système physique à partir d’une image système.
1. Appliquez des correctifs ou des mises à jour à AEM formsAEM qui ont été appliqués depuis que l’image a été créée. Ces informations ont été enregistrées à l’étape 1 de la procédure de sauvegarde. AEM les formulaires doivent être récupérés au même niveau de correctif que lors de la sauvegarde du système.
1. Restaurez la base de données, le répertoire de stockage global de documents et les connecteurs.
1. Procédez comme suit pour récupérer le référentiel AEM hors ligne :

   >[!NOTE]
   >
   >Si une sauvegarde compressée de référentiel crx a été effectuée en ligne, décompressez-la à n’importe quel emplacement et suivez le processus de restauration hors ligne.

   1. Sur tous les noeuds de la grappe, supprimez les répertoires du référentiel, partagé, de version et des espaces de travail dans le répertoire clusterNode .
   1. Supprimez tous les fichiers et répertoires du répertoire partagé.
   1. Restaurez la sauvegarde du noeud de la grappe (y compris les sous-répertoires) sur un noeud de la grappe.
   1. Copiez tous les fichiers du noeud de grappe restauré dans tous les autres noeuds de grappe. Une fois cette opération terminée, chaque noeud de grappe contient les mêmes données.
   1. Supprimez le fichier clusterNode/revision.log sur tous les noeuds de la grappe.
   1. Supprimez le fichier .lock sur tous les noeuds de la grappe, le cas échéant.
   1. Supprimez repository/system.id tous les noeuds de la grappe, le cas échéant.
   1. Supprimez les fichiers &amp;ast;&amp;ast;/listener.properties sur tous les nœuds de la grappe, le cas échéant.
   1. Restaurez repository/cluster_node.id pour chaque noeud de la grappe.

>[!NOTE]
>
>Tenez compte des points suivants :

* Si le nœud en panne était un nœud maître AEM, copiez tout le contenu du dossier du référentiel esclave (au format crx-repository\crx.0000 où 0000 peut être n’importe quel nombre) au dossier du référentiel crx-repository\.
* Avant de redémarrer tout nœud du cluster, assurez-vous que vous supprimez du nœud principal le fichier /clustered.txt du référentiel.
* Assurez-vous que le noeud Principal est démarré en premier et qu’une fois qu’il est démarré, démarrez d’autres noeuds.

## Sauvegarde et restauration du nœud d’éditeur de la solution Correspondence Management {#back-up-and-restore-correspondence-management-solution-publish-node}

Le nœud d’éditeur ne dispose pas d’une relation maître-esclave dans un environnement organisé en grappes. Vous pouvez sauvegarder n’importe quel noeud de l’éditeur en procédant comme suit : [Sauvegarde et restauration](https://helpx.adobe.com/experience-manager/kb/CRXBackupAndRestoreProcedure.html).

### Récupération d’un seul noeud d’éditeur {#recover-a-single-publisher-node}

1. Arrêtez le noeud qui doit être récupéré et n’effectuez aucune activité de publication tant que le noeud n’est pas réactivé.
1. Restaurez le noeud de publication à l’aide de [Restauration de la sauvegarde](https://helpx.adobe.com/experience-manager/kb/CRXBackupAndRestoreProcedure.html).

### Récupération d’une grappe {#recover-a-cluster}

1. Arrêtez la grappe.
1. Restaurez le noeud de publication à l’aide de [Restauration de la sauvegarde](https://helpx.adobe.com/experience-manager/kb/CRXBackupAndRestoreProcedure.html).
1. Démarrez le nœud maître, puis le nœud esclave de la grappe d’éditeur.
