---
title: Utilisation du référentiel AEM Forms
seo-title: Utilisation du référentiel AEM Forms
description: 'null'
seo-description: 'null'
uuid: 6ead49f9-ca0d-4ee4-86a6-0a9ced6ec4f8
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: d2c95881-6c02-4e34-85af-84607df54287
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Working with AEM Forms Repository {#working-with-aem-forms-repository}

**A propos du service Repository**

Le service Repository fournit des services de stockage des ressources et de gestion à AEM Forms. When developers create an *AEM Forms* application, they can deploy the assets in the repository instead of the file system. Les actifs peuvent être constitués de formulaires XML, de formulaires PDF (y compris de formulaires Acrobat), de fragments de formulaire, d’images, de profils, de stratégies, de fichiers SWF, DDX et WSDL, de schémas XML et de données de test.

Prenons l’exemple de l’application Forms suivante nommée *Applications/FormsApplication*:

![ww_ww_formrepository](assets/ww_ww_formrepository.png)

Notez qu’un fichier nommé Loan.xdp se trouve dans FormsFolder. Pour accéder à cette conception de formulaire, vous spécifiez le chemin d’accès complet (y compris la version) : `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.

>[!NOTE]
>
>Pour plus d’informations sur la création d’une application Forms à l’aide de Workbench, voir Aide [de](https://www.adobe.com/go/learn_aemforms_workbench_63)Workbench.

Le chemin d’accès à une ressource située dans le référentiel AEM Forms est :

`Applications/Application-name/Application-version/Folder.../Filename`

Les valeurs suivantes illustrent des exemples de valeurs URI :

* Applications/AppraisalReport/1.0/Forms/FullForm.xdp
* Applications/AnotherApp/1.1/Assets/picture.jpg
* Applications/SomeApp/2.0/Resources/Data/XSDs/MyData.xsd

>[!NOTE]
>
>Vous pouvez parcourir le référentiel AEM Forms à l’aide d’un navigateur Web. Pour parcourir le référentiel, saisissez l’URL suivante dans un navigateur Web https://[serveur]:port[/référentiel]serveur. Vous pouvez vérifier les résultats de démarrage rapide associés à la section Utilisation du référentiel AEM Forms à l’aide d’un navigateur Web. Par exemple, si vous ajoutez du contenu au référentiel AEM Forms, vous pouvez le voir dans un navigateur Web. (See [Quick Start (SOAP mode): Writing a resource using the Java API](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-writing-a-resource-using-the-java-api).)

L’API du référentiel fournit un certain nombre d’opérations que vous pouvez utiliser pour stocker et récupérer des informations du référentiel. Par exemple, vous pouvez obtenir une liste de ressources ou récupérer des ressources spécifiques stockées dans le référentiel lorsqu’une ressource est nécessaire dans le cadre du traitement d’une application.

>[!NOTE]
>
>L’API du référentiel ne peut pas être utilisée pour interagir avec Content Services (obsolète). Pour interagir avec Content Services (obsolète), vous utilisez l’API Document Management.

L’API du service Repository vous permet d’effectuer les tâches suivantes :

* Création de dossiers. Voir [Création de dossiers](aem-forms-repository.md#creating-folders).
* Ecrivez des ressources et leurs propriétés. Voir [Ecriture de ressources](aem-forms-repository.md#writing-resources).
* Répertorie les ressources d’une collection donnée ou liées à d’autres ressources. Voir [Liste des ressources](aem-forms-repository.md#listing-resources).
* Lisez les ressources et leurs propriétés. Voir [Lecture des ressources](aem-forms-repository.md#reading-resources).
* Mettez à jour les ressources et leurs propriétés. Voir [Mise à jour des ressources](aem-forms-repository.md#updating-resources).
* Recherchez des ressources, y compris leur historique, les ressources connexes et leurs propriétés. Voir [Recherche de ressources](aem-forms-repository.md#searching-for-resources).
* Spécifiez les relations entre les ressources. Voir [Création de relations](aem-forms-repository.md#creating-resource-relationships)de ressources.
* Gérez le contrôle d&#39;accès aux ressources, y compris le verrouillage et le déverrouillage des ressources, ainsi que la lecture et l&#39;écriture des listes de contrôle d&#39;accès (ACL). Voir [Verrouillage des ressources](aem-forms-repository.md#locking-resources).
* Supprimez les ressources et leurs propriétés. Voir [Suppression de ressources](aem-forms-repository.md#deleting-resources).

>[!NOTE]
>
>A l’aide de l’API du référentiel, vous ne pouvez pas gérer le contrôle d’accès aux ressources, rechercher des ressources ou spécifier des relations de ressources à l’aide d’un référentiel ECM.

>[!NOTE]
>
>Lorsqu’un fichier PDF chiffré est écrit dans le référentiel, la fonction d’extraction de relation automatisée ne peut pas être utilisée. Sinon, un fichier PDF chiffré peut être stocké dans le référentiel et récupéré ultérieurement. Le récupérateur peut choisir de déchiffrer le PDF après l’avoir récupéré du référentiel.

>[!NOTE]
>
>For more information about the Repository service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Création de dossiers {#creating-folders}

Les dossiers (collections de ressources) servent à stocker des objets (fichiers ou ressources) dans des regroupements organisés. Les dossiers peuvent contenir des ressources et d’autres dossiers, également appelés sous-dossiers. Les ressources ne peuvent être stockées que dans un dossier à la fois.

Les fichiers héritent des listes de contrôle d’accès (ACL) des dossiers et les sous-dossiers héritent des listes de contrôle d’accès (ACL) de leurs dossiers parents. Par conséquent, les dossiers parents doivent exister avant de pouvoir créer des dossiers enfants. L&#39;IDE vous permet d&#39;interagir uniquement dossier par dossier, et non fichier par fichier. Vous ne pouvez pas modifier les dossiers de version et il n’est pas nécessaire de le faire ; un dossier ne contient pas de données proprement dites. Il s’agit plutôt d’un conteneur pour les ressources qui contiennent des données. La liste de contrôle d’accès par défaut est une autorisation au niveau du système, ce qui signifie que les utilisateurs doivent disposer d’autorisations au niveau du système (lecture, écriture, traversée, gestion des listes de contrôle d’accès) jusqu’à ce qu’un utilisateur leur donne des autorisations pour un dossier particulier. Les listes ACL ne fonctionnent que dans l&#39;IDE.

>[!NOTE]
>
>For more information about the Repository service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary-of-steps}

Pour créer un dossier, procédez comme suit :

1. Incluez des fichiers de projet.
1. Créez le client de service.
1. Créez le dossier.
1. Ecrivez le dossier dans le référentiel.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, incluez les fichiers proxy.

**Création du client de service**

Avant de pouvoir créer une collection de ressources par programmation, vous devez établir une connexion et fournir des informations d’identification. Pour ce faire, vous devez créer un client de service.

**Création du dossier**

Appelez la méthode du service Repository pour créer la collecte de ressources et renseigner la collecte de ressources avec des informations d’identification, y compris son UUID, son nom de dossier et sa description.

**Ecrivez le dossier dans le référentiel**

Appelez la méthode du service Repository pour écrire la collection de ressources, en spécifiant l’URI du dossier cible.

**Voir également**

[Création de dossiers à l’aide de l’API Java](aem-forms-repository.md#create-folders-using-the-java-api)

[Création de dossiers à l’aide de l’API de service Web](aem-forms-repository.md#create-folders-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Démarrage rapide de l’API Repository Service](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Création de dossiers à l’aide de l’API Java {#create-folders-using-the-java-api}

Créez un dossier à l’aide de l’API du service Repository (Java) :

1. Inclure les fichiers de projet

   Incluez des fichiers de projet dans le chemin de classe de votre projet Java.

1. Création du client de service

   Créez un `ResourceRepositoryClient` objet en utilisant son constructeur et en transmettant un `ServiceClientFactory` objet contenant des propriétés de connexion.

1. Création du dossier

   Pour créer une collection de ressources, vous devez d’abord créer un `com.adobe.repository.infomodel.bean.RepositoryInfomodelFactoryBean` objet.

   Appelez la méthode `repositoryInfomodelFactoryBean` `newResourceCollection` de l’objet et transmettez les paramètres suivants :

   * Identifiant `com.adobe.repository.infomodel.Id` UUID à affecter à la ressource.
   * Identifiant `com.adobe.repository.infomodel.Lid` UUID à affecter à la ressource.
   * Un `java.lang.String` nom contenant le nom de la collection de ressources. Par exemple, `FormsFolder`.
   La méthode renvoie un `com.adobe.repository.infomodel.bean.ResourceCollection` objet représentant le nouveau dossier.

   Définissez la description du dossier à l’aide de la `setDescription` méthode et transmettez le paramètre suivant :

   * Description `String` de la collection de ressources. Dans cet exemple, `"test Folder"` est utilisé `.`


1. Ecrivez le dossier dans le référentiel

   Appelez la méthode `ResourceRepositoryClient` de l’objet et transmettez l’URI du dossier et de l’ `writeResource` `ResourceCollection` objet. Par exemple, l’URI du dossier peut être la valeur suivante `/Applications/FormsApplication/1.0/`.

   La méthode renvoie une instance de l’ `com.adobe.repository.infomodel.bean.Resource` objet nouvellement créé. Vous pouvez, par exemple, récupérer la valeur d’identificateur de la nouvelle ressource en appelant la `com.adobe.repository.infomodel.bean.Resource` `getId` méthode de l’objet.

**Voir également**

[Création de dossiers](aem-forms-repository.md#creating-folders)

[Démarrage rapide (mode SOAP) : Création d’un dossier à l’aide de l’API Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-creating-a-folder-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Création de dossiers à l’aide de l’API de service Web {#create-folders-using-the-web-service-api}

Créez un dossier à l’aide de l’API du service de référentiel (service Web) :

1. Inclure les fichiers de projet

   * Créez un assembly client Microsoft .NET qui consomme le fichier WSDL du référentiel à l&#39;aide de base64.
   * Référencez l&#39;assembly client Microsoft .NET.

1. Création du client de service

   A l&#39;aide de l&#39;assembly client Microsoft .NET, créez un `RepositoryServiceService` objet en appelant son constructeur par défaut. Définissez sa `Credentials` propriété à l’aide d’un `System.Net.NetworkCredential` objet contenant le nom d’utilisateur et le mot de passe.

1. Création du dossier

   Créez le dossier à l’aide du constructeur par défaut de la `ResourceCollection` classe et transmettez les paramètres suivants :

   * Un `Id` objet, qui est créé en appelant le constructeur par défaut de la `Id` classe et affecté au `Resource` `id` champ de l’objet.
   * Un `Lid` objet, qui est créé en appelant le constructeur par défaut de la `Lid` classe et affecté au `Resource` `lid` champ de l’objet.
   * Chaîne contenant le nom de la collection de ressources, qui est affectée au `Resource` `name` champ de l’objet. Le nom utilisé dans cet exemple est `"testfolder"`.
   * Chaîne contenant la description de la collection de ressources, qui est affectée au `Resource` `description` champ de l’objet. La description utilisée dans cet exemple est `"test folder"`.

1. Ecrivez le dossier dans le référentiel

   Appelez la méthode `RepositoryServiceService` `writeResource` de l’objet et transmettez les paramètres suivants :

   * Chemin d’accès où le dossier doit être créé.
   * Objet `ResourceCollection` représentant le dossier.
   * Transmettez `null` les deux autres paramètres.

**Voir également**

[Création de dossiers](aem-forms-repository.md#creating-folders)

[Appel d’AEM Forms à l’aide du codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## Ecriture de ressources {#writing-resources}

Vous pouvez créer des ressources à un emplacement donné dans le référentiel. La taille du fichier naturel est soumise à des limitations de base de données et au délai d’expiration de session. Pour la configuration par défaut, les fichiers sont limités à 25 Mo. Pour augmenter ou diminuer la taille maximale du fichier, vous devez modifier la configuration de la base de données.

Ecrire des ressources équivaut à stocker des données dans le référentiel. Une fois que vous écrivez une ressource dans le référentiel, elle devient accessible à tous les clients de l’écosystème du référentiel. Lorsque vous créez des ressources, telles que des schémas XML, des fichiers XDP et des fichiers XSD, dans le référentiel, le contenu est analysé en fonction du type MIME. Si le type MIME est pris en charge, l’analyseur détermine s’il existe une relation implicite avec un autre contenu. Par exemple, si une feuille de style en cascade (CSS) comporte une URL relative qui fait référence à une page CSS commune, vous devez également envoyer la page CSS commune dans le référentiel. La relation entre les deux ressources est stockée en tant que relation en attente pour une période non ajustable de 30 jours. Lorsque vous envoyez la page CSS commune au référentiel au cours de la période de 30 jours, la relation est formée.

Lorsque vous créez une ressource, la liste de contrôle d’accès (ACL) est héritée du dossier parent. Le dossier racine dispose d’autorisations au niveau du système jusqu’à la création d’une ressource ou d’un dossier initial, auquel moment les autorisations ACL par défaut sont attribuées à la ressource ou au dossier.

Vous pouvez écrire des ressources par programmation à l’aide de l’API Java du service Repository ou de l’API du service Web.

>[!NOTE]
>
>For more information about the Repository service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary_of_steps-1}

Pour écrire une ressource, procédez comme suit :

1. Incluez des fichiers de projet.
1. Créez un client de service Repository.
1. Spécifiez l’URI de la ressource à lire.
1. Lisez la ressource.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, incluez les fichiers proxy.

**Création du client de service**

Avant de pouvoir lire une ressource par programmation, vous devez établir une connexion et fournir des informations d’identification. Pour ce faire, vous devez créer un client de service.

**Spécifiez l’URI du dossier cible pour la ressource.**

Créez une chaîne contenant l’URI de la ressource à lire. La syntaxe comprend des barres obliques, comme dans cet exemple : &quot;/*path*/*folder*&quot;.

**Création de la ressource**

Appelez la méthode du service Repository pour créer la ressource et renseignez la ressource avec des informations d’identification, y compris son UUID, son nom et sa description.

**Spécifier le contenu de la ressource**

Appelez la méthode du service Repository pour créer du contenu de ressource et stocker ce contenu dans la ressource.

**Ecrire la ressource dans le dossier cible**

Appelez la méthode du service Repository pour écrire la ressource, en spécifiant l’URI du dossier cible.

**Voir également**

[Ecriture de ressources à l’aide de l’API Java](aem-forms-repository.md#write-resources-using-the-java-api)

[Ecrire des ressources à l’aide de l’API de service Web](aem-forms-repository.md#write-resources-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Démarrage rapide de l’API Repository Service](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Ecriture de ressources à l’aide de l’API Java {#write-resources-using-the-java-api}

Ecrivez une ressource à l’aide de l’API du service Repository (Java) :

1. Inclure les fichiers de projet

   Incluez les fichiers JAR client dans le chemin de classe de votre projet Java.

1. Création du client de service

   Créez un `ResourceRepositoryClient` objet en utilisant son constructeur et en transmettant un `ServiceClientFactory` objet contenant des propriétés de connexion.

1. Spécifiez l’URI du dossier cible pour la ressource.

   Spécifiez l’URI du dossier cible pour la ressource. Dans ce cas, étant donné que la ressource nommée `testResource` sera stockée dans le dossier nommé `testFolder`, l’URI du dossier est `"/testFolder"`. L’URI est stocké sous la forme d’un `java.lang.String` objet.

1. Création de la ressource

   Pour créer une ressource, vous devez d’abord créer un `com.adobe.repository.infomodel.bean.RepositoryInfomodelFactoryBean` objet.

   Appelez la `RepositoryInfomodelFactoryBean` méthode de l’ `newResource` objet, qui crée un `com.adobe.repository.infomodel.bean.Resource` objet. Dans cet exemple, les paramètres suivants sont fournis :

   * Un `com.adobe.repository.infomodel.Id` objet, créé en appelant le constructeur par défaut pour la `Id` classe.
   * Un `com.adobe.repository.infomodel.Lid` objet, créé en appelant le constructeur par défaut pour la `Lid` classe.
   * Un nom `java.lang.String` contenant le nom de fichier de la ressource.
   Pour spécifier la description de la ressource, appelez la `Resource` `setDescription` méthode de l’objet et transmettez une chaîne contenant la description. Dans cet exemple, la description est `"test resource"`.

1. Spécifier le contenu de la ressource

   Pour créer du contenu pour la ressource, appelez la `RepositoryInfomodelFactoryBean` méthode de l’objet, qui renvoie un `newResourceContent` `com.adobe.repository.infomodel.bean.ResourceContent` objet. Add content to the `ResourceContent` object. Dans cet exemple, vous effectuez les tâches suivantes :

   * Appel de la `ResourceContent` méthode de l’ `setDataDocument` objet et transmission d’un `com.adobe.idp.Document` objet
   * Appel de la `ResourceContent` méthode de l’ `setSize` objet et transmission de la taille en octets de l’ `Document` objet
   Ajoutez le contenu à la ressource en appelant la `Resource` méthode de l’objet et en transmettant l’ `setContent` `ResourceContent` objet. For more information, see [AEM Forms API Reference](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. Ecrire la ressource dans le dossier cible

   Appelez la méthode `ResourceRepositoryClient` de l’objet et transmettez l’URI du dossier, ainsi que l’ `writeResource` `Resource` objet.

**Voir également**

[Ecriture de ressources](aem-forms-repository.md#writing-resources)

[Démarrage rapide (mode SOAP) : Ecriture d’une ressource à l’aide de l’API Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-writing-a-resource-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Ecrire des ressources à l’aide de l’API de service Web {#write-resources-using-the-web-service-api}

Ecrivez une ressource à l’aide de l’API du service de référentiel (service Web) :

1. Inclure les fichiers de projet

   * Créez un assembly client Microsoft .NET qui consomme le fichier WSDL du référentiel à l&#39;aide de base64.
   * Référencez l&#39;assembly client Microsoft .NET.

1. Création du client de service

   A l&#39;aide de l&#39;assembly client Microsoft .NET, créez un `RepositoryServiceService` objet en appelant son constructeur par défaut. Définissez sa `Credentials` propriété à l’aide d’un `System.Net.NetworkCredential` objet contenant le nom d’utilisateur et le mot de passe.

1. Spécifiez l’URI du dossier cible pour la ressource.

   Spécifiez l’URI du dossier cible pour la ressource. Dans ce cas, étant donné que la ressource nommée `testResource` sera stockée dans le dossier nommé `testFolder`, l’URI du dossier est `"/testFolder"`. Lorsque vous utilisez un langage compatible avec Microsoft .NET Framework (C#, par exemple), stockez l’URI dans un `System.String` objet.

1. Création de la ressource

   Pour créer une ressource, appelez le constructeur par défaut de la `Resource` classe. Dans cet exemple, les informations suivantes sont stockées dans l’ `Resource` objet :

   * Un `com.adobe.repository.infomodel.Id` objet, qui est créé en appelant le constructeur par défaut de la `Id` classe et affecté au `Resource` champ de l’ `id` objet.
   * Un `com.adobe.repository.infomodel.Lid` objet, qui est créé en appelant le constructeur par défaut de la `Lid` classe et affecté au `Resource` champ de l’ `lid` objet.
   * Chaîne contenant le nom de fichier de la ressource, qui est affectée au `Resource` `name` champ de l’objet. Le nom utilisé dans cet exemple est `"testResource"`.
   * Chaîne contenant la description de la ressource, affectée au `Resource` `description` champ de l’objet. La description utilisée dans cet exemple est `"test resource"`.

1. Spécifier le contenu de la ressource

   Pour créer du contenu pour la ressource, appelez le constructeur par défaut de la `ResourceContent` classe. Ajoutez ensuite du contenu à l’ `ResourceContent` objet. Dans cet exemple, vous effectuez les tâches suivantes :

   * Affectation d’un `BLOB` objet contenant un document au `ResourceContent` `dataDocument` champ de l’objet.
   * Attribuez la taille en octets de l’ `BLOB` objet au `ResourceContent` `size` champ de l’objet.
   Ajoutez le contenu à la ressource en affectant l’ `ResourceContent` objet au `Resource` `content` champ de l’objet.

1. Ecrire la ressource dans le dossier cible

   Appelez la méthode `RepositoryServiceService` de l’objet et transmettez l’URI du dossier, ainsi que l’ `writeResource` `Resource` objet. Transmettez `null` les deux autres paramètres.

**Voir également**

[Ecriture de ressources](aem-forms-repository.md#writing-resources)

[Appel d’AEM Forms à l’aide du codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## Liste des ressources {#listing-resources}

Vous pouvez découvrir des ressources en répertoriant les ressources. Une requête est exécutée sur le référentiel pour rechercher toutes les ressources liées à une collection de ressources donnée.

Une fois vos ressources organisées, vous pouvez examiner la structure que vous avez créée en voyant une branche particulière de la structure, comme vous le feriez dans un système d&#39;exploitation.

La liste des ressources fonctionne par relation : ressources sont des membres de dossiers. L&#39;appartenance est représentée par une relation de type &quot;membre de&quot;. Lorsque vous répertoriez des ressources dans un dossier donné, vous recherchez des ressources liées à un dossier donné par la relation &quot;membre de&quot;. Les relations sont directionnelles : un membre d’une relation a une source qui est un membre de la cible. La source est la ressource; la cible est le dossier parent.

>[!NOTE]
>
>For more information about the Repository service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary_of_steps-2}

Pour répertorier les ressources, procédez comme suit :

1. Incluez des fichiers de projet.
1. Créez le client de service.
1. Spécifiez le chemin d’accès au dossier.
1. Récupérez la liste des ressources.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, incluez les fichiers proxy.

**Création du client de service**

Avant de pouvoir créer une collection de ressources par programmation, vous devez établir une connexion et fournir des informations d’identification. Pour ce faire, vous devez créer un client de service.

**Définition du chemin d’accès au dossier**

Créez une chaîne contenant le chemin du dossier contenant les ressources. La syntaxe comprend des barres obliques, comme dans cet exemple : &quot;/*path*/*folder*&quot;.

**Récupérer la liste des ressources**

Appelez la méthode du service Repository pour récupérer la liste des ressources, en spécifiant le chemin d’accès du dossier cible.

**Voir également**

[Répertorier les ressources à l’aide de l’API Java](aem-forms-repository.md#list-resources-using-the-java-api)

[Répertorier les ressources à l’aide de l’API de service Web](aem-forms-repository.md#list-resources-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Démarrage rapide de l’API Repository Service](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Répertorier les ressources à l’aide de l’API Java {#list-resources-using-the-java-api}

Répertorier les ressources à l’aide de l’API du service Repository (Java) :

1. Inclure les fichiers de projet

   Incluez les fichiers JAR client dans le chemin de classe de votre projet Java.

1. Création du client de service

   Créez un `ResourceRepositoryClient` objet en utilisant son constructeur et en transmettant un `ServiceClientFactory` objet contenant des propriétés de connexion.

1. Définition du chemin d’accès au dossier

   Spécifiez l’URI de la collection de ressources à interroger. Dans ce cas, son URI est `"/testFolder"`. L’URI est stocké sous la forme d’un `java.lang.String` objet.

1. Récupérer la liste des ressources

   Appelez la méthode `ResourceRepositoryClient` `listMembers` de l’objet et transmettez l’URI du dossier.

   La méthode renvoie un `java.util.List` nombre d’ `com.adobe.repository.infomodel.bean.Resource` objets qui sont la source d’un `com.adobe.repository.infomodel.bean.Relation` de type `Relation.TYPE_MEMBER_OF` et dont l’URI de collecte de ressources est la cible. Vous pouvez effectuer une itération `List` pour récupérer chacune des ressources. Dans cet exemple, le nom et la description de chaque ressource sont affichés.

**Voir également**

[Liste des ressources](aem-forms-repository.md#listing-resources).

[Démarrage rapide (mode SOAP) : Liste des ressources à l’aide de l’API Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-listing-resources-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Répertorier les ressources à l’aide de l’API de service Web {#list-resources-using-the-web-service-api}

Répertorier les ressources à l’aide de l’API du service Repository (service Web) :

1. Inclure les fichiers de projet

   * Créez un assembly client Microsoft .NET qui consomme le fichier WSDL du référentiel.
   * Référencez l&#39;assembly client Microsoft .NET.

1. Création du client de service

   A l&#39;aide de l&#39;assembly client Microsoft .NET, créez un `RepositoryServiceService` objet en appelant son constructeur par défaut. Définissez sa `Credentials` propriété à l’aide d’un `System.Net.NetworkCredential` objet contenant le nom d’utilisateur et le mot de passe.

1. Définition du chemin d’accès au dossier

   Spécifiez une chaîne contenant l’URI du dossier à interroger. Dans ce cas, son URI est `"/testFolder"`. Lorsque vous utilisez un langage compatible avec Microsoft .NET Framework (C#, par exemple), stockez l’URI dans un `System.String` objet.

1. Récupérer la liste des ressources

   Appelez la méthode `RepositoryServiceService` `listMembers` de l’objet et transmettez l’URI du dossier comme premier paramètre. Transmettez `null` les deux autres paramètres.

   La méthode renvoie un tableau d’objets pouvant être projetés vers `Resource` des objets. Vous pouvez effectuer une itération dans le tableau d’objets pour récupérer chacune des ressources associées. Dans cet exemple, le nom et la description de chaque ressource sont affichés.

**Voir également**

[Liste des ressources](aem-forms-repository.md#listing-resources).

[Appel d’AEM Forms à l’aide du codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## Ressources de lecture {#reading-resources}

Vous pouvez récupérer des ressources à partir d’un emplacement donné dans le référentiel afin de lire leur contenu et leurs métadonnées. Le flux de travail est recto par un formulaire d’initialisation. Le processus dispose de toutes les autorisations nécessaires pour lire le formulaire. Le système récupère le formulaire de données et lit le contenu du référentiel. Le référentiel permet d’accéder au contenu et aux métadonnées (la possibilité même de connaître la ressource existe).

Le référentiel comporte les quatre types d’autorisations suivants :

* **traverse**: vous permet de répertorier les ressources ; c’est-à-dire pour lire les métadonnées de ressource, mais pas le contenu de la ressource
* **lire**: vous permet de lire le contenu des ressources
* **write**: vous permet d&#39;écrire le contenu des ressources
* **gestion des listes de contrôle d&#39;accès (ACL)**: permet de manipuler les listes de contrôle d’accès sur les ressources

Les utilisateurs ne peuvent exécuter les processus que s’ils sont autorisés à exécuter le processus. Les utilisateurs IDE ont besoin d’autorisations de lecture et de traversée pour se synchroniser avec le référentiel. Les listes de contrôle d’accès s’appliquent uniquement au moment de la conception, car l’exécution se produit dans le contexte du système.

Vous pouvez programmer la lecture des ressources à l’aide de l’API Java du service Repository ou de l’API du service Web.

>[!NOTE]
>
>For more information about the Repository service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary_of_steps-3}

Pour lire une ressource, procédez comme suit :

1. Incluez des fichiers de projet.
1. Créez un client de service Repository.
1. Spécifiez l’URI de la ressource à lire.
1. Lisez la ressource.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, incluez les fichiers proxy.

**Création du client de service**

Avant de pouvoir lire une ressource par programmation, vous devez établir une connexion et fournir des informations d’identification. Pour ce faire, vous devez créer un client de service.

**Spécifiez l’URI de la ressource à lire.**

Créez une chaîne contenant l’URI de la ressource à lire. La syntaxe comprend des barres obliques, comme dans cet exemple : &quot;/*path*/*resource*&quot;.

**Lire la ressource**

Appelez la méthode du service Repository pour lire la ressource, en spécifiant l’URI.

**Voir également**

[Lire les ressources à l’aide de l’API Java](aem-forms-repository.md#read-resources-using-the-java-api)

[Lecture de ressources à l’aide de l’API de service Web](aem-forms-repository.md#reading-resources-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Démarrage rapide de l’API Repository Service](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Lire les ressources à l’aide de l’API Java {#read-resources-using-the-java-api}

Lisez une ressource à l’aide de l’API du service Repository (Java) :

1. Inclure les fichiers de projet

   Incluez les fichiers JAR client dans le chemin de classe de votre projet Java.

1. Création du client de service

   Créez un `ResourceRepositoryClient` objet en utilisant son constructeur et en transmettant un `ServiceClientFactory` objet contenant des propriétés de connexion.

1. Spécifiez l’URI de la ressource à lire.

   Spécifiez une valeur de chaîne qui représente l’URI de la ressource à récupérer. Par exemple, en supposant que la ressource soit nommée *testResource* et se trouve dans un dossier appelé *testFolder*, spécifiez `/testFolder/testResource`.

1. Lire la ressource

   Appelez la méthode `ResourceRepositoryClient` `readResource` de l’objet et transmettez l’URI de la ressource en tant que paramètre. Cette méthode renvoie une `Resource` instance qui représente la ressource.

**Voir également**

[Ressources de lecture](aem-forms-repository.md#reading-resources)

[Démarrage rapide (mode SOAP) : Lecture d’une ressource à l’aide de l’API Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-reading-a-resource-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Lecture de ressources à l’aide de l’API de service Web {#reading-resources-using-the-web-service-api}

Lisez une ressource à l’aide de l’API du service de référentiel (service Web) :

1. Inclure les fichiers de projet

   * Créez un assembly client Microsoft .NET qui consomme le fichier WSDL du référentiel. (voir [Création d&#39;un assembly client .NET utilisant le codage](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)Base64).
   * Référencez l&#39;assembly client Microsoft .NET. (voir [Création d&#39;un assembly client .NET utilisant le codage](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)Base64).

1. Création du client de service

   A l&#39;aide de l&#39;assembly client Microsoft .NET, créez un `RepositoryServiceService` objet en appelant son constructeur par défaut. Définissez sa `Credentials` propriété à l’aide d’un `System.Net.NetworkCredential` objet contenant le nom d’utilisateur et le mot de passe.

1. Spécifiez l’URI de la ressource à lire.

   Spécifiez une chaîne contenant l’URI de la ressource à récupérer. Dans ce cas, puisque la ressource nommée `testResource` se trouve dans le dossier nommé `testFolder`, son URI est `"/testFolder/testResource"`. Lorsque vous utilisez un langage compatible avec Microsoft .NET Framework (C#, par exemple), stockez l’URI dans un `System.String` objet.

1. Lire la ressource

   Appelez la méthode `RepositoryServiceService` `readResource` de l’objet et transmettez l’URI de la ressource comme premier paramètre. Transmettez `null` les deux autres paramètres.

**Voir également**

[Ressources de lecture](aem-forms-repository.md#reading-resources)

[Appel d’AEM Forms à l’aide du codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## Mise à jour des ressources {#updating-resources}

Vous pouvez récupérer et mettre à jour le contenu des ressources dans le référentiel. Lorsque vous mettez à jour des ressources, le contrôle d’accès à ces ressources reste inchangé entre les versions. Lors d’une mise à jour, vous avez la possibilité d’incrémenter la version majeure. Si vous ne choisissez pas d’incrémenter la version majeure, la version mineure est automatiquement mise à jour.

Lorsque vous mettez à jour une ressource, la nouvelle version est créée en fonction des attributs de ressource spécifiés. Lorsque vous mettez à jour une ressource, vous spécifiez deux paramètres importants : l’URI cible et une instance de ressource contenant toutes les métadonnées mises à jour. Il est important de noter que si vous ne modifiez pas un attribut donné (par exemple, le nom), l’attribut est toujours requis dans l’instance que vous transmettez. Les relations créées lors de l’analyse du contenu sont ajoutées à la version spécifique et ne sont pas avancées, sauf indication contraire.

Par exemple, si vous mettez à jour un fichier XDP contenant des références à d’autres ressources, ces références supplémentaires seront également enregistrées. Supposons que form.xdp version 1.0 comporte deux références externes : un logo et une feuille de style, et vous mettez ensuite à jour le fichier form.xdp afin qu’il comporte désormais trois références : un logo, une feuille de style et un fichier de schéma. Pendant la mise à jour, le référentiel ajoute la troisième relation (au fichier de schéma) à sa table de relations en attente. Une fois le fichier de schéma présent dans le référentiel, la relation est automatiquement formée. Cependant, si form.xdp version 2.0 n’utilise plus le logo, form.xdp version 2.0 n’aura pas de relation avec le logo.

Toutes les opérations de mise à jour sont atomiques et transactionnelles. Par exemple, si deux utilisateurs lisent la même ressource et décident tous deux de mettre à jour la version 1.0 vers la version 2.0, l’un d’eux réussira et l’autre échouera, l’intégrité du référentiel sera conservée et un message confirmant la réussite ou l’échec sera envoyé. Si la transaction n’est pas validée, elle est restaurée en cas d’échec de la base de données et expire ou est restaurée selon le serveur d’applications.

Vous pouvez mettre à jour les ressources par programmation à l’aide de l’API Java du service Repository ou de l’API du service Web.

>[!NOTE]
>
>For more information about the Repository service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary_of_steps-4}

Pour mettre à jour une ressource, procédez comme suit :

1. Incluez des fichiers de projet.
1. Créez un client de service Repository.
1. Récupérez la ressource à mettre à jour.
1. Mettez à jour la ressource.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, incluez les fichiers proxy.

**Création du client de service**

Avant de pouvoir lire une ressource par programmation, vous devez établir une connexion et fournir des informations d’identification. Pour ce faire, vous devez créer un client de service.

**Récupérer la ressource à mettre à jour**

Lisez la ressource. Pour plus d’informations, voir [Lecture des ressources](aem-forms-repository.md#reading-resources).

**Mettre à jour la ressource**

Définissez les nouvelles informations dans la ressource et appelez la méthode du service Repository pour mettre à jour la ressource, en spécifiant l&#39;URI, la ressource mise à jour et la manière dont les informations de version doivent être mises à jour.

**Voir également**

[Mise à jour des ressources à l’aide de l’API Java](aem-forms-repository.md#update-resources-using-the-java-api)

[Mise à jour des ressources à l’aide de l’API de service Web](aem-forms-repository.md#update-resources-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Démarrage rapide de l’API Repository Service](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Mise à jour des ressources à l’aide de l’API Java {#update-resources-using-the-java-api}

Mettez à jour une ressource à l’aide de l’API du service Repository (Java) :

1. Inclure les fichiers de projet

   Incluez les fichiers JAR client dans le chemin de classe de votre projet Java.

1. Création du client de service

   Créez un `ResourceRepositoryClient` objet en utilisant son constructeur et en transmettant un `ServiceClientFactory` objet contenant des propriétés de connexion.

1. Récupérer la ressource à mettre à jour

   Spécifiez l’URI de la ressource pour récupérer et lire la ressource. Dans cet exemple, l’URI de la ressource est `"/testFolder/testResource"`.

1. Mettre à jour la ressource

   Mettez à jour les informations de l’ `Resource` objet. Dans cet exemple, pour mettre à jour la description, appelez la `Resource` `setDescription` méthode de l’objet et transmettez la nouvelle chaîne de description en tant que paramètre.

   Appelez ensuite la `ServiceClientFactory` `updateResource` méthode de l’objet, puis transmettez les paramètres suivants :

   * Objet `java.lang.String` contenant l’URI de la ressource.
   * Objet `Resource` contenant les informations de ressource mises à jour.
   * Valeur `boolean` indiquant si la version principale ou secondaire doit être mise à jour. Dans cet exemple, une valeur de `true` est transmise pour indiquer que la version majeure doit être incrémentée.

**Voir également**

[Mise à jour des ressources](aem-forms-repository.md#updating-resources)

[Démarrage rapide (mode SOAP) : Mise à jour d’une ressource à l’aide de l’API Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-updating-a-resource-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Mise à jour des ressources à l’aide de l’API de service Web {#update-resources-using-the-web-service-api}

Mettez à jour une ressource à l’aide de l’API Repository (service Web) :

1. Inclure les fichiers de projet

   * Créez un assembly client Microsoft .NET qui consomme le fichier WSDL du référentiel.
   * Référencez l&#39;assembly client Microsoft .NET.

1. Création du client de service

   A l&#39;aide de l&#39;assembly client Microsoft .NET, créez un `RepositoryServiceService` objet en appelant son constructeur par défaut. Définissez sa `Credentials` propriété à l’aide d’un `System.Net.NetworkCredential` objet contenant le nom d’utilisateur et le mot de passe.

1. Récupérer la ressource à mettre à jour

   Spécifiez l’URI de la ressource à récupérer et lisez-la. Dans cet exemple, l’URI de la ressource est `"/testFolder/testResource"`. Pour plus d’informations, voir [Lecture des ressources](aem-forms-repository.md#reading-resources).

1. Mettre à jour la ressource

   Mettez à jour les informations de l’ `Resource` objet. Dans cet exemple, pour mettre à jour la description, affectez une nouvelle valeur au champ de l’ `Resource` objet `description` .

1. Appelez la méthode `RepositoryServiceService` `updateResource` de l’objet et transmettez les paramètres suivants :

   * Objet `System.String` contenant l’URI de la ressource.
   * Objet `Resource` contenant les informations de ressource mises à jour.
   * Valeur `boolean` indiquant si la version principale ou secondaire doit être mise à jour. Dans cet exemple, une valeur de `true` est transmise pour indiquer que la version majeure doit être incrémentée.
   * Transmettez `null` les deux paramètres restants.

**Voir également**

[Mise à jour des ressources](aem-forms-repository.md#updating-resources)

[Appel d’AEM Forms à l’aide du codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## Recherche de ressources {#searching-for-resources}

Vous pouvez créer des requêtes utilisées pour rechercher des ressources dans le référentiel, y compris l’historique, les ressources connexes et les propriétés.

Vous pouvez récupérer des ressources connexes afin de déterminer les dépendances entre un formulaire et ses fragments. Par exemple, si vous disposez d’un formulaire, vous pouvez déterminer les fragments ou les ressources externes qu’il utilise. Si vous disposez d’une image, vous pouvez également savoir quels formulaires utilisent cette image. Vous pouvez également rechercher des ressources connexes à l’aide du filtrage basé sur les propriétés. Vous pouvez, par exemple, rechercher toutes les images utilisées par un formulaire portant un nom spécifique ou rechercher toutes les images utilisées par un formulaire portant un nom spécifique. Vous pouvez également effectuer des recherches à l’aide des propriétés de ressource. Par exemple, vous pouvez lancer une requête pour rechercher tous les formulaires ou ressources dont le nom commence par une chaîne donnée qui peut inclure des caractères génériques &quot;%&quot; et &quot;_&quot;. N&#39;oubliez pas que les recherches basées sur les propriétés ne sont pas basées sur les relations ; ces recherches reposent sur l’hypothèse que vous connaissez une ressource donnée.

**Instructions de requête**

Une *requête* contient une ou plusieurs instructions qui sont logiquement jointes avec des conditions. Une *instruction* se compose d’un opérande de gauche, d’un opérateur et d’un opérande de droite. En outre, vous pouvez spécifier l’ordre de tri à utiliser pour les résultats de la recherche. L’ordre *de* tri contient des informations équivalentes à une `ORDER BY` clause SQL et comprend des éléments qui contiennent les attributs sur lesquels la recherche a été basée, ainsi qu’une valeur indiquant si l’ordre croissant ou décroissant doit être utilisé.

Vous pouvez rechercher des ressources par programmation à l’aide de l’API Java du service Repository. Actuellement, il n’est pas possible d’utiliser l’API du service Web pour rechercher des ressources.

**Comportement de tri**

L’ordre de tri n’est pas respecté lors de l’appel de la `ResourceRepositoryClient` `searchProperties` méthode de l’objet et de la spécification d’un ordre de tri. Supposons, par exemple, que vous créiez une ressource avec trois propriétés personnalisées, où les noms d’attribut sont `name`, `secondName`et `asecondName`. Vous créez ensuite un élément d’ordre de tri sur le nom de l’attribut et définissez la `ascending` valeur sur `true`.

Ensuite, vous appelez la méthode `ResourceRepositoryClient` `searchProperties` de l’objet et passez dans l’ordre de tri. La recherche renvoie la ressource appropriée, avec les trois propriétés. Toutefois, les propriétés ne sont pas triées par nom d’attribut. Ils sont renvoyés dans l’ordre dans lequel ils ont été ajoutés : `name`, `secondName`et `asecondName`.

>[!NOTE]
>
>For more information about the Repository service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary_of_steps-5}

Pour rechercher des ressources, procédez comme suit :

1. Incluez des fichiers de projet.
1. Créez un client de service Repository.
1. Spécifiez le dossier cible pour la recherche.
1. Spécifiez les attributs utilisés dans la recherche.
1. Créez la requête utilisée dans la recherche.
1. Créez l’ordre de tri des résultats de la recherche.
1. Recherchez les ressources.
1. Récupérez les ressources des résultats de la recherche.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, incluez les fichiers proxy.

**Création du client de service**

Avant de pouvoir lire une ressource par programmation, vous devez établir une connexion et fournir des informations d’identification. Pour ce faire, vous devez créer un client de service.

**Spécifier le dossier cible pour la recherche**

Créez une chaîne contenant le chemin de base à partir duquel effectuer la recherche. La syntaxe comprend des barres obliques, comme dans cet exemple : &quot;/*path*/*folder*&quot;.

**Spécifier les attributs utilisés dans la recherche**

Vous pouvez baser votre recherche sur les attributs contenus dans les ressources. Spécifiez les valeurs des attributs sur lesquels effectuer la recherche.

**Créer la requête utilisée dans la recherche**

Créez une requête à l’aide d’instructions et de conditions. Chaque instruction spécifie l’attribut sur lequel baser la recherche, la condition à utiliser et la valeur d’attribut à utiliser dans la recherche.

**Création de l&#39;ordre de tri des résultats de la recherche**

L’ordre de tri est composé d’éléments, chacun d’eux contenant l’un des attributs utilisés dans la recherche et une valeur indiquant si l’ordre croissant ou décroissant doit être utilisé.

**Rechercher les ressources**

Recherchez les ressources à l’aide du dossier, de la requête et de l’ordre de tri. En outre, indiquez la profondeur de la recherche et une limite supérieure du nombre de résultats à renvoyer.

**Récupérer les ressources des résultats de la recherche**

Effectuez une itération dans la liste des ressources renvoyées et extrayez les informations pour un traitement ultérieur.

**Voir également**

[Rechercher des ressources à l’aide de l’API Java](aem-forms-repository.md#search-for-resources-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Démarrage rapide de l’API Repository Service](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Rechercher des ressources à l’aide de l’API Java {#search-for-resources-using-the-java-api}

Recherchez une ressource à l’aide de l’API du service Repository (Java) :

1. Inclure les fichiers de projet

   Incluez les fichiers JAR client dans le chemin de classe de votre projet Java.

1. Création du client de service

   Créez un `ResourceRepositoryClient` objet en utilisant son constructeur et en transmettant un `ServiceClientFactory` objet contenant des propriétés de connexion.

1. Spécifier le dossier cible pour la recherche

   Spécifiez l’URI du chemin de base à partir duquel exécuter la recherche. Dans cet exemple, l’URI de la ressource est `/testFolder`.

1. Spécifier les attributs utilisés dans la recherche

   Spécifiez les valeurs des attributs sur lesquels effectuer la recherche. Les attributs existent dans un `com.adobe.repository.infomodel.bean.Resource` objet. Dans cet exemple, la recherche sera effectuée sur l&#39;attribut name; par conséquent, un `java.lang.String` contenant le nom de l’ `Resource` objet est utilisé, `testResource` dans ce cas.

1. Créer la requête utilisée dans la recherche

   Pour créer une requête, créez un `com.adobe.repository.query.Query` objet en appelant le constructeur par défaut de la `Query` classe et ajoutez des instructions à la requête.

   Pour créer une instruction, appelez le constructeur de la `com.adobe.repository.query.Query.Statement` classe et transmettez les paramètres suivants :

   * Opérande de gauche contenant la constante d’attribut de ressource. Dans cet exemple, puisque le nom de la ressource est utilisé comme base de la recherche, la valeur statique `Resource.ATTRIBUTE_NAME` est utilisée.
   * Opérateur contenant la condition utilisée dans la recherche de l’attribut. L&#39;opérateur doit être l&#39;une des constantes statiques de la `Query.Statement` classe. Dans cet exemple, la valeur statique `Query.Statement.OPERATOR_BEGINS_WITH` est utilisée.
   * opérande de droite contenant la valeur d’attribut sur laquelle effectuer la recherche. Dans cet exemple, l’attribut name, `String` contenant la valeur `"testResource"`, est utilisé.
   Spécifiez l’espace de noms de l’opérande de gauche en appelant la `Query.Statement` méthode de l’objet et en transmettant l’une des valeurs statiques contenues dans la `setNamespace` `com.adobe.repository.infomodel.bean.ResourceProperty` classe. Dans cet exemple, `ResourceProperty.RESERVED_NAMESPACE_REPOSITORY` est utilisé.

   Ajoutez chaque instruction à la requête en appelant la `Query` méthode de l’objet et en transmettant l’ `addStatement` `Query.Statement` objet.

1. Création de l&#39;ordre de tri des résultats de la recherche

   Pour spécifier l’ordre de tri utilisé dans les résultats de la recherche, créez un `com.adobe.repository.query.sort.SortOrder` objet en appelant le constructeur par défaut de la `SortOrder` classe, puis ajoutez des éléments à l’ordre de tri.

   Pour créer un élément pour l’ordre de tri, appelez l’un des constructeurs de la `com.adobe.repository.query.sort.SortOrder.Element` classe. Dans cet exemple, puisque le nom de la ressource est utilisé comme base de la recherche, la valeur statique `Resource.ATTRIBUTE_NAME` est utilisée comme premier paramètre et l’ordre croissant ( `boolean` valeur de `true`) est spécifié comme second paramètre.

   Ajoutez chaque élément à l’ordre de tri en appelant la `SortOrder` méthode de l’objet et en transmettant l’ `addSortElement` `SortOrder.Element` objet.

1. Rechercher les ressources

   Pour effectuer une recherche `resources` en fonction des propriétés d’attribut, appelez la `ResourceRepositoryClient` `searchProperties` méthode de l’objet et transmettez les paramètres suivants :

   * Un `String` chemin de base à partir duquel exécuter la recherche. Dans ce cas, `"/testFolder"` est utilisé.
   * Requête utilisée dans la recherche.
   * Profondeur de la recherche. Dans ce cas, `com.adobe.repository.infomodel.bean.ResourceCollection.DEPTH_INFINITE` est utilisé pour indiquer que le chemin de base et tous ses dossiers doivent être utilisés.
   * Valeur `int` indiquant la première ligne à partir de laquelle sélectionner le jeu de résultats non paginé. Dans cet exemple, `0` est spécifié.
   * Valeur `int` indiquant le nombre maximal de résultats à renvoyer. Dans cet exemple, `10` est spécifié.
   * Ordre de tri utilisé dans la recherche.
   La méthode renvoie un `java.util.List` nombre d’ `Resource` objets dans l’ordre de tri spécifié.

1. Récupérer les ressources des résultats de la recherche

   Pour récupérer les ressources contenues dans le résultat de la recherche, effectuez une itération dans le fichier `List` et convertissez chaque objet en un `Resource` afin d’extraire ses informations. Dans cet exemple, le nom de chaque ressource est affiché.

**Voir également**

[Recherche de ressources](aem-forms-repository.md#searching-for-resources)

[Démarrage rapide (mode SOAP) : Recherche de ressources à l’aide de l’API Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-searching-for-resources-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Création de relations de ressources {#creating-resource-relationships}

Vous pouvez spécifier des relations entre les ressources dans le référentiel. Il existe trois types de relations :

* **Dépendance**: une relation dans laquelle une ressource dépend d’autres ressources, ce qui signifie que toutes les ressources connexes sont nécessaires dans le référentiel.
* **Appartenance (système de fichiers)**: relation dans laquelle une ressource se trouve dans un dossier donné.
* **Personnalisé**: une relation que vous spécifiez entre les ressources. Par exemple, si une ressource a été abandonnée et qu’une autre ressource a été introduite dans le référentiel, vous pouvez spécifier votre propre relation de remplacement.

Vous pouvez créer vos propres relations personnalisées. Par exemple, si vous stockez un fichier HTML dans le référentiel et qu’il utilise une image, vous pouvez spécifier une relation personnalisée pour relier le fichier HTML à l’image (puisque normalement, seuls les fichiers XML sont associés aux images à l’aide d’une relation de dépendance définie par le référentiel). Un autre exemple de relation personnalisée serait si vous vouliez créer une vue différente du référentiel avec une structure de graphique cyclique au lieu d&#39;une structure d&#39;arborescence. Vous pouvez définir un graphique circulaire avec une visionneuse pour parcourir ces relations. Enfin, vous pouvez indiquer qu’une ressource remplace une autre ressource, même si les deux ressources sont complètement différentes. Dans ce cas, vous pouvez définir un type de relation en dehors de la plage réservée et créer une relation entre ces deux ressources. Votre application serait le seul client à pouvoir détecter et traiter la relation, et elle pourrait être utilisée pour effectuer des recherches sur cette relation.

Vous pouvez par programmation définir des relations entre les ressources à l’aide de l’API Java du service Repository ou de l’API du service Web.

>[!NOTE]
>
>For more information about the Repository service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary_of_steps-6}

Pour définir une relation entre deux ressources, procédez comme suit :

1. Incluez des fichiers de projet.
1. Créez un client de service Repository.
1. Spécifiez les URI des ressources à lier.
1. Créez la relation.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, incluez les fichiers proxy.

**Création du client de service**

Avant de pouvoir lire une ressource par programmation, vous devez établir une connexion et fournir des informations d’identification. Pour ce faire, vous devez créer un client de service.

**Spécifiez les URI des ressources à lier.**

Créez des chaînes contenant les URI de la ressource à relier. La syntaxe comprend des barres obliques, comme dans cet exemple : &quot;/*path*/*resource*&quot;.

**Créer la relation**

Appelez la méthode du service Repository pour créer et spécifier le type de relation.

**Voir également**

[Création de ressources de relation à l’aide de l’API Java](aem-forms-repository.md#create-relationship-resources-using-the-java-api)

[Création de ressources de relation à l’aide de l’API de service Web](aem-forms-repository.md#create-relationship-resources-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Démarrage rapide de l’API Repository Service](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Création de ressources de relation à l’aide de l’API Java {#create-relationship-resources-using-the-java-api}

Créez des ressources de relation à l’aide de l’API Java du service Repository, effectuez les tâches suivantes :

1. Inclure les fichiers de projet

   Incluez les fichiers JAR client dans le chemin de classe de votre projet Java.

1. Création du client de service

   Créez un `ResourceRepositoryClient` objet en utilisant son constructeur et en transmettant un `ServiceClientFactory` objet contenant des propriétés de connexion.

1. Spécifiez les URI des ressources à lier.

   Spécifiez les URI des ressources à lier. Dans ce cas, étant donné que les ressources sont nommées `testResource1` et `testResource2` et se trouvent dans le dossier nommé `testFolder`, leurs URI sont `"/testFolder/testResource1"` et `"/testFolder/testResource2"`. Les URI sont stockés sous la forme d’ `java.lang.String` objets. Dans cet exemple, les ressources sont d’abord écrites dans le référentiel et leurs URI sont récupérés. Pour plus d’informations sur l’écriture d’une ressource, voir [Ecriture de ressources](aem-forms-repository.md#writing-resources).

1. Créer la relation

   Appelez la méthode `ResourceRepositoryClient` `createRelationship` de l’objet et transmettez les paramètres suivants :

   * URI de la ressource source.
   * URI de la ressource cible.
   * Type de relation, qui est l&#39;une des constantes statiques de la `com.adobe.repository.infomodel.bean.Relation` classe. Dans cet exemple, une relation de dépendance est établie en spécifiant la valeur `Relation.TYPE_DEPENDANT_OF`.
   * Valeur `boolean` indiquant si la ressource cible est automatiquement mise à jour vers l’identifiant `com.adobe.repository.infomodel.Id`basé de la nouvelle ressource principale. Dans cet exemple, en raison de la relation de dépendance, la valeur `true` est spécifiée.
   Vous pouvez également récupérer une liste de ressources connexes pour une ressource donnée en appelant la `ResourceRepositoryClient` `getRelated` méthode de l’objet et en transmettant les paramètres suivants :

   * URI de la ressource pour laquelle récupérer les ressources connexes. Dans cet exemple, la ressource source ( `"/testFolder/testResource1"`) est spécifiée.
   * Valeur `boolean` indiquant si la ressource spécifiée est la ressource source dans la relation. Dans cet exemple, la valeur `true` est spécifiée, car c’est le cas.
   * Type de relation, qui est l&#39;une des constantes statiques de la `Relation` classe. Dans cet exemple, une relation de dépendance est spécifiée en utilisant la même valeur utilisée précédemment : `Relation.TYPE_DEPENDANT_OF`.
   La `getRelated` méthode renvoie un `java.util.List` nombre d’objets `Resource` par le biais desquels vous pouvez effectuer une itération pour récupérer chacune des ressources connexes, en faisant passer les objets contenus dans le `List` à `Resource` tel quel. Dans cet exemple, `testResource2` il est prévu que les ressources renvoyées figurent dans la liste.

**Voir également**

[Création de relations de ressources](aem-forms-repository.md#creating-resource-relationships)

[Démarrage rapide (mode SOAP) : Création de relations entre les ressources à l’aide de l’API Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-creating-relationships-between-resources-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Création de ressources de relation à l’aide de l’API de service Web {#create-relationship-resources-using-the-web-service-api}

Créez des ressources de relation à l’aide de l’API Repository (service Web) :

1. Inclure les fichiers de projet

   * Créez un assembly client Microsoft .NET qui consomme le fichier WSDL du référentiel.
   * Référencez l&#39;assembly client Microsoft .NET.

1. Création du client de service

   A l&#39;aide de l&#39;assembly client Microsoft .NET, créez un `RepositoryServiceService` objet en appelant son constructeur par défaut. Définissez sa `Credentials` propriété à l’aide d’un `System.Net.NetworkCredential` objet contenant le nom d’utilisateur et le mot de passe.

1. Spécifiez les URI des ressources à lier.

   Spécifiez les URI des ressources à lier. Dans ce cas, étant donné que les ressources sont nommées `testResource1` et `testResource2` et se trouvent dans le dossier nommé `testFolder`, leurs URI sont `"/testFolder/testResource1"` et `"/testFolder/testResource2"`. Lorsque vous utilisez un langage compatible avec Microsoft .NET Framework (C#, par exemple), les URI sont stockés en tant qu’ `System.String` objets. Dans cet exemple, les ressources sont d’abord écrites dans le référentiel et leurs URI sont récupérés. Pour plus d’informations sur l’écriture d’une ressource, voir [Ecriture de ressources](aem-forms-repository.md#writing-resources).

1. Créer la relation

   Appelez la méthode `RepositoryServiceService` `createRelationship` de l’objet et transmettez les paramètres suivants :

   * URI de la ressource source.
   * URI de la ressource cible.
   * Type de relation. Dans cet exemple, une relation de dépendance est établie en spécifiant la valeur `3`.
   * Valeur `boolean` indiquant si le type de relation a été spécifié. Dans cet exemple, la valeur `true` est spécifiée.
   * Valeur `boolean` indiquant si la ressource cible est automatiquement mise à jour vers l’identifiant `Id`basé de la nouvelle ressource principale. Dans cet exemple, en raison de la relation de dépendance, la valeur `true` est spécifiée.
   * Valeur `boolean` indiquant si la tête cible a été spécifiée. Dans cet exemple, la valeur `true` est spécifiée.
   * Transmettez `null` le dernier paramètre.
   Vous pouvez également récupérer une liste de ressources connexes pour une ressource donnée en appelant la `RepositoryServiceService` `getRelated` méthode de l’objet et en transmettant les paramètres suivants :

   * URI de la ressource pour laquelle récupérer les ressources connexes. Dans cet exemple, la ressource source ( `"/testFolder/testResource1"`) est spécifiée.
   * Valeur `boolean` indiquant si la ressource spécifiée est la ressource source dans la relation. Dans cet exemple, la valeur `true` est spécifiée, car c’est le cas.
   * Valeur `boolean` indiquant si la ressource source a été spécifiée. Dans cet exemple, la valeur `true` est fournie.
   * Tableau d’entiers contenant les types de relations. Dans cet exemple, une relation de dépendance est spécifiée en utilisant la même valeur dans le tableau que celle utilisée précédemment : `3`.
   * Transmettez `null` les deux paramètres restants.
   La `getRelated` méthode renvoie un tableau d’objets pouvant être projetés vers `Resource` des objets à travers lesquels vous pouvez effectuer une itération pour récupérer chacune des ressources associées. Dans cet exemple, `testResource2` il est prévu que les ressources renvoyées figurent dans la liste.

**Voir également**

[Création de relations de ressources](aem-forms-repository.md#creating-resource-relationships)

[Appel d’AEM Forms à l’aide du codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## Verrouillage des ressources {#locking-resources}

Vous pouvez verrouiller une ressource ou un ensemble de ressources pour une utilisation exclusive par un utilisateur particulier ou pour une utilisation partagée entre plusieurs utilisateurs. Un verrou partagé est une indication que quelque chose va se passer avec la ressource, mais cela n&#39;empêche personne d&#39;autre de prendre des mesures avec cette ressource. Un verrou partagé doit être considéré comme un mécanisme de signalisation. Un verrou exclusif signifie que l’utilisateur qui a verrouillé la ressource va modifier la ressource, et le verrou garantit que personne d’autre ne peut le faire tant que l’utilisateur n’a plus besoin d’accéder à la ressource et a libéré le verrou. Si un administrateur de référentiel déverrouille une ressource, tous les verrous exclusifs et partagés de cette ressource seront automatiquement supprimés. Ce type d’action est destiné aux situations où un utilisateur n’est plus disponible et n’a pas déverrouillé la ressource.

Lorsqu’une ressource est verrouillée, une icône de verrouillage s’affiche lorsque vous affichez l’onglet Ressources situé dans Workbench, comme illustré ci-dessous.

![lr_lr_lockrepository](assets/lr_lr_lockrepository.png)

Vous pouvez contrôler par programmation l’accès aux ressources à l’aide de l’API Java du service Repository ou de l’API du service Web.

>[!NOTE]
>
>For more information about the Repository service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary_of_steps-7}

Pour verrouiller et déverrouiller des ressources, procédez comme suit :

1. Incluez des fichiers de projet.
1. Créez un client de service Repository.
1. Spécifiez l’URI de la ressource à verrouiller.
1. Verrouillez la ressource.
1. Récupérez les verrous de la ressource.
1. Déverrouiller la ressource

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, incluez les fichiers proxy.

**Création du client de service**

Avant de pouvoir lire une ressource par programmation, vous devez établir une connexion et fournir des informations d’identification. Pour ce faire, vous devez créer un client de service.

**Spécifiez l’URI de la ressource à verrouiller.**

Créez une chaîne contenant l’URI de la ressource à verrouiller. La syntaxe comprend des barres obliques, comme dans cet exemple : &quot;/*path*/*resource*&quot;.

**Verrouiller la ressource**

Appelez la méthode du service Repository pour verrouiller la ressource, en spécifiant l’URI, le type de verrouillage et la profondeur de verrouillage.

**Récupérer les verrous de la ressource**

Appelez la méthode du service Repository pour récupérer les verrous de la ressource, en spécifiant l’URI.

**Déverrouiller la ressource**

Appelez la méthode du service Repository pour déverrouiller la ressource, en spécifiant l’URI.

**Voir également**

[Verrouillage des ressources à l’aide de l’API Java](aem-forms-repository.md#lock-resources-using-the-java-api)

[Verrouillage des ressources à l’aide de l’API de service Web](aem-forms-repository.md#lock-resources-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Démarrage rapide de l’API Repository Service](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Verrouillage des ressources à l’aide de l’API Java {#lock-resources-using-the-java-api}

Verrouillez les ressources à l’aide de l’API du service Repository (Java) :

1. Inclure les fichiers de projet

   Incluez les fichiers JAR client dans le chemin de classe de votre projet Java.

1. Création du client de service

   Créez un `ResourceRepositoryClient` objet en utilisant son constructeur et en transmettant un `ServiceClientFactory` objet contenant des propriétés de connexion.

1. Spécifiez l’URI de la ressource à verrouiller.

   Spécifiez l’URI de la ressource à verrouiller. Dans ce cas, puisque la ressource nommée `testResource` se trouve dans le dossier nommé `testFolder`, son URI est `"/testFolder/testResource"`. L’URI est stocké sous la forme d’un `java.lang.String` objet.

1. Verrouiller la ressource

   Appelez la méthode `ResourceRepositoryClient` `lockResource` de l’objet et transmettez les paramètres suivants :

   * URI de la ressource.
   * L&#39;étendue de verrouillage. Dans cet exemple, étant donné que la ressource sera verrouillée pour une utilisation exclusive, l’étendue de verrouillage est spécifiée comme `com.adobe.repository.infomodel.bean.Lock.SCOPE_EXCLUSIVE`.
   * La profondeur de verrouillage. Dans cet exemple, étant donné que le verrouillage ne s&#39;applique qu&#39;à la ressource particulière et qu&#39;aucun de ses membres ou enfants ne l&#39;est, la profondeur de verrouillage est spécifiée comme `Lock.DEPTH_ZERO`.
   >[!NOTE]
   >
   >La version surchargée de la `lockResource` méthode qui requiert quatre paramètres renvoie une exception. Veillez à utiliser la `lockResource` méthode qui requiert trois paramètres, comme indiqué dans cette présentation.

1. Récupérer les verrous de la ressource

   Appelez la méthode `ResourceRepositoryClient` `getLocks` de l’objet et transmettez l’URI de la ressource en tant que paramètre. La méthode renvoie une liste d’objets Lock par lesquels vous pouvez effectuer une itération. Dans cet exemple, le propriétaire du verrou, la profondeur et la portée sont imprimés pour chaque objet en appelant respectivement les méthodes `getOwnerUserId`, `getDepth`et `getType` de l’objet Lock.

1. Déverrouiller la ressource

   Appelez la méthode `ResourceRepositoryClient` `unlockResource` de l’objet et transmettez l’URI de la ressource en tant que paramètre. Pour plus d’informations, voir le Guide de référence [de l’API](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)AEM Forms.

**Voir également**

[Verrouillage des ressources](aem-forms-repository.md#locking-resources)

[Démarrage rapide (mode SOAP) : Verrouillage d’une ressource à l’aide de l’API Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-locking-a-resource-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Verrouillage des ressources à l’aide de l’API de service Web {#lock-resources-using-the-web-service-api}

Verrouillez les ressources à l’aide de l’API du service de référentiel (service Web) :

1. Inclure les fichiers de projet

   * Créez un assembly client Microsoft .NET qui consomme le fichier WSDL du référentiel à l&#39;aide de Base64.
   * Référencez l&#39;assembly client Microsoft .NET.

1. Création du client de service

   A l&#39;aide de l&#39;assembly client Microsoft .NET, créez un `RepositoryServiceService` objet en appelant son constructeur par défaut. Définissez sa `Credentials` propriété à l’aide d’un `System.Net.NetworkCredential` objet contenant le nom d’utilisateur et le mot de passe.

1. Spécifiez l’URI de la ressource à verrouiller.

   Spécifiez une chaîne contenant l’URI de la ressource à verrouiller. Dans ce cas, puisque la ressource nommée `testResource` se trouve dans le dossier `testFolder`, son URI est `"/testFolder/testResource"`. Lorsque vous utilisez un langage compatible avec Microsoft .NET Framework (C#, par exemple), stockez l’URI dans un `System.String` objet.

1. Verrouiller la ressource

   Appelez la méthode `RepositoryServiceService` `lockResource` de l’objet et transmettez les paramètres suivants :

   * URI de la ressource.
   * L&#39;étendue de verrouillage. Dans cet exemple, étant donné que la ressource sera verrouillée pour une utilisation exclusive, l’étendue de verrouillage est spécifiée comme `11`.
   * La profondeur de verrouillage. Dans cet exemple, étant donné que le verrouillage ne s&#39;applique qu&#39;à la ressource particulière et qu&#39;aucun de ses membres ou enfants ne l&#39;est, la profondeur de verrouillage est spécifiée comme `2`.
   * Valeur `int` indiquant le nombre de secondes avant l’expiration du verrou. Dans cet exemple, la valeur de `1000` est utilisée.
   * Transmettez `null` le dernier paramètre.

1. Récupérer les verrous de la ressource

   Appelez la méthode `RepositoryServiceService` de l’objet et transmettez l’URI de la ressource comme premier paramètre et `getLocks` `null` pour le second paramètre. La méthode renvoie un `object` tableau contenant `Lock` des objets à travers lesquels vous pouvez effectuer une itération. Dans cet exemple, le propriétaire du verrouillage, la profondeur et la portée sont imprimés pour chaque objet en accédant respectivement aux champs `Lock` , `ownerUserId`et `depth``type` de chaque objet.

1. Déverrouiller la ressource

   Appelez la méthode `RepositoryServiceService` de l’objet et transmettez l’URI de la ressource comme premier paramètre et `unlockResource` `null` pour le second paramètre.

**Voir également**

[Verrouillage des ressources](aem-forms-repository.md#locking-resources)

[Appel d’AEM Forms à l’aide du codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## Suppression de ressources {#deleting-resources}

Vous pouvez supprimer par programmation des ressources d’un emplacement donné dans le référentiel à l’aide de l’API Java (SOAP) du service Repository.

Lorsque vous supprimez une ressource, la suppression est normalement permanente, bien que, dans certains cas, les référentiels ECM stockent les versions de la ressource selon leurs mécanismes d’historique. Par conséquent, lors de la suppression d’une ressource, il est important de s’assurer que vous n’aurez plus jamais besoin de cette ressource. La suppression d’une ressource s’explique généralement par la nécessité d’augmenter l’espace disponible dans la base de données. Vous pouvez supprimer une version d’une ressource, mais si vous le faites, vous devez spécifier l’identifiant de la ressource, et non son identifiant logique (LID) ou son chemin d’accès. Si vous supprimez un dossier, tous ses éléments, y compris les sous-dossiers et les ressources, seront automatiquement supprimés.

Les ressources connexes ne sont pas supprimées. Si, par exemple, vous disposez d’un formulaire qui utilise le fichier logo.gif et que vous supprimez logo.gif, une relation est stockée dans le tableau des relations en attente. En cas d’abandon de version, définissez l’état de l’objet de la dernière version sur désapprouvé.

Une opération de suppression n’est pas sécurisée pour les transactions dans les systèmes ECM. Par exemple, si vous tentez de supprimer 100 ressources et que l’opération échoue sur la 50e ressource, les 49 premières instances seront supprimées, mais pas les autres. Sinon, le comportement par défaut est la restauration (non-engagement).

>[!NOTE]
>
>Lors de l’utilisation de la `com.adobe.repository.bindings.dsc.client.ResourceRepositoryClient.deleteResources()` méthode avec le référentiel ECM (EMC Documentum Content Server et IBM FileNet P8 Content Manager), la transaction ne sera pas annulée si la suppression échoue pour l’une des ressources spécifiées, ce qui signifie que les fichiers supprimés ne peuvent pas être annulés.

>[!NOTE]
>
>For more information about the Repository service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary_of_steps-8}

Pour supprimer une ressource, procédez comme suit :

1. Incluez des fichiers de projet.
1. Créez un client de service Repository.
1. Spécifiez l’URI de la ressource à supprimer.
1. Supprimez la ressource.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, incluez les fichiers proxy.

**Création du client de service**

Avant de pouvoir lire une ressource par programmation, vous devez établir une connexion et fournir des informations d’identification. Pour ce faire, vous devez créer un client de service.

**Spécifiez l&#39;URI de la ressource à supprimer.**

Créez une chaîne contenant l’URI de la ressource à supprimer. La syntaxe comprend des barres obliques, comme dans cet exemple : &quot;/*path*/*resource*&quot;. Si la ressource à supprimer est un dossier, la suppression est récursive.

**Supprimer la ressource**

Appelez la méthode du service Repository pour supprimer la ressource, en spécifiant l’URI.

**Voir également**

[Suppression de ressources à l’aide de l’API Java](aem-forms-repository.md#delete-resources-using-the-java-api-soap)

[Suppression de ressources à l’aide de l’API de service Web](aem-forms-repository.md#delete-resources-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Démarrage rapide de l’API Repository Service](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Suppression de ressources à l’aide de l’API Java (SOAP) {#delete-resources-using-the-java-api-soap}

Supprimez une ressource à l’aide de l’API Repository (Java) :

1. Inclure les fichiers de projet

   Incluez les fichiers JAR client dans le chemin de classe de votre projet Java.

1. Création du client de service

   Créez un `ResourceRepositoryClient` objet en utilisant son constructeur et en transmettant un `ServiceClientFactory` objet contenant des propriétés de connexion.

1. Spécifiez l&#39;URI de la ressource à supprimer.

   Spécifiez l’URI de la ressource à récupérer. Dans ce cas, puisque la ressource nommée testResourceToBeDeleted se trouve dans le dossier appelé testFolder, son URI est `/testFolder/testResourceToBeDeleted`. L’URI est stocké sous la forme d’un `java.lang.String` objet. Dans cet exemple, la ressource est d’abord écrite dans le référentiel et son URI est récupéré. Pour plus d’informations sur l’écriture d’une ressource, voir [Ecriture de ressources](aem-forms-repository.md#writing-resources).

1. Supprimer la ressource

   Appelez la méthode `ResourceRepositoryClient` `deleteResource` de l’objet et transmettez l’URI de la ressource en tant que paramètre.

**Voir également**

[Suppression de ressources](aem-forms-repository.md#deleting-resources)

[Démarrage rapide (mode SOAP) : Recherche de ressources à l’aide de l’API Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-searching-for-resources-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Suppression de ressources à l’aide de l’API de service Web {#delete-resources-using-the-web-service-api}

Supprimez une ressource à l’aide de l’API Repository (service Web) :

1. Inclure les fichiers de projet

   * Créez un assembly client Microsoft .NET qui consomme le fichier WSDL du référentiel à l&#39;aide de Base64.
   * Référencez l&#39;assembly client Microsoft .NET.

1. Création du client de service

   A l&#39;aide de l&#39;assembly client Microsoft .NET, créez un `RepositoryServiceService` objet en appelant son constructeur par défaut. Définissez sa `Credentials` propriété à l’aide d’un `System.Net.NetworkCredential` objet contenant le nom d’utilisateur et le mot de passe.

1. Spécifiez l&#39;URI de la ressource à supprimer.

   Spécifiez l’URI de la ressource à récupérer. Dans ce cas, puisque la ressource nommée `testResourceToBeDeleted` se trouve dans le dossier nommé `testFolder`, son URI est `"/testFolder/testResourceToBeDeleted"`. Dans cet exemple, la ressource est d’abord écrite dans le référentiel et son URI est récupéré. Pour plus d’informations sur l’écriture d’une ressource, voir [Ecriture de ressources](aem-forms-repository.md#writing-resources).

1. Supprimer la ressource

   Appelez la `RepositoryServiceService` méthode de l’objet et transmettez un `deleteResources` `System.String` tableau contenant l’URI de la ressource comme premier paramètre. Transmettez `null` le second paramètre.

**Voir également**

[Suppression de ressources](aem-forms-repository.md#deleting-resources)

[Appel d’AEM Forms à l’aide du codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
