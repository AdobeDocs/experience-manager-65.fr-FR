---
title: Utilisation du référentiel AEM Forms
description: Gérez le référentiel AEM Forms pour créer des dossiers, écrire, répertorier, lire, mettre à jour et rechercher des ressources à l’aide de l’API Java et de l’API Web Service. En outre, découvrez comment créer des relations de ressources, verrouiller et supprimer des ressources.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: a07e51ca-fea0-4719-8071-1b7e805de2ae
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,APIs & Integrations
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: ht
source-wordcount: '9036'
ht-degree: 100%

---

# Utilisation du référentiel AEM Forms {#working-with-aem-forms-repository}

**Les exemples et les échantillons de ce document sont réservés à l’environnement AEM Forms sur JEE.**

**À propos du service Repository**

Le service Repository fournit du stockage de ressources et des services de gestion à AEM Forms. Lorsque des développeurs créent une application *AEM Forms*, ils peuvent déployer les ressources dans le référentiel plutôt que dans le système de fichiers. Les actifs peuvent être constitués de formulaires XML, de formulaires PDF (y compris de formulaires Acrobat), de fragments de formulaire, d’images, de profils, de politiques, de fichiers SWF, DDX et WSDL, de schémas XML et de données de test.

Prenons l’exemple de l’application Forms suivante nommée *Applications/FormsApplication* :

![www_www_formrepository](assets/ww_ww_formrepository.png)

Notez qu’un fichier nommé Loan.xdp se trouve dans le dossier Forms. Pour accéder à cette conception de formulaire, vous devez spécifier le chemin d’accès complet (y compris la version) : `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.

>[!NOTE]
>
>Pour plus d’informations sur la création d’une application Forms à l’aide de Workbench, voir [Aide de Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63_fr).

Le chemin d’accès à une ressource dans le référentiel AEM Forms est :

`Applications/Application-name/Application-version/Folder.../Filename`

Les valeurs suivantes présentent quelques exemples de valeurs URI :

* Applications/AppraisalReport/1.0/Forms/FullForm.xdp
* Applications/AnotherApp/1.1/Assets/picture.jpg
* Applications/SomeApp/2.0/Resources/Data/XSDs/MyData.xsd

>[!NOTE]
>
>Vous pouvez parcourir le référentiel AEM Forms à l’aide d’un navigateur web. Pour parcourir le référentiel, saisissez l’URL suivante dans un navigateur web `https://[server name]:[server port]/repository`. Vous pouvez vérifier les résultats de démarrage rapide associés à la section Utilisation du référentiel AEM Forms à l’aide d’un navigateur web. Par exemple, si vous ajoutez du contenu au référentiel AEM Forms, vous pouvez afficher le contenu dans un navigateur web. (Voir [Démarrage rapide (mode SOAP) : écrire une ressource en utilisant l’API Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-writing-a-resource-using-the-java-api).)

L’API Repository fournit un certain nombre d’opérations que vous pouvez utiliser pour stocker et récupérer des informations du référentiel. Par exemple, vous pouvez obtenir une liste des ressources ou récupérer des ressources spécifiques stockées dans le référentiel lorsqu’une ressource est nécessaire dans le cadre du traitement d’une application.

>[!NOTE]
>
>L’API Repository ne peut pas être utilisée pour interagir avec Content Services (obsolète). Pour interagir avec Content Services (obsolète), utilisez l’API Document Management.

À l’aide de l’API Repository Service, vous pouvez accomplir les tâches suivantes :

* Création de dossiers. Voir [Création de dossiers](aem-forms-repository.md#creating-folders).
* Écrivez des ressources et leurs propriétés. Voir [Écriture de ressources](aem-forms-repository.md#writing-resources).
* Répertoriez les ressources d’une collection donnée ou associées à d’autres ressources. Voir [Liste des ressources](aem-forms-repository.md#listing-resources).
* Lisez les ressources et leurs propriétés. Voir [Lire les ressources](aem-forms-repository.md#reading-resources).
* Mettez à jour les ressources et leurs propriétés. Voir [Mise à jour des ressources](aem-forms-repository.md#updating-resources).
* Recherchez des ressources, y compris leur historique, les ressources associées et les propriétés. Voir [Recherche de ressources](aem-forms-repository.md#searching-for-resources).
* Spécifiez les relations entre les ressources. Voir [Création de relations entre les ressources](aem-forms-repository.md#creating-resource-relationships).
* Gérez le contrôle d’accès aux ressources, notamment le verrouillage et le déverrouillage des ressources, ainsi que la lecture et l’écriture des listes de contrôle d’accès (ACL). Voir [Verrouillage de ressources](aem-forms-repository.md#locking-resources).
* Supprimez les ressources et leurs propriétés. Voir [Suppression de ressources](aem-forms-repository.md#deleting-resources).

>[!NOTE]
>
>Avec l’API Repository, vous ne pouvez pas gérer le contrôle d’accès aux ressources, rechercher des ressources ou définir des relations de ressources à l’aide d’un référentiel ECM.

>[!NOTE]
>
>Lorsqu’un PDF chiffré est écrit dans le référentiel, la fonction d’extraction de relation automatisée ne peut pas être utilisée. Dans le cas contraire, un PDF chiffré peut être stocké dans le référentiel et récupéré ultérieurement. Le récupérateur peut choisir de déchiffrer le PDF une fois qu’il a été récupéré dans le référentiel.

>[!NOTE]
>
>Pour plus d’informations sur le service Repository, voir [Références des services pour AEM Forms](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

## Création de dossiers {#creating-folders}

Les dossiers (collections de ressources) sont utilisés pour stocker des objets (fichiers ou ressources) dans des regroupements organisés. Les dossiers peuvent contenir des ressources et d’autres dossiers, également appelés sous-dossiers. Les ressources ne peuvent être stockées que dans un seul dossier à la fois.

Les fichiers héritent des listes de contrôle d’accès (ACL) des dossiers et les sous-dossiers héritent des ACL de leurs dossiers parents. Par conséquent, les dossiers parents doivent exister avant de pouvoir créer des dossiers enfants. L’IDE permet d’interagir uniquement dossier par dossier, et non fichier par fichier. Vous ne pouvez pas modifier les dossiers et il n’est pas nécessaire de le faire : un dossier ne contient pas de données lui-même. Il s’agit plutôt uniquement d’un conteneur pour les ressources qui contiennent des données. La liste de contrôle d’accès par défaut est une autorisation de niveau système, ce qui signifie que les utilisateurs doivent disposer d’autorisations de niveau système (lecture, écriture, traversée, gestion des listes de contrôle d’accès) jusqu’à ce qu’une personne leur donne des autorisations pour un dossier particulier. Les listes de contrôle d’accès ne fonctionnent que dans l’IDE.

>[!NOTE]
>
>Pour plus d’informations sur le service Repository, voir [Références des services pour AEM Forms](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

### Résumé des étapes {#summary-of-steps}

Pour créer un dossier, procédez comme suit :

1. Incluez les fichiers de projet.
1. Créez le client de service.
1. Créez le dossier.
1. Rédigez le dossier dans le référentiel.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services web, incluez les fichiers proxy.

**Créer le client de service**

Avant de pouvoir créer par programmation une collection de ressources, vous devez établir une connexion et fournir des informations d’identification. Pour ce faire, créez un client de service.

**Créer le dossier**

Appelez la méthode du service Repository pour créer la collection de ressources et renseigner les informations d’identification dans la collection de ressources, y compris son UUID, son nom de dossier et sa description.

**Écrire le dossier dans le référentiel**

Appelez la méthode du service Repository pour écrire la collection de ressources, en spécifiant l’URI du dossier cible.

**Voir également**

[Créer des dossiers à l’aide de l’API Java](aem-forms-repository.md#create-folders-using-the-java-api)

[Créer des dossiers à l’aide de l’API Web Service](aem-forms-repository.md#create-folders-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Démarrages rapides de l’API Repository Service](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Créer des dossiers à l’aide de l’API Java {#create-folders-using-the-java-api}

Créez un dossier à l’aide de l’API Repository Service (Java) :

1. Inclure les fichiers du projet

   Incluez des fichiers de projet dans le chemin de classe du projet Java.

1. Création du client de service

   Créez un objet `ResourceRepositoryClient` en utilisant son constructeur et en transmettant un objet `ServiceClientFactory` contenant des propriétés de connexion.

1. Création du dossier

   Pour créer une collection de ressources, vous devez d’abord créer un objet `com.adobe.repository.infomodel.bean.RepositoryInfomodelFactoryBean`.

   Appelez la méthode `newResourceCollection` de l’objet `repositoryInfomodelFactoryBean` et transmettez les paramètres suivants :

   * Identifiant UUID `com.adobe.repository.infomodel.Id` à affecter à la ressource.
   * Identifiant UUID `com.adobe.repository.infomodel.Lid` à affecter à la ressource.
   * Un `java.lang.String` contenant le nom de la collection de ressources. Par exemple, `FormsFolder`.

   La méthode renvoie un objet `com.adobe.repository.infomodel.bean.ResourceCollection` représentant le nouveau dossier.

   Définissez la description du dossier à l’aide de la méthode `setDescription` et transmettez le paramètre suivant :

   * Un `String` qui décrit la collection de ressources. Dans cet exemple, `"test Folder"` est utilisé `.`.

1. Écriture du dossier dans le référentiel

   Appelez la méthode `writeResource` de l’objet `ResourceRepositoryClient` et transmettez l’URI du dossier et l’objet `ResourceCollection`. Par exemple, l’URI du dossier peut être la valeur suivante : `/Applications/FormsApplication/1.0/`.

   La méthode renvoie une instance du nouvel objet `com.adobe.repository.infomodel.bean.Resource` créé. Par exemple, vous pouvez récupérer la valeur d’identifiant de la nouvelle ressource en appelant la méthode `getId` de l’objet `com.adobe.repository.infomodel.bean.Resource`.

**Voir également**

[Création de dossiers](aem-forms-repository.md#creating-folders)

[Démarrage rapide (mode SOAP) : créer un dossier à l’aide de l’API Java.](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-creating-a-folder-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Créer des dossiers à l’aide de l’API Web Service {#create-folders-using-the-web-service-api}

Créez un dossier à l’aide de l’API Repository Service (Web Service) :

1. Inclure les fichiers du projet

   * Créez un assemblage client Microsoft .NET qui utilise le fichier WSDL du référentiel à l’aide de base64.
   * Référencez l’assemblage client Microsoft .NET.

1. Création du client de service

   À l’aide de l’assemblage client .NET Microsoft, créez un objet `RepositoryServiceService` en appelant son constructeur par défaut. Définissez sa propriété `Credentials` à l’aide d’un objet `System.Net.NetworkCredential` contenant le nom d’utilisateur et le mot de passe.

1. Création du dossier

   Créez le dossier à l’aide du constructeur par défaut pour la classe `ResourceCollection` et transmettez les paramètres suivants :

   * Objet `Id`, créé en appelant le constructeur par défaut pour la classe `Id` et affecté au champ `id` de l’objet `Resource`.
   * Objet `Lid`, créé en appelant le constructeur par défaut pour la classe `Lid` et affecté au champ `lid` de l’objet `Resource`.
   * Chaîne contenant le nom de la collection de ressources et attribuée au champ `name` de l’objet `Resource`. Le nom utilisé dans cet exemple est `"testfolder"`.
   * Chaîne contenant la description de la collection de ressources et attribuée au champe `description` de l’objet `Resource`. La description utilisée dans cet exemple est `"test folder"`.

1. Écriture du dossier dans le référentiel

   Appelez la méthode `writeResource` de l’objet `RepositoryServiceService` et transmettez les paramètres suivants :

   * Chemin d’accès à l’emplacement où le dossier doit être créé.
   * Objet `ResourceCollection` représentant le dossier.
   * Transmettez `null` pour les deux autres paramètres.

**Voir également**

[Création de dossiers](aem-forms-repository.md#creating-folders)

[Appeler AEM Forms en utilisant le codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## Écriture de ressources {#writing-resources}

Vous pouvez créer des ressources à un emplacement donné dans le référentiel. La taille de fichier naturelle est soumise aux restrictions de la base de données et au délai d’expiration de la session. Pour la configuration par défaut, les fichiers sont limités à 25 Mo. Pour augmenter ou réduire la taille maximale du fichier, vous devez modifier la configuration de la base de données.

L’écriture de ressources équivaut à stocker des données dans le référentiel. Une fois que vous avez écrit une ressource dans le référentiel, elle devient accessible à tous les clients de l’écosystème de référentiel. Lorsque vous écrivez des ressources, telles que des schémas XML, des fichiers XDP et des fichiers XSD, dans le référentiel, le contenu est analysé en fonction du type MIME. Si le type MIME est pris en charge, l’analyseur détermine s’il existe une relation implicite avec d’autres contenus. Par exemple, si une feuille de style en cascade (CSS) comporte une URL relative qui fait référence à une page CSS commune, il est prévu que vous envoyiez également la page CSS commune dans le référentiel. La relation entre les deux ressources est stockée en tant que relation en attente pendant une période non ajustable de 30 jours. Lorsque vous envoyez la page CSS commune au référentiel au cours de la période de 30 jours, la relation est formée.

Lorsque vous créez une ressource, la liste de contrôle d’accès (ACL) est héritée du dossier parent. Le dossier racine dispose d’autorisations au niveau du système jusqu’à la création d’une ressource ou d’un dossier initial, auquel cas les autorisations ACL par défaut sont accordées à la ressource ou au dossier.

Vous pouvez écrire des ressources par programmation à l’aide de l’API Java ou Web Service Repository Service.

>[!NOTE]
>
>Pour plus d’informations sur le service Repository, voir [Références des services pour AEM Forms](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

### Résumé des étapes {#summary_of_steps-1}

Pour écrire une ressource, procédez comme suit :

1. Incluez les fichiers de projet.
1. Créez un client de service Repository.
1. Spécifiez l’URI de la ressource à lire.
1. Lisez la ressource.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services web, incluez les fichiers proxy.

**Création du client du service**

Avant de pouvoir lire une ressource par programmation, vous devez établir une connexion et fournir des informations d’identification. Pour ce faire, créez un client de service.

**Spécifier l’URI du dossier cible pour la ressource**

Créez une chaîne contenant l’URI de la ressource à lire. La syntaxe comprend des barres obliques, comme dans cet exemple : « /*chemin*/*dossier* ».

**Créer la ressource**

Appelez la méthode du service Repository pour créer la ressource et renseignez la ressource avec des informations d’identification, y compris son UUID, son nom et sa description.

**Définir le contenu de la ressource**

Appelez la méthode du service Repository pour créer le contenu de la ressource et stocker ce contenu dans la ressource.

**Écrire la ressource dans le dossier cible**

Appelez la méthode du service Repository pour écrire la ressource, en spécifiant l’URI du dossier cible.

**Voir également**

[Écrire des ressources à l’aide de l’API Java](aem-forms-repository.md#write-resources-using-the-java-api)

[Écrire des ressources à l’aide de l’API Web Service](aem-forms-repository.md#write-resources-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Démarrages rapides de l’API Repository Service](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Écrire des ressources à l’aide de l’API Java {#write-resources-using-the-java-api}

Écrivez une ressource à l’aide de l’API Repository Service (Java) :

1. Inclure les fichiers du projet

   Incluez les fichiers JAR client dans le chemin de classe de votre projet Java.

1. Création du client de service

   Créez un objet `ResourceRepositoryClient` en utilisant son constructeur et en transmettant un objet `ServiceClientFactory` contenant des propriétés de connexion.

1. Spécifiez l’URI du dossier cible pour la ressource.

   Spécifiez l’URI du dossier cible pour la ressource. Dans ce cas, comme la ressource appelée `testResource` est stockée dans le dossier nommé `testFolder`, l’URI du dossier est `"/testFolder"`. L’URI est stocké en tant qu’objet `java.lang.String`.

1. Création de la ressource

   Pour créer une ressource, vous devez d’abord créer un objet `com.adobe.repository.infomodel.bean.RepositoryInfomodelFactoryBean`.

   Appelez la méthode `newResource` de l’objet `RepositoryInfomodelFactoryBean`, qui crée un objet `com.adobe.repository.infomodel.bean.Resource`. Dans cet exemple, les paramètres suivants sont fournis :

   * Objet `com.adobe.repository.infomodel.Id`, créé en appelant le constructeur par défaut pour la classe `Id`.
   * Objet `com.adobe.repository.infomodel.Lid`, créé en appelant le constructeur par défaut pour la classe `Lid`.
   * `java.lang.String` contenant le nom de fichier de la ressource.

   Pour spécifier la description de la ressource, appelez la méthode `setDescription` de l’objet `Resource` et transmettez une chaîne contenant la description. Dans cet exemple, la description est `"test resource"`.

1. Définition du contenu de la ressource

   Pour créer du contenu pour la ressource, appelez la méthode `newResourceContent` de l’objet `RepositoryInfomodelFactoryBean`, qui renvoie un objet `com.adobe.repository.infomodel.bean.ResourceContent`. Ajoutez du contenu à l’objet `ResourceContent`. Pour ce faire, dans cet exemple, les tâches suivantes doivent être réalisées :

   * Appel de la méthode `setDataDocument` de l’objet `ResourceContent` et transmission de l’objet `com.adobe.idp.Document`
   * Appel de la méthode `setSize` de l’objet `ResourceContent` et transmission de la taille en octets de l’objet `Document`

   Ajoutez le contenu à la ressource en appelant la méthode `setContent` de l’objet `Resource` et en transmettant l’objet `ResourceContent`. Pour plus d’informations, voir [Référence de l’API pour AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. Enregistrer la ressource dans le dossier cible

   Appelez la méthode `writeResource` de lʼobjet `ResourceRepositoryClient` et transmettez lʼURI du dossier, ainsi que lʼobjet `Resource`.

**Voir également**

[Écriture de ressources](aem-forms-repository.md#writing-resources)

[Démarrage rapide (mode SOAP) : écrire une ressource en utilisant l’API Java.](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-writing-a-resource-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Écrire des ressources à l’aide de l’API Web Service {#write-resources-using-the-web-service-api}

Écrivez une ressource à l’aide de l’API Repository Service (Web Service) :

1. Inclure les fichiers du projet

   * Créez un assemblage client Microsoft .NET qui utilise le fichier WSDL du référentiel à l’aide de base64.
   * Référencez l’assemblage client Microsoft .NET.

1. Création du client de service

   À l’aide de l’assemblage client Microsoft .NET, créez un objet `RepositoryServiceService` en appelant son constructeur par défaut. Définissez sa propriété `Credentials` à l’aide de l’objet `System.Net.NetworkCredential` contenant le nom d’utilisateur et le mot de passe.

1. Spécifiez l’URI du dossier cible pour la ressource.

   Spécifiez l’URI du dossier cible pour la ressource. Dans ce cas, comme la ressource appelée `testResource` est stockée dans le dossier nommé `testFolder`, l’URI du dossier est `"/testFolder"`. Si vous utilisez un langage compatible avec Microsoft .NET Framework (par exemple, C#), stockez lʼURI dans un objet `System.String`.

1. Création de la ressource

   Pour créer une ressource, appelez le constructeur par défaut de la classe `Resource`. Dans cet exemple, les informations suivantes sont stockées dans lʼobjet `Resource` :

   * Un objet `com.adobe.repository.infomodel.Id`, qui est créé en appelant le constructeur par défaut de la classe `Id` et affecté au champ `id` de lʼobjet `Resource`.
   * Un objet `com.adobe.repository.infomodel.Lid`, qui est créé en appelant le constructeur par défaut de la classe `Lid` et affecté au champ `lid` de lʼobjet `Resource`.
   * Une chaîne contenant le nom de fichier de la ressource, qui est attribuée au champ `name` de lʼobjet `Resource`. Le nom utilisé dans cet exemple est `"testResource"`.
   * Une chaîne contenant la description de la ressource, qui est affectée au champ `description` de lʼobjet `Resource`. La description utilisée dans cet exemple est `"test resource"`.

1. Définition du contenu de la ressource

   Pour créer le contenu de la ressource, appelez le constructeur par défaut de la classe `ResourceContent`. Ajoutez ensuite du contenu à lʼobjet `ResourceContent`. Pour ce faire, dans cet exemple, les tâches suivantes doivent être réalisées :

   * Affectation dʼun objet `BLOB` contenant un document au champ `dataDocument` de lʼobjet `ResourceContent`.
   * Affectation de la taille en octets de lʼobjet `BLOB` au champ `size` de lʼobjet `ResourceContent`.

   Ajoutez le contenu à la ressource en affectant lʼobjet `ResourceContent` au champ `content` de lʼobjet `Resource`.

1. Enregistrer la ressource dans le dossier cible

   Appelez la méthode `writeResource` de l’objet `RepositoryServiceService` et transmettez l’URI du dossier, et l’objet `Resource`. Transmettez `null` pour les deux autres paramètres.

**Voir également**

[Écriture de ressources](aem-forms-repository.md#writing-resources)

[Appeler AEM Forms en utilisant le codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## Liste des ressources {#listing-resources}

Vous pouvez découvrir des ressources en les répertoriant. Une requête est exécutée sur le référentiel pour rechercher toutes les ressources associées à une collection de ressources donnée.

Une fois vos ressources organisées, vous pouvez inspecter la structure que vous avez créée en visualisant une branche particulière de la structure, comme vous le feriez dans un système d’exploitation.

La liste des ressources fonctionne par relation : les ressources sont membres de dossiers. L’appartenance est représentée par une relation de type « membre de ». Lorsque vous répertoriez les ressources dʼun dossier donné, vous recherchez les ressources qui sont associées à un dossier donné par la relation « membre de ». Les relations sont directionnelles : un membre d’une relation possède une source qui est un membre de la cible. La source est la ressource ; la cible est le dossier parent.

>[!NOTE]
>
>Pour plus d’informations sur le service Repository, consultez la section [Références des services pour AEM Forms](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

### Résumé des étapes {#summary_of_steps-2}

Pour répertorier les ressources, procédez comme suit :

1. Incluez les fichiers de projet.
1. Créez le client de service.
1. Indiquez le chemin dʼaccès au dossier.
1. Récupérez la liste des ressources.

**Inclusion des fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services web, incluez les fichiers proxy.

**Créer le client de service**

Avant de pouvoir créer par programmation une collection de ressources, vous devez établir une connexion et fournir des informations d’identification. Pour ce faire, créez un client de service.

**Spécification du chemin dʼaccès au dossier**

Créez une chaîne contenant le chemin dʼaccès au dossier comportant les ressources. La syntaxe comprend des barres obliques, comme dans l’exemple suivant : « /*chemin*/*dossier* ».

**Récupération de la liste des ressources**

Appelez la méthode du service Repository pour récupérer la liste des ressources, en spécifiant le chemin du dossier cible.

**Voir également**

[Liste des ressources à l’aide de l’API Java](aem-forms-repository.md#list-resources-using-the-java-api)

[Liste des ressources à l’aide de l’API de service Web](aem-forms-repository.md#list-resources-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Démarrages rapides de l’API Repository Service](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Liste des ressources à l’aide de l’API Java {#list-resources-using-the-java-api}

Répertoriez les ressources à l’aide de l’API du service Repository (Java) :

1. Inclure les fichiers du projet

   Incluez les fichiers JAR client dans le chemin de classe de votre projet Java.

1. Création du client de service

   Créez un objet `ResourceRepositoryClient` à l’aide de son constructeur et en transmettant un objet `ServiceClientFactory` contenant des propriétés de connexion.

1. Définition du chemin du dossier

   Spécifiez l’URI de la collection de ressources à interroger. Dans ce cas, son URI est `"/testFolder"`. L’URI est stocké en tant qu’objet `java.lang.String`.

1. Récupération de la liste des ressources

   Appelez la méthode `listMembers` de l’objet `ResourceRepositoryClient` et transmettez l’URI du dossier.

   La méthode renvoie un `java.util.List` des objets `com.adobe.repository.infomodel.bean.Resource` qui constituent la source d’un `com.adobe.repository.infomodel.bean.Relation` de type `Relation.TYPE_MEMBER_OF` et qui ont l’URI de collecte de ressources comme cible. Vous pouvez effectuer une itération sur cette `List` pour récupérer chacune des ressources. Dans cet exemple, le nom et la description de chaque ressource s’affichent.

**Voir également**

[Inscription de ressources](aem-forms-repository.md#listing-resources).

[Démarrage rapide (mode SOAP) : inscription de ressources à l’aide de l’API Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-listing-resources-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Liste des ressources à l’aide de l’API de service Web {#list-resources-using-the-web-service-api}

Inscription de ressources à l’aide de l’API du service Repository (service Web) :

1. Inclure les fichiers du projet

   * Créez un assemblage client Microsoft .NET qui utilise le fichier WSDL du référentiel.
   * Référencez l’assemblage client Microsoft .NET.

1. Création du client de service

   À l’aide de l’assemblage client Microsoft .NET, créez un objet `RepositoryServiceService` en appelant son constructeur par défaut. Définissez sa propriété `Credentials` à l’aide d’un objet `System.Net.NetworkCredential` contenant le nom d’utilisateur et le mot de passe.

1. Définition du chemin du dossier

   Spécifiez une chaîne contenant l’URI du dossier à interroger. Dans ce cas, son URI est `"/testFolder"`. Lorsque vous utilisez un langage conforme au framework Microsoft .NET (C#, par exemple), stockez l’URI dans un objet `System.String`.

1. Récupération de la liste des ressources

   Appelez la méthode `listMembers` de l’objet `RepositoryServiceService` et transmettez l’URI du dossier en tant que premier paramètre. Transmettez `null` pour les deux autres paramètres.

   La méthode renvoie un tableau d’objets qui peuvent être convertis en objets `Resource`. Vous pouvez effectuer une itération sur le tableau d’objets pour récupérer chacune des ressources associées. Dans cet exemple, le nom et la description de chaque ressource s’affichent.

**Voir également**

[Inscription des ressources](aem-forms-repository.md#listing-resources).

[Appeler AEM Forms en utilisant le codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## Lecture des ressources {#reading-resources}

Vous pouvez récupérer des ressources à partir d’un emplacement donné dans le référentiel afin de lire leur contenu et leurs métadonnées. Le workflow est dirigé par un formulaire d’initialisation. Le processus a toutes les permissions nécessaires pour lire le formulaire. Le système récupère le formulaire de données et lit le contenu du référentiel. Le référentiel donne accès au contenu et aux métadonnées (la possibilité de savoir que la ressource existe).

Le référentiel dispose des quatre types d’autorisations suivants :

* **parcours** : permet de répertorier les ressources, c’est-à-dire de lire les métadonnées de la ressource, mais pas leur contenu.
* **lecture** : permet de lire le contenu d’une ressource.
* **écriture** : permet d’écrire du contenu de ressource.
* **gestion des listes de contrôle d’accès (ACL)** : permet de manipuler les ACL sur les ressources.

Les utilisateurs ne peuvent exécuter des processus que si lʼautorisation leur en a été accordée. Les utilisateurs d’un IDE doivent disposer d’autorisations de parcours et de lecture pour se synchroniser avec le référentiel. Les listes de contrôle d’accès ne s’appliquent quʼau moment de la conception, car l’exécution se produit dans le contexte du système.

Vous pouvez lire les ressources par programmation à l’aide de l’API Java du service Repository ou de l’API de service web.

>[!NOTE]
>
>Pour plus d’informations sur le service Repository, consultez la section [Référence des services pour AEM Forms](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

### Résumé des étapes {#summary_of_steps-3}

Pour lire une ressource, procédez comme suit :

1. Incluez les fichiers de projet.
1. Créez un client de service Repository.
1. Spécifiez l’URI de la ressource à lire.
1. Lisez la ressource.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services web, incluez les fichiers proxy.

**Création du client du service**

Avant de pouvoir lire une ressource par programmation, vous devez établir une connexion et fournir des informations d’identification. Pour ce faire, créez un client de service.

**Spécifier l’URI de la ressource à lire**

Créez une chaîne contenant l’URI de la ressource à lire. La syntaxe comprend des barres obliques, comme dans cet exemple : « /*path*/*resource* ».

**Lire la ressource**

Appelez la méthode du service Repository pour lire la ressource, en spécifiant l’URI.

**Voir également**

[Lire les ressources à l’aide de l’API Java](aem-forms-repository.md#read-resources-using-the-java-api)

[Lire les ressources à l’aide de l’API de service web](aem-forms-repository.md#reading-resources-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Démarrages rapides de l’API Repository Service](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Lire les ressources à l’aide de l’API Java {#read-resources-using-the-java-api}

Lire une ressource à l’aide de l’API du service Repository (Java) :

1. Inclure les fichiers du projet

   Incluez les fichiers JAR client dans le chemin de classe de votre projet Java.

1. Création du client de service

   Créez un objet `ResourceRepositoryClient` en utilisant son constructeur et en transmettant un objet `ServiceClientFactory` qui contient les propriétés de connexion.

1. Spécifier l’URI de la ressource à lire

   Spécifiez une valeur de chaîne qui représente l’URI de la ressource à récupérer. Par exemple, si la ressource s’appelle *testResource* et se trouve dans un dossier nommé *testFolder*, spécifiez `/testFolder/testResource`.

1. Lire la ressource

   Appelez la méthode `readResource` de l’objet `ResourceRepositoryClient` et transmettez l’URI de la ressource comme paramètre. Cette méthode renvoie une instance `Resource` qui représente la ressource.

**Voir également**

[Lecture des ressources](aem-forms-repository.md#reading-resources)

[Démarrage rapide (mode SOAP) : lire une ressource à lʼaide de l’API Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-reading-a-resource-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Lire les ressources à l’aide de l’API de service web {#reading-resources-using-the-web-service-api}

Lire une ressource à l’aide de l’API du service Repository (service web) :

1. Inclure les fichiers du projet

   * Créez un assemblage client Microsoft .NET qui utilise le fichier WSDL du référentiel. (Consultez la section [Créer un assemblage client .NET qui utilise le codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)).
   * Référencez l’assemblage client Microsoft .NET. (Consultez la section [Créer un assemblage client .NET qui utilise le codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)).

1. Création du client de service

   À l’aide de l’assemblage client Microsoft .NET, créez un objet `RepositoryServiceService` en appelant son constructeur par défaut. Définissez sa propriété `Credentials` en utilisant un objet `System.Net.NetworkCredential` contenant le nom d’utilisateur et le mot de passe.

1. Spécifier l’URI de la ressource à lire

   Spécifiez une chaîne contenant l’URI de la ressource à récupérer. Dans ce cas, comme la ressource nommée `testResource` se trouve dans le dossier au nom de `testFolder`, son URI est `"/testFolder/testResource"`. Si vous utilisez un langage compatible avec Microsoft .NET Framework (par exemple, C#), stockez l’URI dans un objet `System.String`.

1. Lire la ressource

   Appelez la méthode `readResource` de l’objet `RepositoryServiceService` et transmettez l’URI de la ressource comme premier paramètre. Transmettez `null` pour les deux autres paramètres.

**Voir également**

[Lecture des ressources](aem-forms-repository.md#reading-resources)

[Appeler AEM Forms en utilisant le codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## Mise à jour des ressources {#updating-resources}

Vous pouvez récupérer et mettre à jour le contenu des ressources dans le référentiel. Lorsque vous mettez à jour des ressources, le contrôle d’accès à ces ressources reste inchangé entre les versions. Lorsque vous effectuez une mise à jour, vous avez la possibilité d’incrémenter la version majeure. Si vous ne choisissez pas d’incrémenter la version majeure, la version mineure est automatiquement mise à jour.

Lorsque vous mettez à jour une ressource, la nouvelle version est créée en fonction des attributs de ressource spécifiés. Lorsque vous mettez à jour une ressource, vous spécifiez deux paramètres importants : l’URI cible et une instance de ressource contenant toutes les métadonnées mises à jour. Il est important de noter que même si vous ne modifiez pas un attribut donné (par exemple, le nom), cet attribut reste obligatoire dans lʼinstance que vous transmettez. Les relations créées lors de l’analyse du contenu sont ajoutées à la version spécifique et ne sont pas transférées, sauf indication contraire.

Par exemple, si vous mettez à jour un fichier XDP qui contient des références à d’autres ressources, ces références supplémentaires seront également enregistrées. Supposons que la version 1.0 de form.xdp possède deux références externes : un logo et une feuille de style. Vous mettez à jour le fichier form.xdp, de sorte quʼil possède maintenant trois références : un logo, une feuille de style et un fichier de schéma. Lors de la mise à jour, le référentiel ajoute la troisième relation (au fichier de schéma) à sa table de relations en attente. Une fois que le fichier de schéma est présent dans le référentiel, la relation est automatiquement formée. Cependant, si la version 2.0 de form.xdp n’utilise plus le logo, la version 2.0 de form.xdp nʼaura pas de relation avec le logo.

Toutes les opérations de mise à jour sont de nature atomique et transactionnelle. Par exemple, si deux utilisateurs lisent la même ressource et décident tous deux de mettre à jour la version 1.0 vers la version 2.0, lʼun dʼeux réussira et lʼautre échouera, lʼintégrité du référentiel sera maintenue et les deux utilisateurs recevront un message confirmant le succès ou lʼéchec. Si la transaction n’est pas validée, elle sera restaurée en cas de défaillance de la base de données et expirera ou sera restaurée en fonction du serveur d’applications.

Vous pouvez mettre à jour les ressources par programmation à l’aide de l’API Java du service Repository ou de l’API de service web.

>[!NOTE]
>
>Pour plus d’informations sur le service Repository, consultez la section [Références des services pour AEM Forms](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

### Résumé des étapes {#summary_of_steps-4}

Pour mettre à jour une ressource, procédez comme suit :

1. Incluez les fichiers de projet.
1. Créez un client de service Repository.
1. Récupérez la ressource à mettre à jour.
1. Mettez à jour la ressource.

**Inclusion des fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services web, incluez les fichiers proxy.

**Création du client du service**

Avant de pouvoir lire une ressource par programmation, vous devez établir une connexion et fournir des informations d’identification. Pour ce faire, créez un client de service.

**Récupération de la ressource à mettre à jour**

Lisez la ressource. Pour plus d’informations, consultez la section [Lecture des ressources](aem-forms-repository.md#reading-resources).

**Mise à jour de la ressource**

Définissez les nouvelles informations dans la ressource et appelez la méthode du service Repository pour mettre à jour la ressource : spécifiez l’URI, la ressource mise à jour et la manière dont les informations de version doivent être mises à jour.

**Voir également**

[Mise à jour des ressources à l’aide de l’API Java](aem-forms-repository.md#update-resources-using-the-java-api)

[Mise à jour des ressources à l’aide de l’API de service web](aem-forms-repository.md#update-resources-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Démarrages rapides de l’API Repository Service](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Mise à jour des ressources à l’aide de l’API Java {#update-resources-using-the-java-api}

Pour mettre à jour une ressource à l’aide de l’API du service Repository (Java), procédez comme suit :

1. Inclure les fichiers du projet

   Incluez les fichiers JAR client dans le chemin de classe de votre projet Java.

1. Création du client de service

   Créez un objet `ResourceRepositoryClient` en utilisant son constructeur et en transmettant un objet `ServiceClientFactory` qui contient les propriétés de connexion.

1. Récupérer la ressource à mettre à jour

   Spécifier lʼURI de la ressource pour récupérer et lire la ressource. Dans cet exemple, l’URI de la ressource est `"/testFolder/testResource"`.

1. Mettre à jour la ressource

   Mettez à jour les informations de lʼobjet `Resource`. Pour mettre à jour la description dans cet exemple, appelez la méthode `setDescription` de lʼobjet `Resource` et transmettez la nouvelle chaîne de description comme paramètre.

   Appelez ensuite la méthode `updateResource` de lʼobjet `ServiceClientFactory` et transmettez les paramètres suivants :

   * Un objet `java.lang.String` contenant l’URI de la ressource.
   * Lʼobjet `Resource` contenant les informations de la ressource mise à jour.
   * Une valeur `boolean` indiquant s’il faut mettre à jour la version majeure ou mineure. Dans cet exemple, une valeur de `true` est transmise pour indiquer que la version majeure doit être incrémentée.

**Voir également**

[Mise à jour des ressources](aem-forms-repository.md#updating-resources)

[Didacticiel de mise en route (mode SOAP) : mise à jour d’une ressource en utilisant l’API Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-updating-a-resource-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Mise à jour des ressources à l’aide de l’API de service web {#update-resources-using-the-web-service-api}

Pour mettre à jour une ressource en utilisant l’API Repository (service web), procédez comme suit :

1. Inclure les fichiers du projet

   * Créez un assemblage client Microsoft .NET qui utilise le fichier WSDL du référentiel.
   * Référencez l’assemblage client Microsoft .NET.

1. Création du client de service

   À l’aide de l’assemblage client Microsoft .NET, créez un objet `RepositoryServiceService` en appelant son constructeur par défaut. Définissez sa propriété `Credentials` à l’aide d’un objet `System.Net.NetworkCredential` contenant le nom d’utilisateur et le mot de passe.

1. Récupérer la ressource à mettre à jour

   Indiquez l’URI de la ressource à récupérer et lisez la ressource. Dans cet exemple, l’URI de la ressource est `"/testFolder/testResource"`. Pour plus d’informations, voir [Lire les ressources](aem-forms-repository.md#reading-resources).

1. Mettre à jour la ressource

   Mettez à jour les informations de l’objet `Resource`. Pour mettre à jour la description dans cet exemple, saisissez une nouvelle valeur dans le champ `description` de lʼobjet `Resource`.

1. Appelez la méthode `updateResource` de lʼobjet `RepositoryServiceService` et transmettez les paramètres suivants :

   * Un objet `System.String` contenant l’URI de la ressource.
   * Lʼobjet `Resource` contenant les informations de la ressource mise à jour.
   * Une valeur `boolean` indiquant s’il faut mettre à jour la version majeure ou mineure. Dans cet exemple, une valeur de `true` est transmise pour indiquer que la version majeure doit être incrémentée.
   * Transmettez `null` pour les deux paramètres restants.

**Voir également**

[Mise à jour des ressources](aem-forms-repository.md#updating-resources)

[Appeler AEM Forms en utilisant le codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## Recherche de ressources {#searching-for-resources}

Vous pouvez construire des requêtes utilisées pour rechercher des ressources dans le référentiel, y compris l’historique, les ressources associées et les propriétés.

Vous pouvez récupérer les ressources associées pour déterminer les dépendances entre un formulaire et ses fragments. Par exemple, si vous disposez d’un formulaire, vous pouvez déterminer les fragments ou les ressources externes qu’il utilise. Si vous disposez d’une image, vous pouvez également découvrir les formulaires qui l’utilisent. Vous pouvez également rechercher des ressources associées à l’aide du filtrage basé sur les propriétés. Par exemple, vous pouvez rechercher tous les formulaires qui utilisent une image avec un nom spécifié, ou trouver toute image utilisée par un formulaire avec un nom spécifié. Vous pouvez également effectuer une recherche à l’aide des propriétés des ressources. Par exemple, vous pouvez effectuer une requête pour trouver tous les formulaires ou ressources dont le nom commence par une chaîne de caractères donnée qui peut inclure les caractères génériques « % » et « _ ». Gardez à lʼesprit que les recherches basées sur les propriétés ne sont pas basées sur les relations : ces recherches partent du principe que vous avez des connaissances spécifiques sur une ressource donnée.

**Instructions de requête**

Une *requête* contient une ou plusieurs instructions associées à des conditions de façon logique. Une *instruction* est constituée d’un opérande gauche, d’un opérateur et d’un opérande droit. De plus, vous pouvez spécifier l’ordre de tri à utiliser pour les résultats de la recherche. Lʼ&#x200B;*ordre de tri* contient des informations équivalentes à une clause SQL `ORDER BY` et est composé dʼéléments qui contiennent les attributs sur lesquels la recherche a été basée, ainsi quʼune valeur indiquant si lʼordre ascendant ou descendant doit être utilisé.

Vous pouvez rechercher des ressources par programmation à l’aide de l’API Java du service Repository. Actuellement, il n’est pas possible d’utiliser l’API de service web pour rechercher des ressources.

**Comportement de tri**

L’ordre de tri n’est pas respecté lors de l’appel de la méthode `searchProperties` de lʼobjet `ResourceRepositoryClient` et de la spécification dʼun ordre de tri. Prenons lʼexemple suivant : vous créez une ressource avec trois propriétés personnalisées, dont les noms d’attribut sont `name`, `secondName` et `asecondName`. Ensuite, vous créez un élément d’ordre de tri sur le nom de l’attribut et définissez la valeur `ascending` sur `true`.

Ensuite, vous appelez la méthode `searchProperties` de lʼobjet `ResourceRepositoryClient` et transmettez l’ordre de tri. La recherche renvoie la bonne ressource, avec les trois propriétés. Toutefois, les propriétés ne sont pas triées par nom d’attribut. Elles sont retournées dans l’ordre dans lequel elles ont été ajoutées : `name`, `secondName` et `asecondName`.

>[!NOTE]
>
>Pour plus d’informations sur le service Repository, consultez la section [Références des services pour AEM Forms](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

### Résumé des étapes {#summary_of_steps-5}

Pour rechercher des ressources, procédez comme suit :

1. Incluez les fichiers de projet.
1. Créez un client de service Repository.
1. Spécifiez le dossier cible de la recherche.
1. Indiquez les attributs utilisés dans la recherche.
1. Créez la requête utilisée dans la recherche.
1. Créez lʼordre de tri des résultats de la recherche.
1. Recherchez les ressources.
1. Récupérez les ressources dans les résultats de la recherche.

**Inclusion des fichiers du projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services web, incluez les fichiers proxy.

**Création du client du service**

Avant de pouvoir lire une ressource par programmation, vous devez établir une connexion et fournir des informations d’identification. Pour ce faire, créez un client de service.

**Définition du dossier cible de la recherche**

Créez une chaîne contenant le chemin d’accès de base à partir duquel effectuer la recherche. La syntaxe comprend des barres obliques, comme dans cet exemple : « /*chemin*/*dossier* ».

**Spécifier les attributs utilisés dans la recherche**

Vous pouvez baser la recherche sur les attributs contenus dans les ressources. Spécifiez les valeurs des attributs sur lesquels effectuer la recherche.

**Créer la requête utilisée dans la recherche**

Créez une requête à l’aide d’instructions et de conditions. Chaque instruction spécifie l’attribut sur lequel baser la recherche, la condition à utiliser et la valeur d’attribut à utiliser dans la recherche.

**Créer l’ordre de tri des résultats de recherche**

L’ordre de tri est constitué d’éléments dont chacun contient l’un des attributs utilisés dans la recherche et une valeur indiquant si l’ordre croissant ou décroissant doit être utilisé.

**Rechercher des ressources**

Recherchez les ressources à l’aide du dossier, de la requête et de l’ordre de tri. Indiquez en outre la profondeur de la recherche et une limite supérieure du nombre de résultats à renvoyer.

**Récupérer des ressources à partir du résultat de la recherche**

Parcourez la liste des ressources renvoyée et extrayez les informations en vue d’un traitement ultérieur.

**Voir également**

[Recherche de ressources à l’aide de l’API Java](aem-forms-repository.md#search-for-resources-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Démarrages rapides de l’API Repository Service](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Recherche de ressources à l’aide de l’API Java {#search-for-resources-using-the-java-api}

Recherchez une ressource à l’aide de l’API Repository Service (Java) :

1. Inclure les fichiers du projet

   Incluez les fichiers JAR client dans le chemin de classe de votre projet Java.

1. Création du client de service

   Créez un objet `ResourceRepositoryClient` en utilisant son constructeur et en transmettant un objet `ServiceClientFactory` contenant des propriétés de connexion.

1. Définition du dossier cible de la recherche

   Spécifiez l’URI du chemin d’accès de base à partir duquel exécuter la recherche. Dans cet exemple, l’URI de la ressource est `/testFolder`.

1. Spécification des attributs utilisés dans la recherche

   Spécifiez les valeurs des attributs sur lesquels effectuer la recherche. Les attributs existent dans un objet `com.adobe.repository.infomodel.bean.Resource`. Dans cet exemple, la recherche sera effectuée sur l’attribut name. Par conséquent, un `java.lang.String` contenant le nom de l’objet `Resource` est utilisé, lequel est `testResource` dans ce cas.

1. Création de la requête utilisée dans la recherche

   Pour créer une requête, créez un objet `com.adobe.repository.query.Query` en appelant le constructeur par défaut pour la classe `Query` et ajoutez des instructions à la requête.

   Pour créer une instruction, appelez le constructeur pour la classe `com.adobe.repository.query.Query.Statement` et transmettez les paramètres suivants :

   * Un opérande gauche contenant la constante de l’attribut de ressource. Dans cet exemple, comme le nom de la ressource sert de base à la recherche, la valeur statique `Resource.ATTRIBUTE_NAME` est utilisée.
   * Un opérateur contenant la condition utilisée dans la recherche de l’attribut. L’opérateur doit être l’une des constantes statiques de la classe `Query.Statement`. Dans cet exemple, la valeur statique `Query.Statement.OPERATOR_BEGINS_WITH` est utilisée.
   * Un opérande droit contenant la valeur de l’attribut sur lequel effectuer la recherche. Dans cet exemple, l’attribut « name », une `String` contenant la valeur `"testResource"`, est utilisé.

   Indiquez l’espace de nommage de l’opérande gauche en appelant la méthode `setNamespace` de l’objet `Query.Statement` et en transmettant l’une des valeurs statiques contenues dans la classe `com.adobe.repository.infomodel.bean.ResourceProperty`. Dans cet exemple, la valeur `ResourceProperty.RESERVED_NAMESPACE_REPOSITORY` est utilisée.

   Ajoutez chaque instruction à la requête en appelant la méthode `addStatement` de l’objet `Query` et en transmettant l’objet `Query.Statement`.

1. Créer lʼordre de tri des résultats de la recherche

   Pour spécifier l’ordre de tri utilisé dans les résultats de la recherche, créez un objet `com.adobe.repository.query.sort.SortOrder` en appelant le constructeur par défaut de la classe `SortOrder` et ajoutez des éléments à l’ordre de tri.

   Pour créer un élément pour l’ordre de tri, appelez l’un des constructeurs de la classe `com.adobe.repository.query.sort.SortOrder.Element`. Dans cet exemple, comme le nom de la ressource sert de base à la recherche, la valeur statique `Resource.ATTRIBUTE_NAME` est utilisée comme premier paramètre et lʼordre croissant (une valeur `boolean` de `true`) est spécifié comme deuxième paramètre.

   Ajoutez chaque élément à lʼordre de tri en appelant la méthode `addSortElement` de l’objet `SortOrder` et en transmettant l’objet `SortOrder.Element`.

1. Rechercher les ressources

   Pour rechercher des `resources` en fonction des propriétés des attributs, appelez la méthode `searchProperties` de l’objet `ResourceRepositoryClient` et transmettez les paramètres suivants :

   * Une valeur `String` contenant le chemin d’accès de base à partir duquel exécuter la recherche. Dans ce cas, la valeur `"/testFolder"` est utilisée.
   * La requête utilisée dans la recherche.
   * La précision de la recherche. Dans ce cas, `com.adobe.repository.infomodel.bean.ResourceCollection.DEPTH_INFINITE` est utilisé pour indiquer que le chemin d’accès de base et tous ses dossiers doivent être utilisés.
   * Une valeur `int` indiquant la première ligne à partir de laquelle sélectionner le jeu de résultats non paginés. Dans cet exemple, `0` est spécifié.
   * Une valeur `int` indiquant le nombre maximal de résultats à renvoyer. Dans cet exemple, `10` est spécifié.
   * Lʼordre de tri utilisé dans la recherche.

   La méthode renvoie une liste `java.util.List` d’objets `Resource` dans lʼordre de tri spécifié.

1. Récupérer les ressources à partir des résultats de recherche

   Pour récupérer les ressources contenues dans les résultats de recherche, il faut itérer au sein de `List` et convertir chaque objet en `Resource` afin d’extraire ses informations. Dans cet exemple, le nom de chaque ressource est affiché.

**Voir également**

[Recherche de ressources](aem-forms-repository.md#searching-for-resources)

[Démarrage rapide (mode SOAP) : rechercher des ressources à l’aide de l’API Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-searching-for-resources-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Créer des relations entre les ressources {#creating-resource-relationships}

Vous pouvez spécifier des relations entre les ressources dans le référentiel. Il existe trois types de relations :

* **Dépendance** : relation dans laquelle une ressource dépend d’autres ressources, ce qui signifie que toutes les ressources liées sont nécessaires dans le référentiel.
* **Appartenance (système de fichiers)** : relation dans laquelle une ressource est située dans un dossier donné.
* **Personnalisé** : relation que vous spécifiez entre les ressources. Par exemple, si une ressource est devenue obsolète et qu’une autre ressource a été introduite dans le référentiel, vous pouvez spécifier votre propre relation de remplacement.

Vous pouvez créer vos propres relations personnalisées. Par exemple, si vous stockez un fichier HTML dans le référentiel et qu’il utilise une image, vous pouvez spécifier une relation personnalisée pour relier le fichier HTML avec l’image (puisque normalement seuls les fichiers XML sont associés aux images à l’aide d’une relation de dépendance définie par le référentiel). Un autre exemple de relation personnalisée est celui où vous souhaitez créer une vue différente du référentiel avec une structure de graphique cyclique au lieu d’une structure dʼarborescence. Vous pourriez définir un graphique circulaire ainsi quʼune visionneuse pour parcourir ces relations. Enfin, vous pouvez indiquer qu’une ressource remplace une autre ressource, même si les deux ressources sont complètement différentes. Dans ce cas, vous pouvez définir un type de relation en dehors de la plage réservée et créer une relation entre ces deux ressources. Votre application serait le seul client capable de détecter et de traiter la relation, et elle pourrait être utilisée pour effectuer des recherches sur cette relation.

Vous pouvez spécifier par programmation les relations entre les ressources à lʼaide de l’API Java ou de service web du service Repository.

>[!NOTE]
>
>Pour plus d’informations sur le service Repository, voir [Références des services pour AEM Forms](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

### Résumé des étapes {#summary_of_steps-6}

Pour définir une relation entre deux ressources, procédez comme suit :

1. Incluez les fichiers de projet.
1. Créez un client de service Repository.
1. Spécifiez les URI des ressources à relier.
1. Créez la relation.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services web, incluez les fichiers proxy.

**Création du client du service**

Avant de pouvoir lire une ressource par programmation, vous devez établir une connexion et fournir des informations d’identification. Pour ce faire, créez un client de service.

**Spécifier les URI des ressources à relier**

Créez des chaînes contenant les URI de la ressource à relier. La syntaxe comprend des barres obliques, comme dans cet exemple : « /*chemin*/*ressource* ».

**Créer la relation**

Appelez la méthode de service Repository pour créer et spécifier le type de relation.

**Voir également**

[Créer des ressources de relation à l’aide de l’API Java](aem-forms-repository.md#create-relationship-resources-using-the-java-api)

[Créer des ressources de relation à l’aide de l’API Web Service](aem-forms-repository.md#create-relationship-resources-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Démarrages rapides de l’API Repository Service](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Créer des ressources de relation à l’aide de l’API Java {#create-relationship-resources-using-the-java-api}

Créez des ressources de relation à l’aide de l’API Java Repository Service et effectuez les tâches suivantes :

1. Inclure les fichiers du projet

   Incluez les fichiers JAR client dans le chemin de classe de votre projet Java.

1. Création du client de service

   Créez un objet `ResourceRepositoryClient` en utilisant son constructeur et en transmettant un objet `ServiceClientFactory` contenant des propriétés de connexion.

1. Spécification des URI des ressources à relier

   Spécifiez les URI des ressources à relier. Dans ce cas, comme les ressources sont nommées `testResource1` et `testResource2` et se trouvent dans le dossier nommé `testFolder`, leurs URI sont `"/testFolder/testResource1"` et `"/testFolder/testResource2"`. Les URI sont stockés en tant qu’objets `java.lang.String`. Dans cet exemple, les ressources sont d’abord écrites dans le référentiel et leurs URI sont récupérés. Pour plus d’informations sur l’écriture d’une ressource, voir [Écriture de ressources](aem-forms-repository.md#writing-resources).

1. Création de la relation

   Appelez la méthode `createRelationship` de l’objet `ResourceRepositoryClient` et transmettez les paramètres suivants :

   * URI de la ressource source.
   * URI de la ressource cible.
   * Le type de relation, qui est l’une des constantes statiques dans la classe `com.adobe.repository.infomodel.bean.Relation`. Dans cet exemple, une relation de dépendance est établie en spécifiant la valeur `Relation.TYPE_DEPENDANT_OF`.
   * Valeur `boolean` indiquant si la ressource cible est automatiquement mise à jour vers l’identifiant basé sur `com.adobe.repository.infomodel.Id` de la nouvelle ressource HEAD. Dans cet exemple, en raison de la relation de dépendance, la valeur `true` est spécifiée.

   Vous pouvez également récupérer une liste des ressources associées pour une ressource donnée en appelant la méthode `getRelated` de l’objet `ResourceRepositoryClient` et en transmettant les paramètres suivants :

   * L’URI de la ressource pour laquelle récupérer les ressources associées. Dans cet exemple, la ressource source (`"/testFolder/testResource1"`) est spécifiée.
   * Valeur `boolean` indiquant si la ressource spécifiée est la ressource source dans la relation. Dans cet exemple, la valeur `true` est spécifiée, car c’est le cas.
   * Le type de relation, qui est l’une des constantes statiques dans la classe `Relation`. Dans cet exemple, une relation de dépendance est spécifiée en utilisant la même valeur que celle utilisée précédemment : `Relation.TYPE_DEPENDANT_OF`.

   La méthode `getRelated` renvoie un `java.util.List` des objets de `Resource` à travers lesquels vous pouvez effectuer une itération pour récupérer chacune des ressources associées, en projetant les objets contenus dans le `List` vers `Resource` comme vous le faites. Dans cet exemple, `testResource2` doit se trouver dans la liste des ressources renvoyées.

**Voir également**

[Créer des relations entre les ressources](aem-forms-repository.md#creating-resource-relationships)

[Démarrage rapide (mode SOAP) : créer des relations entre les ressources à l’aide de l’API Java.](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-creating-relationships-between-resources-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Créer des ressources de relation à l’aide de l’API Web Service {#create-relationship-resources-using-the-web-service-api}

Créez des ressources de relation à l’aide de l’API Repository (Web Service) :

1. Inclure les fichiers du projet

   * Créez un assemblage client Microsoft .NET qui utilise le fichier WSDL du référentiel.
   * Référencez l’assemblage client Microsoft .NET.

1. Création du client de service

   À l’aide de l’assemblage client Microsoft .NET, créez un objet `RepositoryServiceService` en appelant son constructeur par défaut. Définissez sa propriété `Credentials` à l’aide de l’objet `System.Net.NetworkCredential` contenant le nom d’utilisateur et le mot de passe.

1. Spécification des URI des ressources à relier

   Spécifiez les URI des ressources à relier. Dans ce cas, étant donné que les ressources sont nommées `testResource1` et `testResource2` et se trouvent dans le dossier nommé `testFolder`, leurs URI sont `"/testFolder/testResource1"` et `"/testFolder/testResource2"`. Lors de l’utilisation d’un langage conforme à Microsoft .NET Framework (C#, par exemple), les URI sont stockés sous la forme d’un objet `System.String`. Dans cet exemple, les ressources sont d’abord écrites dans le référentiel et leurs URI sont récupérés. Pour plus d’informations sur l’écriture d’une ressource, voir [Écriture de ressources](aem-forms-repository.md#writing-resources).

1. Création de la relation

   Appelez la méthode `createRelationship` de l’objet `RepositoryServiceService` et transmettez les paramètres suivants :

   * URI de la ressource source.
   * URI de la ressource cible.
   * Le type de relation. Dans cet exemple, une relation de dépendance est établie en spécifiant la valeur `3`.
   * Valeur `boolean` indiquant si le type de relation a été spécifié. Dans cet exemple, la valeur `true` est spécifiée.
   * Valeur `boolean` indiquant si la ressource cible est automatiquement mise à jour vers l’identificateur basé sur `Id` de la nouvelle ressource HEAD. Dans cet exemple, en raison de la relation de dépendance, la valeur `true` est spécifiée.
   * Valeur `boolean` indiquant si la cible HEAD a été spécifiée. Dans cet exemple, la valeur `true` est spécifiée.
   * Transmettez `null` pour le dernier paramètre.

   Vous pouvez également récupérer une liste des ressources associées pour une ressource donnée en appelant la méthode `getRelated` de l’objet `RepositoryServiceService` et en transmettant les paramètres suivants :

   * L’URI de la ressource pour laquelle récupérer les ressources associées. Dans cet exemple, la ressource source (`"/testFolder/testResource1"`) est spécifiée.
   * Valeur `boolean` indiquant si la ressource spécifiée est la ressource source dans la relation. Dans cet exemple, la valeur `true` est spécifiée parce que c’est le cas.
   * Valeur `boolean` indiquant si la ressource source a été spécifiée. Dans cet exemple, la valeur `true` est fournie.
   * Tableau d’entiers contenant les types de relations. Dans cet exemple, une relation de dépendance est spécifiée en utilisant la même valeur dans le tableau que celle utilisée précédemment : `3`.
   * Transmettez `null` pour les deux paramètres restants.

   La méthode `getRelated` renvoie un tableau d’objets qui peuvent être convertis en objets `Resource` par l’intermédiaire desquels vous pouvez effectuer une itération pour récupérer chacune des ressources associées. Dans cet exemple, `testResource2` doit se trouver dans la liste des ressources renvoyées.

**Voir également**

[Créer des relations entre les ressources](aem-forms-repository.md#creating-resource-relationships)

[Appeler AEM Forms en utilisant le codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## Verrouiller les ressources {#locking-resources}

Vous pouvez verrouiller une ressource ou un ensemble de ressources pour une utilisation exclusive par un utilisateur particulier ou une utilisation partagée entre plusieurs utilisateurs. Un verrou partagé est une indication que quelque chose va se produire avec la ressource, mais cela n’empêche personne d’autre de prendre des mesures avec cette ressource. Un verrou partagé doit être considéré comme un mécanisme de signalisation. Un verrou exclusif signifie que l’utilisateur qui a verrouillé la ressource va la modifier. Le verrou garantit que personne d’autre ne peut le faire jusqu’à ce que l’utilisateur n’ait plus besoin d’accéder à la ressource et ait libéré le verrou. Si un administrateur de référentiel déverrouille une ressource, tous les verrous exclusifs et partagés de cette ressource sont automatiquement supprimés. Ce type d’action est destiné aux situations dans lesquelles un utilisateur n’est plus disponible et n’a pas déverrouillé la ressource.

Lorsqu’une ressource est verrouillée, une icône de verrou s’affiche lorsque vous affichez l’onglet Ressources situé dans Workbench, comme illustré ci-dessous.

![lr_lr_lockrepository](assets/lr_lr_lockrepository.png)

Vous pouvez contrôler l’accès aux ressources par programmation à l’aide de l’API Java Repository Service ou de l’API Web Service.

>[!NOTE]
>
>Pour plus d’informations sur le service Forms, voir [Références des services pour AEM Forms](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

### Résumé des étapes {#summary_of_steps-7}

Pour verrouiller et déverrouiller des ressources, procédez comme suit :

1. Incluez les fichiers de projet.
1. Créez un client de service Repository.
1. Spécifiez l’URI de la ressource à verrouiller.
1. Verrouillez la ressource.
1. Récupérez les verrous de la ressource.
1. Déverrouiller la ressource

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services web, incluez les fichiers proxy.

**Création du client du service**

Avant de pouvoir lire une ressource par programmation, vous devez établir une connexion et fournir des informations d’identification. Pour ce faire, créez un client de service.

**Spécifier l’URI de la ressource à verrouiller**

Créez une chaîne contenant l’URI de la ressource à verrouiller. La syntaxe comprend des barres obliques, comme dans cet exemple : « /*path*/*resource* ».

**Verrouiller la ressource**

Appelez la méthode du service Repository pour verrouiller la ressource, en spécifiant l’URI, le type et la profondeur de verrouillage.

**Récupérer les verrous pour la ressource**

Appelez la méthode du service Repository pour récupérer les verrous de la ressource, en spécifiant l’URI.

**Déverrouiller la ressource**

Appelez la méthode de service Repository pour déverrouiller la ressource, en spécifiant l’URI.

**Voir également**

[Verrouiller les ressources à l’aide de l’API Java](aem-forms-repository.md#lock-resources-using-the-java-api)

[Verrouiller les ressources à lʼaide de l’API de service web](aem-forms-repository.md#lock-resources-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Démarrages rapides de l’API Repository Service](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Verrouiller les ressources à l’aide de l’API Java {#lock-resources-using-the-java-api}

Verrouiller les ressources à l’aide de l’API du service Repository (Java) :

1. Inclure les fichiers du projet

   Incluez les fichiers JAR client dans le chemin de classe de votre projet Java.

1. Création du client de service

   Créez un objet `ResourceRepositoryClient` en utilisant son constructeur et en transmettant un objet `ServiceClientFactory` qui contient les propriétés de connexion.

1. Spécifiez l’URI de la ressource à verrouiller.

   Spécifiez l’URI de la ressource à verrouiller. Dans ce cas, comme la ressource nommée `testResource` se trouve dans le dossier du nom de `testFolder`, son URI est `"/testFolder/testResource"`. L’URI est stocké comme un objet `java.lang.String`.

1. Verrouiller la ressource

   Appelez la méthode `lockResource` de l’objet `ResourceRepositoryClient` et transmettez les paramètres suivants :

   * L’URI de la ressource.
   * La portée du verrouillage. Dans cet exemple, comme la ressource sera verrouillée pour une utilisation exclusive, la portée du verrouillage est fixée à `com.adobe.repository.infomodel.bean.Lock.SCOPE_EXCLUSIVE`.
   * Le niveau de verrouillage. Dans cet exemple, comme le verrouillage ne s’appliquera qu’à la ressource particulière et à aucun de ses membres ou enfants, le niveau de verrouillage est spécifié comme `Lock.DEPTH_ZERO`.

   >[!NOTE]
   >
   >La version surchargée de la méthode `lockResource` qui nécessite quatre paramètres renvoie une exception. Veillez à utiliser la méthode `lockResource` qui nécessite trois paramètres, comme indiqué dans cette présentation.

1. Récupérer les verrouillages de la ressource

   Appelez la méthode `getLocks` de l’objet `ResourceRepositoryClient` et transmettez l’URI de la ressource comme paramètre. La méthode renvoie une liste d’objets verrouillés par laquelle vous pouvez effectuer une itération. Dans cet exemple, le propriétaire, le niveau et la portée du verrouillage sont imprimés pour chaque objet en appelant les méthodes `getOwnerUserId`, `getDepth` et `getType` de chaque objet verrouillé, respectivement.

1. Déverrouiller la ressource

   Appelez la méthode `unlockResource` de l’objet `ResourceRepositoryClient` et transmettez l’URI de la ressource comme paramètre. Pour plus d’informations, consultez la section [Référence de l’API AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Voir également**

[Verrouiller les ressources](aem-forms-repository.md#locking-resources)

[Démarrage rapide (mode SOAP) : verrouiller une ressource à l’aide de l’API Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-locking-a-resource-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Verrouiller les ressources à lʼaide de l’API de service web {#lock-resources-using-the-web-service-api}

Pour verrouiller les ressources à l’aide de l’API du service Repository (service web), procédez comme suit :

1. Inclure les fichiers du projet

   * Créez un assemblage client Microsoft .NET qui utilise le WSDL Repository codé en Base64.
   * Référencez l’assemblage client Microsoft .NET.

1. Création du client de service

   À l’aide de l’assemblage client Microsoft .NET, créez un objet `RepositoryServiceService` en appelant son constructeur par défaut. Définissez sa propriété `Credentials` en utilisant un objet `System.Net.NetworkCredential` contenant le nom d’utilisateur et le mot de passe.

1. Spécifiez l’URI de la ressource à verrouiller.

   Spécifiez une chaîne contenant l’URI de la ressource à verrouiller. Dans ce cas, comme la ressource nommée `testResource` se trouve dans le dossier `testFolder`, son URI est `"/testFolder/testResource"`. Si vous utilisez un langage conforme à Microsoft .NET Framework (C#, par exemple), stockez l’URI dans un objet `System.String`.

1. Verrouiller la ressource

   Appelez la méthode `lockResource` de l’objet `RepositoryServiceService` et transmettez les paramètres suivants :

   * L’URI de la ressource.
   * La portée du verrouillage. Dans cet exemple, comme la ressource sera verrouillée pour une utilisation exclusive, la portée du verrouillage est fixée à `11`.
   * Le niveau de verrouillage. Dans cet exemple, comme le verrouillage ne s’applique qu’à la ressource particulière et à aucun de ses membres ou enfants, le niveau de verrouillage est fixé à `2`.
   * Une valeur `int` indiquant le nombre de secondes avant l’expiration du verrouillage. Dans cet exemple, la valeur de `1000` est utilisée.
   * Transmettez `null` pour le dernier paramètre.

1. Récupérer les verrouillages de la ressource

   Appelez la méthode `getLocks` de l’objet `RepositoryServiceService` et transmettez l’URI de la ressource comme premier paramètre et `null` comme deuxième paramètre. La méthode renvoie un tableau `object` contenant des objets `Lock` par lesquels vous pouvez effectuer une itération. Dans cet exemple, le propriétaire, la profondeur et la portée du verrou sont imprimés pour chaque objet en accédant à chaque `ownerUserId` de l’objet `Lock`, les champs `depth` et `type`, respectivement.

1. Déverrouiller la ressource

   Appelez la méthode `unlockResource` de l’objet `RepositoryServiceService` et transmettez l’URI de la ressource comme premier paramètre et `null` pour le deuxième paramètre.

**Voir également**

[Verrouiller les ressources](aem-forms-repository.md#locking-resources)

[Appeler AEM Forms en utilisant le codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## Suppression des ressources {#deleting-resources}

Vous pouvez supprimer des ressources par programmation d’un emplacement donné dans le référentiel à l’aide de l’API Java du service de référentiel (SOAP).

Lorsque vous supprimez une ressource, la suppression est en principe permanente, bien que, dans certains cas, les référentiels ECM puissent stocker les versions de la ressource en fonction de leurs mécanismes d’historique. Par conséquent, lors de la suppression d’une ressource, il est important de s’assurer que vous n’aurez plus besoin de cette dernière. La suppression d’une ressource est généralement motivée par la nécessité d’augmenter l’espace disponible dans la base de données. Vous pouvez supprimer une version d’une ressource, mais en le faisant, vous devez spécifier l’identificateur de la ressource, et non son identificateur logique (LID) ou son chemin d’accès. Si vous supprimez un dossier, tous éléments y contenus, notamment les sous-dossiers et les ressources, seront automatiquement supprimés.

Les ressources connexes ne sont pas supprimées. Par exemple, si un formulaire utilise le fichier logo.gif et que vous supprimez logo.gif, une relation est stockée dans le tableau de relation en attente. Alternativement, en ce qui concerne l’obsolescence de la version, définissez l’état de l’objet de la dernière version sur obsolète.

Une opération de suppression n’est pas compatible avec les transactions dans les systèmes ECM. Par exemple, si vous tentez de supprimer 100 ressources et que l’opération échoue sur la 50e ressource, les 49 premières instances seront supprimées, mais ce ne sera pas le cas pour le reste. Dans le cas contraire, le comportement par défaut est la restauration (non-engagement).

>[!NOTE]
>
>Lors de l’utilisation de la méthode `com.adobe.repository.bindings.dsc.client.ResourceRepositoryClient.deleteResources()` avec le référentiel ECM (EMC Documentum Content Server et IBM FileNet P8 Content Manager), la transaction ne sera pas restaurée si la suppression échoue pour l’une des ressources spécifiées, ce qui signifie que les fichiers qui ont été supprimés ne peuvent pas être restaurés.

>[!NOTE]
>
>Pour plus d’informations sur le service Repository, voir [Références des services pour AEM Forms](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

### Résumé des étapes {#summary_of_steps-8}

Pour supprimer une ressource, procédez de la manière suivante :

1. Incluez les fichiers de projet.
1. Créez un client de service Repository.
1. Indiquez l’URI de la ressource à supprimer.
1. Supprimez la ressource.

**Inclure des fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services web, incluez les fichiers proxy.

**Création du client du service**

Avant de pouvoir lire une ressource par programmation, vous devez établir une connexion et fournir des informations d’identification. Pour ce faire, créez un client de service.

**Spécifier l’URI de la ressource à supprimer**

Créez une chaîne contenant l’URI de la ressource à supprimer. La syntaxe comprend des barres obliques, comme dans l’exemple suivant : « /*chemin*/*ressource* ». Si la ressource à supprimer est un dossier, la suppression sera récursive.

**Supprimer la ressource**

Appelez la méthode du service Repository pour supprimer la ressource, en spécifiant l’URI.

**Voir également**

[Supprimer des ressources à l’aide de l’API Java](aem-forms-repository.md#delete-resources-using-the-java-api-soap)

[Suppression des ressources à l’aide de l’API de service web](aem-forms-repository.md#delete-resources-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Démarrages rapides de l’API Repository Service](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Supprimer des ressources à l’aide de l’API Java (SOAP) {#delete-resources-using-the-java-api-soap}

Supprimez une ressource à l’aide de l’API de référentiel (Java) :

1. Inclure les fichiers du projet

   Incluez les fichiers JAR client dans le chemin de classe de votre projet Java.

1. Création du client de service

   Créez un objet `ResourceRepositoryClient` en utilisant son constructeur et en transmettant un objet `ServiceClientFactory` contenant des propriétés de connexion.

1. Spécification de l’URI de la ressource à supprimer

   Spécifiez l’URI de la ressource à récupérer. Dans ce cas, puisque la ressource désignée par testResourceToBeDeleted se trouve dans le dossier nommé testFolder, son URI est `/testFolder/testResourceToBeDeleted`. L’URI est stocké en tant qu’objet `java.lang.String`. Dans cet exemple, la ressource est d’abord écrite dans le référentiel, puis son URI est récupéré. Pour plus d’informations sur l’écriture d’une ressource, voir [Écriture de ressources](aem-forms-repository.md#writing-resources).

1. Suppression de la ressource

   Appelez la méthode `deleteResource` de l’objet `ResourceRepositoryClient` et transmettez l’URI de la ressource en tant que paramètre.

**Voir également**

[Suppression des ressources](aem-forms-repository.md#deleting-resources)

[Démarrage rapide (mode SOAP) : rechercher des ressources à l’aide de l’API Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-searching-for-resources-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Suppression des ressources à l’aide de l’API de service web {#delete-resources-using-the-web-service-api}

Pour supprimer une ressource en utilisant l’API Repository (service web), procédez comme suit :

1. Inclure les fichiers du projet

   * Créez un assemblage client Microsoft .NET qui utilise le WSDL Repository codé en Base64.
   * Référencez l’assemblage client Microsoft .NET.

1. Création du client de service

   À l’aide de l’assemblage client Microsoft .NET, créez un objet `RepositoryServiceService` en appelant son constructeur par défaut. Définissez sa propriété `Credentials` en utilisant un objet `System.Net.NetworkCredential` contenant le nom dʼutilisateur et le mot de passe.

1. Spécification de l’URI de la ressource à supprimer

   Spécifiez l’URI de la ressource à récupérer. Dans ce cas, comme la ressource nommée `testResourceToBeDeleted` se trouve dans le dossier `testFolder`, son URI est `"/testFolder/testResourceToBeDeleted"`. Dans cet exemple, la ressource est d’abord écrite dans le référentiel, puis son URI est récupéré. Pour plus d’informations sur l’écriture d’une ressource, voir [Écriture de ressources](aem-forms-repository.md#writing-resources).

1. Suppression de la ressource

   Appelez la méthode `deleteResources` de lʼobjet `RepositoryServiceService` et transmettez un tableau `System.String` contenant lʼURI de la ressource comme premier paramètre. Transmettez `null` pour le deuxième paramètre.

**Voir également**

[Suppression des ressources](aem-forms-repository.md#deleting-resources)

[Appeler AEM Forms en utilisant le codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
