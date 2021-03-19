---
title: Rendu de Forms HTML à l’aide de fichiers CSS personnalisés
seo-title: Rendu de Forms HTML à l’aide de fichiers CSS personnalisés
description: Utilisez le service Forms pour faire référence à des fichiers CSS personnalisés pour générer des formulaires HTML en réponse à une demande HTTP provenant d’un navigateur Web. Vous pouvez générer un formulaire HTML qui utilise un fichier CSS à l’aide de l’API Java et de l’API de service Web.
seo-description: Utilisez le service Forms pour faire référence à des fichiers CSS personnalisés pour générer des formulaires HTML en réponse à une demande HTTP provenant d’un navigateur Web. Vous pouvez générer un formulaire HTML qui utilise un fichier CSS à l’aide de l’API Java et de l’API de service Web.
uuid: a44e96f1-001d-48a2-8c96-15cb9d0c71b3
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 8fe7c072-7df0-44b7-92d0-bf39dc1e688a
role: Développeur
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1739'
ht-degree: 2%

---


# Rendu de HTML Forms à l’aide de fichiers CSS personnalisés {#rendering-html-forms-using-custom-css-files}

**Les exemples et exemples de ce document ne concernent que l’environnement AEM Forms on JEE.**

Le service Forms effectue le rendu des formulaires HTML en réponse à une requête HTTP provenant d’un navigateur Web. Lors du rendu d’un formulaire HTML, le service Forms peut référencer un fichier CSS personnalisé. Vous pouvez créer un fichier CSS personnalisé pour répondre aux besoins de votre entreprise et référencer ce fichier CSS lors de l’utilisation du service Forms pour générer des formulaires HTML.

Le service Forms analyse silencieusement le fichier CSS personnalisé. En d’autres termes, le service Forms ne signale pas les erreurs qui peuvent se produire si le fichier CSS personnalisé ne respecte pas les normes CSS. Dans ce cas, le service Forms ignore le style et continue avec les styles restants situés dans le fichier CSS.

La liste suivante spécifie les styles pris en charge dans un fichier CSS personnalisé :

* **Paires** de type sélecteur de niveau classe : S’il est présent dans un fichier CSS personnalisé, les sélecteurs utilisés dans le formulaire HTML en tant que styles de classe sont utilisés. Les styles de classe inutilisés sont ignorés.
* **Paires** de type sélecteur de niveau identificateur : Tous les styles d’identificateur sont utilisés s’ils sont utilisés dans le formulaire HTML.
* **Paires** de type sélecteur de niveau élément : Tous les styles d’élément sont utilisés s’ils sont utilisés dans le formulaire HTML.
* **Priorité** du style : La priorité de style (importante) est prise en charge et peut être utilisée dans un fichier CSS personnalisé.
* **Type** de support : Une ou plusieurs paires de style sélecteur peuvent être encapsulées dans le style @media pour définir le type de média. Le service Forms ne vérifie pas si le type de support spécifié est pris en charge. Le type de support spécifié dans le fichier CSS personnalisé est fusionné dans le formulaire HTML.

Vous pouvez récupérer un exemple de fichier CSS à l’aide de l’application FormsIVS. Téléchargez le formulaire, sélectionnez-le dans la page Conception de formulaire de test, puis cliquez sur GenerateCSS. Vous n&#39;avez pas besoin de définir le type de transformation HTML avant de cliquer sur le bouton. Sélectionnez ensuite Enregistrer. Vous pouvez modifier ce fichier CSS pour répondre aux besoins de votre entreprise.

>[!NOTE]
>
>Avant de générer un formulaire HTML qui utilise un fichier CSS personnalisé, il est important de bien comprendre le rendu des formulaires HTML. (Voir [Rendu de Forms au format HTML](/help/forms/developing/rendering-forms-html.md).)

>[!NOTE]
>
>Pour plus d’informations sur le service Forms, voir [Guide de référence des services pour AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Résumé des étapes {#summary-of-steps}

Pour générer un formulaire HTML utilisant un fichier CSS, effectuez les tâches suivantes :

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

**Génération d’un formulaire HTML**

Pour générer un formulaire HTML, vous devez spécifier une conception de formulaire créée dans Designer et enregistrée dans un fichier XDP. Vous devez également sélectionner un type de transformation HTML. Par exemple, vous pouvez spécifier le type de transformation HTML qui effectue le rendu d’un fichier HTML dynamique pour Internet Explorer 5.0 ou version ultérieure.

Le rendu d’un formulaire HTML requiert également des valeurs, telles que les valeurs URI nécessaires au rendu d’autres types de formulaire.

**Ecrire le flux de données du formulaire dans le navigateur Web client**

Lorsque le service Forms effectue le rendu d’un formulaire HTML, il renvoie un flux de données de formulaire que vous devez écrire dans le navigateur Web client pour rendre le formulaire HTML visible à l’utilisateur.

**Voir également**

[Générer un formulaire HTML utilisant un fichier CSS à l’aide de l’API Java](#render-an-html-form-that-uses-a-css-file-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Débuts rapides de l’API du service Forms](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Rendu des PDF forms interactifs](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Rendu de Forms au format HTML](/help/forms/developing/rendering-forms-html.md)

[Création d’Applications web renvoyant Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

## Générer un formulaire HTML utilisant un fichier CSS à l’aide de l’API Java {#render-an-html-form-that-uses-a-css-file-using-the-java-api}

Générer un formulaire HTML utilisant un fichier CSS personnalisé à l’aide de l’API Forms (Java) :

1. Inclure les fichiers de projet

   Incluez des fichiers JAR client, tels que adobe-forms-client.jar, dans le chemin de classe de votre projet Java.

1. Création d’un objet API Java Forms

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `FormsServiceClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`. 

1. Référence au fichier CSS

   * Créez un objet `HTMLRenderSpec` en utilisant son constructeur.
   * Pour générer le formulaire HTML qui utilise un fichier CSS personnalisé, appelez la méthode `HTMLRenderSpec` de l’objet `setCustomCSSURI` et transmettez une valeur de chaîne qui spécifie l’emplacement et le nom du fichier CSS.

1. Génération d’un formulaire HTML

   Appelez la méthode `(Deprecated) (Deprecated) renderHTMLForm` de l’objet `FormsServiceClient` et transmettez les valeurs suivantes :

   * Valeur de chaîne qui spécifie le nom de la conception de formulaire, y compris l’extension du nom de fichier. Si vous référencez une conception de formulaire faisant partie d’une application Forms, veillez à spécifier le chemin d’accès complet, tel que `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Valeur d’énumération `TransformTo` qui spécifie le type de préférence HTML. Par exemple, pour générer un formulaire HTML compatible avec le code HTML dynamique pour Internet Explorer 5.0 ou une version ultérieure, spécifiez `TransformTo.MSDHTML`.
   * Objet `com.adobe.idp.Document` contenant les données à fusionner avec le formulaire. Si vous ne souhaitez pas fusionner de données, transmettez un objet `com.adobe.idp.Document` vide.
   * Objet `HTMLRenderSpec` qui stocke les options d’exécution HTML.
   * Valeur de chaîne qui spécifie la valeur d’en-tête `HTTP_USER_AGENT`, telle que `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
   * Objet `URLSpec` qui stocke les valeurs URI requises pour générer un formulaire HTML.
   * Objet `java.util.HashMap` qui stocke les pièces jointes. Il s’agit d’un paramètre facultatif et vous pouvez spécifier `null` si vous ne souhaitez pas joindre de fichiers au formulaire.

   La méthode `(Deprecated) renderHTMLForm` renvoie un objet `FormsResult` contenant un flux de données de formulaire qui doit être écrit dans le navigateur Web client.

1. Ecrire le flux de données du formulaire dans le navigateur Web client

   * Créez un objet `com.adobe.idp.Document` en appelant la méthode `FormsResult` de l&#39;objet &quot;s `getOutputContent`.
   * Obtenez le type de contenu de l&#39;objet `com.adobe.idp.Document` en appelant sa méthode `getContentType`.
   * Définissez le type de contenu de l&#39;objet `javax.servlet.http.HttpServletResponse` en appelant sa méthode `setContentType` et en transmettant le type de contenu de l&#39;objet `com.adobe.idp.Document`.
   * Créez un objet `javax.servlet.ServletOutputStream` utilisé pour écrire le flux de données du formulaire dans le navigateur Web client en appelant la méthode `javax.servlet.h\ttp.HttpServletResponse` de l’objet `getOutputStream`.
   * Créez un objet `java.io.InputStream` en appelant la méthode `com.adobe.idp.Document` de l&#39;objet `getInputStream`.
   * Créez un tableau d’octets et remplissez-le avec le flux de données du formulaire en appelant la méthode `InputStream` de l’objet `read` et en transmettant le tableau d’octets comme argument.
   * Appelez la méthode `javax.servlet.ServletOutputStream` de l’objet `write` pour envoyer le flux de données de formulaire au navigateur Web client. Transférez le tableau d’octets à la méthode `write`.

**Voir également**

[Rendu de Forms HTML à l’aide de fichiers CSS personnalisés](#rendering-html-forms-using-custom-css-files)

[Début rapide (mode SOAP) : Rendu d’un formulaire HTML utilisant un fichier CSS à l’aide de l’API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-an-html-form-that-uses-a-css-file-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Générer un formulaire HTML utilisant un fichier CSS à l’aide de l’API de service Web {#render-an-html-form-that-uses-a-css-file-using-the-web-service-api}

Générer un formulaire HTML utilisant un fichier CSS personnalisé à l’aide de l’API Forms (service Web) :

1. Inclure les fichiers de projet

   * Créez des classes de proxy Java qui utilisent le WSDL du service Forms.
   * Incluez les classes proxy Java dans le chemin de classe.

1. Création d’un objet API Java Forms

   Créez un objet `FormsService` et définissez des valeurs d’authentification.

1. Référence au fichier CSS

   * Créez un objet `HTMLRenderSpec` en utilisant son constructeur.
   * Pour générer le formulaire HTML qui utilise un fichier CSS personnalisé, appelez la méthode `HTMLRenderSpec` de l’objet `setCustomCSSURI` et transmettez une valeur de chaîne qui spécifie l’emplacement et le nom du fichier CSS.

1. Génération d’un formulaire HTML

   Appelez la méthode `(Deprecated) renderHTMLForm` de l’objet `FormsService` et transmettez les valeurs suivantes :

   * Valeur de chaîne qui spécifie le nom de la conception de formulaire, y compris l’extension du nom de fichier. Si vous référencez une conception de formulaire faisant partie d’une application Forms, veillez à spécifier le chemin d’accès complet, tel que `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Valeur d’énumération `TransformTo` qui spécifie le type de préférence HTML. Par exemple, pour générer un formulaire HTML compatible avec le code HTML dynamique pour Internet Explorer 5.0 ou une version ultérieure, spécifiez `TransformTo.MSDHTML`.
   * Objet `BLOB` contenant les données à fusionner avec le formulaire. Si vous ne souhaitez pas fusionner les données, transmettez `null`. (Voir [Préremplissage de Forms avec des dispositions souple](/help/forms/developing/prepopulating-forms-flowable-layouts.md).)
   * Objet `HTMLRenderSpec` qui stocke les options d’exécution HTML.
   * Valeur de chaîne qui spécifie la valeur d’en-tête `HTTP_USER_AGENT`, telle que `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`. Vous pouvez transmettre une chaîne vide si vous ne souhaitez pas définir cette valeur.
   * Objet `URLSpec` qui stocke les valeurs URI requises pour générer un formulaire HTML.
   * Objet `java.util.HashMap` qui stocke les pièces jointes. Il s’agit d’un paramètre facultatif et vous pouvez spécifier `null` si vous ne souhaitez pas joindre de fichiers au formulaire.
   * Objet `com.adobe.idp.services.holders.BLOBHolder` vide renseigné par la méthode `(Deprecated) renderHTMLForm`. Cette valeur de paramètre stocke le formulaire rendu.
   * Objet `com.adobe.idp.services.holders.BLOBHolder` vide renseigné par la méthode `(Deprecated) renderHTMLForm`. Ce paramètre stocke les données XML de sortie.
   * Objet `javax.xml.rpc.holders.LongHolder` vide renseigné par la méthode `(Deprecated) renderHTMLForm`. Cet argument enregistre le nombre de pages dans le formulaire.
   * Objet `javax.xml.rpc.holders.StringHolder` vide renseigné par la méthode `(Deprecated) renderHTMLForm`. Cet argument stocke la valeur du paramètre régional.
   * Objet `javax.xml.rpc.holders.StringHolder` vide renseigné par la méthode `(Deprecated) renderHTMLForm`. Cet argument stocke la valeur de rendu HTML utilisée.
   * Un objet `com.adobe.idp.services.holders.FormsResultHolder` vide qui contiendra les résultats de cette opération.

   La méthode `(Deprecated) renderHTMLForm` remplit l’objet `com.adobe.idp.services.holders.FormsResultHolder` transmis en tant que valeur du dernier argument avec un flux de données de formulaire qui doit être écrit dans le navigateur Web client.

1. Ecrire le flux de données du formulaire dans le navigateur Web client

   * Créez un objet `FormResult` en obtenant la valeur du membre de données `com.adobe.idp.services.holders.FormsResultHolder` de l&#39;objet `value`.
   * Créez un objet `BLOB` contenant des données de formulaire en appelant la méthode `FormsResult` de l&#39;objet `getOutputContent`.
   * Obtenez le type de contenu de l&#39;objet `BLOB` en appelant sa méthode `getContentType`.
   * Définissez le type de contenu de l&#39;objet `javax.servlet.http.HttpServletResponse` en appelant sa méthode `setContentType` et en transmettant le type de contenu de l&#39;objet `BLOB`.
   * Créez un objet `javax.servlet.ServletOutputStream` utilisé pour écrire le flux de données du formulaire dans le navigateur Web client en appelant la méthode `javax.servlet.http.HttpServletResponse` de l’objet `getOutputStream`.
   * Créez un tableau d’octets et remplissez-le en appelant la méthode `BLOB` de l’objet `getBinaryData`. Cette tâche affecte le contenu de l&#39;objet `FormsResult` au tableau d&#39;octets.
   * Appelez la méthode `javax.servlet.http.HttpServletResponse` de l’objet `write` pour envoyer le flux de données de formulaire au navigateur Web client. Transférez le tableau d’octets à la méthode `write`.

**Voir également**

[Rendu de Forms HTML à l’aide de fichiers CSS personnalisés](#rendering-html-forms-using-custom-css-files)

[Appel de AEM Forms à l’aide du codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
