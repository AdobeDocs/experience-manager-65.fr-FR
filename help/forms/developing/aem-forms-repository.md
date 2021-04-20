---
title: Utilisation du référentiel AEM Forms
seo-title: Utilisation du référentiel AEM Forms
description: Gérez le référentiel AEM Forms pour créer des dossiers, écrire, liste, lire, mettre à jour et rechercher des ressources à l’aide de l’API Java et de l’API de service Web. En outre, apprenez comment créer des relations de ressources, verrouiller et supprimer des ressources.
seo-description: Gérez le référentiel AEM Forms pour créer des dossiers, écrire, liste, lire, mettre à jour des ressources et rechercher des ressources à l’aide de l’API Java et de l’API de service Web. En outre, apprenez comment créer des relations de ressources, verrouiller et supprimer des ressources.
uuid: 6ead49f9-ca0d-4ee4-86a6-0a9ced6ec4f8
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: d2c95881-6c02-4e34-85af-84607df54287
role: Developer
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '9158'
ht-degree: 2%

---


# Utilisation du référentiel AEM Forms {#working-with-aem-forms-repository}

**Les exemples et exemples de ce document ne concernent que l’environnement AEM Forms on JEE.**

**A propos du service Repository**

Le service Repository fournit des services d’enregistrement de ressources et de gestion à AEM Forms. Lorsque les développeurs créent une application *AEM Forms*, ils peuvent déployer les actifs dans le référentiel au lieu du système de fichiers. Les actifs peuvent être constitués de formulaires XML, de formulaires PDF (y compris de formulaires Acrobat), de fragments de formulaire, d’images, de profils, de stratégies, de fichiers SWF, DDX et WSDL, de schémas XML et de données de test.

Par exemple, considérez l’application Forms suivante nommée *Applications/FormsApplication* :

![ww_ww_formrepository](assets/ww_ww_formrepository.png)

Notez qu’un fichier nommé Loan.xdp se trouve dans FormsFolder. Pour accéder à cette conception de formulaire, vous spécifiez le chemin d’accès complet (y compris la version) : `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.

>[!NOTE]
>
>Pour plus d’informations sur la création d’une application Forms à l’aide de Workbench, voir [Aide de Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).

Le chemin d&#39;accès à une ressource située dans le référentiel AEM Forms est :

`Applications/Application-name/Application-version/Folder.../Filename`

Les valeurs suivantes présentent quelques exemples de valeurs URI :

* Applications/AppraisalReport/1.0/Forms/FullForm.xdp
* Applications/AnotherApp/1.1/Assets/picture.jpg
* Applications/SomeApp/2.0/Resources/Data/XSDs/MyData.xsd

>[!NOTE]
>
>Vous pouvez parcourir le référentiel AEM Forms à l’aide d’un navigateur Web. Pour parcourir le référentiel, saisissez l’URL suivante dans un navigateur Web `https://[server name]:[server port]/repository`. Vous pouvez vérifier rapidement les résultats des débuts associés à la section Utilisation du référentiel AEM Forms à l’aide d’un navigateur Web. Par exemple, si vous ajoutez du contenu au référentiel AEM Forms, vous pouvez afficher le contenu dans un navigateur Web. (Voir [Début rapide (mode SOAP) : Ecriture d’une ressource à l’aide de l’API Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-writing-a-resource-using-the-java-api).)

L’API du référentiel fournit un certain nombre d’opérations que vous pouvez utiliser pour stocker et récupérer des informations du référentiel. Par exemple, vous pouvez obtenir une liste de ressources ou récupérer des ressources spécifiques stockées dans le référentiel lorsqu’une ressource est nécessaire dans le cadre du traitement d’une application.

>[!NOTE]
>
>L’API du référentiel ne peut pas être utilisée pour interagir avec Content Services (obsolète). Pour interagir avec Content Services (obsolète), vous utilisez l’API de gestion de Document.

A l’aide de l’API du service Repository, vous pouvez effectuer les tâches suivantes :

* Création de dossiers. Voir [Création de dossiers](aem-forms-repository.md#creating-folders).
* Écrivez des ressources et leurs propriétés. Voir [Writing Resources](aem-forms-repository.md#writing-resources).
* Liste des ressources d’une collection donnée ou liées à d’autres ressources. Voir [Liste des ressources](aem-forms-repository.md#listing-resources).
* Lisez les ressources et leurs propriétés. Voir [Reading Resources](aem-forms-repository.md#reading-resources).
* Mettez à jour les ressources et leurs propriétés. Voir [Mise à jour des ressources](aem-forms-repository.md#updating-resources).
* Rechercher des ressources, y compris leur historique, les ressources connexes et leurs propriétés. Voir [Recherche de ressources](aem-forms-repository.md#searching-for-resources).
* Spécifiez les relations entre les ressources. Voir [Création de relations de ressources](aem-forms-repository.md#creating-resource-relationships).
* Gérez le contrôle d&#39;accès des ressources, y compris le verrouillage et le déverrouillage des ressources, ainsi que la lecture et l&#39;écriture de listes de contrôle d&#39;accès (ACL). Voir [Verrouillage des ressources](aem-forms-repository.md#locking-resources).
* Supprimer les ressources et leurs propriétés. Voir [Suppression de ressources](aem-forms-repository.md#deleting-resources).

>[!NOTE]
>
>A l’aide de l’API du référentiel, vous ne pouvez pas gérer le contrôle d&#39;accès des ressources, rechercher des ressources ou spécifier des relations de ressources à l’aide d’un référentiel ECM.

>[!NOTE]
>
>Lorsqu’un fichier PDF chiffré est écrit dans le référentiel, la fonction d’extraction des relations automatisée ne peut pas être utilisée. Sinon, un fichier PDF chiffré peut être stocké dans le référentiel et récupéré ultérieurement. Le récupérateur peut choisir de déchiffrer le PDF après l’avoir récupéré dans le référentiel.

>[!NOTE]
>
>Pour plus d’informations sur le service Repository, voir [Guide de référence des services pour AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Création de dossiers {#creating-folders}

Les dossiers (collections de ressources) servent à stocker des objets (fichiers ou ressources) dans des regroupements organisés. Les dossiers peuvent contenir des ressources et d&#39;autres dossiers, également appelés sous-dossiers. Les ressources ne peuvent être stockées que dans un dossier à la fois.

Les fichiers héritent des listes de contrôle d&#39;accès (ACL) des dossiers et les sous-dossiers héritent des ACL de leurs dossiers parents. Par conséquent, les dossiers parents doivent exister avant que vous puissiez créer des dossiers enfants. L&#39;IDE vous permet d&#39;interagir uniquement dossier par dossier, et non fichier par fichier. Vous ne pouvez pas modifier les dossiers de version et il n’est pas nécessaire de le faire ; un dossier ne contient pas de données lui-même. Il ne s&#39;agit plutôt que d&#39;un conteneur de ressources contenant des données. La liste de contrôle d’accès par défaut est une autorisation de niveau système, ce qui signifie que les utilisateurs doivent disposer d’autorisations de niveau système (lecture, écriture, traversée, gestion des listes de contrôle d’accès) jusqu’à ce que quelqu’un leur accorde des autorisations pour un dossier particulier. Les listes ACL ne fonctionnent que dans l&#39;IDE.

>[!NOTE]
>
>Pour plus d’informations sur le service Repository, voir [Guide de référence des services pour AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary-of-steps}

Pour créer un dossier, procédez comme suit :

1. Incluez des fichiers de projet.
1. Créez le client de service.
1. Créez le dossier.
1. Enregistrez le dossier dans le référentiel.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, incluez les fichiers proxy.

**Créer le client de service**

Avant de pouvoir créer par programmation une collecte de ressources, vous devez établir une connexion et fournir des informations d’identification. Pour ce faire, vous devez créer un client de service.

**Création du dossier**

Appelez la méthode du service Repository pour créer la collecte de ressources et renseigner la collecte de ressources avec des informations d&#39;identification, y compris son UUID, son nom de dossier et sa description.

**Écrire le dossier dans le référentiel**

Appelez la méthode du service Repository pour écrire la collection de ressources, en spécifiant l’URI du dossier de cible.

**Voir également**

[Création de dossiers à l’aide de l’API Java](aem-forms-repository.md#create-folders-using-the-java-api)

[Création de dossiers à l’aide de l’API du service Web](aem-forms-repository.md#create-folders-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Débuts rapides de l’API Repository Service](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Création de dossiers à l’aide de l’API Java {#create-folders-using-the-java-api}

Créez un dossier à l’aide de l’API du service de référentiel (Java) :

1. Inclure les fichiers de projet

   Incluez des fichiers de projet dans le chemin de classe de votre projet Java.

1. Créer le client de service

   Créez un objet `ResourceRepositoryClient` en utilisant son constructeur et en transmettant un objet `ServiceClientFactory` contenant des propriétés de connexion.

1. Création du dossier

   Pour créer une collection de ressources, vous devez d&#39;abord créer un objet `com.adobe.repository.infomodel.bean.RepositoryInfomodelFactoryBean`.

   Appelez la méthode `newResourceCollection` de l’objet `repositoryInfomodelFactoryBean` et transmettez les paramètres suivants :

   * Identificateur UUID `com.adobe.repository.infomodel.Id` à affecter à la ressource.
   * Identificateur UUID `com.adobe.repository.infomodel.Lid` à affecter à la ressource.
   * `java.lang.String` contenant le nom de la collecte de ressources. Par exemple, `FormsFolder`.

   La méthode renvoie un objet `com.adobe.repository.infomodel.bean.ResourceCollection` représentant le nouveau dossier.

   Définissez la description du dossier à l’aide de la méthode `setDescription` et transmettez le paramètre suivant :

   * `String` qui décrit la collecte de ressources. Dans cet exemple, `"test Folder"` est utilisé `.`


1. Écrire le dossier dans le référentiel

   Appelez la méthode `ResourceRepositoryClient` de l’objet `writeResource` et transmettez l’URI du dossier et l’objet `ResourceCollection`. Par exemple, l’URI du dossier peut être la valeur suivante `/Applications/FormsApplication/1.0/`.

   La méthode renvoie une instance de l&#39;objet `com.adobe.repository.infomodel.bean.Resource` nouvellement créé. Vous pouvez, par exemple, récupérer la valeur d&#39;identificateur de la nouvelle ressource en appelant la méthode `com.adobe.repository.infomodel.bean.Resource` de l&#39;objet `getId`.

**Voir également**

[Création de dossiers](aem-forms-repository.md#creating-folders)

[Début rapide (mode SOAP) : Création d’un dossier à l’aide de l’API Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-creating-a-folder-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Création de dossiers à l’aide de l’API du service Web {#create-folders-using-the-web-service-api}

Créez un dossier à l’aide de l’API du service de référentiel (service Web) :

1. Inclure les fichiers de projet

   * Créez un assembly client Microsoft .NET qui consomme le fichier WSDL du référentiel à l&#39;aide de base64.
   * Référencez l&#39;assembly client Microsoft .NET.

1. Créer le client de service

   A l&#39;aide de l&#39;assembly client Microsoft .NET, créez un objet `RepositoryServiceService` en appelant son constructeur par défaut. Définissez sa propriété `Credentials` à l’aide d’un objet `System.Net.NetworkCredential` contenant le nom d’utilisateur et le mot de passe.

1. Création du dossier

   Créez le dossier en utilisant le constructeur par défaut pour la classe `ResourceCollection` et transmettez les paramètres suivants :

   * Un objet `Id`, créé en appelant le constructeur par défaut pour la classe `Id` et affecté au champ `id` de l&#39;objet `Resource`.
   * Un objet `Lid`, créé en appelant le constructeur par défaut pour la classe `Lid` et affecté au champ `lid` de l&#39;objet `Resource`.
   * Chaîne contenant le nom de la collection de ressources, qui est affectée au champ `Resource` de l&#39;objet `name`. Le nom utilisé dans cet exemple est `"testfolder"`.
   * Chaîne contenant la description de la collection de ressources, qui est affectée au champ `Resource` de l&#39;objet `description`. La description utilisée dans cet exemple est `"test folder"`.

1. Écrire le dossier dans le référentiel

   Appelez la méthode `writeResource` de l’objet `RepositoryServiceService` et transmettez les paramètres suivants :

   * Chemin d’accès à l’emplacement de création du dossier.
   * Objet `ResourceCollection` représentant le dossier.
   * Transmettez `null` pour les deux autres paramètres.

**Voir également**

[Création de dossiers](aem-forms-repository.md#creating-folders)

[Appel de AEM Forms à l’aide du codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## Ecriture de ressources {#writing-resources}

Vous pouvez créer des ressources à un emplacement donné dans le référentiel. La taille de fichier naturelle est soumise à des restrictions de base de données et de délai d’expiration de session. Pour la configuration par défaut, les fichiers sont limités à 25 Mo. Pour augmenter ou diminuer la taille maximale du fichier, vous devez modifier la configuration de la base de données.

L&#39;écriture de ressources équivaut à stocker des données dans le référentiel. Une fois que vous écrivez une ressource au référentiel, elle devient accessible à tous les clients de l&#39;écosystème du référentiel. Lorsque vous écrivez des ressources, telles que des schémas XML, des fichiers XDP et des fichiers XSD, dans le référentiel, le contenu est analysé en fonction du type MIME. Si le type MIME est pris en charge, l’analyseur détermine s’il existe une relation implicite avec un autre contenu. Par exemple, si une feuille de style en cascade (CSS) comporte une URL relative qui fait référence à une page CSS commune, il est prévu que vous envoyiez également la page CSS commune dans le référentiel. La relation entre les deux ressources est stockée en tant que relation en attente pour une période non ajustable de 30 jours. Lorsque vous envoyez la page CSS commune au référentiel au cours de la période de 30 jours, la relation est formée.

Lorsque vous créez une ressource, la liste de contrôle d&#39;accès (ACL) est héritée du dossier parent. Le dossier racine dispose d’autorisations au niveau du système jusqu’à la création d’une ressource ou d’un dossier initial, à ce moment-là, la ressource ou le dossier se voit attribuer des autorisations ACL par défaut.

Vous pouvez écrire des ressources par programmation en utilisant l’API Java du service Repository ou l’API du service Web.

>[!NOTE]
>
>Pour plus d’informations sur le service Repository, voir [Guide de référence des services pour AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary_of_steps-1}

Pour écrire une ressource, procédez comme suit :

1. Incluez des fichiers de projet.
1. Créez un client de service Repository.
1. Spécifiez l&#39;URI de la ressource à lire.
1. Lisez la ressource.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, incluez les fichiers proxy.

**Créer le client de service**

Avant de pouvoir lire une ressource par programmation, vous devez établir une connexion et fournir des informations d’identification. Pour ce faire, vous devez créer un client de service.

**Spécifiez l’URI du dossier de cible pour la ressource.**

Créez une chaîne contenant l&#39;URI de la ressource à lire. La syntaxe comprend des barres obliques verticales, comme dans cet exemple : &quot;/*chemin*/*dossier*&quot;.

**Créer la ressource**

Appelez la méthode du service Repository pour créer la ressource et renseignez la ressource avec des informations d&#39;identification, y compris son UUID, son nom de ressource et sa description.

**Spécifier le contenu de la ressource**

Appelez la méthode du service Repository pour créer du contenu de ressource et stocker ce contenu dans la ressource.

**Écrire la ressource dans le dossier cible**

Appelez la méthode du service Repository pour écrire la ressource, en spécifiant l’URI du dossier de cible.

**Voir également**

[Écrire des ressources à l’aide de l’API Java](aem-forms-repository.md#write-resources-using-the-java-api)

[Écrire des ressources à l’aide de l’API du service Web](aem-forms-repository.md#write-resources-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Débuts rapides de l’API Repository Service](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Écrire des ressources à l’aide de l’API Java {#write-resources-using-the-java-api}

Ecrivez une ressource à l’aide de l’API du service Repository (Java) :

1. Inclure les fichiers de projet

   Incluez les fichiers JAR client dans le chemin de classe de votre projet Java.

1. Créer le client de service

   Créez un objet `ResourceRepositoryClient` en utilisant son constructeur et en transmettant un objet `ServiceClientFactory` contenant des propriétés de connexion.

1. Spécifiez l’URI du dossier de cible pour la ressource.

   Spécifiez l&#39;URI du dossier de cible pour la ressource. Dans ce cas, puisque la ressource `testResource` sera stockée dans le dossier `testFolder`, l’URI du dossier est `"/testFolder"`. L&#39;URI est stocké en tant qu&#39;objet `java.lang.String`.

1. Créer la ressource

   Pour créer une ressource, vous devez d&#39;abord créer un objet `com.adobe.repository.infomodel.bean.RepositoryInfomodelFactoryBean`.

   Appelez la méthode `RepositoryInfomodelFactoryBean` de l&#39;objet `newResource`, qui crée un objet `com.adobe.repository.infomodel.bean.Resource`. Dans cet exemple, les paramètres suivants sont fournis :

   * Objet `com.adobe.repository.infomodel.Id`, créé en appelant le constructeur par défaut pour la classe `Id`.
   * Objet `com.adobe.repository.infomodel.Lid`, créé en appelant le constructeur par défaut pour la classe `Lid`.
   * `java.lang.String` contenant le nom de fichier de la ressource.

   Pour spécifier la description de la ressource, appelez la méthode `Resource` de l&#39;objet `setDescription` et transmettez une chaîne contenant la description. Dans cet exemple, la description est `"test resource"`.

1. Spécifier le contenu de la ressource

   Pour créer du contenu pour la ressource, appelez la méthode `RepositoryInfomodelFactoryBean` de l&#39;objet `newResourceContent`, qui renvoie un objet `com.adobe.repository.infomodel.bean.ResourceContent`. Ajoutez le contenu à l&#39;objet `ResourceContent`. Dans cet exemple, vous effectuez les tâches suivantes :

   * Appeler la méthode `ResourceContent` de l&#39;objet `setDataDocument` et transmettre un objet `com.adobe.idp.Document`
   * Appel de la méthode `setSize` de l&#39;objet `ResourceContent` et transmission de la taille en octets de l&#39;objet `Document`

   Ajoutez le contenu à la ressource en appelant la méthode `Resource` de l&#39;objet `setContent` et en transmettant l&#39;objet `ResourceContent`. Pour plus d’informations, voir [Référence de l’API AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. Écrire la ressource dans le dossier cible

   Appelez la méthode `ResourceRepositoryClient` de l’objet `writeResource` et transmettez l’URI du dossier, ainsi que l’objet `Resource`.

**Voir également**

[Ecriture de ressources](aem-forms-repository.md#writing-resources)

[Début rapide (mode SOAP) : Écriture d&#39;une ressource à l&#39;aide de l&#39;API Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-writing-a-resource-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Écrire des ressources à l’aide de l’API du service Web {#write-resources-using-the-web-service-api}

Ecrivez une ressource à l’aide de l’API du service de référentiel (service Web) :

1. Inclure les fichiers de projet

   * Créez un assembly client Microsoft .NET qui consomme le fichier WSDL du référentiel à l&#39;aide de base64.
   * Référencez l&#39;assembly client Microsoft .NET.

1. Créer le client de service

   A l&#39;aide de l&#39;assembly client Microsoft .NET, créez un objet `RepositoryServiceService` en appelant son constructeur par défaut. Définissez sa propriété `Credentials` à l’aide d’un objet `System.Net.NetworkCredential` contenant le nom d’utilisateur et le mot de passe.

1. Spécifiez l’URI du dossier de cible pour la ressource.

   Spécifiez l&#39;URI du dossier de cible pour la ressource. Dans ce cas, puisque la ressource `testResource` sera stockée dans le dossier `testFolder`, l’URI du dossier est `"/testFolder"`. Lorsque vous utilisez un langage compatible avec Microsoft .NET Framework (C#, par exemple), stockez l&#39;URI dans un objet `System.String`.

1. Créer la ressource

   Pour créer une ressource, appelez le constructeur par défaut pour la classe `Resource`. Dans cet exemple, les informations suivantes sont stockées dans l&#39;objet `Resource` :

   * Objet `com.adobe.repository.infomodel.Id`, créé en appelant le constructeur par défaut pour la classe `Id` et affecté au champ `id` de l&#39;objet `Resource`.
   * Objet `com.adobe.repository.infomodel.Lid`, créé en appelant le constructeur par défaut pour la classe `Lid` et affecté au champ `lid` de l&#39;objet `Resource`.
   * Chaîne contenant le nom de fichier de la ressource, qui est affectée au champ `Resource` de l&#39;objet `name`. Le nom utilisé dans cet exemple est `"testResource"`.
   * Chaîne contenant la description de la ressource, affectée au champ `Resource` de l&#39;objet `description`. La description utilisée dans cet exemple est `"test resource"`.

1. Spécifier le contenu de la ressource

   Pour créer du contenu pour la ressource, appelez le constructeur par défaut de la classe `ResourceContent`. Ajoutez ensuite du contenu à l’objet `ResourceContent`. Dans cet exemple, vous effectuez les tâches suivantes :

   * Affectation d&#39;un objet `BLOB` contenant un document au champ `ResourceContent` de l&#39;objet `dataDocument`.
   * Attribuer la taille en octets de l&#39;objet `BLOB` au champ `ResourceContent` de l&#39;objet `size`.

   Ajoutez le contenu à la ressource en attribuant l&#39;objet `ResourceContent` au champ `Resource` de l&#39;objet `content`.

1. Écrire la ressource dans le dossier cible

   Appelez la méthode `RepositoryServiceService` de l’objet `writeResource` et transmettez l’URI du dossier, ainsi que l’objet `Resource`. Transmettez `null` pour les deux autres paramètres.

**Voir également**

[Ecriture de ressources](aem-forms-repository.md#writing-resources)

[Appel de AEM Forms à l’aide du codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## Liste des ressources {#listing-resources}

Vous pouvez découvrir des ressources en répertoriant les ressources. Une requête est exécutée sur le référentiel pour rechercher toutes les ressources liées à une collecte de ressources donnée.

Une fois que vous avez organisé vos ressources, vous pouvez inspecter la structure que vous avez créée en voyant une branche particulière de la structure, comme vous le feriez dans un système d&#39;exploitation.

La liste des ressources fonctionne par relation : ressources sont membres de dossiers. L&#39;adhésion est représentée par une relation de type &quot;membre de&quot;. Lorsque vous liste des ressources dans un dossier donné, vous recherchez des ressources liées à un dossier donné par la relation &quot;membre de&quot;. Les relations sont directionnelles : un membre d&#39;une relation a une source qui est membre de la cible. La source est la ressource ; la cible est le dossier parent.

>[!NOTE]
>
>Pour plus d’informations sur le service Repository, voir [Guide de référence des services pour AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary_of_steps-2}

Pour liste des ressources, procédez comme suit :

1. Incluez des fichiers de projet.
1. Créez le client de service.
1. Spécifiez le chemin d’accès au dossier.
1. Récupérer la liste des ressources.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, incluez les fichiers proxy.

**Créer le client de service**

Avant de pouvoir créer par programmation une collecte de ressources, vous devez établir une connexion et fournir des informations d’identification. Pour ce faire, vous devez créer un client de service.

**Spécification du chemin d’accès au dossier**

Créez une chaîne contenant le chemin du dossier contenant les ressources. La syntaxe comprend des barres obliques verticales, comme dans cet exemple : &quot;/*chemin*/*dossier*&quot;.

**Récupérer la liste des ressources**

Appelez la méthode du service Repository pour récupérer la liste des ressources, en spécifiant le chemin d’accès du dossier cible.

**Voir également**

[Ressources de liste à l’aide de l’API Java](aem-forms-repository.md#list-resources-using-the-java-api)

[Ressources de liste à l’aide de l’API de service Web](aem-forms-repository.md#list-resources-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Débuts rapides de l’API Repository Service](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Ressources de liste à l’aide de l’API Java {#list-resources-using-the-java-api}

Liste des ressources à l’aide de l’API du service Repository (Java) :

1. Inclure les fichiers de projet

   Incluez les fichiers JAR client dans le chemin de classe de votre projet Java.

1. Créer le client de service

   Créez un objet `ResourceRepositoryClient` en utilisant son constructeur et en transmettant un objet `ServiceClientFactory` contenant des propriétés de connexion.

1. Spécification du chemin d’accès au dossier

   Spécifiez l&#39;URI de la collection de ressources à interroger. Dans ce cas, son URI est `"/testFolder"`. L&#39;URI est stocké en tant qu&#39;objet `java.lang.String`.

1. Récupérer la liste des ressources

   Appelez la méthode `ResourceRepositoryClient` de l’objet `listMembers` et transmettez l’URI du dossier.

   La méthode renvoie un `java.util.List` objet `com.adobe.repository.infomodel.bean.Resource` qui est la source d&#39;un `com.adobe.repository.infomodel.bean.Relation` de type `Relation.TYPE_MEMBER_OF` et dont l&#39;URI de collecte de ressources est la cible. Vous pouvez effectuer une itération dans `List` pour récupérer chacune des ressources. Dans cet exemple, le nom et la description de chaque ressource s&#39;affichent.

**Voir également**

[Liste des ressources](aem-forms-repository.md#listing-resources).

[Début rapide (mode SOAP) : Liste des ressources à l’aide de l’API Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-listing-resources-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Ressources de liste à l’aide de l’API de service Web {#list-resources-using-the-web-service-api}

Liste des ressources à l’aide de l’API du service de référentiel (service Web) :

1. Inclure les fichiers de projet

   * Créez un assembly client Microsoft .NET qui consomme le fichier WSDL du référentiel.
   * Référencez l&#39;assembly client Microsoft .NET.

1. Créer le client de service

   A l&#39;aide de l&#39;assembly client Microsoft .NET, créez un objet `RepositoryServiceService` en appelant son constructeur par défaut. Définissez sa propriété `Credentials` à l’aide d’un objet `System.Net.NetworkCredential` contenant le nom d’utilisateur et le mot de passe.

1. Spécification du chemin d’accès au dossier

   Spécifiez une chaîne contenant l’URI du dossier à interroger. Dans ce cas, son URI est `"/testFolder"`. Lorsque vous utilisez un langage compatible avec Microsoft .NET Framework (C#, par exemple), stockez l&#39;URI dans un objet `System.String`.

1. Récupérer la liste des ressources

   Appelez la méthode `RepositoryServiceService` de l’objet `listMembers` et transmettez l’URI du dossier en tant que premier paramètre. Transmettez `null` pour les deux autres paramètres.

   La méthode renvoie un tableau d&#39;objets pouvant être moulés dans des objets `Resource`. Vous pouvez effectuer une itération dans le tableau d&#39;objets pour récupérer chacune des ressources associées. Dans cet exemple, le nom et la description de chaque ressource s&#39;affichent.

**Voir également**

[Liste des ressources](aem-forms-repository.md#listing-resources).

[Appel de AEM Forms à l’aide du codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## Ressources de lecture {#reading-resources}

Vous pouvez récupérer des ressources à partir d’un emplacement donné dans le référentiel afin de lire leur contenu et leurs métadonnées. Le flux de travail est recto par un formulaire d’initialisation. Le processus dispose de toutes les autorisations nécessaires pour lire le formulaire. Le système récupère le formulaire de données et lit le contenu du référentiel. Le référentiel permet d&#39;accéder au contenu et aux métadonnées (la possibilité de connaître même la ressource).

Le référentiel possède les quatre types d&#39;autorisations suivants :

* **traverse** : vous permet de liste des ressources ; c&#39;est-à-dire, pour lire les métadonnées de ressources, mais pas le contenu de ressources
* **lire** : vous permet de lire le contenu des ressources
* **écrire** : vous permet d&#39;écrire du contenu de ressource
* **gestion des listes de contrôle d&#39;accès (ACL)** : permet de manipuler les listes de contrôle d&#39;accès sur les ressources

Les utilisateurs ne peuvent exécuter des processus que s’ils sont autorisés à exécuter le processus. Les utilisateurs IDE doivent parcourir et lire les autorisations pour se synchroniser avec le référentiel. Les listes de contrôle d’accès s’appliquent uniquement au moment de la conception, car l’exécution se produit dans le contexte du système.

Vous pouvez lire des ressources par programmation à l’aide de l’API Java du service Repository ou de l’API du service Web.

>[!NOTE]
>
>Pour plus d’informations sur le service Repository, voir [Guide de référence des services pour AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary_of_steps-3}

Pour lire une ressource, procédez comme suit :

1. Incluez des fichiers de projet.
1. Créez un client de service Repository.
1. Spécifiez l&#39;URI de la ressource à lire.
1. Lisez la ressource.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, incluez les fichiers proxy.

**Créer le client de service**

Avant de pouvoir lire une ressource par programmation, vous devez établir une connexion et fournir des informations d’identification. Pour ce faire, vous devez créer un client de service.

**Spécifiez l&#39;URI de la ressource à lire.**

Créez une chaîne contenant l&#39;URI de la ressource à lire. La syntaxe comprend des barres obliques verticales, comme dans cet exemple : &quot;/*chemin*/*ressource*&quot;.

**Lire la ressource**

Appelez la méthode du service Repository pour lire la ressource, en spécifiant l&#39;URI.

**Voir également**

[Lire les ressources à l’aide de l’API Java](aem-forms-repository.md#read-resources-using-the-java-api)

[Lecture des ressources à l’aide de l’API du service Web](aem-forms-repository.md#reading-resources-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Débuts rapides de l’API Repository Service](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Lire les ressources à l’aide de l’API Java {#read-resources-using-the-java-api}

Lisez une ressource à l’aide de l’API du service de référentiel (Java) :

1. Inclure les fichiers de projet

   Incluez les fichiers JAR client dans le chemin de classe de votre projet Java.

1. Créer le client de service

   Créez un objet `ResourceRepositoryClient` en utilisant son constructeur et en transmettant un objet `ServiceClientFactory` contenant des propriétés de connexion.

1. Spécifiez l&#39;URI de la ressource à lire.

   Spécifiez une valeur de chaîne qui représente l&#39;URI de la ressource à récupérer. Par exemple, en supposant que la ressource soit nommée *testResource* située dans un dossier nommé *testFolder*, spécifiez `/testFolder/testResource`.

1. Lire la ressource

   Appelez la méthode `ResourceRepositoryClient` de l&#39;objet `readResource` et transmettez l&#39;URI de la ressource en tant que paramètre. Cette méthode renvoie une instance `Resource` qui représente la ressource.

**Voir également**

[Ressources de lecture](aem-forms-repository.md#reading-resources)

[Début rapide (mode SOAP) : Lecture d&#39;une ressource à l&#39;aide de l&#39;API Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-reading-a-resource-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Lecture des ressources à l’aide de l’API du service Web {#reading-resources-using-the-web-service-api}

Lisez une ressource à l’aide de l’API du service de référentiel (service Web) :

1. Inclure les fichiers de projet

   * Créez un assembly client Microsoft .NET qui consomme le fichier WSDL du référentiel. (Voir [Création d&#39;un assembly client .NET utilisant l&#39;encodage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding).)
   * Référencez l&#39;assembly client Microsoft .NET. (Voir [Création d&#39;un assembly client .NET utilisant l&#39;encodage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding).)

1. Créer le client de service

   A l&#39;aide de l&#39;assembly client Microsoft .NET, créez un objet `RepositoryServiceService` en appelant son constructeur par défaut. Définissez sa propriété `Credentials` à l’aide d’un objet `System.Net.NetworkCredential` contenant le nom d’utilisateur et le mot de passe.

1. Spécifiez l&#39;URI de la ressource à lire.

   Spécifiez une chaîne contenant l&#39;URI de la ressource à récupérer. Dans ce cas, puisque la ressource `testResource` se trouve dans le dossier `testFolder`, son URI est `"/testFolder/testResource"`. Lorsque vous utilisez un langage compatible avec Microsoft .NET Framework (C#, par exemple), stockez l&#39;URI dans un objet `System.String`.

1. Lire la ressource

   Appelez la méthode `RepositoryServiceService` de l&#39;objet `readResource` et transmettez l&#39;URI de la ressource en tant que premier paramètre. Transmettez `null` pour les deux autres paramètres.

**Voir également**

[Ressources de lecture](aem-forms-repository.md#reading-resources)

[Appel de AEM Forms à l’aide du codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## Mise à jour des ressources {#updating-resources}

Vous pouvez récupérer et mettre à jour le contenu des ressources dans le référentiel. Lorsque vous mettez à jour des ressources, leur contrôle d&#39;accès reste inchangé entre les versions. Lors d’une mise à jour, vous avez la possibilité d’incrémenter la version principale. Si vous ne choisissez pas d’incrémenter la version majeure, la version mineure est automatiquement mise à jour.

Lorsque vous mettez à jour une ressource, la nouvelle version est créée en fonction des attributs de ressource spécifiés. Lorsque vous mettez à jour une ressource, vous spécifiez deux paramètres importants : l’URI de la cible et une instance de ressource contenant toutes les métadonnées mises à jour. Il est important de noter que si vous ne modifiez pas un attribut donné (par exemple, le nom), l’attribut est toujours requis dans l’instance que vous transmettez. Les relations créées lors de l’analyse du contenu sont ajoutées à la version spécifique et ne sont pas transférées, sauf indication contraire.

Par exemple, si vous mettez à jour un fichier XDP contenant des références à d’autres ressources, ces références supplémentaires seront également enregistrées. Supposons que form.xdp version 1.0 comporte deux références externes : un logo et une feuille de style, et vous mettez ensuite à jour le fichier form.xdp afin qu’il comporte maintenant trois références : un logo, une feuille de style et un fichier de schéma. Pendant la mise à jour, le référentiel ajoute la troisième relation (au fichier de schéma) à sa table de relations en attente. Une fois que le fichier de schéma est présent dans le référentiel, la relation est automatiquement formée. Cependant, si form.xdp version 2.0 n’utilise plus le logo, form.xdp version 2.0 n’aura pas de relation avec le logo.

Toutes les opérations de mise à jour sont atomiques et transactionnelles. Par exemple, si deux utilisateurs lisent la même ressource et décident tous deux de mettre à jour la version 1.0 vers la version 2.0, l’un d’eux réussira et l’autre échouera, l’intégrité du référentiel sera conservée et tous deux obtiendront un message confirmant la réussite ou l’échec. Si la transaction n’est pas validée, elle est restaurée en cas d’échec de la base de données et expire ou recule selon le serveur d’applications.

Vous pouvez mettre à jour les ressources par programmation en utilisant l’API Java du service Repository ou l’API du service Web.

>[!NOTE]
>
>Pour plus d’informations sur le service Repository, voir [Guide de référence des services pour AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary_of_steps-4}

Pour mettre à jour une ressource, procédez comme suit :

1. Incluez des fichiers de projet.
1. Créez un client de service Repository.
1. Récupérez la ressource à mettre à jour.
1. Mettez à jour la ressource.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, incluez les fichiers proxy.

**Créer le client de service**

Avant de pouvoir lire une ressource par programmation, vous devez établir une connexion et fournir des informations d’identification. Pour ce faire, vous devez créer un client de service.

**Récupérer la ressource à mettre à jour**

Lisez la ressource. Pour plus d’informations, voir [Reading Resources](aem-forms-repository.md#reading-resources).

**Mettre à jour la ressource**

Définissez les nouvelles informations dans la ressource et appelez la méthode du service Repository pour mettre à jour la ressource, en spécifiant l&#39;URI, la ressource mise à jour et comment les informations de version doivent être mises à jour.

**Voir également**

[Mise à jour des ressources à l’aide de l’API Java](aem-forms-repository.md#update-resources-using-the-java-api)

[Mise à jour des ressources à l’aide de l’API de service Web](aem-forms-repository.md#update-resources-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Débuts rapides de l’API Repository Service](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Mettre à jour les ressources à l’aide de l’API Java {#update-resources-using-the-java-api}

Mettez à jour une ressource à l’aide de l’API du service Repository (Java) :

1. Inclure les fichiers de projet

   Incluez les fichiers JAR client dans le chemin de classe de votre projet Java.

1. Créer le client de service

   Créez un objet `ResourceRepositoryClient` en utilisant son constructeur et en transmettant un objet `ServiceClientFactory` contenant des propriétés de connexion.

1. Récupérer la ressource à mettre à jour

   Spécifiez l&#39;URI de la ressource pour récupérer et lire la ressource. Dans cet exemple, l&#39;URI de la ressource est `"/testFolder/testResource"`.

1. Mettre à jour la ressource

   Mettez à jour les informations de l&#39;objet `Resource`. Dans cet exemple, pour mettre à jour la description, appelez la méthode `Resource` de l’objet `setDescription` et transmettez la nouvelle chaîne de description en tant que paramètre.

   Appelez ensuite la méthode `updateResource` de l’objet `ServiceClientFactory`, puis transmettez les paramètres suivants :

   * Objet `java.lang.String` contenant l&#39;URI de la ressource.
   * Objet `Resource` contenant les informations de ressource mises à jour.
   * Valeur `boolean` indiquant si la version principale ou mineure doit être mise à jour. Dans cet exemple, une valeur `true` est transmise pour indiquer que la version majeure doit être incrémentée.

**Voir également**

[Mise à jour des ressources](aem-forms-repository.md#updating-resources)

[Début rapide (mode SOAP) : Mise à jour d’une ressource à l’aide de l’API Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-updating-a-resource-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Mettre à jour les ressources à l’aide de l’API de service Web {#update-resources-using-the-web-service-api}

Mettez à jour une ressource à l’aide de l’API Repository (service Web) :

1. Inclure les fichiers de projet

   * Créez un assembly client Microsoft .NET qui consomme le fichier WSDL du référentiel.
   * Référencez l&#39;assembly client Microsoft .NET.

1. Créer le client de service

   A l&#39;aide de l&#39;assembly client Microsoft .NET, créez un objet `RepositoryServiceService` en appelant son constructeur par défaut. Définissez sa propriété `Credentials` à l’aide d’un objet `System.Net.NetworkCredential` contenant le nom d’utilisateur et le mot de passe.

1. Récupérer la ressource à mettre à jour

   Spécifiez l&#39;URI de la ressource à récupérer et lisez-la. Dans cet exemple, l&#39;URI de la ressource est `"/testFolder/testResource"`. Pour plus d’informations, voir [Reading Resources](aem-forms-repository.md#reading-resources).

1. Mettre à jour la ressource

   Mettez à jour les informations de l&#39;objet `Resource`. Dans cet exemple, pour mettre à jour la description, affectez une nouvelle valeur au champ `Resource` de l&#39;objet `description`.

1. Appelez la méthode `updateResource` de l’objet `RepositoryServiceService` et transmettez les paramètres suivants :

   * Objet `System.String` contenant l&#39;URI de la ressource.
   * Objet `Resource` contenant les informations de ressource mises à jour.
   * Valeur `boolean` indiquant si la version principale ou mineure doit être mise à jour. Dans cet exemple, une valeur `true` est transmise pour indiquer que la version majeure doit être incrémentée.
   * Transmettez `null` pour les deux paramètres restants.

**Voir également**

[Mise à jour des ressources](aem-forms-repository.md#updating-resources)

[Appel de AEM Forms à l’aide du codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## Recherche de ressources {#searching-for-resources}

Vous pouvez créer des requêtes utilisées pour rechercher des ressources dans le référentiel, y compris l’historique, les ressources connexes et les propriétés.

Vous pouvez récupérer des ressources connexes afin de déterminer les dépendances entre un formulaire et ses fragments. Par exemple, si vous disposez d’un formulaire, vous pouvez déterminer les fragments ou les ressources externes qu’il utilise. Si vous disposez d’une image, vous pouvez également déterminer quels formulaires utilisent l’image. Vous pouvez également rechercher des ressources connexes à l’aide du filtrage basé sur les propriétés. Par exemple, vous pouvez rechercher toutes les images utilisées par un formulaire portant un nom donné ou rechercher toutes les images utilisées par un formulaire portant un nom donné. Vous pouvez également effectuer des recherches à l’aide des propriétés de ressource. Par exemple, vous pouvez exécuter une requête pour rechercher tous les formulaires ou ressources dont le nom début avec une chaîne donnée pouvant inclure des caractères génériques &quot;%&quot; et &quot;_&quot;. Rappelez-vous que les recherches basées sur les propriétés ne sont pas basées sur les relations ; ces recherches reposent sur l&#39;hypothèse que vous connaissez une ressource donnée.

**Instructions de requête**

Une *requête* contient une ou plusieurs instructions qui sont logiquement jointes par des conditions. Une instruction ** consiste en un opérande de gauche, un opérateur et un opérande de droite. En outre, vous pouvez spécifier l’ordre de tri à utiliser pour les résultats de la recherche. L&#39;*ordre de tri* contient des informations équivalentes à une clause SQL `ORDER BY` et comprend des éléments qui contiennent les attributs sur lesquels la recherche a été basée, ainsi qu&#39;une valeur indiquant si l&#39;ordre croissant ou décroissant doit être utilisé.

Vous pouvez rechercher des ressources par programmation à l’aide de l’API Java du service Repository. Actuellement, il n’est pas possible d’utiliser l’API du service Web pour rechercher des ressources.

**Comportement de tri**

L’ordre de tri n’est pas respecté lors de l’appel de la méthode `searchProperties` de l’objet `ResourceRepositoryClient` et de la spécification d’un ordre de tri. Par exemple, supposons que vous créez une ressource avec trois propriétés personnalisées, où les noms d&#39;attribut sont `name`, `secondName` et `asecondName`. Ensuite, vous créez un élément d&#39;ordre de tri sur le nom d&#39;attribut et définissez la valeur `ascending` sur `true`.

Ensuite, vous appelez la méthode `ResourceRepositoryClient` de l’objet `searchProperties` et passez dans l’ordre de tri. La recherche renvoie la ressource appropriée, avec les trois propriétés. Cependant, les propriétés ne sont pas triées par nom d’attribut. Ils sont renvoyés dans l’ordre dans lequel ils ont été ajoutés : `name`, `secondName` et `asecondName`.

>[!NOTE]
>
>Pour plus d’informations sur le service Repository, voir [Guide de référence des services pour AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary_of_steps-5}

Pour rechercher des ressources, procédez comme suit :

1. Incluez des fichiers de projet.
1. Créez un client de service Repository.
1. Spécifiez le dossier de cible pour la recherche.
1. Spécifiez les attributs utilisés dans la recherche.
1. Créez la requête utilisée dans la recherche.
1. Créez l&#39;ordre de tri des résultats de la recherche.
1. Recherchez les ressources.
1. Récupérez les ressources à partir des résultats de la recherche.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, incluez les fichiers proxy.

**Créer le client de service**

Avant de pouvoir lire une ressource par programmation, vous devez établir une connexion et fournir des informations d’identification. Pour ce faire, vous devez créer un client de service.

**Spécifier le dossier de cible pour la recherche**

Créez une chaîne contenant le chemin de base à partir duquel effectuer la recherche. La syntaxe comprend des barres obliques verticales, comme dans cet exemple : &quot;/*chemin*/*dossier*&quot;.

**Spécifier les attributs utilisés dans la recherche**

Vous pouvez baser votre recherche sur les attributs contenus dans les ressources. Spécifiez les valeurs des attributs sur lesquels effectuer la recherche.

**Créer la requête utilisée dans la recherche**

Créez une requête à l’aide d’instructions et de conditions. Chaque instruction spécifie l&#39;attribut sur lequel baser la recherche, la condition à utiliser et la valeur d&#39;attribut à utiliser dans la recherche.

**Créer l&#39;ordre de tri des résultats de la recherche**

L’ordre de tri est composé d’éléments, chacun d’eux contenant l’un des attributs utilisés dans la recherche et une valeur indiquant si l’ordre croissant ou décroissant doit être utilisé.

**Rechercher les ressources**

Recherchez les ressources à l’aide du dossier, de la requête et de l’ordre de tri. En outre, indiquez la profondeur de la recherche et une limite supérieure au nombre de résultats à renvoyer.

**Récupérer les ressources des résultats de la recherche**

Effectuer une itération sur la liste des ressources renvoyée et extraire les informations pour les traiter ultérieurement.

**Voir également**

[Recherche de ressources à l’aide de l’API Java](aem-forms-repository.md#search-for-resources-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Débuts rapides de l’API Repository Service](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Rechercher des ressources à l’aide de l’API Java {#search-for-resources-using-the-java-api}

Recherchez une ressource à l’aide de l’API du service Repository (Java) :

1. Inclure les fichiers de projet

   Incluez les fichiers JAR client dans le chemin de classe de votre projet Java.

1. Créer le client de service

   Créez un objet `ResourceRepositoryClient` en utilisant son constructeur et en transmettant un objet `ServiceClientFactory` contenant des propriétés de connexion.

1. Spécifier le dossier de cible pour la recherche

   Spécifiez l’URI du chemin de base à partir duquel exécuter la recherche. Dans cet exemple, l&#39;URI de la ressource est `/testFolder`.

1. Spécifier les attributs utilisés dans la recherche

   Spécifiez les valeurs des attributs sur lesquels effectuer la recherche. Les attributs existent dans un objet `com.adobe.repository.infomodel.bean.Resource`. Dans cet exemple, la recherche sera effectuée sur l&#39;attribut name ; par conséquent, un `java.lang.String` contenant le nom de l’objet `Resource` est utilisé, c’est-à-dire `testResource` dans ce cas.

1. Créer la requête utilisée dans la recherche

   Pour créer une requête, créez un objet `com.adobe.repository.query.Query` en appelant le constructeur par défaut pour la classe `Query` et ajoutez des instructions à la requête.

   Pour créer une instruction, appelez le constructeur de la classe `com.adobe.repository.query.Query.Statement` et transmettez les paramètres suivants :

   * Opérande de gauche contenant la constante d&#39;attribut de ressource. Dans cet exemple, étant donné que le nom de la ressource est utilisé comme base de la recherche, la valeur statique `Resource.ATTRIBUTE_NAME` est utilisée.
   * Opérateur contenant la condition utilisée dans la recherche de l’attribut. L&#39;opérateur doit être l&#39;une des constantes statiques de la classe `Query.Statement`. Dans cet exemple, la valeur statique `Query.Statement.OPERATOR_BEGINS_WITH` est utilisée.
   * Opérande de droite contenant la valeur d’attribut sur laquelle effectuer la recherche. Dans cet exemple, l’attribut name, un `String` contenant la valeur `"testResource"`, est utilisé.

   Spécifiez l’espace de nommage de l’opérande de gauche en appelant la méthode `Query.Statement` de l’objet `setNamespace` et en transmettant l’une des valeurs statiques contenues dans la classe `com.adobe.repository.infomodel.bean.ResourceProperty`. Dans cet exemple, `ResourceProperty.RESERVED_NAMESPACE_REPOSITORY` est utilisé.

   Ajoutez chaque instruction à la requête en appelant la méthode `Query` de l&#39;objet `addStatement` et en transmettant l&#39;objet `Query.Statement`.

1. Créer l&#39;ordre de tri des résultats de la recherche

   Pour spécifier l&#39;ordre de tri utilisé dans les résultats de la recherche, créez un objet `com.adobe.repository.query.sort.SortOrder` en appelant le constructeur par défaut pour la classe `SortOrder` et ajoutez des éléments à l&#39;ordre de tri.

   Pour créer un élément pour l&#39;ordre de tri, appelez l&#39;un des constructeurs de la classe `com.adobe.repository.query.sort.SortOrder.Element`. Dans cet exemple, puisque le nom de la ressource est utilisé comme base de la recherche, la valeur statique `Resource.ATTRIBUTE_NAME` est utilisée comme premier paramètre et l’ordre croissant (une valeur `boolean` de `true`) est spécifié comme second paramètre.

   Ajoutez chaque élément à l’ordre de tri en appelant la méthode `SortOrder` de l’objet `addSortElement` et en transmettant l’objet `SortOrder.Element`.

1. Rechercher les ressources

   Pour rechercher `resources` en fonction des propriétés d&#39;attribut, appelez la méthode `ResourceRepositoryClient` de l&#39;objet `searchProperties` et transmettez les paramètres suivants :

   * `String` contenant le chemin de base à partir duquel exécuter la recherche. Dans ce cas, `"/testFolder"` est utilisé.
   * Requête utilisée dans la recherche.
   * Profondeur de la recherche. Dans ce cas, `com.adobe.repository.infomodel.bean.ResourceCollection.DEPTH_INFINITE` est utilisé pour indiquer que le chemin de base et tous ses dossiers doivent être utilisés.
   * Valeur `int` indiquant la première ligne à partir de laquelle sélectionner le jeu de résultats non paginé. Dans cet exemple, `0` est spécifié.
   * Valeur `int` indiquant le nombre maximal de résultats à renvoyer. Dans cet exemple, `10` est spécifié.
   * Ordre de tri utilisé dans la recherche.

   La méthode renvoie un `java.util.List` objet `Resource` dans l&#39;ordre de tri spécifié.

1. Récupérer les ressources des résultats de la recherche

   Pour récupérer les ressources contenues dans le résultat de la recherche, effectuez une itération dans `List` et convertissez chaque objet en `Resource` afin d&#39;extraire ses informations. Dans cet exemple, le nom de chaque ressource s&#39;affiche.

**Voir également**

[Recherche de ressources](aem-forms-repository.md#searching-for-resources)

[Début rapide (mode SOAP) : Recherche de ressources à l’aide de l’API Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-searching-for-resources-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Création de relations de ressources {#creating-resource-relationships}

Vous pouvez spécifier des relations entre les ressources dans le référentiel. Il existe trois types de relations :

* **Dépendance** : une relation dans laquelle une ressource dépend d&#39;autres ressources, ce qui signifie que toutes les ressources connexes sont nécessaires dans le référentiel.
* **Appartenance (système de fichiers)** : relation dans laquelle une ressource se trouve dans un dossier donné.
* **Personnalisé** : une relation que vous spécifiez entre les ressources. Par exemple, si une ressource a été abandonnée et qu’une autre ressource a été introduite dans le référentiel, vous pouvez spécifier votre propre relation de remplacement.

Vous pouvez créer vos propres relations personnalisées. Par exemple, si vous stockez un fichier HTML dans le référentiel et qu’il utilise une image, vous pouvez spécifier une relation personnalisée pour relier le fichier HTML à l’image (puisque, normalement, seuls les fichiers XML sont associés aux images à l’aide d’une relation de dépendance définie par le référentiel). Un autre exemple de relation personnalisée serait si vous vouliez créer une vue différente du référentiel avec une structure de graphique cyclique au lieu d&#39;une structure d&#39;arborescence. Vous pouvez définir un graphique circulaire avec une visionneuse pour parcourir ces relations. Enfin, vous pouvez indiquer qu&#39;une ressource remplace une autre ressource même si les deux ressources sont complètement différentes. Dans ce cas, vous pouvez définir un type de relation en dehors de la plage réservée et créer une relation entre ces deux ressources. Votre application serait le seul client à pouvoir détecter et traiter la relation, et elle pourrait être utilisée pour effectuer des recherches sur cette relation.

Vous pouvez par programmation définir des relations entre les ressources à l’aide de l’API Java du service Repository ou de l’API du service Web.

>[!NOTE]
>
>Pour plus d’informations sur le service Repository, voir [Guide de référence des services pour AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary_of_steps-6}

Pour définir une relation entre deux ressources, procédez comme suit :

1. Incluez des fichiers de projet.
1. Créez un client de service Repository.
1. Spécifiez les URI des ressources à relier.
1. Créez la relation.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, incluez les fichiers proxy.

**Créer le client de service**

Avant de pouvoir lire une ressource par programmation, vous devez établir une connexion et fournir des informations d’identification. Pour ce faire, vous devez créer un client de service.

**Spécifier les URI des ressources à relier**

Créez des chaînes contenant les URI de la ressource à relier. La syntaxe comprend des barres obliques verticales, comme dans cet exemple : &quot;/*chemin*/*ressource*&quot;.

**Créer la relation**

Appelez la méthode du service Repository pour créer et spécifier le type de relation.

**Voir également**

[Créer des ressources de relation à l’aide de l’API Java](aem-forms-repository.md#create-relationship-resources-using-the-java-api)

[Créer des ressources de relation à l’aide de l’API de service Web](aem-forms-repository.md#create-relationship-resources-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Débuts rapides de l’API Repository Service](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Créez des ressources de relation à l’aide de l’API Java {#create-relationship-resources-using-the-java-api}

Créez des ressources de relation à l’aide de l’API Java du service Repository, effectuez les tâches suivantes :

1. Inclure les fichiers de projet

   Incluez les fichiers JAR client dans le chemin de classe de votre projet Java.

1. Créer le client de service

   Créez un objet `ResourceRepositoryClient` en utilisant son constructeur et en transmettant un objet `ServiceClientFactory` contenant des propriétés de connexion.

1. Spécifier les URI des ressources à relier

   Spécifiez les URI des ressources à relier. Dans ce cas, puisque les ressources sont nommées `testResource1` et `testResource2` et se trouvent dans le dossier `testFolder`, leurs URI sont `"/testFolder/testResource1"` et `"/testFolder/testResource2"`. Les URI sont stockés en tant qu&#39;objets `java.lang.String`. Dans cet exemple, les ressources sont d’abord écrites dans le référentiel et leurs URI sont récupérés. Pour plus d&#39;informations sur l&#39;écriture d&#39;une ressource, voir [Writing Resources](aem-forms-repository.md#writing-resources).

1. Créer la relation

   Appelez la méthode `createRelationship` de l’objet `ResourceRepositoryClient` et transmettez les paramètres suivants :

   * URI de la ressource source.
   * URI de la ressource de cible.
   * Type de relation, qui est l&#39;une des constantes statiques de la classe `com.adobe.repository.infomodel.bean.Relation`. Dans cet exemple, une relation de dépendance est établie en spécifiant la valeur `Relation.TYPE_DEPENDANT_OF`.
   * Valeur `boolean` indiquant si la ressource de cible est automatiquement mise à jour vers l&#39;identifiant `com.adobe.repository.infomodel.Id` de la nouvelle ressource principale. Dans cet exemple, en raison de la relation de dépendance, la valeur `true` est spécifiée.

   Vous pouvez également récupérer une liste de ressources connexes pour une ressource donnée en appelant la méthode `ResourceRepositoryClient` de l&#39;objet `getRelated` et en transmettant les paramètres suivants :

   * URI de la ressource pour laquelle récupérer les ressources connexes. Dans cet exemple, la ressource source ( `"/testFolder/testResource1"`) est spécifiée.
   * Valeur `boolean` indiquant si la ressource spécifiée est la ressource source dans la relation. Dans cet exemple, la valeur `true` est spécifiée, car c&#39;est le cas.
   * Type de relation, qui est l&#39;une des constantes statiques de la classe `Relation`. Dans cet exemple, une relation de dépendance est spécifiée en utilisant la même valeur que celle utilisée précédemment : `Relation.TYPE_DEPENDANT_OF`.

   La méthode `getRelated` renvoie `java.util.List` des objets `Resource` par l&#39;intermédiaire desquels vous pouvez itérer pour récupérer chacune des ressources connexes, en faisant passer les objets contenus dans `List` à `Resource` comme vous le faites. Dans cet exemple, `testResource2` devrait être dans la liste des ressources renvoyées.

**Voir également**

[Création de relations de ressources](aem-forms-repository.md#creating-resource-relationships)

[Début rapide (mode SOAP) : Création de relations entre les ressources à l’aide de l’API Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-creating-relationships-between-resources-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Créer des ressources de relation à l’aide de l’API de service Web {#create-relationship-resources-using-the-web-service-api}

Créez des ressources de relation à l’aide de l’API Repository (service Web) :

1. Inclure les fichiers de projet

   * Créez un assembly client Microsoft .NET qui consomme le fichier WSDL du référentiel.
   * Référencez l&#39;assembly client Microsoft .NET.

1. Créer le client de service

   A l&#39;aide de l&#39;assembly client Microsoft .NET, créez un objet `RepositoryServiceService` en appelant son constructeur par défaut. Définissez sa propriété `Credentials` à l’aide d’un objet `System.Net.NetworkCredential` contenant le nom d’utilisateur et le mot de passe.

1. Spécifier les URI des ressources à relier

   Spécifiez les URI des ressources à relier. Dans ce cas, puisque les ressources sont nommées `testResource1` et `testResource2` et se trouvent dans le dossier `testFolder`, leurs URI sont `"/testFolder/testResource1"` et `"/testFolder/testResource2"`. Lorsque vous utilisez un langage compatible avec Microsoft .NET Framework (C#, par exemple), les URI sont stockés sous la forme d&#39;objets `System.String`. Dans cet exemple, les ressources sont d’abord écrites dans le référentiel et leurs URI sont récupérés. Pour plus d&#39;informations sur l&#39;écriture d&#39;une ressource, voir [Writing Resources](aem-forms-repository.md#writing-resources).

1. Créer la relation

   Appelez la méthode `createRelationship` de l’objet `RepositoryServiceService` et transmettez les paramètres suivants :

   * URI de la ressource source.
   * URI de la ressource de cible.
   * Type de relation. Dans cet exemple, une relation de dépendance est établie en spécifiant la valeur `3`.
   * Valeur `boolean` indiquant si le type de relation a été spécifié. Dans cet exemple, la valeur `true` est spécifiée.
   * Valeur `boolean` indiquant si la ressource de cible est automatiquement mise à jour vers l&#39;identifiant `Id` de la nouvelle ressource principale. Dans cet exemple, en raison de la relation de dépendance, la valeur `true` est spécifiée.
   * Valeur `boolean` indiquant si le titre de la cible a été spécifié. Dans cet exemple, la valeur `true` est spécifiée.
   * Transmettez `null` pour le dernier paramètre.

   Vous pouvez également récupérer une liste de ressources connexes pour une ressource donnée en appelant la méthode `RepositoryServiceService` de l&#39;objet `getRelated` et en transmettant les paramètres suivants :

   * URI de la ressource pour laquelle récupérer les ressources connexes. Dans cet exemple, la ressource source ( `"/testFolder/testResource1"`) est spécifiée.
   * Valeur `boolean` indiquant si la ressource spécifiée est la ressource source dans la relation. Dans cet exemple, la valeur `true` est spécifiée, car c&#39;est le cas.
   * Valeur `boolean` indiquant si la ressource source a été spécifiée. Dans cet exemple, la valeur `true` est fournie.
   * Tableau d’entiers contenant les types de relation. Dans cet exemple, une relation de dépendance est spécifiée en utilisant la même valeur dans le tableau que celle utilisée précédemment : `3`.
   * Transmettez `null` pour les deux paramètres restants.

   La méthode `getRelated` renvoie un tableau d&#39;objets qui peuvent être convertis en objets `Resource` par l&#39;intermédiaire desquels vous pouvez itérer pour récupérer chacune des ressources associées. Dans cet exemple, `testResource2` devrait être dans la liste des ressources renvoyées.

**Voir également**

[Création de relations de ressources](aem-forms-repository.md#creating-resource-relationships)

[Appel de AEM Forms à l’aide du codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## Verrouillage des ressources {#locking-resources}

Vous pouvez verrouiller une ressource ou un ensemble de ressources pour une utilisation exclusive par un utilisateur particulier ou pour une utilisation partagée par plusieurs utilisateurs. Un verrou partagé est une indication que quelque chose arrivera avec la ressource, mais cela n&#39;empêche personne d&#39;autre de prendre des mesures avec cette ressource. Un verrou partagé doit être considéré comme un mécanisme de signalisation. Un verrou exclusif signifie que l&#39;utilisateur qui a verrouillé la ressource va changer la ressource, et le verrou garantit que personne d&#39;autre ne peut le faire jusqu&#39;à ce que l&#39;utilisateur n&#39;ait plus besoin d&#39;accéder à la ressource et ait libéré le verrou. Si un administrateur de référentiel déverrouille une ressource, tous les verrous exclusifs et partagés de cette ressource seront automatiquement supprimés. Ce type d&#39;action est destiné aux situations où un utilisateur n&#39;est plus disponible et n&#39;a pas déverrouillé la ressource.

Lorsqu’une ressource est verrouillée, une icône de verrouillage s’affiche lorsque vous vue l’onglet Ressources situé dans Workbench, comme illustré ci-dessous.

![lr_lr_lockrepository](assets/lr_lr_lockrepository.png)

Vous pouvez contrôler par programmation l’accès aux ressources en utilisant l’API Java du service Repository ou l’API du service Web.

>[!NOTE]
>
>Pour plus d’informations sur le service Repository, voir [Guide de référence des services pour AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary_of_steps-7}

Pour verrouiller et déverrouiller des ressources, procédez comme suit :

1. Incluez des fichiers de projet.
1. Créez un client de service Repository.
1. Spécifiez l&#39;URI de la ressource à verrouiller.
1. Verrouillez la ressource.
1. Récupérez les verrous de la ressource.
1. Déverrouiller la ressource

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, incluez les fichiers proxy.

**Créer le client de service**

Avant de pouvoir lire une ressource par programmation, vous devez établir une connexion et fournir des informations d’identification. Pour ce faire, vous devez créer un client de service.

**Spécifiez l&#39;URI de la ressource à verrouiller.**

Créez une chaîne contenant l&#39;URI de la ressource à verrouiller. La syntaxe comprend des barres obliques verticales, comme dans cet exemple : &quot;/*chemin*/*ressource*&quot;.

**Verrouiller la ressource**

Appelez la méthode du service Repository pour verrouiller la ressource, en spécifiant l&#39;URI, le type de verrouillage et la profondeur de verrouillage.

**Récupérer les verrous de la ressource**

Appelez la méthode du service Repository pour récupérer les verrous de la ressource, en spécifiant l&#39;URI.

**Déverrouiller la ressource**

Appelez la méthode du service Repository pour déverrouiller la ressource, en spécifiant l&#39;URI.

**Voir également**

[Verrouillage des ressources à l’aide de l’API Java](aem-forms-repository.md#lock-resources-using-the-java-api)

[Verrouillage des ressources à l’aide de l’API du service Web](aem-forms-repository.md#lock-resources-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Débuts rapides de l’API Repository Service](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Verrouillage des ressources à l’aide de l’API Java {#lock-resources-using-the-java-api}

Verrouillez les ressources à l’aide de l’API du service Repository (Java) :

1. Inclure les fichiers de projet

   Incluez les fichiers JAR client dans le chemin de classe de votre projet Java.

1. Créer le client de service

   Créez un objet `ResourceRepositoryClient` en utilisant son constructeur et en transmettant un objet `ServiceClientFactory` contenant des propriétés de connexion.

1. Spécifiez l&#39;URI de la ressource à verrouiller.

   Spécifiez l&#39;URI de la ressource à verrouiller. Dans ce cas, puisque la ressource `testResource` se trouve dans le dossier `testFolder`, son URI est `"/testFolder/testResource"`. L&#39;URI est stocké en tant qu&#39;objet `java.lang.String`.

1. Verrouiller la ressource

   Appelez la méthode `lockResource` de l’objet `ResourceRepositoryClient` et transmettez les paramètres suivants :

   * URI de la ressource.
   * Portée de verrouillage. Dans cet exemple, étant donné que la ressource sera verrouillée pour une utilisation exclusive, l&#39;étendue de verrouillage est spécifiée comme `com.adobe.repository.infomodel.bean.Lock.SCOPE_EXCLUSIVE`.
   * La profondeur de verrouillage. Dans cet exemple, étant donné que le verrouillage s&#39;applique uniquement à la ressource particulière et qu&#39;aucun de ses membres ou enfants ne l&#39;est, la profondeur de verrouillage est spécifiée comme `Lock.DEPTH_ZERO`.

   >[!NOTE]
   >
   >La version surchargée de la méthode `lockResource` qui requiert quatre paramètres renvoie une exception. Veillez à utiliser la méthode `lockResource` qui requiert trois paramètres, comme indiqué dans cette procédure pas à pas.

1. Récupérer les verrous de la ressource

   Appelez la méthode `ResourceRepositoryClient` de l&#39;objet `getLocks` et transmettez l&#39;URI de la ressource en tant que paramètre. La méthode renvoie une Liste d&#39;objets Lock par laquelle vous pouvez effectuer une itération. Dans cet exemple, le propriétaire du verrou, la profondeur et la portée sont imprimés pour chaque objet en appelant respectivement les méthodes `getOwnerUserId`, `getDepth` et `getType` de chaque objet Lock.

1. Déverrouiller la ressource

   Appelez la méthode `ResourceRepositoryClient` de l&#39;objet `unlockResource` et transmettez l&#39;URI de la ressource en tant que paramètre. Pour plus d’informations, voir la [Référence de l’API AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Voir également**

[Verrouillage des ressources](aem-forms-repository.md#locking-resources)

[Début rapide (mode SOAP) : Verrouillage d&#39;une ressource à l&#39;aide de l&#39;API Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-locking-a-resource-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Verrouillage des ressources à l’aide de l’API de service Web {#lock-resources-using-the-web-service-api}

Verrouillez les ressources à l’aide de l’API du service de référentiel (service Web) :

1. Inclure les fichiers de projet

   * Créez un assembly client Microsoft .NET qui consomme le fichier WSDL du référentiel à l&#39;aide de Base64.
   * Référencez l&#39;assembly client Microsoft .NET.

1. Créer le client de service

   A l&#39;aide de l&#39;assembly client Microsoft .NET, créez un objet `RepositoryServiceService` en appelant son constructeur par défaut. Définissez sa propriété `Credentials` à l’aide d’un objet `System.Net.NetworkCredential` contenant le nom d’utilisateur et le mot de passe.

1. Spécifiez l&#39;URI de la ressource à verrouiller.

   Spécifiez une chaîne contenant l&#39;URI de la ressource à verrouiller. Dans ce cas, puisque la ressource `testResource` se trouve dans le dossier `testFolder`, son URI est `"/testFolder/testResource"`. Lorsque vous utilisez un langage compatible avec Microsoft .NET Framework (C#, par exemple), stockez l&#39;URI dans un objet `System.String`.

1. Verrouiller la ressource

   Appelez la méthode `lockResource` de l’objet `RepositoryServiceService` et transmettez les paramètres suivants :

   * URI de la ressource.
   * Portée de verrouillage. Dans cet exemple, étant donné que la ressource sera verrouillée pour une utilisation exclusive, l&#39;étendue de verrouillage est spécifiée comme `11`.
   * La profondeur de verrouillage. Dans cet exemple, étant donné que le verrouillage s&#39;applique uniquement à la ressource particulière et qu&#39;aucun de ses membres ou enfants ne l&#39;est, la profondeur de verrouillage est spécifiée comme `2`.
   * Valeur `int` indiquant le nombre de secondes avant l’expiration du verrou. Dans cet exemple, la valeur `1000` est utilisée.
   * Transmettez `null` pour le dernier paramètre.

1. Récupérer les verrous de la ressource

   Appelez la méthode `RepositoryServiceService` de l’objet `getLocks` et transmettez l’URI de la ressource en tant que premier paramètre et `null` en tant que second paramètre. La méthode renvoie un tableau `object` contenant des objets `Lock` par lesquels vous pouvez effectuer une itération. Dans cet exemple, le propriétaire du verrou, la profondeur et la portée sont imprimés pour chaque objet en accédant respectivement aux champs `Lock`, `ownerUserId`, `depth` et `type` de chaque objet.

1. Déverrouiller la ressource

   Appelez la méthode `RepositoryServiceService` de l’objet `unlockResource` et transmettez l’URI de la ressource en tant que premier paramètre et `null` en tant que second paramètre.

**Voir également**

[Verrouillage des ressources](aem-forms-repository.md#locking-resources)

[Appel de AEM Forms à l’aide du codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## Suppression de ressources {#deleting-resources}

Vous pouvez supprimer par programmation des ressources d’un emplacement donné dans le référentiel à l’aide du service Repository Java API (SOAP).

Lorsque vous supprimez une ressource, la suppression est normalement permanente, bien que, dans certains cas, les référentiels ECM puissent stocker les versions de la ressource en fonction de leurs mécanismes d&#39;historique. Par conséquent, lors de la suppression d&#39;une ressource, il est important de s&#39;assurer que vous n&#39;aurez plus jamais besoin de cette ressource. Les raisons courantes de la suppression d&#39;une ressource incluent la nécessité d&#39;augmenter l&#39;espace disponible dans la base de données. Vous pouvez supprimer une version d&#39;une ressource, mais si vous le faites, vous devez spécifier l&#39;identificateur de la ressource, et non son identificateur logique (LID) ou son chemin d&#39;accès. Si vous supprimez un dossier, tous ses éléments, y compris les sous-dossiers et les ressources, seront automatiquement supprimés.

Les ressources connexes ne sont pas supprimées. Par exemple, si vous disposez d’un formulaire qui utilise le fichier logo.gif et que vous supprimez logo.gif, une relation est stockée dans le tableau des relations en attente. En cas d’abandon de version, définissez l’état de l’objet de la dernière version sur désapprouvé.

Une opération de suppression n&#39;est pas sécurisée par les transactions dans les systèmes ECM. Par exemple, si vous tentez de supprimer 100 ressources et que l&#39;opération échoue sur la 50e ressource, les 49 premières instances seront supprimées, mais le reste ne le sera pas. Sinon, le comportement par défaut est la restauration (non-engagement).

>[!NOTE]
>
>Lors de l’utilisation de la méthode `com.adobe.repository.bindings.dsc.client.ResourceRepositoryClient.deleteResources()` avec le référentiel ECM (EMC Documentum Content Server et IBM FileNet P8 Content Manager), la transaction ne sera pas annulée si la suppression échoue pour l’une des ressources spécifiées, ce qui signifie que les fichiers qui ont été supprimés ne peuvent pas être supprimés.

>[!NOTE]
>
>Pour plus d’informations sur le service Repository, voir [Guide de référence des services pour AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary_of_steps-8}

Pour supprimer une ressource, procédez comme suit :

1. Incluez des fichiers de projet.
1. Créez un client de service Repository.
1. Spécifiez l&#39;URI de la ressource à supprimer.
1. Supprimez la ressource.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, incluez les fichiers proxy.

**Créer le client de service**

Avant de pouvoir lire une ressource par programmation, vous devez établir une connexion et fournir des informations d’identification. Pour ce faire, vous devez créer un client de service.

**Spécifiez l&#39;URI de la ressource à supprimer.**

Créez une chaîne contenant l&#39;URI de la ressource à supprimer. La syntaxe comprend des barres obliques verticales, comme dans cet exemple : &quot;/*chemin*/*ressource*&quot;. Si la ressource à supprimer est un dossier, la suppression est récursive.

**Supprimer la ressource**

Appelez la méthode du service Repository pour supprimer la ressource, en spécifiant l&#39;URI.

**Voir également**

[Suppression de ressources à l’aide de l’API Java](aem-forms-repository.md#delete-resources-using-the-java-api-soap)

[Suppression de ressources à l’aide de l’API de service Web](aem-forms-repository.md#delete-resources-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Débuts rapides de l’API Repository Service](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Supprimer des ressources à l&#39;aide de l&#39;API Java (SOAP) {#delete-resources-using-the-java-api-soap}

Supprimez une ressource à l&#39;aide de l&#39;API Repository (Java) :

1. Inclure les fichiers de projet

   Incluez les fichiers JAR client dans le chemin de classe de votre projet Java.

1. Créer le client de service

   Créez un objet `ResourceRepositoryClient` en utilisant son constructeur et en transmettant un objet `ServiceClientFactory` contenant des propriétés de connexion.

1. Spécifiez l&#39;URI de la ressource à supprimer.

   Spécifiez l&#39;URI de la ressource à récupérer. Dans ce cas, puisque la ressource nommée testResourceToBeDeleted se trouve dans le dossier appelé testFolder, son URI est `/testFolder/testResourceToBeDeleted`. L&#39;URI est stocké en tant qu&#39;objet `java.lang.String`. Dans cet exemple, la ressource est d&#39;abord écrite dans le référentiel et son URI est récupéré. Pour plus d&#39;informations sur l&#39;écriture d&#39;une ressource, voir [Writing Resources](aem-forms-repository.md#writing-resources).

1. Supprimer la ressource

   Appelez la méthode `ResourceRepositoryClient` de l&#39;objet `deleteResource` et transmettez l&#39;URI de la ressource en tant que paramètre.

**Voir également**

[Suppression de ressources](aem-forms-repository.md#deleting-resources)

[Début rapide (mode SOAP) : Recherche de ressources à l’aide de l’API Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-searching-for-resources-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Supprimer des ressources à l’aide de l’API de service Web {#delete-resources-using-the-web-service-api}

Supprimez une ressource à l’aide de l’API Repository (service Web) :

1. Inclure les fichiers de projet

   * Créez un assembly client Microsoft .NET qui consomme le fichier WSDL du référentiel à l&#39;aide de Base64.
   * Référencez l&#39;assembly client Microsoft .NET.

1. Créer le client de service

   A l&#39;aide de l&#39;assembly client Microsoft .NET, créez un objet `RepositoryServiceService` en appelant son constructeur par défaut. Définissez sa propriété `Credentials` à l’aide d’un objet `System.Net.NetworkCredential` contenant le nom d’utilisateur et le mot de passe.

1. Spécifiez l&#39;URI de la ressource à supprimer.

   Spécifiez l&#39;URI de la ressource à récupérer. Dans ce cas, puisque la ressource `testResourceToBeDeleted` se trouve dans le dossier `testFolder`, son URI est `"/testFolder/testResourceToBeDeleted"`. Dans cet exemple, la ressource est d&#39;abord écrite dans le référentiel et son URI est récupéré. Pour plus d&#39;informations sur l&#39;écriture d&#39;une ressource, voir [Writing Resources](aem-forms-repository.md#writing-resources).

1. Supprimer la ressource

   Appelez la méthode `RepositoryServiceService` de l&#39;objet `deleteResources` et transmettez un tableau `System.String` contenant l&#39;URI de la ressource en tant que premier paramètre. Transmettez `null` pour le second paramètre.

**Voir également**

[Suppression de ressources](aem-forms-repository.md#deleting-resources)

[Appel de AEM Forms à l’aide du codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
