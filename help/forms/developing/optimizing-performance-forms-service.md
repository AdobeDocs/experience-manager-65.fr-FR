---
title: Optimisation des performances du service Forms
seo-title: Optimisation des performances du service Forms
description: Définissez les options d’exécution lors du rendu d’un formulaire et stockez des fichiers XDP dans le référentiel afin d’optimiser les performances du service Forms.
seo-description: Définissez les options d’exécution lors du rendu d’un formulaire et stockez des fichiers XDP dans le référentiel afin d’optimiser les performances du service Forms.
uuid: 9040c09a-e5d0-432b-b1c5-ad46ab57c4fc
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 9f883483-b81e-42c6-a4a1-eb499dd112e7
translation-type: tm+mt
source-git-commit: 9cf46a26d2aa2e41b924a4de89cf8ab5fdeeefc6
workflow-type: tm+mt
source-wordcount: '1459'
ht-degree: 6%

---


# Optimisation des performances du service Forms {#optimizing-the-performance-of-theforms-service}

**Les exemples et exemples de ce document ne concernent que l’environnement AEM Forms on JEE.**

## Optimisation des performances du service Forms {#optimizing-the-performance-of-the-forms-service}

Lors du rendu d’un formulaire, vous pouvez définir des options d’exécution qui optimiseront les performances du service Forms. Une autre tâche que vous pouvez effectuer pour améliorer les performances du service Forms est de stocker des fichiers XDP dans le référentiel. Toutefois, cette section ne décrit pas comment effectuer cette tâche. (Voir [Appel d’un service à l’aide d’une bibliothèque cliente Java](/help/forms/developing/invoking-aem-forms-using-java.md#invoking-a-service-using-a-java-client-library).)

>[!NOTE]
>
>Pour plus d’informations sur le service Forms, voir [Guide de référence des services pour AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary-of-steps}

Pour optimiser les performances du service Forms lors de la génération d’un formulaire, effectuez les tâches suivantes :

1. Incluez des fichiers de projet.
1. Créez un objet API Client Forms.
1. Définissez les options d’exécution des performances.
1. Générer le formulaire.
1. Ecrivez le flux de données du formulaire dans le navigateur Web client.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

**Création d’un objet API Client Forms**

Avant de pouvoir exécuter par programmation une opération d’API Client de service Forms, vous devez créer un client de service Forms. Si vous utilisez l’API Java, créez un objet `FormsServiceClient`. Si vous utilisez l’API du service Web Forms, créez un objet `FormsService`.

**Définition des options d’exécution des performances**

Vous pouvez définir les options d’exécution de performances suivantes pour améliorer les performances du service Forms :

* **Mise en cache** des formulaires : Vous pouvez mettre en cache un formulaire rendu au format PDF dans le cache du serveur. Chaque formulaire est mis en cache après avoir été généré pour la première fois. Sur un rendu ultérieur, si le formulaire mis en cache est plus récent que l’horodatage de conception de formulaire, le formulaire est récupéré depuis le cache. En mettant en cache des formulaires, vous améliorez les performances du service Forms, car il n’est pas nécessaire de récupérer la conception de formulaire à partir d’un référentiel.
* Le rendu des guides de formulaire (obsolète) peut prendre plus de temps que celui des autres types de transformation. Il est recommandé de mettre en cache les guides de formulaire (obsolète) afin d’améliorer les performances.
* **Option** autonome : Si vous n’avez pas besoin du service Forms pour effectuer des calculs côté serveur, vous pouvez définir l’option Autonome sur  `true`laquelle les formulaires sont générés sans informations d’état. Les informations d’état sont nécessaires si vous souhaitez rendre un formulaire interactif à un utilisateur final qui entre ensuite les informations dans le formulaire et envoie le formulaire au service Forms. Le service Forms effectue ensuite une opération de calcul et renvoie le formulaire à l’utilisateur avec les résultats affichés dans le formulaire. Si un formulaire sans informations d’état est renvoyé au service Forms, seules les données XML sont disponibles et les calculs côté serveur ne sont pas effectués.
* **PDF** linéarisé : Un fichier PDF linéarisé est organisé pour permettre un accès incrémentiel efficace dans un environnement réseau. Le fichier PDF est un fichier PDF valide à tous égards et compatible avec toutes les visionneuses et autres applications PDF existantes. En d’autres termes, un PDF linéarisé peut être affiché pendant son téléchargement.
* Cette option n’améliore pas les performances lorsqu’un formulaire PDF est rendu sur le client.
* **Option** GuideRSL : Active la génération du guide de formulaire (obsolète) à l’aide de bibliothèques partagées à l’exécution. Cela signifie que la première requête télécharge un fichier SWF plus petit, ainsi que des bibliothèques partagées plus grandes qui sont stockées dans le cache du navigateur. Pour plus d’informations, voir RSL dans la documentation Flex.
* Vous pouvez également améliorer les performances du service Forms en affichant un formulaire sur le client. (Voir [Rendu de Forms sur le client](/help/forms/developing/rendering-forms-client.md).)

**Rendu du formulaire**

Pour générer le formulaire après avoir défini les options de performances, vous utilisez la même logique d’application que pour effectuer le rendu d’un formulaire sans options de performances.

**Ecrire le flux de données du formulaire dans le navigateur Web client**

Une fois que le service Forms a rendu un formulaire, il renvoie un flux de données de formulaire que vous devez écrire dans le navigateur Web client. Lorsqu’il est écrit dans le navigateur Web client, le formulaire est visible pour l’utilisateur.

**Voir également**

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Débuts rapides de l’API du service Forms](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Rendu des PDF forms interactifs](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Rendu de Forms au format HTML](/help/forms/developing/rendering-forms-html.md)

[Création d’Applications web renvoyant Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

### Optimiser les performances à l&#39;aide de l&#39;API Java {#optimize-the-performance-using-the-java-api}

Générer un formulaire avec des performances optimisées à l’aide de l’API Forms (Java) :

1. Inclure les fichiers de projet

   Incluez des fichiers JAR client, tels que adobe-forms-client.jar, dans le chemin de classe de votre projet Java.

1. Création d’un objet API Client Forms

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `FormsServiceClient` en utilisant son constructeur et en transmettant l&#39;objet `ServiceClientFactory`.

1. Définition des options d’exécution des performances

   * Créez un objet `PDFFormRenderSpec` en utilisant son constructeur.
   * Définissez l’option de cache de formulaire en appelant la méthode `PDFFormRenderSpec` de l’objet `setCacheEnabled` et en transmettant `true`.
   * Définissez l’option linéarisée en appelant la méthode `setLinearizedPDF` de l’objet `PDFFormRenderSpec` et en transmettant `true.`

1. Rendu du formulaire

   Appelez la méthode `renderPDFForm` de l’objet `FormsServiceClient` et transmettez les valeurs suivantes :

   * Valeur de chaîne qui spécifie le nom de la conception de formulaire, y compris l’extension du nom de fichier.
   * Objet `com.adobe.idp.Document` contenant les données à fusionner avec le formulaire. Si vous ne souhaitez pas fusionner de données, transmettez un objet `com.adobe.idp.Document` vide.
   * Objet `PDFFormRenderSpec` qui stocke les options d’exécution afin d’améliorer les performances.
   * Objet `URLSpec` contenant des valeurs URI requises par le service Forms.
   * Objet `java.util.HashMap` qui stocke les pièces jointes. Il s’agit d’un paramètre facultatif et vous pouvez spécifier `null` si vous ne souhaitez pas joindre de fichiers au formulaire.

   La méthode `renderPDFForm` renvoie un objet `FormsResult` contenant un flux de données de formulaire qui doit être écrit dans le navigateur Web client.

1. Ecrire le flux de données du formulaire dans le navigateur Web client

   * Créez un objet `javax.servlet.ServletOutputStream` utilisé pour envoyer un flux de données de formulaire au navigateur Web client.
   * Créez un objet `com.adobe.idp.Document` en appelant la méthode `FormsResult` de l&#39;objet &quot;s `getOutputContent`.
   * Créez un objet `java.io.InputStream` en appelant la méthode `com.adobe.idp.Document` de l&#39;objet `getInputStream`.
   * Créez un tableau d’octets et remplissez-le avec le flux de données du formulaire en appelant la méthode `InputStream` de l’objet `read`et en transmettant le tableau d’octets comme argument.
   * Appelez la méthode `javax.servlet.ServletOutputStream` de l’objet `write` pour envoyer le flux de données de formulaire au navigateur Web client. Transférez le tableau d’octets à la méthode `write`.

**Voir également**

[Début rapide (mode SOAP) : Optimisation des performances à l’aide de l’API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-optimizing-performance-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Optimiser les performances à l’aide de l’API de service Web {#optimize-the-performance-using-the-web-service-api}

Générer un formulaire avec des performances optimisées à l’aide de l’API Forms (service Web) :

1. Inclure les fichiers de projet

   * Créez des classes de proxy Java qui utilisent le WSDL du service Forms.
   * Incluez les classes proxy Java dans votre chemin de classe.

1. Création d’un objet API Client Forms

   Créez un objet `FormsService` et définissez des valeurs d’authentification.

1. Définition des options d’exécution des performances

   * Créez un objet `PDFFormRenderSpec` en utilisant son constructeur.
   * Définissez l’option de cache de formulaire en appelant la méthode `PDFFormRenderSpec` de l’objet `setCacheEnabled` et en transmettant true.
   * Définissez l’option autonome en appelant la méthode `PDFFormRenderSpec` de l’objet `setStandAlone` et en transmettant true.
   * Définissez l’option linéarisée en appelant la méthode `PDFFormRenderSpec` de l’objet `setLinearizedPDF` et en transmettant true.

1. Rendu du formulaire

   Appelez la méthode `renderPDFForm` de l’objet `FormsService` et transmettez les valeurs suivantes :

   * Valeur de chaîne qui spécifie le nom de la conception de formulaire, y compris l’extension du nom de fichier.
   * Objet `BLOB` contenant les données à fusionner avec le formulaire. Si vous ne souhaitez pas fusionner les données, transmettez `null`.
   * Objet `PDFFormRenderSpecc` qui stocke les options d’exécution.
   * Objet `URLSpec` contenant des valeurs URI requises par le service Forms.
   * Objet `java.util.HashMap` qui stocke les pièces jointes. Il s’agit d’un paramètre facultatif et vous pouvez spécifier `null` si vous ne souhaitez pas joindre de fichiers au formulaire.
   * Objet `com.adobe.idp.services.holders.BLOBHolder` vide renseigné par la méthode. Elle permet de stocker le formulaire PDF rendu.
   * Objet `javax.xml.rpc.holders.LongHolder` vide renseigné par la méthode. (Cet argument stocke le nombre de pages dans le formulaire).
   * Objet `javax.xml.rpc.holders.StringHolder` vide renseigné par la méthode. (Cet argument stocke la valeur du paramètre régional).
   * Un objet `com.adobe.idp.services.holders.FormsResultHolder` vide qui contiendra les résultats de cette opération.

   La méthode `renderPDFForm` remplit l’objet `com.adobe.idp.services.holders.FormsResultHolder` transmis en tant que valeur du dernier argument avec un flux de données de formulaire qui doit être écrit dans le navigateur Web client.

1. Ecrire le flux de données du formulaire dans le navigateur Web client

   * Créez un objet `FormResult` en obtenant la valeur du membre de données `com.adobe.idp.services.holders.FormsResultHolder` de l&#39;objet `value`.
   * Créez un objet `javax.servlet.ServletOutputStream` utilisé pour envoyer un flux de données de formulaire au navigateur Web client.
   * Créez un objet `BLOB` contenant des données de formulaire en appelant la méthode `FormsResult` de l&#39;objet `getOutputContent`.
   * Créez un tableau d’octets et remplissez-le en appelant la méthode `BLOB` de l’objet `getBinaryData`. Cette tâche affecte le contenu de l&#39;objet `FormsResult` au tableau d&#39;octets.
   * Appelez la méthode `javax.servlet.http.HttpServletResponse` de l’objet `write` pour envoyer le flux de données de formulaire au navigateur Web client. Transférez le tableau d’octets à la méthode `write`.

**Voir également**

[Appel de AEM Forms à l’aide du codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
