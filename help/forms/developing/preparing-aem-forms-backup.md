---
title: Préparation d’AEM Forms pour la sauvegarde
seo-title: Préparation d’AEM Forms pour la sauvegarde
description: 'null'
seo-description: 'null'
uuid: b8ef2bed-62e2-4000-b55a-30d2fc398a5f
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: e747147e-e96d-43c7-87b3-55947eef81f5
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Préparation d’AEM Forms pour la sauvegarde {#preparing-aem-forms-for-backup}

## À propos du service de sauvegarde et de restauration {#about-the-backup-and-restore-service}

Le service Sauvegarde et restauration vous permet de mettre AEM Forms en mode *de* sauvegarde, ce qui permet d’effectuer des sauvegardes à chaud. Le service Sauvegarde et restauration n’effectue pas de sauvegarde d’AEM Forms ni ne restaure votre système. Il place plutôt votre serveur dans un état pour des sauvegardes cohérentes et fiables tout en permettant à votre serveur de continuer à fonctionner. Vous êtes responsable des actions de sauvegarde du stockage global de documents et de la base de données connectée au serveur Forms. Le répertoire de stockage global de documents est un répertoire utilisé pour stocker les fichiers utilisés dans un processus de longue durée.

Le mode de sauvegarde est un état que le serveur saisit afin que les fichiers du répertoire de stockage global de documents ne soient pas purgés pendant une procédure de sauvegarde. Les sous-répertoires sont créés sous le répertoire de stockage global de documents afin de conserver un enregistrement des fichiers à purger une fois le mode de sauvegarde terminé. Un fichier est destiné à survivre aux redémarrages du système et peut s’étendre sur plusieurs jours, voire plusieurs années. Ces fichiers constituent une partie essentielle de l’état global du serveur Forms et peuvent inclure des fichiers PDF, des stratégies ou des modèles de formulaire. Si l’un de ces fichiers est perdu ou corrompu, les processus sur le serveur Forms peuvent devenir instables et les données peuvent être perdues.

Vous pouvez choisir d’effectuer des sauvegardes d’instantané, où vous passez généralement en mode de sauvegarde pendant une période, puis quittez le mode de sauvegarde une fois vos activités de sauvegarde terminées. Il est nécessaire de quitter le mode de sauvegarde pour purger les fichiers du répertoire de stockage global de documents afin de s’assurer qu’ils ne sont pas trop volumineux. Vous pouvez quitter explicitement le mode de sauvegarde ou attendre que le temps expire lors d’une session du mode de sauvegarde.

Vous pouvez également laisser votre serveur en mode de sauvegarde perpétuelle, ce qui est typique pour les stratégies de sauvegarde pour les sauvegardes restauration ou la couverture système continue. Le mode de sauvegarde restauration indique que le système est toujours en mode de sauvegarde et qu’une nouvelle session du mode de sauvegarde est lancée dès que la session précédente est libérée. En mode de sauvegarde continue, un fichier est purgé après deux sessions du mode de sauvegarde et n’est plus référencé.

Vous pouvez utiliser le service Sauvegarde et restauration pour ajouter des éléments aux applications existantes ou aux nouvelles applications que vous créez afin d’effectuer des sauvegardes du répertoire de stockage global de documents ou de la base de données connectée au serveur Forms.

>[!NOTE]
>
>Comme pour tout autre aspect de votre implémentation d’AEM Forms, votre stratégie de sauvegarde et de récupération doit être développée et testée dans un environnement de développement ou d’évaluation avant d’être utilisée en production pour vous assurer que la solution complète fonctionne comme prévu sans perte de données.

Vous pouvez effectuer les tâches suivantes à l’aide du service Sauvegarde et restauration :

* Passez en mode de sauvegarde.
* Quittez le mode de sauvegarde.

>[!NOTE]
>
>Pour plus d’informations sur les éléments à prendre en compte lors des sauvegardes pour AEM Forms, voir Aide [à l’](https://www.adobe.com/go/learn_aemforms_admin_63)administration.

>[!NOTE]
>
>For more information about the Backup and Restore service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Saisie du mode de sauvegarde sur le serveur Forms {#entering-backup-mode-on-the-forms-server}

Vous passez en mode de sauvegarde pour autoriser les sauvegardes à chaud d’un serveur Forms. Lorsque vous passez en mode de sauvegarde, vous spécifiez les informations suivantes en fonction des procédures de sauvegarde de votre entreprise :

* Libellé unique permettant d’identifier la session du mode de sauvegarde qui peut être utile pour vos processus de sauvegarde.
* Heure de fin de la procédure de sauvegarde.
* Indicateur qui indique si vous devez être en mode de sauvegarde continue, ce qui n’est utile que si vous effectuez des sauvegardes en continu.

Avant d’écrire des applications pour passer en mode de sauvegarde, il est recommandé de comprendre les procédures de sauvegarde qui seront utilisées après avoir mis le serveur Forms en mode de sauvegarde. Pour plus d’informations sur les éléments à prendre en compte lors des sauvegardes pour AEM Forms, voir Aide [à l’](https://www.adobe.com/go/learn_aemforms_admin_63)administration.

>[!NOTE]
>
>For more information about the Backup and Restore service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary-of-steps}

Pour créer une application qui passe en mode de sauvegarde, procédez comme suit :

1. Incluez des fichiers de projet.
1. Créez un objet client BackupService.
1. Déterminez une étiquette unique, la durée d’exécution de la sauvegarde et si vous souhaitez passer en mode de sauvegarde continue.
1. Passez en mode de sauvegarde.
1. (Facultatif) Récupérez des informations sur la session du mode de sauvegarde sur le serveur.
1. Effectuez la sauvegarde du répertoire de stockage global de documents (stockage global de données) et de la base de données.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Ces fichiers sont importants à inclure dans votre projet pour compiler correctement votre code et utiliser l’API du service de sauvegarde et de restauration.

Pour plus d’informations sur l’emplacement de ces fichiers, voir [Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Création d’un objet API Client BackupService**

Pour quitter le mode de sauvegarde par programmation, vous créez un objet client BackupService afin d’utiliser l’API Service de sauvegarde et de restauration.

**Choisissez une étiquette unique, déterminez la durée d’exécution de la sauvegarde et décidez si vous êtes en mode de sauvegarde continue.**

Avant de passer en mode de sauvegarde, vous devez choisir une étiquette unique, déterminer le temps que vous souhaitez allouer pour effectuer la sauvegarde et décider si vous souhaitez que le serveur Forms reste en mode de sauvegarde. Ces considérations sont importantes pour l’intégration aux procédures de sauvegarde établies par votre organisation. (See [administration help](https://www.adobe.com/go/learn_aemforms_admin_63).)

**Passer en mode de sauvegarde**

Passez en mode de sauvegarde avec les paramètres compatibles avec les procédures de sauvegarde de votre entreprise.

**Récupérer des informations sur la session du mode de sauvegarde sur le serveur**

Une fois que vous êtes en mode de sauvegarde, vous pouvez récupérer des informations sur la session. Ces informations peuvent être utilisées pour l&#39;intégration à vos procédures de sauvegarde

**Exécution de la sauvegarde du répertoire de stockage global de documents et de la base de données**

Une fois que vous êtes en mode de sauvegarde, vous pouvez effectuer une sauvegarde du stockage global de documents et de la base de données à laquelle le serveur Forms est connecté. Cette étape est spécifique à votre entreprise, puisque vous pouvez effectuer cette étape manuellement ou exécuter d’autres outils pour effectuer la procédure de sauvegarde.

### Passer en mode de sauvegarde à l’aide de l’API Java {#enter-backup-mode-using-the-java-api}

Passez en mode de sauvegarde à l’aide de l’API Service de sauvegarde et de restauration :

1. Inclure les fichiers de projet

   Incluez les fichiers JAR client nécessaires, tels que adobe-backup-restore-client-sdk.jar, dans le chemin de classe de votre projet Java. Pour créer l’application cliente Java, vous devez ajouter les fichiers JAR suivants au chemin de classe de votre projet :

   * adobe-backup-restore-client-sdk.jar
   * adobe-livecycle-client.jar
   * adobe-usermanager-client.jar
   * adobe-utilities.jar (requis si AEM Forms est déployé sur JBoss Application Server)
   * jbossall-client.jar (requis si AEM Forms est déployé sur JBoss Application Server)

1. Création d’un objet API Client BackupService

   Vous utilisez ensemble un `ServiceClientFactory` objet et l’objet API client BackupService.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion. (Voir [Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
   * Create an `BackupService` object by using its constructor and passing the `ServiceClientFactory` object.

1. Choisissez une étiquette unique, déterminez la durée d’exécution de la sauvegarde et décidez si vous êtes en mode de sauvegarde continue.

   Choisissez une étiquette unique, déterminez le temps que vous souhaitez allouer pour effectuer la sauvegarde et décidez si vous souhaitez que le serveur Forms reste en mode de sauvegarde continue.

1. Passer en mode de sauvegarde

   Passez en mode de sauvegarde en appelant la `enterBackupMode` méthode avec les paramètres suivants :

   * Valeur `String` spécifiant un libellé lisible par un utilisateur unique qui identifie la session du mode de sauvegarde. Il est recommandé de ne pas utiliser d’espaces ou de caractères qui ne peuvent pas être codés au format XML.
   * Valeur `int` indiquant le nombre de minutes pendant lesquelles rester en mode de sauvegarde. Vous pouvez spécifier une valeur comprise entre `1` et `10080` (nombre de minutes par semaine). Cette valeur est ignorée lors de l’utilisation du mode de sauvegarde continue.
   * Valeur `Boolean` indiquant si le mode de sauvegarde continue doit être activé. La valeur `True` indique d’être en mode de sauvegarde continue. En mode de sauvegarde continue, la valeur que vous spécifiez pour le nombre de minutes de maintien en mode de sauvegarde est ignorée.

      Le mode de sauvegarde continue signifie qu’une nouvelle session du mode de sauvegarde est démarrée une fois la session en cours terminée. Une valeur de `False` signifie que le mode de sauvegarde continue n’est pas utilisé et que, après avoir quitté le mode de sauvegarde, la purge des fichiers du répertoire de stockage global de documents reprend.

1. Récupérer des informations sur la session du mode de sauvegarde sur le serveur

   Récupérez les informations à l’aide de l’ `BackupModeEntryResult` objet renvoyé après avoir appelé la `enterBackupMode` méthode. Les informations que vous pouvez récupérer après avoir passé en mode de sauvegarde peuvent s’avérer utiles pour l’intégration à vos procédures de sauvegarde. Par exemple, le libellé, l’ID de sauvegarde et l’heure de début peuvent être utiles comme entrée pour les noms de fichier de votre procédure de sauvegarde.

1. Exécution de la sauvegarde du répertoire de stockage global de documents et de la base de données

   Sauvegardez le stockage global de documents (GDS) et la base de données à laquelle votre serveur Forms est connecté. Les actions permettant d’effectuer la sauvegarde ne font pas partie du SDK d’AEM Forms et peuvent même inclure des étapes manuelles spécifiques aux procédures de sauvegarde de votre entreprise.

### Passer en mode de sauvegarde à l’aide de l’API du service Web {#enter-backup-mode-using-the-web-service-api}

Passez en mode de sauvegarde à l’aide du service Web fourni par l’API Service de sauvegarde et de restauration :

1. Inclure les fichiers de projet

   * Créez un assembly client Microsoft .NET qui utilise le WSDL de l&#39;API du service de sauvegarde et de restauration.
   * Référencez l&#39;assembly client Microsoft .NET.

1. Création d’un objet API Client BackupService

   A l&#39;aide de l&#39;assembly client Microsoft .NET, créez un `BackupServiceService` objet en appelant son constructeur par défaut et spécifiez les informations d&#39;identification à l&#39;aide de la `Credentials` méthode.

1. Choisissez une étiquette unique, déterminez la durée d’exécution de la sauvegarde et décidez si vous êtes en mode de sauvegarde continue.

   Choisissez une étiquette unique, déterminez le temps que vous souhaitez allouer pour effectuer la sauvegarde et décidez si vous souhaitez que le serveur Forms reste en mode de sauvegarde continue.

1. Passer en mode de sauvegarde

   Pour passer en mode de sauvegarde, appelez la méthode enterBackupMode et transmettez les valeurs suivantes :

   * Valeur `String` spécifiant un libellé lisible par un utilisateur unique qui identifie la session du mode de sauvegarde. Il est recommandé de ne pas utiliser d’espaces ou de caractères qui ne peuvent pas être codés au format XML.
   * Valeur `Uint32` indiquant le nombre de minutes pendant lesquelles rester en mode de sauvegarde. Vous pouvez spécifier une valeur comprise entre `1` et `10080` (nombre de minutes par semaine). Cette valeur est ignorée lors de l’utilisation du mode de sauvegarde continue.
   * Valeur `Boolean` indiquant si le mode de sauvegarde continue doit être activé. La valeur `True` indique d’être en mode de sauvegarde continue. En mode de sauvegarde continue, la valeur que vous spécifiez pour le nombre de minutes de maintien en mode de sauvegarde est ignorée. Le mode de sauvegarde continue signifie qu’une nouvelle session du mode de sauvegarde est démarrée une fois la session en cours terminée.

      Une valeur de `False` signifie que le mode de sauvegarde continue n’est pas utilisé et que, après avoir quitté le mode de sauvegarde, la purge des fichiers du répertoire de stockage global de documents reprend.

1. Récupérer des informations sur la session du mode de sauvegarde sur le serveur

   Récupérez des informations sur la session du mode de sauvegarde après avoir appelé la méthode enterBackupMode à partir du paramètre BackupModeEntryResult renvoyé pour vérifier qu’il a réussi. Les informations que vous pouvez récupérer après avoir passé en mode de sauvegarde peuvent s’avérer utiles pour l’intégration à vos procédures de sauvegarde. Par exemple, le libellé, l’ID de sauvegarde et l’heure de début peuvent être utiles comme entrée pour les noms de fichier de votre procédure de sauvegarde.

1. Exécution de la sauvegarde du répertoire de stockage global de documents et de la base de données

   Sauvegardez le stockage global de documents (GDS) et la base de données à laquelle votre serveur Forms est connecté. Les actions permettant d’effectuer la sauvegarde ne font pas partie du SDK d’AEM Forms et peuvent même inclure des étapes manuelles spécifiques aux procédures de sauvegarde de votre entreprise.

## Quitter le mode de sauvegarde sur le serveur Forms {#leaving-backup-mode-on-the-forms-server}

Vous quittez le mode de sauvegarde afin que le serveur Forms reprenne la purge des fichiers du répertoire de stockage global de documents (GDS) sur le serveur Forms.

Avant d’écrire des applications pour passer en mode de sortie, il est recommandé de comprendre les procédures de sauvegarde utilisées avec AEM Forms. Pour plus d’informations sur les éléments à prendre en compte lors des sauvegardes pour AEM Forms, voir Aide [à l’](https://www.adobe.com/go/learn_aemforms_admin_63)administration.

>[!NOTE]
>
>For more information about the Backup and Restore service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary_of_steps-1}

Pour quitter le mode de sauvegarde, procédez comme suit :

1. Incluez des fichiers de projet.
1. Créez un objet client BackupService.
1. Quittez le mode de sauvegarde.
1. (Facultatif) Récupérez des informations sur la session du mode de sauvegarde en cours d’exécution sur le serveur Forms.

**Inclure les fichiers de projet**

Incluez tous les fichiers nécessaires dans votre projet de développement. Ces fichiers sont importants pour compiler correctement votre code et utiliser l’API du service de sauvegarde et de restauration.

Pour plus d’informations sur l’emplacement de ces fichiers, voir [Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Création d’un objet API Client BackupService**

Pour quitter le mode de sauvegarde par programmation, vous créez un objet client BackupService afin d’utiliser l’API Service de sauvegarde et de restauration.

**Quitter le mode de sauvegarde**

Laissez le mode de sauvegarde pour reprendre la purge normale des fichiers du stockage global de documents (GDS). Avant de quitter le mode de sauvegarde, vous devez vérifier que vos procédures de sauvegarde sont terminées.

**Récupérer les informations sur la session du mode de sauvegarde qui s’est terminée**

Après avoir quitté le mode de sauvegarde, vous pouvez récupérer des informations sur la session. Ces informations peuvent être utilisées pour l’intégration à vos procédures de sauvegarde.

### Quitter le mode de sauvegarde à l’aide de l’API Java {#leave-backup-mode-using-the-java-api}

Quittez le mode de sauvegarde à l’aide de l’API du service de sauvegarde et de restauration (Java) :

1. Inclure les fichiers de projet

   Incluez les fichiers JAR client nécessaires, tels que adobe-backup-restore-client-sdk.jar, dans le chemin de classe de votre projet Java. Pour créer une application cliente Java, les fichiers JAR suivants doivent être ajoutés au chemin de classe de votre projet :

   * adobe-backup-restore-client-sdk.jar
   * adobe-livecycle-client.jar
   * adobe-usermanager-client.jar
   * adobe-utilities.jar (requis si AEM Forms est déployé sur JBoss Application Server)
   * jbossall-client.jar (requis si AEM Forms est déployé sur JBoss Application Server)

1. Création d’un objet API Client BackupService

   Vous utilisez ensemble un `ServiceClientFactory` objet et l’objet API client BackupService.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion. (Voir [Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
   * Create a `BackupService` object by using its constructor and passing the `ServiceClientFactory` object as parameter.

1. Passer en mode de sauvegarde

   Quittez le mode de sauvegarde en appelant la `leaveBackupMode` méthode.

1. Récupérer des informations sur la session du mode de sauvegarde sur le serveur

   Récupérez des informations sur l’opération à l’aide de l’ `BackupModeResult` objet renvoyé. Les informations que vous pouvez récupérer après avoir passé en mode de sauvegarde peuvent s’avérer utiles pour l’intégration à vos procédures de sauvegarde. Par exemple, le libellé, l’ID de sauvegarde et l’heure de début peuvent être utiles comme entrée pour les noms de fichier de votre procédure de sauvegarde.

### Quitter le mode de sauvegarde à l’aide de l’API du service Web {#leave-backup-mode-using-the-web-service-api}

Quittez le mode de sauvegarde à l’aide de l’API Service de sauvegarde et de restauration (service Web) :

1. Inclure les fichiers de projet

   Pour utiliser les services Web, vous devez vous assurer d’inclure les fichiers proxy. Procédez comme suit pour configurer votre projet afin d’utiliser l’API du service de sauvegarde et de restauration en tant que service Web.

   * Créez un assembly client Microsoft .NET qui utilise le WSDL de l&#39;API du service de sauvegarde et de restauration.
   * Référencez l&#39;assembly client Microsoft .NET.

1. Création d’un objet API Client BackupService

   A l&#39;aide de l&#39;assembly client Microsoft .NET, créez un `BackupServiceService` objet en appelant son constructeur par défaut.

1. Passer en mode de sauvegarde

   Quittez le mode de sauvegarde en appelant l’opération de service `leaveBackupMode` Web.

1. Récupérer des informations sur la session du mode de sauvegarde sur le serveur

   Récupérez l&#39;identifiant du mode de sauvegarde après l&#39;opération pour vérifier qu&#39;elle a réussi. Les informations que vous pouvez récupérer après avoir quitté le mode de sauvegarde peuvent s’avérer utiles pour l’intégration à vos procédures de sauvegarde.

