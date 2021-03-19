---
title: Rendu Forms par valeur
seo-title: Rendu Forms par valeur
description: Utilisez l’API Forms (Java) pour générer un formulaire par valeur à l’aide de l’API Java et de l’API de service Web.
seo-description: Utilisez l’API Forms (Java) pour générer un formulaire par valeur à l’aide de l’API Java et de l’API de service Web.
uuid: b932cc54-662f-40ae-94e0-20ac82845f3b
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: ddbb2b82-4c57-4845-a5be-2435902d312b
role: Développeur
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1863'
ht-degree: 3%

---


# Rendu de Forms par valeur {#rendering-forms-by-value}

**Les exemples et exemples de ce document ne concernent que l’environnement AEM Forms on JEE.**

En règle générale, une conception de formulaire créée dans Designer est transmise par référence au service Forms. Les conceptions de formulaire peuvent être volumineuses et, par conséquent, il est plus efficace de les transmettre par référence pour éviter d’avoir à regrouper les octets de conception de formulaire par valeur. Le service Forms peut également mettre en cache la conception de formulaire de sorte qu’il n’ait pas à lire en continu la conception de formulaire lorsqu’elle est mise en cache.

Si une conception de formulaire contient un attribut UUID, il est mis en cache. La valeur UUID est unique pour toutes les conceptions de formulaire et sert à identifier un formulaire de manière unique. Lors de la génération d’un formulaire par valeur, le formulaire ne doit être mis en cache que s’il est utilisé à plusieurs reprises. Cependant, si le formulaire n’est pas utilisé à plusieurs reprises et doit être unique, vous pouvez éviter de le mettre en cache à l’aide des options de mise en cache définies à l’aide de l’API AEM Forms.

Le service Forms peut également résoudre l’emplacement du contenu lié dans la conception de formulaire. Par exemple, les images liées référencées dans la conception de formulaire sont des URL relatives. Le contenu lié est toujours supposé être relatif à l’emplacement de la conception de formulaire. Par conséquent, la résolution du contenu lié consiste à déterminer son emplacement en appliquant le chemin relatif à l’emplacement absolu de la conception de formulaire.

Au lieu de transmettre une conception de formulaire par référence, vous pouvez transmettre une conception de formulaire par valeur. La transmission d’une conception de formulaire par valeur est efficace lorsqu’une conception de formulaire est créée dynamiquement ; c’est-à-dire lorsqu’une application cliente génère le code XML qui crée une conception de formulaire lors de l’exécution. Dans ce cas, une conception de formulaire n’est pas stockée dans un référentiel physique, car elle est stockée en mémoire. Lors de la création dynamique d’une conception de formulaire au moment de l’exécution et de sa transmission par valeur, vous pouvez mettre en cache le formulaire et améliorer les performances du service Forms.

**Limites de transmission d’un formulaire par valeur**

Les restrictions suivantes s’appliquent lorsqu’une conception de formulaire est transmise par valeur :

* Aucun contenu lié relatif ne peut figurer dans la conception de formulaire. Toutes les images et tous les fragments doivent être incorporés dans la conception de formulaire ou être référencés de manière absolue.
* Les calculs côté serveur ne peuvent pas être effectués après la génération du formulaire. Si le formulaire est renvoyé au service Forms, les données sont extraites et renvoyées sans aucun calcul côté serveur.
* HTML ne pouvant utiliser que des images liées au moment de l’exécution, il n’est pas possible de générer du code HTML avec des images incorporées. En effet, le service Forms prend en charge les images incorporées avec du code HTML en récupérant les images d’une conception de formulaire référencée. Dans la mesure où une conception de formulaire transmise par valeur ne dispose pas d’un emplacement référencé, les images incorporées ne peuvent pas être extraites lorsque la page HTML est affichée. Par conséquent, les références d’image doivent être des chemins absolus à rendre dans HTML.

>[!NOTE]
>
>Bien que vous puissiez générer différents types de formulaires par valeur (par exemple, les formulaires HTML ou les formulaires qui contiennent des droits d’utilisation), cette section traite du rendu des PDF forms interactifs.

>[!NOTE]
>
>Pour plus d’informations sur le service Forms, voir [Guide de référence des services pour AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Résumé des étapes {#summary-of-steps}

Pour générer un formulaire par valeur, effectuez les étapes suivantes :

1. Incluez des fichiers de projet.
1. Créez un objet API Client Forms.
1. Référencez la conception de formulaire.
1. Générer un formulaire par valeur.
1. Ecrivez le flux de données du formulaire dans le navigateur Web client.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

**Création d’un objet API Client Forms**

Avant de pouvoir importer des données par programmation dans une API Client de formulaire PDF, vous devez créer un client de service d’intégration de données. Lors de la création d’un client de service, vous définissez les paramètres de connexion requis pour appeler un service.

**Référence à la conception de formulaire**

Lors du rendu d’un formulaire par valeur, vous devez créer un objet `com.adobe.idp.Document` contenant la conception de formulaire à générer. Vous pouvez référencer un fichier XDP existant ou créer dynamiquement une conception de formulaire au moment de l’exécution et renseigner `com.adobe.idp.Document` avec ces données.

>[!NOTE]
>
>Cette section et le début rapide correspondant font référence à un fichier XDP existant.

**Générer un formulaire par valeur**

Pour effectuer le rendu d’un formulaire par valeur, transmettez une instance `com.adobe.idp.Document` contenant la conception de formulaire au paramètre `inDataDoc` de la méthode de rendu (il peut s’agir de l’une des méthodes de rendu de l’objet `FormsServiceClient` telles que `renderPDFForm`, `(Deprecated) renderHTMLForm`, etc.). Cette valeur de paramètre est normalement réservée aux données fusionnées avec le formulaire. De même, transmettez une valeur de chaîne vide au paramètre `formQuery`. Normalement, ce paramètre requiert une valeur de chaîne qui spécifie le nom de la conception de formulaire.

>[!NOTE]
>
>Si vous souhaitez afficher des données dans le formulaire, les données doivent être spécifiées dans l’élément `xfa:datasets`. Pour plus d’informations sur l’architecture XFA, voir [https://partners.adobe.com/public/developer/xml/index_arch.html](https://partners.adobe.com/public/developer/xml/index_arch.html).

**Ecrire le flux de données du formulaire dans le navigateur Web client**

Lorsque le service Forms effectue le rendu d’un formulaire par valeur, il renvoie un flux de données de formulaire que vous devez écrire dans le navigateur Web client. Lorsqu’il est écrit dans le navigateur Web client, le formulaire est visible pour l’utilisateur.

**Voir également**

[Générer un formulaire par valeur à l’aide de l’API Java](#render-a-form-by-value-using-the-java-api)

[Générer un formulaire par valeur à l’aide de l’API du service Web](#render-a-form-by-value-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Débuts rapides de l’API du service Forms](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Transmission de Documents au service Forms](/help/forms/developing/passing-documents-forms-service.md)

[Création d’Applications web renvoyant Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

## Générer un formulaire par valeur à l’aide de l’API Java {#render-a-form-by-value-using-the-java-api}

Générer un formulaire par valeur à l’aide de l’API Forms (Java) :

1. Inclure les fichiers de projet

   Incluez des fichiers JAR client, tels que adobe-forms-client.jar, dans le chemin de classe de votre projet Java.

1. Création d’un objet API Client Forms

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `FormsServiceClient` en utilisant son constructeur et en transmettant l&#39;objet `ServiceClientFactory`.

1. Référence à la conception de formulaire

   * Créez un objet `java.io.FileInputStream` qui représente la conception de formulaire à rendre en utilisant son constructeur et en transmettant une valeur de chaîne qui spécifie l’emplacement du fichier XDP.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Générer un formulaire par valeur

   Appelez la méthode `renderPDFForm` de l’objet `FormsServiceClient` et transmettez les valeurs suivantes :

   * Valeur de chaîne vide. (Normalement, ce paramètre requiert une valeur de chaîne qui spécifie le nom de la conception de formulaire.)
   * Objet `com.adobe.idp.Document` contenant la conception de formulaire. Normalement, cette valeur de paramètre est réservée aux données fusionnées avec le formulaire.
   * Objet `PDFFormRenderSpec` qui stocke les options d’exécution. Il s’agit d’un paramètre facultatif et vous pouvez spécifier `null` si vous ne souhaitez pas spécifier d’options d’exécution.
   * Objet `URLSpec` contenant des valeurs URI requises par le service Forms.
   * Objet `java.util.HashMap` qui stocke les pièces jointes. Il s’agit d’un paramètre facultatif et vous pouvez spécifier `null` si vous ne souhaitez pas joindre de fichiers au formulaire.

   La méthode `renderPDFForm` renvoie un objet `FormsResult` contenant un flux de données de formulaire pouvant être écrit dans le navigateur Web client.

1. Ecrire le flux de données du formulaire dans le navigateur Web client

   * Créez un objet `com.adobe.idp.Document` en appelant la méthode `FormsResult` de l&#39;objet &quot;s `getOutputContent`.
   * Obtenez le type de contenu de l&#39;objet `com.adobe.idp.Document` en appelant sa méthode `getContentType`.
   * Définissez le type de contenu de l&#39;objet `javax.servlet.http.HttpServletResponse` en appelant sa méthode `setContentType` et en transmettant le type de contenu de l&#39;objet `com.adobe.idp.Document`.
   * Créez un objet `javax.servlet.ServletOutputStream` utilisé pour écrire le flux de données du formulaire dans le navigateur Web client en appelant la méthode `javax.servlet.http.HttpServletResponse` de l’objet `getOutputStream`.
   * Créez un objet `java.io.InputStream` en appelant la méthode `com.adobe.idp.Document` de l&#39;objet `getInputStream`.
   * Créez un tableau d’octets et affectez la taille de l’objet `InputStream`. Appelez la méthode `InputStream` de l&#39;objet `available` pour obtenir la taille de l&#39;objet `InputStream`.
   * Renseignez le tableau d’octets avec le flux de données du formulaire en appelant la méthode `InputStream` de l’objet `read`et en transmettant le tableau d’octets comme argument.
   * Appelez la méthode `javax.servlet.ServletOutputStream` de l’objet `write` pour envoyer le flux de données de formulaire au navigateur Web client. Transférez le tableau d’octets à la méthode `write`.

**Voir également**

[Rendu Forms par valeur](/help/forms/developing/rendering-forms.md)

[Début rapide (mode SOAP) : Rendu par valeur à l’aide de l’API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-by-value-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Générer un formulaire par valeur à l’aide de l’API de service Web {#render-a-form-by-value-using-the-web-service-api}

Générer un formulaire par valeur à l’aide de l’API Forms (service Web) :

1. Inclure les fichiers de projet

   * Créez des classes de proxy Java qui utilisent le WSDL du service Forms.
   * Incluez les classes proxy Java dans votre chemin de classe.

1. Création d’un objet API Client Forms

   Créez un objet `FormsService` et définissez des valeurs d’authentification.

1. Référence à la conception de formulaire

   * Créez un objet `java.io.FileInputStream` en utilisant son constructeur. Transmettez une valeur de chaîne qui spécifie l’emplacement du fichier XDP.
   * Créez un objet `BLOB` en utilisant son constructeur. L’objet `BLOB` permet de stocker un document PDF chiffré avec un mot de passe.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `java.io.FileInputStream`. Vous pouvez déterminer la taille du tableau d’octets en obtenant la taille de l’objet `java.io.FileInputStream` à l’aide de sa méthode `available`.
   * Renseignez le tableau d’octets avec les données de flux en appelant la méthode `java.io.FileInputStream` de l’objet `read` et en transmettant le tableau d’octets.
   * Renseignez l’objet `BLOB` en appelant sa méthode `setBinaryData` et en transmettant le tableau d’octets.

1. Générer un formulaire par valeur

   Appelez la méthode `renderPDFForm` de l’objet `FormsService` et transmettez les valeurs suivantes :

   * Valeur de chaîne vide. (Normalement, ce paramètre requiert une valeur de chaîne qui spécifie le nom de la conception de formulaire.)
   * Objet `BLOB` contenant la conception de formulaire. Normalement, cette valeur de paramètre est réservée aux données fusionnées avec le formulaire.
   * Objet `PDFFormRenderSpec` qui stocke les options d’exécution. Il s’agit d’un paramètre facultatif et vous pouvez spécifier `null` si vous ne souhaitez pas spécifier d’options d’exécution.
   * Objet `URLSpec` contenant des valeurs URI requises par le service Forms.
   * Objet `java.util.HashMap` qui stocke les pièces jointes. Il s’agit d’un paramètre facultatif et vous pouvez spécifier `null` si vous ne souhaitez pas joindre de fichiers au formulaire.
   * Objet `com.adobe.idp.services.holders.BLOBHolder` vide renseigné par la méthode. Elle permet de stocker le formulaire PDF rendu.
   * Objet `javax.xml.rpc.holders.LongHolder` vide renseigné par la méthode. (Cet argument stocke le nombre de pages dans le formulaire.)
   * Objet `javax.xml.rpc.holders.StringHolder` vide renseigné par la méthode. (Cet argument stocke la valeur du paramètre régional.)
   * Un objet `com.adobe.idp.services.holders.FormsResultHolder` vide qui contiendra les résultats de cette opération.

   La méthode `renderPDFForm` remplit l’objet `com.adobe.idp.services.holders.FormsResultHolder` transmis en tant que valeur du dernier argument avec un flux de données de formulaire qui doit être écrit dans le navigateur Web client.

1. Ecrire le flux de données du formulaire dans le navigateur Web client

   * Créez un objet `FormResult` en obtenant la valeur du membre de données `com.adobe.idp.services.holders.FormsResultHolder` de l&#39;objet `value`.
   * Créez un objet `BLOB` contenant des données de formulaire en appelant la méthode `FormsResult` de l&#39;objet `getOutputContent`.
   * Obtenez le type de contenu de l&#39;objet `BLOB` en appelant sa méthode `getContentType`.
   * Définissez le type de contenu de l&#39;objet `javax.servlet.http.HttpServletResponse` en appelant sa méthode `setContentType` et en transmettant le type de contenu de l&#39;objet `BLOB`.
   * Créez un objet `javax.servlet.ServletOutputStream` utilisé pour écrire le flux de données du formulaire dans le navigateur Web client en appelant la méthode `javax.servlet.http.HttpServletResponse` de l’objet `getOutputStream`.
   * Créez un tableau d’octets et remplissez-le en appelant la méthode `BLOB` de l’objet `getBinaryData`. Cette tâche affecte le contenu de l&#39;objet `FormsResult` au tableau d&#39;octets.
   * Appelez la méthode `javax.servlet.http.HttpServletResponse` de l’objet `write` pour envoyer le flux de données de formulaire au navigateur Web client. Transférez le tableau d’octets à la méthode `write`.

**Voir également**

[Rendu Forms par valeur](#rendering-forms-by-value)

[Appel de AEM Forms à l’aide du codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
