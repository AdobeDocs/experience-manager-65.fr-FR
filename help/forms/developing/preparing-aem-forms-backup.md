---
title: Préparation de AEM Forms pour la sauvegarde
seo-title: Préparation de AEM Forms pour la sauvegarde
description: Découvrez comment utiliser le service Sauvegarde et restauration pour passer en mode Sauvegarde et quitter le mode Sauvegarde du serveur AEM Forms à l’aide de l’API Java et de l’API Service Web.
seo-description: Découvrez comment utiliser le service Sauvegarde et restauration pour passer en mode Sauvegarde et quitter le mode Sauvegarde du serveur AEM Forms à l’aide de l’API Java et de l’API Service Web.
uuid: b8ef2bed-62e2-4000-b55a-30d2fc398a5f
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: e747147e-e96d-43c7-87b3-55947eef81f5
translation-type: tm+mt
source-git-commit: 9cf46a26d2aa2e41b924a4de89cf8ab5fdeeefc6
workflow-type: tm+mt
source-wordcount: '2554'
ht-degree: 2%

---


# Préparation de AEM Forms pour la sauvegarde {#preparing-aem-forms-for-backup}

**Les exemples et exemples de ce document ne concernent que l’environnement AEM Forms on JEE.**

## À propos du service de sauvegarde et de restauration {#about-the-backup-and-restore-service}

Le service Sauvegarde et restauration vous permet de mettre AEM Forms en *mode de sauvegarde*, ce qui permet d&#39;effectuer des sauvegardes à chaud. Le service Sauvegarde et restauration n&#39;effectue pas de sauvegarde d&#39;AEM Forms ou ne restaure pas votre système. Il place plutôt votre serveur dans un état permettant des sauvegardes cohérentes et fiables tout en permettant à votre serveur de continuer à fonctionner. Vous êtes responsable des actions de sauvegarde de l’Enregistrement de Document global (GDS) et de la base de données connectée au serveur Forms. Le répertoire de stockage global de documents est un répertoire utilisé pour stocker les fichiers utilisés dans un processus de longue durée.

Le mode de sauvegarde est l’état où le serveur entre, de sorte que les fichiers du répertoire de stockage global de documents ne soient pas purgés pendant une procédure de sauvegarde. Au lieu de cela, les sous-répertoires sont créés sous le répertoire de stockage global de documents afin de conserver un enregistrement des fichiers à purger après la fin du mode de sauvegarde. Un fichier est destiné à survivre aux redémarrages du système et peut s&#39;étendre sur plusieurs jours, voire plusieurs années. Ces fichiers constituent une partie essentielle de l’état global du serveur Forms et peuvent inclure des fichiers PDF, des stratégies ou des modèles de formulaires. Si l’un de ces fichiers est perdu ou endommagé, les processus sur le serveur Forms peuvent devenir instables et les données risquent d’être perdues.

Vous pouvez choisir d&#39;effectuer des sauvegardes de type instantané, où vous passez généralement en mode de sauvegarde pendant un certain temps, puis quitter le mode de sauvegarde une fois vos activités de sauvegarde terminées. Il est nécessaire de quitter le mode de sauvegarde pour purger les fichiers du répertoire de stockage global de documents afin de s’assurer qu’ils ne s’agrandissent pas inutilement. Vous pouvez soit quitter explicitement le mode de sauvegarde, soit attendre l’expiration du délai lors d’une session du mode de sauvegarde.

Vous pouvez également laisser votre serveur en mode de sauvegarde perpétuelle, ce qui est typique pour les stratégies de sauvegarde pour les sauvegardes restauration ou la couverture système continue. Le mode de sauvegarde restauration indique que le système est toujours en mode de sauvegarde et qu’une nouvelle session du mode de sauvegarde est lancée dès que la session précédente est libérée. En mode de sauvegarde continue, un fichier est purgé après deux sessions du mode de sauvegarde et n’est plus référencé.

Vous pouvez utiliser le service Sauvegarde et restauration pour ajouter des applications existantes ou de nouvelles applications que vous créez afin d’effectuer des sauvegardes du répertoire de stockage global de documents ou de la base de données connectée au serveur Forms.

>[!NOTE]
>
>Comme pour tout autre aspect de votre mise en oeuvre AEM Forms, votre stratégie de sauvegarde et de récupération doit être développée et testée dans un environnement de développement ou d’évaluation avant d’être utilisée en production pour s’assurer que la solution complète fonctionne comme prévu sans perte de données.

Vous pouvez exécuter ces tâches à l’aide du service Sauvegarde et restauration :

* Passez en mode de sauvegarde.
* Quittez le mode de sauvegarde.

>[!NOTE]
>
>Pour plus d’informations sur ce que vous devez prendre en compte lors des sauvegardes pour AEM Forms, voir [Aide à l’administration](https://www.adobe.com/go/learn_aemforms_admin_63).

>[!NOTE]
>
>Pour plus d’informations sur le service Sauvegarde et restauration, voir [Guide de référence des services pour AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Saisie du mode de sauvegarde sur le serveur Forms {#entering-backup-mode-on-the-forms-server}

Vous entrez en mode de sauvegarde pour autoriser les sauvegardes à chaud d’un serveur Forms. Lorsque vous passez en mode de sauvegarde, vous spécifiez les informations suivantes en fonction des procédures de sauvegarde de votre entreprise :

* Libellé unique permettant d’identifier la session du mode de sauvegarde qui peut être utile pour vos processus de sauvegarde.
* Heure de fin de la procédure de sauvegarde.
* Indicateur qui indique si vous êtes en mode de sauvegarde continue, ce qui n’est utile que si vous effectuez des sauvegardes en continu.

Avant d’écrire des applications pour passer en mode de sauvegarde, il est recommandé de comprendre les procédures de sauvegarde qui seront utilisées après avoir mis le serveur Forms en mode de sauvegarde. Pour plus d’informations sur ce que vous devez prendre en compte lors des sauvegardes pour AEM Forms, voir [Aide à l’administration](https://www.adobe.com/go/learn_aemforms_admin_63).

>[!NOTE]
>
>Pour plus d’informations sur le service Sauvegarde et restauration, voir [Guide de référence des services pour AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary-of-steps}

Pour créer une application qui passe en mode de sauvegarde, procédez comme suit :

1. Incluez des fichiers de projet.
1. Créez un objet client BackupService.
1. Déterminez une étiquette unique, le temps nécessaire pour effectuer la sauvegarde et si vous souhaitez passer en mode de sauvegarde continue.
1. Passez en mode de sauvegarde.
1. (Facultatif) Récupérez des informations sur la session du mode de sauvegarde sur le serveur.
1. Effectuez la sauvegarde du répertoire de stockage global de données et de la base de données.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Ces fichiers sont importants à inclure dans votre projet pour compiler correctement votre code et utiliser l’API du service de sauvegarde et de restauration.

Pour plus d’informations sur l’emplacement de ces fichiers, voir [Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Création d’un objet API Client BackupService**

Pour quitter le mode de sauvegarde par programmation, vous créez un objet client BackupService pour utiliser l’API Service de sauvegarde et de restauration.

**Choisissez une étiquette unique, déterminez la durée d’exécution de la sauvegarde et décidez si vous êtes en mode de sauvegarde continue.**

Avant de passer en mode de sauvegarde, vous devez choisir une étiquette unique, déterminer le temps que vous souhaitez allouer pour effectuer la sauvegarde et décider si vous souhaitez que le serveur Forms reste en mode de sauvegarde. Ces considérations sont importantes pour l’intégration aux procédures de sauvegarde établies par votre organisation. (Voir [Aide à l&#39;administration](https://www.adobe.com/go/learn_aemforms_admin_63).)

**Passer en mode de sauvegarde**

Passez en mode de sauvegarde avec les paramètres compatibles avec les procédures de sauvegarde de votre entreprise.

**Récupérer des informations sur la session du mode de sauvegarde sur le serveur**

Une fois que vous êtes en mode de sauvegarde, vous pouvez récupérer des informations sur la session. Ces informations peuvent être utilisées pour l&#39;intégration à vos procédures de sauvegarde

**Effectuer la sauvegarde du répertoire de stockage global de documents et de la base de données**

Une fois que vous êtes en mode de sauvegarde, vous pouvez effectuer une sauvegarde du répertoire de stockage global de Documents (GDS) et de la base de données à laquelle le serveur Forms est connecté. Cette étape est spécifique à votre organisation, car vous pouvez effectuer cette étape manuellement ou exécuter d&#39;autres outils pour effectuer la procédure de sauvegarde.

### Passer en mode de sauvegarde à l’aide de l’API Java {#enter-backup-mode-using-the-java-api}

Passez en mode de sauvegarde à l’aide de l’API Service de sauvegarde et de restauration :

1. Inclure les fichiers de projet

   Incluez les fichiers JAR client nécessaires, tels que adobe-backup-restore-client-sdk.jar, dans le chemin de classe de votre projet Java. Pour créer l’application cliente Java, les fichiers JAR suivants doivent être ajoutés au chemin de classe de votre projet :

   * adobe-backup-restore-client-sdk.jar
   * adobe-livecycle-client.jar
   * adobe-usermanager-client.jar
   * adobe-utilities.jar (requis si AEM Forms est déployé sur JBoss Application Server)
   * jbossall-client.jar (requis si AEM Forms est déployé sur JBoss Application Server)

1. Création d’un objet API Client BackupService

   Vous utilisez ensemble un objet `ServiceClientFactory` et l&#39;objet API client BackupService.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion. (Voir [Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
   * Créez un objet `BackupService` en utilisant son constructeur et en transmettant l&#39;objet `ServiceClientFactory`.

1. Choisissez une étiquette unique, déterminez la durée d’exécution de la sauvegarde et décidez si vous êtes en mode de sauvegarde continue.

   Choisissez une étiquette unique, déterminez le temps que vous souhaitez allouer pour effectuer la sauvegarde et décidez si vous souhaitez que le serveur Forms reste en mode de sauvegarde continue.

1. Passer en mode de sauvegarde

   Passez en mode de sauvegarde en appelant la méthode `enterBackupMode` avec les paramètres suivants :

   * Valeur `String` qui spécifie un libellé lisible par un utilisateur unique qui identifie la session du mode de sauvegarde. Il est recommandé de ne pas utiliser d’espaces ou de caractères qui ne peuvent pas être codés au format XML.
   * Valeur `int` qui spécifie le nombre de minutes de maintien en mode de sauvegarde. Vous pouvez spécifier une valeur comprise entre `1` et `10080` (nombre de minutes par semaine). Cette valeur est ignorée lors de l’utilisation du mode de sauvegarde continue.
   * Valeur `Boolean` qui spécifie si le mode de sauvegarde continue doit être activé. La valeur `True` indique qu’elle est en mode de sauvegarde continu. En mode de sauvegarde continue, la valeur que vous spécifiez pour le nombre de minutes de maintien en mode de sauvegarde est ignorée.

      Le mode de sauvegarde permanent signifie qu’une nouvelle session du mode de sauvegarde est démarrée une fois la session en cours terminée. La valeur `False` signifie que le mode de sauvegarde continue n’est pas utilisé et que, après avoir quitté le mode de sauvegarde, la purge des fichiers du répertoire de stockage global de documents reprend.

1. Récupérer des informations sur la session du mode de sauvegarde sur le serveur

   Récupérez des informations à l&#39;aide de l&#39;objet `BackupModeEntryResult` renvoyé après avoir appelé la méthode `enterBackupMode`. Les informations que vous pouvez récupérer après avoir passé en mode de sauvegarde peuvent s&#39;avérer utiles pour l&#39;intégration à vos procédures de sauvegarde. Par exemple, l’étiquette, l’identifiant de sauvegarde et le temps de début peuvent être utiles en entrée pour les noms de fichier de votre procédure de sauvegarde.

1. Effectuer la sauvegarde du répertoire de stockage global de documents et de la base de données

   Sauvegardez le répertoire de stockage global de Documents (GDS) et la base de données à laquelle votre serveur Forms est connecté. Les actions permettant d’effectuer la sauvegarde ne font pas partie du SDK AEM Forms et peuvent même inclure des étapes manuelles spécifiques aux procédures de sauvegarde de votre entreprise.

### Passer en mode de sauvegarde à l’aide de l’API de service Web {#enter-backup-mode-using-the-web-service-api}

Passez en mode de sauvegarde en utilisant le service Web fourni par l’API Service de sauvegarde et de restauration :

1. Inclure les fichiers de projet

   * Créez un assembly client Microsoft .NET qui consomme le fichier WSDL de l&#39;API du service de sauvegarde et de restauration.
   * Référencez l&#39;assembly client Microsoft .NET.

1. Création d’un objet API Client BackupService

   A l&#39;aide de l&#39;assembly client Microsoft .NET, créez un objet `BackupServiceService` en appelant son constructeur par défaut et spécifiez les informations d&#39;identification à l&#39;aide de la méthode `Credentials`.

1. Choisissez une étiquette unique, déterminez la durée d’exécution de la sauvegarde et décidez si vous êtes en mode de sauvegarde continue.

   Choisissez une étiquette unique, déterminez le temps que vous souhaitez allouer pour effectuer la sauvegarde et décidez si vous souhaitez que le serveur Forms reste en mode de sauvegarde continue.

1. Passer en mode de sauvegarde

   Pour passer en mode de sauvegarde, appelez la méthode enterBackupMode et transmettez les valeurs suivantes :

   * Valeur `String` qui spécifie un libellé lisible par un utilisateur unique qui identifie la session du mode de sauvegarde. Il est recommandé de ne pas utiliser d’espaces ou de caractères qui ne peuvent pas être codés au format XML.
   * Valeur `Uint32` qui spécifie le nombre de minutes de maintien en mode de sauvegarde. Vous pouvez spécifier une valeur comprise entre `1` et `10080` (nombre de minutes par semaine). Cette valeur est ignorée lors de l’utilisation du mode de sauvegarde continue.
   * Valeur `Boolean` qui spécifie si le mode de sauvegarde continue doit être activé. La valeur `True` indique qu’elle est en mode de sauvegarde continu. En mode de sauvegarde continue, la valeur que vous spécifiez pour le nombre de minutes de maintien en mode de sauvegarde est ignorée. Le mode de sauvegarde permanent signifie qu’une nouvelle session du mode de sauvegarde est démarrée une fois la session en cours terminée.

      La valeur `False` signifie que le mode de sauvegarde continue n’est pas utilisé et que, après avoir quitté le mode de sauvegarde, la purge des fichiers du répertoire de stockage global de documents reprend.

1. Récupérer des informations sur la session du mode de sauvegarde sur le serveur

   Récupérez des informations sur la session du mode de sauvegarde après avoir appelé la méthode enterBackupMode à partir de BackupModeEntryResult renvoyé pour vérifier qu&#39;elle a réussi. Les informations que vous pouvez récupérer après avoir passé en mode de sauvegarde peuvent s&#39;avérer utiles pour l&#39;intégration à vos procédures de sauvegarde. Par exemple, l’étiquette, l’identifiant de sauvegarde et le temps de début peuvent être utiles en entrée pour les noms de fichier de votre procédure de sauvegarde.

1. Effectuer la sauvegarde du répertoire de stockage global de documents et de la base de données

   Sauvegardez le répertoire de stockage global de Documents (GDS) et la base de données à laquelle votre serveur Forms est connecté. Les actions permettant d’effectuer la sauvegarde ne font pas partie du SDK AEM Forms et peuvent même inclure des étapes manuelles spécifiques aux procédures de sauvegarde de votre entreprise.

## Quitter le mode de sauvegarde sur le serveur de formulaires {#leaving-backup-mode-on-the-forms-server}

Vous quittez le mode de sauvegarde afin que le serveur Forms puisse à nouveau purger les fichiers du répertoire de stockage global de documents (Enregistrement de Document global) sur le serveur Forms.

Avant d’écrire des demandes pour passer en mode de sortie, il est recommandé de comprendre les procédures de sauvegarde utilisées avec AEM Forms. Pour plus d’informations sur ce que vous devez prendre en compte lors des sauvegardes pour AEM Forms, voir [Aide à l’administration](https://www.adobe.com/go/learn_aemforms_admin_63).

>[!NOTE]
>
>Pour plus d’informations sur le service Sauvegarde et restauration, voir [Guide de référence des services pour AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary_of_steps-1}

Pour quitter le mode de sauvegarde, effectuez les étapes suivantes :

1. Incluez des fichiers de projet.
1. Créez un objet client BackupService.
1. Quittez le mode de sauvegarde.
1. (Facultatif) Récupérez des informations sur la session du mode de sauvegarde qui s’exécutait sur le serveur Forms.

**Inclure les fichiers de projet**

Incluez tous les fichiers nécessaires dans votre projet de développement. Ces fichiers sont importants pour la compilation correcte de votre code et l’utilisation de l’API Service de sauvegarde et de restauration.

Pour plus d’informations sur l’emplacement de ces fichiers, voir [Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Création d’un objet API Client BackupService**

Pour quitter le mode de sauvegarde par programmation, vous créez un objet client BackupService pour utiliser l’API Service de sauvegarde et de restauration.

**Quitter le mode de sauvegarde**

Quittez le mode de sauvegarde pour reprendre la purge normale des fichiers de l’Enregistrement de Document global (GDS). Avant de quitter le mode de sauvegarde, vous devez vérifier que vos procédures de sauvegarde sont terminées.

**Récupérer les informations sur la session du mode de sauvegarde qui s&#39;est terminée**

Après avoir quitté le mode de sauvegarde, vous pouvez récupérer des informations sur la session. Ces informations peuvent être utilisées pour l&#39;intégration à vos procédures de sauvegarde.

### Quitter le mode de sauvegarde à l’aide de l’API Java {#leave-backup-mode-using-the-java-api}

Quittez le mode de sauvegarde en utilisant l’API du service de sauvegarde et de restauration (Java) :

1. Inclure les fichiers de projet

   Incluez les fichiers JAR client nécessaires, tels que adobe-backup-restore-client-sdk.jar, dans le chemin de classe de votre projet Java. Pour créer une application cliente Java, les fichiers JAR suivants doivent être ajoutés au chemin de classe de votre projet :

   * adobe-backup-restore-client-sdk.jar
   * adobe-livecycle-client.jar
   * adobe-usermanager-client.jar
   * adobe-utilities.jar (requis si AEM Forms est déployé sur JBoss Application Server)
   * jbossall-client.jar (requis si AEM Forms est déployé sur JBoss Application Server)

1. Création d’un objet API Client BackupService

   Vous utilisez ensemble un objet `ServiceClientFactory` et l&#39;objet API client BackupService.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion. (Voir [Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
   * Créez un objet `BackupService` en utilisant son constructeur et en transmettant l&#39;objet `ServiceClientFactory` en tant que paramètre.

1. Passer en mode de sauvegarde

   Quittez le mode de sauvegarde en appelant la méthode `leaveBackupMode`.

1. Récupérer des informations sur la session du mode de sauvegarde sur le serveur

   Récupérez des informations sur l&#39;opération à l&#39;aide de l&#39;objet `BackupModeResult` renvoyé. Les informations que vous pouvez récupérer après avoir passé en mode de sauvegarde peuvent s&#39;avérer utiles pour l&#39;intégration à vos procédures de sauvegarde. Par exemple, l’étiquette, l’identifiant de sauvegarde et le temps de début peuvent être utiles en entrée pour les noms de fichier de votre procédure de sauvegarde.

### Quitter le mode de sauvegarde à l’aide de l’API de service Web {#leave-backup-mode-using-the-web-service-api}

Quittez le mode de sauvegarde à l’aide de l’API Service de sauvegarde et de restauration (service Web) :

1. Inclure les fichiers de projet

   Pour utiliser les services Web, vous devez vous assurer d’inclure les fichiers proxy. Suivez ces étapes pour configurer votre projet afin d’utiliser l’API Service de sauvegarde et de restauration en tant que service Web.

   * Créez un assembly client Microsoft .NET qui consomme le fichier WSDL de l&#39;API du service de sauvegarde et de restauration.
   * Référencez l&#39;assembly client Microsoft .NET.

1. Création d’un objet API Client BackupService

   A l&#39;aide de l&#39;assembly client Microsoft .NET, créez un objet `BackupServiceService` en appelant son constructeur par défaut.

1. Passer en mode de sauvegarde

   Quittez le mode de sauvegarde en appelant l&#39;opération de service Web `leaveBackupMode`.

1. Récupérer des informations sur la session du mode de sauvegarde sur le serveur

   Récupérez l&#39;identifiant du mode de sauvegarde après l&#39;opération pour vérifier qu&#39;elle a réussi. Les informations que vous pouvez récupérer après avoir quitté le mode de sauvegarde peuvent s’avérer utiles pour l’intégration à vos procédures de sauvegarde.

