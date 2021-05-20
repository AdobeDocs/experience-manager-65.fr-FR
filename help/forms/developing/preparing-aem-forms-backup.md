---
title: Préparation d’AEM Forms pour la sauvegarde
seo-title: Préparation d’AEM Forms pour la sauvegarde
description: Découvrez comment utiliser le service Backup and Restore pour passer en mode Sauvegarde du serveur AEM Forms et le quitter à l’aide de l’API Java et de l’API Web Service.
seo-description: Découvrez comment utiliser le service Backup and Restore pour passer en mode Sauvegarde du serveur AEM Forms et le quitter à l’aide de l’API Java et de l’API Web Service.
uuid: b8ef2bed-62e2-4000-b55a-30d2fc398a5f
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: e747147e-e96d-43c7-87b3-55947eef81f5
role: Developer
exl-id: aeab003d-ba64-4760-9c56-44638501e9ff
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2554'
ht-degree: 2%

---

# Préparation d’AEM Forms pour la sauvegarde {#preparing-aem-forms-for-backup}

**Les exemples et les exemples de ce document sont réservés à l’environnement AEM Forms on JEE.**

## À propos du service de sauvegarde et de restauration {#about-the-backup-and-restore-service}

Le service Sauvegarde et restauration vous permet de mettre AEM Forms en *mode de sauvegarde*, ce qui permet d’effectuer des sauvegardes à chaud. Le service Sauvegarde et restauration n’effectue pas de sauvegarde d’AEM Forms ni ne restaure votre système. Il place plutôt votre serveur dans un état pour des sauvegardes cohérentes et fiables tout en permettant à votre serveur de continuer à fonctionner. Vous êtes responsable des actions de sauvegarde du stockage global de documents et de la base de données connectée au serveur Forms. Le répertoire de stockage global de documents est un répertoire utilisé pour stocker les fichiers utilisés dans un processus de longue durée.

Le mode de sauvegarde est un état où le serveur entre, de sorte que les fichiers du répertoire de stockage global de documents ne soient pas purgés pendant une procédure de sauvegarde. Au lieu de cela, les sous-répertoires sont créés sous le répertoire de stockage global de documents afin de conserver un enregistrement des fichiers à purger après la fin du mode de sauvegarde. Un fichier est conçu pour survivre aux redémarrages du système et peut couvrir des jours, voire des années. Ces fichiers constituent une partie essentielle de l’état global du serveur Forms et peuvent inclure des fichiers PDF, des stratégies ou des modèles de formulaire. Si l’un de ces fichiers est perdu ou corrompu, les processus sur le serveur Forms peuvent devenir instables et les données risquent d’être perdues.

Vous pouvez choisir d’effectuer des sauvegardes instantanées, où vous passez généralement en mode de sauvegarde pendant un certain temps, puis quitter le mode de sauvegarde une fois vos activités de sauvegarde terminées. Le fait de quitter le mode de sauvegarde est nécessaire afin que les fichiers puissent être purgés du répertoire de stockage global de documents pour s’assurer qu’il ne s’étend pas inutilement. Vous pouvez quitter le mode de sauvegarde explicitement ou attendre que le temps expire au cours d’une session du mode de sauvegarde.

Vous pouvez également laisser votre serveur en mode de sauvegarde perpétuelle, ce qui est typique des stratégies de sauvegarde pour les sauvegardes en continu ou la couverture système continue. Le mode de sauvegarde restauration indique que le système est toujours en mode de sauvegarde, avec une nouvelle session du mode de sauvegarde lancée dès que la session précédente est libérée. En mode de sauvegarde continue, un fichier est purgé après deux sessions de mode de sauvegarde et n’est plus référencé.

Vous pouvez utiliser le service Backup and Restore pour ajouter des éléments aux applications existantes ou aux nouvelles applications que vous créez afin d’effectuer des sauvegardes du répertoire de stockage global de documents ou de la base de données connectée au serveur Forms.

>[!NOTE]
>
>Comme pour tout autre aspect de votre mise en oeuvre AEM Forms, votre stratégie de sauvegarde et de récupération doit être développée et testée dans un environnement de développement ou d’évaluation avant d’être utilisée en production pour vous assurer que l’ensemble de la solution fonctionne comme prévu sans perte de données.

Vous pouvez effectuer les tâches suivantes à l’aide du service Sauvegarde et restauration :

* Passez en mode de sauvegarde.
* Quittez le mode de sauvegarde.

>[!NOTE]
>
>Pour plus d’informations sur ce qu’il convient de prendre en compte lors des sauvegardes pour AEM Forms, voir [Aide à l’administration](https://www.adobe.com/go/learn_aemforms_admin_63).

>[!NOTE]
>
>Pour plus d’informations sur le service Backup and Restore, voir [Guide de référence des services pour AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Passage en mode de sauvegarde sur le serveur Forms {#entering-backup-mode-on-the-forms-server}

Vous passez en mode de sauvegarde pour permettre les sauvegardes à chaud d’un serveur Forms. Lorsque vous passez en mode de sauvegarde, vous spécifiez les informations suivantes en fonction des procédures de sauvegarde de votre entreprise :

* Libellé unique permettant d’identifier la session de mode de sauvegarde qui peut s’avérer utile pour vos processus de sauvegarde.
* Heure à laquelle la procédure de sauvegarde doit être terminée.
* Indicateur qui indique si le mode de sauvegarde en continu doit être activé, ce qui n’est utile que si vous effectuez des sauvegardes en continu.

Avant d’écrire des applications pour passer en mode de sauvegarde, il est recommandé de comprendre les procédures de sauvegarde qui seront utilisées après avoir mis le serveur Forms en mode de sauvegarde. Pour plus d’informations sur ce qu’il convient de prendre en compte lors des sauvegardes pour AEM Forms, voir [Aide à l’administration](https://www.adobe.com/go/learn_aemforms_admin_63).

>[!NOTE]
>
>Pour plus d’informations sur le service Backup and Restore, voir [Guide de référence des services pour AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary-of-steps}

Pour créer une application qui passe en mode de sauvegarde, procédez comme suit :

1. Inclure les fichiers de projet.
1. Créez un objet client BackupService .
1. Déterminez un libellé unique, le temps nécessaire pour effectuer la sauvegarde et si vous souhaitez passer en mode de sauvegarde continue.
1. Passez en mode de sauvegarde.
1. (Facultatif) Récupérez des informations sur la session du mode de sauvegarde sur le serveur.
1. Effectuez la sauvegarde du stockage global de documents (Global Data Store) et de la base de données.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Ces fichiers sont importants à inclure dans votre projet afin de compiler votre code correctement et d’utiliser l’API du service de sauvegarde et de restauration.

Pour plus d’informations sur l’emplacement de ces fichiers, voir [Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Création d’un objet API client BackupService**

Pour quitter le mode de sauvegarde par programmation, vous créez un objet client BackupService afin d’utiliser l’API Backup and Restore Service.

**Choisissez un libellé unique, déterminez le temps nécessaire à la sauvegarde et décidez s’il faut passer en mode de sauvegarde continue.**

Avant de passer en mode de sauvegarde, vous devez choisir un libellé unique, déterminer le temps que vous souhaitez allouer pour effectuer la sauvegarde et décider si vous souhaitez que le serveur Forms reste en mode de sauvegarde. Ces considérations sont importantes pour l’intégration aux procédures de sauvegarde établies par votre organisation. (Voir [Aide à l’administration](https://www.adobe.com/go/learn_aemforms_admin_63).)

**Activation du mode de sauvegarde**

Passez en mode de sauvegarde avec les paramètres conformes aux procédures de sauvegarde de votre entreprise.

**Récupération des informations sur la session du mode de sauvegarde sur le serveur**

Une fois que vous êtes en mode de sauvegarde, vous pouvez récupérer des informations sur la session. Ces informations peuvent être utilisées pour l’intégration à vos procédures de sauvegarde.

**Sauvegarde du répertoire de stockage global de documents et de la base de données**

Une fois le mode de sauvegarde activé, vous pouvez effectuer une sauvegarde du stockage global de documents (GDS) et de la base de données à laquelle le serveur Forms est connecté. Cette étape est spécifique à votre entreprise, car vous pouvez effectuer cette étape manuellement ou exécuter d’autres outils pour exécuter la procédure de sauvegarde.

### Passez en mode de sauvegarde à l’aide de l’API Java {#enter-backup-mode-using-the-java-api}

Passez en mode de sauvegarde à l’aide de l’API du service de sauvegarde et de restauration :

1. Inclure les fichiers de projet

   Incluez les fichiers JAR client nécessaires, tels que adobe-backup-restore-client-sdk.jar, dans le chemin de classe de votre projet Java. Pour créer l’application cliente Java, les fichiers JAR suivants doivent être ajoutés au chemin de classe de votre projet :

   * adobe-backup-restore-client-sdk.jar
   * adobe-livecycle-client.jar
   * adobe-usermanager-client.jar
   * adobe-utility.jar (obligatoire si AEM Forms est déployé sur JBoss Application Server)
   * jbossall-client.jar (obligatoire si AEM Forms est déployé sur JBoss Application Server)

1. Création d’un objet API client BackupService

   Vous utilisez un objet `ServiceClientFactory` et l’objet API client BackupService ensemble.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion. (Voir [Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
   * Créez un objet `BackupService` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`.

1. Choisissez un libellé unique, déterminez le temps nécessaire à la sauvegarde et décidez s’il faut passer en mode de sauvegarde continue.

   Choisissez un libellé unique, déterminez le temps que vous souhaitez allouer pour effectuer la sauvegarde, puis décidez si vous souhaitez que le serveur Forms reste en mode de sauvegarde continue.

1. Activation du mode de sauvegarde

   Passez en mode de sauvegarde en appelant la méthode `enterBackupMode` avec les paramètres suivants :

   * Valeur `String` qui spécifie un libellé lisible par l’utilisateur unique qui identifie la session du mode de sauvegarde. Il est recommandé de ne pas utiliser d’espaces ou de caractères qui ne peuvent pas être codés au format XML.
   * Valeur `int` qui spécifie le nombre de minutes pour rester en mode de sauvegarde. Vous pouvez définir une valeur comprise entre `1` et `10080` (nombre de minutes dans une semaine). Cette valeur est ignorée lors de l’utilisation du mode de sauvegarde continue.
   * Valeur `Boolean` qui spécifie s’il faut être en mode de sauvegarde continu. La valeur `True` indique qu’il s’agit d’un mode de sauvegarde continu. En mode de sauvegarde continue, la valeur que vous indiquez pour le nombre de minutes de maintien en mode de sauvegarde est ignorée.

      Le mode de sauvegarde continu signifie qu’une nouvelle session du mode de sauvegarde est lancée une fois la session en cours terminée. Une valeur `False` signifie que le mode de sauvegarde continue n’est pas utilisé et, après avoir quitté le mode de sauvegarde, la purge des fichiers du répertoire de stockage global de documents reprend.

1. Récupération des informations sur la session du mode de sauvegarde sur le serveur

   Récupérez les informations à l’aide de l’objet `BackupModeEntryResult` renvoyé après avoir appelé la méthode `enterBackupMode` . Les informations que vous pouvez récupérer après avoir passé en mode de sauvegarde peuvent s’avérer utiles pour l’intégration à vos procédures de sauvegarde. Par exemple, le libellé, l’identifiant de sauvegarde et l’heure de début peuvent être utiles comme entrée pour les noms de fichier de votre procédure de sauvegarde.

1. Sauvegarde du répertoire de stockage global de documents et de la base de données

   Sauvegardez le stockage global de documents et la base de données à laquelle votre serveur Forms est connecté. Les actions permettant d’effectuer la sauvegarde ne font pas partie du SDK AEM Forms et peuvent même inclure des étapes manuelles spécifiques aux procédures de sauvegarde de votre entreprise.

### Passez en mode de sauvegarde à l’aide de l’API de service Web {#enter-backup-mode-using-the-web-service-api}

Passez en mode de sauvegarde à l’aide du service Web fourni par l’API du service de sauvegarde et de restauration :

1. Inclure les fichiers de projet

   * Créez un assemblage client Microsoft .NET qui utilise le fichier WSDL de l’API du service de sauvegarde et de restauration.
   * Référencez l’assemblage client Microsoft .NET.

1. Création d’un objet API client BackupService

   À l’aide de l’assemblage client Microsoft .NET, créez un objet `BackupServiceService` en appelant son constructeur par défaut et spécifiez les informations d’identification à l’aide de la méthode `Credentials` .

1. Choisissez un libellé unique, déterminez le temps nécessaire à la sauvegarde et décidez s’il faut passer en mode de sauvegarde continue.

   Choisissez un libellé unique, déterminez le temps que vous souhaitez allouer pour effectuer la sauvegarde, puis décidez si vous souhaitez que le serveur Forms reste en mode de sauvegarde continue.

1. Activation du mode de sauvegarde

   Pour passer en mode de sauvegarde, appelez la méthode enterBackupMode et transmettez les valeurs suivantes :

   * Valeur `String` qui spécifie un libellé lisible par l’utilisateur unique qui identifie la session du mode de sauvegarde. Il est recommandé de ne pas utiliser d’espaces ou de caractères qui ne peuvent pas être codés au format XML.
   * Valeur `Uint32` qui spécifie le nombre de minutes pour rester en mode de sauvegarde. Vous pouvez spécifier une valeur comprise entre `1` et `10080` (nombre de minutes dans une semaine). Cette valeur est ignorée lors de l’utilisation du mode de sauvegarde continue.
   * Valeur `Boolean` qui spécifie s’il faut être en mode de sauvegarde continu. La valeur `True` indique qu’il s’agit d’un mode de sauvegarde continu. En mode de sauvegarde continue, la valeur que vous indiquez pour le nombre de minutes de maintien en mode de sauvegarde est ignorée. Le mode de sauvegarde continu signifie qu’une nouvelle session du mode de sauvegarde est lancée une fois la session en cours terminée.

      Une valeur `False` signifie que le mode de sauvegarde continue n’est pas utilisé et, après avoir quitté le mode de sauvegarde, la purge des fichiers du répertoire de stockage global de documents reprend.

1. Récupération des informations sur la session du mode de sauvegarde sur le serveur

   Récupérez des informations sur la session du mode de sauvegarde après l’appel de la méthode enterBackupMode à partir du paramètre BackupModeEntryResult renvoyé pour vérifier qu’il a réussi. Les informations que vous pouvez récupérer après avoir passé en mode de sauvegarde peuvent s’avérer utiles pour l’intégration à vos procédures de sauvegarde. Par exemple, le libellé, l’identifiant de sauvegarde et l’heure de début peuvent être utiles comme entrée pour les noms de fichier de votre procédure de sauvegarde.

1. Sauvegarde du répertoire de stockage global de documents et de la base de données

   Sauvegardez le stockage global de documents et la base de données à laquelle votre serveur Forms est connecté. Les actions permettant d’effectuer la sauvegarde ne font pas partie du SDK AEM Forms et peuvent même inclure des étapes manuelles spécifiques aux procédures de sauvegarde de votre entreprise.

## Quitter le mode de sauvegarde sur le serveur Forms {#leaving-backup-mode-on-the-forms-server}

Vous quittez le mode de sauvegarde afin que le serveur Forms puisse reprendre la purge des fichiers du répertoire de stockage global de documents (GDS) sur le serveur Forms.

Avant d’écrire des demandes pour passer en mode de sortie, il est recommandé de comprendre les procédures de sauvegarde utilisées avec AEM Forms. Pour plus d’informations sur ce qu’il convient de prendre en compte lors des sauvegardes pour AEM Forms, voir [Aide à l’administration](https://www.adobe.com/go/learn_aemforms_admin_63).

>[!NOTE]
>
>Pour plus d’informations sur le service Backup and Restore, voir [Guide de référence des services pour AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary_of_steps-1}

Pour quitter le mode de sauvegarde, procédez comme suit :

1. Inclure les fichiers de projet.
1. Créez un objet client BackupService .
1. Quittez le mode de sauvegarde.
1. (Facultatif) Récupérez des informations sur la session du mode de sauvegarde en cours d’exécution sur le serveur Forms.

**Inclure les fichiers de projet**

Incluez tous les fichiers nécessaires dans votre projet de développement. Ces fichiers sont importants pour la compilation correcte de votre code et l’utilisation de l’API du service de sauvegarde et de restauration.

Pour plus d’informations sur l’emplacement de ces fichiers, voir [Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Création d’un objet API client BackupService**

Pour quitter le mode de sauvegarde par programmation, vous créez un objet client BackupService afin d’utiliser l’API Backup and Restore Service.

**Quitter le mode de sauvegarde**

Laissez le mode de sauvegarde pour reprendre la purge normale des fichiers du stockage global de documents (GDS). Avant de quitter le mode de sauvegarde, vous devez vérifier que vos procédures de sauvegarde sont terminées.

**Récupérez des informations sur la session du mode de sauvegarde qui s’est terminée.**

Après avoir quitté le mode de sauvegarde, vous pouvez récupérer des informations sur la session. Ces informations peuvent être utilisées pour l’intégration à vos procédures de sauvegarde.

### Quitter le mode de sauvegarde à l’aide de l’API Java {#leave-backup-mode-using-the-java-api}

Quittez le mode de sauvegarde à l’aide de l’API du service de sauvegarde et de restauration (Java) :

1. Inclure les fichiers de projet

   Incluez les fichiers JAR client nécessaires, tels que adobe-backup-restore-client-sdk.jar, dans le chemin de classe de votre projet Java. Pour créer une application cliente Java, les fichiers JAR suivants doivent être ajoutés au chemin de classe de votre projet :

   * adobe-backup-restore-client-sdk.jar
   * adobe-livecycle-client.jar
   * adobe-usermanager-client.jar
   * adobe-utility.jar (obligatoire si AEM Forms est déployé sur JBoss Application Server)
   * jbossall-client.jar (obligatoire si AEM Forms est déployé sur JBoss Application Server)

1. Création d’un objet API client BackupService

   Vous utilisez un objet `ServiceClientFactory` et l’objet API client BackupService ensemble.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion. (Voir [Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
   * Créez un objet `BackupService` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory` comme paramètre.

1. Activation du mode de sauvegarde

   Quittez le mode de sauvegarde en appelant la méthode `leaveBackupMode` .

1. Récupération des informations sur la session du mode de sauvegarde sur le serveur

   Récupérez des informations sur l’opération à l’aide de l’objet `BackupModeResult` renvoyé. Les informations que vous pouvez récupérer après avoir passé en mode de sauvegarde peuvent s’avérer utiles pour l’intégration à vos procédures de sauvegarde. Par exemple, le libellé, l’identifiant de sauvegarde et l’heure de début peuvent être utiles comme entrée pour les noms de fichier de votre procédure de sauvegarde.

### Quitter le mode de sauvegarde à l’aide de l’API de service Web {#leave-backup-mode-using-the-web-service-api}

Quittez le mode de sauvegarde à l’aide de l’API du service de sauvegarde et de restauration (service Web) :

1. Inclure les fichiers de projet

   Pour utiliser les services web, vous devez vous assurer d’inclure les fichiers proxy. Pour configurer votre projet de manière à utiliser l’API du service de sauvegarde et de restauration en tant que service Web, procédez comme suit.

   * Créez un assemblage client Microsoft .NET qui utilise le fichier WSDL de l’API du service de sauvegarde et de restauration.
   * Référencez l’assemblage client Microsoft .NET.

1. Création d’un objet API client BackupService

   À l’aide de l’assemblage client Microsoft .NET, créez un objet `BackupServiceService` en appelant son constructeur par défaut.

1. Activation du mode de sauvegarde

   Quittez le mode de sauvegarde en appelant l’opération de service Web `leaveBackupMode`.

1. Récupération des informations sur la session du mode de sauvegarde sur le serveur

   Récupérez l’identifiant du mode de sauvegarde après l’opération pour vérifier qu’il a réussi. Les informations que vous pouvez récupérer après avoir quitté le mode de sauvegarde peuvent s’avérer utiles pour l’intégration à vos procédures de sauvegarde.
