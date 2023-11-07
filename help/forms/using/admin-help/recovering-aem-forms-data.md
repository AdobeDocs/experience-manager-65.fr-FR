---
title: Récupération des données AEM Forms
seo-title: Recovering the AEM forms data
description: Ce document décrit les étapes nécessaires à la récupération des données AEM Forms.
seo-description: This document describes the steps required to recover the AEM forms data.
uuid: b5735196-5a8d-4358-884f-e9b8d8f4f682
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 4e093114-219b-4018-9530-9002eb665448
exl-id: 9e648bab-9284-4fda-abb4-8bd7cd085981
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '1121'
ht-degree: 97%

---

# Récupération des données AEM Forms {#recovering-the-aem-forms-data}

Cette section décrit les étapes nécessaires à la récupération des données AEM Forms. Voir également [Remarques spécifiques à la sauvegarde et la récupération](/help/forms/using/admin-help/backup-recovery-strategy-aem-forms.md#special-considerations-for-backup-and-recovery).

>[!NOTE]
>
>La base de données, le répertoire de stockage global de documents, le référentiel AEM et le répertoire racine de stockage de contenu doivent être restaurés sur un ordinateur avec le même nom DNS que le nom d’origine.

AEM forms doit pouvoir récupérer de manière fiable après les échecs suivants :

**Echec du disque :** la dernière version du support de sauvegarde est nécessaire pour récupérer le contenu de la base de données.

**Données corrompues :** les systèmes de fichiers n’enregistrent pas les transactions passées et les systèmes peuvent remplacer accidentellement des données de processus requises.

**Erreur Utilisateur :** la récupération se limite aux données mises à disposition par la base de données. La récupération est d’autant plus simple que les données ont été enregistrées et sont disponibles.

**Panne de courant, panne du système :** souvent, les API d’un système de fichiers ne sont pas assez robustes ou mal utilisées contre les échecs imprévus du système. Ainsi, si une coupure d’électricité ou une panne système survient, il est nettement plus probable que les contenus des documents stockés dans la base de données soient plus à jour que les contenus stockés dans un système de fichiers.

Si vous utilisez le mode de sauvegarde avec remplacement de données, vous restez en mode de sauvegarde après la récupération. Si vous vous trouvez en mode de sauvegarde instantané, vous ne restez pas en mode de sauvegarde après la récupération.

Lorsque vous effectuez une restauration à partir d’une sauvegarde sur un nouveau système, les configurations suivantes peuvent être différentes. Les éléments suivants n’affectent pas les récupérations réussies de l’application AEM Forms :

* Adresse IP
* Configuration du système physique (UC, disque, mémoire)
* Emplacement du répertoire de stockage global de documents

>[!NOTE]
>
>La sauvegarde du répertoire racine de stockage de contenu doit être restaurée à l’emplacement de ce répertoire, tel qu’il a été défini durant la configuration de Content Services.

Si un nœud unique d’un cluster multinœud a échoué et si les nœuds restants du cluster fonctionnent correctement, effectuez une récupération du nœud unique du cluster.

## Récuper les données AEM Forms {#recover-the-aem-forms-data}

1. Arrêtez les services AEM Forms et le serveur d’applications en cours d’exécution.
1. Au besoin, recréez le système physique à partir d’une image système. Par exemple, cette étape peut ne pas être nécessaire si la raison de la récupération est un serveur de bases de données déficient.
1. Appliquez les correctifs ou les mises à jour à AEM Forms qui ont été appliqués depuis que l’image a été créée. Cette information a été mentionnée dans la procédure de sauvegarde. AEM Forms doit se voir appliquer le même niveau de correctif auquel il se trouvait lors de la sauvegarde du système.
1. (WebSphere® Application Server) Si vous récupérez une nouvelle instance de WebSphere® Application Server, exécutez la commande restoreConfig.bat/sh.
1. Récupérez la base de données AEM forms en procédant tout d’abord à une opération de restauration de la base de données à l’aide des fichiers de sauvegarde, puis en appliquant les journaux de rétablissement des transactions à la base de données récupérée. (Voir [Base de données AEM Forms](/help/forms/using/admin-help/files-back-recover.md#aem-forms-database).) Pour plus d’informations, voir l’un des articles suivants de la base de connaissances :

   * [DB2](/help/forms/using/admin-help/files-back-recover.md#db2)
   * [Sauvegarde et récupération d’Oracle pour AEM Forms](/help/forms/using/admin-help/files-back-recover.md#oracle)
   * [Microsoft](/help/forms/using/admin-help/files-back-recover.md#sql-server)
   * [MySQL - Sauvegarde et récupération pour AEM Forms](/help/forms/using/admin-help/files-back-recover.md#mysql)

1. Récupérez le répertoire de stockage global de documents en commençant par supprimer le contenu de ce répertoire sur l’installation existante d’AEM Forms, puis copiez le contenu de ce même répertoire depuis le stockage global de documents sauvegardé. Si vous avez changé l’emplacement du répertoire de stockage global de documents, voir [Modification de l’emplacement du stockage global de documents durant la récupération](recovering-aem-forms-data.md#changing-the-gds-location-during-recovery).
1. Renommez le répertoire de sauvegarde du répertoire de stockage global de documents à restaurer comme indiqué dans les exemples suivants :

   >[!NOTE]
   >
   >Si le répertoire / restore existe déjà, sauvegardez-le, puis supprimez-le avant de renommer le répertoire / backup qui contient les dernières données.

   * (JBoss®) Renommez `[appserver root]/server/'server'/svcnative/DocumentStorage/backup` en :

     `[appserver root]/server/'server'/svcnative/DocumentStorage/restore`.

   * (WebLogic) Renommer `[appserverdomain]/'server'/adobe/AEMformsserver/DocumentStorage/backup` en :

     `[appserverdomain]/'server'/adobe/AEMformsserver/DocumentStorage/restore`.

   * (WebSphere®) Renommez `[appserver root]/installedApps/adobe/'server'/DocumentStorage/backup` en :

     `[appserver root]/installedApps/adobe/'server'/DocumentStorage/restore`.

1. Pour récupérer le répertoire racine de stockage de contenu, supprimez le contenu du répertoire racine de stockage de contenu sur l’installation existante d’AEM Forms, puis récupérez le contenu en suivant les tâches pour les environnements autonomes ou organisés en cluster :

   >[!NOTE]
   >
   >La sauvegarde du répertoire racine de stockage de contenu doit être restaurée à l’emplacement du répertoire racine de stockage de contenu tel qu’il a été défini lors de la configuration de Content Services (obsolète).

   **Autonome :** pendant le processus de récupération, restaurez tous les répertoires sauvegardés. Lorsque ces répertoires sont restaurés, si le répertoire /backup-lucene-indexes existe, renommez-le /lucene-indexes. Si le répertoire lucene-indexes existe déjà, aucune action n’est requise.

   **En grappe :** pendant le processus de récupération, restaurez tous les répertoires sauvegardés. Pour restaurer le répertoire racine d’index, procédez comme suit sur chaque nœud du cluster :

   * Supprimez tout le contenu du répertoire racine d’index.
   * Si le répertoire /backup-lucene-indexes existe, copiez le contenu du *répertoire racine de stockage de contenu* /backup-lucene-indexes dans le répertoire racine d’index et supprimez le *répertoire racine de stockage de contenu* /backup-lucene-indexes.
   * Si le répertoire /lucene-indexes existe, copiez le contenu du *répertoire racine de stockage de contenu* /lucene-indexes dans le répertoire racine d’index.

1. Restaurez/récupérez le référentiel CRX.

   * **Autonome**

     *Restaurez les instances d’auteur et de publication* : si une catastrophe se produit, vous pouvez restaurer le référentiel à l’état de la dernière sauvegarde en effectuant les étapes décrites dans le document [Sauvegarde et de restauration.](https://helpx.adobe.com/fr/experience-manager/kb/CRXBackupAndRestoreProcedure.html)

     La restauration complète du nœud de création vérifie également la restauration des données du gestionnaire Forms et de l’espace de travail AEM Forms.

   * **En cluster**

     Pour la restauration dans un environnement en cluster, voir [Stratégie de sauvegarde et de restauration dans un environnement en cluster](/help/forms/using/admin-help/strategy-backup-restore-clustered-environment.md#strategy-for-backup-and-restore-in-a-clustered-environment).

1. Supprimez les fichiers temporaires d’AEM forms créés dans le répertoire java.io.temp ou dans le répertoire temporaire d’Adobe.
1. Démarrez AEM Forms (voir [Démarrer et arrêter des services](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services))<!-- BROKEN LINK and the application server(s) (see [Maintaining the Application Server](/help/forms/using/admin-help/topics/maintaining-the-application-server.md))-->.

## Modification de l’emplacement du répertoire de stockage global de documents pendant la récupération {#changing-the-gds-location-during-recovery}

Si votre répertoire de stockage global de documents est restauré à un emplacement différent de celui d’origine, exécutez le script LCSetGDS pour définir le répertoire de stockage global de documents sur le nouvel emplacement. Le script se trouve dans le dossier `[aem-forms root]\sdk\misc\Foundation\SetGDSCommandline`. Le script utilise deux paramètres, `defaultGDS` et `newGDS`. Voir le fichier `ReadMe.txt` dans le même dossier pour obtenir des instructions sur la façon d’exécuter le script.

>[!NOTE]
>
>Si vous avez activé le stockage de documents dans la base de données, il n’est pas nécessaire de modifier l’emplacement du répertoire de stockage global de documents.

>[!NOTE]
>
>Il s’agit de la seule situation dans laquelle vous devez utiliser ce script pour modifier l’emplacement du répertoire de stockage global de documents. Pour modifier l’emplacement du répertoire de stockage global de documents pendant l’exécution d’AEM Forms, utilisez la console d’administration. (voir [Configuration des paramètres généraux d’AEM forms](/help/forms/using/admin-help/configure-general-aem-forms-settings.md#configure-general-aem-forms-settings)).

>[!NOTE]
>
>Le déploiement des composants échoue sous Windows si le répertoire de stockage global de documents se trouve à la racine du disque (par exemple, D:\). Pour le répertoire de stockage global de documents, vous devez vous assurer que le répertoire ne se trouve pas à la racine du lecteur, mais dans un sous-répertoire. Par exemple, le répertoire doit être D:\GDS et pas uniquement D:\.

## Récupération du répertoire de stockage global de documents dans un environnement en cluster {#recovering-the-gds-to-a-clustered-environment}

Pour modifier l’emplacement du répertoire de stockage global de documents dans un environnement en cluster, arrêtez l’ensemble du cluster et exécutez le script LCSetGDS sur un seul nœud du cluster. (Voir [Modification de l’emplacement du répertoire de stockage global de documents pendant la récupération](recovering-aem-forms-data.md#changing-the-gds-location-during-recovery).) Démarrez uniquement ce nœud. Une fois que ce nœud a complètement démarré, vous pouvez démarrer d’autres nœuds du cluster en toute sécurité. Ils pointeront correctement vers le nouveau répertoire de stockage global de documents.

>[!NOTE]
>
>Si vous ne pouvez pas garantir le démarrage complet d’un nœud avant de démarrer d’autres nœuds, exécutez le script LCSetGDS sur chaque nœud du cluster avant de le démarrer.
