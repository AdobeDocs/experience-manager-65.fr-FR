---
title: Utilisation du référentiel AEM Forms
seo-title: Utilisation du référentiel AEM Forms
description: Gérez le référentiel AEM Forms pour créer des dossiers, écrire, répertorier, lire, mettre à jour et rechercher des ressources à l’aide de l’API Java et de l’API de service Web. En outre, découvrez comment créer des relations de ressources, verrouiller et supprimer des ressources.
seo-description: Gérez le référentiel AEM Forms pour créer des dossiers, écrire, répertorier, lire, mettre à jour des ressources et rechercher des ressources à l’aide de l’API Java et de l’API de service Web. En outre, découvrez comment créer des relations de ressources, verrouiller et supprimer des ressources.
uuid: 6ead49f9-ca0d-4ee4-86a6-0a9ced6ec4f8
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: d2c95881-6c02-4e34-85af-84607df54287
role: Developer
exl-id: a07e51ca-fea0-4719-8071-1b7e805de2ae
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '9157'
ht-degree: 2%

---

# Utilisation du référentiel AEM Forms {#working-with-aem-forms-repository}

**Les exemples et les exemples de ce document sont réservés à l’environnement AEM Forms on JEE.**

**À propos du service de référentiel**

Le service Repository fournit des services de stockage et de gestion des ressources à AEM Forms. Lorsque les développeurs créent une application *AEM Forms*, ils peuvent déployer les ressources dans le référentiel au lieu du système de fichiers. Les actifs peuvent être constitués de formulaires XML, de formulaires PDF (y compris de formulaires Acrobat), de fragments de formulaire, d’images, de profils, de stratégies, de fichiers SWF, DDX et WSDL, de schémas XML et de données de test.

Prenons l’exemple de l’application Forms suivante nommée *Applications/FormsApplication* :

![www_www_formrepository](assets/ww_ww_formrepository.png)

Notez qu’un fichier nommé Loan.xdp se trouve dans le dossier Forms. Pour accéder à cette conception de formulaire, vous devez spécifier le chemin d’accès complet (y compris la version) : `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.

>[!NOTE]
>
>Pour plus d’informations sur la création d’une application Forms à l’aide de Workbench, voir [Aide de Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).

Le chemin d’accès à une ressource située dans le référentiel AEM Forms est le suivant :

`Applications/Application-name/Application-version/Folder.../Filename`

Les valeurs suivantes présentent quelques exemples de valeurs URI :

* Applications/AppraisalReport/1.0/Forms/FullForm.xdp
* Applications/AnotherApp/1.1/Assets/picture.jpg
* Applications/SomeApp/2.0/Resources/Data/XSDs/MyData.xsd

>[!NOTE]
>
>Vous pouvez parcourir le référentiel AEM Forms à l’aide d’un navigateur web. Pour parcourir le référentiel, saisissez l’URL suivante dans un navigateur Web `https://[server name]:[server port]/repository`. Vous pouvez vérifier les résultats de démarrage rapide associés à la section Utilisation du référentiel AEM Forms à l’aide d’un navigateur web. Par exemple, si vous ajoutez du contenu au référentiel AEM Forms, vous pouvez afficher le contenu dans un navigateur web. (Voir [Démarrage rapide (mode SOAP) : Écriture d’une ressource à l’aide de l’API Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-writing-a-resource-using-the-java-api).)

L’API de référentiel fournit un certain nombre d’opérations que vous pouvez utiliser pour stocker et récupérer des informations du référentiel. Par exemple, vous pouvez obtenir une liste des ressources ou récupérer des ressources spécifiques stockées dans le référentiel lorsqu’une ressource est nécessaire dans le cadre du traitement d’une application.

>[!NOTE]
>
>L’API de référentiel ne peut pas être utilisée pour interagir avec Content Services (obsolète). Pour interagir avec Content Services (obsolète), vous utilisez l’API Document Management.

À l’aide de l’API Repository, vous pouvez accomplir les tâches suivantes :

* Création de dossiers. Voir [Création de dossiers](aem-forms-repository.md#creating-folders).
* Écrivez des ressources et leurs propriétés. Voir [Écriture de ressources](aem-forms-repository.md#writing-resources).
* Répertorier les ressources d’une collection donnée ou associées à d’autres ressources. Voir [Liste des ressources](aem-forms-repository.md#listing-resources).
* Lisez les ressources et leurs propriétés. Voir [Ressources de lecture](aem-forms-repository.md#reading-resources).
* Mettez à jour les ressources et leurs propriétés. Voir [Mise à jour des ressources](aem-forms-repository.md#updating-resources).
* Recherchez des ressources, y compris leur historique, les ressources associées et les propriétés. Voir [Recherche de ressources](aem-forms-repository.md#searching-for-resources).
* Spécifiez les relations entre les ressources. Voir [Création de relations de ressources](aem-forms-repository.md#creating-resource-relationships).
* Gérez le contrôle d’accès aux ressources, notamment le verrouillage et le déverrouillage des ressources, ainsi que la lecture et l’écriture des listes de contrôle d’accès (ACL). Voir [Verrouillage de ressources](aem-forms-repository.md#locking-resources).
* Supprimez les ressources et leurs propriétés. Voir [Suppression de ressources](aem-forms-repository.md#deleting-resources).

>[!NOTE]
>
>À l’aide de l’API de référentiel, vous ne pouvez pas gérer le contrôle d’accès aux ressources, rechercher des ressources ou définir des relations de ressources à l’aide d’un référentiel ECM.

>[!NOTE]
>
>Lorsqu’un fichier PDF chiffré est écrit dans le référentiel, la fonction d’extraction de relation automatisée ne peut pas être utilisée. Dans le cas contraire, un PDF chiffré peut être stocké dans le référentiel et récupéré ultérieurement. Le récupérateur peut choisir de déchiffrer le PDF après l’avoir récupéré dans le référentiel.

>[!NOTE]
>
>Pour plus d’informations sur le service Repository, voir [Guide de référence des services pour AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Création de dossiers {#creating-folders}

Les dossiers (collections de ressources) sont utilisés pour stocker des objets (fichiers ou ressources) dans des regroupements organisés. Les dossiers peuvent contenir des ressources et d’autres dossiers, également appelés sous-dossiers. Les ressources ne peuvent être stockées que dans un seul dossier à la fois.

Les fichiers héritent des listes de contrôle d’accès (ACL) des dossiers et les sous-dossiers héritent des ACL de leurs dossiers parents. Par conséquent, les dossiers parents doivent exister avant de pouvoir créer des dossiers enfants. L’IDE permet d’interagir uniquement dossier par dossier, et non fichier par fichier. Vous ne pouvez pas modifier les dossiers et il n’est pas nécessaire de le faire ; un dossier ne contient pas de données lui-même. Il s’agit plutôt uniquement d’un conteneur pour les ressources qui contiennent des données. La liste de contrôle d’accès par défaut est une autorisation de niveau système, ce qui signifie que les utilisateurs doivent disposer d’autorisations de niveau système (lecture, écriture, traversée, gestion des listes de contrôle d’accès) jusqu’à ce qu’une personne leur donne des autorisations pour un dossier particulier. Les listes de contrôle d’accès ne fonctionnent que dans l’IDE.

>[!NOTE]
>
>Pour plus d’informations sur le service Repository, voir [Guide de référence des services pour AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary-of-steps}

Pour créer un dossier, procédez comme suit :

1. Inclure les fichiers de projet.
1. Créez le client de service.
1. Créez le dossier .
1. Rédigez le dossier dans le référentiel.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, incluez les fichiers proxy.

**Création du client de service**

Avant de pouvoir créer par programmation une collection de ressources, vous devez établir une connexion et fournir des informations d’identification. Pour ce faire, créez un client de service.

**Création du dossier**

Appelez la méthode du service Repository pour créer la collection de ressources et renseigner les informations d’identification dans la collection de ressources, y compris son UUID, son nom de dossier et sa description.

**Écrire le dossier dans le référentiel**

Appelez la méthode du service Repository pour écrire la collection de ressources, en spécifiant l’URI du dossier cible.

**Voir également**

[Création de dossiers à l’aide de l’API Java](aem-forms-repository.md#create-folders-using-the-java-api)

[Création de dossiers à l’aide de l’API de service Web](aem-forms-repository.md#create-folders-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Démarrages rapides de l’API Repository Service](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Création de dossiers à l’aide de l’API Java {#create-folders-using-the-java-api}

Créez un dossier à l’aide de l’API Repository service (Java) :

1. Inclure les fichiers de projet

   Incluez des fichiers de projet dans le chemin de classe de votre projet Java.

1. Création du client de service

   Créez un objet `ResourceRepositoryClient` en utilisant son constructeur et en transmettant un objet `ServiceClientFactory` contenant des propriétés de connexion.

1. Création du dossier

   Pour créer une collection de ressources, vous devez d’abord créer un objet `com.adobe.repository.infomodel.bean.RepositoryInfomodelFactoryBean`.

   Appelez la méthode `newResourceCollection` de l’objet `repositoryInfomodelFactoryBean` et transmettez les paramètres suivants :

   * Identifiant UUID `com.adobe.repository.infomodel.Id` à attribuer à la ressource.
   * Identifiant UUID `com.adobe.repository.infomodel.Lid` à attribuer à la ressource.
   * `java.lang.String` contenant le nom de la collection de ressources. Par exemple, `FormsFolder`.

   La méthode renvoie un objet `com.adobe.repository.infomodel.bean.ResourceCollection` représentant le nouveau dossier.

   Définissez la description du dossier à l’aide de la méthode `setDescription` et transmettez le paramètre suivant :

   * `String` qui décrit la collection de ressources. Dans cet exemple, `"test Folder"` est utilisé `.`


1. Écrire le dossier dans le référentiel

   Appelez la méthode `writeResource` de l’objet `ResourceRepositoryClient` et transmettez l’URI du dossier et l’objet `ResourceCollection` . Par exemple, l’URI du dossier peut être la valeur `/Applications/FormsApplication/1.0/` suivante.

   La méthode renvoie une instance de l’objet `com.adobe.repository.infomodel.bean.Resource` nouvellement créé. Vous pouvez, par exemple, récupérer la valeur de l’identifiant de la nouvelle ressource en appelant la méthode `getId` de l’objet `com.adobe.repository.infomodel.bean.Resource`.

**Voir également**

[Création de dossiers](aem-forms-repository.md#creating-folders)

[Démarrage rapide (mode SOAP) : Création d’un dossier à l’aide de l’API Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-creating-a-folder-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Créer des dossiers à l’aide de l’API de service Web {#create-folders-using-the-web-service-api}

Créez un dossier à l’aide de l’API Repository service (service Web) :

1. Inclure les fichiers de projet

   * Créez un assemblage client Microsoft .NET qui utilise le fichier WSDL du référentiel en utilisant base64.
   * Référencez l’assemblage client Microsoft .NET.

1. Création du client de service

   À l’aide de l’assemblage client Microsoft .NET, créez un objet `RepositoryServiceService` en appelant son constructeur par défaut. Définissez sa propriété `Credentials` à l’aide d’un objet `System.Net.NetworkCredential` contenant le nom d’utilisateur et le mot de passe.

1. Création du dossier

   Créez le dossier à l’aide du constructeur par défaut pour la classe `ResourceCollection` et transmettez les paramètres suivants :

   * Objet `Id`, créé en appelant le constructeur par défaut pour la classe `Id` et affecté au champ `id` de l’objet `Resource`.
   * Objet `Lid`, créé en appelant le constructeur par défaut pour la classe `Lid` et affecté au champ `lid` de l’objet `Resource`.
   * Chaîne contenant le nom de la collection de ressources, attribuée au champ `Resource` de l’objet `name`. Le nom utilisé dans cet exemple est `"testfolder"`.
   * Chaîne contenant la description de la collection de ressources attribuée au champ `Resource` de l’objet `description`. La description utilisée dans cet exemple est `"test folder"`.

1. Écrire le dossier dans le référentiel

   Appelez la méthode `writeResource` de l’objet `RepositoryServiceService` et transmettez les paramètres suivants :

   * Chemin d’accès à l’emplacement où le dossier doit être créé.
   * Objet `ResourceCollection` représentant le dossier.
   * Transmettez `null` pour les deux autres paramètres.

**Voir également**

[Création de dossiers](aem-forms-repository.md#creating-folders)

[Appel d’AEM Forms à l’aide du codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## Écriture de ressources {#writing-resources}

Vous pouvez créer des ressources à un emplacement donné dans le référentiel. La taille de fichier naturelle est soumise aux restrictions de la base de données et au délai d’expiration de la session. Pour la configuration par défaut, les fichiers sont limités à 25 Mo. Pour augmenter ou réduire la taille maximale du fichier, vous devez modifier la configuration de la base de données.

L’écriture de ressources équivaut à stocker des données dans le référentiel. Une fois que vous avez écrit une ressource dans le référentiel, elle devient accessible à tous les clients de l’écosystème de référentiel. Lorsque vous écrivez des ressources, telles que des schémas XML, des fichiers XDP et des fichiers XSD, dans le référentiel, le contenu est analysé en fonction du type MIME. Si le type MIME est pris en charge, l’analyseur détermine s’il existe une relation implicite avec d’autres contenus. Par exemple, si une feuille de style en cascade (CSS) comporte une URL relative qui fait référence à une page CSS commune, il est prévu que vous envoyiez également la page CSS commune dans le référentiel. La relation entre les deux ressources est stockée en tant que relation en attente pendant une période non ajustable de 30 jours. Lorsque vous envoyez la page CSS commune au référentiel au cours de la période de 30 jours, la relation est formée.

Lorsque vous créez une ressource, la liste de contrôle d’accès (ACL) est héritée du dossier parent. Le dossier racine dispose d’autorisations au niveau du système jusqu’à la création d’une ressource ou d’un dossier initial, auquel cas les autorisations ACL par défaut sont accordées à la ressource ou au dossier.

Vous pouvez écrire des ressources par programmation à l’aide de l’API Java du service Repository ou de l’API du service Web.

>[!NOTE]
>
>Pour plus d’informations sur le service Repository, voir [Guide de référence des services pour AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary_of_steps-1}

Pour écrire une ressource, procédez comme suit :

1. Inclure les fichiers de projet.
1. Créez un client de service Repository.
1. Spécifiez l’URI de la ressource à lire.
1. Lisez la ressource.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, incluez les fichiers proxy.

**Création du client de service**

Avant de pouvoir lire une ressource par programmation, vous devez établir une connexion et fournir des informations d’identification. Pour ce faire, créez un client de service.

**Spécifiez l’URI du dossier cible pour la ressource.**

Créez une chaîne contenant l’URI de la ressource à lire. La syntaxe comprend des barres obliques, comme dans cet exemple : &quot;/*path*/*folder*&quot;.

**Création de la ressource**

Appelez la méthode du service Repository pour créer la ressource et renseignez la ressource avec des informations d’identification, y compris son UUID, son nom et sa description.

**Définition du contenu de la ressource**

Appelez la méthode du service Repository pour créer le contenu de la ressource et stocker ce contenu dans la ressource.

**Écrire la ressource dans le dossier cible**

Appelez la méthode du service Repository pour écrire la ressource, en spécifiant l’URI du dossier cible.

**Voir également**

[Écrire des ressources à l’aide de l’API Java](aem-forms-repository.md#write-resources-using-the-java-api)

[Écrire des ressources à l’aide de l’API de service Web](aem-forms-repository.md#write-resources-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Démarrages rapides de l’API Repository Service](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Écrire des ressources à l’aide de l’API Java {#write-resources-using-the-java-api}

Ecrivez une ressource à l’aide de l’API Repository service (Java) :

1. Inclure les fichiers de projet

   Incluez les fichiers JAR client dans le chemin de classe de votre projet Java.

1. Création du client de service

   Créez un objet `ResourceRepositoryClient` en utilisant son constructeur et en transmettant un objet `ServiceClientFactory` contenant des propriétés de connexion.

1. Spécifiez l’URI du dossier cible pour la ressource.

   Spécifiez l’URI du dossier cible pour la ressource. Dans ce cas, puisque la ressource `testResource` sera stockée dans le dossier `testFolder`, l’URI du dossier est `"/testFolder"`. L’URI est stocké en tant qu’objet `java.lang.String`.

1. Création de la ressource

   Pour créer une ressource, vous devez d’abord créer un objet `com.adobe.repository.infomodel.bean.RepositoryInfomodelFactoryBean`.

   Appelez la méthode `newResource` de l’objet `RepositoryInfomodelFactoryBean`, qui crée un objet `com.adobe.repository.infomodel.bean.Resource`. Dans cet exemple, les paramètres suivants sont fournis :

   * Objet `com.adobe.repository.infomodel.Id`, créé en appelant le constructeur par défaut pour la classe `Id`.
   * Objet `com.adobe.repository.infomodel.Lid`, créé en appelant le constructeur par défaut pour la classe `Lid`.
   * `java.lang.String` contenant le nom de fichier de la ressource.

   Pour spécifier la description de la ressource, appelez la méthode `setDescription` de l’objet `Resource` et transmettez une chaîne contenant la description. Dans cet exemple, la description est `"test resource"`.

1. Définition du contenu de la ressource

   Pour créer du contenu pour la ressource, appelez la méthode `newResourceContent` de l’objet `RepositoryInfomodelFactoryBean` , qui renvoie un objet `com.adobe.repository.infomodel.bean.ResourceContent`. Ajoutez du contenu à l’objet `ResourceContent` . Dans cet exemple, les tâches suivantes sont nécessaires :

   * Appel de la méthode `setDataDocument` de l’objet `ResourceContent` et transmission d’un objet `com.adobe.idp.Document`
   * Appel de la méthode `setSize` de l’objet `ResourceContent` et transmission de la taille en octets de l’objet `Document`

   Ajoutez le contenu à la ressource en appelant la méthode `setContent` de l’objet `Resource` et en transmettant l’objet `ResourceContent`. Pour plus d’informations, voir [Référence de l’API AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. Écrire la ressource dans le dossier cible

   Appelez la méthode `writeResource` de l’objet `ResourceRepositoryClient` et transmettez l’URI du dossier, ainsi que l’objet `Resource` .

**Voir également**

[Écriture de ressources](aem-forms-repository.md#writing-resources)

[Démarrage rapide (mode SOAP) : Écriture d’une ressource à l’aide de l’API Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-writing-a-resource-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Écrire des ressources à l’aide de l’API de service Web {#write-resources-using-the-web-service-api}

Rédigez une ressource à l’aide de l’API Repository service (service Web) :

1. Inclure les fichiers de projet

   * Créez un assemblage client Microsoft .NET qui utilise le fichier WSDL du référentiel en utilisant base64.
   * Référencez l’assemblage client Microsoft .NET.

1. Création du client de service

   À l’aide de l’assemblage client Microsoft .NET, créez un objet `RepositoryServiceService` en appelant son constructeur par défaut. Définissez sa propriété `Credentials` à l’aide d’un objet `System.Net.NetworkCredential` contenant le nom d’utilisateur et le mot de passe.

1. Spécifiez l’URI du dossier cible pour la ressource.

   Spécifiez l’URI du dossier cible pour la ressource. Dans ce cas, puisque la ressource `testResource` sera stockée dans le dossier `testFolder`, l’URI du dossier est `"/testFolder"`. Lorsque vous utilisez un langage conforme à Microsoft .NET Framework (C#, par exemple), stockez l’URI dans un objet `System.String` .

1. Création de la ressource

   Pour créer une ressource, appelez le constructeur par défaut pour la classe `Resource` . Dans cet exemple, les informations suivantes sont stockées dans l’objet `Resource` :

   * Objet `com.adobe.repository.infomodel.Id`, créé en appelant le constructeur par défaut pour la classe `Id` et affecté au champ `id` de l’objet `Resource`.
   * Objet `com.adobe.repository.infomodel.Lid`, créé en appelant le constructeur par défaut pour la classe `Lid` et affecté au champ `lid` de l’objet `Resource`.
   * Chaîne contenant le nom de fichier de la ressource, attribué au champ `Resource` de l’objet `name`. Le nom utilisé dans cet exemple est `"testResource"`.
   * Chaîne contenant la description de la ressource, attribuée au champ `description` de l’objet `Resource`. La description utilisée dans cet exemple est `"test resource"`.

1. Définition du contenu de la ressource

   Pour créer du contenu pour la ressource, appelez le constructeur par défaut pour la classe `ResourceContent` . Ajoutez ensuite du contenu à l’objet `ResourceContent` . Dans cet exemple, les tâches suivantes sont nécessaires :

   * Affectation d’un objet `BLOB` contenant un document au champ `dataDocument` de l’objet `ResourceContent`.
   * Affectez la taille en octets de l’objet `BLOB` au champ `size` de l’objet `ResourceContent`.

   Ajoutez le contenu à la ressource en affectant l’objet `ResourceContent` au champ `Resource` de l’objet `content`.

1. Écrire la ressource dans le dossier cible

   Appelez la méthode `writeResource` de l’objet `RepositoryServiceService` et transmettez l’URI du dossier, ainsi que l’objet `Resource` . Transmettez `null` pour les deux autres paramètres.

**Voir également**

[Écriture de ressources](aem-forms-repository.md#writing-resources)

[Appel d’AEM Forms à l’aide du codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## Liste des ressources {#listing-resources}

Vous pouvez découvrir des ressources en répertoriant les ressources. Une requête est exécutée sur le référentiel pour rechercher toutes les ressources liées à une collection de ressources donnée.

Une fois vos ressources organisées, vous pouvez examiner la structure que vous avez créée en visualisant une branche particulière de la structure, comme vous le feriez dans un système d’exploitation.

La liste des ressources fonctionne par relation : ressources sont des membres de dossiers. L’appartenance est représentée par une relation de type &quot;membre de&quot;. Lorsque vous répertoriez des ressources dans un dossier donné, vous recherchez des ressources liées à un dossier donné par la relation &quot;membre de&quot;. Les relations sont directionnelles : un membre d’une relation possède une source qui est un membre de la cible. La source est la ressource ; la cible est le dossier parent.

>[!NOTE]
>
>Pour plus d’informations sur le service Repository, voir [Guide de référence des services pour AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary_of_steps-2}

Pour répertorier les ressources, procédez comme suit :

1. Inclure les fichiers de projet.
1. Créez le client de service.
1. Spécifiez le chemin du dossier.
1. Récupérez la liste des ressources.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, incluez les fichiers proxy.

**Création du client de service**

Avant de pouvoir créer par programmation une collection de ressources, vous devez établir une connexion et fournir des informations d’identification. Pour ce faire, créez un client de service.

**Définition du chemin du dossier**

Créez une chaîne contenant le chemin du dossier contenant les ressources. La syntaxe comprend des barres obliques, comme dans cet exemple : &quot;/*path*/*folder*&quot;.

**Récupération de la liste des ressources**

Appelez la méthode du service Repository pour récupérer la liste des ressources, en spécifiant le chemin du dossier cible.

**Voir également**

[Liste des ressources à l’aide de l’API Java](aem-forms-repository.md#list-resources-using-the-java-api)

[Liste des ressources à l’aide de l’API de service Web](aem-forms-repository.md#list-resources-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Démarrages rapides de l’API Repository Service](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Liste des ressources à l’aide de l’API Java {#list-resources-using-the-java-api}

Répertorier les ressources à l’aide de l’API Repository service (Java) :

1. Inclure les fichiers de projet

   Incluez les fichiers JAR client dans le chemin de classe de votre projet Java.

1. Création du client de service

   Créez un objet `ResourceRepositoryClient` en utilisant son constructeur et en transmettant un objet `ServiceClientFactory` contenant des propriétés de connexion.

1. Définition du chemin du dossier

   Spécifiez l’URI de la collection de ressources à interroger. Dans ce cas, son URI est `"/testFolder"`. L’URI est stocké en tant qu’objet `java.lang.String`.

1. Récupération de la liste des ressources

   Appelez la méthode `listMembers` de l’objet `ResourceRepositoryClient` et transmettez l’URI du dossier.

   La méthode renvoie un `java.util.List` d’objets `com.adobe.repository.infomodel.bean.Resource` qui sont la source d’un `com.adobe.repository.infomodel.bean.Relation` de type `Relation.TYPE_MEMBER_OF` et dont l’URI de collecte de ressources est la cible. Vous pouvez effectuer une itération sur cette `List` pour récupérer chacune des ressources. Dans cet exemple, le nom et la description de chaque ressource s&#39;affichent.

**Voir également**

[Liste des ressources](aem-forms-repository.md#listing-resources).

[Démarrage rapide (mode SOAP) : Liste des ressources à l’aide de l’API Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-listing-resources-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Liste des ressources à l’aide de l’API de service Web {#list-resources-using-the-web-service-api}

Répertorier les ressources à l’aide de l’API Repository service (service Web) :

1. Inclure les fichiers de projet

   * Créez un assemblage client Microsoft .NET qui utilise le fichier WSDL du référentiel.
   * Référencez l’assemblage client Microsoft .NET.

1. Création du client de service

   À l’aide de l’assemblage client Microsoft .NET, créez un objet `RepositoryServiceService` en appelant son constructeur par défaut. Définissez sa propriété `Credentials` à l’aide d’un objet `System.Net.NetworkCredential` contenant le nom d’utilisateur et le mot de passe.

1. Définition du chemin du dossier

   Spécifiez une chaîne contenant l’URI du dossier à interroger. Dans ce cas, son URI est `"/testFolder"`. Lorsque vous utilisez un langage conforme à Microsoft .NET Framework (C#, par exemple), stockez l’URI dans un objet `System.String` .

1. Récupération de la liste des ressources

   Appelez la méthode `listMembers` de l’objet `RepositoryServiceService` et transmettez l’URI du dossier comme premier paramètre. Transmettez `null` pour les deux autres paramètres.

   La méthode renvoie un tableau d’objets qui peuvent être convertis en objets `Resource`. Vous pouvez effectuer une itération sur le tableau d’objets pour récupérer chacune des ressources associées. Dans cet exemple, le nom et la description de chaque ressource s&#39;affichent.

**Voir également**

[Liste des ressources](aem-forms-repository.md#listing-resources).

[Appel d’AEM Forms à l’aide du codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## Ressources de lecture {#reading-resources}

Vous pouvez récupérer des ressources à partir d’un emplacement donné dans le référentiel afin de lire leur contenu et leurs métadonnées. Le workflow est dirigé par un formulaire d’initialisation. Le processus dispose de toutes les autorisations nécessaires pour lire le formulaire. Le système récupère le formulaire de données et lit le contenu du référentiel. Le référentiel accorde l’accès au contenu et aux métadonnées (la possibilité même de connaître la ressource).

Le référentiel dispose des quatre types d’autorisations suivants :

* **traverse** : permet de répertorier les ressources ; c’est-à-dire pour lire les métadonnées de ressource, mais pas le contenu de la ressource
* **lire** : vous permet de lire le contenu de la ressource.
* **write** : vous permet d’écrire du contenu de ressource.
* **gestion des listes de contrôle d’accès**: permet de manipuler les listes de contrôle d’accès sur les ressources.

Les utilisateurs peuvent uniquement exécuter des processus lorsqu’ils sont autorisés à exécuter le processus. Les utilisateurs d’IDE doivent disposer d’autorisations de navigation et de lecture pour se synchroniser avec le référentiel. Les listes de contrôle d’accès s’appliquent uniquement au moment de la conception, car l’exécution se produit dans le contexte du système.

Vous pouvez lire des ressources par programmation à l’aide de l’API Java du service Repository ou de l’API du service Web.

>[!NOTE]
>
>Pour plus d’informations sur le service Repository, voir [Guide de référence des services pour AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary_of_steps-3}

Pour lire une ressource, procédez comme suit :

1. Inclure les fichiers de projet.
1. Créez un client de service Repository.
1. Spécifiez l’URI de la ressource à lire.
1. Lisez la ressource.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, incluez les fichiers proxy.

**Création du client de service**

Avant de pouvoir lire une ressource par programmation, vous devez établir une connexion et fournir des informations d’identification. Pour ce faire, créez un client de service.

**Spécifiez l’URI de la ressource à lire.**

Créez une chaîne contenant l’URI de la ressource à lire. La syntaxe comprend des barres obliques, comme dans cet exemple : &quot;/*path*/*resource*&quot;.

**Lire la ressource**

Appelez la méthode de service Repository pour lire la ressource, en spécifiant l’URI.

**Voir également**

[Lecture des ressources à l’aide de l’API Java](aem-forms-repository.md#read-resources-using-the-java-api)

[Lecture de ressources à l’aide de l’API de service Web](aem-forms-repository.md#reading-resources-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Démarrages rapides de l’API Repository Service](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Lire les ressources à l’aide de l’API Java {#read-resources-using-the-java-api}

Lisez une ressource à l’aide de l’API Repository service (Java) :

1. Inclure les fichiers de projet

   Incluez les fichiers JAR client dans le chemin de classe de votre projet Java.

1. Création du client de service

   Créez un objet `ResourceRepositoryClient` en utilisant son constructeur et en transmettant un objet `ServiceClientFactory` contenant des propriétés de connexion.

1. Spécifiez l’URI de la ressource à lire.

   Spécifiez une valeur string qui représente l’URI de la ressource à récupérer. Par exemple, en supposant que la ressource soit nommée *testResource* qui se trouve dans un dossier nommé *testFolder*, spécifiez `/testFolder/testResource`.

1. Lire la ressource

   Appelez la méthode `readResource` de l’objet `ResourceRepositoryClient` et transmettez l’URI de la ressource en tant que paramètre. Cette méthode renvoie une instance `Resource` qui représente la ressource.

**Voir également**

[Lire les ressources](aem-forms-repository.md#reading-resources)

[Démarrage rapide (mode SOAP) : Lecture d&#39;une ressource à l&#39;aide de l&#39;API Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-reading-a-resource-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Lecture de ressources à l’aide de l’API de service Web {#reading-resources-using-the-web-service-api}

Lisez une ressource à l’aide de l’API Repository service (service Web) :

1. Inclure les fichiers de projet

   * Créez un assemblage client Microsoft .NET qui utilise le fichier WSDL du référentiel. (Voir [Création d’un assemblage client .NET qui utilise l’encodage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding).)
   * Référencez l’assemblage client Microsoft .NET. (Voir [Création d’un assemblage client .NET qui utilise l’encodage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding).)

1. Création du client de service

   À l’aide de l’assemblage client Microsoft .NET, créez un objet `RepositoryServiceService` en appelant son constructeur par défaut. Définissez sa propriété `Credentials` à l’aide d’un objet `System.Net.NetworkCredential` contenant le nom d’utilisateur et le mot de passe.

1. Spécifiez l’URI de la ressource à lire.

   Spécifiez une chaîne contenant l’URI de la ressource à récupérer. Dans ce cas, puisque la ressource nommée `testResource` se trouve dans le dossier nommé `testFolder`, son URI est `"/testFolder/testResource"`. Lorsque vous utilisez un langage conforme à Microsoft .NET Framework (C#, par exemple), stockez l’URI dans un objet `System.String` .

1. Lire la ressource

   Appelez la méthode `readResource` de l’objet `RepositoryServiceService` et transmettez l’URI de la ressource comme premier paramètre. Transmettez `null` pour les deux autres paramètres.

**Voir également**

[Lire les ressources](aem-forms-repository.md#reading-resources)

[Appel d’AEM Forms à l’aide du codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## Mise à jour des ressources {#updating-resources}

Vous pouvez récupérer et mettre à jour le contenu des ressources dans le référentiel. Lorsque vous mettez à jour des ressources, le contrôle d’accès à ces ressources reste inchangé entre les versions. Lors d’une mise à jour, vous avez la possibilité d’incrémenter la version majeure. Si vous ne choisissez pas d’incrémenter la version majeure, la version mineure est automatiquement mise à jour.

Lorsque vous mettez à jour une ressource, la nouvelle version est créée en fonction des attributs de ressource spécifiés. Lorsque vous mettez à jour une ressource, vous spécifiez deux paramètres importants : l’URI cible et une instance de ressource contenant toutes les métadonnées mises à jour. Il est important de noter que si vous ne modifiez pas un attribut donné (par exemple, le nom), l’attribut est toujours requis dans l’instance que vous transmettez. Les relations créées lors de l’analyse du contenu sont ajoutées à la version spécifique et ne sont pas transférées, sauf indication contraire.

Par exemple, si vous mettez à jour un fichier XDP qui contient des références à d’autres ressources, ces références supplémentaires seront également enregistrées. Supposons que form.xdp version 1.0 comporte deux références externes : un logo et une feuille de style, puis vous mettez à jour le fichier form.xdp afin qu’il comporte désormais trois références : un logo, une feuille de style et un fichier de schéma. Lors de la mise à jour, le référentiel ajoute la troisième relation (au fichier de schéma) à sa table de relation en attente. Une fois que le fichier de schéma est présent dans le référentiel, la relation est automatiquement formée. Cependant, si form.xdp version 2.0 n’utilise plus le logo, form.xdp version 2.0 n’a pas de rapport avec le logo.

Toutes les opérations de mise à jour sont atomiques et transactionnelles. Par exemple, si deux utilisateurs lisent la même ressource et décident tous deux de mettre à jour la version 1.0 vers la version 2.0, l’un d’eux réussit et l’autre échoue, l’intégrité du référentiel est conservée et tous deux reçoivent un message confirmant la réussite ou l’échec. Si la transaction n’est pas validée, elle sera restaurée en cas d’échec de la base de données et expirera ou restaurera selon le serveur d’applications.

Vous pouvez mettre à jour des ressources par programmation à l’aide de l’API Java du service Repository ou de l’API du service Web.

>[!NOTE]
>
>Pour plus d’informations sur le service Repository, voir [Guide de référence des services pour AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary_of_steps-4}

Pour mettre à jour une ressource, procédez comme suit :

1. Inclure les fichiers de projet.
1. Créez un client de service Repository.
1. Récupérez la ressource à mettre à jour.
1. Mettez à jour la ressource.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, incluez les fichiers proxy.

**Création du client de service**

Avant de pouvoir lire une ressource par programmation, vous devez établir une connexion et fournir des informations d’identification. Pour ce faire, créez un client de service.

**Récupérer la ressource à mettre à jour**

Lisez la ressource. Pour plus d’informations, voir [Ressources de lecture](aem-forms-repository.md#reading-resources).

**Mettre à jour la ressource**

Définissez les nouvelles informations dans la ressource et appelez la méthode du service Repository pour mettre à jour la ressource, en spécifiant l’URI, la ressource mise à jour et la manière dont les informations de version doivent être mises à jour.

**Voir également**

[Mettre à jour des ressources à l’aide de l’API Java](aem-forms-repository.md#update-resources-using-the-java-api)

[Mettre à jour des ressources à l’aide de l’API de service Web](aem-forms-repository.md#update-resources-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Démarrages rapides de l’API Repository Service](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Mettre à jour les ressources à l’aide de l’API Java {#update-resources-using-the-java-api}

Mettez à jour une ressource à l’aide de l’API Repository service (Java) :

1. Inclure les fichiers de projet

   Incluez les fichiers JAR client dans le chemin de classe de votre projet Java.

1. Création du client de service

   Créez un objet `ResourceRepositoryClient` en utilisant son constructeur et en transmettant un objet `ServiceClientFactory` contenant des propriétés de connexion.

1. Récupérer la ressource à mettre à jour

   Spécifiez l’URI de la ressource à récupérer et à lire. Dans cet exemple, l’URI de la ressource est `"/testFolder/testResource"`.

1. Mettre à jour la ressource

   Mettez à jour les informations de l’objet `Resource`. Dans cet exemple, pour mettre à jour la description, appelez la méthode `setDescription` de l’objet `Resource` et transmettez la nouvelle chaîne de description en tant que paramètre.

   Ensuite, appelez la méthode `updateResource` de l’objet `ServiceClientFactory` et transmettez les paramètres suivants :

   * Objet `java.lang.String` contenant l’URI de la ressource.
   * Objet `Resource` contenant les informations de ressource mises à jour.
   * Valeur `boolean` indiquant s’il faut mettre à jour la version majeure ou mineure. Dans cet exemple, une valeur `true` est transmise pour indiquer que la version majeure doit être incrémentée.

**Voir également**

[Mise à jour des ressources](aem-forms-repository.md#updating-resources)

[Démarrage rapide (mode SOAP) : Mise à jour d’une ressource à l’aide de l’API Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-updating-a-resource-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Mettre à jour des ressources à l’aide de l’API de service Web {#update-resources-using-the-web-service-api}

Mettre à jour une ressource à l’aide de l’API Repository (service Web) :

1. Inclure les fichiers de projet

   * Créez un assemblage client Microsoft .NET qui utilise le fichier WSDL du référentiel.
   * Référencez l’assemblage client Microsoft .NET.

1. Création du client de service

   À l’aide de l’assemblage client Microsoft .NET, créez un objet `RepositoryServiceService` en appelant son constructeur par défaut. Définissez sa propriété `Credentials` à l’aide d’un objet `System.Net.NetworkCredential` contenant le nom d’utilisateur et le mot de passe.

1. Récupérer la ressource à mettre à jour

   Indiquez l’URI de la ressource à récupérer et lisez-la. Dans cet exemple, l’URI de la ressource est `"/testFolder/testResource"`. Pour plus d’informations, voir [Ressources de lecture](aem-forms-repository.md#reading-resources).

1. Mettre à jour la ressource

   Mettez à jour les informations de l’objet `Resource`. Dans cet exemple, pour mettre à jour la description, affectez une nouvelle valeur au champ `description` de l’objet `Resource`.

1. Appelez la méthode `updateResource` de l’objet `RepositoryServiceService` et transmettez les paramètres suivants :

   * Objet `System.String` contenant l’URI de la ressource.
   * Objet `Resource` contenant les informations de ressource mises à jour.
   * Valeur `boolean` indiquant s’il faut mettre à jour la version majeure ou mineure. Dans cet exemple, une valeur `true` est transmise pour indiquer que la version majeure doit être incrémentée.
   * Transmettez `null` pour les deux paramètres restants.

**Voir également**

[Mise à jour des ressources](aem-forms-repository.md#updating-resources)

[Appel d’AEM Forms à l’aide du codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## Recherche de ressources {#searching-for-resources}

Vous pouvez construire des requêtes utilisées pour rechercher des ressources dans le référentiel, y compris l’historique, les ressources associées et les propriétés.

Vous pouvez récupérer les ressources associées pour déterminer les dépendances entre un formulaire et ses fragments. Par exemple, si vous disposez d’un formulaire, vous pouvez déterminer les fragments ou les ressources externes qu’il utilise. Si vous disposez d’une image, vous pouvez également découvrir les formulaires qui l’utilisent. Vous pouvez également rechercher des ressources associées à l’aide du filtrage en fonction des propriétés. Vous pouvez, par exemple, rechercher tous les formulaires qui utilisent une image portant le nom spécifié ou rechercher n’importe quelle image utilisée par un formulaire portant le nom spécifié. Vous pouvez également effectuer des recherches à l’aide des propriétés de ressource. Par exemple, vous pouvez effectuer une requête pour rechercher tous les formulaires ou ressources dont le nom commence par une chaîne donnée pouvant inclure les caractères génériques ’%’ et ’_’. N’oubliez pas que les recherches basées sur les propriétés ne sont pas basées sur des relations ; ces recherches partent du principe que vous connaissez une ressource donnée.

**Instructions de requête**

Une *requête* contient une ou plusieurs instructions qui sont logiquement unies par des conditions. Une *instruction* se compose d’un opérande de gauche, d’un opérateur et d’un opérande de droite. En outre, vous pouvez spécifier l’ordre de tri à utiliser pour les résultats de la recherche. L’ *ordre de tri* contient des informations équivalentes à une clause SQL `ORDER BY` et est constitué d’éléments qui contiennent les attributs sur lesquels la recherche a été basée, ainsi qu’une valeur indiquant si l’ordre croissant ou décroissant doit être utilisé.

Vous pouvez rechercher des ressources par programmation à l’aide de l’API Java du service Repository. Actuellement, il n’est pas possible d’utiliser l’API de service Web pour rechercher des ressources.

**Comportement du tri**

L’ordre de tri n’est pas respecté lors de l’appel de la méthode `searchProperties` de l’objet `ResourceRepositoryClient` et de la spécification d’un ordre de tri. Supposons, par exemple, que vous créiez une ressource avec trois propriétés personnalisées, où les noms d’attribut sont `name`, `secondName` et `asecondName`. Ensuite, vous créez un élément d’ordre de tri sur le nom de l’attribut et définissez la valeur `ascending` sur `true`.

Vous pouvez ensuite appeler la méthode `searchProperties` de l’objet `ResourceRepositoryClient` et la transmettre dans l’ordre de tri. La recherche renvoie la ressource appropriée, avec les trois propriétés . Toutefois, les propriétés ne sont pas triées par nom d’attribut. Ils sont renvoyés dans l’ordre dans lequel ils ont été ajoutés : `name`, `secondName` et `asecondName`.

>[!NOTE]
>
>Pour plus d’informations sur le service Repository, voir [Guide de référence des services pour AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary_of_steps-5}

Pour rechercher des ressources, procédez comme suit :

1. Inclure les fichiers de projet.
1. Créez un client de service Repository.
1. Spécifiez le dossier cible de la recherche.
1. Indiquez les attributs utilisés dans la recherche.
1. Créez la requête utilisée dans la recherche.
1. Créez l’ordre de tri des résultats de la recherche.
1. Recherchez les ressources.
1. Récupérez les ressources du résultat de la recherche.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, incluez les fichiers proxy.

**Création du client de service**

Avant de pouvoir lire une ressource par programmation, vous devez établir une connexion et fournir des informations d’identification. Pour ce faire, créez un client de service.

**Définition du dossier cible de la recherche**

Créez une chaîne contenant le chemin de base à partir duquel effectuer la recherche. La syntaxe comprend des barres obliques, comme dans cet exemple : &quot;/*path*/*folder*&quot;.

**Spécifier les attributs utilisés dans la recherche**

Vous pouvez baser votre recherche sur les attributs contenus dans les ressources. Spécifiez les valeurs des attributs sur lesquels effectuer la recherche.

**Créer la requête utilisée dans la recherche**

Créez une requête à l’aide d’instructions et de conditions. Chaque instruction spécifie l’attribut sur lequel baser la recherche, la condition à utiliser et la valeur d’attribut à utiliser dans la recherche.

**Création de l’ordre de tri des résultats de recherche**

L’ordre de tri est constitué d’éléments dont chacun contient l’un des attributs utilisés dans la recherche et une valeur indiquant si l’ordre croissant ou décroissant doit être utilisé.

**Recherche des ressources**

Recherchez les ressources à l’aide du dossier, de la requête et de l’ordre de tri. Indiquez en outre la profondeur de la recherche et une limite supérieure du nombre de résultats à renvoyer.

**Récupération des ressources du résultat de la recherche**

Parcourez la liste des ressources renvoyée et extrayez les informations en vue d’un traitement ultérieur.

**Voir également**

[Recherche de ressources à l’aide de l’API Java](aem-forms-repository.md#search-for-resources-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Démarrages rapides de l’API Repository Service](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Recherchez des ressources à l’aide de l’API Java {#search-for-resources-using-the-java-api}

Recherchez une ressource à l’aide de l’API Repository service (Java) :

1. Inclure les fichiers de projet

   Incluez les fichiers JAR client dans le chemin de classe de votre projet Java.

1. Création du client de service

   Créez un objet `ResourceRepositoryClient` en utilisant son constructeur et en transmettant un objet `ServiceClientFactory` contenant des propriétés de connexion.

1. Définition du dossier cible de la recherche

   Spécifiez l’URI du chemin de base à partir duquel exécuter la recherche. Dans cet exemple, l’URI de la ressource est `/testFolder`.

1. Spécifier les attributs utilisés dans la recherche

   Spécifiez les valeurs des attributs sur lesquels effectuer la recherche. Les attributs existent dans un objet `com.adobe.repository.infomodel.bean.Resource`. Dans cet exemple, la recherche sera effectuée sur l’attribut name . par conséquent, un `java.lang.String` contenant le nom de l’objet `Resource` est utilisé, qui est `testResource` dans ce cas.

1. Créer la requête utilisée dans la recherche

   Pour créer une requête, créez un objet `com.adobe.repository.query.Query` en appelant le constructeur par défaut pour la classe `Query` et ajoutez des instructions à la requête.

   Pour créer une instruction, appelez le constructeur pour la classe `com.adobe.repository.query.Query.Statement` et transmettez les paramètres suivants :

   * Un opérande de gauche contenant la constante d’attribut de ressource. Dans cet exemple, comme le nom de la ressource est utilisé comme base de la recherche, la valeur statique `Resource.ATTRIBUTE_NAME` est utilisée.
   * Opérateur contenant la condition utilisée dans la recherche de l’attribut. L’opérateur doit être l’une des constantes statiques de la classe `Query.Statement` . Dans cet exemple, la valeur statique `Query.Statement.OPERATOR_BEGINS_WITH` est utilisée.
   * Opérateur de droit contenant la valeur d’attribut sur laquelle effectuer la recherche. Dans cet exemple, l&#39;attribut name, `String` contenant la valeur `"testResource"`, est utilisé.

   Indiquez l’espace de noms de l’opérande de gauche en appelant la méthode `setNamespace` de l’objet `Query.Statement` et en transmettant l’une des valeurs statiques contenues dans la classe `com.adobe.repository.infomodel.bean.ResourceProperty`. Dans cet exemple, `ResourceProperty.RESERVED_NAMESPACE_REPOSITORY` est utilisé.

   Ajoutez chaque instruction à la requête en appelant la méthode `addStatement` de l’objet `Query` et en transmettant l’objet `Query.Statement`.

1. Création de l’ordre de tri des résultats de recherche

   Pour spécifier l’ordre de tri utilisé dans les résultats de recherche, créez un objet `com.adobe.repository.query.sort.SortOrder` en appelant le constructeur par défaut pour la classe `SortOrder` et ajoutez des éléments à l’ordre de tri.

   Pour créer un élément pour l’ordre de tri, appelez l’un des constructeurs de la classe `com.adobe.repository.query.sort.SortOrder.Element`. Dans cet exemple, puisque le nom de la ressource sert de base à la recherche, la valeur statique `Resource.ATTRIBUTE_NAME` est utilisée comme premier paramètre et l’ordre croissant (une valeur `boolean` de `true`) est spécifié comme second paramètre.

   Ajoutez chaque élément à l’ordre de tri en appelant la méthode `addSortElement` de l’objet `SortOrder` et en transmettant l’objet `SortOrder.Element`.

1. Recherche des ressources

   Pour rechercher `resources` en fonction des propriétés d’attribut, appelez la méthode `searchProperties` de l’objet `ResourceRepositoryClient` et transmettez les paramètres suivants :

   * `String` contenant le chemin de base à partir duquel exécuter la recherche. Dans ce cas, `"/testFolder"` est utilisé.
   * Requête utilisée dans la recherche.
   * Profondeur de la recherche. Dans ce cas, `com.adobe.repository.infomodel.bean.ResourceCollection.DEPTH_INFINITE` est utilisé pour indiquer que le chemin de base et tous ses dossiers doivent être utilisés.
   * Une valeur `int` indiquant la première ligne à partir de laquelle sélectionner le jeu de résultats non paginé. Dans cet exemple, `0` est spécifié.
   * Une valeur `int` indiquant le nombre maximal de résultats à renvoyer. Dans cet exemple, `10` est spécifié.
   * Ordre de tri utilisé dans la recherche.

   La méthode renvoie un `java.util.List` d’objets `Resource` dans l’ordre de tri spécifié.

1. Récupération des ressources du résultat de la recherche

   Pour récupérer les ressources contenues dans le résultat de la recherche, effectuez une itération sur la balise `List` et attribuez chaque objet à une balise `Resource` afin d’extraire ses informations. Dans cet exemple, le nom de chaque ressource est affiché.

**Voir également**

[Recherche de ressources](aem-forms-repository.md#searching-for-resources)

[Démarrage rapide (mode SOAP) : Recherche de ressources à l’aide de l’API Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-searching-for-resources-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Création de relations avec les ressources {#creating-resource-relationships}

Vous pouvez spécifier des relations entre les ressources dans le référentiel. Il existe trois types de relations :

* **Dépendance** : une relation dans laquelle une ressource dépend d’autres ressources, ce qui signifie que toutes les ressources associées sont nécessaires dans le référentiel.
* **Adhésion (système de fichiers)** : une relation dans laquelle une ressource se trouve dans un dossier donné.
* **Personnalisé** : une relation que vous spécifiez entre les ressources. Par exemple, si une ressource a été abandonnée et qu’une autre ressource a été introduite dans le référentiel, vous pouvez spécifier votre propre relation de remplacement.

Vous pouvez créer vos propres relations personnalisées. Par exemple, si vous stockez un fichier HTML dans le référentiel et qu’il utilise une image, vous pouvez spécifier une relation personnalisée pour mettre en relation le fichier HTML avec l’image (puisque, normalement, seuls les fichiers XML sont associés aux images à l’aide d’une relation de dépendance définie par le référentiel). Un autre exemple de relation personnalisée serait de créer une vue différente du référentiel avec une structure de graphique cyclique au lieu d’une structure d’arborescence. Vous pouvez définir un graphique circulaire avec une visionneuse pour parcourir ces relations. Enfin, vous pouvez indiquer qu’une ressource remplace une autre ressource même si les deux ressources sont complètement différentes. Dans ce cas, vous pouvez définir un type de relation en dehors de la plage réservée et créer une relation entre ces deux ressources. Votre application serait le seul client à pouvoir détecter et traiter la relation, et elle pourrait être utilisée pour effectuer des recherches sur cette relation.

Vous pouvez définir par programmation les relations entre les ressources à l’aide de l’API Java du service Repository ou de l’API du service Web.

>[!NOTE]
>
>Pour plus d’informations sur le service Repository, voir [Guide de référence des services pour AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary_of_steps-6}

Pour définir une relation entre deux ressources, procédez comme suit :

1. Inclure les fichiers de projet.
1. Créez un client de service Repository.
1. Spécifiez les URI des ressources à relier.
1. Créez la relation.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, incluez les fichiers proxy.

**Création du client de service**

Avant de pouvoir lire une ressource par programmation, vous devez établir une connexion et fournir des informations d’identification. Pour ce faire, créez un client de service.

**Spécifier les URI des ressources à relier**

Créez des chaînes contenant les URI de la ressource à relier. La syntaxe comprend des barres obliques, comme dans cet exemple : &quot;/*path*/*resource*&quot;.

**Création de la relation**

Appelez la méthode de service Repository pour créer et spécifier le type de relation.

**Voir également**

[Création de ressources de relation à l’aide de l’API Java](aem-forms-repository.md#create-relationship-resources-using-the-java-api)

[Création de ressources de relation à l’aide de l’API de service Web](aem-forms-repository.md#create-relationship-resources-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Démarrages rapides de l’API Repository Service](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Créez des ressources de relation à l’aide de l’API Java {#create-relationship-resources-using-the-java-api}

Créez des ressources de relation à l’aide de l’API Java du service Repository, effectuez les tâches suivantes :

1. Inclure les fichiers de projet

   Incluez les fichiers JAR client dans le chemin de classe de votre projet Java.

1. Création du client de service

   Créez un objet `ResourceRepositoryClient` en utilisant son constructeur et en transmettant un objet `ServiceClientFactory` contenant des propriétés de connexion.

1. Spécifier les URI des ressources à relier

   Spécifiez les URI des ressources à relier. Dans ce cas, puisque les ressources sont nommées `testResource1` et `testResource2` et se trouvent dans le dossier `testFolder`, leurs URI sont `"/testFolder/testResource1"` et `"/testFolder/testResource2"`. Les URI sont stockés sous la forme d’objets `java.lang.String`. Dans cet exemple, les ressources sont d’abord écrites dans le référentiel et leurs URI sont récupérés. Pour plus d’informations sur l’écriture d’une ressource, voir [Écriture de ressources](aem-forms-repository.md#writing-resources).

1. Création de la relation

   Appelez la méthode `createRelationship` de l’objet `ResourceRepositoryClient` et transmettez les paramètres suivants :

   * URI de la ressource source.
   * URI de la ressource cible.
   * Type de relation, qui est l’une des constantes statiques de la classe `com.adobe.repository.infomodel.bean.Relation`. Dans cet exemple, une relation de dépendance est établie en spécifiant la valeur `Relation.TYPE_DEPENDANT_OF`.
   * Valeur `boolean` indiquant si la ressource cible est automatiquement mise à jour vers l’identifiant `com.adobe.repository.infomodel.Id` de la nouvelle ressource head. Dans cet exemple, en raison de la relation de dépendance, la valeur `true` est spécifiée.

   Vous pouvez également récupérer une liste des ressources associées pour une ressource donnée en appelant la méthode `getRelated` de l’objet `ResourceRepositoryClient` et en transmettant les paramètres suivants :

   * L’URI de la ressource pour laquelle récupérer les ressources associées. Dans cet exemple, la ressource source ( `"/testFolder/testResource1"`) est spécifiée.
   * Valeur `boolean` indiquant si la ressource spécifiée est la ressource source dans la relation. Dans cet exemple, la valeur `true` est spécifiée car c’est le cas.
   * Le type de relation, qui est l’une des constantes statiques de la classe `Relation`. Dans cet exemple, une relation de dépendance est spécifiée en utilisant la même valeur que celle utilisée précédemment : `Relation.TYPE_DEPENDANT_OF`.

   La méthode `getRelated` renvoie un `java.util.List` d’objets `Resource` par lequel vous pouvez itérer pour récupérer chacune des ressources associées, en projetant les objets contenus dans la balise `List` sur `Resource` au fur et à mesure. Dans cet exemple, `testResource2` doit figurer dans la liste des ressources renvoyées.

**Voir également**

[Création de relations avec les ressources](aem-forms-repository.md#creating-resource-relationships)

[Démarrage rapide (mode SOAP) : Création de relations entre les ressources à l’aide de l’API Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-creating-relationships-between-resources-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Créez des ressources de relation à l’aide de l’API de service Web {#create-relationship-resources-using-the-web-service-api}

Créez des ressources de relation à l’aide de l’API Repository (service Web) :

1. Inclure les fichiers de projet

   * Créez un assemblage client Microsoft .NET qui utilise le fichier WSDL du référentiel.
   * Référencez l’assemblage client Microsoft .NET.

1. Création du client de service

   À l’aide de l’assemblage client Microsoft .NET, créez un objet `RepositoryServiceService` en appelant son constructeur par défaut. Définissez sa propriété `Credentials` à l’aide d’un objet `System.Net.NetworkCredential` contenant le nom d’utilisateur et le mot de passe.

1. Spécifier les URI des ressources à relier

   Spécifiez les URI des ressources à relier. Dans ce cas, puisque les ressources sont nommées `testResource1` et `testResource2` et se trouvent dans le dossier `testFolder`, leurs URI sont `"/testFolder/testResource1"` et `"/testFolder/testResource2"`. Lors de l’utilisation d’un langage conforme à Microsoft .NET Framework (C#, par exemple), les URI sont stockés sous la forme d’objets `System.String`. Dans cet exemple, les ressources sont d’abord écrites dans le référentiel et leurs URI sont récupérés. Pour plus d’informations sur l’écriture d’une ressource, voir [Écriture de ressources](aem-forms-repository.md#writing-resources).

1. Création de la relation

   Appelez la méthode `createRelationship` de l’objet `RepositoryServiceService` et transmettez les paramètres suivants :

   * URI de la ressource source.
   * URI de la ressource cible.
   * Type de relation. Dans cet exemple, une relation de dépendance est établie en spécifiant la valeur `3`.
   * Valeur `boolean` indiquant si le type de relation a été spécifié. Dans cet exemple, la valeur `true` est spécifiée.
   * Valeur `boolean` indiquant si la ressource cible est automatiquement mise à jour vers l’identifiant `Id` de la nouvelle ressource head. Dans cet exemple, en raison de la relation de dépendance, la valeur `true` est spécifiée.
   * Valeur `boolean` indiquant si l’en-tête de la cible a été spécifié. Dans cet exemple, la valeur `true` est spécifiée.
   * Transmettez `null` pour le dernier paramètre.

   Vous pouvez également récupérer une liste des ressources associées pour une ressource donnée en appelant la méthode `getRelated` de l’objet `RepositoryServiceService` et en transmettant les paramètres suivants :

   * L’URI de la ressource pour laquelle récupérer les ressources associées. Dans cet exemple, la ressource source ( `"/testFolder/testResource1"`) est spécifiée.
   * Valeur `boolean` indiquant si la ressource spécifiée est la ressource source dans la relation. Dans cet exemple, la valeur `true` est spécifiée car c’est le cas.
   * Valeur `boolean` indiquant si la ressource source a été spécifiée. Dans cet exemple, la valeur `true` est fournie.
   * Tableau d’entiers contenant les types de relations. Dans cet exemple, une relation de dépendance est spécifiée en utilisant la même valeur dans le tableau que celle utilisée précédemment : `3`.
   * Transmettez `null` pour les deux paramètres restants.

   La méthode `getRelated` renvoie un tableau d’objets qui peuvent être convertis en objets `Resource` par le biais desquels vous pouvez effectuer une itération pour récupérer chacune des ressources associées. Dans cet exemple, `testResource2` doit figurer dans la liste des ressources renvoyées.

**Voir également**

[Création de relations avec les ressources](aem-forms-repository.md#creating-resource-relationships)

[Appel d’AEM Forms à l’aide du codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## Verrouillage de ressources {#locking-resources}

Vous pouvez verrouiller une ressource ou un ensemble de ressources pour une utilisation exclusive par un utilisateur particulier ou une utilisation partagée entre plusieurs utilisateurs. Un verrou partagé est une indication que quelque chose va se produire avec la ressource, mais cela n&#39;empêche personne d&#39;autre de prendre des mesures avec cette ressource. Un verrou partagé doit être considéré comme un mécanisme de signalisation. Un verrou exclusif signifie que l’utilisateur qui a verrouillé la ressource va modifier la ressource, et le verrou garantit que personne d’autre ne peut le faire jusqu’à ce que l’utilisateur n’ait plus besoin d’accéder à la ressource et ait libéré le verrou. Si un administrateur de référentiel déverrouille une ressource, tous les verrous exclusifs et partagés de cette ressource sont automatiquement supprimés. Ce type d’action est destiné aux situations dans lesquelles un utilisateur n’est plus disponible et n’a pas déverrouillé la ressource.

Lorsqu’une ressource est verrouillée, une icône de verrouillage s’affiche lorsque vous affichez l’onglet Ressources situé dans Workbench, comme illustré ci-dessous.

![lr_lr_lockrepository](assets/lr_lr_lockrepository.png)

Vous pouvez contrôler par programmation l’accès aux ressources à l’aide de l’API Java du service Repository ou de l’API du service Web.

>[!NOTE]
>
>Pour plus d’informations sur le service Repository, voir [Guide de référence des services pour AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary_of_steps-7}

Pour verrouiller et déverrouiller des ressources, procédez comme suit :

1. Inclure les fichiers de projet.
1. Créez un client de service Repository.
1. Spécifiez l’URI de la ressource à verrouiller.
1. Verrouillez la ressource.
1. Récupérez les verrous de la ressource.
1. Déverrouiller la ressource

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, incluez les fichiers proxy.

**Création du client de service**

Avant de pouvoir lire une ressource par programmation, vous devez établir une connexion et fournir des informations d’identification. Pour ce faire, créez un client de service.

**Spécifiez l’URI de la ressource à verrouiller.**

Créez une chaîne contenant l’URI de la ressource à verrouiller. La syntaxe comprend des barres obliques, comme dans cet exemple : &quot;/*path*/*resource*&quot;.

**Verrouillage de la ressource**

Appelez la méthode du service Repository pour verrouiller la ressource, en spécifiant l’URI, le type de verrouillage et la profondeur de verrouillage.

**Récupération des verrous pour la ressource**

Appelez la méthode du service Repository pour récupérer les verrous de la ressource, en spécifiant l’URI.

**Déverrouiller la ressource**

Appelez la méthode de service Repository pour déverrouiller la ressource, en spécifiant l’URI.

**Voir également**

[Verrouillage de ressources à l’aide de l’API Java](aem-forms-repository.md#lock-resources-using-the-java-api)

[Verrouillage de ressources à l’aide de l’API de service Web](aem-forms-repository.md#lock-resources-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Démarrages rapides de l’API Repository Service](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Verrouillage de ressources à l’aide de l’API Java {#lock-resources-using-the-java-api}

Verrouillez des ressources à l’aide de l’API Repository service (Java) :

1. Inclure les fichiers de projet

   Incluez les fichiers JAR client dans le chemin de classe de votre projet Java.

1. Création du client de service

   Créez un objet `ResourceRepositoryClient` en utilisant son constructeur et en transmettant un objet `ServiceClientFactory` contenant des propriétés de connexion.

1. Spécifiez l’URI de la ressource à verrouiller.

   Spécifiez l’URI de la ressource à verrouiller. Dans ce cas, puisque la ressource nommée `testResource` se trouve dans le dossier nommé `testFolder`, son URI est `"/testFolder/testResource"`. L’URI est stocké en tant qu’objet `java.lang.String`.

1. Verrouillage de la ressource

   Appelez la méthode `lockResource` de l’objet `ResourceRepositoryClient` et transmettez les paramètres suivants :

   * URI de la ressource.
   * Portée du verrou. Dans cet exemple, puisque la ressource sera verrouillée pour une utilisation exclusive, le périmètre de verrouillage est spécifié sous la forme `com.adobe.repository.infomodel.bean.Lock.SCOPE_EXCLUSIVE`.
   * Profondeur de verrouillage. Dans cet exemple, comme le verrouillage s’applique uniquement à la ressource particulière et qu’aucun de ses membres ou enfants n’y est associé, la profondeur de verrouillage est spécifiée sous la forme `Lock.DEPTH_ZERO`.

   >[!NOTE]
   >
   >La version surchargée de la méthode `lockResource` qui nécessite quatre paramètres renvoie une exception. Veillez à utiliser la méthode `lockResource` qui nécessite trois paramètres, comme indiqué dans cette présentation.

1. Récupération des verrous pour la ressource

   Appelez la méthode `getLocks` de l’objet `ResourceRepositoryClient` et transmettez l’URI de la ressource en tant que paramètre. La méthode renvoie une liste d’objets Lock à travers lesquels vous pouvez effectuer une itération. Dans cet exemple, le propriétaire, la profondeur et la portée du verrouillage sont imprimés pour chaque objet en appelant respectivement les méthodes `getOwnerUserId`, `getDepth` et `getType` de chaque objet de verrouillage.

1. Déverrouiller la ressource

   Appelez la méthode `unlockResource` de l’objet `ResourceRepositoryClient` et transmettez l’URI de la ressource en tant que paramètre. Pour plus d’informations, voir [Référence de l’API AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Voir également**

[Verrouillage de ressources](aem-forms-repository.md#locking-resources)

[Démarrage rapide (mode SOAP) : Verrouillage d’une ressource à l’aide de l’API Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-locking-a-resource-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Verrouillage de ressources à l’aide de l’API de service Web {#lock-resources-using-the-web-service-api}

Verrouillez des ressources à l’aide de l’API Repository service (service Web) :

1. Inclure les fichiers de projet

   * Créez un assemblage client Microsoft .NET qui utilise le fichier WSDL du référentiel à l’aide de Base64.
   * Référencez l’assemblage client Microsoft .NET.

1. Création du client de service

   À l’aide de l’assemblage client Microsoft .NET, créez un objet `RepositoryServiceService` en appelant son constructeur par défaut. Définissez sa propriété `Credentials` à l’aide d’un objet `System.Net.NetworkCredential` contenant le nom d’utilisateur et le mot de passe.

1. Spécifiez l’URI de la ressource à verrouiller.

   Spécifiez une chaîne contenant l’URI de la ressource à verrouiller. Dans ce cas, puisque la ressource nommée `testResource` se trouve dans le dossier `testFolder`, son URI est `"/testFolder/testResource"`. Lorsque vous utilisez un langage conforme à Microsoft .NET Framework (C#, par exemple), stockez l’URI dans un objet `System.String` .

1. Verrouillage de la ressource

   Appelez la méthode `lockResource` de l’objet `RepositoryServiceService` et transmettez les paramètres suivants :

   * URI de la ressource.
   * Portée du verrou. Dans cet exemple, puisque la ressource sera verrouillée pour une utilisation exclusive, le périmètre de verrouillage est spécifié sous la forme `11`.
   * Profondeur de verrouillage. Dans cet exemple, comme le verrouillage s’applique uniquement à la ressource particulière et qu’aucun de ses membres ou enfants n’y est associé, la profondeur de verrouillage est spécifiée sous la forme `2`.
   * Valeur `int` indiquant le nombre de secondes jusqu’à l’expiration du verrou. Dans cet exemple, la valeur de `1000` est utilisée.
   * Transmettez `null` pour le dernier paramètre.

1. Récupération des verrous pour la ressource

   Appelez la méthode `getLocks` de l’objet `RepositoryServiceService` et transmettez l’URI de la ressource comme premier paramètre et `null` comme second paramètre. La méthode renvoie un tableau `object` contenant des objets `Lock` par lesquels vous pouvez effectuer une itération. Dans cet exemple, le propriétaire, la profondeur et la portée du verrouillage sont imprimés pour chaque objet en accédant respectivement aux champs `ownerUserId`, `depth` et `type` de chaque objet.`Lock`

1. Déverrouiller la ressource

   Appelez la méthode `unlockResource` de l’objet `RepositoryServiceService` et transmettez l’URI de la ressource comme premier paramètre et `null` comme second paramètre.

**Voir également**

[Verrouillage de ressources](aem-forms-repository.md#locking-resources)

[Appel d’AEM Forms à l’aide du codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## Suppression de ressources {#deleting-resources}

Vous pouvez supprimer des ressources par programmation d’un emplacement donné dans le référentiel à l’aide de l’API Java du service de référentiel (SOAP).

Lorsque vous supprimez une ressource, la suppression est normalement permanente, bien que, dans certains cas, les référentiels ECM puissent stocker les versions de la ressource en fonction de leurs mécanismes d’historique. Par conséquent, lors de la suppression d’une ressource, il est important de s’assurer que vous n’aurez plus besoin de cette ressource. La suppression d&#39;une ressource est généralement motivée par la nécessité d&#39;augmenter l&#39;espace disponible dans la base de données. Vous pouvez supprimer une version d’une ressource, mais si vous le faites, vous devez spécifier l’identifiant de la ressource, et non son identifiant logique (LID) ou son chemin d’accès. Si vous supprimez un dossier, tous ses éléments, y compris les sous-dossiers et les ressources, seront automatiquement supprimés.

Les ressources connexes ne sont pas supprimées. Par exemple, si un formulaire utilise le fichier logo.gif et que vous supprimez logo.gif, une relation est stockée dans le tableau de relation en attente. Autre possibilité : pour l’obsolescence de la version, définissez l’état de l’objet de la dernière version sur obsolète.

Une opération de suppression n’est pas compatible avec les transactions dans les systèmes ECM. Par exemple, si vous tentez de supprimer 100 ressources et que l’opération échoue sur la 50e ressource, les 49 premières instances seront supprimées, mais le reste ne le sera pas. Sinon, le comportement par défaut est la restauration (non-engagement).

>[!NOTE]
>
>Lors de l’utilisation de la méthode `com.adobe.repository.bindings.dsc.client.ResourceRepositoryClient.deleteResources()` avec le référentiel ECM (EMC Documentum Content Server et IBM FileNet P8 Content Manager), la transaction ne sera pas annulée si la suppression échoue pour l’une des ressources spécifiées, ce qui signifie que les fichiers qui ont été supprimés ne peuvent pas être supprimés.

>[!NOTE]
>
>Pour plus d’informations sur le service Repository, voir [Guide de référence des services pour AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary_of_steps-8}

Pour supprimer une ressource, procédez comme suit :

1. Inclure les fichiers de projet.
1. Créez un client de service Repository.
1. Indiquez l’URI de la ressource à supprimer.
1. Supprimez la ressource.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, incluez les fichiers proxy.

**Création du client de service**

Avant de pouvoir lire une ressource par programmation, vous devez établir une connexion et fournir des informations d’identification. Pour ce faire, créez un client de service.

**Spécifier l’URI de la ressource à supprimer**

Créez une chaîne contenant l’URI de la ressource à supprimer. La syntaxe comprend des barres obliques, comme dans cet exemple : &quot;/*path*/*resource*&quot;. Si la ressource à supprimer est un dossier, la suppression sera récursive.

**Supprimer la ressource**

Appelez la méthode du service Repository pour supprimer la ressource, en spécifiant l’URI.

**Voir également**

[Suppression de ressources à l’aide de l’API Java](aem-forms-repository.md#delete-resources-using-the-java-api-soap)

[Suppression de ressources à l’aide de l’API de service Web](aem-forms-repository.md#delete-resources-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Démarrages rapides de l’API Repository Service](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Supprimer des ressources à l’aide de l’API Java (SOAP) {#delete-resources-using-the-java-api-soap}

Supprimez une ressource à l’aide de l’API Repository (Java) :

1. Inclure les fichiers de projet

   Incluez les fichiers JAR client dans le chemin de classe de votre projet Java.

1. Création du client de service

   Créez un objet `ResourceRepositoryClient` en utilisant son constructeur et en transmettant un objet `ServiceClientFactory` contenant des propriétés de connexion.

1. Spécifier l’URI de la ressource à supprimer

   Spécifiez l’URI de la ressource à récupérer. Dans ce cas, puisque la ressource nommée testResourceToBeDeleted se trouve dans le dossier nommé testFolder, son URI est `/testFolder/testResourceToBeDeleted`. L’URI est stocké en tant qu’objet `java.lang.String`. Dans cet exemple, la ressource est d’abord écrite dans le référentiel et son URI est récupéré. Pour plus d’informations sur l’écriture d’une ressource, voir [Écriture de ressources](aem-forms-repository.md#writing-resources).

1. Supprimer la ressource

   Appelez la méthode `deleteResource` de l’objet `ResourceRepositoryClient` et transmettez l’URI de la ressource en tant que paramètre.

**Voir également**

[Suppression de ressources](aem-forms-repository.md#deleting-resources)

[Démarrage rapide (mode SOAP) : Recherche de ressources à l’aide de l’API Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-searching-for-resources-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Supprimer des ressources à l’aide de l’API de service Web {#delete-resources-using-the-web-service-api}

Supprimez une ressource à l’aide de l’API Repository (service Web) :

1. Inclure les fichiers de projet

   * Créez un assemblage client Microsoft .NET qui utilise le fichier WSDL du référentiel à l’aide de Base64.
   * Référencez l’assemblage client Microsoft .NET.

1. Création du client de service

   À l’aide de l’assemblage client Microsoft .NET, créez un objet `RepositoryServiceService` en appelant son constructeur par défaut. Définissez sa propriété `Credentials` à l’aide d’un objet `System.Net.NetworkCredential` contenant le nom d’utilisateur et le mot de passe.

1. Spécifier l’URI de la ressource à supprimer

   Spécifiez l’URI de la ressource à récupérer. Dans ce cas, puisque la ressource nommée `testResourceToBeDeleted` se trouve dans le dossier nommé `testFolder`, son URI est `"/testFolder/testResourceToBeDeleted"`. Dans cet exemple, la ressource est d’abord écrite dans le référentiel et son URI est récupéré. Pour plus d’informations sur l’écriture d’une ressource, voir [Écriture de ressources](aem-forms-repository.md#writing-resources).

1. Supprimer la ressource

   Appelez la méthode `deleteResources` de l’objet `RepositoryServiceService` et transmettez un tableau `System.String` contenant l’URI de la ressource comme premier paramètre. Transmettez `null` pour le deuxième paramètre.

**Voir également**

[Suppression de ressources](aem-forms-repository.md#deleting-resources)

[Appel d’AEM Forms à l’aide du codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
