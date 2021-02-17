---
title: Récupération des données AEM Forms
seo-title: Récupération des données AEM Forms
description: Ce document décrit les étapes nécessaires à la récupération des données AEM Forms.
seo-description: Ce document décrit les étapes nécessaires à la récupération des données AEM Forms.
uuid: b5735196-5a8d-4358-884f-e9b8d8f4f682
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 4e093114-219b-4018-9530-9002eb665448
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f
workflow-type: tm+mt
source-wordcount: '1174'
ht-degree: 95%

---


# Récupération des données AEM Forms {#recovering-the-aem-forms-data}

Cette section décrit les étapes nécessaires à la récupération des données AEM Forms. Voir également [Remarques spécifiques à la sauvegarde et la récupération](/help/forms/using/admin-help/backup-recovery-strategy-aem-forms.md#special-considerations-for-backup-and-recovery).

>[!NOTE]
>
>La base de données, le répertoire de stockage global de documents, le référentiel AEM et le répertoire racine de stockage de contenu doivent être restaurés sur un ordinateur avec le même nom DNS que le nom d’origine.

AEM Forms doit pouvoir récupérer de manière fiable après les échecs suivants :

**Echec du disque :** la dernière version du support de sauvegarde est nécessaire pour récupérer le contenu de la base de données.

**Données corrompues :** les systèmes de fichiers n’enregistrent pas les transactions passées et les systèmes peuvent remplacer accidentellement des données de processus requises.

**Erreur Utilisateur :** la récupération se limite aux données mises à disposition par la base de données. La récupération est d’autant plus simple que les données ont été enregistrées et sont disponibles.

**Panne de courant, panne du système :** souvent, les API d’un système de fichiers ne sont pas assez robustes ou mal utilisées contre les échecs imprévus du système. Ainsi, si une coupure d’électricité ou une panne système survient, il est nettement plus probable que les contenus des documents stockés dans la base de données soient plus à jour que les contenus stockés dans un système de fichiers.

Si vous utilisez le mode de sauvegarde restauration, vous restez en mode de sauvegarde après la récupération. Si vous vous trouvez en mode de sauvegarde instantané, vous ne restez pas en mode de sauvegarde après la récupération.

Lorsque vous effectuez une restauration à partir d’une sauvegarde sur un nouveau système, les configurations suivantes peuvent être différentes. Les éléments suivants n’affectent pas les récupérations réussies de l’application AEM Forms :

* Adresse IP
* Configuration du système physique (UC, disque et mémoire)
* Emplacement du répertoire de stockage global de documents

>[!NOTE]
>
>la sauvegarde du répertoire racine de stockage de contenu doit être restaurée à l’emplacement de ce répertoire, tel qu’il a été défini durant la configuration de Content Services.

Si un nœud unique d’une grappe multinœud a échoué et si les nœuds restants de la grappe fonctionnent correctement, effectuez une récupération du nœud unique de la grappe.

## Récupération des données AEM Forms {#recover-the-aem-forms-data}

1. Arrêtez les services AEM Forms et le serveur d’applications en cours d’exécution.
1. Au besoin, recréez le système physique à partir d’une image système. Par exemple, cette étape peut ne pas être nécessaire si la raison de la récupération est un serveur de bases de données déficient.
1. Appliquez à AEM Forms les correctifs et mises à jour qui ont été appliqués depuis que l’image a été réalisée. Cette information a été mentionnée dans la procédure de sauvegarde. AEM Forms doit se voir appliquer le même niveau de correctif auquel il se trouvait lors de la sauvegarde du système.
1. (WebSphere Application Server) Si vous récupérez sur une nouvelle instance de WebSphere Application Server, exécutez la commande restoreConfig.bat/sh.
1. Récupérez la base de données AEM forms en procédant tout d’abord à une opération de restauration de la base de données à l’aide des fichiers de sauvegarde, puis en appliquant les journaux de rétablissement des transactions à la base de données récupérée (voir [Base de données AEM Forms](/help/forms/using/admin-help/files-back-recover.md#aem-forms-database)). Pour plus d’informations, voir l’un des articles suivants de la base de connaissances :

   * [Oracle Backup and Recovery for AEM Forms](https://www.adobe.com/go/kb403624)
   * [MySQL Backup and Recovery for AEM Forms](https://www.adobe.com/go/kb403625)
   * [Microsoft SQL Server Backup and Recovery for AEM Forms](https://www.adobe.com/go/kb403623)
   * [DB2 Backup and Recovery for AEM Forms](https://www.adobe.com/go/kb403626)

1. Récupérez le répertoire de stockage global de documents en commençant par supprimer le contenu de ce répertoire sur l’installation existante d’AEM Forms, puis récupérez ce même répertoire depuis le stockage global de documents sauvegardé. Si vous avez changé l’emplacement du répertoire de stockage global de documents, voir [Modification de l’emplacement du stockage global de documents durant la récupération](recovering-aem-forms-data.md#changing-the-gds-location-during-recovery).
1. Renommez le répertoire de sauvegarde du répertoire de stockage global de documents à restaurer comme indiqué dans les exemples suivants :

   >[!NOTE]
   >
   >si le répertoire /restore existe déjà, sauvegardez-le, puis supprimez-le avant de renommer le répertoire /backup qui contient les dernières données.

   * (JBoss) Renommez `[appserver root]/server/'server'/svcnative/DocumentStorage/backup` en :

      `[appserver root]/server/'server'/svcnative/DocumentStorage/restore`.

   * (WebLogic) Renommez `[appserverdomain]/'server'/adobe/AEMformsserver/DocumentStorage/backup` en :

      `[appserverdomain]/'server'/adobe/AEMformsserver/DocumentStorage/restore`.

   * (WebSphere) Renommez `[appserver root]/installedApps/adobe/'server'/DocumentStorage/backup` en :

      `[appserver root]/installedApps/adobe/'server'/DocumentStorage/restore`.

1. Récupérez le répertoire racine de stockage de contenu en commençant par supprimer les contenus de ce répertoire sur l’installation existante d’AEM Forms, puis procédez à la récupération du contenu en suivant la procédure applicable aux environnements autonomes ou organisés en grappe :

   >[!NOTE]
   >
   >la sauvegarde du répertoire racine de stockage de contenu doit être restaurée à l’emplacement de ce répertoire, tel qu’il a été défini durant la configuration de Content Services (obsolète).

   **Autonome :** pendant le processus de récupération, restaurez tous les répertoires sauvegardés. Lorsque ces répertoires sont restaurés, si le répertoire /backup-lucene-indexes existe, renommez-le en /lucene-indexes. Dans le cas contraire, le répertoire lucene-indexes existe déjà et aucune action n’est nécessaire.

   **En grappe :** pendant le processus de récupération, restaurez tous les répertoires sauvegardés. Pour restaurer le répertoire racine d’index, procédez comme suit sur chacun des nœuds de la grappe :

   * Supprimez l’ensemble du contenu du répertoire racine d’index.
   * Si le répertoire /backup-lucene-indexes existe, copiez les contenus du répertoire *racine de stockage de contenu*/backup-lucene-indexes dans le répertoire racine d’index, puis supprimez le répertoire *racine de stockage de contenu*/backup-lucene-indexes.
   * Si le répertoire /lucene-indexes existe, copiez les contenus du répertoire *racine de stockage de contenu*/lucene-indexes dans le répertoire racine d’index.

1. Restaurez/récupérer CRX-repository.

   * **Autonome**

      *Restaurez les instances d’auteur et de publication* : si une catastrophe se produit, vous pouvez restaurer le référentiel à l’état de la dernière sauvegarde en effectuant les étapes décrites dans le document [Sauvegarde et de restauration.](https://docs.adobe.com/docs/en/crx/current/administering/backup_and_restore.html)

      La restauration complète du nœud d’auteur vérifie également la restauration des données Forms Manager et AEM Forms Workspace.

   * **En grappe**

      Pour la restauration dans un environnement organisé en grappes, consultez la section [Stratégie de sauvegarde et de restauration dans un environnement organisé en grappes](/help/forms/using/admin-help/strategy-backup-restore-clustered-environment.md#strategy-for-backup-and-restore-in-a-clustered-environment).

1. Supprimez tous les fichiers temporaires AEM forms créés dans le répertoire java.io.temp ou dans le répertoire temporaire Adobe.
1. Formulaires d&#39;AEM début (voir [Démarrage et arrêt des services](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services))<!-- BROKEN LINK and the application server(s) (see [Maintaining the Application Server](/help/forms/using/admin-help/topics/maintaining-the-application-server.md))-->.

## Modification de l’emplacement du stockage global de documents durant la récupération {#changing-the-gds-location-during-recovery}

Si votre répertoire de stockage global de documents est restauré à un emplacement différent de son emplacement d’origine, exécutez le script LCSetGDS pour définir le répertoire de stockage global de documents sur le nouvel emplacement. Le script se trouve dans le dossier `[aem-forms root]\sdk\misc\Foundation\SetGDSCommandline`. Le script utilise deux paramètres, `defaultGDS` et `newGDS`. Voir le fichier `ReadMe.txt` dans le même dossier pour obtenir des instructions sur la façon d’exécuter le script.

>[!NOTE]
>
>si vous aviez activé le stockage de documents dans la base de données, la modification de l’emplacement du répertoire de stockage global de documents n’est pas nécessaire.

>[!NOTE]
>
>il s’agit là de la seule circonstance vous permettant d’utiliser ce script pour modifier l’emplacement du répertoire de stockage global de documents. Pour modifier l’emplacement du répertoire de stockage global de documents pendant l’exécution d’AEM forms, utilisez Administration Console (voir [Configuration des paramètres généraux d’AEM forms](/help/forms/using/admin-help/configure-general-aem-forms-settings.md#configure-general-aem-forms-settings)).

>[!NOTE]
>
>le déploiement des composants échoue sous Windows si le répertoire de stockage global de documents se situe à la racine du disque (par exemple D:\). Vous devez vous assurer que le répertoire ne se trouve pas en racine, mais bien dans un sous-répertoire du lecteur. Par exemple, il peut s’agir de D:\GDS, au lieu de D:\.

## Récupération du stockage global de documents sur un environnement organisé en grappe  {#recovering-the-gds-to-a-clustered-environment}

Pour modifier l’emplacement du stockage global de documents dans un environnement organisé en grappe, fermez l’intégralité de la grappe, puis exécutez le script LCSetGDS sur un seul nœud de la grappe (voir [Modification de l’emplacement du stockage global de documents durant la récupération](recovering-aem-forms-data.md#changing-the-gds-location-during-recovery)). Démarrez ce nœud uniquement. Une fois ce nœud entièrement démarré, d’autres nœuds de la grappe peuvent l’être en toute sécurité. Ils pointeront alors correctement vers le nouveau stockage global de documents.

>[!NOTE]
>
>si vous ne pouvez pas vous assurer du démarrage complet d’un nœud avant le démarrage des autres nœuds, vous devez exécuter le script LCSetGDS sur chacun des nœuds avant de démarrer la grappe.

