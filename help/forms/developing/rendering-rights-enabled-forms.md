---
title: Rendu de Forms compatible avec les droits
seo-title: Rendu de Forms compatible avec les droits
description: Utilisez le service Forms pour effectuer le rendu des formulaires auxquels des droits d’utilisation sont appliqués. Vous pouvez générer des formulaires activés pour les droits à l’aide de l’API Java et de l’API de service Web.
seo-description: Utilisez le service Forms pour effectuer le rendu des formulaires auxquels des droits d’utilisation sont appliqués. Vous pouvez générer des formulaires activés pour les droits à l’aide de l’API Java et de l’API de service Web.
uuid: ce5e4be6-d9b0-4989-a0e1-a8c3b98aed77
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: d4c2b2f0-613a-409d-b39b-8e37fdb96eea
role: Developer
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1494'
ht-degree: 5%

---


# Forms compatible avec les droits de rendu {#rendering-rights-enabled-forms}

Le service Forms peut générer des formulaires pour lesquels des droits d’utilisation sont appliqués. Les droits d’utilisation appartiennent à la fonctionnalité disponible par défaut dans Acrobat mais non dans Adobe Reader, telle que la capacité à ajouter des commentaires à un formulaire ou à remplir des champs de formulaire et enregistrer ce dernier. Les Forms pour lesquelles des droits d’utilisation leur sont appliqués sont appelés des formulaires dotés de droits d’utilisation. Un utilisateur qui ouvre un formulaire doté de droits d’accès en Adobe Reader peut effectuer des opérations activées pour ce formulaire.

Pour appliquer des droits d’utilisation à un formulaire, le service des extensions Acrobat Reader DC doit faire partie de l’installation AEM forms. En outre, vous devez disposer d’informations d’identification valides vous permettant d’appliquer des droits d’utilisation aux documents PDF. En d’autres termes, vous devez configurer correctement le service des extensions Acrobat Reader DC avant de pouvoir générer un formulaire avec droits d’accès. (Voir [A propos du service des extensions Acrobat Reader DC](/help/forms/developing/assigning-usage-rights.md#about-the-acrobat-reader-dc-extensions-service).)

>[!NOTE]
>
>Pour générer un formulaire contenant des droits d’utilisation, vous devez utiliser un fichier XDP en entrée et non un fichier PDF. Si vous utilisez un fichier PDF en entrée, le formulaire est toujours rendu ; toutefois, il ne s&#39;agira pas d&#39;un formulaire dont les droits sont activés.

>[!NOTE]
>
>Vous ne pouvez pas préremplir un formulaire avec des données XML lorsque vous spécifiez les droits d’utilisation suivants : `enableComments`, `enableCommentsOnline`, `enableEmbeddedFiles` ou `enableDigitalSignatures`. (Voir [Préremplissage de Forms avec des dispositions souple](/help/forms/developing/prepopulating-forms-flowable-layouts.md).)

>[!NOTE]
>
>Pour plus d’informations sur le service Forms, voir [Guide de référence des services pour AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Résumé des étapes {#summary-of-steps}

Pour effectuer le rendu d’un formulaire dont les droits sont activés, effectuez les tâches suivantes :

1. Incluez des fichiers de projet.
1. Créez un objet API Client Forms.
1. Définissez les options d’exécution des droits d’utilisation.
1. Générer un formulaire avec droits d’utilisation.
1. Ecrivez le formulaire doté de droits d’utilisation dans le navigateur Web client.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

**Création d’un objet API Client Forms**

Avant de pouvoir exécuter par programmation une opération d’API Client de service Forms, vous devez créer un client de service Forms.

**Définition des droits d’utilisation options d’exécution**

Vous devez définir les droits d’utilisation des options d’exécution pour générer un formulaire dont les droits sont activés. Vous devez également spécifier l’alias des informations d’identification utilisées pour appliquer des droits d’utilisation à un formulaire. Après avoir spécifié la valeur d’alias, vous spécifiez chaque droit d’utilisation à appliquer au formulaire.

**Rendu d’un formulaire avec droits d’utilisation**

Pour générer un formulaire avec droits d’utilisation, vous utilisez la même logique d’application que pour effectuer le rendu d’un formulaire sans droits d’utilisation. La seule différence est que vous devez vous assurer que les options d’exécution des droits d’utilisation sont incluses dans votre logique d’application.

>[!NOTE]
>
>Lors du rendu d’un formulaire avec droits d’utilisation à l’aide de l’API du service Web Forms, vous ne pouvez pas joindre de fichiers au formulaire.

**Ecrire le flux de données du formulaire dans le navigateur Web client**

Lorsque le service Forms effectue le rendu d’un formulaire doté de droits d’utilisation, il renvoie un flux de données de formulaire que vous devez écrire dans le navigateur Web client. Une fois écrit dans le navigateur Web client, le formulaire est visible pour l’utilisateur. Un utilisateur qui consulte le formulaire doté des droits d’accès en Adobe Reader peut effectuer les opérations activées pour ce formulaire.

**Voir également**

[Rendu de formulaires activés pour les droits à l’aide de l’API Java](#render-rights-enabled-forms-using-the-java-api)

[Générer des formulaires activés pour les droits à l’aide de l’API du service Web](#render-rights-enabled-forms-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Débuts rapides de l’API du service Forms](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Rendu des PDF forms interactifs](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Création d’Applications web renvoyant Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

### Rendu de formulaires activés pour les droits à l’aide de l’API Java {#render-rights-enabled-forms-using-the-java-api}

Générer un formulaire compatible avec les droits d’utilisation à l’aide de l’API Forms (Java) :

1. Inclure les fichiers de projet

   Incluez des fichiers JAR client, tels que adobe-forms-client.jar, dans le chemin de classe de votre projet Java.

1. Création d’un objet API Client Forms

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `FormsServiceClient` en utilisant son constructeur et en transmettant l&#39;objet `ServiceClientFactory`.

1. Définition des droits d’utilisation options d’exécution

   * Créez un objet `ReaderExtensionSpec` en utilisant son constructeur.
   * Spécifiez l’alias des informations d’identification en appelant la méthode `ReaderExtensionSpec` de l’objet `setReCredentialAlias` et spécifiez une valeur de chaîne qui représente la valeur d’alias.
   * Définissez chaque droit d&#39;utilisation en appelant la méthode correspondante qui appartient à l&#39;objet `ReaderExtensionSpec`. Cependant, vous ne pouvez définir un droit d’utilisation que si les informations d’identification que vous référencez vous permettent de le faire. En d’autres termes, vous ne pouvez pas définir un droit d’utilisation si les informations d’identification ne vous permettent pas de le définir. Par exemple. pour définir le droit d’utilisation permettant à un utilisateur de remplir des champs de formulaire et d’enregistrer le formulaire, appelez la méthode `ReaderExtensionSpec` de l’objet `setReFillIn` et transmettez `true`.

   >[!NOTE]
   >
   >Il n’est pas nécessaire d’appeler la méthode `setReCredentialPassword` de l’objet `ReaderExtensionSpec`. Cette méthode n’est pas utilisée par le service Forms.

1. Rendu d’un formulaire avec droits d’utilisation

   Appelez la méthode `renderPDFFormWithUsageRights` de l’objet `FormsServiceClient` et transmettez les valeurs suivantes :

   * Valeur de chaîne qui spécifie le nom de la conception de formulaire, y compris l’extension du nom de fichier. Si vous référencez une conception de formulaire faisant partie d’une application Forms, veillez à spécifier le chemin d’accès complet, tel que `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Objet `com.adobe.idp.Document` contenant les données à fusionner avec le formulaire. Si vous ne souhaitez pas fusionner de données, transmettez un objet `com.adobe.idp.Document` vide.
   * Objet `PDFFormRenderSpec` qui stocke les options d’exécution.
   * Objet `ReaderExtensionSpec` qui stocke les options d’exécution des droits d’utilisation.
   * Objet `URLSpec` contenant des valeurs URI requises par le service Forms.

   La méthode `renderPDFFormWithUsageRights` renvoie un objet `FormsResult` contenant un flux de données de formulaire qui doit être écrit dans le navigateur Web client.

1. Ecrire le flux de données du formulaire dans le navigateur Web client

   * Créez un objet `com.adobe.idp.Document` en appelant la méthode `FormsResult` de l&#39;objet &quot;s `getOutputContent`.
   * Obtenez le type de contenu de l&#39;objet `com.adobe.idp.Document` en appelant sa méthode `getContentType`.
   * Définissez le type de contenu de l&#39;objet `javax.servlet.http.HttpServletResponse` en appelant sa méthode `setContentType` et en transmettant le type de contenu de l&#39;objet `com.adobe.idp.Document`.
   * Créez un objet `javax.servlet.ServletOutputStream` utilisé pour écrire le flux de données du formulaire dans le navigateur Web client en appelant la méthode `javax.servlet.http.HttpServletResponse` de l’objet `getOutputStream`.
   * Créez un objet `java.io.InputStream` en appelant la méthode `com.adobe.idp.Document` de l&#39;objet `getInputStream`.
   * Créez un tableau d’octets pour le remplir avec le flux de données du formulaire en appelant la méthode `InputStream` de l’objet `read` et en transmettant le tableau d’octets comme argument.
   * Appelez la méthode `javax.servlet.ServletOutputStream` de l’objet `write` pour envoyer le flux de données de formulaire au navigateur Web client. Transférez le tableau d’octets à la méthode `write`.

**Voir également**

[Début rapide (mode SOAP) : Rendu d’un formulaire avec droits d’utilisation à l’aide de l’API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-a-rights-enabled-form-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Générer des formulaires activés pour les droits à l’aide de l’API du service Web {#render-rights-enabled-forms-using-the-web-service-api}

Générer un formulaire avec droits d’utilisation à l’aide de l’API Forms (service Web) :

1. Inclure les fichiers de projet

   * Créez des classes de proxy Java qui utilisent le WSDL du service Forms.
   * Incluez les classes proxy Java dans votre chemin de classe.

1. Création d’un objet API Client Forms

   Créez un objet `FormsService` et définissez des valeurs d’authentification.

1. Définition des droits d’utilisation options d’exécution

   * Créez un objet `ReaderExtensionSpec` en utilisant son constructeur.
   * Spécifiez l’alias des informations d’identification en appelant la méthode `ReaderExtensionSpec` de l’objet `setReCredentialAlias` et spécifiez une valeur de chaîne qui représente la valeur d’alias.
   * Définissez chaque droit d&#39;utilisation en appelant la méthode correspondante qui appartient à l&#39;objet `ReaderExtensionSpec`. Cependant, vous ne pouvez définir un droit d’utilisation que si les informations d’identification que vous référencez vous permettent de le faire. En d’autres termes, vous ne pouvez pas définir un droit d’utilisation si les informations d’identification ne vous permettent pas de le définir. Pour définir le droit d’utilisation permettant à un utilisateur de remplir des champs de formulaire et d’enregistrer le formulaire, appelez la méthode `ReaderExtensionSpec` de l’objet `setReFillIn` et transmettez `true`.

1. Rendu d’un formulaire avec droits d’utilisation

   Appelez la méthode `renderPDFFormWithUsageRights` de l’objet `FormsService` et transmettez les valeurs suivantes :

   * Valeur de chaîne qui spécifie le nom de la conception de formulaire, y compris l’extension du nom de fichier. Si vous référencez une conception de formulaire faisant partie d’une application Forms, veillez à spécifier le chemin d’accès complet, tel que `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Objet `BLOB` contenant les données à fusionner avec le formulaire. Si vous ne souhaitez pas fusionner des données avec le formulaire, vous devez transmettre un objet `BLOB` basé sur une source de données XML vide. Vous ne pouvez pas transmettre un objet `BLOB` nul ; dans le cas contraire, une exception est levée.
   * Objet `PDFFormRenderSpec` qui stocke les options d’exécution.
   * Objet `ReaderExtensionSpec` qui stocke les options d’exécution des droits d’utilisation.
   * Objet `URLSpec` contenant des valeurs URI requises par le service Forms.

   La méthode `renderPDFFormWithUsageRights` renvoie un objet `FormsResult` contenant un flux de données de formulaire qui doit être écrit dans le navigateur Web client.

1. Ecrire le flux de données du formulaire dans le navigateur Web client

   * Créez un objet `BLOB` contenant des données de formulaire en appelant la méthode `FormsResult` de l&#39;objet `getOutputContent`.
   * Obtenez le type de contenu de l&#39;objet `BLOB` en appelant sa méthode `getContentType`.
   * Définissez le type de contenu de l&#39;objet `javax.servlet.http.HttpServletResponse` en appelant sa méthode `setContentType` et en transmettant le type de contenu de l&#39;objet `BLOB`.
   * Créez un objet `javax.servlet.ServletOutputStream` utilisé pour écrire le flux de données du formulaire dans le navigateur Web client en appelant la méthode `javax.servlet.http.HttpServletResponse` de l’objet `getOutputStream`.
   * Créez un tableau d’octets et remplissez-le en appelant la méthode `BLOB` de l’objet `getBinaryData`. Cette tâche affecte le contenu de l&#39;objet `FormsResult` au tableau d&#39;octets.
   * Appelez la méthode `javax.servlet.http.HttpServletResponse` de l’objet `write` pour envoyer le flux de données de formulaire au navigateur Web client. Transférez le tableau d’octets à la méthode `write`.

**Voir également**

[Rendu de Forms compatible avec les droits](#rendering-rights-enabled-forms)

[Appel de AEM Forms à l’aide du codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
