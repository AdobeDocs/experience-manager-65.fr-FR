---
title: Gestion des formulaires envoyés
seo-title: Gestion des formulaires envoyés
description: 'null'
seo-description: 'null'
uuid: 673b28f1-f023-4da8-a6a0-c5ff921c5f5d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 3d838027-6bde-4a71-a428-4d5102f7d799
translation-type: tm+mt
source-git-commit: 7cbe3e94eddb81925072f68388649befbb027e6d

---


# Gestion des formulaires envoyés {#handling-submitted-forms}

Les applications Web qui permettent à un utilisateur de remplir des formulaires interactifs nécessitent que les données soient renvoyées au serveur. Le service Forms vous permet de récupérer les données saisies par l’utilisateur dans un formulaire interactif. Une fois les données récupérées, vous pouvez les traiter en fonction des besoins de votre entreprise. Par exemple, vous pouvez stocker les données dans une base de données, envoyer les données à une autre application, envoyer les données à un autre service, fusionner les données dans une conception de formulaire, afficher les données dans un navigateur Web, etc.

Les données de formulaire sont envoyées au service Forms sous forme de données XML ou PDF, une option définie dans Designer. Un formulaire envoyé au format XML vous permet d’extraire des valeurs de données de champ individuelles. En d’autres termes, vous pouvez extraire la valeur de chaque champ de formulaire saisi par l’utilisateur dans le formulaire. Un formulaire envoyé au format PDF est constitué de données binaires et non de données XML. Vous pouvez enregistrer le formulaire au format PDF ou l’envoyer à un autre service. Si vous souhaitez extraire des données d’un formulaire envoyé au format XML, puis utiliser les données du formulaire pour créer un document PDF, appelez une autre opération AEM Forms. (voir [Création de documents PDF avec des données](/help/forms/developing/creating-pdf-documents-submitted-xml.md)XML envoyées).

Le diagramme suivant montre les données envoyées à une servlet Java nommée `HandleData` à partir d’un formulaire interactif affiché dans un navigateur Web.

![hs_hs_handlesubmit](assets/hs_hs_handlesubmit.png)

Le tableau suivant décrit les étapes du diagramme.

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
   <td><p>Les données sont envoyées au servlet <code>HandleData</code> Java sous forme de données XML.</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>Le servlet <code>HandleData</code> Java contient la logique d’application pour récupérer les données.</p></td>
  </tr>
 </tbody>
</table>

## Gestion des données XML envoyées {#handling-submitted-xml-data}

Lorsque des données de formulaire sont envoyées au format XML, vous pouvez récupérer des données XML qui représentent les données envoyées. Tous les champs de formulaire apparaissent sous la forme de noeuds dans un schéma XML. Les valeurs de noeud correspondent aux valeurs que l’utilisateur a renseignées. Prenons l’exemple d’un formulaire de prêt dans lequel chaque champ du formulaire apparaît comme un noeud dans les données XML. La valeur de chaque noeud correspond à la valeur qu’un utilisateur remplit. Supposons qu’un utilisateur renseigne le formulaire de prêt avec les données affichées dans le formulaire suivant.

![hs_hs_loanformdata](assets/hs_hs_loanformdata.png)

L’illustration suivante présente les données XML correspondantes récupérées à l’aide de l’API Client du service Forms.

![hs_hs_loandata](assets/hs_hs_loandata.png)

Champs du formulaire de prêt. Ces valeurs peuvent être récupérées à l’aide de classes XML Java.

>[!NOTE]
>
>La conception de formulaire doit être correctement configurée dans Designer pour que les données soient envoyées sous forme de données XML. Pour configurer correctement la conception de formulaire afin d’envoyer des données XML, assurez-vous que le bouton Envoyer situé sur la conception de formulaire est configuré pour envoyer des données XML. Pour plus d’informations sur la définition du bouton Envoyer pour envoyer des données XML, voir [AEM Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63).

## Gestion des données PDF envoyées {#handling-submitted-pdf-data}

Prenons l’exemple d’une application Web qui appelle le service Forms. Une fois que le service Forms a rendu un formulaire PDF interactif à un navigateur Web client, l’utilisateur remplit le formulaire et l’envoie en tant que données PDF. Lorsque le service Forms reçoit les données PDF, il peut envoyer les données PDF à un autre service ou les enregistrer dans un fichier PDF. Le diagramme suivant illustre le flux logique de l’application.

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
   <td><p>Une page Web contient un lien qui accède à un servlet Java qui appelle le service Forms.</p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>Le service Forms génère un formulaire PDF interactif dans le navigateur Web client.</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>L’utilisateur remplit un formulaire interactif et clique sur un bouton d’envoi. Le formulaire est renvoyé au service Forms sous forme de données PDF. Cette option est définie dans Designer.</p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>Le service Forms enregistre les données PDF dans un fichier PDF. </p></td>
  </tr>
 </tbody>
</table>

## Gestion des données UTF-16 d’URL envoyées {#handling-submitted-url-utf-16-data}

Si les données de formulaire sont envoyées sous forme de données UTF-16 URL, l’ordinateur client nécessite Adobe Reader ou Acrobat 8.1 ou version ultérieure. De même, si la conception de formulaire contient un bouton d’envoi contenant des données codées URL (HTTP Post) et que l’option de codage des données est UTF-16, la conception de formulaire doit être modifiée dans un éditeur de texte tel que le Bloc-notes. Vous pouvez définir l’option de codage sur `UTF-16LE` ou `UTF-16BE` pour le bouton d’envoi. Designer ne fournit pas cette fonctionnalité.

>[!NOTE]
>
>For more information about the Forms service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Résumé des étapes {#summary-of-steps}

Pour gérer les formulaires envoyés, effectuez les tâches suivantes :

1. Incluez des fichiers de projet.
1. Créez un objet API Client Forms.
1. Récupérez les données de formulaire.
1. Déterminez si l’envoi du formulaire contient des pièces jointes.
1. Traitez les données envoyées.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

**Création d’un objet API du client Forms**

Avant de pouvoir exécuter par programmation une opération d’API Client de service Forms, vous devez créer un client de service Forms. Si vous utilisez l’API Java, créez un `FormsServiceClient` objet. Si vous utilisez l’API du service Web de Forms, créez un `FormsService` objet.

**Récupération des données de formulaire**

Pour récupérer les données de formulaire envoyées, vous appelez la `FormsServiceClient` `processFormSubmission` méthode de l’objet. Lorsque vous appelez cette méthode, vous devez spécifier le type de contenu du formulaire envoyé. Lorsque des données sont envoyées d’un navigateur Web client au service Forms, elles peuvent être envoyées sous forme de données XML ou PDF. Pour récupérer les données saisies dans les champs du formulaire, les données peuvent être envoyées sous forme de données XML.

Vous pouvez également récupérer les champs de formulaire d’un formulaire envoyé au format PDF en définissant les options d’exécution suivantes :

* Transmettez la valeur suivante à la `processFormSubmission` méthode en tant que paramètre de type de contenu : `CONTENT_TYPE=application/pdf`.
* Définissez la `RenderOptionsSpec` `PDFToXDP` valeur de l’objet sur `true`
* Définissez la `RenderOptionsSpec` `ExportDataFormat` valeur de l’objet sur `XMLData`

Vous spécifiez le type de contenu du formulaire envoyé lorsque vous appelez la `processFormSubmission` méthode. La liste suivante spécifie les valeurs de type de contenu applicables :

* **text/xml**: Représente le type de contenu à utiliser lorsqu’un formulaire PDF envoie des données de formulaire au format XML.
* **application/x-www-form-urlencoded**: Représente le type de contenu à utiliser lorsqu’un formulaire HTML envoie des données au format XML.
* **application/pdf**: Représente le type de contenu à utiliser lorsqu’un formulaire PDF envoie des données au format PDF.

>[!NOTE]
>
>Vous remarquerez qu’il existe trois démarrages rapides correspondants associés à la section Gestion des formulaires envoyés. Le guide de gestion des formulaires PDF envoyés au format PDF à l’aide de l’API Java montre comment gérer les données PDF envoyées. Le type de contenu spécifié dans ce démarrage rapide est `application/pdf`. Le guide de gestion des formulaires PDF envoyés au format XML à l’aide de l’API Java montre comment gérer les données XML envoyées à partir d’un formulaire PDF. Le type de contenu spécifié dans ce démarrage rapide est `text/xml`. De même, la gestion des formulaires HTML envoyés en tant que formulaires XML à l’aide du démarrage rapide de l’API Java montre comment gérer les données XML envoyées à partir d’un formulaire HTML. Le type de contenu spécifié dans ce démarrage rapide est application/x-www-form-urlencoded.

Vous récupérez les données de formulaire qui ont été publiées dans le service Forms et déterminez leur état de traitement. En d’autres termes, lorsque des données sont envoyées au service Forms, cela ne signifie pas nécessairement que le service Forms a terminé le traitement des données et que les données sont prêtes à être traitées. Par exemple, les données peuvent être envoyées au service Forms pour qu’un calcul puisse être effectué. Une fois le calcul terminé, le formulaire est rendu à l’utilisateur avec les résultats affichés. Avant de traiter les données envoyées, il est recommandé de déterminer si le service Forms a terminé le traitement des données.

Le service Forms renvoie les valeurs suivantes pour indiquer s’il a terminé le traitement des données :

* **** 0 (envoi) : Les données envoyées sont prêtes à être traitées.
* **** 1 (Calculer) : Le service Forms a effectué une opération de calcul sur les données et les résultats doivent être rendus à l’utilisateur.
* **** 2 (Valider) : Le service Forms a validé les données de formulaire et les résultats doivent être rendus à l’utilisateur.
* **** 3 (Suivant) : La page active a changé avec les résultats qui doivent être écrits dans l’application cliente.
* **4 (Précédent**) : La page active a changé avec les résultats qui doivent être écrits dans l’application cliente.

>[!NOTE]
>
>Les calculs et validations doivent être rendus à l’utilisateur. (Voir [Calcul des données]de formulaire (/help/forms/development/render-forms-render-forms-calculate-form-data-calculate-form-form-calculate-form.md#calculate-form-data)*.)*

**Déterminer si l’envoi du formulaire contient des pièces jointes**

Les formulaires envoyés au service Forms peuvent contenir des pièces jointes. Par exemple, à l’aide du volet de pièces jointes intégré d’Acrobat, un utilisateur peut sélectionner des pièces jointes à envoyer avec le formulaire. En outre, un utilisateur peut également sélectionner des pièces jointes à l’aide d’une barre d’outils HTML générée avec un fichier HTML.

Après avoir déterminé si un formulaire contient des pièces jointes, vous pouvez traiter les données. Par exemple, vous pouvez enregistrer le fichier joint dans le système de fichiers local.

>[!NOTE]
>
>Le formulaire doit être envoyé au format PDF pour récupérer les pièces jointes. Si le formulaire est envoyé sous forme de données XML, les pièces jointes ne sont pas envoyées.

**Traiter les données envoyées**

Selon le type de contenu des données envoyées, vous pouvez extraire des valeurs de champ de formulaire individuelles des données XML envoyées ou enregistrer les données PDF envoyées sous forme de fichier PDF (ou les envoyer à un autre service). Pour extraire des champs de formulaire individuels, convertissez les données XML envoyées en source de données XML, puis récupérez les valeurs de source de données XML à l’aide de `org.w3c.dom` classes.

**Voir également**

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Démarrage rapide de l’API du service Forms](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Transmission de documents au service Forms](/help/forms/developing/passing-documents-forms-service.md)

[Création d&#39;applications Web qui renvoient des formulaires](/help/forms/developing/creating-web-applications-renders-forms.md)

## Gestion des formulaires envoyés à l’aide de l’API Java {#handle-submitted-forms-using-the-java-api}

Gérez un formulaire envoyé à l’aide de l’API Forms (Java) :

1. Inclure les fichiers de projet

   Incluez des fichiers JAR client, tels que adobe-forms-client.jar, dans le chemin de classe de votre projet Java.

1. Création d’un objet API du client Forms

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Create an `FormsServiceClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. Récupération des données de formulaire

   * Pour récupérer les données de formulaire publiées sur un servlet Java, créez un `com.adobe.idp.Document` objet à l’aide de son constructeur et appelez la `javax.servlet.http.HttpServletResponse` `getInputStream` méthode de l’objet depuis le constructeur.
   * Créez un objet `RenderOptionsSpec` en utilisant son constructeur. Définissez la valeur du paramètre régional en appelant la `RenderOptionsSpec` `setLocale` méthode de l’objet et en transmettant une valeur de chaîne qui spécifie la valeur du paramètre régional.
   >[!NOTE]
   >
   >Vous pouvez demander au service Forms de créer des données XDP ou XML à partir du contenu PDF envoyé en appelant la `RenderOptionsSpec` méthode de l’ `setPDF2XDP` objet et en transmettant `true` et en appelant `setXMLData` et en transmettant `true`. Vous pouvez ensuite appeler la `FormsResult` `getOutputXML` méthode de l’objet pour récupérer les données XML qui correspondent aux données XDP/XML. (L’ `FormsResult` objet est renvoyé par la `processFormSubmission` méthode, qui est expliquée à l’étape suivante.)

   * Appelez la méthode `FormsServiceClient` `processFormSubmission` de l’objet et transmettez les valeurs suivantes :

      * Objet `com.adobe.idp.Document` contenant les données du formulaire.
      * Valeur de chaîne qui spécifie les variables d’environnement, y compris tous les en-têtes HTTP appropriés. Spécifiez le type de contenu à gérer. Pour gérer les données XML, spécifiez la valeur de chaîne suivante pour ce paramètre : `CONTENT_TYPE=text/xml`. Pour gérer les données PDF, spécifiez la valeur de chaîne suivante pour ce paramètre : `CONTENT_TYPE=application/pdf`.
      * Valeur de chaîne qui spécifie la valeur d’ `HTTP_USER_AGENT` en-tête, par exemple . `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`. Cette valeur de paramètre est facultative.
      * Objet `RenderOptionsSpec` qui stocke les options d’exécution.
      La `processFormSubmission` méthode renvoie un `FormsResult` objet contenant les résultats de l’envoi du formulaire.

   * Déterminez si le service Forms a terminé le traitement des données de formulaire en appelant la `FormsResult` `getAction` méthode de l’objet. Si cette méthode renvoie la valeur `0`, les données sont prêtes à être traitées.



1. Déterminer si l’envoi du formulaire contient des pièces jointes

   * Appelez la méthode `FormsResult` `getAttachments` de l’objet. Cette méthode renvoie un `java.util.List` objet contenant des fichiers qui ont été envoyés avec le formulaire.
   * Parcourez l’ `java.util.List` objet pour déterminer s’il existe des pièces jointes. S’il existe des pièces jointes, chaque élément est une `com.adobe.idp.Document` instance. Vous pouvez enregistrer les pièces jointes en appelant la `com.adobe.idp.Document` méthode de l’objet et en transmettant un `copyToFile` `java.io.File` objet.
   >[!NOTE]
   >
   >Cette étape s’applique uniquement si le formulaire est envoyé au format PDF.

1. Traiter les données envoyées

   * Si le type de contenu de données est `application/vnd.adobe.xdp+xml` ou `text/xml`, créez une logique d’application pour récupérer les valeurs de données XML.

      * Créez un `com.adobe.idp.Document` objet en appelant la `FormsResult` méthode de l’ `getOutputContent` objet.
      * Créez un `java.io.InputStream` objet en appelant le `java.io.DataInputStream` constructeur et en transmettant l’ `com.adobe.idp.Document` objet.
      * Créez un `org.w3c.dom.DocumentBuilderFactory` objet en appelant la `org.w3c.dom.DocumentBuilderFactory` `newInstance` méthode de l’objet statique.
      * Créez un `org.w3c.dom.DocumentBuilder` objet en appelant la `org.w3c.dom.DocumentBuilderFactory` méthode de l’ `newDocumentBuilder` objet.
      * Create an `org.w3c.dom.Document` object by invoking the `org.w3c.dom.DocumentBuilder` object’s `parse` method and passing the `java.io.InputStream` object.
      * Récupérez la valeur de chaque noeud dans le document XML. Pour ce faire, vous pouvez créer une méthode personnalisée qui accepte deux paramètres : l’ `org.w3c.dom.Document` objet et le nom du noeud dont vous souhaitez récupérer la valeur. Cette méthode renvoie une valeur de chaîne représentant la valeur du noeud. Dans l’exemple de code qui suit ce processus, cette méthode personnalisée est appelée `getNodeText`. Le corps de cette méthode est illustré.
   * Si le type de contenu de données est `application/pdf`défini, créez une logique d’application pour enregistrer les données PDF envoyées sous forme de fichier PDF.

      * Créez un `com.adobe.idp.Document` objet en appelant la `FormsResult` méthode de l’ `getOutputContent` objet.
      * Create a `java.io.File` object by using its public constructor. Veillez à spécifier PDF comme extension de nom de fichier.
      * Renseignez le fichier PDF en appelant la `com.adobe.idp.Document` méthode de l’objet et en transmettant l’ `copyToFile` `java.io.File` objet.


**Voir également**

[Démarrage rapide (mode SOAP) : Gestion des formulaires PDF envoyés au format XML à l’aide de l’API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-handling-pdf-forms-submitted-as-xml-using-the-java-api)

[Démarrage rapide (mode SOAP) : Gestion des formulaires HTML envoyés au format XML à l’aide de l’API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-handling-html-forms-submitted-as-xml-using-the-java-api)

[Démarrage rapide (mode SOAP) : Gestion des formulaires PDF envoyés au format PDF à l’aide de l’API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-handling-pdf-forms-submitted-as-pdf-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Gestion des données PDF envoyées à l’aide de l’API du service Web {#handle-submitted-pdf-data-using-the-web-service-api}

Gérez un formulaire envoyé à l’aide de l’API Forms (service Web) :

1. Inclure les fichiers de projet

   * Créez des classes de proxy Java qui utilisent le WSDL du service Forms.
   * Incluez les classes proxy Java dans le chemin de votre classe.

1. Création d’un objet API du client Forms

   Créez un `FormsService` objet et définissez des valeurs d’authentification.

1. Récupération des données de formulaire

   * Pour récupérer les données de formulaire publiées sur un servlet Java, créez un `BLOB` objet à l’aide de son constructeur.
   * Créez un `java.io.InputStream` objet en appelant la `javax.servlet.http.HttpServletResponse` méthode de l’ `getInputStream` objet.
   * Create a `java.io.ByteArrayOutputStream` object by using its constructor and passing the length of the `java.io.InputStream` object.
   * Copiez le contenu de l’ `java.io.InputStream` objet dans l’ `java.io.ByteArrayOutputStream` objet.
   * Créez un tableau d’octets en appelant la `java.io.ByteArrayOutputStream` `toByteArray` méthode de l’objet.
   * Renseignez l’ `BLOB` objet en appelant sa `setBinaryData` méthode et en transmettant le tableau d’octets comme argument.
   * Créez un objet `RenderOptionsSpec` en utilisant son constructeur. Définissez la valeur du paramètre régional en appelant la `RenderOptionsSpec` `setLocale` méthode de l’objet et en transmettant une valeur de chaîne qui spécifie la valeur du paramètre régional.
   * Appelez la méthode `FormsService` `processFormSubmission` de l’objet et transmettez les valeurs suivantes :

      * Objet `BLOB` contenant les données du formulaire.
      * Valeur de chaîne qui spécifie les variables d’environnement, y compris tous les en-têtes HTTP appropriés. Spécifiez le type de contenu à gérer. Pour gérer les données XML, spécifiez la valeur de chaîne suivante pour ce paramètre : `CONTENT_TYPE=text/xml`. Pour gérer les données PDF, spécifiez la valeur de chaîne suivante pour ce paramètre : `CONTENT_TYPE=application/pdf`.
      * Valeur de chaîne qui spécifie la valeur d’ `HTTP_USER_AGENT` en-tête ; par exemple, `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
      * Objet `RenderOptionsSpec` qui stocke les options d’exécution.
      * Objet vide `BLOBHolder` rempli par la méthode.
      * Objet vide `javax.xml.rpc.holders.StringHolder` rempli par la méthode.
      * Objet vide `BLOBHolder` rempli par la méthode.
      * Objet vide `BLOBHolder` rempli par la méthode.
      * Objet vide `javax.xml.rpc.holders.ShortHolder` rempli par la méthode.
      * Objet vide `MyArrayOf_xsd_anyTypeHolder` rempli par la méthode. Ce paramètre permet de stocker les pièces jointes envoyées avec le formulaire.
      * Objet vide `FormsResultHolder` rempli par la méthode avec le formulaire envoyé.
      La `processFormSubmission` méthode renseigne le `FormsResultHolder` paramètre avec les résultats de l’envoi du formulaire.

   * Déterminez si le service Forms a terminé le traitement des données de formulaire en appelant la `FormsResult` `getAction` méthode de l’objet. Si cette méthode renvoie la valeur `0`, les données du formulaire sont prêtes à être traitées. Vous pouvez obtenir un `FormsResult` objet en obtenant la valeur du membre `FormsResultHolder` de données de l’ `value` objet.


1. Déterminer si l’envoi du formulaire contient des pièces jointes

   Obtient la valeur du membre `MyArrayOf_xsd_anyTypeHolder` de données de l’ `value` objet (l’ `MyArrayOf_xsd_anyTypeHolder` objet a été transmis à la `processFormSubmission` méthode). Ce membre de données renvoie un tableau de `Objects`. Chaque élément du `Object` tableau est un élément `Object`qui correspond aux fichiers envoyés avec le formulaire. Vous pouvez obtenir chaque élément du tableau et le projeter dans un `BLOB` objet.

1. Traiter les données envoyées

   * Si le type de contenu de données est `application/vnd.adobe.xdp+xml` ou `text/xml`, créez une logique d’application pour récupérer les valeurs de données XML.

      * Créez un `BLOB` objet en appelant la `FormsResult` méthode de l’ `getOutputContent` objet.
      * Créez un tableau d’octets en appelant la `BLOB` `getBinaryData` méthode de l’objet.
      * Créez un `java.io.InputStream` objet en appelant le `java.io.ByteArrayInputStream` constructeur et en transmettant le tableau d’octets.
      * Créez un `org.w3c.dom.DocumentBuilderFactory` objet en appelant la `org.w3c.dom.DocumentBuilderFactory` `newInstance` méthode de l’objet statique.
      * Créez un `org.w3c.dom.DocumentBuilder` objet en appelant la `org.w3c.dom.DocumentBuilderFactory` méthode de l’ `newDocumentBuilder` objet.
      * Create an `org.w3c.dom.Document` object by invoking the `org.w3c.dom.DocumentBuilder` object’s `parse` method and passing the `java.io.InputStream` object.
      * Récupérez la valeur de chaque noeud dans le document XML. Pour ce faire, vous pouvez créer une méthode personnalisée qui accepte deux paramètres : l’ `org.w3c.dom.Document` objet et le nom du noeud dont vous souhaitez récupérer la valeur. Cette méthode renvoie une valeur de chaîne représentant la valeur du noeud. Dans l’exemple de code qui suit ce processus, cette méthode personnalisée est appelée `getNodeText`. Le corps de cette méthode est illustré.
   * Si le type de contenu de données est `application/pdf`défini, créez une logique d’application pour enregistrer les données PDF envoyées sous forme de fichier PDF.

      * Créez un `BLOB` objet en appelant la `FormsResult` méthode de l’ `getOutputContent` objet.
      * Créez un tableau d’octets en appelant la `BLOB` `getBinaryData` méthode de l’objet.
      * Create a `java.io.File` object by using its public constructor. Veillez à spécifier PDF comme extension de nom de fichier.
      * Créez un objet `java.io.FileOutputStream` en utilisant son constructeur et en transmettant l’objet `java.io.File`. 
      * Renseignez le fichier PDF en appelant la `java.io.FileOutputStream` `write` méthode de l’objet et en transmettant le tableau d’octets.


**Voir également**

[Appel d’AEM Forms à l’aide du codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)