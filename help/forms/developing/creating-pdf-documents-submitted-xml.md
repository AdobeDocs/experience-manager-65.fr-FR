---
title: Création de documents PDF avec des données XML envoyées
seo-title: Création de documents PDF avec des données XML envoyées
description: 'null'
seo-description: 'null'
uuid: 2676c614-8988-451b-ac7c-bd07731a3f5f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 62490230-a24e-419d-95bb-c0bb04a03f96
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Création de documents PDF avec des données XML envoyées {#creating-pdf-documents-with-submittedxml-data}

## Création de documents PDF avec des données XML envoyées {#creating-pdf-documents-with-submitted-xml-data}

Les applications Web qui permettent aux utilisateurs de remplir des formulaires interactifs nécessitent que les données soient renvoyées au serveur. Le service Forms vous permet de récupérer les données de formulaire saisies par l’utilisateur dans un formulaire interactif. Vous pouvez ensuite transmettre les données de formulaire à une autre opération de service AEM Forms et créer un document PDF à l’aide des données.

>[!NOTE]
>
>Avant de lire ce contenu, il est recommandé de bien comprendre la gestion des formulaires envoyés. Des concepts tels que la relation entre une conception de formulaire et les données XML envoyées sont traités dans Gestion des formulaires envoyés.

Tenez compte du flux de travail suivant qui implique trois services AEM Forms :

* Un utilisateur envoie des données XML au service Forms à partir d’une application Web.
* Le service Forms est utilisé pour traiter le formulaire envoyé et extraire les champs de formulaire. Les données de formulaire peuvent être traitées. Par exemple, les données peuvent être envoyées à une base de données d’entreprise.
* Les données de formulaire sont envoyées au service Output pour créer un document PDF non interactif.
* Le document PDF non interactif est stocké dans Content Services (obsolète).

Le diagramme suivant fournit une représentation visuelle de ce processus.

![cd_cd_finsrv_architecture_xml_pdf1](assets/cd_cd_finsrv_architecture_xml_pdf1.png)

Une fois le formulaire envoyé par l’utilisateur à partir du navigateur Web client, le document PDF non interactif est stocké dans Content Services (obsolète). L’illustration suivante présente un document PDF stocké dans Content Services (obsolète).

![cd_cd_cs_gui](assets/cd_cd_cs_gui.png)

### Résumé des étapes {#summary-of-steps}

Pour créer un document PDF non interactif avec des données XML envoyées et le stocker dans le document PDF dans Content Services (obsolète), effectuez les tâches suivantes :

1. Incluez des fichiers de projet.
1. Créez des objets Forms, Output et Document Management.
1. Récupérez les données de formulaire à l’aide du service Forms.
1. Créez un document PDF non interactif à l’aide du service Output.
1. Stockez le formulaire PDF dans Content Services (obsolète) à l’aide du service Document Management.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

**Création d’objets Forms, Output et Document Management**

Avant de pouvoir exécuter par programmation une opération d’API de service Forms, créez un objet API Client Forms. De même, puisque ce processus appelle les services Output et Document Management, créez un objet API Client Output et un objet API Client Document Management.

**Récupération des données de formulaire à l’aide du service Forms**

Récupérez les données de formulaire qui ont été envoyées au service Forms. Vous pouvez traiter les données envoyées pour répondre aux besoins de votre entreprise. Par exemple, vous pouvez stocker des données de formulaire dans une base de données d’entreprise. Toutefois, pour créer un document PDF non interactif, les données de formulaire sont transmises au service Output.

**Créez un document PDF non interactif à l’aide du service Output.**

Utilisez le service Output pour créer un document PDF non interactif basé sur une conception de formulaire et des données de formulaire XML. Dans le processus, les données de formulaire sont récupérées à partir du service Forms.

**Stockez le formulaire PDF dans Content Services (obsolète) à l’aide du service Document Management.**

Utilisez l’API du service Document Management pour stocker un document PDF dans Content Services (obsolète).

**Voir également**

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Démarrage rapide de l’API du service Forms](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

### Création d’un document PDF avec des données XML envoyées à l’aide de l’API Java {#create-a-pdf-document-with-submitted-xml-data-using-the-java-api}

Créez un document PDF avec des données XML envoyées à l’aide de l’API Forms, Output et Document Management (Java) :

1. Inclure les fichiers de projet

   Incluez les fichiers JAR client, tels que adobe-forms-client.jar, adobe-output-client.jar et adobe-contentservices-client.jar dans le chemin de classe de votre projet Java.

1. Création d’objets Forms, Output et Document Management

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `FormsServiceClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`. 
   * Create an `OutputClient` object by using its constructor and passing the `ServiceClientFactory` object.
   * Créez un objet `DocumentManagementServiceClientImpl` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`. 

1. Récupération des données de formulaire à l’aide du service Forms

   * Appelez la méthode `FormsServiceClient` `processFormSubmission` de l’objet et transmettez les valeurs suivantes :

      * Objet `com.adobe.idp.Document` contenant les données du formulaire.
      * Valeur de chaîne qui spécifie les variables d’environnement, y compris tous les en-têtes HTTP appropriés. Spécifiez le type de contenu à gérer en spécifiant une ou plusieurs valeurs pour la variable `CONTENT_TYPE` d’environnement. Par exemple, pour gérer les données XML, spécifiez la valeur de chaîne suivante pour ce paramètre : `CONTENT_TYPE=text/xml`.
      * Valeur de chaîne qui spécifie la valeur d’ `HTTP_USER_AGENT` en-tête, telle que `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
      * Objet `RenderOptionsSpec` qui stocke les options d’exécution.
      La `processFormSubmission` méthode renvoie un `FormsResult` objet contenant les résultats de l’envoi du formulaire.

   * Déterminez si le service Forms a terminé le traitement des données de formulaire en appelant la `FormsResult` `getAction` méthode de l’objet. Si cette méthode renvoie la valeur `0`, les données sont prêtes à être traitées.
   * Récupérez des données de formulaire en créant un `com.adobe.idp.Document` objet en appelant la `FormsResult` méthode de l’ `getOutputContent` objet. (Cet objet contient des données de formulaire pouvant être envoyées au service Output.)
   * Créez un `java.io.InputStream` objet en appelant le `java.io.DataInputStream` constructeur et en transmettant l’ `com.adobe.idp.Document` objet.
   * Créez un `org.w3c.dom.DocumentBuilderFactory` objet en appelant la `org.w3c.dom.DocumentBuilderFactory` `newInstance` méthode de l’objet statique.
   * Créez un `org.w3c.dom.DocumentBuilder` objet en appelant la `org.w3c.dom.DocumentBuilderFactory` méthode de l’ `newDocumentBuilder` objet.
   * Create an `org.w3c.dom.Document` object by invoking the `org.w3c.dom.DocumentBuilder` object’s `parse` method and passing the `java.io.InputStream` object.
   * Récupérez la valeur de chaque noeud dans le document XML. Pour ce faire, vous pouvez créer une méthode personnalisée qui accepte deux paramètres : l’ `org.w3c.dom.Document` objet et le nom du noeud dont vous souhaitez récupérer la valeur. Cette méthode renvoie une valeur de chaîne représentant la valeur du noeud. Dans l’exemple de code qui suit ce processus, cette méthode personnalisée est appelée `getNodeText`. Le corps de cette méthode est illustré.


1. Créez un document PDF non interactif à l’aide du service Output.

   Create a PDF document by invoking the `OutputClient` object’s `generatePDFOutput` method and passing the following values:

   * Valeur `TransformationFormat` enum. Pour générer un document PDF, spécifiez `TransformationFormat.PDF`.
   * Valeur string spécifiant le nom de la nouvelle conception de formulaire. Assurez-vous que la conception de formulaire est compatible avec les données de formulaire extraites du service Forms.
   * Valeur de chaîne qui spécifie la racine de contenu où se trouve la conception de formulaire.
   * Objet `PDFOutputOptionsSpec` contenant des options d’exécution PDF.
   * Objet `RenderOptionsSpec` contenant des options d’exécution de rendu.
   * Objet `com.adobe.idp.Document` contenant la source de données XML contenant les données à fusionner avec la conception de formulaire. Assurez-vous que cet objet a été renvoyé par la `FormsResult` `getOutputContent` méthode de l’objet.
   * The `generatePDFOutput` method returns an `OutputResult` object that contains the results of the operation.
   * Récupérez le document PDF non interactif en appelant la `OutputResult` `getGeneratedDoc` méthode de l’objet. Cette méthode renvoie une `com.adobe.idp.Document` instance représentant le document PDF non interactif.

1. Stockez le formulaire PDF dans Content Services (obsolète) à l’aide du service Document Management.

   Ajoutez le contenu en appelant la `DocumentManagementServiceClientImpl` `storeContent` méthode de l’objet et en transmettant les valeurs suivantes :

   * Valeur de chaîne qui spécifie le magasin où le contenu est ajouté. Le magasin par défaut est `SpacesStore`. Cette valeur est un paramètre obligatoire.
   * Valeur de chaîne qui spécifie le chemin d’accès complet à l’espace dans lequel le contenu est ajouté (par exemple, `/Company Home/Test Directory`). Cette valeur est un paramètre obligatoire.
   * Nom du noeud qui représente le nouveau contenu (par exemple, `MortgageForm.pdf`). Cette valeur est un paramètre obligatoire.
   * Valeur de chaîne qui spécifie le type de noeud. Pour ajouter un nouveau contenu, tel qu’un fichier PDF, spécifiez `{https://www.alfresco.org/model/content/1.0}content`. Cette valeur est un paramètre obligatoire.
   * Objet `com.adobe.idp.Document` représentant le contenu. Cette valeur est un paramètre obligatoire.
   * Valeur de chaîne qui spécifie la valeur de codage (par exemple, `UTF-8`). Cette valeur est un paramètre obligatoire.
   * Valeur `UpdateVersionType` d’énumération spécifiant comment gérer les informations de version ( `UpdateVersionType.INCREMENT_MAJOR_VERSION` pour incrémenter la version de contenu, par exemple). ) Cette valeur est un paramètre obligatoire.
   * Une `java.util.List` instance qui spécifie les aspects liés au contenu. Cette valeur est un paramètre facultatif que vous pouvez spécifier `null`.
   * Objet `java.util.Map` qui stocke les attributs de contenu.
   La `storeContent` méthode renvoie un `CRCResult` objet qui décrit le contenu. A l’aide d’un `CRCResult` objet, vous pouvez, par exemple, obtenir la valeur d’identificateur unique du contenu. Pour effectuer cette tâche, appelez la `CRCResult` `getNodeUuid` méthode de l’objet.

**Voir également**

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
