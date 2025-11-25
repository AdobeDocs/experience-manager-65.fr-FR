---
title: Gestion des points d’entrée par programmation
description: Utilisez le service Endpoint Registry pour ajouter des points d’entrée EJB, ajouter des points d’entrée SOAP, ajouter des points d’entrée Watched Folder, ajouter des points d’entrée Email, ajouter des points d’entrée Remoting, ajouter des points d’entrée Task Manager, modifier des points d’entrée, supprimer des points d’entrée et récupérer les informations du connecteur de point d’entrée.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: b94dcca2-136b-4b7d-b5ce-544804575876
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,APIs & Integrations
source-git-commit: 07289e891399a78568dcac957bc089cc08c7898c
workflow-type: tm+mt
source-wordcount: '10799'
ht-degree: 99%

---

# Gestion des points d’entrée par programmation {#programmatically-managing-endpoints}

**Les exemples et les échantillons de ce document sont réservés à l’environnement AEM Forms sur JEE.**

**À propos du service Endpoint Registry**

Le service Endpoint Registry permet de gérer les points d’entrée par programmation. Vous pouvez, par exemple, ajouter les types de points d’entrée suivants à un service :

* EJB
* méthode d’objet
* Watched Folder
* E-mail
* (Obsolète pour AEM forms) Remoting
* Task Manager

>[!NOTE]
>
>Les points d’entrée SOAP, EJB et (obsolète pour AEM Forms sur JEE) Remoting sont automatiquement créés pour chaque service activé. Les points d’entrée SOAP et EJB activent SOAP et EJB pour toutes les opérations de service.

Un point d’entrée Remoting permet aux clients Flex d’appeler des opérations sur le service AEM Forms auquel le point d’entrée est ajouté. Une destination Flex portant le même nom que le point d’entrée est créée, ce qui permet aux clients Flex de créer des objets distants pointant vers cette destination afin d’appeler des opérations sur le service adéquat.

Les points d’entrée Email, Task Manager et Watched Folder n’exposent qu’une opération spécifique du service. L’ajout de ces points d’entrée nécessite une seconde étape de configuration pour sélectionner une méthode d’appel du service, la définition de paramètres de configuration et la spécification des mappages de paramètres d’entrée et de sortie.

Vous pouvez organiser les points d’entrée TaskManager en groupes appelés *catégories*. Ces catégories sont ensuite exposées à Workspace par le biais de TaskManager, où les utilisateurs finaux voient les points d’entrée TaskManager tels qu’ils sont classés. Dans Workspace, les utilisateurs finaux voient ces catégories dans le volet de navigation. Les points d’entrée de chaque catégorie sont affichés sous forme de cartes de processus sur la page Démarrer les processus de Workspace.

Vous pouvez accomplir ces tâches à l’aide du service Endpoint Registry :

* Ajoutez des points d’entrée EJB. (Voir [Ajouter des points d’entrée EJB](programmatically-endpoints.md#adding-ejb-endpoints).)
* Ajoutez des points d’entrée SOAP. (Voir [Ajouter des points d’entrée SOAP](programmatically-endpoints.md#adding-soap-endpoints).)
* Ajoutez des points d’entrée Watched Folder (voir [Ajouter des points d’entrée Watched Folder](programmatically-endpoints.md#adding-watched-folder-endpoints).)
* Ajoutez des points d’entrée Email. (Voir [Ajouter des points d’entrée Email](programmatically-endpoints.md#adding-email-endpoints).)
* Ajoutez des points d’entrée Remoting. (Voir [Ajouter des points d’entrée Remoting](programmatically-endpoints.md#adding-remoting-endpoints).)
* Ajoutez des points d’entrée TaskManager (voir [Ajouter des points d’entrée TaskManager](programmatically-endpoints.md#adding-taskmanager-endpoints).)
* Modifiez des points d’entrée (voir [Modifier des points d’entrée](programmatically-endpoints.md#modifying-endpoints).)
* Supprimez des points d’entrée (voir [Supprimer des points d’entrée](programmatically-endpoints.md#removing-endpoints).)
* Récupérez des informations sur le connecteur du point d’entrée (voir [Récupérer des informations sur le connecteur de point d’entrée](programmatically-endpoints.md#retrieving-endpoint-connector-information).)

## Ajouter des points d’entrée EJB {#adding-ejb-endpoints}

Vous pouvez ajouter par programmation un point d’entrée EJB à un service à l’aide de l’API Java AEM Forms. En ajoutant un point d’entrée EJB à un service, vous activez une application cliente pour appeler le service à l’aide du mode EJB. En d’autres termes, lorsque vous définissez les propriétés de connexion requises pour appeler AEM Forms, vous pouvez sélectionner le mode EJB. (Voir [Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)

>[!NOTE]
>
>Vous ne pouvez pas ajouter de point d’entrée EJB à l’aide de services web.

>[!NOTE]
>
>En règle générale, un point d’entrée EJB est ajouté par défaut à un service. Cependant, un point d’entrée EJB peut être ajouté à un processus déployé par programmation ou lorsqu’un point d’entrée EJB a été supprimé et doit être ajouté à nouveau.

### Résumé des étapes {#summary-of-steps}

Pour ajouter un point d’entrée EJB à un service, effectuez les tâches suivantes :

1. Incluez les fichiers de projet.
1. Créez un objet `EndpointRegistry Client`.
1. Définissez les attributs du point d’entrée EJB.
1. Créez un point d’entrée EJB.
1. Activez le point d’entrée.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Les fichiers JAR suivants doivent être ajoutés au chemin d’accès aux classes de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (obligatoire si AEM Forms est déployé sur JBoss Application Server)
* jbossall-client.jar (obligatoire si AEM Forms est déployé sur JBoss Application Server)

Pour plus d’informations sur l’emplacement de ces fichiers, voir [Inclure des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Créez un objet client EndpointRegistry**

Avant de pouvoir ajouter un point d’entrée EJB par programmation, vous devez créer un objet `EndpointRegistryClient`.

**Définissez les attributs du point d’entrée EJB**

Pour créer un point d’entrée EJB pour un service, spécifiez les valeurs suivantes :

* **Identifiant du connecteur** : indique le type de point d’entrée à créer. Pour créer un point d’entrée EJB, spécifiez `EJB`.
* **Description** : indique la description du point d’entrée.
* **Nom** : indique le nom du point d’entrée.
* **Identifiant du service** : indique le service auquel appartient le point d’entrée.
* **Nom de l’opération** : indique le nom de l’opération appelée à l’aide du point d’entrée. Lors de la création d’un point d’entrée EJB, spécifiez un caractère générique (`*`). Cependant, si vous souhaitez indiquer une opération spécifique plutôt que d’appeler toutes les opérations de service, indiquez le nom de l’opération au lieu d’utiliser le caractère générique (`*`).

**Créez un point d’entrée EJB**

Après avoir défini les attributs du point d’entrée EJB, vous pouvez créer un point d’entrée EJB pour un service.

**Activez le point d’entrée**

Après avoir créé un point d’entrée, vous devez l’activer. Une fois le point d’entrée activé, il peut être utilisé pour appeler le service. Une fois le point d’entrée activé, vous pouvez l’afficher dans la console d’administration.

**Voir également**

[Ajouter un point d’entrée EJB à l’aide de l’API Java](programmatically-endpoints.md#adding-an-ejb-endpoint-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Ajouter un point d’entrée EJB à l’aide de l’API Java {#adding-an-ejb-endpoint-using-the-java-api}

Ajoutez un point d’entrée EJB à l’aide de l’API Java :

1. Incluez les fichiers de projet.

   Incluez les fichiers JAR client, tels qu’adobe-livecycle-client.jar, dans le chemin d’accès aux classes de votre projet Java. (

1. Créez un objet client EndpointRegistry.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `EndpointRegistryClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`. 

1. Définissez les attributs du point d’entrée EJB.

   * Créez un objet `CreateEndpointInfo` en utilisant son constructeur.
   * Spécifiez la valeur de l’identifiant du connecteur en appelant la méthode `setConnectorId` de l’objet `CreateEndpointInfo` et en transmettant la valeur de chaîne `EJB`.
   * Fournissez une description du point d’entrée en appelant la méthode `setDescription` de l’objet `CreateEndpointInfo` et en transmettant une valeur de chaîne qui décrit le point d’entrée.
   * Indiquez le nom du point d’entrée en appelant la méthode `setName` de l’objet `CreateEndpointInfo` et en transmettant une valeur de chaîne qui spécifie le nom.
   * Spécifiez le service auquel appartient le point d’entrée en appelant la méthode `setServiceId` de l’objet `CreateEndpointInfo` et en transmettant une valeur de chaîne qui spécifie le nom du service.
   * Spécifiez l’opération appelée en appelant la méthode `setOperationName` de l’objet `CreateEndpointInfo` et en transmettant une valeur de chaîne qui spécifie le nom de l’opération. Pour les points d’entrée SOAP et EJB, spécifiez un caractère générique (`*`) qui implique toutes les opérations.

1. Créez un point d’entrée EJB.

   Créez le point d’entrée en appelant la méthode `createEndpoint` de l’objet `EndpointRegistryClient` et en transmettant l’objet `CreateEndpointInfo`. Cette méthode renvoie un objet `Endpoint` représentant le nouveau point d’entrée EJB.

1. Activez le point d’entrée.

   Activez le point d’entrée en appelant la méthode d’activation de l’objet `EndpointRegistryClient` et en transmettant l’objet `Endpoint` qui a été renvoyé par la méthode `createEndpoint`.

**Voir également**

[Résumé des étapes](programmatically-endpoints.md#summary-of-steps)

[Démarrage rapide : ajouter un point d’entrée EJB à l’aide de l’API Java.](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-an-ejb-endpoint-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Ajouter des points d’entrée SOAP {#adding-soap-endpoints}

Vous pouvez ajouter par programmation un point d’entrée SOAP à un service à l’aide de l’API Java AEM Forms. En ajoutant un point d’entrée SOAP, vous permettez à une application cliente d’appeler le service à l’aide du mode SOAP. En d’autres termes, lorsque vous définissez les propriétés de connexion requises pour appeler AEM Forms, vous pouvez sélectionner le mode SOAP.

>[!NOTE]
>
>Vous ne pouvez pas ajouter de point d’entrée SOAP à l’aide de services web.

>[!NOTE]
>
>En règle générale, un point d’entrée SOAP est ajouté par défaut à un service. Cependant, un point d’entrée SOAP peut être ajouté à un processus déployé par programmation ou lorsqu’un point d’entrée SOAP a été supprimé et doit être ajouté à nouveau.

### Résumé des étapes {#summary_of_steps-1}

Pour ajouter un point d’entrée SOAP à un service, effectuez les tâches suivantes :

1. Incluez les fichiers de projet.
1. Créez un objet `EndpointRegistryClient`.
1. Définissez les attributs de point d’entrée SOAP.
1. Créez un point d’entrée SOAP.
1. Activez le point d’entrée.

**Incluez les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services web, veillez à inclure les fichiers proxy.

Les fichiers JAR suivants doivent être ajoutés au chemin d’accès aux classes de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (obligatoire si AEM Forms est déployé sur JBoss Application Server)
* jbossall-client.jar (obligatoire si AEM Forms est déployé sur JBoss Application Server)

Ces fichiers JAR sont nécessaires pour créer un point d’entrée SOAP. Toutefois, vous avez besoin de fichiers JAR supplémentaires si vous utilisez le point d’entrée SOAP pour appeler le service. Pour plus d’informations sur les fichiers JAR AEM Forms, voir [Inclure des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Créer un objet client EndpointRegistry**

Pour ajouter par programmation un point d’entrée SOAP à un service, vous devez créer un objet `EndpointRegistryClient`.

**Définition des attributs de point d’entrée SOAP**

Pour ajouter un point d’entrée SOAP à un service, spécifiez les valeurs suivantes :

* **Valeur de l’identifiant du connecteur** : indique le type de point d’entrée à créer. Pour créer un point d’entrée SOAP, spécifiez `SOAP`.
* **Description** : indique la description du point d’entrée.
* **Nom** : indique le nom du point d’entrée.
* **Valeur d’identifiant de service** : indique le service auquel appartient le point d’entrée.
* **Nom de l’opération** : indique le nom de l’opération appelée à l’aide du point d’entrée. Lors de la création d’un point d’entrée SOAP, spécifiez un caractère générique (`*`). Cependant, si vous souhaitez spécifier une opération spécifique plutôt que d’appeler toutes les opérations de service, indiquez le nom de l’opération plutôt que d’utiliser le caractère générique (`*`).

**Créer un point d’entrée SOAP**

Après avoir défini les attributs de point d’entrée SOAP, vous pouvez créer un point d’entrée SOAP.

**Activer le point d’entrée**

Après avoir créé un point d’entrée, vous devez l’activer. Lorsque le point d’entrée est activé, il peut être utilisé pour appeler le service. Une fois le point d’entrée activé, vous pouvez l’afficher dans la console d’administration.

**Voir également**

[Ajouter un point d’entrée SOAP à l’aide de l’API Java](programmatically-endpoints.md#add-a-soap-endpoint-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Ajouter un point d’entrée SOAP à l’aide de l’API Java {#add-a-soap-endpoint-using-the-java-api}

Ajoutez un point d’entrée SOAP à un service à l’aide de l’API Java :

1. Incluez les fichiers de projet.

   Incluez les fichiers JAR client, tels qu’adobe-livecycle-client.jar, dans le chemin d’accès aux classes de votre projet Java.

1. Créez un objet client EndpointRegistry.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `EndpointRegistryClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`. 

1. Définissez les attributs de point d’entrée SOAP.

   * Créez un objet `CreateEndpointInfo` en utilisant son constructeur.
   * Spécifiez la valeur de l’identifiant du connecteur en appelant la méthode `setConnectorId` de l’objet `CreateEndpointInfo` et en transmettant la valeur de chaîne `SOAP`.
   * Fournissez une description du point d’entrée en appelant la méthode `setDescription` de l’objet `CreateEndpointInfo` et en transmettant une valeur de chaîne qui décrit le point d’entrée.
   * Indiquez le nom du point d’entrée en appelant la méthode `setName` de l’objet `CreateEndpointInfo` et en transmettant une valeur de chaîne qui spécifie le nom.
   * Spécifiez le service auquel appartient le point d’entrée en appelant la méthode `setServiceId` de l’objet `CreateEndpointInfo` et en transmettant une valeur de chaîne qui spécifie le nom du service.
   * Spécifiez l’opération appelée en appelant la méthode `setOperationName` de l’objet `CreateEndpointInfo` et en transmettant une valeur de chaîne qui spécifie le nom de l’opération. Pour les points d’entrée SOAP et EJB, spécifiez un caractère générique (`*`), ce qui implique toutes les opérations.

1. Créez un point d’entrée SOAP.

   Créez le point d’entrée en appelant la méthode `createEndpoint` de l’objet `EndpointRegistryClient` et en transmettant l’objet `CreateEndpointInfo`. Cette méthode renvoie un objet `Endpoint` représentant le nouveau point d’entrée SOAP.

1. Activez le point d’entrée.

   Activez le point d’entrée en appelant la méthode d’activation de l’objet `EndpointRegistryClient` et transmettez l’objet `Endpoint` qui a été renvoyé par la méthode `createEndpoint`.

**Voir également**

[Résumé des étapes](programmatically-endpoints.md#summary-of-steps)

[Démarrage rapide : ajouter un point d’entrée SOAP à l’aide de l’API Java.](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-soap-endpoint-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Ajouter des points d’entrée Watched Folder {#adding-watched-folder-endpoints}

Vous pouvez ajouter par programmation un point d’entrée Watched Folder à un service à l’aide de l’API Java AEM Forms. L’ajout d’un point d’entrée Watched Folder permet aux utilisateurs de placer un fichier (un fichier PDF, par exemple) dans un dossier. Lorsque le fichier est placé dans le dossier, le service configuré est alors appelé et manipule le fichier. Après que le service a effectué l’opération spécifiée, il enregistre le fichier modifié dans un dossier de sortie spécifié. Un dossier de contrôle est configuré pour être analysé à intervalles fixes ou selon une planification cron, par exemple tous les lundis, mercredis et vendredis à midi.

Pour ajouter par programmation un point d’entrée Watched Folder à un service, prenez en compte le processus de courte durée suivant nommé *EncryptDocument*. (Voir [Comprendre les processus AEM Forms](/help/forms/developing/aem-forms-processes.md#understanding-aem-forms-processes).)

![aw_aw_encryptdocumentprocess](assets/aw_aw_encryptdocumentprocess.png)

Ce processus accepte un document PDF non sécurisé comme valeur d’entrée, puis transmet le document PDF non sécurisé à l’opération `EncryptPDFUsingPassword` du service de chiffrement. Le document PDF est chiffré avec un mot de passe et le document PDF chiffré par mot de passe est la valeur de sortie de ce processus. Le nom de la valeur d’entrée (le document PDF non sécurisé) est `InDoc` et le type de données est `com.adobe.idp.Document`. Le nom de la valeur de sortie (le document PDF chiffré par mot de passe) est `SecuredDoc` et le type de données est `com.adobe.idp.Document`.

>[!NOTE]
>
>Vous ne pouvez pas ajouter de point d’entrée Watched Folder à l’aide de services web.

### Résumé des étapes {#summary_of_steps-2}

Pour ajouter un point d’entrée Watched Folder à un service, effectuez les tâches suivantes :

1. Incluez les fichiers de projet.
1. Créez un objet `EndpointRegistryClient`.
1. Définissez les attributs du point d’entrée Watched Folder.
1. Spécifiez les valeurs de configuration.
1. Définissez les valeurs des paramètres d’entrée.
1. Définissez une valeur de paramètre de sortie.
1. Créez un point d’entrée Watched Folder.
1. Activez le point d’entrée.

**Incluez les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services web, veillez à inclure les fichiers proxy.

Les fichiers JAR suivants doivent être ajoutés au chemin d’accès aux classes de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (obligatoire si AEM Forms est déployé sur JBoss Application Server)
* jbossall-client.jar (obligatoire si AEM Forms est déployé sur JBoss Application Server)

Pour plus d’informations sur l’emplacement de ces fichiers, voir [Inclure des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Créez un objet client EndpointRegistry**

Pour ajouter par programmation un point d’entrée Watched Folder, vous devez créer un objet `EndpointRegistryClient`.

**Définissez les attributs du point d’entrée Watched Folder**

Pour créer un point d’entrée Watched Folder pour un service, spécifiez les valeurs suivantes :

* **Identifiant du connecteur** : indique le type de point d’entrée créé. Pour créer un point d’entrée Watched Folder, spécifiez `WatchedFolder`.
* **Description** : indique la description du point d’entrée.
* **Nom :** indique le nom du point d’entrée.
* **Identifiant du service** : indique le service auquel appartient le point d’entrée. Par exemple, pour ajouter un point d’entrée Watched Folder au processus présenté dans cette section (un processus devient un service lorsqu’il est activé à l’aide de Workbench), spécifiez `EncryptDocument`.
* **Nom de l’opération** : indique le nom de l’opération appelée à l’aide du point d’entrée. En règle générale, lors de la création d’un point d’entrée Watched Folder pour un service issu d’un processus créé dans Workbench, le nom de l’opération est `invoke`.

**Définissez les valeurs de configuration**

Vous devez spécifier des valeurs de configuration pour un point d’entrée Watched Folder lors de l’ajout par programmation d’un point d’entrée Watched Folder à un service. Ces valeurs de configuration sont spécifiées par un administrateur si un point d’entrée Watched Folder est ajouté à l’aide de la console d’administration.

La liste suivante spécifie les valeurs de configuration définies lors de l’ajout par programmation d’un point d’entrée Watched Folder à un service :

* **URL** : indique l’emplacement du dossier surveillé. Dans un environnement organisé en grappe, ce paramètre doit pointer vers un dossier réseau partagé accessible à tous les ordinateurs de la grappe.
* **Asynchrone** : identifie le type d’invocation comme étant asynchrone ou synchrone. Les processus provisoires et synchrones peuvent être appelés uniquement de façon synchrone. La valeur par défaut est true. Asynchrone est recommandé.
* **cronExpression** : utilisé par quartz pour planifier l’interrogation du répertoire d’entrée.
* **purgeDuration** : il s’agit d’un attribut obligatoire. Les fichiers et les sous-dossiers du dossier Résultats sont vidés lorsqu’ils sont plus anciens que cette valeur. Cette valeur est mesurée en jours. Grâce à ce paramètre, le dossier obtenu n’est jamais plein. La valeur -1 jour indique de ne jamais supprimer le dossier de résultats. La valeur par défaut est -1.
* **repeatInterval** : intervalle (en secondes) entre les analyses du dossier de contrôle d’entrée. A moins que le paramètre Ralentissement ne soit activé, cette valeur doit être supérieure à la durée du traitement d’une tâche moyenne, faute de quoi le système risque d’être surchargé. La valeur par défaut est 5.
* **repeatCount** : nombre d’analyses du dossier ou du répertoire par un dossier de contrôle. La valeur -1 indique une analyse sans limite. La valeur par défaut est -1.
* **throttleOn** : limite le nombre de tâches du dossier de contrôle pouvant être traitées à un moment donné. La valeur batchSize (taille du lot) détermine le nombre maximal de tâches.
* **userName** : nom d’utilisateur utilisé lors de l’appel d’un service cible à partir du dossier de contrôle. Cette valeur est obligatoire. La valeur par défaut est SuperAdmin.
* **domainName** : domaine de l’utilisateur ou utilisatrice. Cette valeur est obligatoire. La valeur par défaut est DefaultDom.
* **batchSize** : le nombre de fichiers ou de dossiers à sélectionner par analyse. Ce paramètre permet d’éviter une surcharge du système, car l’analyse simultanée d’un trop grand nombre de fichiers peut provoquer une panne. La valeur par défaut est 2.
* **waitTime** : délai d’attente (en millisecondes) avant l’analyse d’un dossier ou d’un fichier après sa création. Par exemple, si la durée d’attente est de 36 000 000 millisecondes (une heure) et que le fichier a été créé il y a une minute, ce dernier sera sélectionné à l’issue d’un laps de temps de 59 minutes ou plus. Ce paramètre assure la copie intégrale d’un fichier ou d’un dossier dans le dossier d’entrée. Par exemple, si vous devez traiter un fichier volumineux dont le téléchargement dure dix minutes, définissez une durée d’attente de 10&amp;ast;60 &amp;ast;1000 millisecondes. Ce paramètre empêche le dossier de contrôle d’analyser le fichier s’il n’a pas attendu dix minutes. La valeur par défaut est 0.
* **excludeFilePattern** : le modèle utilisé par un dossier de contrôle pour déterminer les fichiers et les dossiers à analyser et à sélectionner. Les fichiers ou les dossiers pourvus de ce modèle ne sont pas analysés en vue d’être traités. Ce paramètre est utile lorsque l’entrée est un dossier contenant plusieurs fichiers. Vous pouvez copier le contenu du dossier dans un dossier dont le nom sera choisi par le dossier de contrôle. Ceci empêche le dossier de contrôle de sélectionner un dossier en vue de le traiter avant qu’il ne soit complètement copié dans le dossier d’entrée. Ainsi, si l’attribut excludeFilePattern a la valeur `data*`, tous les fichiers et les dossiers correspondant à `data*` ne sont pas sélectionnés. Cela inclut les fichiers et les dossiers nommés `data1`, `data2`, etc. En outre, le modèle peut être complété par des caractères génériques pour spécifier des modèles de fichier. Le dossier de contrôle modifie l’expression régulière afin de prendre en charge les modèles génériques tels que `*.*` et `*.pdf`. Ces modèles de caractères génériques ne sont pas pris en charge par les expressions régulières.
* **includeFilePattern** : le modèle utilisé par le dossier de contrôle pour déterminer les dossiers et les fichiers à analyser et à sélectionner. Ainsi, si l’attribut IncludeFilePattern a la valeur `*`, tous les fichiers et les dossiers correspondant à `input*` sont sélectionnés. Cela inclut les fichiers et les dossiers nommés `input1`, `input2`, etc. La valeur par défaut est `*`. Cette valeur indique tous les fichiers et dossiers. En outre, le modèle peut être complété par des caractères génériques pour spécifier des modèles de fichier. Le dossier de contrôle modifie l’expression régulière afin de prendre en charge les modèles génériques tels que `*.*` et `*.pdf`. Ces modèles de caractères génériques ne sont pas pris en charge par les expressions régulières. Cette valeur n’est pas obligatoire.
* **resultFolderName** : le dossier dans lequel les résultats enregistrés sont stockés. Cet emplacement peut être un chemin d’accès absolu ou relatif au répertoire. Si les résultats ne s’affichent pas dans ce dossier, vérifiez le dossier failure. Les fichiers en lecture seule ne sont pas traités et ils sont enregistrés dans le dossier failure. La valeur par défaut est `result/%Y/%M/%D/`. Il s’agit du dossier de résultats dans le dossier de contrôle.
* **preserveFolderName :** l’emplacement où les fichiers sont stockés après avoir été analysés et sélectionnés. Cet emplacement peut être un chemin d’accès de répertoire absolu, relatif ou nul. La valeur par défaut est `preserve/%Y/%M/%D/`.
* **failureFolderName :** le dossier dans lequel les fichiers d’échec sont enregistrés. Cet emplacement dépend toujours du dossier de contrôle. Les fichiers en lecture seule ne sont pas traités et ils sont enregistrés dans le dossier failure. La valeur par défaut est `failure/%Y/%M/%D/`.
* **preserveOnFailure** : conservez les fichiers d’entrée en cas d’échec de l’exécution de l’opération sur un service. La valeur par défaut est true.
* **overwriteDuplicateFilename :** lorsque la valeur définie est True, les fichiers du dossier de résultats et du dossier de fichiers conservés sont remplacés. Lorsqu’il est défini sur False, les fichiers et les dossiers qui ont un suffixe d’index numérique sont utilisés pour le nom. La valeur par défaut est false. 

**Définir les valeurs des paramètres d’entrée**

Lorsque vous créez un point d’entrée de dossier de contrôle, vous devez définir les valeurs des paramètres d’entrée. En d’autres termes, vous devez décrire les valeurs d’entrée qui sont transmises à l’opération appelée par le dossier de contrôle. Prenons le cas du processus introduit dans cette rubrique. Il comporte une valeur d’entrée appelée `InDoc` et son type de données est `com.adobe.idp.Document`. Lorsque vous créez un point d’entrée de dossier de contrôle pour ce processus (une fois qu’un processus est activé, il devient un service), vous devez définir la valeur du paramètre d’entrée.

Pour définir les valeurs des paramètres d’entrée requis pour un point d’entrée de dossier de contrôle, spécifiez les valeurs suivantes :

**Nom du paramètre d’entrée :** le nom du paramètre d’entrée. Le nom d’une valeur d’entrée est spécifié dans Workbench pour un processus. Si la valeur d’entrée appartient à une opération de service (un service qui n’est pas un processus créé dans Workbench), le nom d’entrée est spécifié dans le fichier component.xml. Par exemple, le nom du paramètre d’entrée pour le processus présenté dans cette section est `InDoc`.

**Type de mappage :** utilisé pour configurer les valeurs d’entrée requises pour appeler l’opération de service. Il existe deux types de mappage :

* `Literal` : le point d’entrée du dossier de contrôle utilise la valeur saisie dans le champ telle qu’elle s’affiche. Tous les types Java de base sont pris en charge. Par exemple, si une API utilise des entrées de type chaîne, long, nombre entier ou valeur booléenne, la chaîne est convertie en type approprié, puis le service est appelé.
* `Variable`: la valeur saisie est un modèle de fichier que le dossier de contrôle utilise pour sélectionner l’entrée. Par exemple, si vous sélectionnez Variable pour le type de mappage et si le document d’entrée doit être un fichier PDF, vous pouvez spécifier `*.pdf` comme valeur de mappage.

**Valeur de mappage :** indique la valeur du type de mappage. Par exemple, si vous sélectionnez un type de mappage `Variable`, vous pouvez spécifier `*.pdf` comme modèle de fichier.

**Type de données :** spécifie le type de données de la ou des valeurs d’entrée. Par exemple, le type de données de la valeur d’entrée du processus présenté dans cette section est `com.adobe.idp.Document`.

**Définir une valeur de paramètre de sortie**

Lors de la création d’un point d’entrée de dossier de contrôle, vous devez définir une valeur de paramètre de sortie. En d’autres termes, vous devez décrire la valeur de sortie qui est renvoyée par le service qui est appelé par le point d’entrée de dossier de contrôle. Prenons le cas du processus introduit dans cette rubrique. Il a une valeur de sortie nommée `SecuredDoc` et son type de données est `com.adobe.idp.Document`. Lorsque vous créez un point d’entrée de dossier de contrôle pour ce processus (une fois qu’un processus est activé, il devient un service), vous devez définir la valeur du paramètre de sortie.

Pour définir une valeur de paramètre de sortie requise pour un point d’entrée de dossier de contrôle, spécifiez les valeurs suivantes :

**Nom du paramètre de sortie :** le nom du paramètre de sortie. Le nom d’une valeur de sortie de processus est spécifié dans Workbench. Si la valeur de sortie appartient à une opération de service (un service qui n’est pas un processus créé dans Workbench), le nom de sortie est spécifié dans le fichier component.xml. Par exemple, le nom du paramètre de sortie pour le processus introduit dans cette section est `SecuredDoc`.

**Type de mappage** : permet de configurer les sorties du service et de l’opération. Les options suivantes sont disponibles :

* Si le service renvoie un seul objet (un seul document), le modèle est `%F.pdf` et la destination de la source est sourcefilename.pdf. Par exemple, le processus présenté dans cette section renvoie un seul document. Par conséquent, le type de mappage peut être défini en tant que `%F.pdf` (`%F` signifie utiliser le nom de fichier donné). Le motif `%E` spécifie l’extension du document d’entrée.
* Si le service renvoie une liste, le modèle est `Result\%F\`et la destination de la source est Result\nom_fichier_source1 (sortie 1) et Result\nom_fichier_source2 (sortie 2).
* Si le service renvoie une carte, le modèle est `Result\%F\` et la destination de la source est Result\nom_fichier_source\fichier1 et Result\nom_fichier_source\fichier2. Si la carte comporte plusieurs objets, le modèle est `Result\%F.pdf` et la destination de la source est Result\nom_fichier_source1.pdf (sortie 1), Result\sourcefilenam2.pdf (sortie 2), etc.

**Type de données** : indique le type de données de la valeur renvoyée. Par exemple, le type de données de la valeur renvoyée par le processus introduit dans cette section est `com.adobe.idp.Document`.

**Créer un point d’entrée Watched Folder**

Après avoir défini les attributs du point d’entrée, les valeurs de configuration et les valeurs des paramètres d’entrée et de sortie, vous devez créer le point d’entrée Watched Folder.

**Activer le point d’entrée**

Après avoir créé un point d’entrée Watched Folder, vous devez l’activer. Lorsque le point d’entrée est activé, il peut être utilisé pour appeler le service. Une fois le point d’entrée activé, vous pouvez l’afficher dans la console d’administration.

**Voir également**

[Ajouter un point d’entrée Watched Folder à l’aide de l’API Java](programmatically-endpoints.md#add-a-watched-folder-endpoint-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Ajouter un point d’entrée Watched Folder à l’aide de l’API Java {#add-a-watched-folder-endpoint-using-the-java-api}

Ajoutez un point d’entrée Watched Folder à l’aide de l’API Java AEM Forms :

1. Incluez les fichiers de projet.

   Incluez les fichiers JAR client, tels qu’adobe-livecycle-client.jar, dans le chemin d’accès aux classes de votre projet Java.

1. Créez un objet client EndpointRegistry.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `EndpointRegistryClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`. 

1. Définissez les attributs du point d’entrée Watched Folder.

   * Créez un objet `CreateEndpointInfo` en utilisant son constructeur.
   * Spécifiez la valeur de l’identifiant du connecteur en appelant la méthode `setConnectorId` de l’objet `CreateEndpointInfo` et en transmettant la valeur de chaîne `WatchedFolder`.
   * Fournissez une description du point d’entrée en appelant la méthode `setDescription` de l’objet `CreateEndpointInfo` et en transmettant une valeur de chaîne qui décrit le point d’entrée.
   * Indiquez le nom du point d’entrée en appelant la méthode `setName` de l’objet `CreateEndpointInfo` et en transmettant une valeur de chaîne qui spécifie le nom.
   * Spécifiez le service auquel appartient le point d’entrée en appelant la méthode `setServiceId` de l’objet `CreateEndpointInfo` et en transmettant une valeur de chaîne qui spécifie le nom du service.
   * Spécifiez l’opération appelée en appelant la méthode `setOperationName` de l’objet `CreateEndpointInfo` et en transmettant une valeur de chaîne qui spécifie le nom de l’opération. En règle générale, lors de la création d’un point d’entrée Watched Folder pour un service issu d’un processus créé dans Workbench, le nom de l’opération est appelé.

1. Spécifiez les valeurs de configuration.

   Pour chaque valeur de configuration à définir pour le point d’entrée Watched Folder, vous devez appeler la méthode `setConfigParameterAsText` de l’objet `CreateEndpointInfo`. Par exemple, pour définir la valeur de configuration `url`, appelez la méthode `setConfigParameterAsText` de l’objet `CreateEndpointInfo` et transmettez les valeurs de chaîne suivantes :

   * Valeur de chaîne spécifiant le nom de la nouvelle conception de formulaire. Lors de la définition de la valeur de configuration `url`, spécifiez `url`.
   * Valeur string qui spécifie la valeur de la valeur de configuration. Lors de la définition de la valeur de configuration `url`, spécifiez l’emplacement du dossier de contrôle.

   >[!NOTE]
   >
   >Pour afficher toutes les valeurs de configuration définies pour le service EncryptDocument, reportez-vous à l’exemple de code Java à la section [Démarrage rapide : Ajouter un point d’entrée Watched Folder à l’aide de l’API Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-watched-folder-endpoint-using-the-java-api).

1. Définissez les valeurs des paramètres d’entrée.

   Définissez une valeur de paramètre d’entrée en appelant la méthode `setInputParameterMapping` de l’objet `CreateEndpointInfo` et transmettez les valeurs suivantes :

   * Valeur string spécifiant le nom du nouveau paramètre d’entrée. Par exemple, le nom du paramètre d’entrée pour le service EncryptDocument est `InDoc`.
   * Valeur string qui spécifie le type de données du paramètre d’entrée. Par exemple, le type de données du paramètre d’entrée `InDoc` est `com.adobe.idp.Document`.
   * Valeur string qui spécifie le type de mappage. Par exemple, vous pouvez spécifier `variable`.
   * Valeur string qui spécifie la valeur du type de mappage. Par exemple, vous pouvez spécifier &amp;ast;.pdf comme modèle de fichier.

   >[!NOTE]
   >
   >Appelez la méthode `setInputParameterMapping` pour chaque valeur de paramètre d’entrée à définir. Le processus EncryptDocument n’ayant qu’un seul paramètre d’entrée, vous devez appeler cette méthode une seule fois.

1. Définissez une valeur de paramètre de sortie.

   Définissez une valeur de paramètre de sortie en appelant la méthode `setOutputParameterMapping` de l’objet `CreateEndpointInfo` et en transmettant les valeurs suivantes :

   * Valeur string spécifiant le nom du paramètre de sortie. Par exemple, le nom du paramètre de sortie pour le service EncryptDocument est `SecuredDoc`.
   * Valeur string qui spécifie le type de données du paramètre de sortie. Par exemple, le type de données du paramètre de sortie `SecuredDoc` est `com.adobe.idp.Document`.
   * Valeur string qui spécifie le type de mappage. Par exemple, vous pouvez spécifier `%F.pdf`.

1. Créez un point d’entrée Watched Folder.

   Créez le point d’entrée en appelant la méthode `createEndpoint` de l’objet `EndpointRegistryClient` et en transmettant l’objet `CreateEndpointInfo`. Cette méthode renvoie un objet `Endpoint` qui représente le point d’entrée Watched Folder.

1. Activez le point d’entrée.

   Activez le point d’entrée en appelant la méthode `enable` de l’objet `EndpointRegistryClient` et en transmettant l’objet `Endpoint` qui a été renvoyé par la méthode `createEndpoint`.

**Voir également**

[Résumé des étapes](programmatically-endpoints.md#summary-of-steps)

[Démarrage rapide : ajouter un point d’entrée Dossier de contrôle à l’aide de l’API Java.](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-watched-folder-endpoint-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Fichier constant des valeurs de configuration du dossier de contrôle {#watched-folder-configuration-values-constant-file}

Le [QuickStart : ajouter un point d’entrée Watched Folder à l’aide de l’API Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-watched-folder-endpoint-using-the-java-api) utilise un fichier constant qui doit faire partie de votre projet Java pour compiler le démarrage rapide. Ce fichier constant représente les valeurs de configuration qui doivent être définies lors de l’ajout d’un point d’entrée Watched Folder. Le code Java suivant représente le fichier constant.

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

## Ajouter des points d’entrée de courrier électronique {#adding-email-endpoints}

Vous pouvez ajouter par programmation un point d’entrée de courrier électronique à un service à l’aide de l’API Java AEM Forms. En ajoutant un point d’entrée de courrier électronique, vous permettez aux utilisateurs d’envoyer un message électronique contenant une ou plusieurs pièces jointes à un compte de messagerie spécifié. Ensuite, l’opération de configuration du service est appelée et manipule les fichiers. Une fois que le service a effectué l’opération spécifiée, il envoie un message électronique à l’expéditeur avec les fichiers modifiés comme pièces jointes.

Pour ajouter par programmation un point d’entrée de courrier électronique à un service, considérez le processus de courte durée suivant nommé *MyApplication\EncryptDocument*. Pour plus d’informations sur les processus de courte durée, voir [Comprendre les processus AEM Forms](/help/forms/developing/aem-forms-processes.md#understanding-aem-forms-processes).

![ae_ae_encryptdocumentprocess](assets/ae_ae_encryptdocumentprocess.png)

Ce processus accepte un document PDF non sécurisé comme valeur d’entrée, puis transmet le document PDF non sécurisé à l’opération `EncryptPDFUsingPassword` du service de chiffrement. Ce processus chiffre le document PDF avec un mot de passe et le renvoie comme valeur de sortie. Le nom de la valeur d’entrée (le document PDF non sécurisé) est `InDoc` et le type de données est `com.adobe.idp.Document`. Le nom de la valeur de sortie (le document PDF chiffré par mot de passe) est `SecuredDoc` et le type de données est `com.adobe.idp.Document`.

>[!NOTE]
>
>Vous ne pouvez pas ajouter de point d’entrée de courrier électronique à l’aide de services web.

### Résumé des étapes {#summary_of_steps-3}

Pour ajouter un point d’entrée de courrier électronique à un service, effectuez les tâches suivantes :

1. Incluez les fichiers de projet.
1. Créez un objet `EndpointRegistryClient`.
1. Définissez les attributs de point d’entrée de courrier électronique.
1. Spécifiez les valeurs de configuration.
1. Définissez les valeurs des paramètres d’entrée.
1. Définissez une valeur de paramètre de sortie.
1. Créez le point d’entrée de courrier électronique.
1. Activez le point d’entrée.

**Incluez les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services web, veillez à inclure les fichiers proxy.

Les fichiers JAR suivants doivent être ajoutés au chemin d’accès aux classes de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (obligatoire si AEM Forms est déployé sur JBoss Application Server)
* jbossall-client.jar (obligatoire si AEM Forms est déployé sur JBoss Application Server)

Pour plus d’informations sur l’emplacement de ces fichiers, voir [Inclure des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Créer un objet client EndpointRegistry**

Avant de pouvoir ajouter par programmation un point d’entrée de courrier électronique, vous devez créer un objet `EndpointRegistryClient`.

**Définir les attributs de point d’entrée de courrier électronique**

Pour créer un point d’entrée de courrier électronique pour un service, spécifiez les valeurs suivantes :

* **Valeur de l’identifiant du connecteur** : indique le type de point d’entrée créé. Pour créer un point d’entrée de courrier électronique, spécifiez `Email`.
* **Description** : indique une description du point d’entrée.
* **Nom** : indique le nom du point d’entrée.
* **Valeur de l’identifiant du service** : indique le service auquel appartient le point d’entrée. Par exemple, pour ajouter un point d’entrée E-mail au processus présenté dans cette section (un processus devient un service lorsqu’il est activé à l’aide de Workbench), spécifiez `EncryptDocument`.
* **Nom de l’opération** : indique le nom de l’opération appelée à l’aide du point d’entrée. En règle générale, lors de la création d’un point d’entrée E-mail pour un service qui provient d’un processus créé dans Workbench, le nom de l’opération est `invoke`.

**Spécifier les valeurs de configuration**

Spécifiez des valeurs de configuration pour un point d’entrée d’e-mail lorsque vous en ajoutez un par programmation à un service. Ces valeurs de configuration sont spécifiées par un administrateur si un point d’entrée de courrier électronique est ajouté à l’aide de la console d’administration.

>[!NOTE]
>
>Le compte de messagerie surveillé est un compte spécial, utilisé uniquement pour le point d’entrée de courrier électronique. Ce compte n’est pas un compte de messagerie typique d’un utilisateur. Le compte de messagerie d’un utilisateur ou d’une utilisatrice ordinaire ne doit pas être configuré comme le compte utilisé par le fournisseur de messagerie, car celui-ci supprime les messages e-mail de la boîte de réception une fois qu’il a terminé avec les messages.

Les valeurs de configuration suivantes sont définies lors de l’ajout par programmation d’un point d’entrée de courrier électronique à un service :

* **cronExpression** : saisissez une expression Cron si l’e-mail doit être programmé en utilisant une expression de ce type.
* **repeatCount** : nombre d’analyses du dossier ou du répertoire par le point d’entrée de courrier électronique. La valeur -1 indique une analyse sans limite. La valeur par défaut est -1.
* **repeatInterval** : taux d’analyse (en secondes) que le destinataire utilise pour vérifier le courrier entrant. La valeur par défaut est 10.
* **startDelay** : durée d’attente avant l’analyse, après le démarrage du planificateur. L’heure par défaut est 0.
* **batchSize** : nombre de messages e-mail que le destinataire traite par analyse pour obtenir des performances optimales. La valeur -1 indique tous les e-mails. La valeur par défaut est 2.
* **userName** : nom d’utilisateur utilisé lors de l’appel d’un service cible à partir d’un e-mail. La valeur par défaut est `SuperAdmin`.
* **domainName** : valeur de configuration obligatoire. La valeur par défaut est `DefaultDom`.
* **domainPattern** : spécifie les modèles de domaine d’e-mail entrant acceptés par le fournisseur. Par exemple, si le domaine `adobe.com` est utilisé, seuls les e-mails de ce domaine sont traités. Ceux provenant d’autres domaines sont ignorés.
*  **filePattern**: indique les modèles de pièce jointe de fichier entrant acceptés par le fournisseur. Cela inclut les fichiers ayant des extensions de nom de fichier spécifiques (&amp;ast;.dat, &amp;ast;.xml), les fichiers ayant des noms spécifiques (données) et les fichiers dont le nom et l’extension comportent des expressions composites (&amp;ast;.``[dD][aA]``&#39;port&#39;). La valeur par défaut est `*`.
* **recipientSuccessfulJob** : adresse électronique à laquelle sont envoyés les messages pour signaler les travaux effectués. Par défaut, un message de travail effectué est toujours envoyé à l’expéditeur. Si vous saisissez `sender`, les résultats des messages électroniques sont envoyés à l’expéditeur. Jusqu’à 100 destinataires sont pris en charge. Spécifiez d’autres destinataires au moyen de leurs adresses e-mail, séparées par des virgules. Pour désactiver cette option, ne remplissez pas ce champ. Dans certains cas, il se peut que vous souhaitiez déclencher un processus et ne pas recevoir de courrier électronique de notification du résultat. La valeur par défaut est `sender`.
* **recipientFailedJob** : adresse électronique à laquelle sont envoyés les messages pour signaler les travaux ayant échoué. Par défaut, un message de travail ayant échoué est toujours envoyé à l’expéditeur. Si vous saisissez `sender`, les résultats des messages électroniques sont envoyés à l’expéditeur. Jusqu’à 100 destinataires sont pris en charge. Spécifiez d’autres destinataires au moyen de leurs adresses e-mail, séparées par des virgules. Pour désactiver cette option, ne remplissez pas ce champ. La valeur par défaut est `sender`.
* **inboxHost** : nom ou adresse IP de l’hôte de la boîte de réception du fournisseur de messagerie électronique à analyser.
* **inboxPort** : port utilisé par le serveur de messagerie. La valeur POP3 par défaut est 110 et la valeur IMAP par défaut est 143. Si le protocole SSL est activé, la valeur POP3 par défaut est 995 et la valeur IMAP par défaut est 993.
* **inboxProtocol** : protocole utilisé par le point d’entrée de courrier électronique pour analyser la boîte de réception. Les options disponibles sont `IMAP` ou `POP3`. Le serveur de messagerie de l’hôte boîte de réception doit prendre en charge ces protocoles.
* **inboxTimeOut** : délai (en secondes) pendant lequel le fournisseur d’e-mail attend les réponses de la boîte de réception. La valeur par défaut est 60.
* **inboxUser** : nom d’utilisateur requis pour se connecter au compte e-mail. En fonction du serveur de messagerie et de la configuration, il peut s’agir uniquement de la partie nom d’utilisateur de l’e-mail ou de l’e-mail complet.
* **inboxPassword** : mot de passe de l’utilisateur de la boîte de réception.
* **inboxSSLEnabled** : définissez cette valeur pour forcer le fournisseur de messagerie à utiliser SSL lors de l’envoi de messages de notification de résultats ou d’erreurs. Assurez-vous que l’hôte IMAP ou POP3 prend en charge SSL.
* **smtpHost** : nom d’hôte du serveur de messagerie auquel le fournisseur de messagerie envoie les résultats et les messages d’erreur.
* **smtpPort** : valeur par défaut du port SMTP : 25.
* **smtpUser** : compte d’utilisateur que le fournisseur d’e-mail doit utiliser lorsqu’il envoie des notifications par e-mail pour signaler des résultats et des erreurs.
* **smtpPassword** : mot de passe du compte SMTP. Certains serveurs de messagerie ne nécessitent pas de mot de passe SMTP.
* **charSet** : jeu de caractères utilisé par le fournisseur de messagerie. La valeur par défaut est `UTF-8`.
* **smtpSSLEnabled** : définissez cette valeur pour forcer le fournisseur de messagerie à utiliser SSL lors de l’envoi de messages de notification de résultats ou d’erreurs. Assurez-vous que le serveur SMTP prend en charge SSL.
* **failedJobFolder** : spécifie un répertoire dans lequel stocker les résultats en cas de non-fonctionnement du serveur de courrier SMTP.
* **Asynchrone** : lorsque l’option est définie sur synchrone, tous les documents d’entrée sont traités, puis une seule réponse est renvoyée. Lorsque l’option est définie sur asynchrone, une réponse est envoyée pour chaque document traité. Par exemple, un point d’entrée de courrier électronique est créé pour le processus introduit dans cette rubrique et un message électronique est envoyé à la boîte de réception du point d’entrée qui contient plusieurs documents PDF non sécurisés. Lorsque tous les documents PDF sont chiffrés avec un mot de passe et que le point d’entrée est configuré comme synchrone, un seul message électronique de réponse est envoyé avec tous les documents PDF sécurisés joints. Si le point d’entrée est configuré comme asynchrone, un message électronique de réponse distinct est envoyé pour chaque document PDF sécurisé. Chaque message électronique contient un document PDF unique en tant que pièce jointe. La valeur par défaut est asynchrone.

**Définissez les valeurs de paramètre d’entrée**

Lors de la création d’un point d’entrée de courrier électronique, vous devez définir des valeurs de paramètre d’entrée. En d’autres termes, vous devez décrire les valeurs d’entrée transmises à l’opération appelée par le point d’entrée de courrier électronique. Prenons le cas du processus introduit dans cette rubrique. Il comporte une valeur d’entrée nommée `InDoc` et son type de données est `com.adobe.idp.Document`. Lors de la création d’un point d’entrée de courrier électronique pour ce processus (une fois qu’un processus est activé, il devient un service), vous devez définir la valeur du paramètre d’entrée.

Pour définir les valeurs de paramètre d’entrée requises pour un point d’entrée de courrier électronique, spécifiez les valeurs suivantes :

**Input parameter name** : nom du paramètre d’entrée. Le nom d’une valeur d’entrée est spécifié dans Workbench pour un processus. Si la valeur d’entrée appartient à une opération de service (un service Forms qui n’est pas un processus créé dans Workbench), le nom d’entrée est spécifié dans le fichier component.xml. Par exemple, le nom du paramètre d’entrée pour le processus présenté dans cette section est `InDoc`.

**Type de mappage** : utilisé pour configurer les valeurs d’entrée requises pour appeler l’opération de service. Deux types de mappage sont les suivants :

* `Literal` : le point d’entrée de courrier électronique utilise la valeur saisie dans le champ telle qu’affichée. Tous les types Java de base sont pris en charge. Par exemple, si une interface API utilise une entrée de type chaîne, long, nombre entier ou valeur booléenne, cette entrée est convertie en type approprié, puis le service est appelé.
* `Variable` : la valeur saisie est un modèle de fichier que le point d’entrée de courrier électronique utilise pour sélectionner l’entrée. Par exemple, si vous sélectionnez Variable pour le type de mappage et que le document d’entrée doit être un fichier PDF, vous pouvez spécifier `*.pdf` comme valeur de mappage.

**Valeur de mappage** : indique la valeur du type de mappage. Par exemple, si vous sélectionnez un type de mappage variable, vous pouvez spécifier `*.pdf` comme modèle de fichier.

**Type de données** : indique le type de données des valeurs d’entrée. Par exemple, le type de données de la valeur d’entrée du processus introduit dans cette section est com.adobe.idp.Document.

**Définir une valeur de paramètre de sortie**

Lors de la création d’un endpoint Email, vous devez définir une valeur de paramètre de sortie. En d’autres termes, vous devez décrire la valeur de sortie renvoyée par le service appelé par l’endpoint Email. Prenons le cas du processus introduit dans cette rubrique. Elle a une valeur de sortie nommée `SecuredDoc` et son type de données est `com.adobe.idp.Document`. Lors de la création d’un endpoint Email pour ce processus (une fois qu’un processus est activé, il devient un service), vous devez définir la valeur du paramètre de sortie.

Pour définir une valeur de paramètre de sortie requise pour un endpoint Email, spécifiez les valeurs suivantes :

**Nom du paramètre de sortie**: Nom du paramètre de sortie. Le nom d’une valeur de sortie de processus est spécifié dans Workbench. Si la valeur de sortie appartient à une opération de service (un service qui n’est pas un processus créé dans Workbench), le nom de sortie est spécifié dans le fichier component.xml. Par exemple, le nom du paramètre de sortie pour le processus introduit dans cette section est `SecuredDoc`.

**Type de mappage** : permet de configurer les sorties du service et de l’opération. Les options suivantes sont disponibles :

* Si le service renvoie un seul objet (un seul document), le modèle est `%F.pdf` et la destination de la source est sourcefilename.pdf. Par exemple, le processus présenté dans cette section renvoie un seul document. Par conséquent, le type de mappage peut être défini en tant que `%F.pdf` (`%F` signifie utiliser le nom de fichier donné). Le motif `%E` spécifie l’extension du document d’entrée.
* Si le service renvoie une liste, le modèle est `Result\%F\`et la destination de la source est Result\nom_fichier_source1 (sortie 1) et Result\nom_fichier_source2 (sortie 2).
* Si le service renvoie une carte, le modèle est `Result\%F\` et la destination de la source est Result\nom_fichier_source\fichier1 et Result\nom_fichier_source\fichier2. Si la carte comporte plusieurs objets, le modèle est `Result\%F.pdf` et la destination de la source est Result\nom_fichier_source1.pdf (sortie 1), Result\sourcefilenam2.pdf (sortie 2), etc.

**Type de données** : indique le type de données de la valeur renvoyée. Par exemple, le type de données de la valeur renvoyée par le processus introduit dans cette section est `com.adobe.idp.Document`.

**Créer le point d’entrée de courrier électronique**

Après avoir défini les attributs de point d’entrée de courrier électronique et les valeurs de configuration, ainsi que les valeurs des paramètres d’entrée et de sortie, vous devez créer le point de fin de courrier électronique.

**Activer le point d’entrée**

Après avoir créé un point d’entrée de courrier électronique, vous devez l’activer. Lorsque le point d’entrée est activé, il peut être utilisé pour appeler le service. Une fois le point d’entrée activé, vous pouvez l’afficher dans la console d’administration.

**Voir également**

[Ajouter un point d’entrée de courrier électronique à l’aide de l’API Java](programmatically-endpoints.md#add-an-email-endpoint-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Ajouter un point d’entrée de courrier électronique à l’aide de l’API Java {#add-an-email-endpoint-using-the-java-api}

Ajoutez un point d’entrée Email à l’aide de l’API Java :

1. Incluez les fichiers de projet.

   Incluez les fichiers JAR client, tels qu’adobe-livecycle-client.jar, dans le chemin d’accès aux classes de votre projet Java.

1. Créez un objet client EndpointRegistry.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `EndpointRegistryClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`. 

1. Définissez les attributs de point d’entrée de courrier électronique.

   * Créez un objet `CreateEndpointInfo` en utilisant son constructeur.
   * Spécifiez la valeur de l’identifiant du connecteur en appelant la méthode `setConnectorId` de l’objet `CreateEndpointInfo` et en transmettant la valeur de chaîne `Email`.
   * Fournissez une description du point d’entrée en appelant la méthode `setDescription` de l’objet `CreateEndpointInfo` et en transmettant une valeur de chaîne qui décrit le point d’entrée.
   * Indiquez le nom du point d’entrée en appelant la méthode `setName` de l’objet `CreateEndpointInfo` et en transmettant une valeur de chaîne qui spécifie le nom.
   * Spécifiez le service auquel appartient le point d’entrée en appelant la méthode `setServiceId` de l’objet `CreateEndpointInfo` et en transmettant une valeur de chaîne qui spécifie le nom du service.
   * Spécifiez l’opération appelée en appelant la méthode `setOperationName` de l’objet `CreateEndpointInfo` et en transmettant une valeur de chaîne qui spécifie le nom de l’opération. En règle générale, lors de la création d’un point d’entrée E-mail pour un service qui provient d’un processus créé dans Workbench, le nom de l’opération est appelé.

1. Spécifiez les valeurs de configuration.

   Pour chaque valeur de configuration à définir pour le point d’entrée d’e-mail, vous devez appeler la méthode `setConfigParameterAsText` de l’objet `CreateEndpointInfo`. Par exemple, pour définir la valeur de configuration `smtpHost`, appelez la méthode `setConfigParameterAsText` de l’objet `CreateEndpointInfo` et transmettez les valeurs suivantes :

   * Valeur de chaîne spécifiant le nom de la nouvelle conception de formulaire. Lors de la définition de la valeur de configuration `smtpHost`, spécifiez `smtpHost`.
   * Valeur string qui spécifie la valeur de la valeur de configuration. Lors du paramétrage de la valeur de configuration `smtpHost`, spécifiez une valeur string qui spécifie le nom du serveur SMTP. 

   >[!NOTE]
   >
   >Pour afficher toutes les valeurs de configuration définies pour le service EncryptDocument présentées dans cette section, reportez-vous à l’exemple de code Java situé à l’adresse [QuickStart : ajouter un point d’entrée de courrier électronique à l’aide de l’API Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-an-email-endpoint-using-the-java-api).

1. Définissez les valeurs des paramètres d’entrée.

   Définissez une valeur de paramètre d’entrée en appelant la méthode `setInputParameterMapping` de l’objet `CreateEndpointInfo` et transmettez les valeurs suivantes :

   * Valeur string spécifiant le nom du nouveau paramètre d’entrée. Par exemple, le nom du paramètre d’entrée pour le service EncryptDocument est `InDoc`.
   * Valeur string qui spécifie le type de données du paramètre d’entrée. Par exemple, le type de données du paramètre d’entrée `InDoc` est `com.adobe.idp.Document`.
   * Valeur string qui spécifie le type de mappage. Par exemple, vous pouvez spécifier `variable`.
   * Valeur string qui spécifie la valeur du type de mappage. Par exemple, vous pouvez spécifier &amp;ast;.pdf comme modèle de fichier.

   >[!NOTE]
   >
   >Appelez la méthode `setInputParameterMapping` pour chaque valeur de paramètre d’entrée à définir. Le processus EncryptDocument n’ayant qu’un seul paramètre d’entrée, vous devez appeler cette méthode une seule fois.

1. Définissez une valeur de paramètre de sortie.

   Définissez une valeur de paramètre de sortie en appelant la méthode `setOutputParameterMapping` de l’objet `CreateEndpointInfo` et en transmettant les valeurs suivantes :

   * Valeur string spécifiant le nom du paramètre de sortie. Par exemple, le nom du paramètre de sortie pour le service EncryptDocument est `SecuredDoc`.
   * Valeur string qui spécifie le type de données du paramètre de sortie. Par exemple, le type de données du paramètre de sortie `SecuredDoc` est `com.adobe.idp.Document`.
   * Valeur string qui spécifie le type de mappage. Par exemple, vous pouvez spécifier `%F.pdf`.

1. Créez le point d’entrée de courrier électronique.

   Créez le point d’entrée en appelant la méthode `createEndpoint` de l’objet `EndpointRegistryClient` et en transmettant l’objet `CreateEndpointInfo`. Cette méthode renvoie un objet `Endpoint` qui représente le point d’entrée de courrier électronique.

1. Activez le point d’entrée.

   Activez le point d’entrée en appelant la méthode `enable` de l’objet `EndpointRegistryClient` et en transmettant l’objet `Endpoint` qui a été renvoyé par la méthode `createEndpoint`.

**Voir également**

[Résumé des étapes](programmatically-endpoints.md#summary-of-steps)

[Démarrage rapide : ajouter un point d’entrée Dossier de contrôle à l’aide de l’API Java.](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-watched-folder-endpoint-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Fichier constant de valeurs de configuration des emails {#email-configuration-values-constant-file}

[QuickStart : ajouter un point d’entrée d’e-mail à l’aide de l’API Java](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-an-email-endpoint-using-the-java-api) utilise un fichier constant qui doit faire partie de votre projet Java pour compiler le démarrage rapide. Ce fichier constant représente les valeurs de configuration qui doivent être définies lors de l’ajout d’un point d’entrée de courrier électronique. Le code Java suivant représente le fichier constant.

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

## Ajouter des points d’entrée Remoting {#adding-remoting-endpoints}

>[!NOTE]
>
>API LiveCycle Remoting obsolètes pour AEM Forms on JEE.

Vous pouvez ajouter par programmation un point d’entrée Remoting à un service à l’aide de l’API Java AEM Forms. En ajoutant un point d’entrée Remoting, vous activez une application Flex pour appeler le service à l’aide de la commande Remoting. (Voir [Appeler AEM Forms à l’aide d’AEM Forms Remoting (obsolète pour AEM Forms)](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting).)

Pour ajouter par programmation un point d’entrée Remoting à un service, considérez le processus de courte durée suivant nommé *EncryptDocument*.

![ar_ar_encryptdocumentprocess](assets/ar_ar_encryptdocumentprocess.png)

Ce processus accepte un document PDF non sécurisé comme valeur d’entrée, puis transmet le document PDF non sécurisé à l’opération `EncryptPDFUsingPassword` du service de chiffrement. Le document PDF est chiffré avec un mot de passe et le document PDF chiffré par mot de passe est la valeur de sortie de ce processus. Le nom de la valeur d’entrée (le document PDF non sécurisé) est `InDoc` et le type de données est `com.adobe.idp.Document`. Le nom de la valeur de sortie (le document PDF chiffré par mot de passe) est `SecuredDoc` et le type de données est `com.adobe.idp.Document`.

Pour montrer comment ajouter un point d’entrée Remoting à un service, cette section ajoute un point d’entrée Remoting à un service nommé EncryptDocument.

>[!NOTE]
>
>Vous ne pouvez pas ajouter de point d’entrée Remoting à l’aide de services web.

### Résumé des étapes {#summary_of_steps-4}

Pour supprimer un point d’entrée d’un service, effectuez les tâches suivantes :

1. Incluez les fichiers de projet.
1. Créez un objet `EndpointRegistryClient`.
1. Définissez les attributs des points d’entrée Remoting.
1. Créez un point d’entrée Remoting.
1. Activez le point d’entrée.

**Incluez les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services web, veillez à inclure les fichiers proxy.

Les fichiers JAR suivants doivent être ajoutés au chemin d’accès aux classes de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (obligatoire si AEM Forms est déployé sur JBoss Application Server)
* jbossall-client.jar (obligatoire si AEM Forms est déployé sur JBoss Application Server)

Pour plus d’informations sur l’emplacement de ces fichiers, voir [Inclure des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Créer un objet client EndpointRegistry**

Pour ajouter un point d’entrée Remoting par programmation, vous devez créer un objet `EndpointRegistryClient`.

**Définir les attributs du point d’entrée Remoting**

Pour créer un point d’entrée Remoting pour un service, spécifiez les valeurs suivantes :

* **Valeur de l’identifiant du connecteur** : indique le type de point d’entrée créé. Pour créer un point d’entrée Remoting, spécifiez `Remoting`.
* **Description** : fournit une description du point d’entrée.
* **Nom** : indique le nom du point d’entrée.
* **Valeur de l’identifiant du service** : indique le service auquel appartient le point d’entrée. Par exemple, pour ajouter un point d’entrée Remoting au processus présenté dans cette section (un processus devient un service lorsqu’il est activé dans Workbench), spécifiez `EncryptDocument`.
* **Nom de l’opération** : indique le nom de l’opération appelée à l’aide du point d’entrée. Lors de la création d’un point d’entrée Remoting, spécifiez un caractère générique (&amp;ast;).

**Créer un point d’entrée Remoting**

Une fois que vous avez défini les attributs du point d’entrée Remoting, vous pouvez créer un point d’entrée Remoting pour un service.

**Activer le point d’entrée**

Après avoir créé un point d’entrée, vous devez l’activer. Lorsqu’un point d’entrée Remoting est activé, il permet à un client Flex d’appeler le service.

**Voir également**

[Ajouter un point d’entrée Remoting à l’aide de l’API Java](programmatically-endpoints.md#add-a-remoting-endpoint-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Ajouter un point d’entrée Remoting à l’aide de l’API Java {#add-a-remoting-endpoint-using-the-java-api}

Poir ajouter un point d’entrée Remoting à l’aide de l’API Java, procédez comme suit :

1. Incluez les fichiers de projet.

   Incluez les fichiers JAR client, tels qu’adobe-livecycle-client.jar, dans le chemin d’accès aux classes de votre projet Java.

1. Créez un objet client EndpointRegistry.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `EndpointRegistryClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`.

1. Définissez les attributs des points d’entrée Remoting.

   * Créez un objet `CreateEndpointInfo` en utilisant son constructeur.
   * Spécifiez la valeur de l’identifiant du connecteur en appelant la méthode `setConnectorId` de l’objet `CreateEndpointInfo` et en transmettant la valeur de chaîne `Remoting`.
   * Fournissez une description du point d’entrée en appelant la méthode `setDescription` de l’objet `CreateEndpointInfo` et en transmettant une valeur de chaîne qui décrit le point d’entrée.
   * Indiquez le nom du point d’entrée en appelant la méthode `setName` de l’objet `CreateEndpointInfo` et en transmettant une valeur de chaîne qui spécifie le nom.
   * Spécifiez le service auquel appartient le point d’entrée en appelant la méthode `setServiceId` de l’objet `CreateEndpointInfo` et en transmettant une valeur de chaîne qui spécifie le nom du service.
   * Spécifiez l’opération appelée par la méthode `setOperationName` de l’objet `CreateEndpointInfo` et transmettez une valeur de chaîne qui spécifie le nom de l’opération. Pour un point d’entrée Remoting, spécifiez un caractère générique (&amp;ast;).

1. Créez un point d’entrée Remoting.

   Créez le point d’entrée en appelant la méthode `createEndpoint` de l’objet `EndpointRegistryClient` et en transmettant l’objet `CreateEndpointInfo`. Cette méthode renvoie un objet `Endpoint` qui représente le nouveau point d’entrée Remoting.

1. Activez le point d’entrée.

   Activez le point d’entrée en appelant la méthode `enable` de l’objet `EndpointRegistryClient` et en transmettant l’objet `Endpoint` qui a été renvoyé par la méthode `createEndpoint`.

**Voir également**

[Résumé des étapes](programmatically-endpoints.md#summary-of-steps)

[Démarrage rapide : ajouter un point d’entrée Remoting à l’aide de l’API Java.](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-remoting-endpoint-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Ajouter des points d’entrée TaskManager {#adding-taskmanager-endpoints}

Vous pouvez ajouter par programmation un point d’entrée TaskManager à un service à l’aide de l’API Java AEM Forms. En ajoutant un point d’entrée TaskManager à un service, vous permettez à un utilisateur Workspace d’appeler le service. En d’autres termes, un utilisateur travaillant dans Workspace peut appeler un processus auquel correspond un point d’entrée TaskManager.

>[!NOTE]
>
>Vous ne pouvez pas ajouter de point d’entrée TaskManager à l’aide de services web.

### Résumé des étapes {#summary_of_steps-5}

Pour ajouter un point d’entrée TaskManager à un service, procédez comme suit :

1. Incluez les fichiers de projet.
1. Créez un objet `EndpointRegistryClient`.
1. Créez une catégorie pour le point d’entrée.
1. Définissez les attributs du point d’entrée TaskManager.
1. Créez un point d’entrée TaskManager.
1. Activez le point d’entrée.

**Incluez les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services web, veillez à inclure les fichiers proxy.

Les fichiers JAR suivants doivent être ajoutés au chemin d’accès aux classes de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (obligatoire si AEM Forms est déployé sur JBoss Application Server)
* jbossall-client.jar (obligatoire si AEM Forms est déployé sur JBoss Application Server)

Pour plus d’informations sur l’emplacement de ces fichiers, voir [Inclure des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Créer un objet client EndpointRegistry**

Avant de pouvoir ajouter un point d’entrée TaskManager par programmation, vous devez créer un objet `EndpointRegistryClient`.

**Créer une catégorie pour le point d’entrée**

Les catégories sont utilisées pour organiser les services dans Workspace. En d’autres termes, un utilisateur de Workspace peut appeler un service disposant d’un point d’entrée TaskManager en sélectionnant une catégorie dans Workspace. Lors de la création d’un point d’entrée TaskManager, vous pouvez référencer une catégorie existante ou en créer une par programmation.

>[!NOTE]
>
>Cette section permet de créer une catégorie dans le cadre de l’ajout d’un point d’entrée TaskManager à un service.

**Définissez les attributs du point d’entrée TaskManager**

Pour créer un point d’entrée TaskManager pour un service, spécifiez les valeurs suivantes :

* **Identifiant du connecteur**: indique le type de point d’entrée créé. Pour créer un point d’entrée TaskManager, spécifiez `TaskManagerConnector`.
* **Description**: indique la description du point d’entrée.
* **Nom :** indique le nom du point d’entrée.
* **Identifiant du service** : indique le service auquel appartient le point d’entrée.
* **Catégorie** : spécifie une valeur d’identifiant de catégorie associée au point d’entrée TaskManager.
* **Nom de l’opération** : en règle générale, lors de la création d’un point d’entrée TaskManager pour un service issu d’un processus créé dans Workbench, le nom de l’opération est `invoke`.

**Créez un point d’entrée TaskManager**

Après avoir défini des attributs de point d’entrée TaskManager, vous pouvez créer un point d’entrée TaskManager pour un service.

**Activez le point d’entrée**

Après avoir créé un point d’entrée, vous devez l’activer. Lorsque le point d’entrée est activé, il peut être utilisé pour appeler le service depuis Workspace. Une fois le point d’entrée activé, vous pouvez l’afficher dans la console d’administration.

**Voir également**

[Ajoutez un point d’entrée TaskManager à l’aide de l’API Java](programmatically-endpoints.md#add-a-taskmanager-endpoint-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Ajoutez un point d’entrée TaskManager à l’aide de l’API Java {#add-a-taskmanager-endpoint-using-the-java-api}

Ajoutez un point d’entrée TaskManager à l’aide de l’API Java :

1. Incluez les fichiers de projet.

   Incluez les fichiers JAR client, tels qu’adobe-livecycle-client.jar, dans le chemin d’accès aux classes de votre projet Java.

1. Créez un objet client EndpointRegistry.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `EndpointRegistryClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`. 

1. Créez une catégorie pour le point d’entrée.

   * Créez un objet `CreateEndpointCategoryInfo` en utilisant son constructeur et en transmettant les valeurs suivantes :

      * Une valeur string représentant la valeur de l’identifiant de la catégorie
      * Valeur string spécifiant la description de la catégorie

   * Créez la catégorie en appelant la méthode `createEndpointCategory` de l’objet `EndpointRegistryClient` et en transmettant l’objet `CreateEndpointCategoryInfo`. Cette méthode renvoie un objet `EndpointCategory` représentant la nouvelle catégorie.

1. Définissez les attributs du point d’entrée TaskManager.

   * Créez un objet `CreateEndpointInfo` en utilisant son constructeur.
   * Spécifiez la valeur de l’identifiant du connecteur en appelant la méthode `setConnectorId` de l’objet `CreateEndpointInfo` et en transmettant la valeur de chaîne `TaskManagerConnector`.
   * Fournissez une description du point d’entrée en appelant la méthode `setDescription` de l’objet `CreateEndpointInfo` et en transmettant une valeur de chaîne qui décrit le point d’entrée.
   * Indiquez le nom du point d’entrée en appelant la méthode `setName` de l’objet `CreateEndpointInfo` et en transmettant une valeur de chaîne qui spécifie le nom.
   * Spécifiez le service auquel appartient le point d’entrée en appelant la méthode `setServiceId` de l’objet `CreateEndpointInfo` et en transmettant une valeur de chaîne qui spécifie le nom du service.
   * Spécifiez la catégorie à laquelle appartient le point d’entrée en appelant la méthode `setCategoryId` de l’objet `CreateEndpointInfo` et en transmettant une valeur de chaîne qui spécifie la valeur de l’identifiant de catégorie. Vous pouvez appeler la méthode `getId` de l’objet `EndpointCategory` afin d’obtenir la valeur d’identifiant de cette catégorie.
   * Spécifiez l’opération appelée en appelant la méthode `setOperationName` de l’objet `CreateEndpointInfo` et en transmettant une valeur de chaîne qui spécifie le nom de l’opération. En règle générale, lors de la création d’un point d’entrée `TaskManager` pour un service qui provient d’un processus créé dans Workbench, le nom de l’opération est `invoke`.

1. Créez un point d’entrée TaskManager.

   Créez le point d’entrée en appelant la méthode `createEndpoint` de l’objet `EndpointRegistryClient` et en transmettant l’objet `CreateEndpointInfo`. Cette méthode renvoie un objet `Endpoint` qui représente le nouveau point d’entrée TaskManager.

1. Activez le point d’entrée.

   Activez le point d’entrée en appelant la méthode `enable` de l’objet `EndpointRegistryClient` et en transmettant l’objet `Endpoint` qui a été renvoyé par la méthode `createEndpoint`.

**Voir également**

[Résumé des étapes](programmatically-endpoints.md#summary-of-steps)

[Démarrage rapide : ajouter un point d’entrée TaskManager à l’aide de l’API Java.](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-taskmanager-endpoint-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Modifier les points d’entrée {#modifying-endpoints}

Vous pouvez modifie par programmation un point d’entrée existant à l’aide de l’API Java dʼAEM Forms. Lorsque vous modifiez un point d’entrée, vous modifiez également son comportement. Prenons l’exemple d’un point d’entrée « Watched Folder » (Dossier de contrôle), qui spécifie un dossier utilisé comme dossier de contrôle. Vous pouvez modifier par programmation les valeurs de configuration qui appartiennent au point d’entrée Watched Folder. En conséquence, un autre dossier agira en tant que dossier de contrôle. Pour plus d’informations sur les valeurs de configuration qui appartiennent à un point d’entrée Watched Folder, consultez la section [Ajouter des points d’entrée Watched Folder](programmatically-endpoints.md#adding-watched-folder-endpoints).

Cette section décrit la modification dʼun point d’entrée, en lʼoccurence un point d’entrée Watched Folder, en modifiant le dossier qui se comporte comme le dossier de contrôle.

>[!NOTE]
>
>Vous ne pouvez pas modifier un point dʼentrée à l’aide des services web.

### Résumé des étapes {#summary_of_steps-6}

Pour modifier un point dʼentée, procédez comme suit :

1. Incluez les fichiers de projet.
1. Créez un objet `EndpointRegistryClient`.
1. Récupérez le point d’entrée.
1. Spécifiez de nouvelles valeurs de configuration.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services web, veillez à inclure les fichiers proxy.

Les fichiers JAR suivants doivent être ajoutés au chemin d’accès aux classes de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (obligatoire si AEM Forms est déployé sur JBoss Application Server)
* jbossall-client.jar (obligatoire si AEM Forms est déployé sur JBoss Application Server)

Pour plus d’informations sur l’emplacement de ces fichiers, voir [Inclure des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Créer un objet EndpointRegistry Client**

Pour modifier un point dʼentrée par programmation, vous devez créer un objet `EndpointRegistryClient`.

**Récupérer le point dʼentrée à modifier**

Avant de pouvoir modifier un point dʼentrée, vous devez le récupérer. Pour récupérer un point d’entrée, vous devez vous connecter en tant qu’utilisateur autorisé à accéder aux points d’entrée. Il est recommandé de se connecter en tant qu’administrateur. (Voir [Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)).

Vous pouvez récupérer un point d’entrée en récupérant une liste de points d’entrée. Vous pouvez ensuite effectuer une itération au sein de la liste et rechercher le point d’entrée spécifique à supprimer. Par exemple, vous pouvez localiser un point d’entrée en déterminant le service correspondant et le type de point d’entrée. Lorsque vous avez localisé le point dʼentrée, vous pouvez le modifier.

**Définir de nouvelles valeurs de configuration**

Lors de la modification d’un point dʼentrée, spécifiez de nouvelles valeurs de configuration. Par exemple, pour modifier un point dʼentrée Watched Folder, réinitialisez toutes les valeurs de configuration du point dʼentrée Watched Folder, et pas seulement celles que vous souhaitez modifier. Pour plus d’informations sur les valeurs de configuration disponibles pour un point dʼentrée Watched Folder, consultez la section [Ajouter des points dʼentrée Watched Folder](programmatically-endpoints.md#adding-watched-folder-endpoints).

>[!NOTE]
>
>Pour plus d’informations sur les valeurs de configuration disponibles pour un point dʼentrée Email, consultez la section [Ajouter des points dʼentrée Email](programmatically-endpoints.md#adding-email-endpoints).

>[!NOTE]
>
>Vous ne pouvez pas modifier le service appelé par le point dʼentrée. Dans le cas contraire, une exception est générée. Pour modifier le service associé à un point dʼentrée spécifique, supprimez ce dernier et créez-en un. (Consultez la section [Supprimer des points dʼentrée](programmatically-endpoints.md#removing-endpoints)).

**Voir également**

[Modifier un point dʼentrée à l’aide de l’API Java](programmatically-endpoints.md#modifying-an-endpoint-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Modifier un point dʼentrée à l’aide de l’API Java {#modifying-an-endpoint-using-the-java-api}

Pour modifier un point dʼentrée à l’aide de l’API Java, procédez comme suit :

1. Incluez les fichiers de projet.

   Incluez les fichiers JAR client, tels qu’adobe-livecycle-client.jar, dans le chemin d’accès aux classes de votre projet Java.

1. Créez un objet client EndpointRegistry.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `EndpointRegistryClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`.

1. Récupérez le point dʼentrée à modifier.

   * Récupérez une liste de tous les points dʼentrée auxquels l’utilisateur ou l’utilisatrice en cours (spécifiés dans les propriétés de connexion) peut accéder en appelant la méthode `getEndpoints` de lʼobjet `EndpointRegistryClient` et en transmettant un objet `PagingFilter` qui agit comme un filtre. Vous pouvez transmettre une valeur `(PagingFilter)null` pour retourner tous les points dʼentrée. Cette méthode renvoie un objet `java.util.List` où chaque élément est un objet `Endpoint`. Pour plus d’informations sur lʼobjet `PagingFilter`, consultez la section [Référence API pour AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * Effectuez une itération à l’aide de l’objet `java.util.List` pour déterminer s’il contient des points d’entrée. Si des points d’entrée existent, chaque élément est une instance `EndPoint`.
   * Déterminez le service qui correspond à un point d’entrée en appelant la méthode `getServiceId` de l’objet `EndPoint`. Cette méthode renvoie une valeur de chaîne qui spécifie le nom du service.
   * Déterminez le type de point d’entrée en appelant la méthode `getConnectorId` de l’objet `EndPoint`. Cette méthode renvoie une valeur de chaîne qui spécifie le type de point d’entrée. Par exemple, si le point d’entrée est un point d’entrée Watched Folder, cette méthode renvoie la valeur `WatchedFolder`.

1. Spécifiez de nouvelles valeurs de configuration.

   * Créez un objet `ModifyEndpointInfo` en utilisant son constructeur.
   * Pour chaque valeur de configuration à définir, appelez la méthode `setConfigParameterAsText` de l’objet `ModifyEndpointInfo`. Par exemple, pour définir la valeur de configuration de l’URL, appelez la méthode `setConfigParameterAsText` de l’objet `ModifyEndpointInfo` et transmettez les valeurs suivantes :

      * Valeur de chaîne spécifiant le nom de la nouvelle conception de formulaire. Par exemple, pour définir la valeur de configuration `url`, spécifiez `url`.
      * Valeur string qui spécifie la valeur de la valeur de configuration. Pour définir une valeur pour la valeur de configuration `url`, spécifiez l’emplacement du dossier de contrôle.

   * Appelez la méthode `modifyEndpoint` de l’objet `EndpointRegistryClient` et transmettez l’objet `ModifyEndpointInfo`.

**Voir également**

[Résumé des étapes](programmatically-endpoints.md#summary-of-steps)

[Démarrage rapide : modifier un point d’entrée à l’aide de l’API Java.](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-modifying-an-endpoint-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Supprimer des points d’entrée {#removing-endpoints}

Vous pouvez supprimer par programmation un point d’entrée d’un service à l’aide de l’API Java AEM Forms. Après avoir supprimé un point d’entrée, le service ne peut pas être appelé à l’aide de la méthode d’appel activée par le point d’entrée. Par exemple, si vous supprimez un point d’entrée SOAP d’un service, vous ne pouvez pas appeler le service à l’aide du mode SOAP.

Cette section décrit comment supprimer un point d’entrée EJB d’un service nommé *EncryptDocument*.

>[!NOTE]
>
>Vous ne pouvez pas supprimer un point d’entrée à l’aide de services web.

### Résumé des étapes {#summary_of_steps-7}

Pour supprimer un point d’entrée d’un service, effectuez les tâches suivantes :

1. Incluez les fichiers de projet.
1. Créez un objet `EndpointRegistryClient`.
1. Récupérez le point d’entrée.
1. Supprimez le point d’entrée.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services web, veillez à inclure les fichiers proxy.

Les fichiers JAR suivants doivent être ajoutés au chemin d’accès aux classes de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (obligatoire si AEM Forms est déployé sur JBoss Application Server)
* jbossall-client.jar (obligatoire si AEM Forms est déployé sur JBoss Application Server)

Pour plus d’informations sur l’emplacement de ces fichiers, voir [Inclure des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Créer un objet client EndpointRegistry**

Pour supprimer un point d’entrée par programmation, vous devez créer un objet `EndpointRegistryClient`.

**Récupérer le point d’entrée à supprimer**

Avant de pouvoir supprimer un point d’entrée, vous devez le récupérer. Pour récupérer un point d’entrée, vous devez vous connecter en tant qu’utilisateur autorisé à accéder aux points d’entrée. Il est recommandé de se connecter en tant qu’administrateur. (Voir [Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)).

Vous pouvez récupérer un point d’entrée en récupérant une liste de points d’entrée. Vous pouvez ensuite effectuer une itération au sein de la liste et rechercher le point d’entrée spécifique à supprimer. Par exemple, vous pouvez localiser un point d’entrée en déterminant le service correspondant et le type de point d’entrée. Une fois localisé, vous pouvez le supprimer.

**Supprimer le point d’entrée**

Après avoir créé un point d’entrée, vous devez l’activer. Lorsque le point d’entrée est activé, il peut être utilisé pour appeler le service. Une fois le point d’entrée activé, vous pouvez l’afficher dans la console d’administration.

**Voir également**

[Supprimer un point d’entrée à l’aide de l’API Java](programmatically-endpoints.md#removing-an-endpoint-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Supprimer un point d’entrée à l’aide de l’API Java {#removing-an-endpoint-using-the-java-api}

Pour supprimer un point d’entrée à l’aide de l’API Java, procédez comme suit :

1. Incluez les fichiers de projet.

   Incluez les fichiers JAR client, tels qu’adobe-livecycle-client.jar, dans le chemin d’accès aux classes de votre projet Java.

1. Créez un objet client EndpointRegistry.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `EndpointRegistryClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`.

1. Récupérez le point d’entrée à supprimer.

   * Récupérez une liste de tous les points d’entrée auxquels l’utilisateur ou l’utilisatrice en cours (spécifiés dans les propriétés de connexion) a accès en appelant la méthode `getEndpoints` de l’objet `EndpointRegistryClient` et en transmettant un objet `PagingFilter` qui agit comme un filtre. Vous pouvez transmettre `(PagingFilter)null` pour renvoyer tous les points d’entrée. Cette méthode renvoie un objet `java.util.List` où chaque élément est un objet `Endpoint`.
   * Effectuez une itération au sein de l’objet `java.util.List` pour déterminer s’il contient des points d’entrée. Si des points d’entrée existent, chaque élément est une instance `EndPoint`.
   * Déterminez le service qui correspond à un point d’entrée en appelant la méthode `getServiceId` de l’objet `EndPoint`. Cette méthode renvoie une valeur de chaîne qui spécifie le nom du service.
   * Déterminez le type de point d’entrée en appelant la méthode `getConnectorId` de l’objet `EndPoint`. Cette méthode renvoie une valeur de chaîne qui spécifie le type de point d’entrée. Par exemple, si le point d’entrée est un point d’entrée EJB, cette méthode renvoie la valeur `EJB`.

1. Supprimez le point d’entrée.

   Supprimez le point d’entrée en appelant la méthode `remove` de l’objet `EndpointRegistryClient` et en transmettant l’objet `EndPoint` qui représente le point d’entrée à supprimer.

**Voir également**

[Résumé des étapes](programmatically-endpoints.md#summary-of-steps)

[Démarrage rapide : supprimer un point d’entrée à l’aide de l’API Java.](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-removing-an-endpoint-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Récupérer les informations du connecteur de point d’entrée {#retrieving-endpoint-connector-information}

Vous pouvez récupérer par programmation des informations sur les connecteurs de point d’entrée à l’aide de l’API AEM Forms. Un connecteur permet à un point d’entrée d’appeler un service à l’aide de diverses méthodes d’appel. Par exemple, un connecteur Watched Folder permet à un point d’entrée d’appeler un service à l’aide de dossiers de contrôle. En récupérant par programmation des informations sur les connecteurs de point d’entrée, vous pouvez récupérer les valeurs de configuration associées à un connecteur, telles que les valeurs de configuration requises et celles facultatives.

Dans cette section, découvrez comment récupérer des informations sur les connecteurs de point d’entrée, en l’occurence le connecteur Watched Folder. (Consultez la section [Ajouter des points d’entrée Watched Folder](programmatically-endpoints.md#adding-watched-folder-endpoints)).

>[!NOTE]
>
>Vous ne pouvez pas récupérer d’informations sur les points d’entrée à l’aide des services web.

>[!NOTE]
>
>Cette rubrique utilise l’API `ConnectorRegistryClient` pour récupérer des informations sur les connecteurs de point d’entrée. (Consultez la section [Référence de l’API AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)).

### Résumé des étapes {#summary_of_steps-8}

Pour récupérer les informations du connecteur de point d’entrée, procédez comme suit :

1. Incluez les fichiers de projet.
1. Créez un objet `ConnectorRegistryClient`.
1. Spécifiez le type de connecteur.
1. Récupérez les valeurs de configuration.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services web, veillez à inclure les fichiers proxy.

Les fichiers JAR suivants doivent être ajoutés au chemin d’accès aux classes de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (obligatoire si AEM Forms est déployé sur JBoss Application Server)
* jbossall-client.jar (obligatoire si AEM Forms est déployé sur JBoss Application Server)

Si AEM Forms est déployé sur un serveur d’applications J2EE pris en charge qui n’est pas JBoss, remplacez adobe-utilities.jar et jbossall-client.jar par les fichiers JAR spécifiques au serveur d’applications J2EE sur lequel AEM Forms est déployé. Pour plus d’informations sur l’emplacement de tous les fichiers JAR AEM Forms, consultez la section [Inclure des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Créez un objet client ConnectorRegistry**

Pour récupérer par programmation les informations du connecteur de point d’entrée, créez un objet `ConnectorRegistryClient`.

**Définissez le type de connecteur**

Spécifiez le type de connecteur à partir duquel récupérer les informations. Les types de connecteurs suivants existent :

* **EJB** : permet à une application cliente d’appeler un service en mode EJB.
* **SOAP** : permet à une application cliente d’appeler un service à l’aide du mode SOAP.
* **Watched Folder** : permet aux dossiers de contrôle d’appeler un service.
* **Email** : permet aux messages électroniques d’appeler un service.
* **Remoting** : permet à une application cliente Flex d’appeler un service.
* **TaskManagerConnector** : permet à un utilisateur de Workspace d’appeler un service depuis Workspace.

**Récupérez les valeurs de configuration**

Après avoir spécifié le type de connecteur, vous pouvez récupérer des informations sur le connecteur, telles que la valeur de configuration prise en charge. Par exemple, pour n’importe quel connecteur, vous pouvez déterminer les valeurs de configuration requises et celles qui sont facultatives.

**Voir également**

[Récupérez les informations du connecteur de point d’entrée à l’aide de l’API Java](programmatically-endpoints.md#retrieve-endpoint-connector-information-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Récupérez les informations du connecteur de point d’entrée à l’aide de l’API Java {#retrieve-endpoint-connector-information-using-the-java-api}

Récupérez les informations du connecteur de point d’entrée à l’aide de l’API Java :

1. Incluez les fichiers de projet.

   Incluez les fichiers JAR client, tels qu’adobe-livecycle-client.jar, dans le chemin d’accès aux classes de votre projet Java.

1. Créez un objet client ConnectorRegistry.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `ConnectorRegistryClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`. 

1. Spécifiez le type de connecteur.

   Spécifiez le type de connecteur en appelant la méthode `getEndpointDefinition` de l’objet `ConnectorRegistryClient` et en transmettant une valeur de chaîne qui spécifie le type de connecteur. Par exemple, pour spécifier le type de connecteur Watched Folder, transmettez la valeur string `WatchedFolder`. Cette méthode renvoie un objet `Endpoint` qui correspond au type de connecteur.

1. Récupérez les valeurs de configuration.

   * Récupérez les valeurs de configuration associées à ce point d’entrée en appelant la méthode `getConfigParameters` de l’objet `Endpoint`. Cette méthode renvoie un tableau d’objets `ConfigParameter`.
   * Récupérez des informations sur chaque valeur de configuration en récupérant chaque élément dans le tableau. Chaque élément est un objet `ConfigParameter`. Vous pouvez, par exemple, déterminer si la valeur de configuration est requise ou facultative en appelant la méthode `isRequired` de l’objet `ConfigParameter`. Si la valeur de configuration est requise, cette méthode renvoie `true`.

**Voir également**

[Résumé des étapes](programmatically-endpoints.md#summary-of-steps)

[Démarrage rapide : récupérer des informations du connecteur de point d’entrée à l’aide de l’API Java.](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-retrieving-endpoint-connector-information-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
