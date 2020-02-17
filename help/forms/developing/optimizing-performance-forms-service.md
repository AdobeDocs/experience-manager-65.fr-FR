---
title: Optimisation des performances du service Forms
seo-title: Optimisation des performances du service Forms
description: 'null'
seo-description: 'null'
uuid: 9040c09a-e5d0-432b-b1c5-ad46ab57c4fc
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 9f883483-b81e-42c6-a4a1-eb499dd112e7
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Optimisation des performances du service Forms {#optimizing-the-performance-of-theforms-service}

## Optimisation des performances du service Forms {#optimizing-the-performance-of-the-forms-service}

Lors du rendu d’un formulaire, vous pouvez définir des options d’exécution qui optimiseront les performances du service Forms. Une autre tâche que vous pouvez effectuer pour améliorer les performances du service Forms consiste à stocker des fichiers XDP dans le référentiel. Toutefois, cette section ne décrit pas comment effectuer cette tâche. (See [Invoking a service using a Java client library](/help/forms/developing/invoking-aem-forms-using-java.md#invoking-a-service-using-a-java-client-library).)

>[!NOTE]
>
>For more information about the Forms service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary-of-steps}

Pour optimiser les performances du service Forms lors de la génération d’un formulaire, effectuez les tâches suivantes :

1. Incluez des fichiers de projet.
1. Créez un objet API Client Forms.
1. Définissez les options d’exécution des performances.
1. Générer le formulaire.
1. Ecrivez le flux de données du formulaire dans le navigateur Web client.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

**Création d’un objet API du client Forms**

Avant de pouvoir exécuter par programmation une opération d’API Client de service Forms, vous devez créer un client de service Forms. Si vous utilisez l’API Java, créez un `FormsServiceClient` objet. Si vous utilisez l’API du service Web de Forms, créez un `FormsService` objet.

**Définition des options d’exécution des performances**

Vous pouvez définir les options d’exécution de performances suivantes pour améliorer les performances du service Forms :

* **Mise en cache** des formulaires : Vous pouvez mettre en cache un formulaire rendu au format PDF dans le cache du serveur. Chaque formulaire est mis en cache après avoir été généré pour la première fois. Sur un rendu ultérieur, si le formulaire mis en cache est plus récent que l’horodatage de conception de formulaire, le formulaire est récupéré depuis le cache. En mettant en cache des formulaires, vous améliorez les performances du service Forms, car il n’est pas nécessaire de récupérer la conception de formulaire à partir d’un référentiel.
* Le rendu des guides de formulaire (obsolète) peut prendre plus de temps que celui des autres types de transformation. Il est recommandé de mettre en cache les guides de formulaire (obsolète) afin d’améliorer les performances.
* **Option** autonome : Si vous n’avez pas besoin du service Forms pour effectuer des calculs côté serveur, vous pouvez définir l’option Autonome sur `true`, ce qui génère des formulaires sans informations d’état. Les informations d’état sont nécessaires si vous souhaitez rendre un formulaire interactif à un utilisateur final qui entre ensuite les informations dans le formulaire et envoie le formulaire au service Forms. Le service Forms effectue ensuite une opération de calcul et renvoie le formulaire à l’utilisateur avec les résultats affichés dans le formulaire. Si un formulaire sans informations d’état est renvoyé au service Forms, seules les données XML sont disponibles et les calculs côté serveur ne sont pas effectués.
* **PDF** linéarisé : Un fichier PDF linéarisé est organisé pour permettre un accès incrémentiel efficace dans un environnement réseau. Le fichier PDF est valide à tous égards et compatible avec toutes les visionneuses et autres applications PDF existantes. En d’autres termes, un PDF linéarisé peut être affiché pendant son téléchargement.
* Cette option n’améliore pas les performances lorsqu’un formulaire PDF est rendu sur le client.
* **Option** GuideRSL : Active la génération de guides de formulaire (obsolète) à l’aide de bibliothèques partagées à l’exécution. Cela signifie que la première requête téléchargera un fichier SWF plus petit, ainsi que des bibliothèques partagées plus grandes qui sont stockées dans le cache du navigateur. Pour plus d’informations, voir RSL dans la documentation Flex.
* Vous pouvez également améliorer les performances du service Forms en affichant un formulaire sur le client. (voir [Rendu de formulaires sur le client](/help/forms/developing/rendering-forms-client.md)).

**Rendu du formulaire**

Pour générer le formulaire après avoir défini les options de performances, vous utilisez la même logique applicative que pour générer un formulaire sans options de performances.

**Ecrire le flux de données du formulaire dans le navigateur Web client**

Une fois que le service Forms a généré un formulaire, il renvoie un flux de données de formulaire que vous devez écrire dans le navigateur Web client. Lorsqu’il est écrit dans le navigateur Web client, le formulaire est visible par l’utilisateur.

**Voir également**

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Démarrage rapide de l’API du service Forms](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Rendu de formulaires PDF interactifs](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Rendu des formulaires au format HTML](/help/forms/developing/rendering-forms-html.md)

[Création d&#39;applications Web qui renvoient des formulaires](/help/forms/developing/creating-web-applications-renders-forms.md)

### Optimiser les performances à l’aide de l’API Java {#optimize-the-performance-using-the-java-api}

Générer un formulaire avec des performances optimisées à l’aide de l’API Forms (Java) :

1. Inclure les fichiers de projet

   Incluez des fichiers JAR client, tels que adobe-forms-client.jar, dans le chemin de classe de votre projet Java.

1. Création d’un objet API du client Forms

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Create an `FormsServiceClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. Définition des options d’exécution des performances

   * Créez un objet `PDFFormRenderSpec` en utilisant son constructeur.
   * Définissez l’option de cache de formulaire en appelant la `PDFFormRenderSpec` méthode de l’objet et en transmettant `setCacheEnabled` `true`.
   * Définissez l’option linéarisée en appelant la `PDFFormRenderSpec` `setLinearizedPDF` méthode de l’objet et en transmettant `true.`

1. Rendu du formulaire

   Appelez la méthode `FormsServiceClient` `renderPDFForm` de l’objet et transmettez les valeurs suivantes :

   * Valeur de chaîne qui spécifie le nom de la conception de formulaire, y compris l’extension du nom de fichier.
   * Objet `com.adobe.idp.Document` contenant des données à fusionner avec le formulaire. Si vous ne souhaitez pas fusionner les données, transmettez un `com.adobe.idp.Document` objet vide.
   * Objet `PDFFormRenderSpec` qui stocke les options d’exécution pour améliorer les performances.
   * Objet `URLSpec` contenant des valeurs URI requises par le service Forms.
   * Objet `java.util.HashMap` qui stocke les pièces jointes. Il s’agit d’un paramètre facultatif que vous pouvez spécifier `null` si vous ne souhaitez pas joindre de fichiers au formulaire.
   La `renderPDFForm` méthode renvoie un `FormsResult` objet qui contient un flux de données de formulaire qui doit être écrit dans le navigateur Web client.

1. Ecrire le flux de données du formulaire dans le navigateur Web client

   * Créez un `javax.servlet.ServletOutputStream` objet utilisé pour envoyer un flux de données de formulaire au navigateur Web client.
   * Créez un `com.adobe.idp.Document` objet en appelant la `FormsResult` méthode de l’ `getOutputContent` objet.
   * Créez un `java.io.InputStream` objet en appelant la `com.adobe.idp.Document` méthode de l’ `getInputStream` objet.
   * Créez un tableau d’octets et renseignez-le avec le flux de données du formulaire en appelant la `InputStream` `read`méthode de l’objet et en transmettant le tableau d’octets comme argument.
   * Appelez la `javax.servlet.ServletOutputStream` `write` méthode de l’objet pour envoyer le flux de données du formulaire au navigateur Web client. Transmettez le tableau d’octets à la `write` méthode.

**Voir également**

[Démarrage rapide (mode SOAP) : Optimisation des performances à l’aide de l’API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-optimizing-performance-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Optimiser les performances à l’aide de l’API du service Web {#optimize-the-performance-using-the-web-service-api}

Générer un formulaire avec des performances optimisées à l’aide de l’API Forms (service Web) :

1. Inclure les fichiers de projet

   * Créez des classes de proxy Java qui utilisent le WSDL du service Forms.
   * Incluez les classes proxy Java dans le chemin de votre classe.

1. Création d’un objet API du client Forms

   Créez un `FormsService` objet et définissez des valeurs d’authentification.

1. Définition des options d’exécution des performances

   * Créez un objet `PDFFormRenderSpec` en utilisant son constructeur.
   * Définissez l’option de cache de formulaire en appelant la `PDFFormRenderSpec` `setCacheEnabled` méthode de l’objet et en transmettant true.
   * Définissez l’option autonome en appelant la `PDFFormRenderSpec` `setStandAlone` méthode de l’objet et en transmettant true.
   * Définissez l’option linéarisée en appelant la `PDFFormRenderSpec` `setLinearizedPDF` méthode de l’objet et en transmettant true.

1. Rendu du formulaire

   Appelez la méthode `FormsService` `renderPDFForm` de l’objet et transmettez les valeurs suivantes :

   * Valeur de chaîne qui spécifie le nom de la conception de formulaire, y compris l’extension du nom de fichier.
   * Objet `BLOB` contenant des données à fusionner avec le formulaire. Si vous ne souhaitez pas fusionner des données, transmettez-les `null`.
   * Objet `PDFFormRenderSpecc` qui stocke les options d’exécution.
   * Objet `URLSpec` contenant des valeurs URI requises par le service Forms.
   * Objet `java.util.HashMap` qui stocke les pièces jointes. Il s’agit d’un paramètre facultatif que vous pouvez spécifier `null` si vous ne souhaitez pas joindre de fichiers au formulaire.
   * Objet vide `com.adobe.idp.services.holders.BLOBHolder` rempli par la méthode. Elle permet de stocker le formulaire PDF rendu.
   * Objet vide `javax.xml.rpc.holders.LongHolder` rempli par la méthode. (Cet argument stocke le nombre de pages dans le formulaire).
   * Objet vide `javax.xml.rpc.holders.StringHolder` rempli par la méthode. (Cet argument stocke la valeur du paramètre régional).
   * Objet vide `com.adobe.idp.services.holders.FormsResultHolder` qui contiendra les résultats de cette opération.
   La `renderPDFForm` méthode remplit l’ `com.adobe.idp.services.holders.FormsResultHolder` objet transmis en tant que valeur du dernier argument avec un flux de données de formulaire qui doit être écrit dans le navigateur Web client.

1. Ecrire le flux de données du formulaire dans le navigateur Web client

   * Créez un `FormResult` objet en obtenant la valeur du membre `com.adobe.idp.services.holders.FormsResultHolder` de données de l’ `value` objet.
   * Créez un `javax.servlet.ServletOutputStream` objet utilisé pour envoyer un flux de données de formulaire au navigateur Web client.
   * Créez un `BLOB` objet contenant des données de formulaire en appelant la `FormsResult` méthode de l’ `getOutputContent` objet.
   * Créez un tableau d’octets et renseignez-le en appelant la méthode `BLOB` `getBinaryData` de l’objet. Cette tâche affecte le contenu de l’ `FormsResult` objet au tableau d’octets.
   * Appelez la `javax.servlet.http.HttpServletResponse` `write` méthode de l’objet pour envoyer le flux de données du formulaire au navigateur Web client. Transmettez le tableau d’octets à la `write` méthode.

**Voir également**

[Appel d’AEM Forms à l’aide du codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
