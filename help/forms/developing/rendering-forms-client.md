---
title: Rendu de Forms sur le client
seo-title: Rendu de Forms sur le client
description: Optimiser la diffusion de contenu PDF et améliorer la capacité du service Forms à gérer la charge réseau à l’aide de la fonctionnalité de rendu côté client d’Acrobat ou d’Adobe Reader
seo-description: Optimiser la diffusion de contenu PDF et améliorer la capacité du service Forms à gérer la charge réseau à l’aide de la fonctionnalité de rendu côté client d’Acrobat ou d’Adobe Reader
uuid: 09bcc23d-28b0-473a-87f1-bc17e87620f4
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 08d36e9f-cafc-478e-9781-8fc29ac6262e
role: Developer
exl-id: e485980d-f200-46b7-9284-c9996003aa47
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1730'
ht-degree: 2%

---

# Rendu de Forms sur le client {#rendering-forms-at-the-client}

**Les exemples et les exemples de ce document sont réservés à l’environnement AEM Forms on JEE.**

## Rendu de Forms sur le client {#rendering-forms-at-the-client-inner}

Vous pouvez optimiser la diffusion de contenu PDF et améliorer la capacité du service Forms à gérer la charge réseau à l’aide de la fonctionnalité de rendu côté client d’Acrobat ou d’Adobe Reader. Ce processus est connu sous le nom de rendu d’un formulaire au niveau du client. Pour effectuer le rendu d’un formulaire sur le client, le périphérique client (généralement un navigateur web) doit utiliser Acrobat 7.0 ou Adobe Reader 7.0 ou une version ultérieure.

Les modifications apportées à un formulaire résultant de l’exécution de script côté serveur ne sont pas répercutées dans un formulaire rendu sur le client, sauf si le sous-formulaire racine contient l’attribut `restoreState` défini sur `auto`. Pour plus d’informations sur cet attribut, voir [Forms Designer.](https://www.adobe.com/go/learn_aemforms_designer_63)

>[!NOTE]
>
>Pour plus d’informations sur le service Forms, voir [Référence des services pour AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary-of-steps}

Pour générer un formulaire au niveau du client, effectuez les tâches suivantes :

1. Inclure les fichiers de projet.
1. Créez un objet API client Forms.
1. Définissez les options d’exécution du rendu client.
1. Effectuez le rendu d’un formulaire au niveau du client.
1. Ecrivez le formulaire dans le navigateur Web client.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

**Création d’un objet API client Forms**

Avant d’effectuer par programmation une opération d’API client de service Forms, vous devez créer un client de service Forms. Si vous utilisez l’API Java, créez un objet `FormsServiceClient` . Si vous utilisez l’API du service Web Forms, créez un objet `FormsService` .

**Définition des options d’exécution du rendu client**

Vous devez définir l’option d’exécution de rendu client pour générer un formulaire au niveau du client en définissant l’option d’exécution `RenderAtClient` sur `true`. Le formulaire est ainsi transmis au périphérique client où il est rendu. Si `RenderAtClient` est `auto` (la valeur par défaut), la conception de formulaire détermine si le formulaire est rendu sur le client. La conception de formulaire doit être une conception de formulaire avec une disposition souple.

Une option d’exécution facultative que vous pouvez définir est l’option `SeedPDF`. L’option `SeedPDF` combine le conteneur PDF (document PDF d’origine) à la conception de formulaire et aux données XML. La conception de formulaire et les données XML sont transmises à Acrobat ou à Adobe Reader, où le formulaire est rendu. L’option `SeedPDF` peut être utilisée lorsque l’ordinateur client ne dispose pas de polices utilisées dans le formulaire, par exemple lorsqu’un utilisateur final n’est pas autorisé à utiliser une police que le propriétaire du formulaire est autorisé à utiliser.

Vous pouvez utiliser Designer pour créer un fichier PDF dynamique simple à utiliser comme fichier PDF d’origine. Pour effectuer cette tâche, procédez comme suit :

1. Déterminez si vous devez incorporer des polices dans le fichier PDF d’origine. Le fichier PDF source doit contenir les polices supplémentaires requises par le formulaire en cours de rendu. Lors de l’incorporation de polices dans le fichier PDF d’origine, assurez-vous de ne pas enfreindre les accords de licence des polices. Dans Designer, vous pouvez déterminer si vous pouvez incorporer légalement des polices. Lors de l’enregistrement, si vous ne pouvez pas incorporer de polices dans le formulaire, Designer affiche un message répertoriant les polices que vous ne pouvez pas incorporer. Ce message ne s’affiche pas dans Designer pour les documents PDF statiques.
1. Si vous créez le fichier PDF d’origine dans Designer, il est recommandé d’ajouter au minimum un champ de texte contenant un message. Le message doit être adressé aux utilisateurs des versions antérieures d’Adobe Reader en indiquant qu’ils ont besoin d’Acrobat 7.0 ou version ultérieure ou d’Adobe Reader 7.0 ou version ultérieure pour afficher le document.
1. Enregistrez le fichier PDF d’origine en tant que fichier PDF dynamique avec l’extension de nom de fichier PDF.

>[!NOTE]
>
>Vous n’avez pas besoin de définir l’option d’exécution PDF d’origine pour générer un formulaire sur le client. Si vous ne spécifiez pas de PDF source, le service Forms crée un shell pdf qui ne contiendra pas d’objets COS mais contiendra un wrapper PDF avec le contenu XDP réel incorporé à l’intérieur. Les étapes de cette section ne définissent pas l’option d’exécution PDF d’origine. Pour plus d’informations sur les objets COS, consultez le guide de référence d’Adobe PDF.

**Rendu d’un formulaire au niveau du client**

Pour effectuer le rendu d’un formulaire sur le client, vous devez vous assurer que les options d’exécution de rendu client sont incluses dans la logique de votre application pour générer un formulaire.

**Écrire le flux de données de formulaire dans le navigateur Web client**

Le service Forms crée un flux de données de formulaire que vous devez écrire dans le navigateur Web client. Lorsqu’il est écrit dans le navigateur Web client, le formulaire est rendu par Acrobat 7.0 ou Adobe Reader 7.0 ou version ultérieure et est visible par l’utilisateur.

**Voir également**

[Rendu d’un formulaire sur le client à l’aide de l’API Java](#render-a-form-at-the-client-using-the-java-api)

[Rendu d’un formulaire au client à l’aide de l’API du service Web](#render-a-form-at-the-client-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Démarrages rapides de l’API Forms Service](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Transmission de documents au service Forms](/help/forms/developing/passing-documents-forms-service.md)

[Création d’applications web qui renvoient Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

### Rendu d’un formulaire sur le client à l’aide de l’API Java {#render-a-form-at-the-client-using-the-java-api}

Rendre un formulaire au client à l’aide de l’API Forms (Java) :

1. Inclure les fichiers de projet

   Incluez les fichiers JAR client, tels que adobe-forms-client.jar, dans le chemin de classe de votre projet Java.

1. Création d’un objet API client Forms

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `FormsServiceClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`.

1. Définition des options d’exécution du rendu client

   * Créez un objet `PDFFormRenderSpec` en utilisant son constructeur.
   * Définissez l’option d’exécution `RenderAtClient` en appelant la méthode `setRenderAtClient` de l’objet `PDFFormRenderSpec` et en transmettant la valeur d’énumération `RenderAtClient.Yes`.

1. Rendu d’un formulaire au niveau du client

   Appelez la méthode `renderPDFForm` de l’objet `FormsServiceClient` et transmettez les valeurs suivantes :

   * Une valeur string qui spécifie le nom de la conception de formulaire, y compris l’extension du nom de fichier. Si vous référencez une conception de formulaire qui fait partie d’une application AEM Forms, veillez à spécifier le chemin d’accès complet, tel que `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Objet `com.adobe.idp.Document` contenant les données à fusionner avec le formulaire. Si vous ne souhaitez pas fusionner de données, transmettez un objet `com.adobe.idp.Document` vide.
   * Objet `PDFFormRenderSpec` qui stocke les options d’exécution requises pour générer un formulaire au niveau du client.
   * Objet `URLSpec` contenant les valeurs URI requises par le service Forms pour générer un formulaire.
   * Objet `java.util.HashMap` qui stocke les pièces jointes. Il s’agit d’un paramètre facultatif qui vous permet de spécifier `null` si vous ne souhaitez pas joindre de fichiers au formulaire.

   La méthode `renderPDFForm` renvoie un objet `FormsResult` contenant un flux de données de formulaire qui doit être écrit dans le navigateur Web client.

1. Écrire le flux de données de formulaire dans le navigateur Web client

   * Créez un objet `com.adobe.idp.Document` en appelant la méthode `FormsResult` de l’objet `getOutputContent`.
   * Obtenez le type de contenu de l’objet `com.adobe.idp.Document` en appelant sa méthode `getContentType`.
   * Définissez le type de contenu de l’objet `javax.servlet.http.HttpServletResponse` en appelant sa méthode `setContentType` et en transmettant le type de contenu de l’objet `com.adobe.idp.Document`.
   * Créez un objet `javax.servlet.ServletOutputStream` utilisé pour écrire le flux de données de formulaire dans le navigateur Web client en appelant la méthode `getOutputStream` de l’objet `javax.servlet.http.HttpServletResponse`.
   * Créez un objet `java.io.InputStream` en appelant la méthode `getInputStream` de l’objet `com.adobe.idp.Document`.
   * Créez un tableau d’octets et renseignez-le avec le flux de données de formulaire en appelant la méthode `InputStream` de l’objet `read` et en transmettant le tableau d’octets en tant qu’argument.
   * Appelez la méthode `write` de l’objet `javax.servlet.ServletOutputStream` pour envoyer le flux de données de formulaire au navigateur Web client. Transmettez le tableau d’octets à la méthode `write` .

**Voir également**

[Démarrage rapide (mode SOAP) : Rendu d’un formulaire au niveau du client à l’aide de l’API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-a-form-at-the-client-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Rendre un formulaire sur le client à l’aide de l’API de service Web {#render-a-form-at-the-client-using-the-web-service-api}

Rendre un formulaire au client à l’aide de l’API Forms (service Web) :

1. Inclure les fichiers de projet

   * Créez des classes proxy Java qui utilisent le WSDL du service Forms.
   * Incluez les classes proxy Java dans le chemin de classe.

1. Création d’un objet API client Forms

   Créez un objet `FormsService` et définissez des valeurs d’authentification.

1. Définition des options d’exécution du rendu client

   * Créez un objet `PDFFormRenderSpec` en utilisant son constructeur.
   * Définissez l’option d’exécution `RenderAtClient` en appelant la méthode `setRenderAtClient` de l’objet `PDFFormRenderSpec` et en transmettant la valeur de chaîne `RenderAtClient.Yes`.

1. Rendu d’un formulaire au niveau du client

   Appelez la méthode `renderPDFForm` de l’objet `FormsService` et transmettez les valeurs suivantes :

   * Une valeur string qui spécifie le nom de la conception de formulaire, y compris l’extension du nom de fichier. Si vous référencez une conception de formulaire qui fait partie d’une application Forms, veillez à spécifier le chemin d’accès complet, tel que `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Objet `BLOB` contenant les données à fusionner avec le formulaire. Si vous ne souhaitez pas fusionner les données, transmettez `null`. (Voir [Préremplissage de Forms avec des dispositions souple](/help/forms/developing/prepopulating-forms-flowable-layouts.md).)
   * Objet `PDFFormRenderSpec` qui stocke les options d’exécution requises pour générer un formulaire au niveau du client.
   * Objet `URLSpec` contenant des valeurs URI requises par le service Forms.
   * Objet `java.util.HashMap` qui stocke les pièces jointes. Il s’agit d’un paramètre facultatif qui vous permet de spécifier `null` si vous ne souhaitez pas joindre de fichiers au formulaire.
   * Objet `com.adobe.idp.services.holders.BLOBHolder` vide renseigné par la méthode . Ce paramètre est utilisé pour stocker le formulaire PDF rendu.
   * Objet `javax.xml.rpc.holders.LongHolder` vide renseigné par la méthode . (Cet argument stocke le nombre de pages dans le formulaire).
   * Objet `javax.xml.rpc.holders.StringHolder` vide renseigné par la méthode . (Cet argument stocke la valeur du paramètre régional).
   * Objet `com.adobe.idp.services.holders.FormsResultHolder` vide qui contiendra les résultats de cette opération.

   La méthode `renderPDFForm` renseigne l’objet `com.adobe.idp.services.holders.FormsResultHolder` transmis en tant que valeur du dernier argument avec un flux de données de formulaire qui doit être écrit dans le navigateur Web client.

1. Écrire le flux de données de formulaire dans le navigateur Web client

   * Créez un objet `FormResult` en obtenant la valeur du membre de données `value` de l’objet `com.adobe.idp.services.holders.FormsResultHolder`.
   * Créez un objet `BLOB` contenant des données de formulaire en appelant la méthode `getOutputContent` de l’objet `FormsResult`.
   * Obtenez le type de contenu de l’objet `BLOB` en appelant sa méthode `getContentType`.
   * Définissez le type de contenu de l’objet `javax.servlet.http.HttpServletResponse` en appelant sa méthode `setContentType` et en transmettant le type de contenu de l’objet `BLOB`.
   * Créez un objet `javax.servlet.ServletOutputStream` utilisé pour écrire le flux de données de formulaire dans le navigateur Web client en appelant la méthode `getOutputStream` de l’objet `javax.servlet.http.HttpServletResponse`.
   * Créez un tableau d’octets et renseignez-le en appelant la méthode `getBinaryData` de l’objet `BLOB`. Cette tâche affecte le contenu de l’objet `FormsResult` au tableau d’octets.
   * Appelez la méthode `write` de l’objet `javax.servlet.http.HttpServletResponse` pour envoyer le flux de données de formulaire au navigateur Web client. Transmettez le tableau d’octets à la méthode `write` .

**Voir également**

[Rendu de Forms sur le client](#rendering-forms-at-the-client)

[Appel d’AEM Forms à l’aide du codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
