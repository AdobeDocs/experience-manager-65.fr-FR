---
title: Rendu des formulaires par valeur
seo-title: Rendu des formulaires par valeur
description: 'null'
seo-description: 'null'
uuid: b932cc54-662f-40ae-94e0-20ac82845f3b
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: ddbb2b82-4c57-4845-a5be-2435902d312b
translation-type: tm+mt
source-git-commit: 66bfd6870b4c09dc2ca1b66058e0b9e040a71507

---


# Rendu des formulaires par valeur {#rendering-forms-by-value}

En règle générale, une conception de formulaire créée dans Designer est transmise par référence au service Forms. Les conceptions de formulaire peuvent être volumineuses et, par conséquent, il est plus efficace de les transmettre par référence pour éviter d’avoir à regrouper les octets de conception de formulaire par valeur. Le service Forms peut également mettre en cache la conception de formulaire de sorte qu’il n’ait pas à lire la conception de formulaire en continu lorsqu’elle est mise en cache.

Si une conception de formulaire contient un attribut UUID, il est mis en cache. La valeur UUID est unique pour toutes les conceptions de formulaire et sert à identifier un formulaire de manière unique. Lors du rendu d’un formulaire par valeur, le formulaire ne doit être mis en cache que lorsqu’il est utilisé de manière répétée. Cependant, si le formulaire n’est pas utilisé de manière répétée et doit être unique, vous pouvez éviter de le mettre en cache à l’aide des options de mise en cache définies à l’aide de l’API AEM Forms.

Le service Forms peut également résoudre l’emplacement du contenu lié dans la conception de formulaire. Par exemple, les images liées référencées dans la conception de formulaire sont des URL relatives. Le contenu lié est toujours considéré comme étant relatif à l’emplacement de la conception de formulaire. Par conséquent, la résolution du contenu lié consiste à déterminer son emplacement en appliquant le chemin relatif à l’emplacement absolu de la conception de formulaire.

Au lieu de transmettre une conception de formulaire par référence, vous pouvez transmettre une conception de formulaire par valeur. La transmission d’une conception de formulaire par valeur est efficace lorsqu’une conception de formulaire est créée dynamiquement ; c’est-à-dire lorsqu’une application cliente génère le code XML qui crée une conception de formulaire lors de l’exécution. Dans ce cas, une conception de formulaire n’est pas stockée dans un référentiel physique, car elle est stockée en mémoire. Lors de la création dynamique d’une conception de formulaire au moment de l’exécution et de sa transmission par valeur, vous pouvez mettre en cache le formulaire et améliorer les performances du service Forms.

**Limites de transmission d’un formulaire par valeur**

Les restrictions suivantes s’appliquent lorsqu’une conception de formulaire est transmise par valeur :

* Aucun contenu lié relatif ne peut figurer dans la conception de formulaire. Toutes les images et tous les fragments doivent être incorporés dans la conception de formulaire ou être référencés de manière absolue.
* Les calculs côté serveur ne peuvent pas être effectués une fois le formulaire généré. Si le formulaire est renvoyé au service Forms, les données sont extraites et renvoyées sans aucun calcul côté serveur.
* HTML ne pouvant utiliser que des images liées au moment de l’exécution, il n’est pas possible de générer du code HTML avec des images incorporées. En effet, le service Forms prend en charge les images incorporées avec du code HTML en récupérant les images d’une conception de formulaire référencée. Une conception de formulaire transmise par valeur n’ayant pas d’emplacement référencé, les images incorporées ne peuvent pas être extraites lorsque la page HTML est affichée. Par conséquent, les références d’image doivent être des chemins absolus pour être rendues en HTML.

>[!NOTE]
>
>Bien que vous puissiez générer différents types de formulaires par valeur (par exemple, des formulaires HTML ou des formulaires contenant des droits d’utilisation), cette section traite du rendu des formulaires PDF interactifs.

>[!NOTE]
>
>For more information about the Forms service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Résumé des étapes {#summary-of-steps}

Pour effectuer le rendu d’un formulaire par valeur, procédez comme suit :

1. Incluez des fichiers de projet.
1. Créez un objet API Client Forms.
1. Référencez la conception de formulaire.
1. Générer un formulaire par valeur.
1. Ecrivez le flux de données du formulaire dans le navigateur Web client.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, assurez-vous d’inclure les fichiers proxy.

**Création d’un objet API du client Forms**

Avant de pouvoir importer par programmation des données dans une API Client de formulaire PDF, vous devez créer un client de service d’intégration de données. Lors de la création d’un client de service, vous définissez les paramètres de connexion requis pour appeler un service.

**Référencer la conception de formulaire**

Lors du rendu d’un formulaire par valeur, vous devez créer un `com.adobe.idp.Document` objet contenant la conception de formulaire à générer. Vous pouvez référencer un fichier XDP existant ou créer dynamiquement une conception de formulaire au moment de l’exécution et remplir un formulaire `com.adobe.idp.Document` avec ces données.

>[!NOTE]
>
>Cette section et le rapide correspondant font référence à un fichier XDP existant.

**Générer un formulaire par valeur**

Pour effectuer le rendu d’un formulaire par valeur, transmettez une `com.adobe.idp.Document` instance contenant la conception de formulaire au `inDataDoc` paramètre de la méthode de rendu (il peut s’agir de l’une des méthodes de rendu de l’ `FormsServiceClient` objet, telles que `renderPDFForm`, `(Deprecated) renderHTMLForm`, etc.). Cette valeur de paramètre est normalement réservée aux données fusionnées avec le formulaire. De même, transmettez une valeur de chaîne vide au `formQuery` paramètre. Normalement, ce paramètre requiert une valeur de chaîne qui spécifie le nom de la conception de formulaire.

>[!NOTE]
>
>Si vous souhaitez afficher des données dans le formulaire, elles doivent être spécifiées dans l’ `xfa:datasets` élément. Pour plus d’informations sur l’architecture XFA, rendez-vous sur [https://partners.adobe.com/public/developer/xml/index_arch.html](https://partners.adobe.com/public/developer/xml/index_arch.html).

**Ecrire le flux de données du formulaire dans le navigateur Web client**

Lorsque le service Forms génère un formulaire par valeur, il renvoie un flux de données de formulaire que vous devez écrire dans le navigateur Web client. Lorsqu’il est écrit dans le navigateur Web client, le formulaire est visible par l’utilisateur.

**Voir également**

[Générer un formulaire par valeur à l’aide de l’API Java](#render-a-form-by-value-using-the-java-api)

[Générer un formulaire par valeur à l’aide de l’API du service Web](#render-a-form-by-value-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[rapide de l’API du service Forms](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Transmission de  au service Forms](/help/forms/developing/passing-documents-forms-service.md)

[Création de   de qui rend les formulaires](/help/forms/developing/creating-web-applications-renders-forms.md)

## Générer un formulaire par valeur à l’aide de l’API Java {#render-a-form-by-value-using-the-java-api}

Générer un formulaire par valeur à l’aide de l’API Forms (Java) :

1. Inclure les fichiers de projet

   Incluez des fichiers JAR client, tels que adobe-forms-client.jar, dans le chemin de classe de votre projet Java.

1. Création d’un objet API du client Forms

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Create an `FormsServiceClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. Référencer la conception de formulaire

   * Créez un `java.io.FileInputStream` objet qui représente la conception de formulaire à rendre en utilisant son constructeur et en transmettant une valeur de chaîne qui spécifie l’emplacement du fichier XDP.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Générer un formulaire par valeur

   Appelez la méthode `FormsServiceClient` `renderPDFForm` de l’objet et transmettez les valeurs suivantes :

   * Valeur de chaîne vide. (Normalement, ce paramètre nécessite une valeur de chaîne qui spécifie le nom de la conception de formulaire.)
   * Objet `com.adobe.idp.Document` contenant la conception de formulaire. Normalement, cette valeur de paramètre est réservée aux données fusionnées avec le formulaire.
   * Objet `PDFFormRenderSpec` qui stocke les options d’exécution. Il s’agit d’un paramètre facultatif que vous pouvez spécifier `null` si vous ne souhaitez pas spécifier d’options d’exécution.
   * Objet `URLSpec` contenant des valeurs URI requises par le service Forms.
   * Objet `java.util.HashMap` qui stocke les pièces jointes. Il s’agit d’un paramètre facultatif que vous pouvez spécifier `null` si vous ne souhaitez pas joindre de fichiers au formulaire.
   La `renderPDFForm` méthode renvoie un `FormsResult` objet qui contient un flux de données de formulaire pouvant être écrit dans le navigateur Web client.

1. Ecrire le flux de données du formulaire dans le navigateur Web client

   * Créez un `com.adobe.idp.Document` objet en appelant la `FormsResult` méthode de l’ `getOutputContent` objet.
   * Obtenez le type de contenu de l’ `com.adobe.idp.Document` objet en appelant sa `getContentType` méthode.
   * Définissez le type de contenu de l’ `javax.servlet.http.HttpServletResponse` objet en appelant sa `setContentType` méthode et en transmettant le type de contenu de l’ `com.adobe.idp.Document` objet.
   * Créez un `javax.servlet.ServletOutputStream` objet utilisé pour écrire le flux de données du formulaire dans le navigateur Web client en appelant la `javax.servlet.http.HttpServletResponse` `getOutputStream` méthode de l’objet.
   * Créez un `java.io.InputStream` objet en appelant la `com.adobe.idp.Document` méthode de l’ `getInputStream` objet.
   * Créez un tableau d’octets et affectez la taille de l’ `InputStream` objet. Appelez la `InputStream` méthode de l’ `available` objet pour obtenir la taille de l’ `InputStream` objet.
   * Renseignez le tableau d’octets avec le flux de données du formulaire en appelant la `InputStream` `read`méthode de l’objet et en transmettant le tableau d’octets comme argument.
   * Appelez la `javax.servlet.ServletOutputStream` `write` méthode de l’objet pour envoyer le flux de données du formulaire au navigateur Web client. Transmettez le tableau d’octets à la `write` méthode.

**Voir également**

[Rendu des formulaires par valeur](/help/forms/developing/rendering-forms.md)

[rapide (mode SOAP) : Rendu par valeur à l’aide de l’API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-by-value-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Générer un formulaire par valeur à l’aide de l’API du service Web {#render-a-form-by-value-using-the-web-service-api}

Générer un formulaire par valeur à l’aide de l’API Forms (service Web) :

1. Inclure les fichiers de projet

   * Créez des classes de proxy Java qui utilisent le WSDL du service Forms.
   * Incluez les classes proxy Java dans le chemin de votre classe.

1. Création d’un objet API du client Forms

   Créez un `FormsService` objet et définissez des valeurs d’authentification.

1. Référencer la conception de formulaire

   * Créez un objet `java.io.FileInputStream` en utilisant son constructeur. Transmettez une valeur de chaîne qui spécifie l’emplacement du fichier XDP.
   * Créez un objet `BLOB` en utilisant son constructeur. L’ `BLOB` objet est utilisé pour stocker un PDF chiffré avec un mot de passe.
   * Créez un tableau d’octets qui stocke le contenu de l’ `java.io.FileInputStream` objet. Vous pouvez déterminer la taille du tableau d’octets en obtenant la taille de l’ `java.io.FileInputStream` objet à l’aide de sa `available` méthode.
   * Renseignez le tableau d’octets avec les données de flux en appelant la `java.io.FileInputStream` `read` méthode de l’objet et en transmettant le tableau d’octets.
   * Renseignez l’ `BLOB` objet en appelant sa `setBinaryData` méthode et en transmettant le tableau d’octets.

1. Générer un formulaire par valeur

   Appelez la méthode `FormsService` `renderPDFForm` de l’objet et transmettez les valeurs suivantes :

   * Valeur de chaîne vide. (Normalement, ce paramètre nécessite une valeur de chaîne qui spécifie le nom de la conception de formulaire.)
   * Objet `BLOB` contenant la conception de formulaire. Normalement, cette valeur de paramètre est réservée aux données fusionnées avec le formulaire.
   * Objet `PDFFormRenderSpec` qui stocke les options d’exécution. Il s’agit d’un paramètre facultatif que vous pouvez spécifier `null` si vous ne souhaitez pas spécifier d’options d’exécution.
   * Objet `URLSpec` contenant des valeurs URI requises par le service Forms.
   * Objet `java.util.HashMap` qui stocke les pièces jointes. Il s’agit d’un paramètre facultatif que vous pouvez spécifier `null` si vous ne souhaitez pas joindre de fichiers au formulaire.
   * Objet vide `com.adobe.idp.services.holders.BLOBHolder` renseigné par la méthode. Elle permet de stocker le formulaire PDF rendu.
   * Objet vide `javax.xml.rpc.holders.LongHolder` renseigné par la méthode. (Cet argument stocke le nombre de pages dans le formulaire.)
   * Objet vide `javax.xml.rpc.holders.StringHolder` renseigné par la méthode. (Cet argument stocke la valeur du paramètre régional.)
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

[Rendu des formulaires par valeur](#rendering-forms-by-value)

[Appel d’AEM Forms à l’aide du codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
