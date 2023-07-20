---
title: Sauvegarde des données Adobe Experience Manager Forms
description: Ce document décrit les étapes nécessaires à la sauvegarde à chaud ou en ligne de la base de données Adobe Experience Manager (AEM) forms, du répertoire de stockage global de documents et du répertoire racine de stockage de contenu.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 536615a4-ab42-4b72-83b1-fad110b011ee
source-git-commit: 3885cc51f7e821cdb352737336a29f9c4f0c2f41
workflow-type: tm+mt
source-wordcount: '1535'
ht-degree: 10%

---

# Sauvegarde des données Forms Adobe Experience Manager (AEM) {#backing-up-the-aem-forms-data}

<!-- back up is two words when used as a verb; backup is one word when used as an adjective or noun. -->

Cette section décrit les étapes nécessaires pour effectuer une sauvegarde à chaud ou en ligne de la base de données AEM Forms, du répertoire de stockage global de documents et du répertoire racine de stockage de contenu.

Une fois qu’AEM Forms est installé et déployé dans les zones de production, l’administrateur de base de données doit effectuer une sauvegarde initiale complète ou à froid de la base de données. La base de données doit être arrêtée pour cette sauvegarde. Ensuite, les sauvegardes différentielles ou incrémentielles (ou à chaud) de la base de données doivent être effectuées régulièrement.

Pour garantir la réussite de la sauvegarde et de la récupération, une sauvegarde de l’image système doit toujours être disponible. Ensuite, si une perte se produit, vous pouvez récupérer l’ensemble de votre environnement à un état cohérent.

La sauvegarde de la base de données en même temps que les sauvegardes du répertoire de stockage global de documents, du référentiel AEM et du répertoire racine de stockage de contenu permet de maintenir la synchronisation de ces systèmes si une récupération est nécessaire.

La procédure de sauvegarde décrite dans cette section nécessite que vous passiez en mode de sauvegarde sécurisé avant de sauvegarder la base de données AEM Forms, le référentiel AEM, le répertoire de stockage global de documents et les répertoires racine de stockage de contenu. Une fois la sauvegarde terminée, vous devez quitter le mode de sauvegarde sécurisé. Le mode de sauvegarde sécurisé est utilisé pour marquer les documents de longue durée et persistants qui résident dans le répertoire de stockage global de documents. Ce mode garantit que le mécanisme de nettoyage de fichier automatisé (le collecteur de fichiers) ne supprime pas les fichiers expirés tant que le mode de sauvegarde sécurisé n’est pas libéré. Il est nécessaire de conserver une sauvegarde du répertoire de stockage global de documents en synchronisation avec une sauvegarde de base de données.

La fréquence de sauvegarde de l’emplacement du répertoire de stockage global de documents dépend de l’utilisation d’AEM Forms et des fenêtres de sauvegarde disponibles. La fenêtre de sauvegarde peut être affectée par les processus de longue durée, car ils peuvent s’exécuter pendant plusieurs jours. Si vous modifiez, ajoutez et supprimez continuellement des fichiers dans ce répertoire, sauvegardez plus souvent l’emplacement du répertoire de stockage global de documents.

Si la base de données s’exécute en mode de journalisation, comme décrit dans la section précédente, les journaux de la base de données doivent également être sauvegardés fréquemment afin de pouvoir être utilisés pour restaurer la base de données en cas d’échec du média.

>[!NOTE]
>
>Les fichiers non référencés peuvent persister dans le répertoire de stockage global de documents après le processus de récupération. Il s’agit actuellement d’une limitation connue.

## Sauvegarde de la base de données, du répertoire de stockage global de documents, du référentiel AEM et des répertoires racine de stockage de contenu {#back-up-the-database-gds-aem-repository-and-content-storage-root-directories}

Vous devez mettre AEM Forms en mode de sauvegarde sécurisé (instantané) ou de sauvegarde restauration (couverture continue). Avant de configurer AEM Forms pour qu’il passe en mode de sauvegarde, vérifiez les points suivants :

* Vérifiez la version du système et enregistrez les correctifs ou mises à jour appliqués depuis la dernière sauvegarde complète de l’image système effectuée.
* Si vous utilisez des sauvegardes en mode restauration ou instantané, assurez-vous que votre base de données est configurée avec les paramètres de journal corrects pour permettre les sauvegardes à chaud de la base de données. (Voir [Base de données AEM Forms](/help/forms/using/admin-help/files-back-recover.md#aem-forms-database).)

En outre, respectez les instructions suivantes pour le processus de sauvegarde/restauration.

* Sauvegardez le répertoire de stockage global de documents à l’aide d’un système d’exploitation disponible ou d’un utilitaire de sauvegarde tiers. (Voir [Emplacement du répertoire de stockage global de documents](/help/forms/using/admin-help/files-back-recover.md#gds-location).)
* (Facultatif) Sauvegardez le répertoire racine de stockage de contenu à l’aide d’un système d’exploitation disponible ou d’une sauvegarde et d’un utilitaire tiers. (Voir [Emplacement racine de stockage de contenu (environnement autonome)](/help/forms/using/admin-help/files-back-recover.md#content-storage-root-location-stand-alone-environment) ou [Emplacement racine de stockage de contenu (environnement en grappe)](/help/forms/using/admin-help/files-back-recover.md#content-storage-root-location-clustered-environment).)
* Sauvegardez les instances d’auteur et de publication (sauvegarde crx-repository).

  Pour sauvegarder l’environnement de la solution Correspondence Management, effectuez les étapes sur les instances de création et de publication, comme décrit dans la section [Sauvegarde et restauration](/help/sites-administering/backup-and-restore.md).

  Tenez compte des points suivants lors de la sauvegarde des instances d’auteur et de publication :

   * Assurez-vous que la sauvegarde des instances de création et de publication est synchronisée pour qu’elle démarre en même temps. Bien que vous puissiez continuer à utiliser les instances de création et de publication pendant la sauvegarde, il est recommandé de ne pas publier de ressource pendant la sauvegarde afin d’éviter toute modification non capturée. Attendez que la sauvegarde des instances d’auteur et de publication se termine avant de publier de nouvelles ressources.
   * La sauvegarde complète du noeud Auteur comprend la sauvegarde des données Forms Manager et AEM Forms Workspace.
   * Les développeurs de Workbench peuvent continuer à travailler sur leurs processus localement. Ils ne doivent pas déployer de nouveaux processus pendant la phase de sauvegarde.
   * La décision concernant la durée de chaque session de sauvegarde (pour le mode de sauvegarde restauration) doit être basée sur la durée totale de sauvegarde de toutes les données dans AEM Forms (base de données, stockage global de documents, référentiel d’AEM et de toutes les autres données personnalisées supplémentaires).

Sauvegardez la base de données AEM Forms, y compris les logs de transaction. Voir [Base de données AEM Forms](/help/forms/using/admin-help/files-back-recover.md#aem-forms-database).

Pour plus d’informations, consultez l’article correspondant à votre base de données dans la base de connaissances :
<!-- The four URLs below are all 404s; checked July 19, 2023 -->
* [Sauvegarde et récupération des Oracles pour AEM Forms](https://www.adobe.com/go/kb403624)
* [Sauvegarde et récupération MySQL pour AEM Forms](https://www.adobe.com/go/kb403625)
* [Sauvegarde et récupération de Microsoft® SQL Server pour AEM Forms](https://www.adobe.com/go/kb403623)
* [Sauvegarde et récupération de DB2® pour AEM Forms](https://www.adobe.com/go/kb403626)

Ces articles fournissent des conseils sur les fonctions de base de données pour la sauvegarde et la récupération des données. Ils ne sont pas conçus comme des guides techniques complets de la fonctionnalité de sauvegarde et de récupération de base de données d’un fournisseur spécifique. Ils décrivent les commandes nécessaires à la création d’une stratégie de sauvegarde de base de données fiable pour les données de votre application AEM Forms.

>[!NOTE]
>
>La sauvegarde de la base de données doit être terminée avant de commencer la sauvegarde du répertoire de stockage global de documents. Si la sauvegarde de la base de données n’est pas terminée, vos données ne sont pas synchronisées.

### Passage en mode de sauvegarde {#entering-the-backup-modes}

Vous pouvez utiliser Administration Console, la commande LCBackupMode ou l’API disponible avec l’installation d’AEM Forms pour passer en mode de sauvegarde. Pour le sauvegarde restauration (couverture continue), l’option Administration Console n’est pas disponible ; vous devez utiliser l’option de ligne de commande ou l’API. <!-- Fix broken link For information about using the API to enter and leave backup modes, see AEM Forms API Reference on Help and Tutorials page. -->

>[!NOTE]
>
>Si vous avez configuré SSL sur le serveur Forms, vous ne pouvez pas placer le serveur Forms en mode de sauvegarde à l’aide du script LCBackupMode.CMD.

**Utilisation d’Administration Console pour passer en mode de sauvegarde sécurisé**

1. Connectez-vous à Administration Console.
1. Cliquez sur Paramètres > Paramètres de Core System > Utilitaires de sauvegarde.
1. Sélectionnez Fonctionner en mode de sauvegarde sécurisé et cliquez sur OK.

   Cette méthode passe AEM Forms en mode de sauvegarde indéfiniment (pas de délai d’expiration) et passe en mode instantané plutôt qu’en mode de sauvegarde restauration.

**Utilisation de l’option de ligne de commande pour passer en mode de sauvegarde sécurisé**

Vous pouvez utiliser l’interface de ligne de commande `LCBackupMode` pour mettre AEM Forms en mode de sauvegarde sécurisé.

1. Définissez ADOBE_LIVECYCLE et lancez le serveur d’applications.
1. Accédez au dossier `*[aem-forms root]*/sdk/misc/Foundation/BackupRestoreCommandline`.
1. Modifiez le script `LCBackupMode.cmd` ou `LCBackupMode.sh` de façon à indiquer les valeurs par défaut correspondant à votre système d’exploitation.
1. Dans l’invite de commande, exécutez la commande suivante sur une seule ligne :

   * (Windows) `LCBackupMode.cmd enter [-Host=`*hostname* `] [-port=`*portnumber* `] [-user=`*username* `] [-password=`*password* `] [-label=`*labelname* `] [-timeout=`*seconds* `]`
   * (Linux®, UNIX®) `LCBackupMode.sh enter [-host=`*hostname* `] [-port=`*portnumber* `] [-user=`*username* `] [-password=`*password* `] [-label=`*labelname* `]`

   Dans les commandes précédentes, les emplacements réservés peuvent être définis comme suit :

   `Host` est le nom de l’hôte sur lequel AEM Forms est exécuté.

   `port` est le port WebServices du serveur d’applications sur lequel AEM Forms est exécuté.

   `user` est le nom d’utilisateur de l’administrateur AEM Forms.

   `password` est le mot de passe de l’administrateur AEM Forms.

   `label` est le libellé de texte de cette sauvegarde (il peut s’agir de n’importe quelle chaîne).

   `timeout` est le nombre de secondes après lequel le mode de sauvegarde est quitté automatiquement. Il peut être de 0 à 10 080. S’il s’agit de 0, qui est la valeur par défaut, le mode de sauvegarde n’expire jamais.

   Pour plus d’informations sur l’interface de ligne de commande du mode de sauvegarde, voir le fichier Lisez-moi dans le répertoire BackupRestoreCommandline .

### Quitter les modes de sauvegarde {#leaving-backup-modes}

Vous pouvez utiliser Administration Console ou l’option de ligne de commande pour quitter les modes de sauvegarde.

**Quitter le mode de sauvegarde sécurisé (mode instantané)**

Pour utiliser Administration Console afin de sortir AEM Forms du mode de sauvegarde sécurisé (mode instantané), effectuez les tâches suivantes.

1. Connectez-vous à Administration Console.
1. Cliquez sur Paramètres > Paramètres de Core System > Utilitaires de sauvegarde.
1. Désélectionnez Fonctionner en mode de sauvegarde sécurisé et cliquez sur OK.

**Quitter tous les modes de sauvegarde**

Vous pouvez utiliser l’interface de ligne de commande pour sortir AEM Forms du mode de sauvegarde sécurisé (mode instantané) ou pour mettre fin à la session du mode de sauvegarde actuel (mode de sauvegarde restauration). Vous ne pouvez pas utiliser Administration Console pour quitter le mode de sauvegarde restauration. En mode de sauvegarde restauration, les commandes Utilitaires de sauvegarde d’ Administration Console sont désactivées. Utilisez l’appel API ou la commande LCBackupMode .

1. Accédez au dossier `*[aem-forms root]*/sdk/misc/Foundation/BackupRestoreCommandline`.
1. Modifiez le script `LCBackupMode.cmd` ou `LCBackupMode.sh` de façon à indiquer les valeurs par défaut correspondant à votre système d’exploitation.

   >[!NOTE]
   >
   >Vous devez définir le répertoire JAVA_HOME comme décrit dans le chapitre correspondant pour votre serveur d’applications dans la section [Préparation à l’installation d’AEM Forms](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_63_fr)*.*

1. Exécutez la commande suivante sur une seule ligne :

   * (Windows) `LCBackupMode.cmd leaveContinuousCoverage [-Host=`*nom_hôte* `] [-port=`*numéro_port* `] [-user=`*nom_utilisateur* `] [-password=`*mot_de_passe* `]`
   * (Linux®, UNIX®) `LCBackupMode.sh leaveContinuousCoverage [-Host=`*hostname* `] [-port=`*portnumber* `] [-user=`*username* `] [-password=`*password* `]`

     Dans les commandes précédentes, les emplacements réservés peuvent être définis comme suit :

     `Host` est le nom de l’hôte sur lequel AEM Forms est exécuté.

     `port` est le port sur lequel AEM Forms s’exécute sur le serveur d’applications.

     `user` est le nom d’utilisateur de l’administrateur AEM Forms.

     `password` est le mot de passe de l’administrateur AEM Forms.

     `leaveContinuousCoverage` : cette option permet de désactiver totalement le mode de sauvegarde restauration.

   >[!NOTE]
   >
   >Pendant que ce mode de sauvegarde est désactivé, la couverture continue ne peut pas être rétablie. Les modifications effectuées pendant cette période ne sont pas protégées.

   >[!NOTE]
   >
   >Si vous avez activé le stockage de documents dans la base de données, le mode de sauvegarde instantané et le mode de sauvegarde restauration ne sont pas applicables.

   Pour plus d’informations sur l’interface de ligne de commande du mode de sauvegarde, consultez le fichier Lisez-moi dans le répertoire BackupRestoreCommandline .
