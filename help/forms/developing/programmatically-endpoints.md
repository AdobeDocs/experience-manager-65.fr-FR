---
title: Gestion des points de fin par programmation
seo-title: Gestion des points de fin par programmation
description: Utilisez le service Endpoint Registry pour ajouter des points de fin EJB, ajouter des points de fin SOAP, ajouter des points de fin Watched Folder, ajouter des points de fin Email, ajouter des points de fin Remoting, ajouter des points de fin Task Manager, modifier des points de fin, supprimer des points de fin et récupérer les informations du connecteur de point de fin.
seo-description: Utilisez le service Endpoint Registry pour ajouter des points de fin EJB, ajouter des points de fin SOAP, ajouter des points de fin Watched Folder, ajouter des points de fin Email, ajouter des points de fin Remoting, ajouter des points de fin Task Manager, modifier des points de fin, supprimer des points de fin et récupérer les informations du connecteur de point de fin.
uuid: 5dc50946-3323-4c5d-a43b-31c1c980bd04
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 076889a7-9c9f-4b6f-a45b-67a9b3923c36
role: Developer
exl-id: b94dcca2-136b-4b7d-b5ce-544804575876
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '10863'
ht-degree: 6%

---

# Gestion des points de fin par programmation {#programmatically-managing-endpoints}

**Les exemples et les exemples de ce document sont réservés à l’environnement AEM Forms on JEE.**

**À propos du service Endpoint Registry**

Le service Endpoint Registry permet de gérer les points de terminaison par programmation. Vous pouvez, par exemple, ajouter les types de points de fin suivants à un service :

* EJB
* méthode d’objet
* Watched Folder
* E-mail
* (Obsolète pour AEM forms) Remoting
* Gestionnaire des tâches

>[!NOTE]
>
>SOAP, EJB et (obsolète pour AEM forms on JEE) Les points de fin Remoting sont automatiquement créés pour chaque service activé. Les points d’entrée SOAP et EJB activent SOAP et EJB pour toutes les opérations de service.

Un point de fin Remoting permet aux clients Flex d’appeler des opérations sur le service AEM Forms auquel le point de fin est ajouté. Une destination Flex portant le même nom que le point de terminaison est créée et les clients Flex peuvent créer des objets distants pointant vers cette destination pour appeler des opérations sur le service approprié.

Les points de fin Email, Task Manager et Watched Folder n’exposent qu’une opération spécifique du service. L’ajout de ces points de fin nécessite une deuxième étape de configuration pour sélectionner une méthode à appeler, définir des paramètres de configuration et spécifier les mappages des paramètres d’entrée et de sortie.

Vous pouvez organiser les points d’entrée TaskManager en groupes appelés *categories*. Ces catégories sont ensuite exposées à Workspace par le biais de TaskManager, où les utilisateurs finaux voient les points de terminaison TaskManager tels qu’ils sont classés. Dans Workspace, les utilisateurs finaux voient ces catégories dans le volet de navigation. Les points de fin de chaque catégorie sont affichés sous forme de cartes de processus sur la page Démarrer les processus de Workspace.

Vous pouvez accomplir ces tâches à l’aide du service Endpoint Registry :

* Ajoutez des points de fin EJB. (Voir [Ajout de points de fin EJB](programmatically-endpoints.md#adding-ejb-endpoints).)
* Ajoutez des points de fin SOAP. (Voir [Ajout de points de fin SOAP](programmatically-endpoints.md#adding-soap-endpoints).)
* Ajoutez des points de fin Watched Folder (voir [Ajout de points de fin Watched Folder](programmatically-endpoints.md#adding-watched-folder-endpoints)).
* Ajoutez des points de fin Email. (Voir [Ajout de points de fin de courrier électronique](programmatically-endpoints.md#adding-email-endpoints).)
* Ajoutez des points de fin Remoting. (Voir [Ajout de points de fin Remoting](programmatically-endpoints.md#adding-remoting-endpoints).)
* Ajoutez des points d’entrée TaskManager (voir [Ajout de points d’entrée TaskManager](programmatically-endpoints.md#adding-taskmanager-endpoints)).
* Modifier les points de fin (voir [Modification des points de fin](programmatically-endpoints.md#modifying-endpoints))
* Supprimez les points de fin (voir [Suppression des points de fin](programmatically-endpoints.md#removing-endpoints)).
* Récupérez les informations du connecteur de point d’entrée (voir [Récupération des informations du connecteur de point d’entrée](programmatically-endpoints.md#retrieving-endpoint-connector-information)).

## Ajout de points de fin EJB {#adding-ejb-endpoints}

Vous pouvez ajouter par programmation un point d’entrée EJB à un service à l’aide de l’API Java AEM Forms. En ajoutant un point de fin EJB à un service, vous activez une application cliente pour appeler le service à l’aide du mode EJB. En d’autres termes, lorsque vous définissez les propriétés de connexion requises pour appeler AEM Forms, vous pouvez sélectionner le mode EJB. (Voir [Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)

>[!NOTE]
>
>Vous ne pouvez pas ajouter de point de terminaison EJB à l’aide de services web.

>[!NOTE]
>
>En règle générale, un point de terminaison EJB est ajouté par défaut à un service. Cependant, un point de terminaison EJB peut être ajouté à un processus déployé par programmation ou lorsqu’un point de terminaison EJB a été supprimé et doit être ajouté à nouveau.

### Résumé des étapes {#summary-of-steps}

Pour ajouter un point de fin EJB à un service, effectuez les tâches suivantes :

1. Inclure les fichiers de projet.
1. Créez un objet `EndpointRegistry Client` .
1. Définissez les attributs de point d’entrée EJB.
1. Créez un point de terminaison EJB.
1. Activez le point de terminaison .

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Les fichiers JAR suivants doivent être ajoutés au chemin de classe de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utility.jar (obligatoire si AEM Forms est déployé sur JBoss Application Server)
* jbossall-client.jar (obligatoire si AEM Forms est déployé sur JBoss Application Server)

Pour plus d’informations sur l’emplacement de ces fichiers JAR, voir [Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Création d’un objet client EndpointRegistry**

Avant de pouvoir ajouter un point de terminaison EJB par programmation, vous devez créer un objet `EndpointRegistryClient`.

**Définition des attributs de point de fin EJB**

Pour créer un point de fin EJB pour un service, spécifiez les valeurs suivantes :

* **Identifiant** du connecteur : Indique le type de point de terminaison à créer. Pour créer un point de terminaison EJB, spécifiez `EJB`.
* **Description** : Indique la description du point de fin.
* **Nom** : Indique le nom du point de fin.
* **Identifiant** du service : Indique le service auquel appartient le point de fin.
* **Nom de l’opération** : Indique le nom de l’opération appelée à l’aide du point de terminaison . Lors de la création d’un point de fin EJB, spécifiez un caractère générique ( `*`). Cependant, si vous souhaitez spécifier une opération spécifique plutôt que d’appeler toutes les opérations de service, indiquez le nom de l’opération plutôt que d’utiliser le caractère générique ( `*`).

**Création d’un point de fin EJB**

Après avoir défini les attributs de point de fin EJB, vous pouvez créer un point de fin EJB pour un service.

**Activation du point de terminaison**

Après avoir créé un nouveau point de terminaison, vous devez l’activer. Une fois le point de fin activé, il peut être utilisé pour appeler le service. Une fois le point de terminaison activé, vous pouvez l’afficher dans Administration Console.

**Voir également**

[Ajout d’un point de terminaison EJB à l’aide de l’API Java](programmatically-endpoints.md#adding-an-ejb-endpoint-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Ajout d’un point de terminaison EJB à l’aide de l’API Java {#adding-an-ejb-endpoint-using-the-java-api}

Ajoutez un point de terminaison EJB à l’aide de l’API Java :

1. Inclure les fichiers de projet.

   Incluez les fichiers JAR client, tels que adobe-livecycle-client.jar, dans le chemin de classe de votre projet Java. (

1. Créez un objet Client EndpointRegistry.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `EndpointRegistryClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`.

1. Définissez les attributs de point d’entrée EJB.

   * Créez un objet `CreateEndpointInfo` en utilisant son constructeur.
   * Indiquez la valeur de l’identifiant du connecteur en appelant la méthode `setConnectorId` de l’objet `CreateEndpointInfo` et en transmettant la valeur de chaîne `EJB`.
   * Spécifiez la description du point de terminaison en appelant la méthode `setDescription` de l’objet `CreateEndpointInfo` et en transmettant une valeur string qui décrit le point de terminaison.
   * Indiquez le nom du point de terminaison en appelant la méthode `setName` de l’objet `CreateEndpointInfo` et en transmettant une valeur string qui spécifie le nom.
   * Spécifiez le service auquel appartient le point de terminaison en appelant la méthode `setServiceId` de l’objet `CreateEndpointInfo` et en transmettant une valeur string qui spécifie le nom du service.
   * Indiquez l’opération appelée en appelant la méthode `setOperationName` de l’objet `CreateEndpointInfo` et transmettez une valeur string qui spécifie le nom de l’opération. Pour les points de fin SOAP et EJB, spécifiez un caractère générique ( `*`), ce qui implique toutes les opérations.

1. Créez un point de terminaison EJB.

   Créez le point de terminaison en appelant la méthode `EndpointRegistryClient` de l’objet `createEndpoint` et en transmettant l’objet `CreateEndpointInfo`. Cette méthode renvoie un objet `Endpoint` qui représente le nouveau point de terminaison EJB.

1. Activez le point de terminaison .

   Activez le point de terminaison en appelant la méthode enable de l’objet `EndpointRegistryClient` et en transmettant l’objet `Endpoint` qui a été renvoyé par la méthode `createEndpoint` .

**Voir également**

[Résumé des étapes](programmatically-endpoints.md#summary-of-steps)

[QuickStart : Ajout d’un point de terminaison EJB à l’aide de l’API Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-an-ejb-endpoint-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Ajout de points de fin SOAP {#adding-soap-endpoints}

Vous pouvez ajouter par programmation un point de terminaison SOAP à un service à l’aide de l’API Java AEM Forms. En ajoutant un point de terminaison SOAP, vous activez une application cliente à appeler le service à l’aide du mode SOAP. En d’autres termes, lorsque vous définissez les propriétés de connexion requises pour appeler AEM Forms, vous pouvez sélectionner le mode SOAP.

>[!NOTE]
>
>Vous ne pouvez pas ajouter de point de terminaison SOAP à l’aide de services web.

>[!NOTE]
>
>En règle générale, un point d’entrée SOAP est ajouté par défaut à un service. Cependant, un point d’entrée SOAP peut être ajouté à un processus déployé par programmation ou lorsqu’un point d’entrée SOAP a été supprimé et doit être ajouté à nouveau.

### Résumé des étapes {#summary_of_steps-1}

Pour ajouter un point de fin SOAP à un service, effectuez les tâches suivantes :

1. Inclure les fichiers de projet.
1. Créez un objet `EndpointRegistryClient` .
1. Définissez les attributs de point d’entrée SOAP.
1. Créez un point de terminaison SOAP.
1. Activez le point de terminaison .

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

Les fichiers JAR suivants doivent être ajoutés au chemin de classe de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utility.jar (obligatoire si AEM Forms est déployé sur JBoss Application Server)
* jbossall-client.jar (obligatoire si AEM Forms est déployé sur JBoss Application Server)

Ces fichiers JAR sont nécessaires pour créer un point de terminaison SOAP. Toutefois, vous avez besoin de fichiers JAR supplémentaires si vous utilisez le point de fin SOAP pour appeler le service. Pour plus d’informations sur les fichiers JAR AEM Forms, voir [Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Création d’un objet client EndpointRegistry**

Pour ajouter par programmation un point d’entrée SOAP à un service, vous devez créer un objet `EndpointRegistryClient` .

**Définition des attributs de point d’entrée SOAP**

Pour ajouter un point de fin SOAP à un service, spécifiez les valeurs suivantes :

* **Valeur** de l&#39;identifiant du connecteur : Indique le type de point de terminaison à créer. Pour créer un point de terminaison SOAP, spécifiez `SOAP`.
* **Description** : Indique la description du point de fin.
* **Nom** : Indique le nom du point de fin.
* **Valeur** de l’identifiant du service : Indique le service auquel appartient le point de fin.
* **Nom de l’opération** : Indique le nom de l’opération appelée à l’aide du point de terminaison . Lors de la création d’un point de fin SOAP, spécifiez un caractère générique ( `*`). Cependant, si vous souhaitez spécifier une opération spécifique plutôt que d’appeler toutes les opérations de service, indiquez le nom de l’opération plutôt que d’utiliser le caractère générique ( `*`).

**Création d’un point d’entrée SOAP**

Après avoir défini les attributs de point d’entrée SOAP, vous pouvez créer un point d’entrée SOAP.

**Activation du point de terminaison**

Après avoir créé un nouveau point de terminaison, vous devez l’activer. Lorsque le point de terminaison est activé, il peut être utilisé pour appeler le service. Une fois le point de terminaison activé, vous pouvez l’afficher dans Administration Console.

**Voir également**

[Ajout d’un point d’entrée SOAP à l’aide de l’API Java](programmatically-endpoints.md#add-a-soap-endpoint-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Ajoutez un point d’entrée SOAP à l’aide de l’API Java {#add-a-soap-endpoint-using-the-java-api}

Ajoutez un point d’entrée SOAP à un service à l’aide de l’API Java :

1. Inclure les fichiers de projet.

   Incluez les fichiers JAR client, tels que adobe-livecycle-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un objet Client EndpointRegistry.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `EndpointRegistryClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`.

1. Définissez les attributs de point d’entrée SOAP.

   * Créez un objet `CreateEndpointInfo` en utilisant son constructeur.
   * Indiquez la valeur de l’identifiant du connecteur en appelant la méthode `setConnectorId` de l’objet `CreateEndpointInfo` et en transmettant la valeur de chaîne `SOAP`.
   * Spécifiez la description du point de terminaison en appelant la méthode `setDescription` de l’objet `CreateEndpointInfo` et en transmettant une valeur string qui décrit le point de terminaison.
   * Indiquez le nom du point de terminaison en appelant la méthode `setName` de l’objet `CreateEndpointInfo` et en transmettant une valeur string qui spécifie le nom.
   * Spécifiez le service auquel appartient le point de terminaison en appelant la méthode `setServiceId` de l’objet `CreateEndpointInfo` et en transmettant une valeur string qui spécifie le nom du service.
   * Indiquez l’opération appelée en appelant la méthode `setOperationName` de l’objet `CreateEndpointInfo` et en transmettant une valeur string qui spécifie le nom de l’opération. Pour les points de fin SOAP et EJB, spécifiez un caractère générique ( `*`), ce qui implique toutes les opérations.

1. Créez un point de terminaison SOAP.

   Créez le point de terminaison en appelant la méthode `EndpointRegistryClient` de l’objet `createEndpoint` et en transmettant l’objet `CreateEndpointInfo`. Cette méthode renvoie un objet `Endpoint` qui représente le nouveau point de terminaison SOAP.

1. Activez le point de terminaison .

   Activez le point de terminaison en appelant la méthode enable de l’objet `EndpointRegistryClient` et transmettez l’objet `Endpoint` qui a été renvoyé par la méthode `createEndpoint` .

**Voir également**

[Résumé des étapes](programmatically-endpoints.md#summary-of-steps)

[QuickStart : Ajout d’un point d’entrée SOAP à l’aide de l’API Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-soap-endpoint-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Ajout de points de fin Watched Folder {#adding-watched-folder-endpoints}

Vous pouvez ajouter par programmation un point de fin Watched Folder à un service à l’aide de l’API Java AEM Forms. En ajoutant un point de fin Watched Folder, vous pouvez permettre aux utilisateurs de placer un fichier (un fichier PDF, par exemple) dans un dossier. Lorsque le fichier est placé dans le dossier, le service configuré est alors appelé et manipule le fichier. Après que le service a effectué l’opération spécifiée, il enregistre le fichier modifié dans un dossier de sortie spécifié. Un dossier de contrôle est configuré pour être analysé à un intervalle fixe ou selon une planification cron, par exemple tous les lundis, mercredis et vendredis à midi.

Pour ajouter par programmation un point de fin Watched Folder à un service, considérez le processus de courte durée suivant nommé *EncryptDocument*. (Voir [Présentation des processus AEM Forms](/help/forms/developing/aem-forms-processes.md#understanding-aem-forms-processes).)

![aw_aw_encryptdocumentprocess](assets/aw_aw_encryptdocumentprocess.png)

Ce processus accepte un document PDF non sécurisé comme valeur d’entrée, puis transmet le document PDF non sécurisé à l’opération `EncryptPDFUsingPassword` du service Encryption. Le document PDF est chiffré avec un mot de passe et le document PDF chiffré par mot de passe est la valeur de sortie de ce processus. Le nom de la valeur d’entrée (le document PDF non sécurisé) est `InDoc` et le type de données est `com.adobe.idp.Document`. Le nom de la valeur de sortie (le document PDF chiffré par mot de passe) est `SecuredDoc` et le type de données est `com.adobe.idp.Document`.

>[!NOTE]
>
>Vous ne pouvez pas ajouter de point de fin Watched Folder à l’aide de services Web.

### Résumé des étapes {#summary_of_steps-2}

Pour ajouter un point de fin Watched Folder à un service, effectuez les tâches suivantes :

1. Inclure les fichiers de projet.
1. Créez un objet `EndpointRegistryClient` .
1. Définissez les attributs Watched Folder endpoint.
1. Spécifiez les valeurs de configuration.
1. Définissez les valeurs des paramètres d’entrée.
1. Définissez une valeur de paramètre de sortie.
1. Créez un point de fin Watched Folder.
1. Activez le point de terminaison .

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

Les fichiers JAR suivants doivent être ajoutés au chemin de classe de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utility.jar (obligatoire si AEM Forms est déployé sur JBoss Application Server)
* jbossall-client.jar (obligatoire si AEM Forms est déployé sur JBoss Application Server)

Pour plus d’informations sur l’emplacement de ces fichiers JAR, voir [Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Création d’un objet client EndpointRegistry**

Pour ajouter par programmation un point de fin Watched Folder, vous devez créer un objet `EndpointRegistryClient`.

**Définition des attributs Watched Folder endpoint**

Pour créer un point de fin Watched Folder pour un service, spécifiez les valeurs suivantes :

* **Identifiant** du connecteur : Indique le type de point de terminaison créé. Pour créer un point de fin Watched Folder, indiquez `WatchedFolder`.
* **Description** : Indique la description du point de fin.
* **Nom** : Indique le nom du point de fin.
* **Identifiant** du service : Indique le service auquel appartient le point de fin. Par exemple, pour ajouter un point de fin Watched Folder au processus introduit dans cette section (un processus devient un service lorsqu’il est activé à l’aide de Workbench), spécifiez `EncryptDocument`.
* **Nom de l’opération** : Indique le nom de l’opération appelée à l’aide du point de terminaison . En règle générale, lors de la création d’un point de fin Watched Folder pour un service qui provient d’un processus créé dans Workbench, le nom de l’opération est `invoke`.

**Définition des valeurs de configuration**

Vous devez spécifier des valeurs de configuration pour un point de fin Watched Folder lors de l’ajout par programmation d’un point de fin Watched Folder à un service. Ces valeurs de configuration sont spécifiées par un administrateur si un point de fin Watched Folder est ajouté à l’aide d’Administration Console.

La liste suivante spécifie les valeurs de configuration définies lors de l’ajout par programmation d’un point de fin Watched Folder à un service :

* **url** : Indique l’emplacement du dossier de contrôle. Dans un environnement organisé en grappe, cette valeur doit pointer vers un dossier réseau partagé accessible à partir de tous les ordinateurs de la grappe.
* **asynchrone** : Identifie le type d’appel comme étant asynchrone ou synchrone. Les processus provisoires et synchrones peuvent être appelés uniquement de façon synchrone. La valeur par défaut est true. Asynchrone est recommandé.
* **cronExpression** : Utilisé par quartz pour planifier l’interrogation du répertoire d’entrée. Pour plus d’informations sur la configuration de l’expression cron, voir [https://quartz.sourceforge.net/javadoc/org/quartz/CronTrigger.html](https://quartz.sourceforge.net/javadoc/org/quartz/CronTrigger.html).
* **purgeDuration** : Il s’agit d’un attribut obligatoire. Les fichiers et les dossiers du dossier result sont purgés lorsqu’ils sont plus anciens que cette valeur. Cette valeur est mesurée en jours. Cet attribut est utile pour s’assurer que le dossier de résultats ne devient pas plein. La valeur -1 jour indique de ne jamais supprimer le dossier result. La valeur par défaut est -1.
* **repeatInterval** : Intervalle, en secondes, d’analyse du dossier de contrôle en vue de l’entrée. À moins que le ralentissement ne soit activé, cette valeur doit être supérieure au temps nécessaire au traitement d’une tâche moyenne ; sinon, le système risque d’être surchargé. La valeur par défaut est 5.
* **repeatCount** : Nombre d’analyses du dossier ou du répertoire par un dossier de contrôle. La valeur -1 indique une analyse indéfinie. La valeur par défaut est -1.
* **throttleOn** : Limite le nombre de tâches du dossier de contrôle pouvant être traitées à un moment donné. Le nombre maximal de tâches est déterminé par la valeur batchSize.
* **userName** : Nom d’utilisateur utilisé lors de l’appel d’un service cible à partir du dossier de contrôle. Cette valeur est obligatoire. La valeur par défaut est SuperAdmin.
* **domainName** : Domaine de l’utilisateur. Cette valeur est obligatoire. La valeur par défaut est DefaultDom.
* **batchSize** : Nombre de fichiers ou de dossiers à sélectionner par analyse. Utilisez cette valeur pour éviter une surcharge du système. l’analyse simultanée d’un trop grand nombre de fichiers peut entraîner un blocage. La valeur par défaut est 2.
* **waitTime** : Délai (en millisecondes) d’attente avant l’analyse d’un dossier ou d’un fichier après sa création. Par exemple, si le temps d’attente est de 36 000 000 millisecondes (une heure) et que le fichier a été créé il y a une minute, ce fichier est récupéré après 59 minutes ou plus. Cet attribut est utile pour s’assurer qu’un fichier ou un dossier est entièrement copié dans le dossier input. Par exemple, si vous avez un fichier volumineux à traiter et que le téléchargement du fichier prend dix minutes, définissez le temps d’attente sur 10&amp;ast;60 &amp;ast;1000 millisecondes. Ce paramètre empêche le dossier de contrôle d’analyser le fichier s’il n’a pas attendu dix minutes. La valeur par défaut est 0.
* **excludeFilePattern** : Le modèle utilisé par un dossier de contrôle pour déterminer les fichiers et les dossiers à analyser et à sélectionner. Les fichiers ou les dossiers présentant ce modèle ne seront pas analysés en vue d’être traités. Ce paramètre est utile lorsque l’entrée est un dossier contenant plusieurs fichiers. Le contenu du dossier peut être copié dans un dossier dont le nom sera sélectionné par le dossier de contrôle. Cette étape empêche le dossier de contrôle de sélectionner un dossier à traiter avant que le dossier ne soit complètement copié dans le dossier input. Par exemple, si la valeur excludeFilePattern est `data*`, tous les fichiers et dossiers correspondant à `data*` ne sont pas sélectionnés. Cela inclut les fichiers et les dossiers nommés `data1`, `data2`, etc. En outre, le modèle peut être complété par des caractères génériques pour spécifier des modèles de fichier. Le dossier de contrôle modifie l’expression régulière afin de prendre en charge les modèles de caractères génériques tels que `*.*` et `*.pdf`. Ces modèles de caractères génériques ne sont pas pris en charge par les expressions régulières.
* **includeFilePattern** : Le modèle utilisé par le dossier de contrôle pour déterminer les dossiers et les fichiers à analyser et à sélectionner. Par exemple, si cette valeur est `*`, tous les fichiers et dossiers correspondant à `input*` sont sélectionnés. Cela inclut les fichiers et les dossiers nommés `input1`, `input2`, etc. La valeur par défaut est `*`. Cette valeur indique tous les fichiers et dossiers. En outre, le modèle peut être complété par des caractères génériques pour spécifier des modèles de fichier. Le dossier de contrôle modifie l’expression régulière afin de prendre en charge les modèles de caractères génériques tels que `*.*` et `*.pdf`. Ces modèles de caractères génériques ne sont pas pris en charge par les expressions régulières. Cette valeur est obligatoire.
* **resultFolderName** : Dossier dans lequel les résultats enregistrés sont stockés. Cet emplacement peut être un chemin d’accès absolu ou relatif au répertoire. Si les résultats ne se trouvent pas dans ce dossier, vérifiez le dossier failure. Les fichiers en lecture seule ne sont pas traités et ils sont enregistrés dans le dossier failure. La valeur par défaut est `result/%Y/%M/%D/`. Il s’agit du dossier de résultats dans le dossier de contrôle.
* **preserveFolderName** : L’emplacement où les fichiers sont stockés après une analyse et une récupération réussies. Cet emplacement peut être un chemin d’accès de répertoire absolu, relatif ou nul. La valeur par défaut est `preserve/%Y/%M/%D/`.
* **failureFolderName** : Dossier dans lequel les fichiers d’échec sont enregistrés. Cet emplacement dépend toujours du dossier de contrôle. Les fichiers en lecture seule ne sont pas traités et ils sont enregistrés dans le dossier failure. La valeur par défaut est `failure/%Y/%M/%D/`.
* **preserveOnFailure** : Conserver les fichiers d’entrée en cas d’échec de l’exécution de l’opération sur un service. La valeur par défaut est true.
* **overwriteDuplicateFilename** : Lorsque la valeur est définie sur true, les fichiers du dossier de résultats et du dossier de fichiers conservés sont remplacés. Lorsque la valeur est définie sur false, les fichiers et les dossiers comportant un suffixe d’index numérique sont utilisés pour le nom. La valeur par défaut est false. 

**Définition des valeurs de paramètre d’entrée**

Lors de la création d’un point de fin Watched Folder, vous devez définir des valeurs de paramètre d’entrée. En d’autres termes, vous devez décrire les valeurs d’entrée transmises à l’opération appelée par le dossier de contrôle. Prenons l’exemple du processus introduit dans cette rubrique. Il a une valeur d’entrée nommée `InDoc` et son type de données est `com.adobe.idp.Document`. Lors de la création d’un point de fin Watched Folder pour ce processus (une fois qu’un processus est activé, il devient un service), vous devez définir la valeur du paramètre d’entrée.

Pour définir les valeurs de paramètre d’entrée requises pour un point de fin Watched Folder, spécifiez les valeurs suivantes :

**Input parameter name** : Nom du paramètre d’entrée. Le nom d’une valeur d’entrée est spécifié dans Workbench pour un processus. Si la valeur d’entrée appartient à une opération de service (un service qui n’est pas un processus créé dans Workbench), le nom d’entrée est spécifié dans le fichier component.xml. Par exemple, le nom du paramètre d’entrée pour le processus introduit dans cette section est `InDoc`.

**Type de mappage** : Utilisé pour configurer les valeurs d’entrée requises pour appeler l’opération de service. Il existe deux types de mappage :

* `Literal`: Le point de fin Watched Folder utilise la valeur saisie dans le champ telle qu’elle est affichée. Tous les types Java de base sont pris en charge. Par exemple, si une API utilise une entrée telle que String, long, int et Boolean, la chaîne est convertie dans le type approprié et le service est appelé.
* `Variable`: la valeur saisie est un modèle de fichier que le dossier de contrôle utilise pour sélectionner l’entrée. Par exemple, si vous sélectionnez Variable pour le type de mappage et que le document d’entrée doit être un fichier PDF, vous pouvez spécifier `*.pdf`comme valeur de mappage.

**Valeur de mappage** : Indique la valeur du type de mappage. Par exemple, si vous sélectionnez un type de mappage `Variable`, vous pouvez spécifier `*.pdf` comme modèle de fichier.

**Type** de données : Spécifie le type de données de la ou des valeurs d’entrée. Par exemple, le type de données de la valeur d’entrée du processus introduit dans cette section est `com.adobe.idp.Document`.

**Définition d’une valeur de paramètre de sortie**

Lors de la création d’un point de fin Watched Folder, vous devez définir une valeur de paramètre de sortie. En d’autres termes, vous devez décrire la valeur de sortie renvoyée par le service appelé par le point de fin Watched Folder. Prenons l’exemple du processus introduit dans cette rubrique. Il a une valeur de sortie `SecuredDoc` et son type de données est `com.adobe.idp.Document`. Lors de la création d’un point de fin Watched Folder pour ce processus (une fois qu’un processus est activé, il devient un service), vous devez définir la valeur du paramètre de sortie.

Pour définir une valeur de paramètre de sortie requise pour un point de fin Watched Folder, spécifiez les valeurs suivantes :

**Output parameter name** : Nom du paramètre de sortie. Le nom d’une valeur de sortie de processus est spécifié dans Workbench. Si la valeur de sortie appartient à une opération de service (un service qui n’est pas un processus créé dans Workbench), le nom de sortie est spécifié dans le fichier component.xml. Par exemple, le nom du paramètre de sortie pour le processus introduit dans cette section est `SecuredDoc`.

**Type de mappage** : Utilisé pour configurer la sortie du service et de l’opération. Les options suivantes sont disponibles :

* Si le service renvoie un seul objet (un seul document), le modèle est `%F.pdf` et la destination source est nom_fichier_source.pdf. Par exemple, le processus introduit dans cette section renvoie un seul document. Par conséquent, le type de mappage peut être défini comme `%F.pdf` ( `%F` signifie utiliser le nom de fichier donné). Le modèle `%E` spécifie l’extension du document d’entrée.
* Si le service renvoie une liste, le modèle est `Result\%F\` et la destination source est Result\sourcefilename\source1 (sortie 1) et Result\sourcefilename\source2 (sortie 2).
* Si le service renvoie une carte, le modèle est `Result\%F\` et la destination source est Result\sourcefilename\file1 and Result\sourcefilename\file2. Si la carte comporte plusieurs objets, le modèle est `Result\%F.pdf` et la destination source est Result\nom_fichier_source1.pdf (sortie 1), Result\sourcefilenam2.pdf (sortie 2), etc.

**Type** de données : Indique le type de données de la valeur renvoyée. Par exemple, le type de données de la valeur renvoyée par le processus introduit dans cette section est `com.adobe.idp.Document`.

**Création d’un point de fin Watched Folder**

Après avoir défini les attributs du point de fin, les valeurs de configuration et les valeurs des paramètres d’entrée et de sortie, vous devez créer le point de fin Watched Folder.

**Activation du point de terminaison**

Après avoir créé un point de fin Watched Folder, vous devez l’activer. Lorsque le point de terminaison est activé, il peut être utilisé pour appeler le service. Une fois le point de terminaison activé, vous pouvez l’afficher dans Administration Console.

**Voir également**

[Ajout d’un point de fin Watched Folder à l’aide de l’API Java](programmatically-endpoints.md#add-a-watched-folder-endpoint-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Ajoutez un point de fin Watched Folder à l’aide de l’API Java {#add-a-watched-folder-endpoint-using-the-java-api}

Ajoutez un point de fin Watched Folder à l’aide de l’API Java AEM Forms :

1. Inclure les fichiers de projet.

   Incluez les fichiers JAR client, tels que adobe-livecycle-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un objet Client EndpointRegistry.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `EndpointRegistryClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`.

1. Définissez les attributs Watched Folder endpoint.

   * Créez un objet `CreateEndpointInfo` en utilisant son constructeur.
   * Indiquez la valeur de l’identifiant du connecteur en appelant la méthode `setConnectorId` de l’objet `CreateEndpointInfo` et en transmettant la valeur de chaîne `WatchedFolder`.
   * Spécifiez la description du point de terminaison en appelant la méthode `setDescription` de l’objet `CreateEndpointInfo` et en transmettant une valeur string qui décrit le point de terminaison.
   * Indiquez le nom du point de terminaison en appelant la méthode `setName` de l’objet `CreateEndpointInfo` et en transmettant une valeur string qui spécifie le nom.
   * Spécifiez le service auquel appartient le point de terminaison en appelant la méthode `setServiceId` de l’objet `CreateEndpointInfo` et en transmettant une valeur string qui spécifie le nom du service.
   * Indiquez l’opération appelée en appelant la méthode `setOperationName` de l’objet `CreateEndpointInfo` et en transmettant une valeur string qui spécifie le nom de l’opération. En règle générale, lors de la création d’un point de fin Watched Folder pour un service issu d’un processus créé dans Workbench, le nom de l’opération est appelé.

1. Spécifiez les valeurs de configuration.

   Pour chaque valeur de configuration à définir pour le point de fin Watched Folder, vous devez appeler la méthode `CreateEndpointInfo` de l’objet `setConfigParameterAsText` . Par exemple, pour définir la valeur de configuration `url`, appelez la méthode `setConfigParameterAsText` de l’objet `CreateEndpointInfo` et transmettez les valeurs string suivantes :

   * Une valeur string qui spécifie le nom de la valeur de configuration. Lors de la définition de la valeur de configuration `url`, spécifiez `url`.
   * Une valeur string qui spécifie la valeur de la valeur de configuration. Lors de la définition de la valeur de configuration `url`, spécifiez l’emplacement du dossier de contrôle.

   >[!NOTE]
   >
   >Pour afficher toutes les valeurs de configuration définies pour le service EncryptDocument, reportez-vous à l’exemple de code Java situé à l’adresse [QuickStart : Ajout d’un point de fin Watched Folder à l’aide de l’API Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-watched-folder-endpoint-using-the-java-api).

1. Définissez les valeurs des paramètres d’entrée.

   Définissez une valeur de paramètre d’entrée en appelant la méthode `setInputParameterMapping` de l’objet `CreateEndpointInfo` et transmettez les valeurs suivantes :

   * Une valeur string qui spécifie le nom du paramètre d’entrée. Par exemple, le nom du paramètre d’entrée du service EncryptDocument est `InDoc`.
   * Une valeur string qui spécifie le type de données du paramètre d’entrée. Par exemple, le type de données du paramètre d’entrée `InDoc` est `com.adobe.idp.Document`.
   * Une valeur string qui spécifie le type de mappage. Par exemple, vous pouvez spécifier `variable`.
   * Une valeur string qui spécifie la valeur de type de mappage. Par exemple, vous pouvez spécifier &amp;ast;.pdf comme modèle de fichier.

   >[!NOTE]
   >
   >Appelez la méthode `setInputParameterMapping` pour chaque valeur de paramètre d’entrée à définir. Le processus EncryptDocument n’ayant qu’un seul paramètre d’entrée, vous devez appeler cette méthode une seule fois.

1. Définissez une valeur de paramètre de sortie.

   Définissez une valeur de paramètre de sortie en appelant la méthode `setOutputParameterMapping` de l’objet `CreateEndpointInfo` et transmettez les valeurs suivantes :

   * Une valeur string qui spécifie le nom du paramètre de sortie. Par exemple, le nom du paramètre de sortie du service EncryptDocument est `SecuredDoc`.
   * Une valeur string qui spécifie le type de données du paramètre de sortie. Par exemple, le type de données du paramètre de sortie `SecuredDoc` est `com.adobe.idp.Document`.
   * Une valeur string qui spécifie le type de mappage. Par exemple, vous pouvez spécifier `%F.pdf`.

1. Créez un point de fin Watched Folder.

   Créez le point de terminaison en appelant la méthode `EndpointRegistryClient` de l’objet `createEndpoint` et en transmettant l’objet `CreateEndpointInfo`. Cette méthode renvoie un objet `Endpoint` qui représente le point de fin Watched Folder.

1. Activez le point de terminaison .

   Activez le point de terminaison en appelant la méthode `enable` de l’objet `EndpointRegistryClient` et en transmettant l’objet `Endpoint` renvoyé par la méthode `createEndpoint` .

**Voir également**

[Résumé des étapes](programmatically-endpoints.md#summary-of-steps)

[QuickStart : Ajout d’un point de fin Watched Folder à l’aide de l’API Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-watched-folder-endpoint-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Valeurs de configuration du dossier de contrôle fichier constant {#watched-folder-configuration-values-constant-file}

Le [QuickStart : L’ajout d’un point de fin Watched Folder à l’aide de l’API Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-watched-folder-endpoint-using-the-java-api) utilise un fichier constant qui doit faire partie de votre projet Java pour compiler le démarrage rapide. Ce fichier constant représente les valeurs de configuration qui doivent être définies lors de l’ajout d’un point de fin Watched Folder. Le code Java suivant représente le fichier constant.

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

## Ajout de points de fin de courrier électronique {#adding-email-endpoints}

Vous pouvez ajouter par programmation un point de fin de courrier électronique à un service à l’aide de l’API Java AEM Forms. En ajoutant un point de fin de courrier électronique, vous pouvez permettre aux utilisateurs d’envoyer un message électronique contenant une ou plusieurs pièces jointes à un compte de courrier électronique spécifié. Ensuite, l’opération de configuration du service est appelée et manipule les fichiers. Une fois que le service a effectué l’opération spécifiée, il envoie un message électronique à l’expéditeur avec les fichiers modifiés comme pièces jointes.

Pour ajouter par programmation un point de fin de courrier électronique à un service, considérez le processus de courte durée suivant nommé *MyApplication\EncryptDocument*. Pour plus d’informations sur les processus de courte durée, voir [Présentation des processus AEM Forms](/help/forms/developing/aem-forms-processes.md#understanding-aem-forms-processes).

![ae_encryptdocumentprocess](assets/ae_ae_encryptdocumentprocess.png)

Ce processus accepte un document PDF non sécurisé comme valeur d’entrée, puis transmet le document PDF non sécurisé à l’opération `EncryptPDFUsingPassword` du service Encryption. Ce processus chiffre le document PDF avec un mot de passe et renvoie le document PDF chiffré par mot de passe en tant que valeur de sortie. Le nom de la valeur d’entrée (le document PDF non sécurisé) est `InDoc` et le type de données est `com.adobe.idp.Document`. Le nom de la valeur de sortie (le document PDF chiffré par mot de passe) est `SecuredDoc` et le type de données est `com.adobe.idp.Document`.

>[!NOTE]
>
>Vous ne pouvez pas ajouter de point de fin de courrier électronique à l’aide de services Web.

### Résumé des étapes {#summary_of_steps-3}

Pour ajouter un point de fin de courrier électronique à un service, effectuez les tâches suivantes :

1. Inclure les fichiers de projet.
1. Créez un objet `EndpointRegistryClient` .
1. Définissez les attributs de point de fin de courrier électronique.
1. Spécifiez les valeurs de configuration.
1. Définissez les valeurs des paramètres d’entrée.
1. Définissez une valeur de paramètre de sortie.
1. Créez le point de fin Email.
1. Activez le point de terminaison .

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

Les fichiers JAR suivants doivent être ajoutés au chemin de classe de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utility.jar (obligatoire si AEM Forms est déployé sur JBoss Application Server)
* jbossall-client.jar (obligatoire si AEM Forms est déployé sur JBoss Application Server)

Pour plus d’informations sur l’emplacement de ces fichiers JAR, voir [Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Création d’un objet client EndpointRegistry**

Avant de pouvoir ajouter par programmation un point de fin de courrier électronique, vous devez créer un objet `EndpointRegistryClient` .

**Définition des attributs de point de fin de courrier électronique**

Pour créer un point de fin de courrier électronique pour un service, spécifiez les valeurs suivantes :

* **Valeur** de l&#39;identifiant du connecteur : Indique le type de point de terminaison créé. Pour créer un point de fin de courrier électronique, spécifiez `Email`.
* **Description** : Indique une description pour le point de fin.
* **Nom** : Indique le nom du point de fin.
* **Valeur** de l’identifiant du service : Indique le service auquel appartient le point de fin. Par exemple, pour ajouter un point de fin Email au processus introduit dans cette section (un processus devient un service lorsqu’il est activé à l’aide de Workbench), spécifiez `EncryptDocument`.
* **Nom de l’opération** : Indique le nom de l’opération appelée à l’aide du point de terminaison . En règle générale, lors de la création d’un point de fin de courrier électronique pour un service qui provient d’un processus créé dans Workbench, le nom de l’opération est `invoke`.

**Définition des valeurs de configuration**

Vous devez spécifier des valeurs de configuration pour un point de fin de courrier électronique lors de l’ajout par programmation d’un point de fin de courrier électronique à un service. Ces valeurs de configuration sont spécifiées par un administrateur si un point de fin de courrier électronique est ajouté à l’aide d’Administration Console.

>[!NOTE]
>
>Le compte de messagerie surveillé est un compte spécial utilisé uniquement pour le point de fin de courrier électronique. Ce compte n’est pas un compte de messagerie d’un utilisateur ordinaire. Le compte de messagerie d’un utilisateur ordinaire ne doit pas être configuré comme le compte utilisé par le fournisseur de messagerie, car celui-ci supprime les messages électroniques de la boîte de réception une fois qu’il a terminé avec les messages.

Les valeurs de configuration suivantes sont définies lors de l’ajout par programmation d’un point de fin de courrier électronique à un service :

* **cronExpression** : Une expression cron si l’email doit être programmé à l’aide d’une expression cron.
* **repeatCount** : Nombre de fois où le point de fin de courrier électronique analyse le dossier ou le répertoire. La valeur -1 indique une analyse indéfinie. La valeur par défaut est -1.
* **repeatInterval** : Taux d’analyse en secondes utilisé par le récepteur pour vérifier les emails entrants. La valeur par défaut est 10.
* **startDelay** : Temps d’attente d’analyse une fois le planificateur démarré. L’heure par défaut est 0.
* **batchSize** : Nombre de messages électroniques traités par le destinataire par analyse pour des performances optimales. La valeur -1 désigne tous les messages électroniques. La valeur par défaut est 2.
* **userName** : Nom d’utilisateur utilisé lors de l’appel d’un service cible à partir d’un courrier électronique. La valeur par défaut est `SuperAdmin`.
* **domainName** : Une valeur de configuration obligatoire. La valeur par défaut est `DefaultDom`.
* **domainPattern** : Indique les modèles de domaine des courriers électroniques entrants que le fournisseur accepte. Par exemple, si `adobe.com` est utilisé, seul le courrier électronique d’adobe.com est traité, le courrier électronique d’autres domaines est ignoré.
* **filePattern** : Spécifie les modèles de pièces jointes entrantes acceptés par le fournisseur. Cela inclut les fichiers ayant des extensions de nom de fichier spécifiques (&amp;ast;.dat, &amp;ast;.xml), les fichiers ayant des noms spécifiques (data) et les fichiers ayant des expressions composites dans le nom et l’extension (&amp;ast;.[dD][aA]&#39;port&#39;). La valeur par défaut est `*`.
* **recipientSuccessJob** : Adresse électronique à laquelle les messages sont envoyés pour indiquer les tâches réussies. Par défaut, un message de travail effectué est toujours envoyé à l’expéditeur. Si vous saisissez `sender`, les résultats des messages électroniques sont envoyés à l’expéditeur. Jusqu’à 100 destinataires sont pris en charge. Spécifiez d’autres destinataires avec des adresses email, chacun séparé par une virgule. Pour désactiver cette option, laissez cette valeur vide. Dans certains cas, il se peut que vous souhaitiez déclencher un processus et ne pas recevoir de notification par courrier électronique du résultat. La valeur par défaut est `sender`.
* **recipientFailedJob** : Adresse électronique à laquelle des messages sont envoyés pour indiquer les tâches ayant échoué. Par défaut, un message de tâche en échec est toujours envoyé à l’expéditeur. Si vous saisissez `sender`, les résultats des messages électroniques sont envoyés à l’expéditeur. Jusqu’à 100 destinataires sont pris en charge. Spécifiez d’autres destinataires avec des adresses email, chacun séparé par une virgule. Pour désactiver cette option, laissez cette valeur vide. La valeur par défaut est `sender`.
* **inboxHost** : Nom d’hôte de boîte de réception ou adresse IP du fournisseur de messagerie à analyser.
* **inboxPort** : port utilisé par le serveur de messagerie. La valeur POP3 par défaut est 110 et la valeur IMAP par défaut est 143. Si le protocole SSL est activé, la valeur POP3 par défaut est 995 et la valeur IMAP par défaut est 993.
* **inboxProtocol** : Protocole de courrier électronique que le point de fin de courrier électronique doit utiliser pour analyser la boîte de réception. Les options sont `IMAP` ou `POP3`. Le serveur de messagerie de l’hôte boîte de réception doit prendre en charge ces protocoles.
* **inboxTimeOut** : Délai d’expiration en secondes pendant lequel le fournisseur de messagerie électronique attend les réponses de la boîte de réception. La valeur par défaut est 60.
* **inboxUser** : Nom d’utilisateur requis pour se connecter au compte de messagerie. Selon le serveur de messagerie et la configuration, il peut s’agir uniquement de la partie nom d’utilisateur de l’e-mail ou de l’adresse électronique complète.
* **inboxPassword** : Mot de passe de l’utilisateur de la boîte de réception.
* **inboxSSLEnabled** : Définissez cette valeur pour forcer le fournisseur de messagerie à utiliser SSL lors de l’envoi de messages de notification de résultats ou d’erreurs. Assurez-vous que l’hôte IMAP ou POP3 prend en charge SSL.
* **smtpHost** : Nom d’hôte du serveur de messagerie auquel le fournisseur de messagerie envoie les résultats et les messages d’erreur.
* **smtpPort** : La valeur par défaut du port SMTP est 25.
* **smtpUser** : Le compte utilisateur que le fournisseur de messagerie électronique doit utiliser lorsqu’il envoie des notifications électroniques de résultats et d’erreurs.
* **smtpPassword** : Mot de passe du compte SMTP. Certains serveurs de messagerie ne nécessitent pas de mot de passe SMTP.
* **charSet** : Jeu de caractères utilisé par le fournisseur de messagerie. La valeur par défaut est `UTF-8`.
* **smtpSSLEnabled** : Définissez cette valeur pour forcer le fournisseur de messagerie à utiliser SSL lors de l’envoi de messages de notification de résultats ou d’erreurs. Assurez-vous que l’hôte SMTP prend en charge SSL.
* **failedJobFolder** : Spécifie un répertoire dans lequel stocker les résultats lorsque le serveur de messagerie SMTP n’est pas opérationnel.
* **asynchrone** : Lorsqu’elle est définie sur synchrone, tous les documents d’entrée sont traités et une seule réponse est renvoyée. Lorsqu’elle est définie sur asynchrone, une réponse est envoyée pour chaque document d’entrée traité. Par exemple, un point de fin de courrier électronique est créé pour le processus introduit dans cette rubrique et un message électronique est envoyé à la boîte de réception du point de fin qui contient plusieurs documents PDF non sécurisés. Lorsque tous les documents PDF sont chiffrés avec un mot de passe et que le point de fin est configuré comme synchrone, un seul message électronique de réponse est envoyé avec tous les documents PDF sécurisés joints. Si le point de fin est configuré comme asynchrone, un message électronique de réponse distinct est envoyé pour chaque document PDF sécurisé. Chaque message électronique contient un document PDF unique en tant que pièce jointe. La valeur par défaut est asynchrone.

**Définition des valeurs de paramètre d’entrée**

Lors de la création d’un point de fin de courrier électronique, vous devez définir des valeurs de paramètre d’entrée. En d’autres termes, vous devez décrire les valeurs d’entrée transmises à l’opération appelée par le point de fin de courrier électronique. Prenons l’exemple du processus introduit dans cette rubrique. Il a une valeur d’entrée nommée `InDoc` et son type de données est `com.adobe.idp.Document`. Lors de la création d’un point de fin de courrier électronique pour ce processus (une fois qu’un processus est activé, il devient un service), vous devez définir la valeur du paramètre d’entrée.

Pour définir les valeurs de paramètre d’entrée requises pour un point de fin de courrier électronique, spécifiez les valeurs suivantes :

**Input parameter name** : Nom du paramètre d’entrée. Le nom d’une valeur d’entrée est spécifié dans Workbench pour un processus. Si la valeur d’entrée appartient à une opération de service (un service Forms qui n’est pas un processus créé dans Workbench), le nom d’entrée est spécifié dans le fichier component.xml. Par exemple, le nom du paramètre d’entrée pour le processus introduit dans cette section est `InDoc`.

**Type de mappage** : Utilisé pour configurer les valeurs d’entrée requises pour appeler l’opération de service. Deux types de mappage sont les suivants :

* `Literal`: Le point de fin Email utilise la valeur saisie dans le champ telle qu&#39;elle est affichée. Tous les types Java de base sont pris en charge. Par exemple, si une interface API utilise une entrée de type chaîne, long, nombre entier ou valeur booléenne, cette entrée est convertie en type approprié, puis le service est appelé.
* `Variable`: La valeur saisie est un modèle de fichier que le point de fin de courrier électronique utilise pour sélectionner l’entrée. Par exemple, si vous sélectionnez Variable pour le type de mappage et que le document d’entrée doit être un fichier PDF, vous pouvez spécifier `*.pdf` comme valeur de mappage.

**Valeur de mappage** : Indique la valeur du type de mappage. Par exemple, si vous sélectionnez un type de mappage de variable , vous pouvez spécifier `*.pdf` comme modèle de fichier.

**Type** de données : Indique le type de données des valeurs d’entrée. Par exemple, le type de données de la valeur d’entrée du processus introduit dans cette section est com.adobe.idp.Document.

**Définition d’une valeur de paramètre de sortie**

Lors de la création d’un point de fin de courrier électronique, vous devez définir une valeur de paramètre de sortie. En d’autres termes, vous devez décrire la valeur de sortie renvoyée par le service appelé par le point de fin Email. Prenons l’exemple du processus introduit dans cette rubrique. Il a une valeur de sortie `SecuredDoc` et son type de données est `com.adobe.idp.Document`. Lors de la création d&#39;un point de fin Email pour ce processus (une fois qu&#39;un processus est activé, il devient un service), vous devez définir la valeur du paramètre de sortie.

Pour définir une valeur de paramètre de sortie requise pour un point de fin Email, spécifiez les valeurs suivantes :

**Output parameter name** : Nom du paramètre de sortie. Le nom d’une valeur de sortie de processus est spécifié dans Workbench. Si la valeur de sortie appartient à une opération de service (un service qui n’est pas un processus créé dans Workbench), le nom de sortie est spécifié dans le fichier component.xml. Par exemple, le nom du paramètre de sortie pour le processus introduit dans cette section est `SecuredDoc`.

**Type de mappage** : Utilisé pour configurer la sortie du service et de l’opération. Les options suivantes sont disponibles :

* Si le service renvoie un seul objet (un seul document), le modèle est `%F.pdf` et la destination source est nom_fichier_source.pdf. Par exemple, le processus introduit dans cette section renvoie un seul document. Par conséquent, le type de mappage peut être défini comme `%F.pdf` ( `%F` signifie utiliser le nom de fichier donné). Le modèle `%E` spécifie l’extension du document d’entrée.
* Si le service renvoie une liste, le modèle est `Result\%F\` et la destination source est Result\sourcefilename\source1 (sortie 1) et Result\sourcefilename\source2 (sortie 2).
* Si le service renvoie une carte, le modèle est `Result\%F\` et la destination source est Result\sourcefilename\file1 and Result\sourcefilename\file2. Si la carte comporte plusieurs objets, le modèle est `Result\%F.pdf` et la destination source est Result\nom_fichier_source1.pdf (sortie 1), Result\sourcefilenam2.pdf (sortie 2), etc.

**Type** de données : Indique le type de données de la valeur renvoyée. Par exemple, le type de données de la valeur renvoyée par le processus introduit dans cette section est `com.adobe.idp.Document`.

**Création du point de fin Email**

Après avoir défini les attributs de point de fin de courrier électronique et les valeurs de configuration, ainsi que les valeurs des paramètres d’entrée et de sortie, vous devez créer le point de fin de courrier électronique.

**Activation du point de terminaison**

Après avoir créé un point de fin de courrier électronique, vous devez l’activer. Lorsque le point de terminaison est activé, il peut être utilisé pour appeler le service. Une fois le point de terminaison activé, vous pouvez l’afficher dans Administration Console.

**Voir également**

[Ajout d’un point de fin de courrier électronique à l’aide de l’API Java](programmatically-endpoints.md#add-an-email-endpoint-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Ajoutez un point de fin Email à l’aide de l’API Java {#add-an-email-endpoint-using-the-java-api}

Ajoutez un point de fin Email à l’aide de l’API Java :

1. Inclure les fichiers de projet.

   Incluez les fichiers JAR client, tels que adobe-livecycle-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un objet Client EndpointRegistry.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `EndpointRegistryClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`.

1. Définissez les attributs de point de fin de courrier électronique.

   * Créez un objet `CreateEndpointInfo` en utilisant son constructeur.
   * Indiquez la valeur de l’identifiant du connecteur en appelant la méthode `setConnectorId` de l’objet `CreateEndpointInfo` et en transmettant la valeur de chaîne `Email`.
   * Spécifiez la description du point de terminaison en appelant la méthode `setDescription` de l’objet `CreateEndpointInfo` et en transmettant une valeur string qui décrit le point de terminaison.
   * Indiquez le nom du point de terminaison en appelant la méthode `setName` de l’objet `CreateEndpointInfo` et en transmettant une valeur string qui spécifie le nom.
   * Spécifiez le service auquel appartient le point de terminaison en appelant la méthode `setServiceId` de l’objet `CreateEndpointInfo` et en transmettant une valeur string qui spécifie le nom du service.
   * Indiquez l’opération appelée en appelant la méthode `setOperationName` de l’objet `CreateEndpointInfo` et en transmettant une valeur string qui spécifie le nom de l’opération. En règle générale, lors de la création d’un point de fin de courrier électronique pour un service qui provient d’un processus créé dans Workbench, le nom de l’opération est appelé.

1. Spécifiez les valeurs de configuration.

   Pour chaque valeur de configuration à définir pour le point de fin Email, vous devez appeler la méthode `CreateEndpointInfo` de l’objet `setConfigParameterAsText` . Par exemple, pour définir la valeur de configuration `smtpHost`, appelez la méthode `setConfigParameterAsText` de l’objet `CreateEndpointInfo` et transmettez les valeurs suivantes :

   * Une valeur string qui spécifie le nom de la valeur de configuration. Lors de la définition de la valeur de configuration `smtpHost`, spécifiez `smtpHost`.
   * Une valeur string qui spécifie la valeur de la valeur de configuration. Lors de la définition de la valeur de configuration `smtpHost`, spécifiez une valeur string qui spécifie le nom du serveur SMTP.

   >[!NOTE]
   >
   >Pour afficher toutes les valeurs de configuration définies pour le service EncryptDocument introduites dans cette section, reportez-vous à l’exemple de code Java situé à l’adresse [QuickStart : Ajout d’un point de fin de courrier électronique à l’aide de l’API Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-an-email-endpoint-using-the-java-api).

1. Définissez les valeurs des paramètres d’entrée.

   Définissez une valeur de paramètre d’entrée en appelant la méthode `setInputParameterMapping` de l’objet `CreateEndpointInfo` et transmettez les valeurs suivantes :

   * Une valeur string qui spécifie le nom du paramètre d’entrée. Par exemple, le nom du paramètre d’entrée du service EncryptDocument est `InDoc`.
   * Une valeur string qui spécifie le type de données du paramètre d’entrée. Par exemple, le type de données du paramètre d’entrée `InDoc` est `com.adobe.idp.Document`.
   * Une valeur string qui spécifie le type de mappage. Par exemple, vous pouvez spécifier `variable`.
   * Une valeur string qui spécifie la valeur de type de mappage. Par exemple, vous pouvez spécifier &amp;ast;.pdf comme modèle de fichier.

   >[!NOTE]
   >
   >Appelez la méthode `setInputParameterMapping` pour chaque valeur de paramètre d’entrée à définir. Le processus EncryptDocument n’ayant qu’un seul paramètre d’entrée, vous devez appeler cette méthode une seule fois.

1. Définissez une valeur de paramètre de sortie.

   Définissez une valeur de paramètre de sortie en appelant la méthode `setOutputParameterMapping` de l’objet `CreateEndpointInfo` et en transmettant les valeurs suivantes :

   * Une valeur string qui spécifie le nom du paramètre de sortie. Par exemple, le nom du paramètre de sortie du service EncryptDocument est `SecuredDoc`.
   * Une valeur string qui spécifie le type de données du paramètre de sortie. Par exemple, le type de données du paramètre de sortie `SecuredDoc` est `com.adobe.idp.Document`.
   * Une valeur string qui spécifie le type de mappage. Par exemple, vous pouvez spécifier `%F.pdf`.

1. Créez le point de fin Email.

   Créez le point de terminaison en appelant la méthode `EndpointRegistryClient` de l’objet `createEndpoint` et en transmettant l’objet `CreateEndpointInfo`. Cette méthode renvoie un objet `Endpoint` qui représente le point de fin Email.

1. Activez le point de terminaison .

   Activez le point de terminaison en appelant la méthode `enable` de l’objet `EndpointRegistryClient` et en transmettant l’objet `Endpoint` renvoyé par la méthode `createEndpoint` .

**Voir également**

[Résumé des étapes](programmatically-endpoints.md#summary-of-steps)

[QuickStart : Ajout d’un point de fin Watched Folder à l’aide de l’API Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-watched-folder-endpoint-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Valeurs de configuration des emails fichier constant {#email-configuration-values-constant-file}

Le [QuickStart : L’ajout d’un point de fin de courrier électronique à l’aide de l’API Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-an-email-endpoint-using-the-java-api) utilise un fichier constant qui doit faire partie de votre projet Java pour compiler le démarrage rapide. Ce fichier constant représente les valeurs de configuration qui doivent être définies lors de l’ajout d’un point de fin de courrier électronique. Le code Java suivant représente le fichier constant.

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

## Ajout de points de fin Remoting {#adding-remoting-endpoints}

>[!NOTE]
>
>API LiveCycle Remoting obsolètes pour AEM forms on JEE.

Vous pouvez ajouter par programmation un point de terminaison Remoting à un service à l’aide de l’API Java AEM Forms. En ajoutant un point de fin Remoting, vous activez une application Flex pour appeler le service à l’aide de la commande remoting. (Voir [Appel d’AEM Forms à l’aide d’ (obsolète pour les formulaires AEM) AEM Forms Remoting](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting).)

Pour ajouter par programmation un point de fin Remoting à un service, considérez le processus de courte durée suivant nommé *EncryptDocument*.

![ar_ar_encryptdocumentprocess](assets/ar_ar_encryptdocumentprocess.png)

Ce processus accepte un document PDF non sécurisé comme valeur d’entrée, puis transmet le document PDF non sécurisé à l’opération `EncryptPDFUsingPassword` du service Encryption. Le document PDF est chiffré avec un mot de passe et le document PDF chiffré par mot de passe est la valeur de sortie de ce processus. Le nom de la valeur d’entrée (le document PDF non sécurisé) est `InDoc` et le type de données est `com.adobe.idp.Document`. Le nom de la valeur de sortie (le document PDF chiffré par mot de passe) est `SecuredDoc` et le type de données est `com.adobe.idp.Document`.

Pour montrer comment ajouter un point de fin Remoting à un service, cette section ajoute un point de fin Remoting à un service nommé EncryptDocument.

>[!NOTE]
>
>Vous ne pouvez pas ajouter de point de fin Remoting à l’aide de services web.

### Résumé des étapes {#summary_of_steps-4}

Pour supprimer un point de fin d’un service, effectuez les tâches suivantes :

1. Inclure les fichiers de projet.
1. Créez un objet `EndpointRegistryClient` .
1. Définissez les attributs de points de fin Remoting.
1. Créez un point de fin Remoting.
1. Activez le point de terminaison .

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

Les fichiers JAR suivants doivent être ajoutés au chemin de classe de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utility.jar (obligatoire si AEM Forms est déployé sur JBoss Application Server)
* jbossall-client.jar (obligatoire si AEM Forms est déployé sur JBoss Application Server)

Pour plus d’informations sur l’emplacement de ces fichiers JAR, voir [Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Création d’un objet client EndpointRegistry**

Pour ajouter un point de fin Remoting par programmation, vous devez créer un objet `EndpointRegistryClient` .

**Définition des attributs de point de fin Remoting**

Pour créer un point de fin Remoting pour un service, spécifiez les valeurs suivantes :

* **Valeur** de l&#39;identifiant du connecteur : Indique le type de point de terminaison créé. Pour créer un point de fin Remoting, spécifiez `Remoting`.
* **Description** : Indique la description du point de fin.
* **Nom** : Indique le nom du point de fin.
* **Valeur** de l’identifiant du service : Indique le service auquel appartient le point de fin. Par exemple, pour ajouter un point de fin Remoting au processus introduit dans cette section (un processus devient un service lorsqu’il est activé dans Workbench), spécifiez `EncryptDocument`.
* **Nom de l’opération** : Indique le nom de l’opération appelée à l’aide du point de terminaison . Lors de la création d’un point de fin Remoting, spécifiez un caractère générique (&amp;ast;).

**Création d’un point de fin Remoting**

Après avoir défini les attributs de point de fin Remoting, vous pouvez créer un point de fin Remoting pour un service.

**Activation du point de terminaison**

Après avoir créé un nouveau point de terminaison, vous devez l’activer. Lorsqu’un point de fin Remoting est activé, il permet à un client Flex d’appeler le service.

**Voir également**

[Ajout d’un point de fin Remoting à l’aide de l’API Java](programmatically-endpoints.md#add-a-remoting-endpoint-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Ajoutez un point de fin Remoting à l’aide de l’API Java {#add-a-remoting-endpoint-using-the-java-api}

Ajoutez un point de terminaison Remoting à l’aide de l’API Java :

1. Inclure les fichiers de projet.

   Incluez les fichiers JAR client, tels que adobe-livecycle-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un objet Client EndpointRegistry.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `EndpointRegistryClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`.

1. Définissez les attributs de points de fin Remoting.

   * Créez un objet `CreateEndpointInfo` en utilisant son constructeur.
   * Indiquez la valeur de l’identifiant du connecteur en appelant la méthode `setConnectorId` de l’objet `CreateEndpointInfo` et en transmettant la valeur de chaîne `Remoting`.
   * Spécifiez la description du point de terminaison en appelant la méthode `setDescription` de l’objet `CreateEndpointInfo` et en transmettant une valeur string qui décrit le point de terminaison.
   * Indiquez le nom du point de terminaison en appelant la méthode `setName` de l’objet `CreateEndpointInfo` et en transmettant une valeur string qui spécifie le nom.
   * Spécifiez le service auquel appartient le point de terminaison en appelant la méthode `setServiceId` de l’objet `CreateEndpointInfo` et en transmettant une valeur string qui spécifie le nom du service.
   * Spécifiez l’opération appelée par la méthode `setOperationName` de l’objet `CreateEndpointInfo` et transmettez une valeur string qui spécifie le nom de l’opération. Pour un point de fin Remoting, spécifiez un caractère générique (&amp;ast;).

1. Créez un point de fin Remoting.

   Créez le point de terminaison en appelant la méthode `EndpointRegistryClient` de l’objet `createEndpoint` et en transmettant l’objet `CreateEndpointInfo`. Cette méthode renvoie un objet `Endpoint` qui représente le nouveau point de fin Remoting.

1. Activez le point de terminaison .

   Activez le point de terminaison en appelant la méthode `enable` de l’objet `EndpointRegistryClient` et en transmettant l’objet `Endpoint` renvoyé par la méthode `createEndpoint` .

**Voir également**

[Résumé des étapes](programmatically-endpoints.md#summary-of-steps)

[QuickStart : Ajout d’un point de fin Remoting à l’aide de l’API Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-remoting-endpoint-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Ajout de points de fin TaskManager {#adding-taskmanager-endpoints}

Vous pouvez ajouter par programmation un point d’entrée TaskManager à un service à l’aide de l’API Java AEM Forms. En ajoutant un point de fin TaskManager à un service, vous activez un utilisateur Workspace à appeler le service. En d’autres termes, un utilisateur travaillant dans Workspace peut appeler un processus qui possède un point d’entrée TaskManager correspondant.

>[!NOTE]
>
>Vous ne pouvez pas ajouter de point de fin TaskManager à l’aide de services Web.

### Résumé des étapes {#summary_of_steps-5}

Pour ajouter un point d’entrée TaskManager à un service, effectuez les tâches suivantes :

1. Inclure les fichiers de projet.
1. Créez un objet `EndpointRegistryClient` .
1. Créez une catégorie pour le point de terminaison .
1. Définissez les attributs TaskManager endpoint .
1. Créez un point de fin TaskManager.
1. Activez le point de terminaison .

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

Les fichiers JAR suivants doivent être ajoutés au chemin de classe de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utility.jar (obligatoire si AEM Forms est déployé sur JBoss Application Server)
* jbossall-client.jar (obligatoire si AEM Forms est déployé sur JBoss Application Server)

Pour plus d’informations sur l’emplacement de ces fichiers JAR, voir [Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Création d’un objet client EndpointRegistry**

Avant de pouvoir ajouter par programmation un point d’entrée TaskManager, vous devez créer un objet `EndpointRegistryClient`.

**Création d’une catégorie pour le point de fin**

Les catégories sont utilisées pour organiser les services dans Workspace. En d’autres termes, un utilisateur de Workspace peut appeler un service disposant d’un point de terminaison TaskManager en sélectionnant une catégorie dans Workspace. Lors de la création d’un point de fin TaskManager, vous pouvez référencer une catégorie existante ou créer une catégorie par programmation.

>[!NOTE]
>
>Cette section crée une catégorie dans le cadre de l’ajout d’un point de fin TaskManager à un service.

**Définition des attributs de point d’entrée TaskManager**

Pour créer un point d’entrée TaskManager pour un service, spécifiez les valeurs suivantes :

* **Identifiant** du connecteur : Indique le type de point de terminaison créé. Pour créer un point d’entrée TaskManager, spécifiez `TaskManagerConnector`.
* **Description** : Indique la description du point de fin.
* **Nom** : Indique le nom du point de fin.
* **Identifiant** du service : Indique le service auquel appartient le point de fin.
* **Catégorie** : Spécifie une valeur d’identifiant de catégorie associée au point de terminaison TaskManager.
* **Nom de l’opération** : En règle générale, lors de la création d’un point d’entrée TaskManager pour un service issu d’un processus créé dans Workbench, le nom de l’opération est  `invoke`.

**Création d’un point d’entrée TaskManager**

Après avoir défini des attributs de point d’entrée TaskManager, vous pouvez créer un point d’entrée TaskManager pour un service.

**Activation du point de terminaison**

Après avoir créé un nouveau point de terminaison, vous devez l’activer. Lorsque le point de terminaison est activé, il peut être utilisé pour appeler le service depuis Workspace. Une fois le point de terminaison activé, vous pouvez l’afficher dans Administration Console.

**Voir également**

[Ajout d’un point d’entrée TaskManager à l’aide de l’API Java](programmatically-endpoints.md#add-a-taskmanager-endpoint-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Ajoutez un point d’entrée TaskManager à l’aide de l’API Java {#add-a-taskmanager-endpoint-using-the-java-api}

Ajoutez un point d’entrée TaskManager à l’aide de l’API Java :

1. Inclure les fichiers de projet.

   Incluez les fichiers JAR client, tels que adobe-livecycle-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un objet Client EndpointRegistry.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `EndpointRegistryClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`.

1. Créez une catégorie pour le point de terminaison .

   * Créez un objet `CreateEndpointCategoryInfo` en utilisant son constructeur et en transmettant les valeurs suivantes :

      * Une valeur string qui spécifie la valeur d’identifiant de la catégorie
      * Une valeur string qui spécifie la description de la catégorie
   * Créez la catégorie en appelant la méthode `EndpointRegistryClient` de l’objet `createEndpointCategory` et en transmettant l’objet `CreateEndpointCategoryInfo`. Cette méthode renvoie un objet `EndpointCategory` qui représente la nouvelle catégorie.


1. Définissez les attributs TaskManager endpoint .

   * Créez un objet `CreateEndpointInfo` en utilisant son constructeur.
   * Indiquez la valeur de l’identifiant du connecteur en appelant la méthode `setConnectorId` de l’objet `CreateEndpointInfo` et en transmettant la valeur de chaîne `TaskManagerConnector`.
   * Spécifiez la description du point de terminaison en appelant la méthode `setDescription` de l’objet `CreateEndpointInfo` et en transmettant une valeur string qui décrit le point de terminaison.
   * Indiquez le nom du point de terminaison en appelant la méthode `setName` de l’objet `CreateEndpointInfo` et en transmettant une valeur string qui spécifie le nom.
   * Spécifiez le service auquel appartient le point de terminaison en appelant la méthode `setServiceId` de l’objet `CreateEndpointInfo` et en transmettant une valeur string qui spécifie le nom du service.
   * Indiquez la catégorie à laquelle appartient le point de terminaison en appelant la méthode `setCategoryId` de l’objet `CreateEndpointInfo` et en transmettant une valeur string qui spécifie la valeur de l’identifiant de catégorie. Vous pouvez appeler la méthode `getId` de l’objet `EndpointCategory` pour obtenir la valeur d’identifiant de cette catégorie.
   * Indiquez l’opération appelée en appelant la méthode `setOperationName` de l’objet `CreateEndpointInfo` et en transmettant une valeur string qui spécifie le nom de l’opération. En règle générale, lors de la création d’un point de terminaison `TaskManager` pour un service qui provient d’un processus créé dans Workbench, le nom de l’opération est `invoke`.

1. Créez un point de fin TaskManager.

   Créez le point de terminaison en appelant la méthode `EndpointRegistryClient` de l’objet `createEndpoint` et en transmettant l’objet `CreateEndpointInfo`. Cette méthode renvoie un objet `Endpoint` qui représente le nouveau point de terminaison TaskManager.

1. Activez le point de terminaison .

   Activez le point de terminaison en appelant la méthode `enable` de l’objet `EndpointRegistryClient` et en transmettant l’objet `Endpoint` renvoyé par la méthode `createEndpoint` .

**Voir également**

[Résumé des étapes](programmatically-endpoints.md#summary-of-steps)

[QuickStart : Ajout d’un point de fin TaskManager à l’aide de l’API Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-taskmanager-endpoint-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Modification des points de fin {#modifying-endpoints}

Vous pouvez modifier un point de terminaison existant par programmation à l’aide de l’API Java AEM Forms. En modifiant un point de terminaison, vous pouvez modifier le comportement du point de terminaison. Prenons l’exemple d’un point de fin Watched Folder qui spécifie un dossier utilisé comme dossier de contrôle. Vous pouvez modifier par programmation les valeurs de configuration qui appartiennent au point de fin Watched Folder, ce qui entraîne l’utilisation d’un autre dossier en tant que dossier de contrôle. Pour plus d’informations sur les valeurs de configuration qui appartiennent à un point de fin Watched Folder, voir [Ajout de points de fin Watched Folder](programmatically-endpoints.md#adding-watched-folder-endpoints).

Pour montrer comment modifier un point de fin, cette section modifie un point de fin Watched Folder en modifiant le dossier qui se comporte comme le dossier de contrôle.

>[!NOTE]
>
>Vous ne pouvez pas modifier un point de terminaison à l’aide des services Web.

### Résumé des étapes {#summary_of_steps-6}

Pour modifier un point de fin, effectuez les tâches suivantes :

1. Inclure les fichiers de projet.
1. Créez un objet `EndpointRegistryClient` .
1. Récupérez le point de terminaison .
1. Spécifiez de nouvelles valeurs de configuration.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

Les fichiers JAR suivants doivent être ajoutés au chemin de classe de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utility.jar (obligatoire si AEM Forms est déployé sur JBoss Application Server)
* jbossall-client.jar (obligatoire si AEM Forms est déployé sur JBoss Application Server)

Pour plus d’informations sur l’emplacement de ces fichiers JAR, voir [Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Création d’un objet client EndpointRegistry**

Pour modifier un point de terminaison par programmation, vous devez créer un objet `EndpointRegistryClient`.

**Récupération du point de terminaison à modifier**

Avant de pouvoir modifier un point de terminaison, vous devez le récupérer. Pour récupérer un point de terminaison, vous devez vous connecter en tant qu’utilisateur pouvant accéder à un point de terminaison . Il est recommandé de se connecter en tant qu’administrateur. (Voir [Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)).

Vous pouvez récupérer un point de fin en récupérant une liste de points de fin. Vous pouvez ensuite effectuer une itération dans la liste, en recherchant le point de terminaison spécifique à supprimer. Par exemple, vous pouvez localiser un point de terminaison en déterminant le service qui correspond au point de terminaison et le type de point de terminaison. Lorsque vous localisez le point de terminaison, vous pouvez le modifier.

**Définition de nouvelles valeurs de configuration**

Lors de la modification d’un point de fin, spécifiez de nouvelles valeurs de configuration. Par exemple, pour modifier un point de fin Watched Folder, réinitialisez toutes les valeurs de configuration de point de fin Watched Folder, et pas seulement celles que vous souhaitez modifier. Pour plus d’informations sur les valeurs de configuration qui appartiennent à un point de fin Watched Folder, voir [Ajout de points de fin Watched Folder](programmatically-endpoints.md#adding-watched-folder-endpoints).

>[!NOTE]
>
>Pour plus d’informations sur les valeurs de configuration qui appartiennent à un point de fin de courrier électronique, voir [Ajout de points de fin de courrier électronique](programmatically-endpoints.md#adding-email-endpoints).

>[!NOTE]
>
>Vous ne pouvez pas modifier le service appelé par le point de terminaison . Si vous tentez de modifier le service, une exception est générée. Pour modifier le service associé à un point de terminaison donné, supprimez ce dernier et créez-en un nouveau. (Voir [Suppression des points de fin](programmatically-endpoints.md#removing-endpoints).)

**Voir également**

[Modification d’un point de terminaison à l’aide de l’API Java](programmatically-endpoints.md#modifying-an-endpoint-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Modification d’un point de terminaison à l’aide de l’API Java {#modifying-an-endpoint-using-the-java-api}

Modifiez un point de terminaison à l’aide de l’API Java :

1. Inclure les fichiers de projet.

   Incluez les fichiers JAR client, tels que adobe-livecycle-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un objet Client EndpointRegistry.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `EndpointRegistryClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`.

1. Récupérez le point de terminaison à modifier.

   * Récupérez une liste de tous les points de terminaison auxquels l’utilisateur actuel (spécifiés dans les propriétés de connexion) peut accéder en appelant la méthode `getEndpoints` de l’objet `EndpointRegistryClient` et en transmettant un objet `PagingFilter` qui agit comme un filtre. Vous pouvez transmettre une valeur `(PagingFilter)null` pour renvoyer tous les points de terminaison. Cette méthode renvoie un objet `java.util.List` où chaque élément est un objet `Endpoint`. Pour plus d’informations sur un objet `PagingFilter`, voir [Référence de l’API AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * Parcourez l’objet `java.util.List` pour déterminer s’il contient des points de fin. S’il existe des points de terminaison, chaque élément est une instance `EndPoint`.
   * Déterminez le service qui correspond à un point de terminaison en appelant la méthode `getServiceId` de l’objet `EndPoint`. Cette méthode renvoie une valeur string qui spécifie le nom du service.
   * Déterminez le type de point de terminaison en appelant la méthode `getConnectorId` de l’objet `EndPoint`. Cette méthode renvoie une valeur string qui spécifie le type de point de terminaison . Par exemple, si le point de fin est un point de fin Watched Folder, cette méthode renvoie `WatchedFolder`.

1. Spécifiez de nouvelles valeurs de configuration.

   * Créez un objet `ModifyEndpointInfo` en appelant son constructeur.
   * Pour chaque valeur de configuration à définir, appelez la méthode `setConfigParameterAsText` de l’objet `ModifyEndpointInfo`. Par exemple, pour définir la valeur de configuration de l’URL, appelez la méthode `setConfigParameterAsText` de l’objet `ModifyEndpointInfo` et transmettez les valeurs suivantes :

      * Une valeur string qui spécifie le nom de la valeur de configuration. Par exemple, pour définir la valeur de configuration `url`, spécifiez `url`.
      * Une valeur string qui spécifie la valeur de la valeur de configuration. Pour définir une valeur pour la valeur de configuration `url`, indiquez l’emplacement du dossier de contrôle.
   * Appelez la méthode `modifyEndpoint` de l’objet `EndpointRegistryClient` et transmettez l’objet `ModifyEndpointInfo` .


**Voir également**

[Résumé des étapes](programmatically-endpoints.md#summary-of-steps)

[QuickStart : Modification d’un point de terminaison à l’aide de l’API Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-modifying-an-endpoint-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Suppression des points de fin {#removing-endpoints}

Vous pouvez supprimer un point de terminaison d’un service par programmation à l’aide de l’API Java AEM Forms. Après avoir supprimé un point de fin, le service ne peut pas être appelé à l’aide de la méthode d’appel activée par le point de fin. Par exemple, si vous supprimez un point de fin SOAP d’un service, vous ne pouvez pas appeler le service à l’aide du mode SOAP.

Pour montrer comment supprimer un point de fin d’un service, cette section supprime un point de fin EJB d’un service nommé *EncryptDocument*.

>[!NOTE]
>
>Vous ne pouvez pas supprimer un point de terminaison à l’aide des services Web.

### Résumé des étapes {#summary_of_steps-7}

Pour supprimer un point de fin d’un service, effectuez les tâches suivantes :

1. Inclure les fichiers de projet.
1. Créez un objet `EndpointRegistryClient` .
1. Récupérez le point de terminaison .
1. Supprimez le point de terminaison .

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

Les fichiers JAR suivants doivent être ajoutés au chemin de classe de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utility.jar (obligatoire si AEM Forms est déployé sur JBoss Application Server)
* jbossall-client.jar (obligatoire si AEM Forms est déployé sur JBoss Application Server)

Pour plus d’informations sur l’emplacement de ces fichiers JAR, voir [Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Création d’un objet client EndpointRegistry**

Pour supprimer un point de terminaison par programmation, vous devez créer un objet `EndpointRegistryClient`.

**Récupération du point de terminaison à supprimer**

Avant de pouvoir supprimer un point de terminaison, vous devez le récupérer. Pour récupérer un point de terminaison, vous devez vous connecter en tant qu’utilisateur pouvant accéder à un point de terminaison . Il est recommandé de se connecter en tant qu’administrateur. (Voir [Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)).

Vous pouvez récupérer un point de fin en récupérant une liste de points de fin. Vous pouvez ensuite effectuer une itération dans la liste, en recherchant le point de terminaison spécifique à supprimer. Par exemple, vous pouvez localiser un point de terminaison en déterminant le service qui correspond au point de terminaison et le type de point de terminaison. Lorsque vous localisez le point de terminaison, vous pouvez le supprimer.

**Suppression du point de terminaison**

Après avoir créé un nouveau point de terminaison, vous devez l’activer. Lorsque le point de terminaison est activé, il peut être utilisé pour appeler le service. Une fois le point de terminaison activé, vous pouvez l’afficher dans Administration Console.

**Voir également**

[Suppression d’un point de terminaison à l’aide de l’API Java](programmatically-endpoints.md#removing-an-endpoint-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Suppression d’un point de terminaison à l’aide de l’API Java {#removing-an-endpoint-using-the-java-api}

Supprimez un point de terminaison à l’aide de l’API Java :

1. Inclure les fichiers de projet.

   Incluez les fichiers JAR client, tels que adobe-livecycle-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un objet Client EndpointRegistry.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `EndpointRegistryClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`.

1. Récupérez le point de terminaison à supprimer.

   * Récupérez une liste de tous les points de terminaison auxquels l’utilisateur actuel (spécifiés dans les propriétés de connexion) a accès en appelant la méthode `getEndpoints` de l’objet `EndpointRegistryClient` et en transmettant un objet `PagingFilter` qui agit comme un filtre. Vous pouvez transmettre `(PagingFilter)null` pour renvoyer tous les points de terminaison. Cette méthode renvoie un objet `java.util.List` où chaque élément est un objet `Endpoint`.
   * Parcourez l’objet `java.util.List` pour déterminer s’il contient des points de fin. S’il existe des points de terminaison, chaque élément est une instance `EndPoint`.
   * Déterminez le service qui correspond à un point de terminaison en appelant la méthode `getServiceId` de l’objet `EndPoint`. Cette méthode renvoie une valeur string qui spécifie le nom du service.
   * Déterminez le type de point de terminaison en appelant la méthode `getConnectorId` de l’objet `EndPoint`. Cette méthode renvoie une valeur string qui spécifie le type de point de terminaison . Par exemple, si le point de terminaison est un point de terminaison EJB, cette méthode renvoie `EJB`.

1. Supprimez le point de terminaison .

   Supprimez le point de terminaison en appelant la méthode `remove` de l’objet `EndpointRegistryClient` et en transmettant l’objet `EndPoint` qui représente le point de terminaison à supprimer.

**Voir également**

[Résumé des étapes](programmatically-endpoints.md#summary-of-steps)

[QuickStart : Suppression d’un point de terminaison à l’aide de l’API Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-removing-an-endpoint-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Récupération des informations du connecteur de point de terminaison {#retrieving-endpoint-connector-information}

Vous pouvez récupérer par programmation des informations sur les connecteurs de point d’entrée à l’aide de l’API AEM Forms. Un connecteur permet à un point de terminaison d’appeler un service à l’aide de diverses méthodes d’appel. Par exemple, un connecteur Watched Folder permet à un point de terminaison d’appeler un service à l’aide de dossiers de contrôle. En récupérant par programmation des informations sur les connecteurs de point d’entrée, vous pouvez récupérer les valeurs de configuration associées à un connecteur, telles que les valeurs de configuration requises et celles facultatives.

Pour découvrir comment récupérer des informations sur les connecteurs de point de fin, cette section récupère des informations sur un connecteur de dossier de contrôle. (Voir [Ajout de points de fin Watched Folder](programmatically-endpoints.md#adding-watched-folder-endpoints).)

>[!NOTE]
>
>Vous ne pouvez pas récupérer des informations sur les points de fin à l’aide des services Web.

>[!NOTE]
>
>Cette rubrique utilise l’API `ConnectorRegistryClient` pour récupérer des informations sur les connecteurs de point de terminaison. (Voir [Référence de l’API AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).)

### Résumé des étapes {#summary_of_steps-8}

Pour récupérer les informations du connecteur de point d’entrée, effectuez les tâches suivantes :

1. Inclure les fichiers de projet.
1. Créez un objet `ConnectorRegistryClient` .
1. Spécifiez le type de connecteur.
1. Récupérez les valeurs de configuration.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

Les fichiers JAR suivants doivent être ajoutés au chemin de classe de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utility.jar (obligatoire si AEM Forms est déployé sur JBoss Application Server)
* jbossall-client.jar (obligatoire si AEM Forms est déployé sur JBoss Application Server)

Si AEM Forms est déployé sur un serveur d’applications J2EE pris en charge qui n’est pas JBoss, remplacez adobe-utility.jar et jbossall-client.jar par les fichiers JAR spécifiques au serveur d’applications J2EE sur lequel AEM Forms est déployé. Pour plus d’informations sur l’emplacement de tous les fichiers JAR AEM Forms, voir [Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Création d’un objet client ConnectorRegistry**

Pour récupérer par programmation les informations du connecteur de point d’entrée, créez un objet `ConnectorRegistryClient` .

**Définition du type de connecteur**

Spécifiez le type de connecteur à partir duquel récupérer les informations. Les types de connecteurs suivants existent :

* **EJB** : Permet à une application cliente d’appeler un service en mode EJB.
* **SOAP** : Permet à une application cliente d’appeler un service à l’aide du mode SOAP.
* **Watched Folder** : Permet aux dossiers de contrôle d’appeler un service.
* **Email** : Permet aux messages électroniques d’appeler un service.
* **Remoting** : Permet à une application cliente Flex d’appeler un service.
* **TaskManagerConnector** : Permet à un utilisateur de Workspace d’appeler un service depuis Workspace.

**Récupération des valeurs de configuration**

Après avoir spécifié le type de connecteur, vous pouvez récupérer des informations sur le connecteur, telles que la valeur de configuration prise en charge. Par exemple, pour n’importe quel connecteur, vous pouvez déterminer les valeurs de configuration requises et celles qui sont facultatives.

**Voir également**

[Récupération des informations du connecteur de point d’entrée à l’aide de l’API Java](programmatically-endpoints.md#retrieve-endpoint-connector-information-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Récupérer les informations du connecteur de point d’entrée à l’aide de l’API Java {#retrieve-endpoint-connector-information-using-the-java-api}

Récupérez les informations du connecteur de point d’entrée à l’aide de l’API Java :

1. Inclure les fichiers de projet. .

   Incluez les fichiers JAR client, tels que adobe-livecycle-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un objet client ConnectorRegistry.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `ConnectorRegistryClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`. 

1. Spécifiez le type de connecteur.

   Spécifiez le type de connecteur en appelant la méthode `getEndpointDefinition` de l’objet `ConnectorRegistryClient` et en transmettant une valeur string qui spécifie le type de connecteur. Par exemple, pour spécifier le type de connecteur Watched Folder, transmettez la valeur string `WatchedFolder`. Cette méthode renvoie un objet `Endpoint` correspondant au type de connecteur.

1. Récupérez les valeurs de configuration.

   * Récupérez les valeurs de configuration associées à ce point de terminaison en appelant la méthode `getConfigParameters` de l’objet `Endpoint`. Cette méthode renvoie un tableau d’objets `ConfigParameter`.
   * Récupérez des informations sur chaque valeur de configuration en récupérant chaque élément dans le tableau . Chaque élément est un objet `ConfigParameter` . Vous pouvez, par exemple, déterminer si la valeur de configuration est requise ou facultative en appelant la méthode `isRequired` de l’objet `ConfigParameter`. Si la valeur de configuration est requise, cette méthode renvoie `true`.

**Voir également**

[Résumé des étapes](programmatically-endpoints.md#summary-of-steps)

[QuickStart : Récupération des informations du connecteur de point d’entrée à l’aide de l’API Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-retrieving-endpoint-connector-information-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
