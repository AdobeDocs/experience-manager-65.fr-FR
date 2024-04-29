---
title: Rendu des formulaires au niveau du client
description: Optimisez la diffusion du contenu PDF et améliorez la capacité du service Forms à gérer la charge du réseau en utilisant la fonctionnalité de rendu côté client d’Acrobat ou d’Adobe Reader.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: e485980d-f200-46b7-9284-c9996003aa47
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: ht
source-wordcount: '1690'
ht-degree: 100%

---

# Rendu des formulaires au niveau du client {#rendering-forms-at-the-client}

**Les exemples et les échantillons de ce document sont réservés à l’environnement AEM Forms sur JEE.**

## Rendu des formulaires au niveau du client {#rendering-forms-at-the-client-inner}

Vous pouvez optimiser la diffusion de contenu PDF et améliorer la capacité du service Forms à gérer la charge du réseau à l’aide de la fonctionnalité de rendu côté client d’Acrobat ou d’Adobe Reader. Ce processus est connu sous le nom de rendu d’un formulaire au niveau du client. Pour effectuer le rendu d’un formulaire au niveau du client, l’appareil client (généralement un navigateur web) doit utiliser Acrobat 7.0 ou Adobe Reader 7.0 ou une version ultérieure.

Les modifications apportées à un formulaire par l’exécution d’un script côté serveur ne sont pas prises en compte dans un formulaire rendu au niveau du client, sauf si le sous-formulaire racine contient l’attribut `restoreState` défini sur `auto`. Pour plus d’informations sur cet attribut, voir [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63_fr).

>[!NOTE]
>
>Pour plus d’informations sur le service Forms, voir [Références des services pour AEM Forms](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

### Résumé des étapes {#summary-of-steps}

Pour effectuer le rendu d’un formulaire au niveau du client, effectuez les tâches suivantes :

1. Incluez les fichiers de projet.
1. Créez un objet API client Forms.
1. Définissez les options d’exécution du rendu client.
1. Rendez un formulaire au niveau du client.
1. Écrivez le formulaire dans le navigateur web du client.

**Inclure des fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

**Créer un objet API client Forms**

Avant d’effectuer par programmation une opération d’API client de service Forms, vous devez créer un client de service Forms. Si vous utilisez l’API Java, créez un objet `FormsServiceClient`. Si vous utilisez l’API Web Service Forms, créez un objet `FormsService`.

**Définir les options d’exécution du rendu client**

Définissez l’option d’exécution du rendu client pour effectuer le rendu d’un formulaire au niveau du client en définissant l’option d’exécution `RenderAtClient` sur `true`. Le formulaire est ainsi livré à l’appareil client où il est rendu. Si `RenderAtClient` est `auto` (la valeur par défaut), la conception du formulaire détermine si le formulaire est rendu au niveau du client. La conception du formulaire doit être une conception de formulaire avec une disposition souple.

Une option d’exécution facultative que vous pouvez définir est l’option `SeedPDF`. L’option `SeedPDF` combine le conteneur PDF (document PDF d’origine) avec la conception du formulaire et les données XML. La conception du formulaire et les données XML sont transmises à Acrobat ou à Adobe Reader, où le formulaire est rendu. L’option `SeedPDF` peut être utilisée lorsque l’ordinateur client ne dispose pas des polices utilisées dans le formulaire, par exemple lorsqu’un utilisateur final n’est pas autorisé à utiliser une police que le propriétaire du formulaire est autorisé à utiliser.

Vous pouvez utiliser Designer pour créer un fichier PDF dynamique simple à utiliser comme fichier PDF d’origine. Pour effectuer cette tâche, les étapes suivantes sont nécessaires :

1. Déterminez si vous devez incorporer des polices dans le fichier PDF d’origine. Le fichier PDF d’origine doit contenir les polices supplémentaires requises par le formulaire qui est en cours de rendu. Lorsque vous incorporez des polices dans le fichier PDF d’origine, assurez-vous de ne pas enfreindre les accords de licence des polices. Dans Designer, vous pouvez déterminer si vous pouvez légalement incorporer des polices. Lors de l’enregistrement, si vous ne pouvez pas incorporer certaines polices dans le formulaire, Designer affiche un message répertoriant les polices que vous ne pouvez pas incorporer. Ce message ne s’affiche pas dans Designer pour les documents PDF statiques.
1. Si vous créez le fichier PDF d’origine dans Designer, il est recommandé d’ajouter au minimum un champ de texte contenant un message. Ce message doit être adressé aux utilisateurs de versions antérieures d’Adobe Reader et leur indiquer qu’ils doivent disposer d’Acrobat 7.0 ou d’une version ultérieure, ou d’Adobe Reader 7.0 ou d’une version ultérieure pour afficher le document.
1. Enregistrez le fichier PDF d’origine en tant que fichier PDF dynamique avec l’extension de nom du fichier PDF.

>[!NOTE]
>
>Vous n’avez pas besoin de définir l’option d’exécution du PDF d’origine pour effectuer le rendu d’un formulaire sur le client. Si vous ne spécifiez pas de PDF d’origine, le service Forms crée un shell pdf qui ne contient pas d’objets COS, mais qui contient un wrapper PDF avec le contenu XDP réel incorporé. Les étapes de cette section ne définissent pas l’option d’exécution du PDF d’origine. Pour plus d’informations sur les objets COS, consultez le Guide de référence d’Adobe PDF.

**Effectuer le rendu d’un formulaire au niveau du client**

Pour effectuer le rendu d’un formulaire au niveau du client, vous devez vous assurer que les options d’exécution du rendu client sont incluses dans votre logique d’application pour effectuer le rendu d’un formulaire.

**Écrire le flux de données de formulaire dans le navigateur web du client**

Le service Forms crée un flux de données de formulaire que vous devez écrire dans le navigateur web du client. Une fois écrit dans le navigateur web du client, le formulaire est rendu par Acrobat 7.0 ou Adobe Reader 7.0 ou une version ultérieure, et est visible par l’utilisateur.

**Voir également**

[Restituer un formulaire au client à l’aide de l’API Java](#render-a-form-at-the-client-using-the-java-api)

[Effectuer le rendu d’un formulaire au niveau du client à l’aide de l’API Web Service](#render-a-form-at-the-client-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Démarrages rapides de l’API Forms Service](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Transmettre des documents au service Forms](/help/forms/developing/passing-documents-forms-service.md)

[Créer des applications web qui génèrent des formulaires](/help/forms/developing/creating-web-applications-renders-forms.md)

### Restituer un formulaire au client à l’aide de l’API Java {#render-a-form-at-the-client-using-the-java-api}

Restituez un formulaire au client à l’aide de l’API Forms (Java) :

1. Inclure les fichiers du projet

   Incluez les fichiers clients JAR, tels qu’adobe-forms-client.jar, dans votre projet Java Classpath.

1. Créer un objet API Forms client

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `FormsServiceClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`.

1. Déterminer des options d’exécution du rendu client

   * Créez un objet `PDFFormRenderSpec` en utilisant son constructeur.
   * Définissez l’option temps d’exécution `RenderAtClient` en faisant appel à la méthode `setRenderAtClient` de l’objet `PDFFormRenderSpec` et en transmettant la valeur d’énumération `RenderAtClient.Yes`.

1. Restituer un formulaire au niveau du client

   Appelez la méthode `renderPDFForm` de l’objet `FormsServiceClient` et transmettez les valeurs suivantes :

   * Valeur string spécifiant le nom du modèle de formulaire, y compris l’extension du nom du fichier. Si vous référencez un modèle de formulaire faisant partie d’une application AEM Forms, veillez à en spécifier le chemin d’accès complet, tel que `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Objet `com.adobe.idp.Document` contenant les données à fusionner avec le formulaire. Si vous ne souhaitez pas fusionner des données, transmettez un objet `com.adobe.idp.Document` vide.
   * Objet `PDFFormRenderSpec` stockant les options d’exécution requises pour générer un formulaire au niveau du client.
   * Objet `URLSpec` contenant des valeurs URI requises par le service Forms pour générer un formulaire.
   * Objet `java.util.HashMap` stockant les pièces jointes. Ce paramètre est facultatif et vous pouvez spécifier `null` si vous ne souhaitez pas joindre de fichiers au formulaire.

   La méthode `renderPDFForm` renvoie un objet `FormsResult` contenant un flux de données de formulaire qui doit être écrit dans le navigateur web client.

1. Écrire le flux de données de formulaire dans le navigateur web client

   * Créez un objet `com.adobe.idp.Document` en appelant la méthode `getOutputContent` de l’objet `FormsResult`.
   * Accédez au type de contenu de l’objet `com.adobe.idp.Document` en appelant sa méthode `getContentType`.
   * Définissez le type de contenu de l’objet `javax.servlet.http.HttpServletResponse` en appelant sa méthode `setContentType` et en transmettant le type de contenu de l’objet `com.adobe.idp.Document`.
   * Créez un objet `javax.servlet.ServletOutputStream` utilisé pour écrire le flux de données de formulaire dans le navigateur web client en appelant la méthode `getOutputStream` de l’objet `javax.servlet.http.HttpServletResponse`.
   * Créez un objet `java.io.InputStream` en appelant la méthode `getInputStream` de l’objet `com.adobe.idp.Document`.
   * Créez un tableau d’octets et renseignez-le avec le flux de données de formulaire en appelant la méthode `read` de l’objet `InputStream` et en transmettant le tableau d’octets en tant qu’argument.
   * Appelez la méthode `write` de l’objet `javax.servlet.ServletOutputStream` pour envoyer le flux de données de formulaire au navigateur web client. Transmettez le tableau d’octets à la méthode `write`.

**Voir également**

[Démarrage rapide (mode SOAP) : rendre un formulaire au niveau du client à l’aide de l’API Java.](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-a-form-at-the-client-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Rendre un formulaire au niveau du client à l’aide de l’API Web Service {#render-a-form-at-the-client-using-the-web-service-api}

Restituez un formulaire au client à l’aide de l’API Forms (Web Service) :

1. Inclure les fichiers du projet

   * Créez des classes proxy Java qui utilisent le service WSDL de Forms.
   * Incluez les classes proxy Java dans le chemin d’accès de classe.

1. Créer un objet API Forms client

   Créez un objet `FormsService` et définissez les valeurs d’authentification.

1. Déterminer des options d’exécution du rendu client

   * Créez un objet `PDFFormRenderSpec` en utilisant son constructeur.
   * Définissez l’option de temps d’exécution `RenderAtClient` en appelant la méthode `setRenderAtClient` de l’objet `PDFFormRenderSpec` et en transmettant la valeur de la chaîne de caractères `RenderAtClient.Yes`.

1. Restituer un formulaire au niveau du client

   Appelez la méthode `renderPDFForm` de l’objet `FormsService` et transmettez les valeurs suivantes :

   * Valeur string spécifiant le nom du modèle de formulaire, y compris l’extension du nom du fichier. Si vous référencez une conception de formulaire qui fait partie d’une application Forms, veillez à spécifier le chemin dʼaccès complet, tel que `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Objet `BLOB` contenant les données à fusionner avec le formulaire. Si vous ne souhaitez pas fusionner des données, transmettez `null`. (Voir [Préremplir des formulaires avec des mises en page fluides](/help/forms/developing/prepopulating-forms-flowable-layouts.md).)
   * Objet `PDFFormRenderSpec` stockant les options d’exécution requises pour générer un formulaire au niveau du client.
   * Objet `URLSpec` contenant les valeurs URI requises par le service Forms.
   * Un objet `java.util.HashMap` qui stocke les pièces jointes. Il sʼagit dʼun paramètre facultatif. Vous pouvez indiquer `null` si vous ne souhaitez pas joindre de fichier au formulaire.
   * Objet `com.adobe.idp.services.holders.BLOBHolder` vide qui est rempli par la méthode. Ce paramètre est utilisé pour stocker le formulaire PDF rendu.
   * Objet `javax.xml.rpc.holders.LongHolder` vide qui est rempli par la méthode. (Cet argument permet de stocker le nombre de pages du formulaire).
   * Un objet `javax.xml.rpc.holders.StringHolder` vide qui est renseigné par la méthode. (Cet argument permet de stocker la valeur du paramètre régional).
   * Un objet `com.adobe.idp.services.holders.FormsResultHolder` vide qui contiendra les résultats de cette opération.

   La méthode `renderPDFForm` renseigne l’objet `com.adobe.idp.services.holders.FormsResultHolder` qui est transmis en tant que dernière valeur d’argument avec un flux de données de formulaire qui doit être écrit dans le navigateur web client.

1. Écrire le flux de données de formulaire dans le navigateur web client

   * Créez un objet `FormResult` en obtenant la valeur du membre de données `value` de l’objet `com.adobe.idp.services.holders.FormsResultHolder`.
   * Créez un objet `BLOB` contenant des données de formulaire en appelant la méthode `getOutputContent` de l’objet `FormsResult`.
   * Obtenez le type de contenu de l’objet `BLOB` en appelant sa méthode `getContentType`.
   * Définissez le type de contenu de l’objet `javax.servlet.http.HttpServletResponse` en appelant sa méthode `setContentType` et en transmettant le type de contenu de l’objet `BLOB`.
   * Créez un objet `javax.servlet.ServletOutputStream` servant à écrire le flux de données de formulaire dans le navigateur web client en appelant la méthode `getOutputStream` de l’objet `javax.servlet.http.HttpServletResponse`.
   * Créez un tableau d’octets et renseignez-le en appelant la méthode `getBinaryData` de l’objet `BLOB`. Cette tâche affecte le contenu de l’objet `FormsResult` au tableau d’octets.
   * Appelez la méthode `write` de l’objet `javax.servlet.http.HttpServletResponse` pour envoyer le flux de données de formulaire au navigateur web client. Transmettez le tableau d’octets à la méthode `write`.

**Voir également**

[Rendu des formulaires au niveau du client](#rendering-forms-at-the-client)

[Appeler AEM Forms en utilisant le codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
