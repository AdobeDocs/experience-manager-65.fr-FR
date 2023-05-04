---
title: Récupération des données AEM Forms
seo-title: Recovering the AEM forms data
description: Ce document décrit les étapes de récupération des données d’AEM forms.
seo-description: This document describes the steps required to recover the AEM forms data.
uuid: b5735196-5a8d-4358-884f-e9b8d8f4f682
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 4e093114-219b-4018-9530-9002eb665448
exl-id: 9e648bab-9284-4fda-abb4-8bd7cd085981
source-git-commit: 3d713021ac410ca2925a282c5dfca98ed4e483ee
workflow-type: tm+mt
source-wordcount: '1122'
ht-degree: 19%

---

# Récupération des données AEM Forms {#recovering-the-aem-forms-data}

Cette section décrit les étapes de récupération des données d’AEM forms. Voir aussi [Remarques spéciales sur la sauvegarde et la récupération](/help/forms/using/admin-help/backup-recovery-strategy-aem-forms.md#special-considerations-for-backup-and-recovery).

>[!NOTE]
>
>La base de données, le répertoire de stockage global de documents, le référentiel AEM et les répertoires racine de stockage de contenu doivent être restaurés sur un ordinateur portant le même nom DNS que l’original.

AEM forms doit récupérer de manière fiable suite aux échecs suivants :

**Echec du disque :** la dernière version du support de sauvegarde est nécessaire pour récupérer le contenu de la base de données.

**Données corrompues :** les systèmes de fichiers n’enregistrent pas les transactions passées et les systèmes peuvent remplacer accidentellement des données de processus requises.

**Erreur Utilisateur :** la récupération se limite aux données mises à disposition par la base de données. La récupération est d’autant plus simple que les données ont été enregistrées et sont disponibles.

**Panne de courant, panne du système :** souvent, les API d’un système de fichiers ne sont pas assez robustes ou mal utilisées contre les échecs imprévus du système. En cas de panne de courant ou de blocage du système, le contenu du document stocké dans la base de données est plus susceptible d’être à jour que le contenu stocké dans un système de fichiers.

Si vous utilisez le mode de sauvegarde restauration, vous êtes toujours en mode de sauvegarde après la récupération. Si vous utilisez le mode de sauvegarde instantané, vous n’êtes pas en mode de sauvegarde après la récupération.

Lors de la restauration d’une sauvegarde vers un nouveau système, les configurations suivantes peuvent être différentes. Les éléments suivants n’affectent pas les récupérations réussies de l’application AEM Forms :

* Adresse IP
* Configuration du système physique (CPU, disque, mémoire)
* Emplacement du répertoire de stockage global de documents

>[!NOTE]
>
>La sauvegarde du répertoire racine de stockage de contenu doit être restaurée à l’emplacement de ce répertoire tel qu’il a été défini lors de la configuration de Content Services.

Si un noeud unique d’une grappe à plusieurs noeuds a échoué et que les noeuds restants de la grappe fonctionnent correctement, effectuez la procédure de récupération à un seul noeud de la grappe.

## Récupération des données d’AEM forms {#recover-the-aem-forms-data}

1. Arrêtez les services d’AEM forms et le serveur d’applications en cas d’exécution.
1. Si nécessaire, recréez le système physique à partir d’une image système. Par exemple, cette étape peut ne pas être nécessaire si la raison de la récupération est un serveur de base de données défectueux.
1. Appliquez des correctifs ou des mises à jour aux formulaires AEM qui ont été appliqués depuis que l’image a été créée. Ces informations ont été enregistrées dans la procédure de sauvegarde. AEM les formulaires doivent être corrigés au même niveau de correctif que lors de la sauvegarde du système.
1. (WebSphere® Application Server) Si vous récupérez une nouvelle instance de WebSphere® Application Server, exécutez la commande restoreConfig.bat/sh.
1. Récupérez la base de données d’AEM forms en exécutant d’abord une opération de restauration de base de données à l’aide des fichiers de sauvegarde de la base de données, puis en appliquant les journaux de rétablissement des transactions à la base de données récupérée. (Voir [AEM base de données forms](/help/forms/using/admin-help/files-back-recover.md#aem-forms-database).) Pour plus d’informations, consultez l’un des articles de la base de connaissances suivants :

   * [DB2](/help/forms/using/admin-help/files-back-recover.md#db2)
   * [Oracle Backup and Recovery for AEM Forms](/help/forms/using/admin-help/files-back-recover.md#oracle)
   * [Microsoft](/help/forms/using/admin-help/files-back-recover.md#sql-server)
   * [MySQL Backup and Recovery for AEM Forms](/help/forms/using/admin-help/files-back-recover.md#mysql)

1. Récupérez le répertoire de stockage global de documents en commençant par supprimer le contenu du répertoire de stockage global de documents sur l’installation existante d’AEM forms, puis en copiant le contenu du répertoire de stockage global de documents à partir du répertoire de stockage global de documents sauvegardé. Si vous avez modifié l’emplacement du répertoire de stockage global de documents, voir [Modification de l’emplacement du répertoire de stockage global de documents pendant la récupération](recovering-aem-forms-data.md#changing-the-gds-location-during-recovery).
1. Renommez le répertoire de sauvegarde du répertoire de stockage global de documents à restaurer, comme illustré dans les exemples suivants :

   >[!NOTE]
   >
   >Si le répertoire /restore existe déjà, sauvegardez-le, puis supprimez-le avant de renommer le répertoire /backup qui contient les dernières données.

   * (JBoss®) Renommer `[appserver root]/server/'server'/svcnative/DocumentStorage/backup` à :

      `[appserver root]/server/'server'/svcnative/DocumentStorage/restore`.

   * (WebLogic) Renommer `[appserverdomain]/'server'/adobe/AEMformsserver/DocumentStorage/backup` en :

      `[appserverdomain]/'server'/adobe/AEMformsserver/DocumentStorage/restore`.

   * (WebSphere®) Renommer `[appserver root]/installedApps/adobe/'server'/DocumentStorage/backup` à :

      `[appserver root]/installedApps/adobe/'server'/DocumentStorage/restore`.

1. Récupérez le répertoire racine de stockage de contenu en supprimant d’abord le contenu du répertoire racine de stockage de contenu sur l’installation existante d’AEM forms, puis en récupérant le contenu en suivant les tâches pour les environnements autonomes ou organisés en grappes :

   >[!NOTE]
   >
   >La sauvegarde du répertoire racine de stockage de contenu doit être restaurée à l’emplacement du répertoire racine de stockage de contenu tel qu’il a été défini lors de la configuration de Content Services (obsolète).

   **Autonome :** pendant le processus de récupération, restaurez tous les répertoires sauvegardés. Lorsque ces répertoires sont restaurés, si le répertoire /backup-lucene-indexes existe, renommez-le /lucene-indexes. Dans le cas contraire, le répertoire lucene-indexes doit déjà exister et aucune action n’est requise.

   **En grappe :** pendant le processus de récupération, restaurez tous les répertoires sauvegardés. Pour restaurer le répertoire racine d’index, procédez comme suit sur chaque noeud de la grappe :

   * Supprimez tout le contenu du répertoire racine d’index.
   * Si le répertoire /backup-lucene-indexes existe, copiez le contenu de *Répertoire racine de stockage de contenu* répertoire /backup-lucene-indexes dans le répertoire racine d’index et supprimez le *Répertoire racine de stockage de contenu* répertoire /backup-lucene-indexes.
   * Si le répertoire /lucene-indexes existe, copiez le contenu de la variable *Répertoire racine de stockage de contenu*/lucene-indexes dans le répertoire racine d’index.

1. Restaurez/récupérez le référentiel CRX.

   * **Autonome**

      *Restaurez les instances d’auteur et de publication* : si une catastrophe se produit, vous pouvez restaurer le référentiel à l’état de la dernière sauvegarde en effectuant les étapes décrites dans le document [Sauvegarde et de restauration.](https://helpx.adobe.com/experience-manager/kb/CRXBackupAndRestoreProcedure.html)

      La restauration complète du noeud Auteur vérifie également la restauration des données Forms Manager et AEM Forms Workspace.

   * **En grappe**

      Pour la restauration dans un environnement organisé en grappes, voir [Stratégie de sauvegarde et de restauration dans un environnement organisé en grappes](/help/forms/using/admin-help/strategy-backup-restore-clustered-environment.md#strategy-for-backup-and-restore-in-a-clustered-environment).

1. Supprimez les fichiers temporaires d’AEM forms créés dans le répertoire java.io.temp ou dans le répertoire temporaire d’Adobe.
1. Démarrez AEM Forms (voir [Démarrer et arrêter des services](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services))<!-- BROKEN LINK and the application server(s) (see [Maintaining the Application Server](/help/forms/using/admin-help/topics/maintaining-the-application-server.md))-->.

## Modification de l’emplacement du répertoire de stockage global de documents pendant la récupération {#changing-the-gds-location-during-recovery}

Si votre répertoire de stockage global de documents est restauré à un emplacement autre qu’il était à l’origine, exécutez le script LCSetGDS pour définir le répertoire de stockage global de documents sur le nouvel emplacement. Le script se trouve dans le dossier `[aem-forms root]\sdk\misc\Foundation\SetGDSCommandline`. Le script utilise deux paramètres, `defaultGDS` et `newGDS`. Voir le fichier `ReadMe.txt` dans le même dossier pour obtenir des instructions sur la façon d’exécuter le script.

>[!NOTE]
>
>Si vous avez activé le stockage de documents dans la base de données, il n’est pas nécessaire de modifier l’emplacement du répertoire de stockage global de documents.

>[!NOTE]
>
>Cette situation est la seule dans laquelle vous devez utiliser ce script pour modifier l’emplacement du répertoire de stockage global de documents. Pour modifier l’emplacement du répertoire de stockage global de documents pendant l’exécution d’AEM forms, utilisez Administration Console. (voir [Configuration des paramètres généraux d’AEM forms](/help/forms/using/admin-help/configure-general-aem-forms-settings.md#configure-general-aem-forms-settings)).

>[!NOTE]
>
>Le déploiement des composants échoue sous Windows si le répertoire de stockage global de documents se trouve à la racine du lecteur (par exemple, D:\). Pour le répertoire de stockage global de documents, vous devez vous assurer que le répertoire ne se trouve pas à la racine du lecteur, mais dans un sous-répertoire. Par exemple, le répertoire doit être D:\GDS and not simply D:\.

## Récupération du répertoire de stockage global de documents dans un environnement en grappe {#recovering-the-gds-to-a-clustered-environment}

Pour modifier l’emplacement du répertoire de stockage global de documents dans un environnement en grappe, arrêtez l’ensemble de la grappe et exécutez le script LCSetGDS sur un seul noeud de la grappe. (Voir [Modification de l’emplacement du répertoire de stockage global de documents pendant la récupération](recovering-aem-forms-data.md#changing-the-gds-location-during-recovery).) Démarrez uniquement ce noeud. Une fois ce noeud entièrement démarré, d’autres noeuds de la grappe peuvent être démarrés en toute sécurité et pointeront correctement vers le nouveau répertoire de stockage global de documents.

>[!NOTE]
>
>Si vous ne pouvez pas vous assurer de démarrer complètement un noeud avant de démarrer d’autres noeuds, vous devez exécuter le script LCSetGDS sur chaque noeud de la grappe avant de le démarrer.
