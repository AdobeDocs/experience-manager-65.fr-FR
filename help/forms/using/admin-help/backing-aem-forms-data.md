---
title: Sauvegarde des données Adobe Experience Manager Forms
description: Ce document décrit les étapes nécessaires à la réalisation d’une sauvegarde complète, à chaud ou en ligne, de la base de données Adobe Experience Manager (AEM) Forms, de même que du répertoire de stockage global de documents et des répertoires racine de stockage de contenu.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 536615a4-ab42-4b72-83b1-fad110b011ee
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: ht
source-wordcount: '1527'
ht-degree: 100%

---

# Sauvegarde des données Adobe Experience Manager (AEM) Forms {#backing-up-the-aem-forms-data}

<!-- back up is two words when used as a verb; backup is one word when used as an adjective or noun. -->

Cette section décrit les étapes nécessaires à la réalisation d’une sauvegarde complète, à chaud ou en ligne, de la base de données AEM Forms, de même que du répertoire de stockage global de documents et des répertoires racine de stockage de contenu.

Une fois AEM Forms installé et déployé dans les zones de production, l’administrateur ou l’administratrice de la base de données doit procéder à une première sauvegarde complète (ou à froid) de la base de données. Pour cela, la base de données doit être fermée. Par la suite, il ou elle devra effectuer régulièrement des sauvegardes incrémentielles (ou à chaud) de la base de données.

Pour une sauvegarde et une restauration réussies, une sauvegarde de l’image système doit toujours être disponible. Ainsi, si une perte de données se produit, vous pouvez récupérer la totalité de votre environnement dans un état cohérent.

Le fait d’effectuer la sauvegarde de la base de données en même temps que les sauvegardes du répertoire global de documents, du référentiel AEM et du répertoire racine de contenu de stockage aide à maintenir ces systèmes synchronisés si une récupération devait intervenir.

La procédure de sauvegarde décrite dans cette section nécessite d’être en mode de sauvegarde sécurisé avant de sauvegarder la base de données AEM Forms, le référentiel AEM, le répertoire de stockage global de documents et les répertoires racine de stockage de contenu. Une fois la sauvegarde terminée, vous devez quitter le mode de sauvegarde sécurisé. Le mode de sauvegarde sécurisé est utilisé pour marquer les documents de longue durée et persistants qui résident dans le répertoire de stockage global de documents. Ce mode garantit que le mécanisme de nettoyage de fichiers automatique (le collecteur de fichiers) ne supprime pas les fichiers ayant expiré jusqu’à l’activation du mode de sauvegarde sécurisé. La sauvegarde d’un répertoire de stockage global de documents doit rester synchronisée avec la sauvegarde d’une base de données.

La fréquence de sauvegarde de l’emplacement du répertoire de stockage global de documents dépend du mode d’utilisation d’AEM Forms et des fenêtres de sauvegarde disponibles. La fenêtre de sauvegarde peut être affectée par les processus de longue durée, qui peuvent parfois s’exécuter pendant plusieurs jours. Si vous modifiez, ajoutez et supprimez en permanence des fichiers dans le répertoire de stockage global de documents, sauvegardez plus souvent cet emplacement.

Si la base de données s’exécute dans un mode de consignation tel que décrit précédemment, les journaux de la base de données doivent également être sauvegardés régulièrement, afin d’en permettre l’utilisation pour restaurer la base de données en cas d’échec du support.

>[!NOTE]
>
>Les fichiers qui ne sont pas référencés peuvent rester dans le répertoire de stockage global de documents après la récupération. Il s’agit d’une limitation connue actuelle.

## Sauvegarde de la base de données, du répertoire de stockage global de documents, du référentiel AEM et des répertoires racine de stockage de contenu. {#back-up-the-database-gds-aem-repository-and-content-storage-root-directories}

Vous pouvez mettre AEM Forms en mode de sauvegarde sécurisé (instantané) ou en mode de sauvegarde restauration (couverture continue). Avant de définir AEM Forms sur l’un de ces modes de sauvegarde, assurez-vous que les conditions suivantes sont remplies :

* Vérifiez la version du système et notez les correctifs et mises à jour appliqués depuis la dernière sauvegarde d’image système complète.
* Si vous utilisez des sauvegardes en mode instantané ou de type restauration, vérifiez que votre base de données est configurée avec des paramètres de consignation corrects pour autoriser les sauvegardes à chaud de la base de données. (Voir [Base de données AEM Forms](/help/forms/using/admin-help/files-back-recover.md#aem-forms-database).)

Outre ces vérifications, observez les recommandations ci-dessous relatives au processus de sauvegarde/restauration.

* Sauvegardez le répertoire de stockage global de documents en utilisant un système d’exploitation disponible ou un utilitaire de sauvegarde tiers. (Voir [Emplacement du répertoire de stockage global de documents](/help/forms/using/admin-help/files-back-recover.md#gds-location)).
* (Facultatif) Sauvegardez le répertoire racine de stockage de contenu en utilisant un système d’exploitation disponible ou un utilitaire de sauvegarde tiers. (Voir [Emplacement racine de stockage de contenu (environnement autonome)](/help/forms/using/admin-help/files-back-recover.md#content-storage-root-location-stand-alone-environment) ou [Emplacement racine de stockage de contenu (environnement en cluster)](/help/forms/using/admin-help/files-back-recover.md#content-storage-root-location-clustered-environment)).
* Sauvegardez les instances de création et de publication (sauvegarde de crx-repository).

  Pour sauvegarder l’environnement de la solution Correspondence Management, effectuez la procédure relative aux instances de création et de publication décrite dans le document [Sauvegarde et restauration](/help/sites-administering/backup-and-restore.md).

  Considérez les points suivants lors de la sauvegarde des instances de création et de publication :

   * Assurez-vous que la sauvegarde des instances de création et de publication est synchronisée pour démarrer simultanément. Bien que vous puissiez continuer à utiliser les instances de création et de publication lorsque la sauvegarde est en cours, il est recommandé de ne pas publier de ressource pendant la sauvegarde afin d’éviter des modifications non enregistrées. Patientez jusqu’à ce que la sauvegarde des instances de création et de publication soit terminée avant de publier de nouvelles ressources.
   * La sauvegarde complète du nœud Création inclut la sauvegarde des données de Forms Manager et de l’espace de travail AEM Forms.
   * Les développeurs et développeuses de Workbench peuvent continuer à travailler sur leurs processus localement. Il n’est pas nécessaire de déployer de nouveaux processus au cours de la phase de sauvegarde.
   * La décision concernant la durée de chaque session de sauvegarde (en mode de sauvegarde restauration) doit être basée sur la durée totale nécessaire pour sauvegarder toutes les données dans AEM Forms (base de données, stockage global de données, référentiel AEM et toutes les autres données personnalisées supplémentaires).

Sauvegardez la base de données AEM Forms, y compris tous les journaux de transactions. Voir [Base de données AEM Forms](/help/forms/using/admin-help/files-back-recover.md#aem-forms-database).

Pour plus d’informations, voir l’article de votre base de données dans la base de connaissances :
<!-- The four URLs below are all 404s; checked July 19, 2023 -->
* [Oracle - Sauvegarde et récupération pour AEM Forms](https://www.adobe.com/go/kb403624)
* [MySQL - Sauvegarde et récupération pour AEM Forms](https://www.adobe.com/go/kb403625)
* [Microsoft® SQL - Sauvegarde et récupération pour AEM Forms](https://www.adobe.com/go/kb403623)
* [DB2® - Sauvegarde et récupération AEM Forms](https://www.adobe.com/go/kb403626)

Ces articles vous aident à utiliser les fonctions de sauvegarde et de récupération de base de la base de données. Ils ne constituent en aucun cas des guides techniques expliquant de manière exhaustive les fonctions de sauvegarde et de récupération de bases de données spécifiques à certains fournisseurs. Ils présentent simplement les commandes nécessaires à la création d’une stratégie de sauvegarde fiable des bases de données pour les données de l’application AEM Forms.

>[!NOTE]
>
>La sauvegarde de la base de données doit être terminée avant que vous commenciez à sauvegarder le répertoire de stockage global de documents. Si ce n’est pas le cas, vos données sont désynchronisées.

### Passage en modes de sauvegarde {#entering-the-backup-modes}

Vous pouvez utiliser la console d’administration, la commande LCBackupMode ou l’API accompagnant l’installation AEM Forms pour passer à un mode de sauvegarde et le quitter. L’option de la console d’administration n’est pas disponible pour le mode de sauvegarde restauration (couverture en continu) ; utilisez l’option de ligne de commande ou l’API.<!-- Fix broken link For information about using the API to enter and leave backup modes, see AEM Forms API Reference on Help and Tutorials page. -->

>[!NOTE]
>
>Si vous avez configuré SSL sur le serveur Forms, vous ne pouvez pas passer le serveur Forms en mode de sauvegarde à l’aide du script LCBackupMode.CMD.

**Utilisation de la console d’administration pour passer en mode de sauvegarde sécurisé**

1. Connectez-vous à Administration Console.
1. Cliquez sur Paramètres > Paramètres de Core System > Utilitaires de sauvegarde.
1. Sélectionnez Fonctionner en mode de sauvegarde sécurisé et cliquez sur OK.

   Cette méthode fait passer indéfiniment AEM Forms en mode de sauvegarde (aucun délai d’expiration), et il passe en mode d’instantané et non en mode de sauvegarde de restauration.

**Utilisation de l’option de ligne de commande pour passer en mode de sauvegarde sécurisé**

Vous pouvez utiliser les scripts `LCBackupMode` de l’interface de ligne de commande pour faire passer AEM Forms en mode de sauvegarde sécurisé.

1. Définissez ADOBE_LIVECYCLE et lancez le serveur d’applications.
1. Accédez au dossier `*[aem-forms root]*/sdk/misc/Foundation/BackupRestoreCommandline`.
1. Modifiez le script `LCBackupMode.cmd` ou `LCBackupMode.sh` de façon à indiquer les valeurs par défaut correspondant à votre système d’exploitation.
1. Dans l’invite de commande, exécutez la commande suivante sur une seule ligne :

   * (Windows) `LCBackupMode.cmd enter [-Host=`*hostname* `] [-port=`*portnumber* `] [-user=`*username* `] [-password=`*password* `] [-label=`*labelname* `] [-timeout=`*seconds* `]`
   * (Linux®, UNIX®) `LCBackupMode.sh enter [-host=`*hostname* `] [-port=`*portnumber* `] [-user=`*username* `] [-password=`*password* `] [-label=`*labelname* `]`

   Dans les commandes précédentes, les emplacements réservés peuvent être définis comme suit :

   `Host` est le nom d’hôte sur lequel AEM Forms est exécuté.

   `port` correspond au port WebServices du serveur d’applications sur lequel AEM Forms s’exécute.

   `user` est le nom d’utilisateur de l’administrateur ou de l’administratrice AEM Forms.

   `password` correspond au mot de passe de l’administrateur ou de l’administratrice AEM Forms.

   `label` est le libellé de texte de cette sauvegarde (il peut s’agir de n’importe quelle chaîne).

   `timeout` est le nombre de secondes après lequel le mode de sauvegarde est quitté automatiquement. Cette valeur peut être comprise en 0 et 10 080. Si elle correspond à 0 (valeur par défaut), le mode de sauvegarde n’expire jamais.

   Pour plus d’informations sur l’interface de ligne de commande pour le mode de sauvegarde, voir le fichier Lisez-moi (Readme) dans le répertoire BackupRestoreCommandline.

### Quitter les modes de sauvegarde {#leaving-backup-modes}

>[!NOTE]
> 
> Vérifiez que l’utilisateur ou l’utilisatrice dispose de droits d’administration pour accéder à la console d’administration.

Vous pouvez utiliser la console d’administration ou l’option de ligne de commande pour quitter les modes de sauvegarde.

**Quitter le mode de sauvegarde sécurisé (mode instantané)**

Pour faire passer AEM Forms en mode de sauvegarde sécurisé (mode instantané) à l’aide de la console d’administration, suivez la procédure suivante.

1. Connectez-vous à Administration Console.
1. Cliquez sur Paramètres > Paramètres de Core System > Utilitaires de sauvegarde.
1. Désélectionnez Fonctionner en mode de sauvegarde sécurisé et cliquez sur OK.

**Quitter tous les modes de sauvegarde**

Vous pouvez utiliser l’interface de ligne de commande pour faire sortir AEM Forms du mode de sauvegarde sécurisé (mode instantané) ou pour mettre un terme à la session du mode de sauvegarde en cours (mode de sauvegarde de restauration). Vous ne pouvez pas utiliser la console d’administration pour quitter le mode de sauvegarde restauration. Lorsque le mode de sauvegarde de restauration est activé, les commandes Utilitaires de sauvegarde de la console d’administration sont désactivées. Utilisez l’appel API ou la commande LCBackupMode.

1. Accédez au dossier `*[aem-forms root]*/sdk/misc/Foundation/BackupRestoreCommandline`.
1. Modifiez le script `LCBackupMode.cmd` ou `LCBackupMode.sh` de façon à indiquer les valeurs par défaut correspondant à votre système d’exploitation.

   >[!NOTE]
   >
   >Définissez le répertoire JAVA_HOME tel qu’indiqué dans le chapitre correspondant relatif au serveur d’applications, dans le document [Préparation à l’installation d’AEM Forms](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_63_fr)*.*

1. Exécutez la commande suivante sur une même ligne :

   * (Windows) `LCBackupMode.cmd leaveContinuousCoverage [-Host=`*nom_hôte* `] [-port=`*numéro_port* `] [-user=`*nom_utilisateur* `] [-password=`*mot_de_passe* `]`
   * (Linux®, UNIX®) `LCBackupMode.sh leaveContinuousCoverage [-Host=`*nom_hôte* `] [-port=`*numéro_port* `] [-user=`*nom_utilisateur* `] [-password=`*mot_de_passe* `]`

     Dans les commandes précédentes, les emplacements réservés peuvent être définis comme suit :

     `Host` est le nom d’hôte sur lequel AEM Forms est exécuté.

     `port` est le port sur lequel AEM Forms est exécuté sur le serveur d’applications.

     `user` est le nom d’utilisateur de l’administrateur ou de l’administratrice AEM Forms.

     `password` correspond au mot de passe de l’administrateur ou de l’administratrice AEM Forms.

     `leaveContinuousCoverage` : cette option permet de désactiver totalement le mode de sauvegarde restauration.

   >[!NOTE]
   >
   >Le paramètre Couverture en continu ne peut être rétabli tant que ce mode de sauvegarde est inactif. Toute modification apportée durant cette période n’est pas protégée.

   >[!NOTE]
   >
   >Si le stockage de documents dans la base de données est activé, le mode de sauvegarde instantané et le mode de sauvegarde de restauration ne sont pas applicables.

   Pour plus d’informations sur l’interface de ligne de commande pour le mode de sauvegarde, voir le fichier Lisez-moi (Readme) dans le répertoire BackupRestoreCommandline.
