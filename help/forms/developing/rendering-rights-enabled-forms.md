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
feature: Adaptive Forms,Document Services,APIs & Integrations
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '1447'
ht-degree: 100%

---

# Générer des formulaires définis avec des droits {#rendering-rights-enabled-forms}

Le service Forms peut restituer des formulaires dotés de droits d’utilisation. Les droits d’utilisation appartiennent à la fonctionnalité disponible par défaut dans Acrobat mais non dans Adobe Reader, telle que la capacité à ajouter des commentaires à un formulaire ou à remplir des champs de formulaire et enregistrer ce dernier. Les formulaires dotés de droits d’utilisation sont appelés des formulaires dont les droits sont activés. Un utilisateur qui ouvre un formulaire dont les droits sont activés dans Adobe Reader peut effectuer les opérations autorisées pour ce formulaire.

Pour appliquer des droits d’utilisation à un formulaire, le service Extensions Acrobat Reader DC doit faire partie de votre installation d’AEM Forms. En outre, vous devez disposer d’informations d’identification valides qui vous permettent d’appliquer des droits d’utilisation aux documents PDF. Car vous devez configurer correctement le service Extensions Acrobat Reader DC avant de pouvoir restituer un formulaire dont les droits sont activés. (Consultez la section [À propos du service Extensions Acrobat Reader DC](/help/forms/developing/assigning-usage-rights.md#about-the-acrobat-reader-dc-extensions-service)).

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

Définissez les options d’exécution des droits d’utilisation pour restituer un formulaire dont les droits sont activés. Spécifiez l’alias des informations d’identification utilisé pour appliquer des droits d’utilisation à un formulaire. Une fois la valeur de l’alias définie, vous pouvez spécifier chaque droit d’utilisation à appliquer au formulaire.

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

   Incluez les fichiers clients JAR, tels qu’adobe-forms-client.jar, dans votre chemin de classe de projet Java.

1. Créer un objet API Forms client

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `FormsServiceClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`.

1. Définir des options d’exécution des droits d’utilisation

   * Créez un objet `ReaderExtensionSpec` en utilisant son constructeur.
   * Spécifiez l’alias des informations d’identification en appelant la méthode `setReCredentialAlias` de l’objet `ReaderExtensionSpec` et indiquez une valeur de chaîne qui représente la valeur d’alias.
   * Définissez chaque droit dʼutilisation en appelant la méthode correspondante qui appartient à lʼobjet `ReaderExtensionSpec`. Cependant, vous ne pouvez définir un droit d’utilisation que si les informations d’identification que vous référencez vous le permettent. En d’autres termes, vous ne pouvez pas définir un droit d’utilisation si les informations d’identification ne vous le permettent pas. Par exemple. pour définir le droit d’utilisation qui permet à l’utilisateur ou l’utilisatrice de remplir des champs de formulaire et d’enregistrer ce dernier, appelez la méthode `setReFillIn` de l’objet `ReaderExtensionSpec` et transmettez `true`.

   >[!NOTE]
   >
   >Il n’est pas nécessaire d’appeler la méthode `setReCredentialPassword` de l’objet `ReaderExtensionSpec`. Cette méthode n’est pas utilisée par le service Forms.

1. Générer un formulaire défini avec des droits

   Appelez la méthode `renderPDFFormWithUsageRights` de l’objet `FormsServiceClient` et transmettez les valeurs suivantes :

   * Valeur string spécifiant le nom du modèle de formulaire, y compris l’extension du nom du fichier. Si vous référencez une conception de formulaire qui fait partie d’une application Forms, veillez à spécifier le chemin dʼaccès complet, tel que `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Objet `com.adobe.idp.Document` contenant les données à fusionner avec le formulaire. Si vous ne souhaitez pas fusionner les données, transmettez un objet `com.adobe.idp.Document` vide.
   * Un objet `PDFFormRenderSpec` stockant les options d’exécution.
   * Un objet `ReaderExtensionSpec` stockant les options d’exécution des droits d’utilisation.
   * Un objet `URLSpec` contenant des valeurs URI requises par le service Forms.

   La méthode `renderPDFFormWithUsageRights` renvoie un objet `FormsResult` contenant un flux de données de formulaire qui doit être écrit dans le navigateur web client.

1. Écrire le flux de données de formulaire dans le navigateur web client

   * Créez un objet `com.adobe.idp.Document` en appelant la méthode `getOutputContent` de l’objet `FormsResult`.
   * Obtenez le type de contenu de l’objet `com.adobe.idp.Document` en appelant sa méthode `getContentType`.
   * Définissez le type de contenu de l’objet `javax.servlet.http.HttpServletResponse` en appelant sa méthode `setContentType` et en transmettant le type de contenu de l’objet `com.adobe.idp.Document`.
   * Créez un objet `javax.servlet.ServletOutputStream` utilisé pour écrire le flux de données de formulaire dans le navigateur web client en appelant la méthode `getOutputStream` de l’objet `javax.servlet.http.HttpServletResponse`.
   * Créez un objet `java.io.InputStream` en appelant la méthode `getInputStream` de l’objet `com.adobe.idp.Document`.
   * Créez un tableau d’octets et remplissez-le avec le flux de données du formulaire en appelant la méthode `read` de l’objet `InputStream` et en transmettant le tableau d’octets comme argument.
   * Appelez la méthode `write` de l’objet `javax.servlet.ServletOutputStream` pour envoyer le flux de données du formulaire au navigateur web du client. Transmettez le tableau d’octets à la méthode `write`.

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
   * Spécifiez l’alias des informations d’identification en appelant la méthode `setReCredentialAlias` de l’objet `ReaderExtensionSpec` et indiquez une valeur de chaîne qui représente la valeur d’alias.
   * Définissez chaque droit dʼutilisation en appelant la méthode correspondante qui appartient à lʼobjet `ReaderExtensionSpec`. Cependant, vous ne pouvez définir un droit d’utilisation que si les informations d’identification que vous référencez vous le permettent. En d’autres termes, vous ne pouvez pas définir un droit d’utilisation si les informations d’identification ne vous le permettent pas. Pour définir le droit d’utilisation permettant à l’utilisateur ou l’utilisatrice de remplir des champs de formulaire et d’enregistrer ce dernier, appelez la méthode `setReFillIn` de l’objet `ReaderExtensionSpec` et transmettez `true`.

1. Générer un formulaire défini avec des droits

   Appelez la méthode `renderPDFFormWithUsageRights` de l’objet `FormsService` et transmettez les valeurs suivantes :

   * Valeur string spécifiant le nom du modèle de formulaire, y compris l’extension du nom du fichier. Si vous référencez une conception de formulaire qui fait partie d’une application Forms, veillez à spécifier le chemin dʼaccès complet, tel que `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Un objet `BLOB` contenant les données à fusionner avec le formulaire. Si vous ne souhaitez pas fusionner de données avec le formulaire, vous devez transmettre un objet `BLOB` basé sur une source de données XML vide. Vous ne pouvez pas transmettre un objet `BLOB` nul ; dans le cas contraire, une exception est générée.
   * Un objet `PDFFormRenderSpec` permettant de stocker les options d’exécution.
   * Un objet `ReaderExtensionSpec` stockant les options d’exécution des droits d’utilisation.
   * Un objet `URLSpec` contenant des valeurs URI requises par le service Forms.

   La méthode `renderPDFFormWithUsageRights` renvoie un objet `FormsResult` contenant un flux de données de formulaire qui doit être écrit dans le navigateur web client.

1. Écrire le flux de données de formulaire dans le navigateur web client

   * Créez un objet `BLOB` contenant des données de formulaire en appelant la méthode `getOutputContent` de l’objet `FormsResult`.
   * Obtenez le type de contenu de l’objet `BLOB` en appelant sa méthode `getContentType`.
   * Définissez le type de contenu de l’objet `javax.servlet.http.HttpServletResponse` en appelant sa méthode `setContentType` et en transmettant le type de contenu de l’objet `BLOB`.
   * Créez un objet `javax.servlet.ServletOutputStream` utilisé pour écrire le flux de données de formulaire dans le navigateur web client en appelant la méthode `getOutputStream` de l’objet `javax.servlet.http.HttpServletResponse`.
   * Créez un tableau d’octets et renseignez-le en appelant la méthode `getBinaryData` de l’objet `BLOB`. Cette tâche affecte le contenu de l’objet `FormsResult` au tableau d’octets.
   * Appelez la méthode `write` de l’objet `javax.servlet.http.HttpServletResponse` pour envoyer le flux de données du formulaire vers le navigateur web du client. Transmettez le tableau d’octets à la méthode `write`.

**Voir également**

[Générer des formulaires définis avec des droits](#rendering-rights-enabled-forms)

[Appeler AEM Forms en utilisant le codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
