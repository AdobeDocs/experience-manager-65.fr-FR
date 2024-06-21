---
title: Rendre des formulaires par valeur
description: Utilisez l’API Forms (Java) pour effectuer le rendu d’un formulaire par valeur à l’aide de l’API Java et de l’API Web Service.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: a3a6a06d-ec90-4147-a5f0-e776a086ee12
solution: Experience Manager, Experience Manager Forms
source-git-commit: 872e2de411f51b5f0b26a2ff47cb49f01313d39f
workflow-type: tm+mt
source-wordcount: '1822'
ht-degree: 100%

---

# Rendre des formulaires par valeur {#rendering-forms-by-value}

**Les exemples et les échantillons de ce document sont réservés à l’environnement AEM Forms sur JEE.**

En règle générale, une conception de formulaire créée dans Designer est transmise par référence au service Forms. Les conceptions de formulaire peuvent être volumineuses et, par conséquent, il est plus efficace de les transmettre par référence pour éviter d’avoir à rassembler les octets de conception de formulaire par valeur. Le service Forms peut également mettre en cache la conception de formulaire de sorte qu’il n’ait pas à lire la conception de formulaire en permanence lorsqu’elle est mise en cache.

Si une conception de formulaire contient un attribut UUID, elle est mise en cache. La valeur UUID est unique pour toutes les conceptions de formulaire et sert à identifier un formulaire de manière unique. Lors du rendu d’un formulaire par valeur, le formulaire ne doit être mis en cache que s’il est utilisé à plusieurs reprises. Cependant, si le formulaire n’est pas utilisé à plusieurs reprises et doit être unique, vous pouvez éviter de le mettre en cache à l’aide des options de mise en cache définies à l’aide de l’API AEM Forms.

Le service Forms peut également résoudre l’emplacement du contenu lié dans la conception de formulaire. Par exemple, les images liées référencées à partir de la conception de formulaire sont des URL relatives. On suppose toujours que le contenu lié est relatif à l’emplacement de conception de formulaire. Par conséquent, la résolution du contenu lié consiste à déterminer son emplacement en appliquant le chemin relatif à l’emplacement de conception de formulaire absolu.

Au lieu de transmettre une conception de formulaire par référence, vous pouvez la transmettre par valeur. La transmission d’une conception de formulaire par valeur est efficace lorsque cette conception est créée de façon dynamique, c’est-à-dire lorsqu’une application client génère le code XML qui crée une conception de formulaire au moment de l’exécution. Dans ce cas, une conception de formulaire n’est pas stockée dans un référentiel physique, car elle est stockée en mémoire. Lors de la création dynamique d’une conception de formulaire au moment de l’exécution et de sa transmission par valeur, vous pouvez mettre le formulaire en cache pour améliorer les performances du service Forms.

**Limites de transmission d’un formulaire par valeur**

Les restrictions suivantes s’appliquent lorsqu’une conception de formulaire est transmise par valeur :

* Aucun contenu lié relatif ne peut être inclus dans la conception de formulaire. Toutes les images et tous les fragments doivent être incorporés dans la conception de formulaire ou être référencés de manière absolue.
* Les calculs côté serveur ne peuvent pas être effectués après le rendu du formulaire. Si le formulaire est renvoyé au service Forms, les données sont extraites et renvoyées sans aucun calcul côté serveur.
* Comme le code HTML ne peut utiliser que des images liées au moment de l’exécution, il n’est pas possible de générer du code HTML avec des images incorporées. En effet, le service Forms prend en charge les images incorporées avec le code HTML en récupérant les images d’une conception de formulaire référencée. Étant donné qu’une conception de formulaire transmise par valeur ne dispose pas d’un emplacement référencé, les images incorporées ne peuvent pas être extraites lorsque la page HTML est affichée. Par conséquent, les références d’image doivent être des chemins absolus à générer en langage HTML.

>[!NOTE]
>
>Bien que vous puissiez effectuer le rendu de différents types de formulaires par valeur (par exemple, formulaires HTML ou formulaires contenant des droits d’utilisation), cette section traite du rendu des formulaires PDF interactifs.

>[!NOTE]
>
>Pour plus d’informations sur le service Forms, voir [Guide de référence des services pour AEM Forms](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

## Résumé des étapes {#summary-of-steps}

Pour effectuer le rendu d’un formulaire par valeur, procédez comme suit :

1. Incluez les fichiers de projet.
1. Créez un objet API client Forms.
1. Référencez la conception de formulaire.
1. Effectuez le rendu d’un formulaire par valeur.
1. Écrivez le flux de données du formulaire dans le navigateur web du client.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services web, veillez à inclure les fichiers proxy.

**Créer un objet API client Forms**

Avant de pouvoir importer des données par programmation dans une API client de formulaire PDF, vous devez créer un client de service Data Integration (Intégration de données). Lors de la création d’un client de service, vous définissez les paramètres de connexion requis pour appeler un service.

**Référencer la conception de formulaire**

Lors du rendu d’un formulaire par valeur, vous devez créer un objet `com.adobe.idp.Document` contenant la conception de formulaire à générer. Vous pouvez référencer un fichier XDP existant ou créer de façon dynamique une conception de formulaire au moment de l’exécution et renseigner un élément `com.adobe.idp.Document` avec ces données.

>[!NOTE]
>
>Cette section et le tutoriel de mise en route rapide correspondant font référence à un fichier XDP existant.

**Rendre un formulaire par valeur**

Pour effectuer le rendu d’un formulaire par valeur, transmettez une instance `com.adobe.idp.Document` qui contient la conception de formulaire au paramètre `inDataDoc` de la méthode de rendu (il peut s’agir d’une des méthodes de rendu de l’objet `FormsServiceClient`, telles que `renderPDFForm`, `(Deprecated) renderHTMLForm`, etc.). Cette valeur de paramètre est normalement réservée aux données fusionnées avec le formulaire. De même, transmettez une valeur de chaîne vide au paramètre `formQuery`. Normalement, ce paramètre nécessite une valeur de chaîne qui spécifie le nom de la conception de formulaire.

>[!NOTE]
>
>Si vous souhaitez afficher des données dans le formulaire, les données doivent être spécifiées dans l’élément `xfa:datasets`. Pour plus d’informations sur l’architecture XFA, voir [https://www.pdfa.org/norm-refs/XFA-3_3.pdf](https://www.pdfa.org/norm-refs/XFA-3_3.pdf).

**Écrire le flux de données de formulaire dans le navigateur web du client**

Lorsque le service Forms effectue le rendu d’un formulaire par valeur, il renvoie un flux de données de formulaire que vous devez écrire dans le navigateur web client. Lorsqu’il est écrit dans le navigateur web client, le formulaire est visible par l’utilisateur.

**Voir également**

[Rendre un formulaire par valeur à l’aide de l’API Java](#render-a-form-by-value-using-the-java-api)

[Rendre un formulaire par valeur à l’aide de l’API de service web](#render-a-form-by-value-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Démarrages rapides de l’API Forms Service](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Transmettre des documents au service Forms](/help/forms/developing/passing-documents-forms-service.md)

[Créer des applications web qui génèrent des formulaires](/help/forms/developing/creating-web-applications-renders-forms.md)

## Rendre un formulaire par valeur à l’aide de l’API Java {#render-a-form-by-value-using-the-java-api}

Rendre un formulaire par valeur à l’aide de l’API Forms (Java) :

1. Inclure les fichiers du projet

   Incluez les fichiers clients JAR, tels qu’adobe-forms-client.jar, dans votre chemin de classe de projet Java.

1. Créer un objet API Forms client

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `FormsServiceClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`.

1. Référencer la conception de formulaire

   * Créez un `java.io.FileInputStream` représentant la conception de formulaire à rendre en utilisant son constructeur et en transmettant une valeur de chaîne spécifiant l’emplacement du fichier XDP.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Rendre un formulaire par valeur

   Appelez la méthode `renderPDFForm` de l’objet `FormsServiceClient` et transmettez les valeurs suivantes :

   * Une valeur de chaîne vide. (Normalement, ce paramètre nécessite une valeur de chaîne qui indique le nom de la conception de formulaire.)
   * Un objet `com.adobe.idp.Document` contenant la conception de formulaire. Normalement, cette valeur de paramètre est réservée aux données fusionnées avec le formulaire.
   * Un objet `PDFFormRenderSpec` stockant les options d’exécution. Ce paramètre est facultatif et vous pouvez indiquer `null` si vous ne souhaitez pas spécifier d’options d’exécution.
   * Un objet `URLSpec` contenant des valeurs URI requises par le service Forms.
   * Un objet `java.util.HashMap` qui stocke les pièces jointes. Ce paramètre est facultatif et vous pouvez spécifier `null` si vous ne souhaitez pas joindre de fichiers au formulaire.

   La méthode `renderPDFForm` renvoie un objet `FormsResult` contenant un flux de données de formulaire pouvant être écrit dans le navigateur web client.

1. Écrire le flux de données de formulaire dans le navigateur web client

   * Créez un objet `com.adobe.idp.Document` en appelant la méthode `getOutputContent` de l’objet `FormsResult`.
   * Obtenez le type de contenu de l’objet `com.adobe.idp.Document` en appelant sa méthode `getContentType`.
   * Définissez le type de contenu de l’objet `javax.servlet.http.HttpServletResponse` en appelant sa méthode `setContentType` et en transmettant le type de contenu de l’objet `com.adobe.idp.Document`.
   * Créez un objet `javax.servlet.ServletOutputStream` utilisé pour écrire le flux de données de formulaire dans le navigateur web client en appelant la méthode `getOutputStream` de l’objet `javax.servlet.http.HttpServletResponse`.
   * Créez un objet `java.io.InputStream` en appelant la méthode `getInputStream` de l’objet `com.adobe.idp.Document`.
   * Créez un tableau d’octets et affectez la taille de l’objet `InputStream`. Appelez la méthode `available` de l’objet `InputStream` pour obtenir la taille de l’objet `InputStream`.
   * Renseignez le tableau d’octets avec le flux de données de formulaire en appelant la méthode `read` de l’objet `InputStream` et en transmettant le tableau d’octets en tant qu’argument.
   * Appelez la méthode `write` de l’objet `javax.servlet.ServletOutputStream` pour envoyer le flux de données de formulaire au navigateur web client. Transmettez le tableau d’octets à la méthode `write`.

**Voir également**

[Rendre des formulaires par valeur](/help/forms/developing/rendering-forms.md)

[Démarrage rapide (mode SOAP) : Rendu par valeur à l’aide de l’API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-by-value-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Rendre un formulaire par valeur à l’aide de l’API de service web {#render-a-form-by-value-using-the-web-service-api}

Rendre un formulaire par valeur à l’aide de l’API Forms (service web) :

1. Inclure les fichiers du projet

   * Créez des classes proxy Java qui utilisent le service WSDL de Forms.
   * Incluez les classes proxy Java dans le chemin d’accès de classe.

1. Créer un objet API Forms client

   Créez un objet `FormsService` et définissez les valeurs d’authentification.

1. Référencer la conception de formulaire

   * Créez un objet `java.io.FileInputStream` en utilisant son constructeur. Transmettez une valeur de chaîne spécifiant l’emplacement du fichier XDP.
   * Créez un objet `BLOB` en utilisant son constructeur. L’objet `BLOB` sert à stocker un document PDF chiffré avec un mot de passe.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `java.io.FileInputStream`. Vous pouvez déterminer la taille du tableau d’octets en obtenant la taille de l’objet `java.io.FileInputStream` à l’aide de sa méthode `available`.
   * Renseignez le tableau d’octets avec les données de flux en appelant la méthode `read` de l’objet `java.io.FileInputStream` et en transmettant le tableau d’octets.
   * Renseignez l’objet `BLOB` en appelant sa méthode `setBinaryData` et en transmettant le tableau d’octets.

1. Rendre un formulaire par valeur

   Appelez la méthode `renderPDFForm` de l’objet `FormsService` et transmettez les valeurs suivantes :

   * Une valeur de chaîne vide. (Normalement, ce paramètre nécessite une valeur de chaîne qui indique le nom de la conception de formulaire.)
   * Un objet `BLOB` contenant la conception de formulaire. Normalement, cette valeur de paramètre est réservée aux données fusionnées avec le formulaire.
   * Un objet `PDFFormRenderSpec` stockant les options d’exécution. Ce paramètre est facultatif et vous pouvez indiquer `null` si vous ne souhaitez pas spécifier d’options d’exécution.
   * Un objet `URLSpec` contenant des valeurs URI requises par le service Forms.
   * Un objet `java.util.HashMap` qui stocke les pièces jointes. Il sʼagit dʼun paramètre facultatif. Vous pouvez indiquer `null` si vous ne souhaitez pas joindre de fichier au formulaire.
   * Un objet `com.adobe.idp.services.holders.BLOBHolder` vide qui est renseigné par la méthode. Il permet de stocker le formulaire PDF rendu.
   * Objet `javax.xml.rpc.holders.LongHolder` vide qui est renseigné par la méthode. (Cet argument stocke le nombre de pages dans le formulaire.)
   * Objet `javax.xml.rpc.holders.StringHolder` vide qui est renseigné par la méthode. (Cet argument stocke la valeur des paramètres régionaux.)
   * Objet `com.adobe.idp.services.holders.FormsResultHolder` vide qui contiendra les résultats de cette opération.

   La méthode `renderPDFForm` renseigne l’objet `com.adobe.idp.services.holders.FormsResultHolder` qui est transmis en tant que dernière valeur d’argument avec un flux de données de formulaire qui doit être écrit dans le navigateur web client.

1. Écrire le flux de données de formulaire dans le navigateur web client

   * Créez un objet `FormResult` en obtenant la valeur du membre de données `value` de l’objet `com.adobe.idp.services.holders.FormsResultHolder`.
   * Créez un objet `BLOB` qui contient les données du formulaire en appelant la méthode `getOutputContent` de l’objet `FormsResult`.
   * Obtenez le type de contenu de l’objet `BLOB` en appelant sa méthode `getContentType`.
   * Définissez le type de contenu de l’objet `javax.servlet.http.HttpServletResponse` en appelant sa méthode `setContentType` et en transmettant le type de contenu de l’objet `BLOB`.
   * Créez un objet `javax.servlet.ServletOutputStream` utilisé pour écrire le flux de données de formulaire dans le navigateur web client en appelant la méthode `getOutputStream` de l’objet `javax.servlet.http.HttpServletResponse`.
   * Créez un tableau d’octets et renseignez-le en appelant la méthode `getBinaryData` de l’objet `BLOB`. Cette tâche affecte le contenu de l’objet `FormsResult` au tableau d’octets.
   * Appelez la méthode `write` de l’objet `javax.servlet.http.HttpServletResponse` pour envoyer le flux de données du formulaire vers le navigateur web du client. Transmettez le tableau d’octets à la méthode `write`.

**Voir également**

[Rendre des formulaires par valeur](#rendering-forms-by-value)

[Appeler AEM Forms en utilisant le codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
