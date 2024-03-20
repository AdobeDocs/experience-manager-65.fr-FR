---
title: Restituer des formulaires dont les droits sont activés
description: Utilisez le service Forms pour restituer des formulaires dotés de droits d’utilisation. Vous pouvez restituer des formulaires dont les droits sont activés à l’aide de l’API Java et de l’API de service web.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 012a3a9f-542c-4ed1-a092-572bfccbdf21
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1447'
ht-degree: 77%

---

# Générer des formulaires définis avec des droits {#rendering-rights-enabled-forms}

Le service Forms peut restituer des formulaires dotés de droits d’utilisation. Les droits d’utilisation appartiennent à la fonctionnalité disponible par défaut dans Acrobat mais non dans Adobe Reader, telle que la capacité à ajouter des commentaires à un formulaire ou à remplir des champs de formulaire et enregistrer ce dernier. Les formulaires dotés de droits d’utilisation sont appelés des formulaires dont les droits sont activés. Un utilisateur qui ouvre un formulaire dont les droits sont activés dans Adobe Reader peut effectuer les opérations autorisées pour ce formulaire.

Pour appliquer des droits d’utilisation à un formulaire, le service d’extensions Acrobat Reader DC doit faire partie de votre installation d’AEM forms. En outre, vous devez disposer d’informations d’identification valides qui vous permettent d’appliquer des droits d’utilisation aux documents PDF. Car vous devez configurer correctement le service Extensions Acrobat Reader DC avant de pouvoir restituer un formulaire dont les droits sont activés. (Consultez la section [À propos du service Extensions Acrobat Reader DC](/help/forms/developing/assigning-usage-rights.md#about-the-acrobat-reader-dc-extensions-service)).

>[!NOTE]
>
>Pour restituer un formulaire doté de droits d’utilisation, vous devez utiliser un fichier XDP comme entrée, et non un fichier PDF. Dans le cas contraire, le formulaire sera toujours rendu, mais il ne s’agira pas d’un formulaire dont les droits sont activés.

>[!NOTE]
>
>Vous ne pouvez pas préremplir un formulaire avec des données XML lorsque vous spécifiez les droits d’utilisation suivants : `enableComments`, `enableCommentsOnline`, `enableEmbeddedFiles` ou `enableDigitalSignatures`. (Consultez le didacticiel de mise en route [Préremplir des formulaires avec les dispositions souple](/help/forms/developing/prepopulating-forms-flowable-layouts.md)).

>[!NOTE]
>
>Pour plus d’informations sur le service Forms, consultez la section [Références des services pour AEM Forms](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

## Résumé des étapes {#summary-of-steps}

Pour restituer un formulaire dont les droits sont activés, procédez comme suit :

1. Incluez les fichiers de projet.
1. Créez un objet API client Forms.
1. Définir les options d’exécution des droits d’utilisation
1. Restituer un formulaire dont les droits sont activés
1. Écrire le formulaire dont les droits sont activés dans le navigateur web du client

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

**Créer un objet de lʼAPI client de Forms**

Avant d’effectuer par programmation une opération de l’API du client de service Forms, vous devez créer un client de service Forms.

**Définir les options d’exécution des droits d’utilisation**

Définissez les options d’exécution des droits d’utilisation pour générer un formulaire dont les droits sont activés. Spécifiez l’alias des informations d’identification utilisées pour appliquer des droits d’utilisation à un formulaire. Une fois la valeur de l’alias définie, vous pouvez spécifier chaque droit d’utilisation à appliquer au formulaire.

**Restituer un formulaire dont les droits sont activés**

Pour restituer un formulaire dont les droits sont activés, vous devez utiliser la même logique d’application que pour restituer un formulaire sans droits d’utilisation. La seule différence est la suivante : vous devez vous assurer que les options d’exécution des droits d’utilisation sont incluses dans votre logique dʼapplication.

>[!NOTE]
>
>Lors de la restitution d’un formulaire dont les droits sont activés à l’aide de l’API de service web Forms, vous ne pouvez pas joindre de fichiers au formulaire.

**Écrire le flux de données de formulaire dans le navigateur web du client**

Lorsque le service Forms restitue un formulaire dont les droits sont activés, il renvoie un flux de données de formulaire que vous devez écrire dans le navigateur web du client. Une fois cette opération effectuée, le formulaire est visible par l’utilisateur. Un utilisateur qui consulte le formulaire dont les droits sont activés dans Adobe Reader peut effectuer les opérations autorisées pour ce formulaire.

**Voir également**

[Restituer des formulaires dont les droits sont activés à l’aide de l’API Java](#render-rights-enabled-forms-using-the-java-api)

[Générer des formulaires définis avec des droits à l’aide de l’API de service web](#render-rights-enabled-forms-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Démarrages rapides de l’API Forms Service](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Effectuer le rendu de formulaires PDF interactifs](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Créer des applications web qui génèrent des formulaires](/help/forms/developing/creating-web-applications-renders-forms.md)

### Restituer des formulaires dont les droits sont activés à l’aide de l’API Java {#render-rights-enabled-forms-using-the-java-api}

Pour restituer un formulaire dont les droits sont activés à l’aide de l’API Forms (Java), procédez comme suit :

1. Inclure les fichiers du projet

   Incluez les fichiers JAR client, tels que adobe-forms-client.jar, dans le chemin de classe de votre projet Java.

1. Créer un objet API Forms client

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `FormsServiceClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`.

1. Définir des options d’exécution des droits d’utilisation

   * Créez un objet `ReaderExtensionSpec` en utilisant son constructeur.
   * Spécifiez l’alias des informations d’identification en appelant la fonction `ReaderExtensionSpec` de `setReCredentialAlias` et indiquez une valeur string qui représente la valeur d’alias.
   * Définissez chaque droit dʼutilisation en appelant la méthode correspondante qui appartient à lʼobjet `ReaderExtensionSpec`. Cependant, vous ne pouvez définir un droit d’utilisation que si les informations d’identification que vous référencez vous le permettent. En d’autres termes, vous ne pouvez pas définir un droit d’utilisation si les informations d’identification ne vous le permettent pas. Par exemple. pour définir le droit d’utilisation qui permet à l’utilisateur de remplir des champs de formulaire et d’enregistrer le formulaire, appelez la méthode `ReaderExtensionSpec` de `setReFillIn` méthode et transmission `true`.

   >[!NOTE]
   >
   >Il n’est pas nécessaire d’appeler la variable `ReaderExtensionSpec` de `setReCredentialPassword` . Cette méthode n’est pas utilisée par le service Forms.

1. Générer un formulaire défini avec des droits

   Appelez la méthode `renderPDFFormWithUsageRights` de l’objet `FormsServiceClient` et transmettez les valeurs suivantes :

   * Valeur string spécifiant le nom du modèle de formulaire, y compris l’extension du nom du fichier. Si vous référencez une conception de formulaire qui fait partie d’une application Forms, veillez à spécifier le chemin dʼaccès complet, tel que `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Objet `com.adobe.idp.Document` contenant les données à fusionner avec le formulaire. Si vous ne souhaitez pas fusionner les données, transmettez un objet `com.adobe.idp.Document` vide.
   * Un objet `PDFFormRenderSpec` stockant les options d’exécution.
   * Un objet `ReaderExtensionSpec` stockant les options d’exécution des droits d’utilisation.
   * Un objet `URLSpec` contenant des valeurs URI requises par le service Forms.

   La méthode `renderPDFFormWithUsageRights` renvoie un objet `FormsResult` contenant un flux de données de formulaire qui doit être écrit dans le navigateur web client.

1. Écrire le flux de données de formulaire dans le navigateur web client

   * Créez un `com.adobe.idp.Document` en appelant la méthode `FormsResult` object’s `getOutputContent` .
   * Accédez au type de contenu de l’objet `com.adobe.idp.Document` en appelant sa méthode `getContentType`.
   * Définissez la variable `javax.servlet.http.HttpServletResponse` type de contenu de l’objet en appelant ses `setContentType` et transmettre le type de contenu de la méthode `com.adobe.idp.Document` .
   * Créez un `javax.servlet.ServletOutputStream` objet utilisé pour écrire le flux de données de formulaire dans le navigateur Web client en appelant la fonction `javax.servlet.http.HttpServletResponse` de `getOutputStream` .
   * Créez un objet `java.io.InputStream` en appelant la méthode `getInputStream` de l’objet `com.adobe.idp.Document`.
   * Créez un tableau d’octets pour le remplir avec le flux de données de formulaire en appelant la fonction `InputStream` de `read` et transmission du tableau d’octets en tant qu’argument.
   * Appeler la variable `javax.servlet.ServletOutputStream` de `write` pour envoyer le flux de données de formulaire au navigateur web client. Transmettez le tableau d’octets à la méthode `write`.

**Voir également**

[Démarrage rapide (mode SOAP) : générer un formulaire dont les droits sont activés à l’aide de l’API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-a-rights-enabled-form-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Générer des formulaires définis avec des droits à l’aide de l’API de service web {#render-rights-enabled-forms-using-the-web-service-api}

Pour générer un formulaire défini avec des droits à l’aide de l’API Forms (service web), procédez comme suit :

1. Inclure les fichiers du projet

   * Créez des classes proxy Java qui utilisent le service WSDL de Forms.
   * Incluez les classes proxy Java dans le chemin d’accès de classe.

1. Créer un objet API Forms client

   Créez un objet `FormsService` et définissez les valeurs d’authentification.

1. Définir des options d’exécution des droits d’utilisation

   * Créez un objet `ReaderExtensionSpec` en utilisant son constructeur.
   * Spécifiez l’alias des informations d’identification en appelant la fonction `ReaderExtensionSpec` de `setReCredentialAlias` et indiquez une valeur string qui représente la valeur d’alias.
   * Définissez chaque droit dʼutilisation en appelant la méthode correspondante qui appartient à lʼobjet `ReaderExtensionSpec`. Cependant, vous ne pouvez définir un droit d’utilisation que si les informations d’identification que vous référencez vous le permettent. En d’autres termes, vous ne pouvez pas définir un droit d’utilisation si les informations d’identification ne vous le permettent pas. Pour définir le droit d’utilisation qui permet à l’utilisateur de remplir des champs de formulaire et d’enregistrer le formulaire, appelez la méthode `ReaderExtensionSpec` de `setReFillIn` méthode et transmission `true`.

1. Générer un formulaire défini avec des droits

   Appelez la méthode `renderPDFFormWithUsageRights` de l’objet `FormsService` et transmettez les valeurs suivantes :

   * Valeur string spécifiant le nom du modèle de formulaire, y compris l’extension du nom du fichier. Si vous référencez une conception de formulaire qui fait partie d’une application Forms, veillez à spécifier le chemin dʼaccès complet, tel que `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Un objet `BLOB` contenant les données à fusionner avec le formulaire. Si vous ne souhaitez pas fusionner de données avec le formulaire, vous devez transmettre un objet `BLOB` basé sur une source de données XML vide. Vous ne pouvez pas transmettre un objet `BLOB` nul ; dans le cas contraire, une exception est générée.
   * Un objet `PDFFormRenderSpec` permettant de stocker les options d’exécution.
   * Un objet `ReaderExtensionSpec` stockant les options d’exécution des droits d’utilisation.
   * Un objet `URLSpec` contenant des valeurs URI requises par le service Forms.

   La méthode `renderPDFFormWithUsageRights` renvoie un objet `FormsResult` contenant un flux de données de formulaire qui doit être écrit dans le navigateur web client.

1. Écrire le flux de données de formulaire dans le navigateur web client

   * Créez un `BLOB` qui contient des données de formulaire en appelant la méthode `FormsResult` de `getOutputContent` .
   * Accédez au type de contenu de l’objet `BLOB` en appelant sa méthode `getContentType`.
   * Définissez la variable `javax.servlet.http.HttpServletResponse` type de contenu de l’objet en appelant ses `setContentType` et transmettre le type de contenu de la méthode `BLOB` .
   * Créez un `javax.servlet.ServletOutputStream` objet utilisé pour écrire le flux de données de formulaire dans le navigateur Web client en appelant la fonction `javax.servlet.http.HttpServletResponse` de `getOutputStream` .
   * Créez un tableau d’octets et renseignez-le en appelant la variable `BLOB` de `getBinaryData` . Cette tâche affecte le contenu de l’objet `FormsResult` au tableau d’octets.
   * Appeler la variable `javax.servlet.http.HttpServletResponse` de `write` pour envoyer le flux de données de formulaire au navigateur web client. Transmettez le tableau d’octets à la méthode `write`.

**Voir également**

[Générer des formulaires définis avec des droits](#rendering-rights-enabled-forms)

[Appeler AEM Forms en utilisant le codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
