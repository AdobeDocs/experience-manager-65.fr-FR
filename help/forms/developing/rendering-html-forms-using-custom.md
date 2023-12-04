---
title: Restituer des formulaires HTML à l’aide de fichiers CSS personnalisés
description: Utilisez le service Forms pour faire référence à des fichiers CSS personnalisés afin de générer des formulaires HTML en réponse à une demande HTTP d’un navigateur web. Vous pouvez générer un formulaire HTML qui utilise un fichier CSS à l’aide de l’API Java et de l’API Web Service.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 5fa385a7-f030-4c0c-8938-0991d02ef361
source-git-commit: 10b370fd8f855f71c6d7d791c272137bb5e04d97
workflow-type: tm+mt
source-wordcount: '1682'
ht-degree: 82%

---

# Restituer des formulaires HTML à l’aide de fichiers CSS personnalisés {#rendering-html-forms-using-custom-css-files}

**Les exemples et les échantillons de ce document sont réservés à l’environnement AEM Forms sur JEE.**

Le service Forms génère les formulaires HTML en réponse à la demande HTTP d’un navigateur web. Lors du rendu d’un formulaire HTML, le service Forms peut référencer un fichier CSS personnalisé. Vous pouvez créer un fichier CSS personnalisé pour répondre aux besoins de votre entreprise et référencer ce fichier CSS lors de l’utilisation du service Forms pour le rendu des formulaires HTML.

Le service Forms analyse silencieusement le fichier CSS personnalisé. En d’autres termes, le service Forms ne signale pas les erreurs qui peuvent se produire si le fichier CSS personnalisé ne respecte pas les normes CSS. Dans ce cas, le service Forms ignore le style et continue avec les styles restants dans le fichier CSS.

La liste suivante spécifie les styles pris en charge dans un fichier CSS personnalisé :

* **Paires style-sélecteur de niveau de classe** : s’ils sont présents dans un fichier CSS personnalisé, les sélecteurs utilisés dans le formulaire HTML en tant que styles de classe sont utilisés. Les styles de classe inutilisés sont ignorés.
* **Paires style-sélecteur de niveau d’identifiant** : tous les styles d’identifiant sont utilisés s’ils le sont dans le formulaire HTML.
* **Paires style-sélecteur de niveau d’élément** : tous les styles d’élément sont utilisés s’ils le sont dans le formulaire HTML.
* **Priorité des styles** : la priorité du style (comme importante) est prise en charge et peut être utilisée dans un fichier CSS personnalisé.
* **Type de média** : une ou plusieurs paires de style-sélecteur peuvent être enveloppées dans le style @media pour définir le type de média. Le service Forms ne vérifie pas si le type de média spécifié est pris en charge. Le type de média spécifié dans le fichier CSS personnalisé est fusionné dans le formulaire HTML.

Vous pouvez récupérer un exemple de fichier CSS à l’aide de l’application FormsIVS. Téléchargez le formulaire, sélectionnez-le dans la page Tester la conception de formulaire, puis cliquez sur Générer un CSS. Il n’est pas nécessaire de définir le type de transformation HTML avant de cliquer sur le bouton. Sélectionnez ensuite Enregistrer. Vous pouvez modifier ce fichier CSS pour répondre aux besoins de votre entreprise.

>[!NOTE]
>
>Avant de générer un formulaire HTML qui utilise un fichier CSS personnalisé, il est important de bien comprendre le rendu des formulaires HTML. (Voir [Rendre des formulaires en tant que HTML](/help/forms/developing/rendering-forms-html.md).)

>[!NOTE]
>
>Pour plus d’informations sur le service Forms, consultez la section [Références des services pour AEM Forms](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

## Résumé des étapes {#summary-of-steps}

Pour afficher un formulaire HTML qui utilise un fichier CSS, effectuez les tâches suivantes :

1. Incluez les fichiers de projet.
1. Créez un objet API Java Forms.
1. Référencez le fichier CSS.
1. Effectuez le rendu d’un formulaire HTML.
1. Écrivez le flux de données du formulaire dans le navigateur web du client.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

**Créer un objet API Java Forms**

Avant de pouvoir effectuer par programmation une opération prise en charge par le service Forms, vous devez créer un objet client Forms.

**Référencer le fichier CSS**

Pour afficher un formulaire HTML utilisant un fichier CSS personnalisé, veillez à référencer un fichier CSS existant.

**Effectuer le rendu d’un formulaire HTML**

Pour effectuer le rendu d’un formulaire HTML, spécifiez une conception de formulaire qui a été créée dans Designer et enregistrée en tant que fichier XDP. Sélectionnez un type de transformation de HTML. Par exemple, vous pouvez spécifier le type de transformation HTML qui effectue le rendu d’un HTML dynamique pour Internet Explorer 5.0 ou version ultérieure.

Le rendu d’un formulaire HTML nécessite également des valeurs, telles que les valeurs URI nécessaires au rendu d’autres types de formulaires.

**Écrire le flux de données de formulaire dans le navigateur web client**

Lorsque le service Forms affiche un formulaire HTML, il renvoie un flux de données de formulaire que vous devez écrire dans le navigateur web client pour que le formulaire HTML soit visible par l’utilisateur.

**Voir également**

[Rendre un formulaire HTML utilisant un fichier CSS à l’aide de l’API Java](#render-an-html-form-that-uses-a-css-file-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Démarrages rapides de l’API Forms Service](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Effectuer le rendu de formulaires PDF interactifs](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Effectuer le rendu de formulaires en HTML](/help/forms/developing/rendering-forms-html.md)

[Créer des applications web qui génèrent des formulaires](/help/forms/developing/creating-web-applications-renders-forms.md)

## Rendre un formulaire HTML utilisant un fichier CSS à l’aide de l’API Java {#render-an-html-form-that-uses-a-css-file-using-the-java-api}

Rendez un formulaire HTML utilisant un fichier CSS personnalisé à l’aide de l’API Forms (Java) :

1. Inclure les fichiers du projet

   Incluez les fichiers JAR client, tels que adobe-forms-client.jar, dans le chemin de classe de votre projet Java.

1. Créer un objet API Java Forms

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `FormsServiceClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`. 

1. Référencer le fichier CSS

   * Créez un objet `HTMLRenderSpec` en utilisant son constructeur.
   * Pour effectuer le rendu du HTML qui utilise un fichier CSS personnalisé, appelez la méthode `HTMLRenderSpec` de `setCustomCSSURI` et transmettez une valeur string qui spécifie l’emplacement et le nom du fichier CSS.

1. Effectuer le rendu d’un formulaire HTML

   Appeler la variable `FormsServiceClient` de `(Deprecated) (Deprecated) renderHTMLForm` et transmettez les valeurs suivantes :

   * Valeur string spécifiant le nom du modèle de formulaire, y compris l’extension du nom du fichier. Si vous référencez une conception de formulaire faisant partie d’une application Forms, veillez à spécifier le chemin complet, tel que `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Une valeur d’énumération `TransformTo` spécifiant le type de préférence HTML. Par exemple, pour effectuer le rendu d’un formulaire HTML compatible avec le HTML dynamique pour Internet Explorer 5.0 ou version ultérieure, spécifiez `TransformTo.MSDHTML`.
   * Objet `com.adobe.idp.Document` contenant les données à fusionner avec le formulaire. Si vous ne souhaitez pas fusionner des données, transmettez un objet `com.adobe.idp.Document`.
   * L’objet `HTMLRenderSpec` qui stocke les options d’exécution HTML.
   * Une valeur de chaîne qui spécifie la valeur dʼen-tête `HTTP_USER_AGENT`, telle que `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
   * Un objet `URLSpec` qui stocke les valeurs URI nécessaires à la restitution dʼun formulaire HTML.
   * Un objet `java.util.HashMap` qui stocke les pièces jointes. Il s’agit d’un paramètre facultatif, si vous ne souhaitez pas joindre de fichier au formulaire, indiquez `null`.

   La méthode `(Deprecated) renderHTMLForm` renvoie un objet `FormsResult` qui contient un flux de données de formulaire qui doit être écrit dans le navigateur web du client.

1. Écrire le flux de données de formulaire dans le navigateur web client

   * Créez un `com.adobe.idp.Document` en appelant la méthode `FormsResult` object’s `getOutputContent` .
   * Accédez au type de contenu de l’objet `com.adobe.idp.Document` en appelant sa méthode `getContentType`.
   * Définissez la variable `javax.servlet.http.HttpServletResponse` type de contenu de l’objet en appelant ses `setContentType` et transmettre le type de contenu de la méthode `com.adobe.idp.Document` .
   * Créez un `javax.servlet.ServletOutputStream` objet utilisé pour écrire le flux de données de formulaire dans le navigateur Web client en appelant la fonction `javax.servlet.h\ttp.HttpServletResponse` de `getOutputStream` .
   * Créez un `java.io.InputStream` en appelant la méthode `com.adobe.idp.Document` de `getInputStream` .
   * Créez un tableau d’octets et renseignez-le avec le flux de données de formulaire en appelant la fonction `InputStream` de `read` et transmission du tableau d’octets en tant qu’argument.
   * Appeler la variable `javax.servlet.ServletOutputStream` de `write` pour envoyer le flux de données de formulaire au navigateur web client. Transmettez le tableau d’octets à la méthode `write`.

**Voir également**

[Restituer des formulaires HTML à l’aide de fichiers CSS personnalisés](#rendering-html-forms-using-custom-css-files)

[Didacticiel de mise en route (mode SOAP) : restituer un formulaire HTML utilisant un fichier CSS à l’aide de l’API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-an-html-form-that-uses-a-css-file-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Restituer un formulaire HTML utilisant un fichier CSS à l’aide de l’API de service web {#render-an-html-form-that-uses-a-css-file-using-the-web-service-api}

Restituez un formulaire HTML utilisant un fichier CSS personnalisé à l’aide de l’API Forms (service web) :

1. Inclure les fichiers du projet

   * Créez des classes proxy Java qui utilisent le service WSDL de Forms.
   * Incluez les classes proxy Java dans votre chemin de classe.

1. Créer un objet API Java Forms

   Créez un objet `FormsService` et définissez les valeurs d’authentification.

1. Référencer le fichier CSS

   * Créez un objet `HTMLRenderSpec` en utilisant son constructeur.
   * Pour effectuer le rendu du HTML qui utilise un fichier CSS personnalisé, appelez la méthode `HTMLRenderSpec` de `setCustomCSSURI` et transmettez une valeur string qui spécifie l’emplacement et le nom du fichier CSS.

1. Effectuer le rendu d’un formulaire HTML

   Appeler la variable `FormsService` de `(Deprecated) renderHTMLForm` et transmettez les valeurs suivantes :

   * Valeur string spécifiant le nom du modèle de formulaire, y compris l’extension du nom du fichier. Si vous référencez une conception de formulaire faisant partie d’une application Forms, veillez à spécifier le chemin complet, tel que `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Une valeur d’énumération `TransformTo` spécifiant le type de préférence HTML. Par exemple, pour effectuer le rendu d’un formulaire HTML compatible avec le HTML dynamique pour Internet Explorer 5.0 ou version ultérieure, spécifiez `TransformTo.MSDHTML`.
   * Objet `BLOB` contenant les données à fusionner avec le formulaire. Si vous ne souhaitez pas fusionner des données, transmettez `null`. (Voir [Préremplir des formulaires avec des mises en page modulables](/help/forms/developing/prepopulating-forms-flowable-layouts.md).)
   * Lʼobjet `HTMLRenderSpec` qui stocke les options d’exécution HTML.
   * Une valeur de chaîne qui spécifie la valeur d’en-tête `HTTP_USER_AGENT`, telle que `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`. Vous pouvez transmettre une chaîne vide si vous ne souhaitez pas définir cette valeur.
   * Un objet `URLSpec` qui stocke les valeurs URI nécessaires à la restitution dʼun formulaire HTML.
   * Un objet `java.util.HashMap` qui stocke les pièces jointes. Il s’agit d’un paramètre facultatif. Si vous ne souhaitez pas joindre de fichier au formulaire, spécifiez `null`.
   * Un objet `com.adobe.idp.services.holders.BLOBHolder` vide renseigné par la méthode `(Deprecated) renderHTMLForm`. La valeur de ce paramètre enregistre le formulaire rendu.
   * Un objet `com.adobe.idp.services.holders.BLOBHolder` vide, renseigné par la méthode `(Deprecated) renderHTMLForm`. Ce paramètre stocke les données XML de sortie.
   * Un objet `javax.xml.rpc.holders.LongHolder` vide, renseigné par la méthode `(Deprecated) renderHTMLForm`. Cet argument stocke le nombre de pages du formulaire.
   * Un objet `javax.xml.rpc.holders.StringHolder` vide, renseigné par la méthode `(Deprecated) renderHTMLForm`. Cet argument stocke la valeur du paramètre régional.
   * Un objet `javax.xml.rpc.holders.StringHolder` vide, renseigné par la méthode `(Deprecated) renderHTMLForm`. Cet argument stocke la valeur de rendu HTML utilisée.
   * Un objet `com.adobe.idp.services.holders.FormsResultHolder` vide qui contiendra les résultats de cette opération.

   La méthode `(Deprecated) renderHTMLForm` renseigne l’objet `com.adobe.idp.services.holders.FormsResultHolder` qui est transmis en tant que dernière valeur d’argument avec un flux de données de formulaire qui doit être écrit dans le navigateur web client.

1. Écrire le flux de données de formulaire dans le navigateur web client

   * Créez un `FormResult` en obtenant la valeur de la variable `com.adobe.idp.services.holders.FormsResultHolder` de `value` membre de données.
   * Créez un `BLOB` qui contient des données de formulaire en appelant la méthode `FormsResult` de `getOutputContent` .
   * Accédez au type de contenu de l’objet `BLOB` en appelant sa méthode `getContentType`.
   * Définissez la variable `javax.servlet.http.HttpServletResponse` type de contenu de l’objet en appelant ses `setContentType` et transmettre le type de contenu de la méthode `BLOB` .
   * Créez un `javax.servlet.ServletOutputStream` objet utilisé pour écrire le flux de données de formulaire dans le navigateur Web client en appelant la fonction `javax.servlet.http.HttpServletResponse` de `getOutputStream` .
   * Créez un tableau d’octets et renseignez-le en appelant la variable `BLOB` de `getBinaryData` . Cette tâche affecte le contenu de l’objet `FormsResult` au tableau d’octets.
   * Appeler la variable `javax.servlet.http.HttpServletResponse` de `write` pour envoyer le flux de données de formulaire au navigateur web client. Transmettez le tableau d’octets à la méthode `write`.

**Voir également**

[Restituer des formulaires HTML à l’aide de fichiers CSS personnalisés](#rendering-html-forms-using-custom-css-files)

[Appeler AEM Forms en utilisant le codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
