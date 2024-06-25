---
title: Gérer des formulaires envoyés
description: Utilisez le service Forms pour récupérer les données envoyées saisies dans un formulaire interactif. L’utilisateur peut envoyer les données de formulaire aux formats XML, PDF et URL UTF-16.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 419335b2-2aae-4e83-98ff-18e61b7efa9c
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services,APIs & Integrations
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '2894'
ht-degree: 100%

---

# Gérer des formulaires envoyés {#handling-submitted-forms}

**Les exemples et les échantillons de ce document sont réservés à l’environnement AEM Forms sur JEE.**

Les applications web permettant à l’utilisateur de remplir des formulaires interactifs nécessitent que les données soient renvoyées au serveur. Le service Forms vous permet de récupérer les données que l’utilisateur a saisies dans un formulaire interactif. Une fois les données récupérées, vous pouvez les traiter pour répondre aux besoins de votre entreprise. Par exemple, vous pouvez stocker les données dans une base de données, les envoyer à une autre application ou à un autre service, les fusionner dans une conception de formulaire, les afficher dans un navigateur web, etc.

Les données de formulaire sont envoyées au service Forms au format XML ou PDF, une option définie dans Designer. Un formulaire envoyé au format XML vous permet d’extraire des valeurs de données de champ individuelles. En d’autres termes, vous pouvez extraire la valeur de chaque champ de formulaire que l’utilisateur a saisi dans le formulaire. Un formulaire envoyé en tant que données PDF est une donnée binaire et non une donnée XML. Vous pouvez enregistrer le formulaire en tant que fichier PDF ou l’envoyer à un autre service. Si vous souhaitez extraire les données d’un formulaire envoyé au format XML, puis utiliser les données du formulaire pour créer un document PDF, appelez une autre opération AEM Forms. (Voir [Créer des documents PDF avec des données XML envoyées](/help/forms/developing/creating-pdf-documents-submitted-xml.md))

Le diagramme suivant montre les données envoyées à une servlet Java nommée `HandleData` à partir d’un formulaire interactif affiché dans un navigateur web.

![hs_hs_handlesubmit](assets/hs_hs_handlesubmit.png)

Le tableau suivant explique les étapes du diagramme.

<table>
 <thead>
  <tr>
   <th><p>Étape</p></th>
   <th><p>Description</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>1</p></td>
   <td><p>Un utilisateur remplit un formulaire interactif et clique sur le bouton Envoyer du formulaire.</p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>Les données sont envoyées à la servlet Java <code>HandleData</code> sous forme de données XML.</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>La servlet Java <code>HandleData</code> contient la logique d’application pour récupérer les données.</p></td>
  </tr>
 </tbody>
</table>

## Gérer les données XML envoyées {#handling-submitted-xml-data}

Lorsque les données de formulaire sont envoyées au format XML, vous pouvez récupérer les données XML qui représentent les données envoyées. Tous les champs de formulaire apparaissent sous la forme de nœuds dans un schéma XML. Les valeurs de nœud correspondent aux valeurs que l’utilisateur a renseignées. Prenons l’exemple d’un formulaire de prêt dans lequel chaque champ du formulaire apparaît comme un nœud au sein des données XML. La valeur de chaque nœud correspond à la valeur qu’un utilisateur renseigne. Supposons qu’un utilisateur renseigne le formulaire de prêt avec les données affichées dans le formulaire suivant.

![hs_hs_loanformdata](assets/hs_hs_loanformdata.png)

L’illustration suivante présente les données XML correspondantes récupérées à l’aide de l’API client du service Forms.

![hs_hs_loandata](assets/hs_hs_loandata.png)

Les champs du formulaire de prêt. Ces valeurs peuvent être récupérées 
à l’aide des classes XML Java.

>[!NOTE]
>
>La conception de formulaire doit être configurée correctement dans Designer pour que les données soient envoyées sous forme de données XML. Pour configurer correctement la conception de formulaire de sorte qu’elle envoie des données XML, assurez-vous que le bouton Envoyer situé sur la conception de formulaire est défini pour envoyer des données XML. Pour plus d’informations sur la définition du bouton Envoyer pour envoyer des données XML, voir [AEM Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63_fr).

## Gérer des données PDF envoyées {#handling-submitted-pdf-data}

Prenons l’exemple d’une application web qui appelle le service Forms. Une fois que le service Forms a rendu un formulaire PDF interactif dans un navigateur web client, l’utilisateur l’a rempli et l’a renvoyé en tant que données PDF. Lorsque le service Forms reçoit les données PDF, il peut les envoyer à un autre service ou les enregistrer en tant que fichier PDF. Le diagramme suivant illustre le flux logique de l’application.

![hs_hs_savingforms](assets/hs_hs_savingforms.png)

Le tableau suivant décrit les étapes de ce diagramme.

<table>
 <thead>
  <tr>
   <th><p>Étape</p></th>
   <th><p>Description</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>1</p></td>
   <td><p>Une page web contient un lien qui accède à une servlet Java qui appelle le service Forms.</p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>Le service Forms effectue le rendu d’un formulaire PDF interactif dans le navigateur web client.</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>L’utilisateur remplit un formulaire interactif et clique sur un bouton d’envoi. Le formulaire est renvoyé au service Forms en tant que données PDF. Cette option est définie dans Designer.</p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>Le service Forms enregistre les données PDF sous la forme d’un fichier PDF. </p></td>
  </tr>
 </tbody>
</table>

## Gérer les données UTF-16 de l’URL envoyées {#handling-submitted-url-utf-16-data}

Si les données de formulaire sont envoyées sous la forme de données UTF-16 d’URL, l’ordinateur client nécessite Adobe Reader, Acrobat 8.1 ou une version ultérieure. En outre, si la conception de formulaire contient un bouton d’envoi contenant des données codées URL (HTTP Post) et que l’option de codage des données est UTF-16, la conception de formulaire doit être modifiée dans un éditeur de texte tel que le Bloc-notes. Vous pouvez définir l’option de codage sur `UTF-16LE` ou `UTF-16BE` pour le bouton d’envoi. Designer ne fournit pas cette fonctionnalité.

>[!NOTE]
>
>Pour plus d’informations sur le service Forms, voir [Référence des services pour AEM Forms](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

## Résumé des étapes {#summary-of-steps}

Pour gérer les formulaires envoyés, effectuez les tâches suivantes :

1. Incluez les fichiers de projet.
1. Créez un objet API client Forms.
1. Récupérez les données de formulaire.
1. Déterminez si l’envoi du formulaire contient des pièces jointes.
1. Traitez les données envoyées.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

**Créer un objet API client Forms**

Avant d’effectuer par programmation une opération d’API client de service Forms, vous devez créer un client de service Forms. Si vous utilisez l’API Java, créez un objet `FormsServiceClient`. Si vous utilisez l’API Web Service Forms, créez un objet `FormsService`.

**Récupérer des données de formulaire**

Pour récupérer les données de formulaire envoyées, vous devez appeler la méthode `processFormSubmission` de l’objet `FormsServiceClient`. Lorsque vous appelez cette méthode, vous devez spécifier le type de contenu du formulaire envoyé. Lorsque des données sont envoyées d’un navigateur web client au service Forms, elles peuvent être envoyées au format XML ou PDF. Pour récupérer les données saisies dans les champs du formulaire, les données peuvent être envoyées au format XML.

Vous pouvez également récupérer les champs de formulaire d’un formulaire envoyé en tant que données PDF en définissant les options d’exécution suivantes :

* Transmettez la valeur suivante à la méthode `processFormSubmission` en tant que paramètre de type de contenu : `CONTENT_TYPE=application/pdf`.
* Définissez la valeur `PDFToXDP` de l’objet `RenderOptionsSpec` sur `true`.
* Définissez la valeur `ExportDataFormat` de l’objet `RenderOptionsSpec` sur `XMLData`.

Vous spécifiez le type de contenu du formulaire envoyé lorsque vous appelez la méthode `processFormSubmission`. La liste suivante spécifie les valeurs de type de contenu applicables :

* **text/xml** : représente le type de contenu à utiliser lorsqu’un formulaire PDF envoie les données de formulaire au format XML.
* **application/x-www-form-urlencoded** : représente le type de contenu à utiliser lorsqu’un formulaire HTML envoie des données au format XML.
* **application/pdf** : représente le type de contenu à utiliser lorsqu’un formulaire PDF envoie des données en tant que PDF.

>[!NOTE]
>
>Vous remarquerez qu’il existe trois démarrages rapides correspondants associés à la section Gestion des formulaires envoyés. Le guide de gestion des formulaires PDF envoyés en tant que PDF à l’aide du démarrage rapide de l’API Java explique comment gérer les données de PDF envoyées. Le type de contenu spécifié dans ce démarrage rapide est `application/pdf`.. Le guide de gestion des formulaires PDF envoyés au format XML à l’aide du démarrage rapide de l’API Java explique comment gérer les données XML envoyées à partir d’un formulaire PDF. Le type de contenu spécifié dans ce démarrage rapide est `text/xml`. De même, le guide de gestion des formulaires HTML envoyés au format XML à l’aide du démarrage rapide de l’API Java montre comment gérer les données XML envoyées à partir d’un formulaire HTML. Le type de contenu spécifié dans ce démarrage rapide est application/x-www-form-urlencoded.

Vous récupérez les données de formulaire qui ont été publiées sur le service Forms et déterminez leur statut de traitement. En d’autres termes, lorsque les données sont envoyées au service Forms, cela ne signifie pas nécessairement que le service Forms a terminé le traitement des données et qu’elles sont prêtes à être traitées. Par exemple, les données peuvent être envoyées au service Forms afin qu’un calcul puisse être effectué. Une fois le calcul terminé, le formulaire est rendu à l’utilisateur avec les résultats du calcul affichés. Avant de traiter les données envoyées, il est recommandé de déterminer si le service Forms a terminé le traitement des données.

Le service Forms renvoie les valeurs suivantes pour indiquer s’il a terminé le traitement des données :

* **0 (Envoyer) :** les données envoyées sont prêtes à être traitées.
* **1 (Calculer) :** le service Forms a effectué une opération de calcul sur les données et les résultats doivent être générés et remis à l’utilisateur.
* **2 (Valider) :** le service Forms a validé les données de formulaire et les résultats doivent être générés et remis à l’utilisateur.
* **3 (Suivant) :** la page actuelle a été modifiée avec des résultats qui doivent être écrits dans l’application cliente.
* **4 (Précédent**) : la page actuelle a été modifiée avec des résultats qui doivent être écrits dans l’application cliente.

>[!NOTE]
>
>Les calculs et validations doivent être générés et remis à l’utilisateur. (Voir [Calcul des données de formulaire](/help/forms/developing/calculating-form-data.md#calculating-form-data).

**Déterminer si l’envoi du formulaire contient des pièces jointes**

Les formulaires envoyés au service Forms peuvent contenir des pièces jointes. Par exemple, à l’aide du volet de pièces jointes intégré d’Acrobat, un utilisateur peut sélectionner des pièces jointes à envoyer avec le formulaire. Un utilisateur peut également sélectionner des pièces jointes à l’aide d’une barre d’outils HTML générée avec un fichier HTML.

Après avoir déterminé si un formulaire contient des pièces jointes, vous pouvez traiter les données. Par exemple, vous pouvez enregistrer la pièce jointe dans le système de fichiers local.

>[!NOTE]
>
>Le formulaire doit être envoyé en tant que données PDF pour récupérer les pièces jointes. Si le formulaire est envoyé en tant que données XML, les pièces jointes ne sont pas envoyées.

**Traiter les données envoyées**

Selon le type de contenu des données envoyées, vous pouvez extraire des valeurs de champ de formulaire individuel des données XML envoyées ou enregistrer les données PDF envoyées sous forme de fichier PDF (ou les envoyer à un autre service). Pour extraire des champs de formulaire individuels, convertissez les données XML envoyées en une source de données XML, puis récupérez les valeurs de source de données XML à l’aide de classes `org.w3c.dom`.

**Voir également**

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Démarrages rapides de l’API Forms Service](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Transmettre des documents au service Forms](/help/forms/developing/passing-documents-forms-service.md)

[Créer des applications web qui génèrent des formulaires](/help/forms/developing/creating-web-applications-renders-forms.md)

## Gérer les formulaires envoyés à l’aide de l’API Java {#handle-submitted-forms-using-the-java-api}

Gérez un formulaire envoyé à l’aide de l’API Forms (Java) :

1. Inclure les fichiers du projet

   Incluez les fichiers clients JAR, tels qu’adobe-forms-client.jar, dans votre projet Java Classpath.

1. Créer un objet API Forms client

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `FormsServiceClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`.

1. Récupérer les données de formulaire

   * Pour récupérer les données de formulaire publiées sur un servlet Java, créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en appelant la méthode `getInputStream` de l’objet `javax.servlet.http.HttpServletResponse` depuis l’intérieur du constructeur.
   * Créez un objet `RenderOptionsSpec` en utilisant son constructeur. Définissez la valeur du paramètre régional en appelant la méthode `setLocale` de l’objet `RenderOptionsSpec` et en transmettant d’une valeur de chaîne spécifiant la valeur du paramètre régional.

   >[!NOTE]
   >
   >Vous pouvez demander au service Forms de créer des données XDP ou XML à partir du contenu du PDF envoyé en appelant la méthode `setPDF2XDP` de l’objet `RenderOptionsSpec` et en transmettant `true` ainsi qu’en appelant `setXMLData` et en transmettant `true`. Vous pouvez ensuite appeler la méthode `getOutputXML` de l’objet `FormsResult` pour récupérer les données XML correspondant aux données XDP/XML. (L’objet `FormsResult` est renvoyé par la méthode `processFormSubmission`, qui est expliquée dans la sous-étape suivante.)

   * Appelez la méthode `processFormSubmission` de l’objet `FormsServiceClient` et transmettez les valeurs suivantes :

      * Objet `com.adobe.idp.Document` contenant les données de formulaire.
      * Une valeur de chaîne qui indique les variables d’environnement, y compris tous les en-têtes HTTP pertinents. Spécifiez le type de contenu à gérer. Pour gérer les données XML, spécifiez la valeur de chaîne suivante pour ce paramètre : `CONTENT_TYPE=text/xml`. Pour gérer les données PDF, spécifiez la valeur de chaîne suivante pour ce paramètre : `CONTENT_TYPE=application/pdf`.
      * Valeur de chaîne spécifiant la valeur d’en-tête `HTTP_USER_AGENT`, par exemple `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`. Cette valeur de paramètre est facultative.
      * Objet `RenderOptionsSpec` stockant les options d’exécution.

     La méthode `processFormSubmission` renvoie un objet `FormsResult` contenant les résultats de l’envoi du formulaire.

   * Déterminez si le service Forms a terminé le traitement des données de formulaire en appelant la méthode `getAction` de l’objet `FormsResult`. Si cette méthode renvoie la valeur `0`, les données sont prêtes à être traitées.

1. Déterminer si le formulaire envoyé contient des pièces jointes

   * Appelez la méthode `getAttachments` de l’objet `FormsResult`. Cette méthode renvoie un objet `java.util.List` contenant les fichiers qui ont été envoyés avec le formulaire.
   * Effectuez une itération à l’aide de l’objet `java.util.List` pour déterminer s’il existe des pièces jointes. S’il existe des pièces jointes, chaque élément est une instance `com.adobe.idp.Document`. Vous pouvez enregistrer les pièces jointes en appelant la méthode `copyToFile` de l’objet `com.adobe.idp.Document` et en transmettant un objet `java.io.File`.

   >[!NOTE]
   >
   >Cette étape ne s’applique que si le formulaire est envoyé en tant que PDF.

1. Traiter les données envoyées

   * Si le type de contenu des données est `application/vnd.adobe.xdp+xml` ou `text/xml`, créez une logique d’application pour récupérer les valeurs des données XML.

      * Créez un objet `com.adobe.idp.Document` en appelant la méthode `getOutputContent` de l’objet `FormsResult`.
      * Créez un objet `java.io.InputStream` en appelant le constructeur `java.io.DataInputStream` et en transmettant l’objet `com.adobe.idp.Document`.
      * Créez un objet `org.w3c.dom.DocumentBuilderFactory` en appelant la méthode `newInstance` de l’objet statique `org.w3c.dom.DocumentBuilderFactory`.
      * Créez un objet `org.w3c.dom.DocumentBuilder` en appelant la méthode `newDocumentBuilder` de l’objet `org.w3c.dom.DocumentBuilderFactory`.
      * Créez un objet `org.w3c.dom.Document` en appelant la méthode `parse` de l’objet `org.w3c.dom.DocumentBuilder` et en transmettant l’objet `java.io.InputStream`.
      * Récupérez la valeur de chaque nœud dans le document XML. Une façon d’accomplir cette tâche est de créer une méthode personnalisée qui accepte deux paramètres : l’objet `org.w3c.dom.Document` et le nom du nœud dont vous souhaitez récupérer la valeur. Cette méthode renvoie une valeur de chaîne représentant la valeur du nœud. Dans l’exemple de code qui suit ce processus, cette méthode personnalisée est appelée `getNodeText`. Le corps de cette méthode est affiché.

   * Si le type de contenu des données est `application/pdf`, créez une logique d’application pour enregistrer les données PDF envoyées sous forme de fichier PDF.

      * Créez un objet `com.adobe.idp.Document` en appelant la méthode `getOutputContent` de l’objet `FormsResult`.
      * Créez un objet `java.io.File` en utilisant son constructeur public. Veillez à spécifier PDF comme extension de nom du fichier.
      * Renseignez le fichier PDF en appelant la méthode `copyToFile` de l’objet `com.adobe.idp.Document` et en transmettant l’objet `java.io.File`.

**Voir également**

[Démarrage rapide (mode SOAP) : gérer des formulaires PDF envoyés au format XML à l’aide de l’API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-handling-pdf-forms-submitted-as-xml-using-the-java-api)

[Démarrage rapide (mode SOAP) : gérer des formulaires HTML envoyés au format XML à l’aide de l’API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-handling-html-forms-submitted-as-xml-using-the-java-api)

[Démarrage rapide (mode SOAP) : gérer des formulaires PDF envoyés en tant que PDF à l’aide de l’API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-handling-pdf-forms-submitted-as-pdf-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Gérer les données PDF envoyées en utilisant l’API du service web {#handle-submitted-pdf-data-using-the-web-service-api}

Gérez un formulaire envoyé en utilisant l’API des formulaires (service Web) :

1. Inclure les fichiers du projet

   * Créez des classes proxy Java qui utilisent le service WSDL de Forms.
   * Incluez les classes proxy Java dans le chemin d’accès de classe.

1. Créer un objet API Forms client

   Créez un objet `FormsService` et définissez les valeurs d’authentification.

1. Récupérer les données de formulaire

   * Pour récupérer les données de formulaire qui ont été publiées sur un servlet Java, créez un objet `BLOB` en utilisant son constructeur.
   * Créez un objet `java.io.InputStream` en appelant la méthode `getInputStream` de l’objet `javax.servlet.http.HttpServletResponse`.
   * Créez un objet `java.io.ByteArrayOutputStream` en utilisant son constructeur et en transmettant la longueur de l’objet `java.io.InputStream`.
   * Copiez le contenu de l’objet `java.io.InputStream` dans l’objet `java.io.ByteArrayOutputStream`.
   * Créez un tableau d’octets en appelant la méthode `toByteArray` de l’objet `java.io.ByteArrayOutputStream`.
   * Renseignez l’objet `BLOB` en appelant sa méthode `setBinaryData` et en transmettant le tableau d’octets comme argument.
   * Créez un objet `RenderOptionsSpec` en utilisant son constructeur. Définissez la valeur du paramètre régional en appelant la méthode `setLocale` de l’objet `RenderOptionsSpec` et en transmettant une valeur de chaîne qui spécifie la valeur du paramètre régional.
   * Appelez la méthode `processFormSubmission` de l’objet `FormsService` et transmettez les valeurs suivantes :

      * Objet `BLOB` contenant les données de formulaire.
      * Une valeur de chaîne qui indique les variables d’environnement, y compris tous les en-têtes HTTP pertinents. Spécifiez le type de contenu à gérer. Pour gérer les données XML, spécifiez la valeur de chaîne suivante pour ce paramètre : `CONTENT_TYPE=text/xml`. Pour gérer les données PDF, spécifiez la valeur de chaîne suivante pour ce paramètre : `CONTENT_TYPE=application/pdf`.
      * Une valeur de chaîne qui spécifie la valeur de l’en-tête `HTTP_USER_AGENT`, par exemple, `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
      * Un objet `RenderOptionsSpec` qui stocke les options d’exécution.
      * Un objet `BLOBHolder` vide qui est renseigné par la méthode.
      * Un objet `javax.xml.rpc.holders.StringHolder` vide qui est renseigné par la méthode.
      * Un objet `BLOBHolder` vide qui est renseigné par la méthode.
      * Un objet `BLOBHolder` vide qui est renseigné par la méthode.
      * Un objet `javax.xml.rpc.holders.ShortHolder` vide qui est renseigné par la méthode.
      * Un objet `MyArrayOf_xsd_anyTypeHolder` vide qui est renseigné par la méthode. Ce paramètre est utilisé pour stocker les pièces jointes envoyées avec le formulaire.
      * Un objet `FormsResultHolder` vide qui est renseigné par la méthode avec le formulaire envoyé.

     La méthode `processFormSubmission` renseigne le paramètre `FormsResultHolder` avec les résultats de l’envoi du formulaire.

   * Déterminez si le service Forms a fini de traiter les données du formulaire en appelant la méthode `getAction` de l’objet `FormsResult`. Si cette méthode renvoie la valeur `0`, les données du formulaire sont prêtes à être traitées. Vous pouvez obtenir un objet `FormsResult` en récupérant la valeur du membre de données `value` de l’objet `FormsResultHolder`.

1. Déterminer si le formulaire envoyé contient des pièces jointes

   Obtenez la valeur du membre de données `value` de l’objet `MyArrayOf_xsd_anyTypeHolder` (l’objet `MyArrayOf_xsd_anyTypeHolder` a été transmis à la méthode `processFormSubmission`). Ce membre de données renvoie un tableau de `Objects`. Chaque élément du tableau `Object` est un `Object` qui correspond aux fichiers qui ont été envoyés avec le formulaire. Vous pouvez obtenir chaque élément du tableau et le convertir en un objet `BLOB`.

1. Traiter les données envoyées

   * Si le type de contenu des données est `application/vnd.adobe.xdp+xml` ou `text/xml`, créez une logique d’application pour récupérer les valeurs des données XML.

      * Créez un objet `BLOB` en appelant la méthode `getOutputContent` de l’objet `FormsResult`.
      * Créez un tableau d’octets en appelant la méthode `getBinaryData` de l’objet `BLOB`.
      * Créez un objet `java.io.InputStream` en appelant le constructeur `java.io.ByteArrayInputStream` et en transmettant le tableau d’octets.
      * Créez un objet `org.w3c.dom.DocumentBuilderFactory` en appelant la méthode `newInstance` de l’objet statique `org.w3c.dom.DocumentBuilderFactory`.
      * Créez un objet `org.w3c.dom.DocumentBuilder` en appelant la méthode `newDocumentBuilder` de l’objet `org.w3c.dom.DocumentBuilderFactory`.
      * Créez un objet `org.w3c.dom.Document` en appelant la méthode `parse` de l’objet `org.w3c.dom.DocumentBuilder` et en transmettant l’objet `java.io.InputStream`.
      * Récupérez la valeur de chaque nœud dans le document XML. Une façon d’accomplir cette tâche est de créer une méthode personnalisée qui accepte deux paramètres : l’objet `org.w3c.dom.Document` et le nom du nœud dont vous souhaitez récupérer la valeur. Cette méthode renvoie une valeur de chaîne représentant la valeur du nœud. Dans l’exemple de code qui suit ce processus, cette méthode personnalisée est appelée `getNodeText`. Le corps de cette méthode est affiché.

   * Si le type de contenu des données est `application/pdf`, créez une logique d’application pour enregistrer les données PDF envoyées sous forme de fichier PDF.

      * Créez un objet `BLOB` en appelant la méthode `getOutputContent` de l’objet `FormsResult`.
      * Créez un tableau d’octets en appelant la méthode `getBinaryData` de l’objet `BLOB`.
      * Créez un objet `java.io.File` en utilisant son constructeur public. Veillez à spécifier PDF comme extension de nom du fichier.
      * Créez un objet `java.io.FileOutputStream` en utilisant son constructeur et en transmettant l’objet `java.io.File`. 
      * Renseignez le fichier PDF en appelant la méthode `write` de l’objet `java.io.FileOutputStream` et en transmettant le tableau d’octets.

**Voir également**

[Appeler AEM Forms en utilisant le codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
