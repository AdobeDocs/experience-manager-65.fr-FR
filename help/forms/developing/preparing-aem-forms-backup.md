---
title: Préparer AEM Forms pour la sauvegarde
seo-title: Preparing AEM Forms for Backup
description: Découvrez comment utiliser le service de sauvegarde et de restauration (Backup and Restore) afin d’activer et de quitter le mode de sauvegarde du serveur AEM Forms à l’aide de l’API Java et de l’API Web Service.
seo-description: Learn how to use the Backup and Restore service to enter and leave the Backup mode for AEM Forms server using the Java API and the Web Service API.
uuid: b8ef2bed-62e2-4000-b55a-30d2fc398a5f
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: e747147e-e96d-43c7-87b3-55947eef81f5
role: Developer
exl-id: aeab003d-ba64-4760-9c56-44638501e9ff
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '2519'
ht-degree: 95%

---

# Préparer AEM Forms pour la sauvegarde {#preparing-aem-forms-for-backup}

**Les exemples et les échantillons de ce document sont réservés à l’environnement AEM Forms sur JEE.**

## À propos du service de sauvegarde et restauration (Backup and Restore) {#about-the-backup-and-restore-service}

Grâce au service de sauvegarde et restauration (Backup and Restore), vous pouvez placer AEM Forms en *mode de sauvegarde*, qui permet d’effectuer des sauvegardes à chaud. Le service de sauvegarde et de restauration n’effectue pas de sauvegarde d’AEM Forms ni ne restaure votre système. Il place plutôt votre serveur dans un état propice à des sauvegardes cohérentes et fiables tout en permettant à votre serveur de continuer à fonctionner. Vous êtes responsable des actions de sauvegarde du stockage global de documents (GDS) et de la base de données connectée au serveur Forms. Le stockage GDS est un répertoire qui sert à stocker les fichiers utilisés dans un processus de longue durée.

Le mode de sauvegarde est un état du serveur selon lequel les fichiers du stockage GDS ne sont pas purgés pendant une procédure de sauvegarde. En lieu et place, des sous-répertoires sont créés dans le répertoire GDS afin de conserver un enregistrement des fichiers à purger après la fin du mode de sauvegarde. Un fichier est conçu pour survivre aux redémarrages du système et peut couvrir des jours, voire des années. Ces fichiers constituent une partie essentielle de l’état global du serveur Forms et peuvent inclure des fichiers PDF, des politiques ou des modèles de formulaire. Si l’un de ces fichiers est perdu ou endommagé, les processus sur le serveur Forms peuvent devenir instables et les données risquent d’être perdues.

Vous pouvez choisir d’effectuer des sauvegardes instantanées, où vous passez généralement en mode de sauvegarde pendant un certain temps, puis quittez le mode de sauvegarde une fois vos activités de sauvegarde terminées. Quitter le mode de sauvegarde est nécessaire afin que les fichiers puissent être purgés du répertoire de stockage global de documents pour s’assurer qu’il ne s’étend pas inutilement. Vous pouvez quitter le mode de sauvegarde de manière explicite ou attendre que le temps expire au cours d’une session en mode de sauvegarde.

Vous pouvez également laisser votre serveur en mode de sauvegarde perpétuel, ce qui est courant dans les stratégies de sauvegarde pour les sauvegardes en continu ou la couverture système continue. Le mode de sauvegarde en continu indique que le système est toujours en mode de sauvegarde et qu’une nouvelle session en mode de sauvegarde est initiée à la libération de la session précédente. En mode de sauvegarde en continu, un fichier est purgé après deux sessions en mode de sauvegarde et n’est plus référencé.

Vous pouvez utiliser le service Sauvegarder et Restaurer pour ajouter des éléments aux applications existantes ou aux applications que vous créez afin d’effectuer des sauvegardes du répertoire de stockage global de documents ou de la base de données connectée au serveur Forms.

>[!NOTE]
>
>Comme pour tous les autres aspects relatifs à l’implémentation d’AEM Forms, vous devez développer et tester une stratégie de sauvegarde et de récupération dans un environnement de développement ou d’évaluation avant de passer à la phase de production. Il s’agit de veiller à ce que l’intégralité de la solution fonctionne comme prévu, sans perte de données.

Vous pouvez effectuer les tâches suivantes à l’aide du service Sauvegarder et Restaurer :

* Passer en mode de sauvegarde.
* Quittez le mode de sauvegarde.

>[!NOTE]
>
>Pour plus d’informations sur les éléments à prendre en compte lors de l’exécution de sauvegardes pour AEM Forms, reportez-vous à l’[aide d’administration](https://www.adobe.com/go/learn_aemforms_admin_63_fr).

>[!NOTE]
>
>Pour plus d’informations sur le service Sauvegarder et Restaurer, reportez-vous aux [Références des services pour AEM Forms](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

## Activer le mode de sauvegarde sur le serveur Forms {#entering-backup-mode-on-the-forms-server}

Vous passez en mode de sauvegarde pour permettre les sauvegardes à chaud d’un serveur Forms. Lorsque vous passez en mode de sauvegarde, vous spécifiez les informations suivantes en fonction des procédures de sauvegarde de votre entreprise :

* Un libellé unique permettant d’identifier la session en mode de sauvegarde qui peut s’avérer utile pour vos processus de sauvegarde.
* La durée d’exécution de la procédure de sauvegarde.
* Un indicateur qui signale si le mode de sauvegarde en continu doit être activé, ce qui n’est utile que si vous effectuez des sauvegardes en continu.

Avant d’écrire des applications pour passer en mode de sauvegarde, il est recommandé de comprendre les procédures de sauvegarde utilisées après avoir mis le serveur Forms en mode de sauvegarde. Pour plus d’informations sur les éléments à prendre en compte lors de l’exécution de sauvegardes pour AEM Forms, reportez-vous à l’[aide d’administration](https://www.adobe.com/go/learn_aemforms_admin_63_fr).

>[!NOTE]
>
>Pour plus d’informations sur le service Sauvegarder et Restaurer, reportez-vous aux [références des services pour AEM Forms](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

### Résumé des étapes {#summary-of-steps}

Pour créer une application qui passe en mode de sauvegarde, procédez comme suit :

1. Incluez les fichiers de projet.
1. Créez un objet client BackupService.
1. Déterminez un libellé unique, le temps nécessaire pour effectuer la sauvegarde et si vous souhaitez passer en mode de sauvegarde continue.
1. Passer en mode de sauvegarde.
1. (Facultatif) Récupérez des informations sur la session en mode de sauvegarde sur le serveur.
1. Effectuez la sauvegarde du stockage global de documents (Global Data Store) et de la base de données.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Il est important d’inclure ces fichiers dans votre projet afin de compiler votre code correctement et d’utiliser l’API du service Sauvegarder et Restaurer.

Pour plus d’informations sur l’emplacement de ces fichiers, voir [Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Créer un objet API client BackupService**

Pour quitter le mode de sauvegarde par programme, créez un objet client BackupService afin d’utiliser l’API du service de sauvegarde et de restauration (Backup and Restore).

**Choisir un libellé unique, déterminer le temps nécessaire à la sauvegarde et décider s’il faut passer en mode de sauvegarde continue**

Avant de passer en mode de sauvegarde, vous devez choisir un libellé unique, déterminer le temps que vous souhaitez allouer à l’exécution de la sauvegarde et décider si vous souhaitez que le serveur Forms reste en mode de sauvegarde. Ces considérations sont importantes pour l’intégration aux procédures de sauvegarde établies par votre organisation. (Voir l’[aide d’administration](https://www.adobe.com/go/learn_aemforms_admin_63_fr).)

**Activer le mode de sauvegarde**

Passez en mode de sauvegarde avec les paramètres conformes aux procédures de sauvegarde de votre entreprise.

**Récupérer les informations sur la session en mode de sauvegarde sur le serveur**

Une fois que vous êtes en mode de sauvegarde, vous pouvez récupérer des informations sur la session. Ces informations peuvent être utilisées pour l’intégration à vos procédures de sauvegarde.

**Sauvegarder le répertoire de stockage global de documents et la base de données**

Une fois le mode de sauvegarde activé, vous pouvez effectuer une sauvegarde du stockage global de documents (GDS) et de la base de données à laquelle le serveur Forms est connecté. Votre organisation a tout loisir de choisir la procédure de sauvegarde : manuelle ou à lʼaide d’autres outils.

### Passer en mode de sauvegarde à l’aide de l’API Java {#enter-backup-mode-using-the-java-api}

Pour passer en mode de sauvegarde à l’aide de l’API du service Backup and Restore, procédez comme suit :

1. Inclure les fichiers du projet

   Incluez les fichiers JAR client nécessaires, tels que adobe-backup-restore-client-sdk.jar, dans le chemin de classe de votre projet Java. Pour créer l’application cliente Java, les fichiers JAR suivants doivent être ajoutés au chemin de classe de votre projet :

   * adobe-backup-restore-client-sdk.jar
   * adobe-livecycle-client.jar
   * adobe-usermanager-client.jar
   * adobe-utilities.jar (obligatoire si AEM Forms est déployé sur JBoss Application Server)
   * jbossall-client.jar (obligatoire si AEM Forms est déployé sur JBoss Application Server)

1. Créer un objet API client BackupService

   Utilisez un objet `ServiceClientFactory` et l’API cliente BackupService ensemble.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion. (Voir [Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
   * Créez un objet `BackupService` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`.

1. Choisissez un libellé unique, déterminez le temps nécessaire à la sauvegarde et décidez s’il faut passer en mode de sauvegarde continue.

   Choisissez un libellé unique, déterminez le temps que vous souhaitez allouer pour effectuer la sauvegarde, puis décidez si vous souhaitez que le serveur Forms reste en mode de sauvegarde continue.

1. Activer le mode de sauvegarde

   Passez en mode de sauvegarde en appelant la méthode `enterBackupMode` avec les paramètres suivants :

   * Une valeur `String` spécifiant un libellé lisible unique qui identifie la session du mode de sauvegarde. Il est recommandé de ne pas utiliser d’espaces ou de caractères qui ne peuvent pas être codés au format XML.
   * Une valeur `int` spécifiant le nombre de minutes à rester en mode de sauvegarde. Vous pouvez spécifier une valeur comprise entre `1` et `10080` (nombre de minutes dans une semaine). Cette valeur est ignorée lors de l’utilisation du mode de sauvegarde continue.
   * Une valeur `Boolean` spécifiant si lʼon doit être en mode de sauvegarde continu. Une valeur de `True` indique que lʼon est en mode de sauvegarde continu. En mode de sauvegarde continue, la valeur que vous indiquez pour le nombre de minutes de maintien en mode de sauvegarde est ignorée.

     Le mode de sauvegarde continu signifie qu’une nouvelle session du mode de sauvegarde est lancée une fois la session en cours terminée. Une valeur de `False` signifie que le mode de sauvegarde continue n’est pas utilisé et, après avoir quitté le mode de sauvegarde, la purge des fichiers du répertoire de stockage global de documents reprend.

1. Récupérer des informations sur la session du mode de sauvegarde sur le serveur

   Récupérez des informations à l’aide de l’objet `BackupModeEntryResult` qui est renvoyé après l’appel de la méthode `enterBackupMode`. Les informations que vous pouvez récupérer après être passé en mode de sauvegarde peuvent s’avérer utiles pour intégrer vos procédures de sauvegarde. Par exemple, le libellé, l’ID de sauvegarde et l’heure de début peuvent être utiles comme entrée pour les noms de fichier de votre procédure de sauvegarde.

1. Sauvegarder le répertoire de stockage global de documents et la base de données

   Sauvegardez le stockage global de documents (GDS) et la base de données à laquelle votre serveur Forms est connecté. Les actions permettant d’effectuer la sauvegarde ne font pas partie du SDK AEM Forms et peuvent même inclure des étapes manuelles spécifiques aux procédures de sauvegarde de votre organisation.

### Passer en mode de sauvegarde à l’aide de l’API de service web {#enter-backup-mode-using-the-web-service-api}

Pour passer en mode de sauvegarde à l’aide du service web fourni par l’API du service Backup and Restore, procédez comme suit :

1. Inclure les fichiers du projet

   * Créez un assemblage client Microsoft .NET qui utilise le fichier WSDL de l’API du service Backup and Restore.
   * Référencez l’assemblage client Microsoft .NET.

1. Créer un objet API client BackupService

   À l’aide de l’assemblage client Microsoft .NET, créez un objet `BackupServiceService` en appelant son constructeur par défaut et en spécifiant les informations d’identification à l’aide de la méthode `Credentials`.

1. Choisissez un libellé unique, déterminez le temps nécessaire à la sauvegarde et décidez s’il faut passer en mode de sauvegarde continue.

   Choisissez un libellé unique, déterminez le temps que vous souhaitez allouer pour effectuer la sauvegarde, puis décidez si vous souhaitez que le serveur Forms reste en mode de sauvegarde continue.

1. Activer le mode de sauvegarde

   Pour passer en mode de sauvegarde, appelez la méthode enterBackupMode et transmettez les valeurs suivantes :

   * Une valeur `String` qui spécifie un libellé lisible unique qui identifie la session du mode de sauvegarde. Il est recommandé de ne pas utiliser d’espaces ou de caractères qui ne peuvent pas être codés au format XML.
   * Une valeur `Uint32` spécifiant le nombre de minutes à rester en mode de sauvegarde. Vous pouvez spécifier une valeur comprise entre `1` et `10080` (nombre de minutes dans une semaine). Cette valeur est ignorée lors de l’utilisation du mode de sauvegarde continue.
   * Une valeur `Boolean` spécifiant si lʼon doit être en mode de sauvegarde continu. Une valeur de `True` indique que lʼon est en mode de sauvegarde continue. En mode de sauvegarde continue, la valeur que vous indiquez pour le nombre de minutes de maintien en mode de sauvegarde est ignorée. Le mode de sauvegarde continue signifie qu’une nouvelle session du mode de sauvegarde est lancée une fois la session en cours terminée.

     Une valeur de `False` signifie que le mode de sauvegarde continue n’est pas utilisé et, après avoir quitté le mode de sauvegarde, la purge des fichiers du répertoire de stockage global de documents reprend.

1. Récupérer des informations sur la session du mode de sauvegarde sur le serveur

   Récupérez des informations sur la session du mode de sauvegarde après l’appel de la méthode enterBackupMode à partir de lʼobjet BackupModeEntryResult renvoyé pour vérifier qu’il a réussi. Les informations que vous pouvez récupérer après être passé en mode de sauvegarde peuvent s’avérer utiles pour intégrer vos procédures de sauvegarde. Par exemple, le libellé, l’ID de sauvegarde et l’heure de début peuvent être utiles comme entrée pour les noms de fichier de votre procédure de sauvegarde.

1. Sauvegarder le répertoire de stockage global de documents et la base de données

   Sauvegardez le stockage global de documents (GDS) et la base de données à laquelle votre serveur Forms est connecté. Les actions permettant d’effectuer la sauvegarde ne font pas partie du SDK AEM Forms et peuvent même inclure des étapes manuelles spécifiques aux procédures de sauvegarde de votre organisation.

## Quitter le mode de sauvegarde sur le serveur Forms {#leaving-backup-mode-on-the-forms-server}

Vous devez quitter le mode de sauvegarde afin que le serveur Forms puisse reprendre la purge des fichiers du répertoire de stockage global de documents (GDS) sur le serveur Forms.

Avant d’écrire des demandes pour quitter le mode de sauvegarde, il est recommandé de comprendre les procédures de sauvegarde utilisées avec AEM Forms. Pour plus d’informations sur les éléments à prendre en compte lors de l’exécution de sauvegardes pour AEM Forms, consultez la section [Aide dʼadministration](https://www.adobe.com/go/learn_aemforms_admin_63_fr).

>[!NOTE]
>
>Pour plus d’informations sur le service Sauvegarder et Restaurer, reportez-vous aux [références des services pour AEM Forms](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

### Résumé des étapes {#summary_of_steps-1}

Pour quitter le mode de sauvegarde, procédez comme suit :

1. Incluez les fichiers de projet.
1. Créez un objet client BackupService.
1. Quittez le mode de sauvegarde.
1. (Facultatif) Récupérez des informations sur la session du mode de sauvegarde exécutée sur le serveur Forms.

**Inclure les fichiers du projet**

Incluez tous les fichiers nécessaires dans votre projet de développement. Ces fichiers sont importants pour la compilation correcte de votre code et l’utilisation de l’API du service de sauvegarde et de restauration (Backup and Restore).

Pour plus d’informations sur l’emplacement de ces fichiers, voir [Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Créer un objet API client BackupService**

Pour quitter le mode de sauvegarde par programme, créez un objet client BackupService afin d’utiliser l’API du service de sauvegarde et de restauration (Backup and Restore).

**Quitter le mode de sauvegarde**

Quittez le mode de sauvegarde pour reprendre la purge normale des fichiers du stockage global de documents (GDS). Avant de quitter le mode de sauvegarde, vous devez vérifier que vos procédures de sauvegarde sont terminées.

**Récupérer des informations sur la session du mode de sauvegarde qui s’est terminée**

Après avoir quitté le mode de sauvegarde, vous pouvez récupérer des informations sur la session. Ces informations peuvent être utilisées pour l’intégration à vos procédures de sauvegarde.

### Quitter le mode de sauvegarde à l’aide de l’API Java {#leave-backup-mode-using-the-java-api}

Quittez le mode de sauvegarde à l’aide de l’API du service de sauvegarde et de restauration (Backup and Restore) (Java) :

1. Inclure les fichiers du projet

   Incluez les fichiers JAR client nécessaires, tels que adobe-backup-restore-client-sdk.jar, dans le chemin de classe de votre projet Java. Pour créer une application cliente Java, les fichiers JAR suivants doivent être ajoutés au chemin de classe de votre projet :

   * adobe-backup-restore-client-sdk.jar
   * adobe-livecycle-client.jar
   * adobe-usermanager-client.jar
   * adobe-utilities.jar (obligatoire si AEM Forms est déployé sur JBoss Application Server)
   * jbossall-client.jar (obligatoire si AEM Forms est déployé sur JBoss Application Server)

1. Créer un objet API client BackupService

   Utilisez un objet `ServiceClientFactory` et l’API cliente BackupService ensemble.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion. (Voir [Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
   * Créez un objet `BackupService` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory` en tant que paramètre. 

1. Activer le mode de sauvegarde

   Quitter le mode de sauvegarde en appelant la méthode `leaveBackupMode`.

1. Récupérer des informations sur la session du mode de sauvegarde sur le serveur

   Récupérez des informations sur l’opération en utilisant l’objet `BackupModeResult` qui est renvoyé. Les informations que vous pouvez récupérer après être passé en mode de sauvegarde peuvent s’avérer utiles pour intégrer vos procédures de sauvegarde. Par exemple, le libellé, l’ID de sauvegarde et l’heure de début peuvent être utiles comme entrée pour les noms de fichier de votre procédure de sauvegarde.

### Quitter le mode de sauvegarde en utilisant l’API du service web {#leave-backup-mode-using-the-web-service-api}

Quittez le mode de sauvegarde en utilisant l’API du service de sauvegarde et de restauration (service Web) :

1. Inclure les fichiers du projet

   Pour utiliser les services Web, vous devez vous assurer d’inclure les fichiers proxy. Pour configurer votre projet afin d’utiliser l’API du service de sauvegarde et de restauration comme un service Web, procédez comme suit.

   * Créez un assemblage client Microsoft .NET qui utilise le fichier WSDL de l’API du service Backup and Restore.
   * Référencez l’assemblage client Microsoft .NET.

1. Créer un objet API client BackupService

   À l’aide de l’assemblage client Microsoft .NET, créez un objet `BackupServiceService` en appelant son constructeur par défaut.

1. Activer le mode de sauvegarde

   Quittez le mode de sauvegarde en appelant l’opération du service web `leaveBackupMode`.

1. Récupérer des informations sur la session du mode de sauvegarde sur le serveur

   Récupérez l’identifiant du mode de sauvegarde après l’opération pour vérifier qu’elle a réussi. Les informations que vous pouvez récupérer après avoir quitté le mode de sauvegarde peuvent s’avérer utiles pour l’intégration à vos procédures de sauvegarde.
