---
title: Rendu des formulaires au niveau du client
seo-title: Rendu des formulaires au niveau du client
description: 'null'
seo-description: 'null'
uuid: 09bcc23d-28b0-473a-87f1-bc17e87620f4
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 08d36e9f-cafc-478e-9781-8fc29ac6262e
translation-type: tm+mt
source-git-commit: ab401a8007f6ea85c0e52169091ce7a38b3dbe5c

---


# Rendu des formulaires au niveau du client {#rendering-forms-at-the-client}

## Rendu des formulaires au niveau du client {#rendering-forms-at-the-client-inner}

Vous pouvez optimiser le du contenu PDF et améliorer la capacité du service Forms à gérer la charge réseau en utilisant la fonctionnalité de rendu côté client d’Acrobat ou d’Adobe Reader. Ce processus est connu sous le nom de rendu d’un formulaire au niveau du client. Pour générer un formulaire au niveau du client, le périphérique client (généralement un navigateur Web) doit utiliser Acrobat 7.0 ou Adobe Reader 7.0 ou une version ultérieure.

Les modifications apportées à un formulaire résultant de l’exécution de script côté serveur ne sont pas répercutées dans un formulaire généré au niveau du client, sauf si le sous-formulaire racine contient l’ `restoreState` attribut défini sur `auto`. Pour plus d’informations sur cet attribut, voir [Forms Designer.](https://www.adobe.com/go/learn_aemforms_designer_63)

>[!NOTE]
>
>For more information about the Forms service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary-of-steps}

Pour générer un formulaire au niveau du client, effectuez le  suivant :

1. Incluez des fichiers de projet.
1. Créez un objet API Client Forms.
1. Définissez les options d’exécution du rendu client.
1. Générer un formulaire au niveau du client.
1. Ecrivez le formulaire dans le navigateur Web client.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

**Création d’un objet API du client Forms**

Avant de pouvoir exécuter par programmation une opération d’API du client de service Forms, vous devez créer un client de service Forms. Si vous utilisez l’API Java, créez un `FormsServiceClient` objet. Si vous utilisez l’API du service Web de Forms, créez un `FormsService` objet.

**Définition des options d’exécution du rendu client**

Vous devez définir l’option d’exécution du rendu client pour générer un formulaire au niveau du client en définissant l’option d’ `RenderAtClient` exécution sur `true`. Le formulaire est alors remis au périphérique client sur lequel il est généré. Si `RenderAtClient` est `auto` (valeur par défaut), la conception de formulaire détermine si le formulaire est généré au niveau du client. La conception de formulaire doit être une conception de formulaire avec une disposition souple.

Une option d’exécution facultative que vous pouvez définir est l’ `SeedPDF` option. Cette `SeedPDF` option associe le  PDF (PDF initial) à la conception de formulaire et aux données XML. La conception de formulaire et les données XML sont transmises à Acrobat ou Adobe Reader, où le formulaire est généré. Cette `SeedPDF` option peut être utilisée lorsque l’ordinateur client ne dispose pas de polices utilisées dans le formulaire, par exemple lorsqu’un utilisateur final n’est pas autorisé à utiliser une police dont le propriétaire est autorisé à utiliser la licence.

Vous pouvez utiliser Designer pour créer un fichier PDF dynamique simple à utiliser comme fichier PDF initial. Les étapes suivantes sont requises pour effectuer cette  de :

1. Déterminez si vous devez incorporer des polices dans le fichier PDF initial. Le fichier PDF initial doit contenir les polices supplémentaires requises par le formulaire généré. Lorsque vous incorporez des polices dans le fichier PDF initial, veillez à ne pas enfreindre les accords de licence des polices. Dans Designer, vous pouvez déterminer si vous pouvez incorporer légalement des polices. Lors de l’enregistrement, si vous ne pouvez pas incorporer de polices dans le formulaire, Designer affiche un message répertoriant les polices que vous ne pouvez pas incorporer. Ce message ne s’affiche pas dans Designer pour les  PDF statiques.
1. Si vous créez le fichier PDF d’origine dans Designer, il est recommandé d’ajouter au minimum un champ de texte contenant un message. Le message doit être adressé aux utilisateurs des versions antérieures d’Adobe Reader pour leur indiquer qu’ils ont besoin d’Acrobat 7.0 (ou version ultérieure) ou d’Adobe Reader 7.0 (ou version ultérieure) pour  le  de.
1. Enregistrez le fichier PDF initial sous forme de fichier PDF dynamique avec l’extension de nom de fichier PDF.

>[!NOTE]
>
>Il n’est pas nécessaire de définir l’option d’exécution PDF d’origine pour générer un formulaire sur le client. Si vous ne spécifiez pas de PDF initial, le service Forms crée un fichier shell pdf qui ne contiendra pas d’objets COS, mais qui contiendra un wrapper PDF avec le contenu XDP réel incorporé à l’intérieur. Les étapes de cette section ne définissent pas l’option d’exécution PDF d’origine. Pour plus d’informations sur les objets COS, voir le guide de référence Adobe PDF.

**Rendu d’un formulaire au niveau du client**

Pour effectuer le rendu d’un formulaire sur le client, vous devez vous assurer que les options d’exécution du rendu client sont incluses dans la logique de votre application pour générer un formulaire.

**Ecrire le flux de données du formulaire dans le navigateur Web client**

Le service Forms crée un flux de données de formulaire que vous devez écrire dans le navigateur Web client. Lorsqu’il est écrit dans le navigateur Web client, le formulaire est généré par Acrobat 7.0 ou Adobe Reader 7.0 (ou version ultérieure) et est visible par l’utilisateur.

**Voir également**

[Générer un formulaire au niveau du client à l’aide de l’API Java](#render-a-form-at-the-client-using-the-java-api)

[Générer un formulaire au niveau du client à l’aide de l’API du service Web](#render-a-form-at-the-client-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[rapide de l’API du service Forms](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Transmission de  au service Forms](/help/forms/developing/passing-documents-forms-service.md)

[Création de   de qui rend les formulaires](/help/forms/developing/creating-web-applications-renders-forms.md)

### Générer un formulaire au niveau du client à l’aide de l’API Java {#render-a-form-at-the-client-using-the-java-api}

Générer un formulaire sur le client à l’aide de l’API Forms (Java) :

1. Inclure les fichiers de projet

   Incluez des fichiers JAR client, tels que adobe-forms-client.jar, dans le chemin de classe de votre projet Java.

1. Création d’un objet API du client Forms

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Create an `FormsServiceClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. Définition des options d’exécution du rendu client

   * Créez un objet `PDFFormRenderSpec` en utilisant son constructeur.
   * Définissez l’option `RenderAtClient` d’exécution en appelant la `PDFFormRenderSpec` méthode de l’objet et en transmettant la valeur enum `setRenderAtClient` `RenderAtClient.Yes`.

1. Rendu d’un formulaire au niveau du client

   Appelez la méthode `FormsServiceClient` `renderPDFForm` de l’objet et transmettez les valeurs suivantes :

   * Valeur de chaîne qui spécifie le nom de la conception de formulaire, y compris l’extension du nom de fichier. Si vous référencez une conception de formulaire faisant partie d’une application AEM Forms, veillez à spécifier le chemin d’accès complet, tel que `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Objet `com.adobe.idp.Document` contenant des données à fusionner avec le formulaire. Si vous ne souhaitez pas fusionner les données, transmettez un `com.adobe.idp.Document` objet vide.
   * Objet `PDFFormRenderSpec` qui stocke les options d’exécution requises pour générer un formulaire au niveau du client.
   * Objet `URLSpec` contenant des valeurs URI requises par le service Forms pour générer un formulaire.
   * Objet `java.util.HashMap` qui stocke les pièces jointes. Il s’agit d’un paramètre facultatif que vous pouvez spécifier `null` si vous ne souhaitez pas joindre de fichiers au formulaire.
   La `renderPDFForm` méthode renvoie un `FormsResult` objet qui contient un flux de données de formulaire qui doit être écrit dans le navigateur Web client.

1. Ecrire le flux de données du formulaire dans le navigateur Web client

   * Créez un `com.adobe.idp.Document` objet en appelant la `FormsResult` méthode de l’ `getOutputContent` objet.
   * Obtenez le type de contenu de l’ `com.adobe.idp.Document` objet en appelant sa `getContentType` méthode.
   * Définissez le type de contenu de l’ `javax.servlet.http.HttpServletResponse` objet en appelant sa `setContentType` méthode et en transmettant le type de contenu de l’ `com.adobe.idp.Document` objet.
   * Créez un `javax.servlet.ServletOutputStream` objet utilisé pour écrire le flux de données du formulaire dans le navigateur Web client en appelant la `javax.servlet.http.HttpServletResponse` `getOutputStream` méthode de l’objet.
   * Créez un `java.io.InputStream` objet en appelant la `com.adobe.idp.Document` méthode de l’ `getInputStream` objet.
   * Créez un tableau d’octets et renseignez-le avec le flux de données du formulaire en appelant la `InputStream` `read` méthode de l’objet et en transmettant le tableau d’octets en tant qu’argument.
   * Appelez la `javax.servlet.ServletOutputStream` `write` méthode de l’objet pour envoyer le flux de données du formulaire au navigateur Web client. Transmettez le tableau d’octets à la `write` méthode.

**Voir également**

[rapide (mode SOAP) : Rendu d’un formulaire sur le client à l’aide de l’API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-a-form-at-the-client-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Générer un formulaire au niveau du client à l’aide de l’API du service Web {#render-a-form-at-the-client-using-the-web-service-api}

Générer un formulaire sur le client à l’aide de l’API Forms (service Web) :

1. Inclure les fichiers de projet

   * Créez des classes de proxy Java qui utilisent le WSDL du service Forms.
   * Insérez les classes proxy Java dans le chemin de votre classe.

1. Création d’un objet API du client Forms

   Créez un `FormsService` objet et définissez des valeurs d’authentification.

1. Définition des options d’exécution du rendu client

   * Créez un objet `PDFFormRenderSpec` en utilisant son constructeur.
   * Définissez l’option `RenderAtClient` d’exécution en appelant la `PDFFormRenderSpec` méthode de l’objet et en transmettant la valeur de chaîne `setRenderAtClient` `RenderAtClient.Yes`.

1. Rendu d’un formulaire au niveau du client

   Appelez la méthode `FormsService` `renderPDFForm` de l’objet et transmettez les valeurs suivantes :

   * Valeur de chaîne qui spécifie le nom de la conception de formulaire, y compris l’extension du nom de fichier. Si vous référencez une conception de formulaire faisant partie d’une application Forms, veillez à spécifier le chemin d’accès complet, tel que `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Objet `BLOB` contenant des données à fusionner avec le formulaire. Si vous ne souhaitez pas fusionner des données, transmettez-les `null`. (Voir [Préremplissage de formulaires avec des mises en page](/help/forms/developing/prepopulating-forms-flowable-layouts.md)à disposition souple.)
   * Objet `PDFFormRenderSpec` qui stocke les options d’exécution requises pour générer un formulaire au niveau du client.
   * Objet `URLSpec` contenant des valeurs URI requises par le service Forms.
   * Objet `java.util.HashMap` qui stocke les pièces jointes. Il s’agit d’un paramètre facultatif que vous pouvez spécifier `null` si vous ne souhaitez pas joindre de fichiers au formulaire.
   * Objet vide `com.adobe.idp.services.holders.BLOBHolder` renseigné par la méthode. Ce paramètre est utilisé pour stocker le formulaire PDF rendu.
   * Objet vide `javax.xml.rpc.holders.LongHolder` renseigné par la méthode. (Cet argument stocke le nombre de pages dans le formulaire).
   * Objet vide `javax.xml.rpc.holders.StringHolder` renseigné par la méthode. (Cet argument stocke la valeur du paramètre régional).
   * Objet vide `com.adobe.idp.services.holders.FormsResultHolder` qui contiendra les résultats de cette opération.
   La `renderPDFForm` méthode remplit l’ `com.adobe.idp.services.holders.FormsResultHolder` objet transmis en tant que valeur du dernier argument avec un flux de données de formulaire qui doit être écrit dans le navigateur Web client.

1. Ecrire le flux de données du formulaire dans le navigateur Web client

   * Créez un `FormResult` objet en obtenant la valeur du membre `com.adobe.idp.services.holders.FormsResultHolder` de données de l’ `value` objet.
   * Créez un `BLOB` objet contenant des données de formulaire en appelant la `FormsResult` méthode de l’ `getOutputContent` objet.
   * Obtenez le type de contenu de l’ `BLOB` objet en appelant sa `getContentType` méthode.
   * Définissez le type de contenu de l’ `javax.servlet.http.HttpServletResponse` objet en appelant sa `setContentType` méthode et en transmettant le type de contenu de l’ `BLOB` objet.
   * Créez un `javax.servlet.ServletOutputStream` objet utilisé pour écrire le flux de données du formulaire dans le navigateur Web client en appelant la `javax.servlet.http.HttpServletResponse` `getOutputStream` méthode de l’objet.
   * Créez un tableau d’octets et renseignez-le en appelant la méthode `BLOB` `getBinaryData` de l’objet. Ce affecte le contenu de l’ `FormsResult` objet au tableau d’octets.
   * Appelez la `javax.servlet.http.HttpServletResponse` `write` méthode de l’objet pour envoyer le flux de données du formulaire au navigateur Web client. Transmettez le tableau d’octets à la `write` méthode.

**Voir également**

[Rendu des formulaires au niveau du client](#rendering-forms-at-the-client)

[Appel d’AEM Forms à l’aide du codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
