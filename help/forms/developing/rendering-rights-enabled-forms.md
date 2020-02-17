---
title: Rendu de formulaires prenant en charge les droits
seo-title: Rendu de formulaires prenant en charge les droits
description: 'null'
seo-description: 'null'
uuid: ce5e4be6-d9b0-4989-a0e1-a8c3b98aed77
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: d4c2b2f0-613a-409d-b39b-8e37fdb96eea
translation-type: tm+mt
source-git-commit: 7cbe3e94eddb81925072f68388649befbb027e6d

---


# Rendu de formulaires prenant en charge les droits {#rendering-rights-enabled-forms}

Le service Forms peut générer des formulaires auxquels des droits d’utilisation sont appliqués. Les droits d’utilisation appartiennent à la fonctionnalité disponible par défaut dans Acrobat mais non dans Adobe Reader, telle que la capacité à ajouter des commentaires à un formulaire ou à remplir des champs de formulaire et enregistrer ce dernier. Les formulaires auxquels des droits d’utilisation sont appliqués sont appelés des formulaires dotés de droits d’utilisation. Un utilisateur qui ouvre un formulaire avec droits d’accès dans Adobe Reader peut effectuer des opérations activées pour ce formulaire.

Pour appliquer des droits d’utilisation à un formulaire, le service des extensions d’Acrobat Reader DC doit faire partie de votre installation AEM forms. En outre, vous devez disposer d’informations d’identification valides vous permettant d’appliquer des droits d’utilisation à des documents PDF. En d’autres termes, vous devez configurer correctement le service des extensions d’Acrobat Reader DC avant de pouvoir générer un formulaire avec droits d’accès. (Voir [A propos du service](/help/forms/developing/assigning-usage-rights.md#about-the-acrobat-reader-dc-extensions-service)des extensions d’Acrobat Reader DC.)

>[!NOTE]
>
>Pour générer un formulaire contenant des droits d’utilisation, vous devez utiliser un fichier XDP comme entrée et non un fichier PDF. Si vous utilisez un fichier PDF comme entrée, le formulaire est toujours généré ; toutefois, il ne s&#39; agira pas d&#39; un formulaire dont les droits sont activés.

>[!NOTE]
>
>Vous ne pouvez pas préremplir un formulaire avec des données XML lorsque vous spécifiez les droits d’utilisation suivants : `enableComments`, `enableCommentsOnline`, `enableEmbeddedFiles`ou `enableDigitalSignatures`. (Voir [Préremplissage de formulaires avec des mises en page](/help/forms/developing/prepopulating-forms-flowable-layouts.md)à disposition souple.)

>[!NOTE]
>
>For more information about the Forms service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Résumé des étapes {#summary-of-steps}

Pour effectuer le rendu d’un formulaire dont les droits sont activés, effectuez les tâches suivantes :

1. Incluez des fichiers de projet.
1. Créez un objet API Client Forms.
1. Définissez les options d’exécution des droits d’utilisation.
1. Générer un formulaire dont les droits sont activés.
1. Ecrivez le formulaire dont les droits sont activés dans le navigateur Web client.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

**Création d’un objet API du client Forms**

Avant de pouvoir exécuter par programmation une opération d’API Client de service Forms, vous devez créer un client de service Forms.

**Définition des droits d’utilisation des options d’exécution**

Vous devez définir les droits d’utilisation des options d’exécution pour rendre un formulaire avec droits activés. Vous devez également spécifier l’alias des informations d’identification utilisées pour appliquer des droits d’utilisation à un formulaire. Après avoir spécifié la valeur d’alias, vous spécifiez chaque droit d’utilisation à appliquer au formulaire.

**Rendu d’un formulaire dont les droits sont activés**

Pour rendre un formulaire avec droits d’utilisation, vous utilisez la même logique d’application que le rendu d’un formulaire sans droits d’utilisation. La seule différence est que vous devez vous assurer que les options d’exécution des droits d’utilisation sont incluses dans la logique de votre application.

>[!NOTE]
>
>Lors du rendu d’un formulaire avec droits d’utilisation à l’aide de l’API du service Web de Forms, vous ne pouvez pas joindre de fichiers au formulaire.

**Ecrire le flux de données du formulaire dans le navigateur Web client**

Lorsque le service Forms génère un formulaire avec droits d’accès, il renvoie un flux de données de formulaire que vous devez écrire dans le navigateur Web client. Une fois le formulaire écrit dans le navigateur Web client, il est visible par l’utilisateur. Un utilisateur qui consulte le formulaire avec droits d’accès dans Adobe Reader est en mesure d’effectuer les opérations activées pour ce formulaire.

**Voir également**

[Rendu de formulaires avec droits d’utilisation à l’aide de l’API Java](#render-rights-enabled-forms-using-the-java-api)

[Rendu de formulaires avec droits d’utilisation à l’aide de l’API de service Web](#render-rights-enabled-forms-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Démarrage rapide de l’API du service Forms](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Rendu de formulaires PDF interactifs](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Création d&#39;applications Web qui renvoient des formulaires](/help/forms/developing/creating-web-applications-renders-forms.md)

### Rendu de formulaires avec droits d’utilisation à l’aide de l’API Java {#render-rights-enabled-forms-using-the-java-api}

Générer un formulaire avec droits activés à l’aide de l’API Forms (Java) :

1. Inclure les fichiers de projet

   Incluez des fichiers JAR client, tels que adobe-forms-client.jar, dans le chemin de classe de votre projet Java.

1. Création d’un objet API du client Forms

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Create an `FormsServiceClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. Définition des droits d’utilisation des options d’exécution

   * Créez un objet `ReaderExtensionSpec` en utilisant son constructeur.
   * Spécifiez l’alias des informations d’identification en appelant la `ReaderExtensionSpec` `setReCredentialAlias` méthode de l’objet et spécifiez une valeur de chaîne qui représente la valeur d’alias.
   * Définissez les droits d’utilisation en appelant la méthode correspondante qui appartient à l’ `ReaderExtensionSpec` objet. Cependant, vous ne pouvez définir un droit d’utilisation que si les informations d’identification que vous référencez vous le permettent. Autrement dit, vous ne pouvez pas définir un droit d’utilisation si les informations d’identification ne vous permettent pas de le définir. Par exemple. pour définir le droit d’utilisation permettant à un utilisateur de remplir des champs de formulaire et d’enregistrer le formulaire, appelez la `ReaderExtensionSpec` méthode de l’objet et transmettez `setReFillIn` `true`.
   >[!NOTE]
   >
   >Il n’est pas nécessaire d’appeler la `ReaderExtensionSpec` `setReCredentialPassword` méthode de l’objet. Cette méthode n’est pas utilisée par le service Forms.

1. Rendu d’un formulaire dont les droits sont activés

   Appelez la méthode `FormsServiceClient` `renderPDFFormWithUsageRights` de l’objet et transmettez les valeurs suivantes :

   * Valeur de chaîne qui spécifie le nom de la conception de formulaire, y compris l’extension du nom de fichier. Si vous référencez une conception de formulaire faisant partie d’une application Forms, veillez à spécifier le chemin d’accès complet, tel que `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Objet `com.adobe.idp.Document` contenant des données à fusionner avec le formulaire. Si vous ne souhaitez pas fusionner les données, transmettez un `com.adobe.idp.Document` objet vide.
   * Objet `PDFFormRenderSpec` qui stocke les options d’exécution.
   * Objet `ReaderExtensionSpec` qui stocke les options d’exécution des droits d’utilisation.
   * Objet `URLSpec` contenant des valeurs URI requises par le service Forms.
   La `renderPDFFormWithUsageRights` méthode renvoie un `FormsResult` objet qui contient un flux de données de formulaire qui doit être écrit dans le navigateur Web client.

1. Ecrire le flux de données du formulaire dans le navigateur Web client

   * Créez un `com.adobe.idp.Document` objet en appelant la `FormsResult` méthode de l’ `getOutputContent` objet.
   * Obtenez le type de contenu de l’ `com.adobe.idp.Document` objet en appelant sa `getContentType` méthode.
   * Définissez le type de contenu de l’ `javax.servlet.http.HttpServletResponse` objet en appelant sa `setContentType` méthode et en transmettant le type de contenu de l’ `com.adobe.idp.Document` objet.
   * Créez un `javax.servlet.ServletOutputStream` objet utilisé pour écrire le flux de données du formulaire dans le navigateur Web client en appelant la `javax.servlet.http.HttpServletResponse` `getOutputStream` méthode de l’objet.
   * Créez un `java.io.InputStream` objet en appelant la `com.adobe.idp.Document` méthode de l’ `getInputStream` objet.
   * Créez un tableau d’octets pour le remplir avec le flux de données du formulaire en appelant la `InputStream` `read` méthode de l’objet et en transmettant le tableau d’octets comme argument.
   * Appelez la `javax.servlet.ServletOutputStream` `write` méthode de l’objet pour envoyer le flux de données du formulaire au navigateur Web client. Transmettez le tableau d’octets à la `write` méthode.

**Voir également**

[Démarrage rapide (mode SOAP) : Rendu d’un formulaire dont les droits sont activés à l’aide de l’API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-a-rights-enabled-form-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Rendu de formulaires avec droits d’utilisation à l’aide de l’API de service Web {#render-rights-enabled-forms-using-the-web-service-api}

Générer un formulaire avec droits activés à l’aide de l’API Forms (service Web) :

1. Inclure les fichiers de projet

   * Créez des classes de proxy Java qui utilisent le WSDL du service Forms.
   * Incluez les classes proxy Java dans le chemin de votre classe.

1. Création d’un objet API du client Forms

   Créez un `FormsService` objet et définissez des valeurs d’authentification.

1. Définition des droits d’utilisation des options d’exécution

   * Créez un objet `ReaderExtensionSpec` en utilisant son constructeur.
   * Spécifiez l’alias des informations d’identification en appelant la `ReaderExtensionSpec` `setReCredentialAlias` méthode de l’objet et spécifiez une valeur de chaîne qui représente la valeur d’alias.
   * Définissez les droits d’utilisation en appelant la méthode correspondante qui appartient à l’ `ReaderExtensionSpec` objet. Cependant, vous ne pouvez définir un droit d’utilisation que si les informations d’identification que vous référencez vous le permettent. Autrement dit, vous ne pouvez pas définir un droit d’utilisation si les informations d’identification ne vous permettent pas de le définir. Pour définir le droit d’utilisation permettant à un utilisateur de remplir des champs de formulaire et d’enregistrer le formulaire, appelez la `ReaderExtensionSpec` méthode de l’objet et transmettez `setReFillIn` `true`.

1. Rendu d’un formulaire dont les droits sont activés

   Appelez la méthode `FormsService` `renderPDFFormWithUsageRights` de l’objet et transmettez les valeurs suivantes :

   * Valeur de chaîne qui spécifie le nom de la conception de formulaire, y compris l’extension du nom de fichier. Si vous référencez une conception de formulaire faisant partie d’une application Forms, veillez à spécifier le chemin d’accès complet, tel que `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Objet `BLOB` contenant des données à fusionner avec le formulaire. Si vous ne souhaitez pas fusionner les données avec le formulaire, vous devez transmettre un `BLOB` objet basé sur une source de données XML vide. Vous ne pouvez pas transmettre un `BLOB` objet nul ; dans le cas contraire, une exception est levée.
   * Objet `PDFFormRenderSpec` qui stocke les options d’exécution.
   * Objet `ReaderExtensionSpec` qui stocke les options d’exécution des droits d’utilisation.
   * Objet `URLSpec` contenant des valeurs URI requises par le service Forms.
   La `renderPDFFormWithUsageRights` méthode renvoie un `FormsResult` objet qui contient un flux de données de formulaire qui doit être écrit dans le navigateur Web client.

1. Ecrire le flux de données du formulaire dans le navigateur Web client

   * Créez un `BLOB` objet contenant des données de formulaire en appelant la `FormsResult` méthode de l’ `getOutputContent` objet.
   * Obtenez le type de contenu de l’ `BLOB` objet en appelant sa `getContentType` méthode.
   * Définissez le type de contenu de l’ `javax.servlet.http.HttpServletResponse` objet en appelant sa `setContentType` méthode et en transmettant le type de contenu de l’ `BLOB` objet.
   * Créez un `javax.servlet.ServletOutputStream` objet utilisé pour écrire le flux de données du formulaire dans le navigateur Web client en appelant la `javax.servlet.http.HttpServletResponse` `getOutputStream` méthode de l’objet.
   * Créez un tableau d’octets et renseignez-le en appelant la méthode `BLOB` `getBinaryData` de l’objet. Cette tâche affecte le contenu de l’ `FormsResult` objet au tableau d’octets.
   * Appelez la `javax.servlet.http.HttpServletResponse` `write` méthode de l’objet pour envoyer le flux de données du formulaire au navigateur Web client. Transmettez le tableau d’octets à la `write` méthode.

**Voir également**

[Rendu de formulaires prenant en charge les droits](#rendering-rights-enabled-forms)

[Appel d’AEM Forms à l’aide du codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
