---
title: Rendu de formulaires HTML à l’aide de fichiers CSS personnalisés
seo-title: Rendu de formulaires HTML à l’aide de fichiers CSS personnalisés
description: 'null'
seo-description: 'null'
uuid: a44e96f1-001d-48a2-8c96-15cb9d0c71b3
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 8fe7c072-7df0-44b7-92d0-bf39dc1e688a
translation-type: tm+mt
source-git-commit: fcbe1d860410e215cb7c438f94579e0b14d262a5

---


# Rendu de formulaires HTML à l’aide de fichiers CSS personnalisés {#rendering-html-forms-using-custom-css-files}

Le service Forms génère des formulaires HTML en réponse à une requête HTTP d’un navigateur Web. Lors du rendu d’un formulaire HTML, le service Forms peut référencer un fichier CSS personnalisé. Vous pouvez créer un fichier CSS personnalisé pour répondre aux besoins de votre entreprise et référencer ce fichier CSS lors de l’utilisation du service Forms pour générer des formulaires HTML.

Le service Forms analyse silencieusement le fichier CSS personnalisé. En d’autres termes, le service Forms ne signale pas les erreurs qui peuvent se produire si le fichier CSS personnalisé ne respecte pas les normes CSS. Dans ce cas, le service Forms ignore le style et continue avec les styles restants situés dans le fichier CSS.

Le suivant spécifie les styles pris en charge dans un fichier CSS personnalisé :

* **paires** de type sélecteur de niveau classe : S’il est présent dans un fichier CSS personnalisé, les sélecteurs utilisés dans le formulaire HTML en tant que styles de classe sont utilisés. Les styles de classe inutilisés sont ignorés.
* **Paires** de type sélecteur de niveau identificateur : Tous les styles d’identificateur sont utilisés s’ils sont utilisés dans le formulaire HTML.
* **paires** de style de sélecteur de niveau élément : Tous les styles d’élément sont utilisés s’ils sont utilisés dans le formulaire HTML.
* **Priorité** du style : La priorité de style (importante également) est prise en charge et peut être utilisée dans un fichier CSS personnalisé.
* **Type** de support : Une ou plusieurs paires de style sélecteur peuvent être encapsulées dans le style @media pour définir le type de média. Le service Forms ne vérifie pas si le type de support spécifié est pris en charge. Le type de support spécifié dans le fichier CSS personnalisé est fusionné dans le formulaire HTML.

Vous pouvez récupérer un exemple de fichier CSS à l’aide de l’application FormsIVS. Téléchargez le formulaire, sélectionnez-le dans la page Conception de formulaire de test, puis cliquez sur GénérerCSS. Il n’est pas nécessaire de définir le type de transformation HTML avant de cliquer sur le bouton. Sélectionnez ensuite Enregistrer. Vous pouvez modifier ce fichier CSS pour répondre aux besoins de votre entreprise.

>[!NOTE]
>
>Avant de générer un formulaire HTML qui utilise un fichier CSS personnalisé, il est important de bien comprendre le rendu des formulaires HTML. (voir [Rendu de formulaires au format HTML](/help/forms/developing/rendering-forms-html.md)).

>[!NOTE]
>
>For more information about the Forms service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Résumé des étapes {#summary-of-steps}

Pour générer un formulaire HTML utilisant un fichier CSS, effectuez le  suivant :

1. Incluez des fichiers de projet.
1. Créez un objet API Java Forms.
1. Référencez le fichier CSS.
1. Générer un formulaire HTML.
1. Ecrivez le flux de données du formulaire dans le navigateur Web client.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

**Création d’un objet API Java Forms**

Avant de pouvoir exécuter par programmation une opération prise en charge par le service Forms, vous devez créer un objet client Forms.

**Référence au fichier CSS**

Pour générer un formulaire HTML utilisant un fichier CSS personnalisé, veillez à référencer un fichier CSS existant.

**Rendu d’un formulaire HTML**

Pour générer un formulaire HTML, vous devez spécifier une conception de formulaire créée dans Designer et enregistrée dans un fichier XDP. Vous devez également sélectionner un type de transformation HTML. Par exemple, vous pouvez spécifier le type de transformation HTML qui effectue le rendu d’un code HTML dynamique pour Internet Explorer 5.0 ou version ultérieure.

Le rendu d’un formulaire HTML requiert également des valeurs, telles que les valeurs URI nécessaires au rendu d’autres types de formulaire.

**Ecrire le flux de données du formulaire dans le navigateur Web client**

Lorsque le service Forms génère un formulaire HTML, il renvoie un flux de données de formulaire que vous devez écrire dans le navigateur Web client pour rendre le formulaire HTML visible à l’utilisateur.

**Voir également**

[Générer un formulaire HTML utilisant un fichier CSS à l’aide de l’API Java](#render-an-html-form-that-uses-a-css-file-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[rapide de l’API du service Forms](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Rendu de formulaires PDF interactifs](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Rendu des formulaires au format HTML](/help/forms/developing/rendering-forms-html.md)

[Création de   de qui rend les formulaires](/help/forms/developing/creating-web-applications-renders-forms.md)

## Générer un formulaire HTML utilisant un fichier CSS à l’aide de l’API Java {#render-an-html-form-that-uses-a-css-file-using-the-java-api}

Générer un formulaire HTML utilisant un fichier CSS personnalisé à l’aide de l’API Forms (Java) :

1. Inclure les fichiers de projet

   Incluez des fichiers JAR client, tels que adobe-forms-client.jar, dans le chemin de classe de votre projet Java.

1. Création d’un objet API Java Forms

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `FormsServiceClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`. 

1. Référence au fichier CSS

   * Create an `HTMLRenderSpec` object by using its constructor.
   * Pour générer le formulaire HTML qui utilise un fichier CSS personnalisé, appelez la `HTMLRenderSpec` `setCustomCSSURI` méthode de l’objet et transmettez une valeur de chaîne qui spécifie l’emplacement et le nom du fichier CSS.

1. Rendu d’un formulaire HTML

   Appelez la méthode `FormsServiceClient` `(Deprecated) (Deprecated) renderHTMLForm` de l’objet et transmettez les valeurs suivantes :

   * Valeur de chaîne qui spécifie le nom de la conception de formulaire, y compris l’extension du nom de fichier. Si vous référencez une conception de formulaire faisant partie d’une application Forms, veillez à spécifier le chemin d’accès complet, tel que `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Valeur `TransformTo` enum qui spécifie le type de préférence HTML. Par exemple, pour générer un formulaire HTML compatible avec le code HTML dynamique pour Internet Explorer 5.0 ou version ultérieure, spécifiez `TransformTo.MSDHTML`.
   * Objet `com.adobe.idp.Document` contenant des données à fusionner avec le formulaire. Si vous ne souhaitez pas fusionner les données, transmettez un `com.adobe.idp.Document` objet vide.
   * Objet `HTMLRenderSpec` qui stocke les options d’exécution HTML.
   * Valeur de chaîne qui spécifie la valeur d’ `HTTP_USER_AGENT` en-tête, telle que `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
   * Objet `URLSpec` qui stocke les valeurs URI requises pour générer un formulaire HTML.
   * Objet `java.util.HashMap` qui stocke les pièces jointes. Il s’agit d’un paramètre facultatif, que vous pouvez spécifier `null` si vous ne souhaitez pas joindre de fichiers au formulaire.
   La `(Deprecated) renderHTMLForm` méthode renvoie un `FormsResult` objet qui contient un flux de données de formulaire qui doit être écrit dans le navigateur Web client.

1. Ecrire le flux de données du formulaire dans le navigateur Web client

   * Créez un `com.adobe.idp.Document` objet en appelant la `FormsResult` méthode de l’ `getOutputContent` objet.
   * Obtenez le type de contenu de l’ `com.adobe.idp.Document` objet en appelant sa `getContentType` méthode.
   * Définissez le type de contenu de l’ `javax.servlet.http.HttpServletResponse` objet en appelant sa `setContentType` méthode et en transmettant le type de contenu de l’ `com.adobe.idp.Document` objet.
   * Créez un `javax.servlet.ServletOutputStream` objet utilisé pour écrire le flux de données du formulaire dans le navigateur Web client en appelant la `javax.servlet.h\ttp.HttpServletResponse` `getOutputStream` méthode de l’objet.
   * Créez un `java.io.InputStream` objet en appelant la `com.adobe.idp.Document` méthode de l’ `getInputStream` objet.
   * Créez un tableau d’octets et renseignez-le avec le flux de données du formulaire en appelant la `InputStream` `read` méthode de l’objet et en transmettant le tableau d’octets en tant qu’argument.
   * Appelez la `javax.servlet.ServletOutputStream` `write` méthode de l’objet pour envoyer le flux de données du formulaire au navigateur Web client. Transmettez le tableau d’octets à la `write` méthode.

**Voir également**

[Rendu de formulaires HTML à l’aide de fichiers CSS personnalisés](#rendering-html-forms-using-custom-css-files)

[rapide (mode SOAP) : Rendu d’un formulaire HTML utilisant un fichier CSS à l’aide de l’API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-an-html-form-that-uses-a-css-file-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Générer un formulaire HTML utilisant un fichier CSS à l’aide de l’API du service Web {#render-an-html-form-that-uses-a-css-file-using-the-web-service-api}

Générer un formulaire HTML qui utilise un fichier CSS personnalisé à l’aide de l’API Forms (service Web) :

1. Inclure les fichiers de projet

   * Créez des classes de proxy Java qui utilisent le WSDL du service Forms.
   * Incluez les classes de proxy Java dans le chemin d’accès de votre classe.

1. Création d’un objet API Java Forms

   Créez un `FormsService` objet et définissez des valeurs d’authentification.

1. Référence au fichier CSS

   * Create an `HTMLRenderSpec` object by using its constructor.
   * Pour générer le formulaire HTML qui utilise un fichier CSS personnalisé, appelez la `HTMLRenderSpec` `setCustomCSSURI` méthode de l’objet et transmettez une valeur de chaîne qui spécifie l’emplacement et le nom du fichier CSS.

1. Rendu d’un formulaire HTML

   Appelez la méthode `FormsService` `(Deprecated) renderHTMLForm` de l’objet et transmettez les valeurs suivantes :

   * Valeur de chaîne qui spécifie le nom de la conception de formulaire, y compris l’extension du nom de fichier. Si vous référencez une conception de formulaire faisant partie d’une application Forms, veillez à spécifier le chemin d’accès complet, tel que `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Valeur `TransformTo` enum qui spécifie le type de préférence HTML. Par exemple, pour générer un formulaire HTML compatible avec le code HTML dynamique pour Internet Explorer 5.0 ou version ultérieure, spécifiez `TransformTo.MSDHTML`.
   * Objet `BLOB` contenant des données à fusionner avec le formulaire. Si vous ne souhaitez pas fusionner des données, transmettez-les `null`. (Voir [Préremplissage de formulaires avec des mises en page](/help/forms/developing/prepopulating-forms-flowable-layouts.md)à disposition souple.)
   * Objet `HTMLRenderSpec` qui stocke les options d’exécution HTML.
   * Valeur de chaîne qui spécifie la valeur d’ `HTTP_USER_AGENT` en-tête, telle que `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`. Vous pouvez transmettre une chaîne vide si vous ne souhaitez pas définir cette valeur.
   * Objet `URLSpec` qui stocke les valeurs URI requises pour générer un formulaire HTML.
   * Objet `java.util.HashMap` qui stocke les pièces jointes. Il s’agit d’un paramètre facultatif, que vous pouvez spécifier `null` si vous ne souhaitez pas joindre de fichiers au formulaire.
   * Objet vide `com.adobe.idp.services.holders.BLOBHolder` renseigné par la `(Deprecated) renderHTMLForm` méthode. Cette valeur de paramètre stocke le formulaire rendu.
   * Objet vide `com.adobe.idp.services.holders.BLOBHolder` renseigné par la `(Deprecated) renderHTMLForm` méthode. Ce paramètre stocke les données XML de sortie.
   * Objet vide `javax.xml.rpc.holders.LongHolder` renseigné par la `(Deprecated) renderHTMLForm` méthode. Cet argument stocke le nombre de pages dans le formulaire.
   * Objet vide `javax.xml.rpc.holders.StringHolder` renseigné par la `(Deprecated) renderHTMLForm` méthode. Cet argument stocke la valeur du paramètre régional.
   * Objet vide `javax.xml.rpc.holders.StringHolder` renseigné par la `(Deprecated) renderHTMLForm` méthode. Cet argument stocke la valeur de rendu HTML utilisée.
   * Objet vide `com.adobe.idp.services.holders.FormsResultHolder` qui contiendra les résultats de cette opération.
   La `(Deprecated) renderHTMLForm` méthode remplit l’ `com.adobe.idp.services.holders.FormsResultHolder` objet transmis en tant que valeur du dernier argument avec un flux de données de formulaire qui doit être écrit dans le navigateur Web client.

1. Ecrire le flux de données du formulaire dans le navigateur Web client

   * Créez un `FormResult` objet en obtenant la valeur du membre `com.adobe.idp.services.holders.FormsResultHolder` de données de l’ `value` objet.
   * Créez un `BLOB` objet contenant des données de formulaire en appelant la `FormsResult` méthode de l’ `getOutputContent` objet.
   * Obtenez le type de contenu de l’ `BLOB` objet en appelant sa `getContentType` méthode.
   * Définissez le type de contenu de l’ `javax.servlet.http.HttpServletResponse` objet en appelant sa `setContentType` méthode et en transmettant le type de contenu de l’ `BLOB` objet.
   * Créez un `javax.servlet.ServletOutputStream` objet utilisé pour écrire le flux de données du formulaire dans le navigateur Web client en appelant la `javax.servlet.http.HttpServletResponse` `getOutputStream` méthode de l’objet.
   * Créez un tableau d’octets et renseignez-le en appelant la méthode `BLOB` `getBinaryData` de l’objet. Ce affecte le contenu de l’ `FormsResult` objet au tableau d’octets.
   * Appelez la `javax.servlet.http.HttpServletResponse` `write` méthode de l’objet pour envoyer le flux de données du formulaire au navigateur Web client. Transmettez le tableau d’octets à la `write` méthode.

**Voir également**

[Rendu de formulaires HTML à l’aide de fichiers CSS personnalisés](#rendering-html-forms-using-custom-css-files)

[Appel d’AEM Forms à l’aide du codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
