---
title: Optimiser les performances du service Forms
description: Définissez les options d’exécution lors du rendu d’un formulaire et stockez les fichiers XDP dans le référentiel afin d’optimiser les performances du service Forms.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 5a746c6c-bf6e-4b25-ba7c-a35edb1f55f3
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services,APIs & Integrations
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '1424'
ht-degree: 100%

---

# Optimiser les performances du service Forms {#optimizing-the-performance-of-theforms-service}

**Les exemples et les échantillons de ce document sont réservés à l’environnement AEM Forms sur JEE.**

## Optimiser les performances du service Forms {#optimizing-the-performance-of-the-forms-service}

Lors du rendu d’un formulaire, vous pouvez définir des options d’exécution afin dʼoptimiser les performances du service Forms. Le stockage des fichiers XDP dans le référentiel permet également dʼaméliorer les performances du service Forms. Toutefois, cette procédure nʼest pas abordée dans cette section. (Consultez la section [Appeler un service à l’aide d’une bibliothèque client Java](/help/forms/developing/invoking-aem-forms-using-java.md#invoking-a-service-using-a-java-client-library)).

>[!NOTE]
>
>Pour plus d’informations sur le service Forms, consultez la section [Références des services pour AEM Forms](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

### Résumé des étapes {#summary-of-steps}

Pour optimiser les performances du service Forms lors du rendu d’un formulaire, procédez comme suit :

1. Incluez les fichiers de projet.
1. Créez un objet API client Forms.
1. Définissez les options d’exécution des performances.
1. Restituer le formulaire
1. Écrivez le flux de données du formulaire dans le navigateur web du client.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

**Créer un objet API client Forms**

Avant d’effectuer par programmation une opération d’API client de service Forms, vous devez créer un client de service Forms. Si vous utilisez l’API Java, créez un objet `FormsServiceClient`. Si vous utilisez l’API du service web Forms, créez un objet `FormsService`.

**Définir les options d’exécution des performances**

Vous pouvez définir les options d’exécution de performances suivantes afin d’améliorer les performances du service Forms :

* **Mettre les formulaires en cache**: vous pouvez mettre en cache un formulaire rendu en tant que PDF dans le cache du serveur. Chaque formulaire est mis en cache après avoir été généré pour la première fois. Lors d’un rendu ultérieur, si le formulaire mis en cache est plus récent que l’horodatage de la conception de formulaire, le formulaire est récupéré dans le cache. En mettant en cache des formulaires, vous améliorez les performances du service Forms car il n’a pas besoin de récupérer la conception de formulaire dans un référentiel.
* Le rendu des guides de formulaire (obsolète) peut prendre plus de temps que les autres types de transformation. Il est recommandé de mettre en cache les guides de formulaires (obsolète) afin d’améliorer les performances.
* **Option autonome** : si vous n’avez pas besoin du service Forms pour effectuer des calculs côté serveur, vous pouvez définir l’option Autonome sur `true`, ce qui entraîne la génération de formulaires sans informations d’état. Les informations d’état sont nécessaires si vous souhaitez générer un formulaire interactif à un utilisateur final qui saisit ensuite les informations dans le formulaire et le renvoie au service Forms. Le service Forms effectue ensuite une opération de calcul et renvoie le formulaire à l’utilisateur avec les résultats affichés dans le formulaire. Si un formulaire sans informations d’état est renvoyé au service Forms, seules les données XML sont disponibles et les calculs côté serveur ne sont pas effectués.
* **PDF linéarisé** : un document PDF linéarisé est organisé pour autoriser l’accès incrémental efficace dans un environnement réseau. Le fichier PDF est un PDF valide à tous les égards et est compatible avec toutes les visionneuses et autres applications de PDF existantes. En d’autres termes, un PDF linéarisé peut être affiché pendant son téléchargement.
* Cette option n’améliore pas les performances lorsqu’un formulaire PDF est rendu sur le client.
* **Option GuideRSL** : active la génération du guide de formulaire (obsolète) à l’aide de bibliothèques d’exécutions partagées. Cela signifie que la première demande téléchargera un fichier SWF plus petit, ainsi que des bibliothèques partagées plus volumineuses qui sont stockées dans le cache du navigateur. Pour plus d’informations, consultez la section dédiée à RSL dans la documentation de Flex.
* Vous pouvez également améliorer les performances du service Forms en effectuant le rendu d’un formulaire sur le client. (Consultez la section [Renvoyer des formulaires au client](/help/forms/developing/rendering-forms-client.md)).

**Rendre le formulaire**

Pour générer le formulaire après avoir défini les options de performances, utilisez la même logique d’application que pour générer un formulaire sans options de performances.

**Écrire le flux de données de formulaire dans le navigateur web client**

Une fois que le service Forms a rendu un formulaire, il renvoie un flux de données de formulaire que vous devez écrire dans le navigateur web client. Lorsqu’il est écrit dans le navigateur web client, le formulaire est visible par l’utilisateur.

**Voir également**

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Démarrages rapides de l’API Forms Service](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Effectuer le rendu de formulaires PDF interactifs](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Effectuer le rendu de formulaires en HTML](/help/forms/developing/rendering-forms-html.md)

[Créer des applications web qui génèrent des formulaires](/help/forms/developing/creating-web-applications-renders-forms.md)

### Optimiser les performances à l’aide de l’API Java {#optimize-the-performance-using-the-java-api}

Pour générer un formulaire avec des performances optimisées à l’aide de l’API Forms (Java), procédez comme suit :

1. Inclure les fichiers du projet

   Incluez les fichiers clients JAR, tels qu’adobe-forms-client.jar, dans votre projet Java Classpath.

1. Créer un objet API Forms client

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `FormsServiceClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`.

1. Définir les options d’exécution des performances

   * Créez un objet `PDFFormRenderSpec` en utilisant son constructeur.
   * Définissez l’option de cache de formulaire en appelant la méthode `setCacheEnabled` de l’objet `PDFFormRenderSpec` et en transmettant `true`.
   * Définissez l’option linéarisée en appelant la méthode `setLinearizedPDF` de l’objet `PDFFormRenderSpec` et en transmettant `true.`.

1. Restituer le formulaire

   Appelez la méthode `renderPDFForm` de l’objet `FormsServiceClient` et transmettez les valeurs suivantes :

   * Une valeur de chaîne qui spécifie le nom de la conception de formulaire, y compris l’extension du nom de fichier.
   * Un objet `com.adobe.idp.Document` contenant les données à fusionner avec le formulaire. Si vous ne souhaitez pas fusionner les données, transmettez un objet `com.adobe.idp.Document`.
   * Un objet `PDFFormRenderSpec` prévu pour stocker les options dʼexécution afin dʼaméliorer les performances.
   * Un objet `URLSpec` contenant les valeurs URI requises par le service Forms.
   * Un objet `java.util.HashMap` qui stocke les pièces jointes. Ce paramètre est facultatif et vous pouvez spécifier `null` si vous ne souhaitez pas joindre de fichiers au formulaire.

   La méthode `renderPDFForm` renvoie un objet `FormsResult` contenant un flux de données de formulaire qui doit être écrit dans le navigateur web client.

1. Écrire le flux de données de formulaire dans le navigateur web client

   * Créez un objet `javax.servlet.ServletOutputStream` utilisé pour envoyer un flux de données de formulaire au navigateur web du client.
   * Créez un objet `com.adobe.idp.Document` en appelant la méthode `getOutputContent` de l’objet `FormsResult`.
   * Créez un objet `java.io.InputStream` en appelant la méthode `getInputStream` de lʼobjet `com.adobe.idp.Document`.
   * Créez un tableau d’octets et renseignez-le avec le flux de données de formulaire en appelant la méthode `read` de lʼobjet `InputStream` et en transmettant le tableau d’octets comme argument.
   * Appelez la méthode `write` de lʼobjet `javax.servlet.ServletOutputStream` pour envoyer le flux de données de formulaire au navigateur web du client. Transmettez le tableau d’octets à la méthode `write`.

**Voir également**

[Démarrage rapide (mode SOAP) : optimiser les performances à l’aide de l’API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-optimizing-performance-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Optimiser les performances à l’aide de l’API de service web {#optimize-the-performance-using-the-web-service-api}

Restituer un formulaire avec des performances optimisées à l’aide de l’API Forms (service web) :

1. Inclure les fichiers du projet

   * Créez des classes proxy Java qui utilisent le service WSDL de Forms.
   * Incluez les classes proxy Java dans le chemin d’accès de classe.

1. Créer un objet API Forms client

   Créez un objet `FormsService` et définissez les valeurs d’authentification.

1. Définir les options d’exécution des performances

   * Créez un objet `PDFFormRenderSpec` en utilisant son constructeur.
   * Définissez l’option de mise en cache du formulaire en appelant la méthode `PDFFormRenderSpec` de lʼobjet `setCacheEnabled` et en transmettant la valeur « true ».
   * Définissez l’option autonome en appelant la méthode `setStandAlone` de lʼobjet `PDFFormRenderSpec` et en transmettant la valeur « true ».
   * Définissez l’option linéaire en appelant la méthode `setLinearizedPDF` de lʼobjet `PDFFormRenderSpec` et en transmettant la valeur « true ».

1. Restituer le formulaire

   Appelez la méthode `renderPDFForm` de l’objet `FormsService` et transmettez les valeurs suivantes :

   * Une valeur de chaîne qui spécifie le nom de la conception de formulaire, y compris l’extension du nom de fichier.
   * Un objet `BLOB` contenant les données à fusionner avec le formulaire. Si vous ne souhaitez pas fusionner les données, transmettez `null`.
   * Un objet `PDFFormRenderSpecc` prévu pour stocker les options d’exécution.
   * Un objet `URLSpec` contenant des valeurs URI requises par le service Forms.
   * Un objet `java.util.HashMap` qui stocke les pièces jointes. Il sʼagit dʼun paramètre facultatif. Vous pouvez indiquer `null` si vous ne souhaitez pas joindre de fichier au formulaire.
   * Un objet `com.adobe.idp.services.holders.BLOBHolder` vide qui est renseigné par la méthode. Il permet de stocker le formulaire PDF rendu.
   * Un objet `javax.xml.rpc.holders.LongHolder` vide qui est renseigné par la méthode. (Cet argument permet de stocker le nombre de pages du formulaire).
   * Un objet `javax.xml.rpc.holders.StringHolder` vide qui est renseigné par la méthode. (Cet argument permet de stocker la valeur du paramètre régional).
   * Un objet `com.adobe.idp.services.holders.FormsResultHolder` vide qui contiendra les résultats de cette opération.

   La méthode `renderPDFForm` renseigne l’objet `com.adobe.idp.services.holders.FormsResultHolder` qui est transmis en tant que dernière valeur d’argument avec un flux de données de formulaire qui doit être écrit dans le navigateur web client.

1. Écrire le flux de données de formulaire dans le navigateur web client

   * Créez un objet `FormResult` en obtenant la valeur du membre de données `value` de lʼobjet `com.adobe.idp.services.holders.FormsResultHolder`.
   * Créez un objet `javax.servlet.ServletOutputStream` utilisé pour envoyer un flux de données de formulaire au navigateur web du client.
   * Créez un objet `BLOB` qui contient les données du formulaire en appelant la méthode `getOutputContent` de l’objet `FormsResult`.
   * Créez un tableau d’octets et remplissez-le en appelant la méthode `getBinaryData` de lʼobjet `BLOB`. Cette tâche affecte le contenu de l’objet `FormsResult` au tableau d’octets.
   * Appelez la méthode `write` de l’objet `javax.servlet.http.HttpServletResponse` pour envoyer le flux de données de formulaire au navigateur web client. Transmettez le tableau d’octets à la méthode `write`.

**Voir également**

[Appeler AEM Forms en utilisant le codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
