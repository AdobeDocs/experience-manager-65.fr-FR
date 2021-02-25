---
title: Gestion par programmation des points de terminaison
seo-title: Gestion par programmation des points de terminaison
description: Utilisez le service Endpoint Registry pour ajouter des points de terminaison EJB, ajouter des points de terminaison SOAP, ajouter des points de terminaison Watched Folder, ajouter des points de terminaison E-mail, ajouter des points de terminaison Remoting, ajouter des points de terminaison Tâche Manager, modifier des points de terminaison, supprimer des points de terminaison et récupérer les informations du connecteur de point de terminaison.
seo-description: Utilisez le service Endpoint Registry pour ajouter des points de terminaison EJB, ajouter des points de terminaison SOAP, ajouter des points de terminaison Watched Folder, ajouter des points de terminaison E-mail, ajouter des points de terminaison Remoting, ajouter des points de terminaison Tâche Manager, modifier des points de terminaison, supprimer des points de terminaison et récupérer les informations du connecteur de point de terminaison.
uuid: 5dc50946-3323-4c5d-a43b-31c1c980bd04
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 076889a7-9c9f-4b6f-a45b-67a9b3923c36
translation-type: tm+mt
source-git-commit: 9cf46a26d2aa2e41b924a4de89cf8ab5fdeeefc6
workflow-type: tm+mt
source-wordcount: '10863'
ht-degree: 6%

---


# Gestion par programmation des points de terminaison {#programmatically-managing-endpoints}

**Les exemples et exemples de ce document ne concernent que l’environnement AEM Forms on JEE.**

**À propos du service de registre des points de terminaison**

Le service de registre des points de terminaison permet de gérer les points de terminaison par programmation. Vous pouvez, par exemple, ajouter les types de points de fin suivants à un service :

* EJB
* méthode d’objet
* Watched Folder
* Courrier électronique
* (Obsolète pour les formulaires AEM) Remoting
* Gestionnaire de tâches

>[!NOTE]
>
>Les points de terminaison SOAP, EJB et (obsolète pour AEM forms on JEE) Remoting sont automatiquement créés pour chaque service activé. Les points de terminaison SOAP et EJB activent SOAP et EJB pour toutes les opérations de service.

Un point de terminaison Remoting permet aux clients Flex d’appeler des opérations sur le service AEM Forms auquel le point de terminaison est ajouté. Une destination Flex portant le même nom que le point de terminaison est créée et les clients Flex peuvent créer des objets RemoteObjects pointant vers cette destination pour appeler des opérations sur le service approprié.

Les points de fin Email, Tâche Manager et Watched Folder n’exposent qu’une opération spécifique du service. Pour Ajouter ces points de terminaison, une deuxième étape de configuration est nécessaire pour sélectionner une méthode à appeler, définir des paramètres de configuration et spécifier les mappages des paramètres d’entrée et de sortie.

Vous pouvez organiser les points de terminaison TaskManager en groupes appelés *catégories*. Ces catégories sont ensuite exposées à Workspace par le biais de TaskManager, les utilisateurs finaux visualisant les points de terminaison TaskManager tels qu’ils sont classés. Dans Workspace, les utilisateurs finaux voient ces catégories dans le volet de navigation. Les points de fin de chaque catégorie sont affichés sous forme de cartes de processus sur la page Processus de Début dans Workspace.

Vous pouvez accomplir ces tâches à l’aide du service de registre des points de terminaison :

* Ajoutez des points de terminaison EJB. (Voir [Ajouter les points de terminaison EJB](programmatically-endpoints.md#adding-ejb-endpoints).)
* Ajoutez des points de terminaison SOAP. (Voir [Ajouter des points de terminaison SOAP](programmatically-endpoints.md#adding-soap-endpoints).)
* Ajoutez des points de terminaison Watched Folder (voir [Ajouter des points de terminaison Watched Folder](programmatically-endpoints.md#adding-watched-folder-endpoints)).
* Ajouter les points de fin de courrier électronique. (Voir [Ajouter des points de terminaison de courriel](programmatically-endpoints.md#adding-email-endpoints).)
* Ajouter les points de terminaison Remoting. (Voir [Ajouter des points de terminaison distants](programmatically-endpoints.md#adding-remoting-endpoints).)
* Ajoutez les points de terminaison TaskManager (voir [Ajouter les points de terminaison TaskManager](programmatically-endpoints.md#adding-taskmanager-endpoints)).
* Modifier les points de terminaison (voir [Modification des points de terminaison](programmatically-endpoints.md#modifying-endpoints)).
* Supprimer des points de terminaison (voir [Suppression des points de terminaison](programmatically-endpoints.md#removing-endpoints)).
* Récupérez les informations du connecteur du point de terminaison (voir [Récupération des informations du connecteur du point de terminaison](programmatically-endpoints.md#retrieving-endpoint-connector-information).)

## Ajouter des points de terminaison EJB {#adding-ejb-endpoints}

Vous pouvez ajouter par programmation un point de terminaison EJB à un service en utilisant l’API Java AEM Forms. En ajoutant un point de terminaison EJB à un service, vous activez une application cliente pour appeler le service en utilisant le mode EJB. En d’autres termes, lorsque vous définissez les propriétés de connexion requises pour appeler AEM Forms, vous pouvez sélectionner le mode EJB. (Voir [Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)

>[!NOTE]
>
>Vous ne pouvez pas ajouter de point de terminaison EJB à l’aide de services Web.

>[!NOTE]
>
>En règle générale, un point de terminaison EJB est ajouté par défaut à un service. Cependant, un point de terminaison EJB peut être ajouté à un processus qui est déployé par programmation ou lorsqu’un point de terminaison EJB a été supprimé et doit être de nouveau ajouté.

### Résumé des étapes {#summary-of-steps}

Pour ajouter un point de terminaison EJB à un service, effectuez les tâches suivantes :

1. Incluez des fichiers de projet.
1. Créez un objet `EndpointRegistry Client`.
1. Définissez les attributs des points de terminaison EJB.
1. Créez un point de terminaison EJB.
1. Activez le point de terminaison.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Les fichiers JAR suivants doivent être ajoutés au chemin de classe de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (requis si AEM Forms est déployé sur JBoss Application Server)
* jbossall-client.jar (requis si AEM Forms est déployé sur JBoss Application Server)

Pour plus d’informations sur l’emplacement de ces fichiers JAR, voir [Inclusion de fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Création d’un objet Client EndpointRegistry**

Avant de pouvoir ajouter par programmation un point de terminaison EJB, vous devez créer un objet `EndpointRegistryClient`.

**Définition des attributs de point de fin EJB**

Pour créer un point de terminaison EJB pour un service, spécifiez les valeurs suivantes :

* **Identificateur** du connecteur : Indique le type de point de terminaison à créer. Pour créer un point de terminaison EJB, spécifiez `EJB`.
* **Description** : Indique la description du point de terminaison.
* **Nom** : Indique le nom du point de terminaison.
* **Identificateur** de service : Spécifie le service auquel le point de terminaison appartient.
* **Nom** de l&#39;opération : Indique le nom de l’opération appelée à l’aide du point de terminaison. Lors de la création d’un point de terminaison EJB, spécifiez un caractère générique ( `*`). Cependant, si vous souhaitez spécifier une opération spécifique plutôt que d&#39;appeler toutes les opérations de service, indiquez le nom de l&#39;opération plutôt que d&#39;utiliser le caractère générique ( `*`).

**Création d’un point de terminaison EJB**

Après avoir défini les attributs de point de terminaison EJB, vous pouvez créer un point de terminaison EJB pour un service.

**Activer le point de terminaison**

Après avoir créé un nouveau point de terminaison, vous devez l’activer. Après avoir activé le point de terminaison, il peut être utilisé pour appeler le service. Après avoir activé le point de terminaison, vous pouvez le vue dans Administration Console.

**Voir également**

[Ajouter un point de terminaison EJB à l’aide de l’API Java](programmatically-endpoints.md#adding-an-ejb-endpoint-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Ajouter un point de terminaison EJB à l’aide de l’API Java {#adding-an-ejb-endpoint-using-the-java-api}

Ajoutez un point de terminaison EJB à l’aide de l’API Java :

1. Incluez des fichiers de projet.

   Incluez des fichiers JAR client, tels que adobe-livecycle-client.jar, dans le chemin de classe de votre projet Java. (

1. Créez un objet Client EndpointRegistry.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `EndpointRegistryClient` en utilisant son constructeur et en transmettant l&#39;objet `ServiceClientFactory`.

1. Définissez les attributs des points de terminaison EJB.

   * Créez un objet `CreateEndpointInfo` en utilisant son constructeur.
   * Spécifiez la valeur de l’identifiant du connecteur en appelant la méthode `CreateEndpointInfo` de l’objet `setConnectorId` et en transmettant la valeur de chaîne `EJB`.
   * Spécifiez la description du point de terminaison en appelant la méthode `CreateEndpointInfo` de l’objet `setDescription` et en transmettant une valeur de chaîne qui décrit le point de terminaison.
   * Spécifiez le nom du point de terminaison en appelant la méthode `CreateEndpointInfo` de l’objet `setName` et en transmettant une valeur de chaîne qui spécifie le nom.
   * Spécifiez le service auquel appartient le point de terminaison en appelant la méthode `CreateEndpointInfo` de l’objet `setServiceId` et en transmettant une valeur de chaîne qui spécifie le nom du service.
   * Spécifiez l’opération appelée en appelant la méthode `CreateEndpointInfo` de l’objet `setOperationName` et transmettez une valeur de chaîne qui spécifie le nom de l’opération. Pour les points de fin SOAP et EJB, spécifiez un caractère générique ( `*`), ce qui implique toutes les opérations.

1. Créez un point de terminaison EJB.

   Créez le point de terminaison en appelant la méthode `EndpointRegistryClient` de l’objet `createEndpoint` et en transmettant l’objet `CreateEndpointInfo`. Cette méthode renvoie un objet `Endpoint` qui représente le nouveau point de terminaison EJB.

1. Activez le point de terminaison.

   Activez le point de terminaison en appelant la méthode d’activation de l’objet `EndpointRegistryClient` et en transmettant l’objet `Endpoint` renvoyé par la méthode `createEndpoint`.

**Voir également**

[Résumé des étapes](programmatically-endpoints.md#summary-of-steps)

[QuickStart : Ajouter un point de terminaison EJB à l’aide de l’API Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-an-ejb-endpoint-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Ajouter des points de terminaison SOAP {#adding-soap-endpoints}

Vous pouvez ajouter par programmation un point de terminaison SOAP à un service à l’aide de l’API Java AEM Forms. En ajoutant un point de terminaison SOAP, vous activez une application cliente pour appeler le service en utilisant le mode SOAP. En d’autres termes, lorsque vous définissez les propriétés de connexion requises pour appeler AEM Forms, vous pouvez sélectionner le mode SOAP.

>[!NOTE]
>
>Vous ne pouvez pas ajouter de point de terminaison SOAP à l’aide de services Web.

>[!NOTE]
>
>En règle générale, un point de terminaison SOAP est ajouté par défaut à un service. Cependant, un point de terminaison SOAP peut être ajouté à un processus qui est déployé par programmation ou lorsqu’un point de terminaison SOAP a été supprimé et doit être de nouveau ajouté.

### Résumé des étapes {#summary_of_steps-1}

Pour ajouter un point de terminaison SOAP à un service, effectuez les tâches suivantes :

1. Incluez des fichiers de projet.
1. Créez un objet `EndpointRegistryClient`.
1. Définissez les attributs des points de terminaison SOAP.
1. Créez un point de terminaison SOAP.
1. Activez le point de terminaison.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

Les fichiers JAR suivants doivent être ajoutés au chemin de classe de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (requis si AEM Forms est déployé sur JBoss Application Server)
* jbossall-client.jar (requis si AEM Forms est déployé sur JBoss Application Server)

Ces fichiers JAR sont nécessaires pour créer un point de terminaison SOAP. Cependant, vous avez besoin de fichiers JAR supplémentaires si vous utilisez le point de terminaison SOAP pour appeler le service. Pour plus d’informations sur les fichiers JAR AEM Forms, voir [Inclusion de fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Création d’un objet Client EndpointRegistry**

Pour ajouter par programmation un point de terminaison SOAP à un service, vous devez créer un objet `EndpointRegistryClient`.

**Définition des attributs des points de fin SOAP**

Pour ajouter un point de terminaison SOAP à un service, spécifiez les valeurs suivantes :

* **Valeur** de l’identifiant du connecteur : Indique le type de point de terminaison à créer. Pour créer un point de terminaison SOAP, spécifiez `SOAP`.
* **Description** : Indique la description du point de terminaison.
* **Nom** : Indique le nom du point de terminaison.
* **Valeur** de l&#39;identifiant de service : Spécifie le service auquel le point de terminaison appartient.
* **Nom** de l&#39;opération : Indique le nom de l’opération appelée à l’aide du point de terminaison. Lors de la création d’un point de terminaison SOAP, spécifiez un caractère générique ( `*`). Cependant, si vous souhaitez spécifier une opération spécifique plutôt que d&#39;appeler toutes les opérations de service, indiquez le nom de l&#39;opération plutôt que d&#39;utiliser le caractère générique ( `*`).

**Création d’un point de terminaison SOAP**

Après avoir défini les attributs de point de terminaison SOAP, vous pouvez créer un point de terminaison SOAP.

**Activer le point de terminaison**

Après avoir créé un nouveau point de terminaison, vous devez l’activer. Lorsque le point de terminaison est activé, il peut être utilisé pour appeler le service. Une fois le point de terminaison activé, vous pouvez le voir dans la vue d’administration Console.

**Voir également**

[Ajouter un point de terminaison SOAP à l’aide de l’API Java](programmatically-endpoints.md#add-a-soap-endpoint-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Ajouter un point de terminaison SOAP à l’aide de l’API Java {#add-a-soap-endpoint-using-the-java-api}

Ajoutez un point de terminaison SOAP à un service à l’aide de l’API Java :

1. Incluez des fichiers de projet.

   Incluez des fichiers JAR client, tels que adobe-livecycle-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un objet Client EndpointRegistry.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `EndpointRegistryClient` en utilisant son constructeur et en transmettant l&#39;objet `ServiceClientFactory`.

1. Définissez les attributs des points de terminaison SOAP.

   * Créez un objet `CreateEndpointInfo` en utilisant son constructeur.
   * Spécifiez la valeur de l’identifiant du connecteur en appelant la méthode `CreateEndpointInfo` de l’objet `setConnectorId` et en transmettant la valeur de chaîne `SOAP`.
   * Spécifiez la description du point de terminaison en appelant la méthode `CreateEndpointInfo` de l’objet `setDescription` et en transmettant une valeur de chaîne qui décrit le point de terminaison.
   * Spécifiez le nom du point de terminaison en appelant la méthode `CreateEndpointInfo` de l’objet `setName` et en transmettant une valeur de chaîne qui spécifie le nom.
   * Spécifiez le service auquel appartient le point de terminaison en appelant la méthode `CreateEndpointInfo` de l’objet `setServiceId` et en transmettant une valeur de chaîne qui spécifie le nom du service.
   * Spécifiez l’opération appelée en appelant la méthode `CreateEndpointInfo` de l’objet `setOperationName` et en transmettant une valeur de chaîne qui spécifie le nom de l’opération. Pour les points de fin SOAP et EJB, spécifiez un caractère générique ( `*`), ce qui implique toutes les opérations.

1. Créez un point de terminaison SOAP.

   Créez le point de terminaison en appelant la méthode `EndpointRegistryClient` de l’objet `createEndpoint` et en transmettant l’objet `CreateEndpointInfo`. Cette méthode renvoie un objet `Endpoint` qui représente le nouveau point de terminaison SOAP.

1. Activez le point de terminaison.

   Activez le point de terminaison en appelant la méthode d’activation de l’objet `EndpointRegistryClient` et en transmettant l’objet `Endpoint` renvoyé par la méthode `createEndpoint`.

**Voir également**

[Résumé des étapes](programmatically-endpoints.md#summary-of-steps)

[QuickStart : Ajouter un point de terminaison SOAP à l’aide de l’API Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-soap-endpoint-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Ajouter les points de terminaison du dossier de contrôle {#adding-watched-folder-endpoints}

Vous pouvez ajouter par programmation un point de terminaison Watched Folder à un service en utilisant l’API Java AEM Forms. En ajoutant un point de terminaison Watched Folder, vous permettez aux utilisateurs de placer un fichier (tel qu’un fichier PDF) dans un dossier. Lorsque le fichier est placé dans le dossier, le service configuré est alors appelé et manipule le fichier. Après que le service a effectué l’opération spécifiée, il enregistre le fichier modifié dans un dossier de sortie spécifié. Un dossier de contrôle est configuré pour être analysé à un intervalle de fréquence fixe ou selon un calendrier cron, par exemple tous les lundis, mercredis et vendredis à midi.

Pour ajouter par programmation un point de terminaison Watched Folder à un service, considérez le processus de courte durée *EncryptDocument* suivant. (Voir [Comprendre les processus AEM Forms](/help/forms/developing/aem-forms-processes.md#understanding-aem-forms-processes).)

![aw_aw_encryptdocumentprocess](assets/aw_aw_encryptdocumentprocess.png)

Ce processus accepte un document PDF non sécurisé en tant que valeur d’entrée, puis transmet le document PDF non sécurisé à l’opération `EncryptPDFUsingPassword` du service Encryption. Le document PDF est chiffré avec un mot de passe et le document PDF chiffré par mot de passe est la valeur de sortie de ce processus. Le nom de la valeur d’entrée (document PDF non sécurisé) est `InDoc` et le type de données est `com.adobe.idp.Document`. Le nom de la valeur de sortie (le document PDF chiffré par mot de passe) est `SecuredDoc` et le type de données est `com.adobe.idp.Document`.

>[!NOTE]
>
>Vous ne pouvez pas ajouter de point de terminaison Watched Folder à l’aide de services Web.

### Résumé des étapes {#summary_of_steps-2}

Pour ajouter un point de terminaison Watched Folder à un service, effectuez les tâches suivantes :

1. Incluez des fichiers de projet.
1. Créez un objet `EndpointRegistryClient`.
1. Définissez les attributs des points de fin Watched Folder.
1. Spécifiez les valeurs de configuration.
1. Définissez les valeurs des paramètres d’entrée.
1. Définissez une valeur de paramètre de sortie.
1. Créez un point de terminaison Watched Folder.
1. Activez le point de terminaison.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

Les fichiers JAR suivants doivent être ajoutés au chemin de classe de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (requis si AEM Forms est déployé sur JBoss Application Server)
* jbossall-client.jar (requis si AEM Forms est déployé sur JBoss Application Server)

Pour plus d’informations sur l’emplacement de ces fichiers JAR, voir [Inclusion de fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Création d’un objet Client EndpointRegistry**

Pour ajouter par programmation un point de terminaison Watched Folder, vous devez créer un objet `EndpointRegistryClient`.

**Définition des attributs des points de fin Watched Folder**

Pour créer un point de terminaison Watched Folder pour un service, spécifiez les valeurs suivantes :

* **Identificateur** du connecteur : Indique le type de point de terminaison créé. Pour créer un point de terminaison Watched Folder, spécifiez `WatchedFolder`.
* **Description** : Indique la description du point de terminaison.
* **Nom** : Indique le nom du point de terminaison.
* **Identificateur** de service : Spécifie le service auquel le point de terminaison appartient. Par exemple, pour ajouter un point de terminaison Watched Folder au processus introduit dans cette section (un processus devient un service lorsqu’il est activé à l’aide de Workbench), spécifiez `EncryptDocument`.
* **Nom** de l&#39;opération : Indique le nom de l’opération appelée à l’aide du point de terminaison. En règle générale, lors de la création d’un point de terminaison Watched Folder pour un service issu d’un processus créé dans Workbench, le nom de l’opération est `invoke`.

**Spécifier les valeurs de configuration**

Vous devez spécifier des valeurs de configuration pour un point de terminaison Watched Folder lors de l’ajout par programmation d’un point de terminaison Watched Folder à un service. Ces valeurs de configuration sont spécifiées par un administrateur si un point de terminaison Watched Folder est ajouté à l’aide d’Administration Console.

La liste suivante spécifie les valeurs de configuration qui sont définies lors de l’ajout par programmation d’un point de terminaison Watched Folder à un service :

* **url** : Indique l’emplacement du dossier de contrôle. Dans un environnement organisé en grappes, cette valeur doit pointer vers un dossier réseau partagé accessible à partir de chaque ordinateur de la grappe.
* **asynchrone** : Identifie le type d’appel comme étant asynchrone ou synchrone. Les processus provisoires et synchrones peuvent être appelés uniquement de façon synchrone. La valeur par défaut est true. Il est recommandé de procéder de façon asynchrone.
* **cronExpression** : Utilisé par quartz pour planifier l’interrogation du répertoire d’entrée. Pour plus d’informations sur la configuration de l’expression cron, voir [https://quartz.sourceforge.net/javadoc/org/quartz/CronTrigger.html](https://quartz.sourceforge.net/javadoc/org/quartz/CronTrigger.html).
* **purgeDuration** : Il s’agit d’un attribut obligatoire. Les fichiers et les dossiers du dossier result sont purgés lorsqu’ils sont plus anciens que cette valeur. Cette valeur est mesurée en jours. Cet attribut est utile pour s’assurer que le dossier de résultats n’est pas plein. La valeur -1 jour indique de ne jamais supprimer le dossier result. La valeur par défaut est -1.
* **repeatInterval** : Intervalle, en secondes, d’analyse du dossier de contrôle pour saisie. Si le ralentissement n’est pas activé, cette valeur doit être supérieure à la durée de traitement d’une tâche moyenne ; sinon, le système risque d&#39;être surchargé. La valeur par défaut est 5.
* **repeatCount** : Nombre de fois où un dossier de contrôle analyse le dossier ou le répertoire. La valeur -1 indique une analyse indéfinie. La valeur par défaut est -1.
* **throttleOn** : Limite le nombre de tâches du dossier de contrôle pouvant être traitées à tout moment. Le nombre maximal de tâches est déterminé par la valeur batchSize.
* **userName** : Nom d’utilisateur utilisé lors de l’appel d’un service de cible à partir du dossier de contrôle. Cette valeur est obligatoire. La valeur par défaut est SuperAdmin.
* **domainName** : Domaine de l’utilisateur. Cette valeur est obligatoire. La valeur par défaut est DefaultDom.
* **batchSize** : Nombre de fichiers ou de dossiers à sélectionner par analyse. Utilisez cette valeur pour éviter une surcharge sur le système ; l’analyse simultanée d’un trop grand nombre de fichiers peut entraîner un blocage. La valeur par défaut est 2.
* **waitTime** : Durée, en millisecondes, d’attente avant l’analyse d’un dossier ou d’un fichier après sa création. Par exemple, si le temps d’attente est de 36 000 000 millisecondes (une heure) et que le fichier a été créé il y a une minute, ce fichier est récupéré après 59 minutes ou plus. Cet attribut est utile pour s’assurer qu’un fichier ou un dossier est entièrement copié dans le dossier input. Par exemple, si vous devez traiter un fichier volumineux et que le téléchargement du fichier prend dix minutes, définissez le délai d’attente sur 10&amp;amp ; ast ; 60 &amp;amp ; ast ; 1000 millisecondes. Ce paramètre empêche le dossier de contrôle d’analyser le fichier s’il n’a pas attendu dix minutes. La valeur par défaut est 0.
* **excludeFilePattern** : modèle utilisé par un dossier de contrôle pour déterminer les fichiers et les dossiers à analyser et à sélectionner. Les fichiers ou les dossiers présentant ce modèle ne seront pas analysés en vue de leur traitement. Ce paramètre est utile lorsque l’entrée est un dossier contenant plusieurs fichiers. Le contenu du dossier peut être copié dans un dossier dont le nom sera choisi par le dossier de contrôle. Cette étape empêche le dossier de contrôle de sélectionner un dossier à traiter avant que le dossier ne soit complètement copié dans le dossier d’entrée. Par exemple, si la valeur excludeFilePattern est `data*`, tous les fichiers et dossiers correspondant à `data*` ne sont pas sélectionnés. Cela inclut les fichiers et les dossiers nommés `data1`, `data2`, etc. En outre, le modèle peut être complété par des modèles génériques pour spécifier des modèles de fichier. Le dossier de contrôle modifie l’expression régulière afin de prendre en charge les modèles de caractères génériques tels que `*.*` et `*.pdf`. Ces modèles de caractères génériques ne sont pas pris en charge par les expressions régulières.
* **includeFilePattern** : modèle utilisé par le dossier de contrôle pour déterminer les dossiers et les fichiers à analyser et à sélectionner. Par exemple, si cette valeur est `*`, tous les fichiers et dossiers correspondant à `input*` sont sélectionnés. Cela inclut les fichiers et les dossiers nommés `input1`, `input2`, etc. La valeur par défaut est `*`. Cette valeur indique tous les fichiers et dossiers. En outre, le modèle peut être complété par des modèles génériques pour spécifier des modèles de fichier. Le dossier de contrôle modifie l’expression régulière afin de prendre en charge les modèles de caractères génériques tels que `*.*` et `*.pdf`. Ces modèles de caractères génériques ne sont pas pris en charge par les expressions régulières. Cette valeur est obligatoire.
* **resultFolderName** : Dossier dans lequel les résultats enregistrés sont stockés. Cet emplacement peut être un chemin d&#39;accès absolu ou relatif au répertoire. Si les résultats ne se trouvent pas dans ce dossier, vérifiez le dossier failure. Les fichiers en lecture seule ne sont pas traités et ils sont enregistrés dans le dossier failure. La valeur par défaut est `result/%Y/%M/%D/`. Il s’agit du dossier de résultats dans le dossier de contrôle.
* **preserveFolderName** : Emplacement de stockage des fichiers après une analyse et une récupération réussies. Cet emplacement peut être absolu, relatif ou un chemin d’accès au répertoire null. La valeur par défaut est `preserve/%Y/%M/%D/`.
* **failureFolderName** : Dossier dans lequel les fichiers d’échec sont enregistrés. Cet emplacement dépend toujours du dossier de contrôle. Les fichiers en lecture seule ne sont pas traités et ils sont enregistrés dans le dossier failure. La valeur par défaut est `failure/%Y/%M/%D/`.
* **preserveOnFailure** : Conserver les fichiers d’entrée en cas d’échec de l’exécution de l’opération sur un service. La valeur par défaut est true.
* **overwriteDuplicateFilename** : Lorsqu’elle est définie sur true, les fichiers du dossier de résultats et du dossier preserve sont remplacés. Lorsqu’elle est définie sur false, le nom est associé à des fichiers et des dossiers contenant un suffixe d’index numérique. La valeur par défaut est false. 

**Définir les valeurs des paramètres d’entrée**

Lors de la création d’un point de terminaison Watched Folder, vous devez définir les valeurs des paramètres d’entrée. En d’autres termes, vous devez décrire les valeurs d’entrée transmises à l’opération appelée par le dossier de contrôle. Prenons l’exemple du processus introduit dans cette rubrique. Il possède une valeur d’entrée nommée `InDoc` et son type de données est `com.adobe.idp.Document`. Lors de la création d’un point de terminaison Watched Folder pour ce processus (une fois qu’un processus est activé, il devient un service), vous devez définir la valeur du paramètre d’entrée.

Pour définir les valeurs des paramètres d’entrée requises pour un point de terminaison Watched Folder, spécifiez les valeurs suivantes :

**Nom** du paramètre d&#39;entrée : Nom du paramètre d’entrée. Le nom d’une valeur d’entrée est spécifié dans Workbench pour un processus. Si la valeur d’entrée appartient à une opération de service (service qui n’est pas un processus créé dans Workbench), le nom d’entrée est spécifié dans le fichier component.xml. Par exemple, le nom du paramètre d’entrée pour le processus introduit dans cette section est `InDoc`.

**Type** de mappage : Permet de configurer les valeurs d’entrée requises pour appeler l’opération de service. Il existe deux types de mappage :

* `Literal`: Le point de terminaison Watched Folder utilise la valeur saisie dans le champ telle qu’elle est affichée. Tous les types Java de base sont pris en charge. Par exemple, si une API utilise des entrées telles que String, long, int et Boolean, la chaîne est convertie en type approprié et le service est appelé.
* `Variable`: la valeur saisie est un modèle de fichier que le dossier de contrôle utilise pour sélectionner l’entrée. Par exemple, si vous sélectionnez Variable pour le type de mappage et que le document d’entrée doit être un fichier PDF, vous pouvez spécifier `*.pdf`comme valeur de mappage.

**Valeur** de mappage : Indique la valeur du type de mappage. Par exemple, si vous sélectionnez un type de mappage `Variable`, vous pouvez spécifier `*.pdf` comme modèle de fichier.

**Type** de données : Indique le type de données des valeurs d’entrée. Par exemple, le type de données de la valeur d’entrée du processus introduit dans cette section est `com.adobe.idp.Document`.

**Définir une valeur de paramètre de sortie**

Lors de la création d’un point de terminaison Watched Folder, vous devez définir une valeur de paramètre de sortie. Autrement dit, vous devez décrire la valeur de sortie renvoyée par le service appelé par le point de terminaison Watched Folder. Prenons l’exemple du processus introduit dans cette rubrique. Il a une valeur de sortie `SecuredDoc` et son type de données est `com.adobe.idp.Document`. Lors de la création d’un point de terminaison Watched Folder pour ce processus (une fois qu’un processus est activé, il devient un service), vous devez définir la valeur du paramètre de sortie.

Pour définir une valeur de paramètre de sortie requise pour un point de terminaison Watched Folder, spécifiez les valeurs suivantes :

**Nom** du paramètre de sortie : Nom du paramètre de sortie. Le nom d’une valeur de sortie de processus est spécifié dans Workbench. Si la valeur de sortie appartient à une opération de service (service qui n’est pas un processus créé dans Workbench), le nom de sortie est spécifié dans le fichier component.xml. Par exemple, le nom du paramètre de sortie pour le processus introduit dans cette section est `SecuredDoc`.

**Type** de mappage : Permet de configurer la sortie du service et de l’opération. Les options suivantes sont disponibles :

* Si le service renvoie un seul objet (un seul document), le modèle est `%F.pdf` et la destination source est nom_fichier_source.pdf. Par exemple, le processus introduit dans cette section renvoie un seul document. Par conséquent, le type de mappage peut être défini comme `%F.pdf` ( `%F` signifie utiliser le nom de fichier donné). Le modèle `%E` spécifie l&#39;extension du document d&#39;entrée.
* Si le service renvoie une liste, le modèle est `Result\%F\` et la destination source est Result\sourcefilename\source1 (output 1) et Result\sourcefilename\source2 (output 2).
* Si le service renvoie un mappage, le modèle est `Result\%F\` et la destination source est Result\sourcefilename\file1 and Result\sourcefilename\file2. Si le mappage comporte plusieurs objets, le modèle est `Result\%F.pdf` et la destination source est Result\nom_fichier_source1.pdf (sortie 1), Result\nom_fichier_source2.pdf (sortie 2), etc.

**Type** de données : Indique le type de données de la valeur renvoyée. Par exemple, le type de données de la valeur de retour du processus introduit dans cette section est `com.adobe.idp.Document`.

**Création d’un point de terminaison Watched Folder**

Après avoir défini les attributs et les valeurs de configuration du point de terminaison et défini les valeurs des paramètres d’entrée et de sortie, vous devez créer le point de terminaison Watched Folder.

**Activer le point de terminaison**

Après avoir créé un point de terminaison Watched Folder, vous devez l’activer. Lorsque le point de terminaison est activé, il peut être utilisé pour appeler le service. Après avoir activé le point de terminaison, vous pouvez le vue dans Administration Console.

**Voir également**

[Ajouter un point de terminaison Watched Folder à l’aide de l’API Java](programmatically-endpoints.md#add-a-watched-folder-endpoint-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Ajouter un point de terminaison Watched Folder à l’aide de l’API Java {#add-a-watched-folder-endpoint-using-the-java-api}

Ajoutez un point de terminaison Watched Folder à l’aide de l’API Java AEM Forms :

1. Incluez des fichiers de projet.

   Incluez des fichiers JAR client, tels que adobe-livecycle-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un objet Client EndpointRegistry.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `EndpointRegistryClient` en utilisant son constructeur et en transmettant l&#39;objet `ServiceClientFactory`.

1. Définissez les attributs des points de fin Watched Folder.

   * Créez un objet `CreateEndpointInfo` en utilisant son constructeur.
   * Spécifiez la valeur de l’identifiant du connecteur en appelant la méthode `CreateEndpointInfo` de l’objet `setConnectorId` et en transmettant la valeur de chaîne `WatchedFolder`.
   * Spécifiez la description du point de terminaison en appelant la méthode `CreateEndpointInfo` de l’objet `setDescription` et en transmettant une valeur de chaîne qui décrit le point de terminaison.
   * Spécifiez le nom du point de terminaison en appelant la méthode `CreateEndpointInfo` de l’objet `setName` et en transmettant une valeur de chaîne qui spécifie le nom.
   * Spécifiez le service auquel appartient le point de terminaison en appelant la méthode `CreateEndpointInfo` de l’objet `setServiceId` et en transmettant une valeur de chaîne qui spécifie le nom du service.
   * Spécifiez l’opération appelée en appelant la méthode `CreateEndpointInfo` de l’objet `setOperationName` et en transmettant une valeur de chaîne qui spécifie le nom de l’opération. En règle générale, lors de la création d’un point de terminaison Watched Folder pour un service issu d’un processus créé dans Workbench, le nom de l’opération est appelé.

1. Spécifiez les valeurs de configuration.

   Pour chaque valeur de configuration à définir pour le point de terminaison Watched Folder, vous devez appeler la méthode `CreateEndpointInfo` de l’objet `setConfigParameterAsText`. Par exemple, pour définir la valeur de configuration `url`, appelez la méthode `CreateEndpointInfo` de l’objet `setConfigParameterAsText` et transmettez les valeurs de chaîne suivantes :

   * Valeur de chaîne qui spécifie le nom de la valeur de configuration. Lors de la définition de la valeur de configuration `url`, spécifiez `url`.
   * Valeur de chaîne qui spécifie la valeur de la valeur de configuration. Lors de la définition de la valeur de configuration `url`, spécifiez l’emplacement du dossier de contrôle.

   >[!NOTE]
   >
   >Pour afficher toutes les valeurs de configuration définies pour le service EncryptDocument, consultez l’exemple de code Java situé à l’adresse [QuickStart: Ajouter un point de terminaison Watched Folder à l’aide de l’API Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-watched-folder-endpoint-using-the-java-api).

1. Définissez les valeurs des paramètres d’entrée.

   Définissez une valeur de paramètre d’entrée en appelant la méthode `setInputParameterMapping` de l’objet `CreateEndpointInfo` et en transmettant les valeurs suivantes :

   * Valeur de chaîne qui spécifie le nom du paramètre d’entrée. Par exemple, le nom du paramètre d’entrée du service EncryptDocument est `InDoc`.
   * Valeur de chaîne qui spécifie le type de données du paramètre d’entrée. Par exemple, le type de données du paramètre d’entrée `InDoc` est `com.adobe.idp.Document`.
   * Valeur de chaîne qui spécifie le type de mappage. Par exemple, vous pouvez spécifier `variable`.
   * Valeur de chaîne qui spécifie la valeur du type de mappage. Par exemple, vous pouvez spécifier &amp;ast;.pdf comme modèle de fichier.

   >[!NOTE]
   >
   >Appelez la méthode `setInputParameterMapping` pour chaque valeur de paramètre d’entrée à définir. Le processus EncryptDocument ne disposant que d’un seul paramètre d’entrée, vous devez appeler cette méthode une seule fois.

1. Définissez une valeur de paramètre de sortie.

   Définissez une valeur de paramètre de sortie en appelant la méthode `setOutputParameterMapping` de l’objet `CreateEndpointInfo` et en transmettant les valeurs suivantes :

   * Valeur de chaîne qui spécifie le nom du paramètre de sortie. Par exemple, le nom du paramètre de sortie pour le service EncryptDocument est `SecuredDoc`.
   * Valeur de chaîne qui spécifie le type de données du paramètre de sortie. Par exemple, le type de données du paramètre de sortie `SecuredDoc` est `com.adobe.idp.Document`.
   * Valeur de chaîne qui spécifie le type de mappage. Par exemple, vous pouvez spécifier `%F.pdf`.

1. Créez un point de terminaison Watched Folder.

   Créez le point de terminaison en appelant la méthode `EndpointRegistryClient` de l’objet `createEndpoint` et en transmettant l’objet `CreateEndpointInfo`. Cette méthode renvoie un objet `Endpoint` qui représente le point de terminaison Watched Folder.

1. Activez le point de terminaison.

   Activez le point de terminaison en appelant la méthode `EndpointRegistryClient` de l&#39;objet `enable` et en transmettant l&#39;objet `Endpoint` renvoyé par la méthode `createEndpoint`.

**Voir également**

[Résumé des étapes](programmatically-endpoints.md#summary-of-steps)

[QuickStart : Ajouter un point de terminaison Watched Folder à l’aide de l’API Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-watched-folder-endpoint-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Fichier de constante de configuration du dossier de contrôle {#watched-folder-configuration-values-constant-file} valeurs

Le [QuickStart: Ajouter un point de terminaison Watched Folder à l’aide de l’API Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-watched-folder-endpoint-using-the-java-api) utilise un fichier constant qui doit faire partie de votre projet Java pour compiler le début rapide. Ce fichier de constante représente les valeurs de configuration qui doivent être définies lors de l’ajout d’un point de terminaison Watched Folder. Le code Java suivant représente le fichier de constante.

```java
 /**
     * This class contains constants that can be used when setting Watched Folder
     * configuration values
     */

 public final class WatchedFolderEndpointConfigConstants {

         public static final String PROPERTY_FILEPROVIDER_URL = "url";
         public static final String PROPERTY_PROPERTY_ASYNCHRONOUS = "asynchronous";
         public static final String PROPERTY_CRON_EXPRESSION = "cronExpression";
         public static final String PROPERTY_PURGE_DURATION = "purgeDuration";
         public static final String PROPERTY_REPEAT_INTERVAL = "repeatInterval";
         public static final String PROPERTY_REPEAT_COUNT = "repeatCount";
         public static final String PROPERTY_THROTTLE = "throttleOn";
         public static final String PROPERTY_USERNAMER = "userName";
         public static final String PROPERTY_DOMAINNAME = "domainName";
         public static final String PROPERTY_FILEPROVIDER_BATCH_SIZE = "batchSize";
         public static final String PROPERTY_FILEPROVIDER_WAIT_TIME = "waitTime";
         public static final String PROPERTY_EXCLUDE_FILE_PATTERN = "excludeFilePattern";
         public static final String PROPERTY_INCLUDE_FILE_PATTERN = "excludeFilePattern";
         public static final String PROPERTY_FILEPROVIDER_RESULT_FOLDER_NAME =  "resultFolderName";
         public static final String PROPERTY_FILEPROVIDER_PRESERVE_FOLDER_NAME = "preserveFolderName";
         public static final String PROPERTY_FILEPROVIDER_FAILURE_FOLDER_NAME = "failureFolderName";
         public static final String PROPERTY_FILEPROVIDER_PRESERVE_ON_FAILURE = "preserveOnFailure";
         public static final String PROPERTY_FILEPROVIDER_OVERWRITE_DUPLICATE_FILENAME = "overwriteDuplicateFilename";
        }
```

## Ajouter des points de terminaison de courrier électronique {#adding-email-endpoints}

Vous pouvez ajouter par programmation un point de terminaison de courrier électronique à un service en utilisant l’API Java AEM Forms. En ajoutant un point de fin Courrier électronique, vous permettez aux utilisateurs d’envoyer un message électronique contenant une ou plusieurs pièces jointes à un compte de messagerie spécifié. Ensuite, l’opération de configuration du service est appelée et manipule les fichiers. Une fois que le service a effectué l’opération spécifiée, il envoie à l’expéditeur un message électronique contenant les fichiers modifiés en tant que pièces jointes.

Pour ajouter par programmation un point de fin de courrier électronique à un service, considérez le processus de courte durée *MyApplication\EncryptDocument* suivant. Pour plus d’informations sur les processus de courte durée, voir [Présentation des processus AEM Forms](/help/forms/developing/aem-forms-processes.md#understanding-aem-forms-processes).

![ae_ae_encryptdocumentprocess](assets/ae_ae_encryptdocumentprocess.png)

Ce processus accepte un document PDF non sécurisé en tant que valeur d’entrée, puis transmet le document PDF non sécurisé à l’opération `EncryptPDFUsingPassword` du service Encryption. Ce processus chiffre le document PDF avec un mot de passe et renvoie le document PDF chiffré par mot de passe en tant que valeur de sortie. Le nom de la valeur d’entrée (document PDF non sécurisé) est `InDoc` et le type de données est `com.adobe.idp.Document`. Le nom de la valeur de sortie (le document PDF chiffré par mot de passe) est `SecuredDoc` et le type de données est `com.adobe.idp.Document`.

>[!NOTE]
>
>Vous ne pouvez pas ajouter de point de fin de courrier électronique à l’aide de services Web.

### Résumé des étapes {#summary_of_steps-3}

Pour ajouter un point de fin de courrier électronique à un service, effectuez les tâches suivantes :

1. Incluez des fichiers de projet.
1. Créez un objet `EndpointRegistryClient`.
1. Définissez les attributs des points de fin de courrier électronique.
1. Spécifiez les valeurs de configuration.
1. Définissez les valeurs des paramètres d’entrée.
1. Définissez une valeur de paramètre de sortie.
1. Créez le point de terminaison Courrier électronique.
1. Activez le point de terminaison.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

Les fichiers JAR suivants doivent être ajoutés au chemin de classe de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (requis si AEM Forms est déployé sur JBoss Application Server)
* jbossall-client.jar (requis si AEM Forms est déployé sur JBoss Application Server)

Pour plus d’informations sur l’emplacement de ces fichiers JAR, voir [Inclusion de fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Création d’un objet Client EndpointRegistry**

Avant de pouvoir ajouter par programmation un point de terminaison E-mail, vous devez créer un objet `EndpointRegistryClient`.

**Définir les attributs du point de fin de courrier électronique**

Pour créer un point de fin de courrier électronique pour un service, spécifiez les valeurs suivantes :

* **Valeur** de l’identifiant du connecteur : Indique le type de point de terminaison créé. Pour créer un point de fin de courrier électronique, spécifiez `Email`.
* **Description** : Spécifie une description du point de terminaison.
* **Nom** : Indique le nom du point de terminaison.
* **Valeur** de l&#39;identifiant de service : Spécifie le service auquel le point de terminaison appartient. Par exemple, pour ajouter un point de fin de courrier électronique au processus introduit dans cette section (un processus devient un service lorsqu’il est activé à l’aide de Workbench), spécifiez `EncryptDocument`.
* **Nom** de l&#39;opération : Indique le nom de l’opération appelée à l’aide du point de terminaison. En règle générale, lors de la création d’un point de fin de courrier électronique pour un service qui provient d’un processus créé dans Workbench, le nom de l’opération est `invoke`.

**Spécifier les valeurs de configuration**

Vous devez spécifier des valeurs de configuration pour un point de terminaison de courrier électronique lors de l’ajout programmatique d’un point de terminaison de courrier électronique à un service. Ces valeurs de configuration sont spécifiées par un administrateur si un point de fin de courrier électronique est ajouté à l’aide d’Administration Console.

>[!NOTE]
>
>Le compte de messagerie surveillé est un compte spécial utilisé uniquement pour le point de terminaison de courrier électronique. Ce compte n’est pas un compte de messagerie d’un utilisateur ordinaire. Le compte de messagerie d’un utilisateur régulier ne doit pas être configuré comme compte utilisé par le fournisseur de messagerie car ce dernier supprime les messages électroniques de la boîte de réception une fois les messages terminés.

Les valeurs de configuration suivantes sont définies lors de l’ajout programmatique d’un point de terminaison E-mail à un service :

* **cronExpression** : Expression cron si le courrier électronique doit être planifié à l’aide d’une expression cron.
* **repeatCount** : Nombre de fois où le point de terminaison du courrier électronique analyse le dossier ou le répertoire. La valeur -1 indique une analyse indéfinie. La valeur par défaut est -1.
* **repeatInterval** : Taux d&#39;analyse en secondes que le destinataire utilise pour vérifier le courrier entrant. La valeur par défaut est 10.
* **startDelay** : Temps d’attente pour l’analyse après les débuts du Planificateur. L’heure par défaut est 0.
* **batchSize** : Nombre de messages électroniques que le destinataire traite par analyse pour obtenir des performances optimales. La valeur -1 désigne tous les messages électroniques. La valeur par défaut est 2.
* **userName** : Nom d’utilisateur utilisé lors de l’appel d’un service de cible à partir d’un courrier électronique. La valeur par défaut est `SuperAdmin`.
* **domainName** : Valeur de configuration obligatoire. La valeur par défaut est `DefaultDom`.
* **domainPattern** : Indique les modèles de domaine du courrier électronique entrant que le fournisseur accepte. Par exemple, si `adobe.com` est utilisé, seul le courrier électronique provenant d’adobe.com est traité, le courrier électronique provenant d’autres domaines est ignoré.
* **filePattern** : Indique les modèles de pièces jointes entrantes que le fournisseur accepte. Cela inclut les fichiers qui ont des extensions de nom de fichier spécifiques (&amp;amp ; ast ; .dat, &amp;amp ; ast ; .xml), les fichiers qui ont des noms spécifiques (data) et les fichiers dont le nom et l’extension contiennent des expressions composites (&amp;amp ; ast ; .[dD][aA]&#39;port&#39;). La valeur par défaut est `*`.
* **destinataireSuccessJob** : Adresse électronique à laquelle les messages sont envoyés pour indiquer les tâches réussies. Par défaut, un message de travail effectué est toujours envoyé à l’expéditeur. Si vous saisissez `sender`, les résultats des messages électroniques sont envoyés à l’expéditeur. Jusqu’à 100 destinataires sont pris en charge. Spécifiez d’autres destinataires avec des adresses électroniques, chacun séparé par une virgule. Pour désactiver cette option, laissez cette valeur vide. Dans certains cas, vous pouvez déclencher un processus et ne pas souhaiter recevoir de notification par courrier électronique du résultat. La valeur par défaut est `sender`.
* **destinataireFailedJob** : Adresse électronique à laquelle des messages sont envoyés pour signaler les travaux ayant échoué. Par défaut, un message de travail ayant échoué est toujours envoyé à l’expéditeur. Si vous saisissez `sender`, les résultats des messages électroniques sont envoyés à l’expéditeur. Jusqu’à 100 destinataires sont pris en charge. Spécifiez d’autres destinataires avec des adresses électroniques, chacun séparé par une virgule. Pour désactiver cette option, laissez cette valeur vide. La valeur par défaut est `sender`.
* **inboxHost** : nom d’hôte de boîte de réception ou adresse IP du fournisseur de messagerie électronique à analyser.
* **inboxPort** : port utilisé par le serveur de messagerie. La valeur POP3 par défaut est 110 et la valeur IMAP par défaut est 143. Si le protocole SSL est activé, la valeur POP3 par défaut est 995 et la valeur IMAP par défaut est 993.
* **inboxProtocol** : protocole de courrier électronique que le point de terminaison de courrier électronique doit utiliser pour analyser la boîte de réception. Les options sont `IMAP` ou `POP3`. Le serveur de messagerie de l’hôte boîte de réception doit prendre en charge ces protocoles.
* **inboxTimeOut** : Délai d’attente en secondes pour que le fournisseur de messagerie électronique attende les réponses de la boîte de réception. La valeur par défaut est 60.
* **inboxUser** : Nom d’utilisateur requis pour se connecter au compte de messagerie. Selon le serveur de messagerie et la configuration, il peut s’agir uniquement de la partie nom d’utilisateur du courrier électronique ou de l’adresse électronique complète.
* **inboxPassword** : Mot de passe de l’utilisateur de la boîte de réception.
* **inboxSSLEnabled** : Définissez cette valeur pour forcer le fournisseur de messagerie électronique à utiliser SSL lors de l’envoi de messages de notification de résultats ou d’erreurs. Assurez-vous que l’hôte IMAP ou POP3 prend en charge SSL.
* **smtpHost** : Nom d’hôte du serveur de messagerie auquel le fournisseur de messagerie envoie les résultats et les messages d’erreur.
* **smtpPort** : La valeur par défaut du port SMTP est 25.
* **smtpUser** : compte utilisateur que le fournisseur de messagerie électronique doit utiliser lorsqu’il envoie des notifications électroniques de résultats et d’erreurs.
* **smtpPassword** : Mot de passe du compte SMTP. Certains serveurs de messagerie ne nécessitent pas de mot de passe SMTP.
* **charSet** : Jeu de caractères utilisé par le fournisseur de messagerie électronique. La valeur par défaut est `UTF-8`.
* **smtpSSLEnabled** : Définissez cette valeur pour forcer le fournisseur de messagerie électronique à utiliser SSL lors de l’envoi de messages de notification de résultats ou d’erreurs. Assurez-vous que l’hôte SMTP prend en charge SSL.
* **failedJobFolder** : Spécifie un répertoire dans lequel stocker les résultats lorsque le serveur de messagerie SMTP n&#39;est pas opérationnel.
* **asynchrone** : Lorsqu’elle est définie sur synchrone, tous les documents d’entrée sont traités et une seule réponse est renvoyée. Lorsqu’elle est définie sur asynchrone, une réponse est envoyée pour chaque document d’entrée traité. Par exemple, un point de fin de courrier électronique est créé pour le processus introduit dans cette rubrique et un message électronique est envoyé à la boîte de réception du point de fin qui contient plusieurs documents PDF non sécurisés. Lorsque tous les documents PDF sont chiffrés avec un mot de passe et que le point de terminaison est configuré de manière synchrone, un message électronique de réponse unique est envoyé avec tous les documents PDF sécurisés joints. Si le point de terminaison est configuré en mode asynchrone, un message électronique de réponse distinct est envoyé pour chaque document PDF sécurisé. Chaque message électronique contient un document PDF unique en tant que pièce jointe. La valeur par défaut est asynchrone.

**Définir les valeurs des paramètres d’entrée**

Lors de la création d’un point de fin de courrier électronique, vous devez définir les valeurs des paramètres d’entrée. En d’autres termes, vous devez décrire les valeurs d’entrée transmises à l’opération appelée par le point de terminaison Courrier électronique. Prenons l’exemple du processus introduit dans cette rubrique. Il possède une valeur d’entrée nommée `InDoc` et son type de données est `com.adobe.idp.Document`. Lors de la création d’un point de terminaison de courrier électronique pour ce processus (une fois qu’un processus est activé, il devient un service), vous devez définir la valeur du paramètre d’entrée.

Pour définir les valeurs des paramètres d’entrée requises pour un point de fin de courrier électronique, spécifiez les valeurs suivantes :

**Nom** du paramètre d&#39;entrée : Nom du paramètre d’entrée. Le nom d’une valeur d’entrée est spécifié dans Workbench pour un processus. Si la valeur d’entrée appartient à une opération de service (service Forms qui n’est pas un processus créé dans Workbench), le nom d’entrée est spécifié dans le fichier component.xml. Par exemple, le nom du paramètre d’entrée pour le processus introduit dans cette section est `InDoc`.

**Type** de mappage : Permet de configurer les valeurs d’entrée requises pour appeler l’opération de service. Deux types de mappage sont les suivants :

* `Literal`: Le point de terminaison Courrier électronique utilise la valeur saisie dans le champ telle qu’elle est affichée. Tous les types Java de base sont pris en charge. Par exemple, si une interface API utilise une entrée de type chaîne, long, nombre entier ou valeur booléenne, cette entrée est convertie en type approprié, puis le service est appelé.
* `Variable`: La valeur saisie est un modèle de fichier utilisé par le point de terminaison Courrier électronique pour sélectionner l’entrée. Par exemple, si vous sélectionnez Variable pour le type de mappage et que le document d’entrée doit être un fichier PDF, vous pouvez spécifier `*.pdf` comme valeur de mappage.

**Valeur** de mappage : Indique la valeur du type de mappage. Par exemple, si vous sélectionnez un type de mappage de variable, vous pouvez spécifier `*.pdf` comme modèle de fichier.

**Type** de données : Indique le type de données des valeurs d’entrée. Par exemple, le type de données de la valeur d’entrée du processus introduit dans cette section est com.adobe.idp.Document.

**Définir une valeur de paramètre de sortie**

Lors de la création d’un point de fin de courrier électronique, vous devez définir une valeur de paramètre de sortie. En d’autres termes, vous devez décrire la valeur de sortie renvoyée par le service appelé par le point de terminaison Courrier électronique. Prenons l’exemple du processus introduit dans cette rubrique. Il a une valeur de sortie `SecuredDoc` et son type de données est `com.adobe.idp.Document`. Lors de la création d’un point de terminaison de courrier électronique pour ce processus (une fois qu’un processus est activé, il devient un service), vous devez définir la valeur du paramètre de sortie.

Pour définir une valeur de paramètre de sortie requise pour un point de fin de courrier électronique, spécifiez les valeurs suivantes :

**Nom** du paramètre de sortie : Nom du paramètre de sortie. Le nom d’une valeur de sortie de processus est spécifié dans Workbench. Si la valeur de sortie appartient à une opération de service (service qui n’est pas un processus créé dans Workbench), le nom de sortie est spécifié dans le fichier component.xml. Par exemple, le nom du paramètre de sortie pour le processus introduit dans cette section est `SecuredDoc`.

**Type** de mappage : Permet de configurer la sortie du service et de l’opération. Les options suivantes sont disponibles :

* Si le service renvoie un seul objet (un seul document), le modèle est `%F.pdf` et la destination source est nom_fichier_source.pdf. Par exemple, le processus introduit dans cette section renvoie un seul document. Par conséquent, le type de mappage peut être défini comme `%F.pdf` ( `%F` signifie utiliser le nom de fichier donné). Le modèle `%E` spécifie l&#39;extension du document d&#39;entrée.
* Si le service renvoie une liste, le modèle est `Result\%F\` et la destination source est Result\sourcefilename\source1 (output 1) et Result\sourcefilename\source2 (output 2).
* Si le service renvoie un mappage, le modèle est `Result\%F\` et la destination source est Result\sourcefilename\file1 and Result\sourcefilename\file2. Si le mappage comporte plusieurs objets, le modèle est `Result\%F.pdf` et la destination source est Result\nom_fichier_source1.pdf (sortie 1), Result\nom_fichier_source2.pdf (sortie 2), etc.

**Type** de données : Indique le type de données de la valeur renvoyée. Par exemple, le type de données de la valeur de retour du processus introduit dans cette section est `com.adobe.idp.Document`.

**Créer un point de terminaison de courrier électronique**

Après avoir défini les attributs de point de fin de courrier électronique et les valeurs de configuration, ainsi que les valeurs des paramètres d’entrée et de sortie, vous devez créer le point de fin de courrier électronique.

**Activer le point de terminaison**

Après avoir créé un point de fin de courrier électronique, vous devez l’activer. Lorsque le point de terminaison est activé, il peut être utilisé pour appeler le service. Après avoir activé le point de terminaison, vous pouvez le vue dans Administration Console.

**Voir également**

[Ajouter un point de fin de courrier électronique à l’aide de l’API Java](programmatically-endpoints.md#add-an-email-endpoint-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Ajouter un point de fin de courrier électronique à l’aide de l’API Java {#add-an-email-endpoint-using-the-java-api}

Ajoutez un point de fin de courrier électronique à l’aide de l’API Java :

1. Incluez des fichiers de projet.

   Incluez des fichiers JAR client, tels que adobe-livecycle-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un objet Client EndpointRegistry.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `EndpointRegistryClient` en utilisant son constructeur et en transmettant l&#39;objet `ServiceClientFactory`.

1. Définissez les attributs des points de fin de courrier électronique.

   * Créez un objet `CreateEndpointInfo` en utilisant son constructeur.
   * Spécifiez la valeur de l’identifiant du connecteur en appelant la méthode `CreateEndpointInfo` de l’objet `setConnectorId` et en transmettant la valeur de chaîne `Email`.
   * Spécifiez la description du point de terminaison en appelant la méthode `CreateEndpointInfo` de l’objet `setDescription` et en transmettant une valeur de chaîne qui décrit le point de terminaison.
   * Spécifiez le nom du point de terminaison en appelant la méthode `CreateEndpointInfo` de l’objet `setName` et en transmettant une valeur de chaîne qui spécifie le nom.
   * Spécifiez le service auquel appartient le point de terminaison en appelant la méthode `CreateEndpointInfo` de l’objet `setServiceId` et en transmettant une valeur de chaîne qui spécifie le nom du service.
   * Spécifiez l’opération appelée en appelant la méthode `CreateEndpointInfo` de l’objet `setOperationName` et en transmettant une valeur de chaîne qui spécifie le nom de l’opération. En règle générale, lors de la création d’un point de fin de courrier électronique pour un service qui provient d’un processus créé dans Workbench, le nom de l’opération est appelé.

1. Spécifiez les valeurs de configuration.

   Pour chaque valeur de configuration à définir pour le point de terminaison Email, vous devez appeler la méthode `CreateEndpointInfo` de l&#39;objet `setConfigParameterAsText`. Par exemple, pour définir la valeur de configuration `smtpHost`, appelez la méthode `CreateEndpointInfo` de l’objet `setConfigParameterAsText` et transmettez les valeurs suivantes :

   * Valeur de chaîne qui spécifie le nom de la valeur de configuration. Lors de la définition de la valeur de configuration `smtpHost`, spécifiez `smtpHost`.
   * Valeur de chaîne qui spécifie la valeur de la valeur de configuration. Lors de la définition de la valeur de configuration `smtpHost`, spécifiez une valeur de chaîne qui spécifie le nom du serveur SMTP.

   >[!NOTE]
   >
   >Pour afficher toutes les valeurs de configuration définies pour le service EncryptDocument présentées dans cette section, consultez l’exemple de code Java situé à l’adresse [QuickStart: Ajouter un point de terminaison de courrier électronique à l’aide de l’API Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-an-email-endpoint-using-the-java-api).

1. Définissez les valeurs des paramètres d’entrée.

   Définissez une valeur de paramètre d’entrée en appelant la méthode `setInputParameterMapping` de l’objet `CreateEndpointInfo` et en transmettant les valeurs suivantes :

   * Valeur de chaîne qui spécifie le nom du paramètre d’entrée. Par exemple, le nom du paramètre d’entrée du service EncryptDocument est `InDoc`.
   * Valeur de chaîne qui spécifie le type de données du paramètre d’entrée. Par exemple, le type de données du paramètre d’entrée `InDoc` est `com.adobe.idp.Document`.
   * Valeur de chaîne qui spécifie le type de mappage. Par exemple, vous pouvez spécifier `variable`.
   * Valeur de chaîne qui spécifie la valeur du type de mappage. Par exemple, vous pouvez spécifier &amp;ast;.pdf comme modèle de fichier.

   >[!NOTE]
   >
   >Appelez la méthode `setInputParameterMapping` pour chaque valeur de paramètre d’entrée à définir. Le processus EncryptDocument ne disposant que d’un seul paramètre d’entrée, vous devez appeler cette méthode une seule fois.

1. Définissez une valeur de paramètre de sortie.

   Définissez une valeur de paramètre de sortie en appelant la méthode `setOutputParameterMapping` de l’objet `CreateEndpointInfo` et en transmettant les valeurs suivantes :

   * Valeur de chaîne qui spécifie le nom du paramètre de sortie. Par exemple, le nom du paramètre de sortie pour le service EncryptDocument est `SecuredDoc`.
   * Valeur de chaîne qui spécifie le type de données du paramètre de sortie. Par exemple, le type de données du paramètre de sortie `SecuredDoc` est `com.adobe.idp.Document`.
   * Valeur de chaîne qui spécifie le type de mappage. Par exemple, vous pouvez spécifier `%F.pdf`.

1. Créez le point de terminaison Courrier électronique.

   Créez le point de terminaison en appelant la méthode `EndpointRegistryClient` de l’objet `createEndpoint` et en transmettant l’objet `CreateEndpointInfo`. Cette méthode renvoie un objet `Endpoint` qui représente le point de terminaison Email.

1. Activez le point de terminaison.

   Activez le point de terminaison en appelant la méthode `EndpointRegistryClient` de l&#39;objet `enable` et en transmettant l&#39;objet `Endpoint` renvoyé par la méthode `createEndpoint`.

**Voir également**

[Résumé des étapes](programmatically-endpoints.md#summary-of-steps)

[QuickStart : Ajouter un point de terminaison Watched Folder à l’aide de l’API Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-watched-folder-endpoint-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Fichier constant de valeurs de configuration de courriel {#email-configuration-values-constant-file}

Le [QuickStart: Ajouter un point de terminaison de courrier électronique à l’aide de l’API Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-an-email-endpoint-using-the-java-api) utilise un fichier constant qui doit faire partie de votre projet Java pour compiler le début rapide. Ce fichier de constante représente les valeurs de configuration qui doivent être définies lors de l’ajout d’un point de fin de courrier électronique. Le code Java suivant représente le fichier de constante.

```java
 /**
     * This class contains constants that can be used when setting email endpoint
     * configuration values
     */
 public class EmailEndpointConfigConstants {

     public static final String PROPERTY_EMAILPROVIDER_CRON_EXPRESSION = "cronExpression";
     public static final String PROPERTY_EMAILPROVIDER_REPREAT_COUNT = "repeatCount";
     public static final String PROPERTY_EMAILPROVIDER_REPREAT_INTERVAL = "repeatInterval";
     public static final String PROPERTY_EMAILPROVIDER_START_DELAY = "startDelay";
     public static final String PROPERTY_EMAILPROVIDER_BATCH_SIZE = "batchSize";
     public static final String PROPERTY_EMAILPROVIDER_USERNAME = "userName";
     public static final String PROPERTY_EMAILPROVIDER_DOMAINNAME = "domainName";
     public static final String PROPERTY_EMAILPROVIDER_DOMAINPATTERN = "domainPattern";
     public static final String PROPERTY_EMAILPROVIDER_FILEPATTERN = "filePattern";
     public static final String PROPERTY_EMAILPROVIDER_RECIPIENT_SUCCESSFUL_JOB = "recipientSuccessfulJob";
     public static final String PROPERTY_EMAILPROVIDER_RECIPIENT_FAILED_JOB = "recipientFailedJob";
     public static final String PROPERTY_EMAILPROVIDER_INBOX_HOST = "inboxHost";
     public static final String PROPERTY_EMAILPROVIDER_INBOX_PORT = "inboxPort";
     public static final String PROPERTY_EMAILPROVIDER_PROTOCOL = "inboxProtocol";
     public static final String PROPERTY_EMAILPROVIDER_INBOX_TIMEOUT = "inboxTimeOut";
     public static final String PROPERTY_EMAILPROVIDER_INBOX_USER = "inboxUser";
     public static final String PROPERTY_EMAILPROVIDER_INBOX_PASSWORD = "inboxPassword";
     public static final String PROPERTY_EMAILPROVIDER_INBOX_SSL = "inboxSSLEnabled";
     public static final String PROPERTY_EMAILPROVIDER_SMTP_HOST = "smtpHost";
     public static final String PROPERTY_EMAILPROVIDER_SMTP_PORT = "smtpPort";
     public static final String PROPERTY_EMAILPROVIDER_SMTP_USER = "smtpUser";
     public static final String PROPERTY_EMAILPROVIDER_SMTP_PASSWORD = "smtpPassword";
     public static final String PROPERTY_EMAILPROVIDER_CHARSET = "charSet";
     public static final String PROPERTY_EMAILPROVIDER_SMTP_SSL = "smtpSSLEnabled";
     public static final String PROPERTY_EMAILPROVIDER_FAILED_FOLDER = "failedJobFolder";
     public static final String PROPERTY_EMAILPROVIDER_ASYNCHRONOUS = "asynchronous";
 }
```

## Ajouter des points de terminaison Remoting {#adding-remoting-endpoints}

>[!NOTE]
>
>API de LiveCycle Remoting obsolètes pour AEM forms on JEE.

Vous pouvez par programmation ajouter un point de terminaison Remoting à un service à l’aide de l’API Java AEM Forms. En ajoutant un point de terminaison Remoting, vous autorisez une application Flex à appeler le service en utilisant la commande Remoting. (Voir [Appel d’AEM Forms à l’aide de (obsolète pour les formulaires AEM) AEM Forms Remoting](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting).)

Pour ajouter par programmation un point de terminaison Remoting à un service, considérez le processus de courte durée suivant nommé *EncryptDocument*.

![ar_ar_encryptdocumentprocess](assets/ar_ar_encryptdocumentprocess.png)

Ce processus accepte un document PDF non sécurisé en tant que valeur d’entrée, puis transmet le document PDF non sécurisé à l’opération `EncryptPDFUsingPassword` du service Encryption. Le document PDF est chiffré avec un mot de passe et le document PDF chiffré par mot de passe est la valeur de sortie de ce processus. Le nom de la valeur d’entrée (document PDF non sécurisé) est `InDoc` et le type de données est `com.adobe.idp.Document`. Le nom de la valeur de sortie (le document PDF chiffré par mot de passe) est `SecuredDoc` et le type de données est `com.adobe.idp.Document`.

Pour montrer comment ajouter un point de terminaison Remoting à un service, cette section ajoute un point de terminaison Remoting à un service appelé EncryptDocument.

>[!NOTE]
>
>Vous ne pouvez pas ajouter de point de terminaison Remoting à l’aide de services Web.

### Résumé des étapes {#summary_of_steps-4}

Pour supprimer un point de terminaison d’un service, effectuez les tâches suivantes :

1. Incluez des fichiers de projet.
1. Créez un objet `EndpointRegistryClient`.
1. Définissez les attributs des points de terminaison Remoting.
1. Créez un point de terminaison Remoting.
1. Activez le point de terminaison.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

Les fichiers JAR suivants doivent être ajoutés au chemin de classe de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (requis si AEM Forms est déployé sur JBoss Application Server)
* jbossall-client.jar (requis si AEM Forms est déployé sur JBoss Application Server)

Pour plus d’informations sur l’emplacement de ces fichiers JAR, voir [Inclusion de fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Création d’un objet Client EndpointRegistry**

Pour ajouter par programmation un point de terminaison Remoting, vous devez créer un objet `EndpointRegistryClient`.

**Définition des attributs de points de fin Remoting**

Pour créer un point de terminaison Remoting pour un service, spécifiez les valeurs suivantes :

* **Valeur** de l’identifiant du connecteur : Indique le type de point de terminaison créé. Pour créer un point de terminaison Remoting, spécifiez `Remoting`.
* **Description** : Indique la description du point de terminaison.
* **Nom** : Indique le nom du point de terminaison.
* **Valeur** de l&#39;identifiant de service : Spécifie le service auquel le point de terminaison appartient. Par exemple, pour ajouter un point de terminaison Remoting au processus introduit dans cette section (un processus devient un service lorsqu’il est activé dans Workbench), spécifiez `EncryptDocument`.
* **Nom** de l&#39;opération : Indique le nom de l’opération appelée à l’aide du point de terminaison. Lors de la création d’un point de terminaison Remoting, spécifiez un caractère générique (&amp;ast;).

**Création d’un point de terminaison Remoting**

Après avoir défini les attributs de point de terminaison Remoting, vous pouvez créer un point de terminaison Remoting pour un service.

**Activer le point de terminaison**

Après avoir créé un nouveau point de terminaison, vous devez l’activer. Lorsqu’un point de terminaison Remoting est activé, il permet à un client Flex d’appeler le service.

**Voir également**

[Ajouter un point de terminaison Remoting à l’aide de l’API Java](programmatically-endpoints.md#add-a-remoting-endpoint-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Ajouter un point de terminaison Remoting à l’aide de l’API Java {#add-a-remoting-endpoint-using-the-java-api}

Ajoutez un point de terminaison Remoting à l’aide de l’API Java :

1. Incluez des fichiers de projet.

   Incluez des fichiers JAR client, tels que adobe-livecycle-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un objet Client EndpointRegistry.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `EndpointRegistryClient` en utilisant son constructeur et en transmettant l&#39;objet `ServiceClientFactory`.

1. Définissez les attributs des points de terminaison Remoting.

   * Créez un objet `CreateEndpointInfo` en utilisant son constructeur.
   * Spécifiez la valeur de l’identifiant du connecteur en appelant la méthode `CreateEndpointInfo` de l’objet `setConnectorId` et en transmettant la valeur de chaîne `Remoting`.
   * Spécifiez la description du point de terminaison en appelant la méthode `CreateEndpointInfo` de l’objet `setDescription` et en transmettant une valeur de chaîne qui décrit le point de terminaison.
   * Spécifiez le nom du point de terminaison en appelant la méthode `CreateEndpointInfo` de l’objet `setName` et en transmettant une valeur de chaîne qui spécifie le nom.
   * Spécifiez le service auquel appartient le point de terminaison en appelant la méthode `CreateEndpointInfo` de l’objet `setServiceId` et en transmettant une valeur de chaîne qui spécifie le nom du service.
   * Spécifiez l’opération appelée par la méthode `setOperationName` de l’objet `CreateEndpointInfo` et transmettez une valeur de chaîne qui spécifie le nom de l’opération. Pour un point de terminaison Remoting, spécifiez un caractère générique (&amp;ast;).

1. Créez un point de terminaison Remoting.

   Créez le point de terminaison en appelant la méthode `EndpointRegistryClient` de l’objet `createEndpoint` et en transmettant l’objet `CreateEndpointInfo`. Cette méthode renvoie un objet `Endpoint` qui représente le nouveau point de terminaison Remoting.

1. Activez le point de terminaison.

   Activez le point de terminaison en appelant la méthode `EndpointRegistryClient` de l&#39;objet `enable` et en transmettant l&#39;objet `Endpoint` renvoyé par la méthode `createEndpoint`.

**Voir également**

[Résumé des étapes](programmatically-endpoints.md#summary-of-steps)

[QuickStart : Ajouter un point de terminaison Remoting à l’aide de l’API Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-remoting-endpoint-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Ajouter les points de terminaison TaskManager {#adding-taskmanager-endpoints}

Vous pouvez ajouter par programmation un point de terminaison TaskManager à un service à l’aide de l’API Java AEM Forms. En ajoutant un point de terminaison TaskManager à un service, vous permettez à un utilisateur de Workspace d’appeler le service. En d’autres termes, un utilisateur travaillant dans Workspace peut appeler un processus qui possède un point de terminaison TaskManager correspondant.

>[!NOTE]
>
>Vous ne pouvez pas ajouter de point de terminaison TaskManager à l’aide de services Web.

### Résumé des étapes {#summary_of_steps-5}

Pour ajouter un point de terminaison TaskManager à un service, effectuez les tâches suivantes :

1. Incluez des fichiers de projet.
1. Créez un objet `EndpointRegistryClient`.
1. Créez une catégorie pour le point de terminaison.
1. Définissez les attributs des points de terminaison TaskManager.
1. Créez un point de terminaison TaskManager.
1. Activez le point de terminaison.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

Les fichiers JAR suivants doivent être ajoutés au chemin de classe de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (requis si AEM Forms est déployé sur JBoss Application Server)
* jbossall-client.jar (requis si AEM Forms est déployé sur JBoss Application Server)

Pour plus d’informations sur l’emplacement de ces fichiers JAR, voir [Inclusion de fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Création d’un objet Client EndpointRegistry**

Avant de pouvoir ajouter par programmation un point de terminaison TaskManager, vous devez créer un objet `EndpointRegistryClient`.

**Création d’une catégorie pour le point de terminaison**

Les catégories sont utilisées pour organiser les services dans Workspace. En d’autres termes, un utilisateur de Workspace peut appeler un service qui possède un point de terminaison TaskManager en sélectionnant une catégorie dans Workspace. Lors de la création d’un point de terminaison TaskManager, vous pouvez référencer une catégorie existante ou créer une nouvelle catégorie par programmation.

>[!NOTE]
>
>Cette section crée une nouvelle catégorie dans le cadre de l’ajout d’un point de terminaison TaskManager à un service.

**Définition des attributs des points de terminaison TaskManager**

Pour créer un point de terminaison TaskManager pour un service, spécifiez les valeurs suivantes :

* **Identificateur** du connecteur : Indique le type de point de terminaison créé. Pour créer un point de terminaison TaskManager, spécifiez `TaskManagerConnector`.
* **Description** : Indique la description du point de terminaison.
* **Nom** : Indique le nom du point de terminaison.
* **Identificateur** de service : Spécifie le service auquel le point de terminaison appartient.
* **Catégorie** : Spécifie une valeur d&#39;identifiant de catégorie associée au point de terminaison TaskManager.
* **Nom** de l&#39;opération : En règle générale, lors de la création d’un point de terminaison TaskManager pour un service qui provient d’un processus créé dans Workbench, le nom de l’opération est  `invoke`.

**Création d’un point de terminaison TaskManager**

Après avoir défini des attributs de point de terminaison TaskManager, vous pouvez créer un point de terminaison TaskManager pour un service.

**Activer le point de terminaison**

Après avoir créé un nouveau point de terminaison, vous devez l’activer. Lorsque le point de terminaison est activé, il peut être utilisé pour appeler le service depuis Workspace. Après avoir activé le point de terminaison, vous pouvez le vue dans Administration Console.

**Voir également**

[Ajouter un point de terminaison TaskManager à l’aide de l’API Java](programmatically-endpoints.md#add-a-taskmanager-endpoint-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Ajouter un point de terminaison TaskManager à l’aide de l’API Java {#add-a-taskmanager-endpoint-using-the-java-api}

Ajoutez un point de terminaison TaskManager à l’aide de l’API Java :

1. Incluez des fichiers de projet.

   Incluez des fichiers JAR client, tels que adobe-livecycle-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un objet Client EndpointRegistry.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `EndpointRegistryClient` en utilisant son constructeur et en transmettant l&#39;objet `ServiceClientFactory`.

1. Créez une catégorie pour le point de terminaison.

   * Créez un objet `CreateEndpointCategoryInfo` en utilisant son constructeur et en transmettant les valeurs suivantes :

      * Valeur de chaîne qui spécifie la valeur d’identificateur de la catégorie
      * Valeur de chaîne qui spécifie la description de la catégorie
   * Créez la catégorie en appelant la méthode `EndpointRegistryClient` de l&#39;objet `createEndpointCategory` et en transmettant l&#39;objet `CreateEndpointCategoryInfo`. Cette méthode renvoie un objet `EndpointCategory` qui représente la nouvelle catégorie.


1. Définissez les attributs des points de terminaison TaskManager.

   * Créez un objet `CreateEndpointInfo` en utilisant son constructeur.
   * Spécifiez la valeur de l’identifiant du connecteur en appelant la méthode `CreateEndpointInfo` de l’objet `setConnectorId` et en transmettant la valeur de chaîne `TaskManagerConnector`.
   * Spécifiez la description du point de terminaison en appelant la méthode `CreateEndpointInfo` de l’objet `setDescription` et en transmettant une valeur de chaîne qui décrit le point de terminaison.
   * Spécifiez le nom du point de terminaison en appelant la méthode `CreateEndpointInfo` de l’objet `setName` et en transmettant une valeur de chaîne qui spécifie le nom.
   * Spécifiez le service auquel appartient le point de terminaison en appelant la méthode `CreateEndpointInfo` de l’objet `setServiceId` et en transmettant une valeur de chaîne qui spécifie le nom du service.
   * Spécifiez la catégorie à laquelle appartient le point de terminaison en appelant la méthode `CreateEndpointInfo` de l’objet `setCategoryId` et en transmettant une valeur de chaîne qui spécifie la valeur de l’identifiant de catégorie. Vous pouvez appeler la méthode `EndpointCategory` de l&#39;objet `getId` pour obtenir la valeur d&#39;identificateur de cette catégorie.
   * Spécifiez l’opération appelée en appelant la méthode `CreateEndpointInfo` de l’objet `setOperationName` et en transmettant une valeur de chaîne qui spécifie le nom de l’opération. En règle générale, lors de la création d’un point de terminaison `TaskManager` pour un service qui provient d’un processus créé dans Workbench, le nom de l’opération est `invoke`.

1. Créez un point de terminaison TaskManager.

   Créez le point de terminaison en appelant la méthode `EndpointRegistryClient` de l’objet `createEndpoint` et en transmettant l’objet `CreateEndpointInfo`. Cette méthode renvoie un objet `Endpoint` qui représente le nouveau point de terminaison TaskManager.

1. Activez le point de terminaison.

   Activez le point de terminaison en appelant la méthode `EndpointRegistryClient` de l&#39;objet `enable` et en transmettant l&#39;objet `Endpoint` renvoyé par la méthode `createEndpoint`.

**Voir également**

[Résumé des étapes](programmatically-endpoints.md#summary-of-steps)

[QuickStart : Ajouter un point de terminaison TaskManager à l’aide de l’API Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-taskmanager-endpoint-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Modification des points de terminaison {#modifying-endpoints}

Vous pouvez modifier par programmation un point de terminaison existant à l’aide de l’API Java AEM Forms. En modifiant un point de terminaison, vous pouvez modifier le comportement du point de terminaison. Prenons l’exemple d’un point de terminaison Watched Folder qui spécifie un dossier utilisé comme dossier de contrôle. Vous pouvez modifier par programmation les valeurs de configuration qui appartiennent au point de terminaison Watched Folder, ce qui entraîne le fonctionnement d’un autre dossier en tant que dossier de contrôle. Pour plus d’informations sur les valeurs de configuration qui appartiennent à un point de terminaison Watched Folder, voir [Ajouter des points de terminaison Watched Folder](programmatically-endpoints.md#adding-watched-folder-endpoints).

Pour montrer comment modifier un point de terminaison, cette section modifie un point de terminaison Watched Folder en modifiant le dossier qui se comporte comme le dossier de contrôle.

>[!NOTE]
>
>Vous ne pouvez pas modifier un point de terminaison à l’aide de services Web.

### Résumé des étapes {#summary_of_steps-6}

Pour modifier un point de terminaison, effectuez les tâches suivantes :

1. Incluez des fichiers de projet.
1. Créez un objet `EndpointRegistryClient`.
1. Récupérez le point de terminaison.
1. Spécifiez de nouvelles valeurs de configuration.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

Les fichiers JAR suivants doivent être ajoutés au chemin de classe de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (requis si AEM Forms est déployé sur JBoss Application Server)
* jbossall-client.jar (requis si AEM Forms est déployé sur JBoss Application Server)

Pour plus d’informations sur l’emplacement de ces fichiers JAR, voir [Inclusion de fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Création d’un objet Client EndpointRegistry**

Pour modifier par programmation un point de terminaison, vous devez créer un objet `EndpointRegistryClient`.

**Récupérer le point de terminaison à modifier**

Avant de pouvoir modifier un point de terminaison, vous devez le récupérer. Pour récupérer un point de terminaison, vous devez vous connecter en tant qu’utilisateur qui peut accéder à un point de terminaison. Il est recommandé de se connecter en tant qu’administrateur. (Voir [Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)).

Vous pouvez récupérer un point de terminaison en récupérant une liste de points de terminaison. Vous pouvez ensuite effectuer une itération dans la liste, en recherchant le point de terminaison spécifique à supprimer. Par exemple, vous pouvez localiser un point de terminaison en déterminant le service qui correspond au point de terminaison et le type de point de terminaison. Lorsque vous localisez le point de terminaison, vous pouvez le modifier.

**Spécifier les nouvelles valeurs de configuration**

Lors de la modification d’un point de terminaison, spécifiez de nouvelles valeurs de configuration. Par exemple, pour modifier un point de terminaison Watched Folder, réinitialisez toutes les valeurs de configuration des points de terminaison Watched Folder, pas seulement celles que vous souhaitez modifier. Pour plus d’informations sur les valeurs de configuration qui appartiennent à un point de terminaison Watched Folder, voir [Ajouter des points de terminaison Watched Folder](programmatically-endpoints.md#adding-watched-folder-endpoints).

>[!NOTE]
>
>Pour plus d’informations sur les valeurs de configuration qui appartiennent à un point de terminaison de courrier électronique, voir [Ajouter des points de terminaison de courrier électronique](programmatically-endpoints.md#adding-email-endpoints).

>[!NOTE]
>
>Vous ne pouvez pas modifier le service appelé par le point de terminaison. Si vous tentez de modifier le service, une exception est générée. Pour modifier le service associé à un point de terminaison donné, supprimez le point de terminaison et créez-en un nouveau. (Voir [Suppression des points de terminaison](programmatically-endpoints.md#removing-endpoints).)

**Voir également**

[Modification d’un point de terminaison à l’aide de l’API Java](programmatically-endpoints.md#modifying-an-endpoint-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Modification d’un point de terminaison à l’aide de l’API Java {#modifying-an-endpoint-using-the-java-api}

Modifiez un point de terminaison à l’aide de l’API Java :

1. Incluez des fichiers de projet.

   Incluez des fichiers JAR client, tels que adobe-livecycle-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un objet Client EndpointRegistry.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `EndpointRegistryClient` en utilisant son constructeur et en transmettant l&#39;objet `ServiceClientFactory`.

1. Récupérez le point de terminaison à modifier.

   * Récupérez une liste de tous les points de terminaison auxquels l’utilisateur actuel (spécifiée dans les propriétés de connexion) peut accéder en appelant la méthode `EndpointRegistryClient` de l’objet `getEndpoints` et en transmettant un objet `PagingFilter` qui agit comme un filtre. Vous pouvez transmettre une valeur `(PagingFilter)null` pour renvoyer tous les points de terminaison. Cette méthode renvoie un objet `java.util.List` où chaque élément est un objet `Endpoint`. Pour plus d’informations sur un objet `PagingFilter`, voir [Référence de l’API AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * Effectuez une itération sur l&#39;objet `java.util.List` pour déterminer s&#39;il possède des points de terminaison. S’il existe des points de terminaison, chaque élément est une instance `EndPoint`.
   * Déterminez le service qui correspond à un point de terminaison en appelant la méthode `EndPoint` de l&#39;objet `getServiceId`. Cette méthode renvoie une valeur de chaîne qui spécifie le nom du service.
   * Déterminez le type de point de terminaison en appelant la méthode `EndPoint` de l’objet `getConnectorId`. Cette méthode renvoie une valeur de chaîne qui spécifie le type de point de terminaison. Par exemple, si le point de terminaison est un point de terminaison Watched Folder, cette méthode renvoie `WatchedFolder`.

1. Spécifiez de nouvelles valeurs de configuration.

   * Créez un objet `ModifyEndpointInfo` en appelant son constructeur.
   * Pour chaque valeur de configuration à définir, appelez la méthode `ModifyEndpointInfo` de l&#39;objet `setConfigParameterAsText`. Par exemple, pour définir la valeur de configuration de l’URL, appelez la méthode `ModifyEndpointInfo` de l’objet `setConfigParameterAsText` et transmettez les valeurs suivantes :

      * Valeur de chaîne qui spécifie le nom de la valeur de configuration. Par exemple, pour définir la valeur de configuration `url`, spécifiez `url`.
      * Valeur de chaîne qui spécifie la valeur de la valeur de configuration. Pour définir une valeur pour la valeur de configuration `url`, spécifiez l’emplacement du dossier de contrôle.
   * Appelez la méthode `EndpointRegistryClient` de l&#39;objet `modifyEndpoint` et transmettez l&#39;objet `ModifyEndpointInfo`.


**Voir également**

[Résumé des étapes](programmatically-endpoints.md#summary-of-steps)

[QuickStart : Modification d’un point de terminaison à l’aide de l’API Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-modifying-an-endpoint-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Suppression des points de terminaison {#removing-endpoints}

Vous pouvez supprimer par programmation un point de terminaison d’un service à l’aide de l’API Java AEM Forms. Une fois que vous avez supprimé un point de terminaison, le service ne peut pas être appelé à l’aide de la méthode d’appel activée par le point de terminaison. Par exemple, si vous supprimez un point de terminaison SOAP d’un service, vous ne pouvez pas appeler le service à l’aide du mode SOAP.

Pour démontrer comment supprimer un point de terminaison d’un service, cette section supprime un point de terminaison EJB d’un service nommé *EncryptDocument*.

>[!NOTE]
>
>Vous ne pouvez pas supprimer un point de terminaison à l’aide de services Web.

### Résumé des étapes {#summary_of_steps-7}

Pour supprimer un point de terminaison d’un service, effectuez les tâches suivantes :

1. Incluez des fichiers de projet.
1. Créez un objet `EndpointRegistryClient`.
1. Récupérez le point de terminaison.
1. Supprimez le point de terminaison.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

Les fichiers JAR suivants doivent être ajoutés au chemin de classe de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (requis si AEM Forms est déployé sur JBoss Application Server)
* jbossall-client.jar (requis si AEM Forms est déployé sur JBoss Application Server)

Pour plus d’informations sur l’emplacement de ces fichiers JAR, voir [Inclusion de fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Création d’un objet Client EndpointRegistry**

Pour supprimer par programmation un point de terminaison, vous devez créer un objet `EndpointRegistryClient`.

**Récupérer le point de terminaison à supprimer**

Avant de pouvoir supprimer un point de terminaison, vous devez le récupérer. Pour récupérer un point de terminaison, vous devez vous connecter en tant qu’utilisateur qui peut accéder à un point de terminaison. Il est recommandé de se connecter en tant qu’administrateur. (Voir [Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)).

Vous pouvez récupérer un point de terminaison en récupérant une liste de points de terminaison. Vous pouvez ensuite effectuer une itération dans la liste, en recherchant le point de terminaison spécifique à supprimer. Par exemple, vous pouvez localiser un point de terminaison en déterminant le service qui correspond au point de terminaison et le type de point de terminaison. Lorsque vous localisez le point de terminaison, vous pouvez le supprimer.

**Suppression du point de terminaison**

Après avoir créé un nouveau point de terminaison, vous devez l’activer. Lorsque le point de terminaison est activé, il peut être utilisé pour appeler le service. Après avoir activé le point de terminaison, vous pouvez le vue dans Administration Console.

**Voir également**

[Suppression d’un point de terminaison à l’aide de l’API Java](programmatically-endpoints.md#removing-an-endpoint-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Suppression d’un point de terminaison à l’aide de l’API Java {#removing-an-endpoint-using-the-java-api}

Supprimez un point de terminaison à l’aide de l’API Java :

1. Incluez des fichiers de projet.

   Incluez des fichiers JAR client, tels que adobe-livecycle-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un objet Client EndpointRegistry.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `EndpointRegistryClient` en utilisant son constructeur et en transmettant l&#39;objet `ServiceClientFactory`.

1. Récupérez le point de terminaison à supprimer.

   * Récupérez une liste de tous les points de terminaison auxquels l’utilisateur actuel (spécifiée dans les propriétés de connexion) a accès en appelant la méthode `EndpointRegistryClient` de l’objet `getEndpoints` et en transmettant un objet `PagingFilter` qui agit comme un filtre. Vous pouvez transmettre `(PagingFilter)null` pour renvoyer tous les points de terminaison. Cette méthode renvoie un objet `java.util.List` où chaque élément est un objet `Endpoint`.
   * Effectuez une itération sur l&#39;objet `java.util.List` pour déterminer s&#39;il possède des points de terminaison. S’il existe des points de terminaison, chaque élément est une instance `EndPoint`.
   * Déterminez le service qui correspond à un point de terminaison en appelant la méthode `EndPoint` de l&#39;objet `getServiceId`. Cette méthode renvoie une valeur de chaîne qui spécifie le nom du service.
   * Déterminez le type de point de terminaison en appelant la méthode `EndPoint` de l’objet `getConnectorId`. Cette méthode renvoie une valeur de chaîne qui spécifie le type de point de terminaison. Par exemple, si le point de terminaison est un point de terminaison EJB, cette méthode renvoie `EJB`.

1. Supprimez le point de terminaison.

   Supprimez le point de terminaison en appelant la méthode `EndpointRegistryClient` de l’objet `remove` et en transmettant l’objet `EndPoint` qui représente le point de terminaison à supprimer.

**Voir également**

[Résumé des étapes](programmatically-endpoints.md#summary-of-steps)

[QuickStart : Suppression d’un point de terminaison à l’aide de l’API Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-removing-an-endpoint-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Récupération des informations du connecteur de point de terminaison {#retrieving-endpoint-connector-information}

Vous pouvez programmer la récupération d’informations sur les connecteurs de point de terminaison à l’aide de l’API AEM Forms. Un connecteur permet à un point de terminaison d’appeler un service à l’aide de diverses méthodes d’appel. Par exemple, un connecteur Watched Folder permet à un point de terminaison d’appeler un service à l’aide de dossiers de contrôle. En récupérant par programmation des informations sur les connecteurs de point de terminaison, vous pouvez récupérer les valeurs de configuration associées à un connecteur, telles que les valeurs de configuration requises et celles qui sont facultatives.

Pour montrer comment récupérer des informations sur les connecteurs de point de terminaison, cette section récupère des informations sur un connecteur de dossier de contrôle. (Voir [Ajouter les points de terminaison du dossier de contrôle](programmatically-endpoints.md#adding-watched-folder-endpoints).)

>[!NOTE]
>
>Vous ne pouvez pas récupérer d’informations sur les points de terminaison à l’aide de services Web.

>[!NOTE]
>
>Cette rubrique utilise l&#39;API `ConnectorRegistryClient` pour récupérer des informations sur les connecteurs de point de terminaison. (Voir [Référence de l’API AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).)

### Résumé des étapes {#summary_of_steps-8}

Pour récupérer les informations du connecteur de point de terminaison, effectuez les tâches suivantes :

1. Incluez des fichiers de projet.
1. Créez un objet `ConnectorRegistryClient`.
1. Spécifiez le type de connecteur.
1. Récupérez les valeurs de configuration.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

Les fichiers JAR suivants doivent être ajoutés au chemin de classe de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (requis si AEM Forms est déployé sur JBoss Application Server)
* jbossall-client.jar (requis si AEM Forms est déployé sur JBoss Application Server)

Si AEM Forms est déployé sur un serveur d’applications J2EE pris en charge qui n’est pas JBoss, remplacez adobe-utilities.jar et jbossall-client.jar par des fichiers JAR spécifiques au serveur d’applications J2EE sur lequel AEM Forms est déployé. Pour plus d’informations sur l’emplacement de tous les fichiers JAR AEM Forms, voir [Inclusion de fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Création d’un objet Client ConnectorRegistry**

Pour récupérer par programmation les informations du connecteur de point de terminaison, créez un objet `ConnectorRegistryClient`.

**Spécifier le type de connecteur**

Spécifiez le type de connecteur à partir duquel récupérer les informations. Les types de connecteurs suivants existent :

* **EJB** : Permet à une application cliente d’appeler un service en mode EJB.
* **SOAP** : Permet à une application cliente d’appeler un service à l’aide du mode SOAP.
* **Watched Folder** : Permet aux dossiers de contrôle d’appeler un service.
* **Courriel** : Permet aux messages électroniques d’appeler un service.
* **Remoting** : Permet à une application cliente Flex d’appeler un service.
* **TaskManagerConnector** : permet à un utilisateur de Workspace d’appeler un service à partir de Workspace.

**Récupérer les valeurs de configuration**

Après avoir spécifié le type de connecteur, vous pouvez récupérer des informations sur le connecteur, telles que la valeur de configuration prise en charge. Par exemple, pour n’importe quel connecteur, vous pouvez déterminer les valeurs de configuration requises et celles qui sont facultatives.

**Voir également**

[Récupération des informations du connecteur de point de terminaison à l’aide de l’API Java](programmatically-endpoints.md#retrieve-endpoint-connector-information-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Récupérer les informations du connecteur de point de terminaison à l’aide de l’API Java {#retrieve-endpoint-connector-information-using-the-java-api}

Récupérez les informations du connecteur de point de terminaison à l’aide de l’API Java :

1. Incluez des fichiers de projet. .

   Incluez des fichiers JAR client, tels que adobe-livecycle-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un objet Client ConnectorRegistry.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `ConnectorRegistryClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`. 

1. Spécifiez le type de connecteur.

   Spécifiez le type de connecteur en appelant la méthode `getEndpointDefinition` de l’objet `ConnectorRegistryClient` et en transmettant une valeur de chaîne qui spécifie le type de connecteur. Par exemple, pour spécifier le type de connecteur Watched Folder, transmettez la valeur de chaîne `WatchedFolder`. Cette méthode renvoie un objet `Endpoint` correspondant au type de connecteur.

1. Récupérez les valeurs de configuration.

   * Récupérez les valeurs de configuration associées dans ce point de terminaison en appelant la méthode `Endpoint` de l&#39;objet `getConfigParameters`. Cette méthode renvoie un tableau d&#39;objets `ConfigParameter`.
   * Récupérez des informations sur chaque valeur de configuration en récupérant chaque élément dans la baie. Chaque élément est un objet `ConfigParameter`. Vous pouvez, par exemple, déterminer si la valeur de configuration est obligatoire ou facultative en appelant la méthode `ConfigParameter` de l’objet `isRequired`. Si la valeur de configuration est requise, cette méthode renvoie `true`.

**Voir également**

[Résumé des étapes](programmatically-endpoints.md#summary-of-steps)

[QuickStart : Récupération des informations du connecteur de point de terminaison à l’aide de l’API Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-retrieving-endpoint-connector-information-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
