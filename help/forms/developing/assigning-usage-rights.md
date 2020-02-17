---
title: Attribution des droits d’utilisation
seo-title: Attribution des droits d’utilisation
description: 'null'
seo-description: 'null'
uuid: 8c2020df-ea3c-49fa-916f-38a458f40d2b
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 9e8db506-9ace-4e1f-8a7b-c4e9b15dde7e
translation-type: tm+mt
source-git-commit: 413af4ef9bc3652e05da78d622183bcf20a8bee7

---


# Attribution des droits d’utilisation {#assigning-usage-rights}

## À propos du service Acrobat Reader DC Extensions {#about-the-acrobat-reader-dc-extensions-service}

Le service Acrobat Reader DC Extensions permet à votre entreprise de partager facilement des documents PDF interactifs en étendant les fonctionnalités d’Adobe Reader. Le service des extensions d’Acrobat Reader DC prend entièrement en charge tout document PDF, y compris PDF 1.7. Il fonctionne avec Adobe Reader 7.0 et versions ultérieures. Le service ajoute des droits d’utilisation à un document PDF, en activant des fonctionnalités qui ne sont généralement pas disponibles à l’ouverture d’un document PDF à l’aide d’Adobe Reader. Les utilisateurs tiers n’ont pas besoin de logiciels ou de modules externes supplémentaires pour travailler avec les documents dont les droits sont activés.

Vous pouvez effectuer les tâches suivantes à l’aide du service des extensions d’Acrobat Reader DC :

* Appliquer des droits d’utilisation aux documents PDF. Pour plus d’informations, voir [Application des droits d’utilisation aux documents](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)PDF.
* Supprimez les droits d’utilisation des documents PDF. Pour plus d’informations, voir [Suppression des droits d’utilisation des documents](assigning-usage-rights.md#removing-usage-rights-from-pdf-documents)PDF.
* Récupérez les informations d’identification. Pour plus d’informations, voir [Récupération des informations d’identification](assigning-usage-rights.md#retrieving-credential-information).

>[!NOTE]
>
>For more information about the Acrobat Reader DC extensions service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Applying Usage Rights to PDF Documents {#applying-usage-rights-to-pdf-documents}

Vous pouvez appliquer des droits d’utilisation aux documents PDF à l’aide de l’API et du service Web du client Java d’Acrobat Reader DC Extensions. Les droits d’utilisation appartiennent à la fonctionnalité disponible par défaut dans Acrobat mais non dans Adobe Reader, telle que la capacité à ajouter des commentaires à un formulaire ou à remplir des champs de formulaire et enregistrer ce dernier. Les documents PDF dotés de droits d’utilisation sont appelés des documents dont les droits sont activés. Un utilisateur qui ouvre un document dont les droits sont activés dans Adobe Reader peut effectuer les opérations autorisées pour ce document spécifique.

>[!NOTE]
>
>Lors de l’application de droits d’utilisation aux documents PDF à l’aide de la `applyUsageRights` méthode, qui fait partie de l’API Java, vous pouvez définir le `isModeFinal` paramètre de l’ `ReaderExtensionsOptionSpec` objet sur `false`. Le compteur de formulaires traités n’est donc pas mis à jour et les performances augmentent. Si la mise à jour du compteur de formulaires traité ne vous préoccupe pas, il est recommandé de définir le `isModeFinal` paramètre sur `false`.

>[!NOTE]
>
>For more information about the Acrobat Reader DC extensions service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary-of-steps}

Pour appliquer des droits d’utilisation à un document PDF, procédez comme suit :

1. Incluez des fichiers de projet.
1. Créez un objet Client des extensions d’Acrobat Reader DC.
1. Récupérez un document PDF.
1. Spécifiez les droits d’utilisation à appliquer.
1. Appliquez des droits d’utilisation au document PDF.
1. Enregistrez le document PDF dont les droits sont activés.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

**Création d’un objet client d’extensions d’Acrobat Reader DC**

Pour exécuter par programmation une opération de service d’extension Acrobat Reader DC, vous devez créer un objet client de service Acrobat Reader DC Extensions. Si vous utilisez l’API Java des extensions d’Acrobat Reader DC, créez un `ReaderExtensionsServiceClient` objet. Si vous utilisez l’API du service Web des extensions d’Acrobat Reader DC, créez un `ReaderExtensionsServiceService` objet.

**Récupération d’un document PDF**

Vous devez récupérer un document PDF pour appliquer des droits d’utilisation. Les documents PDF dont les droits sont activés contiennent un dictionnaire de droits d’utilisation. Lorsqu’Adobe Reader ouvre un document contenant un tel dictionnaire, il active les droits d’utilisation spécifiés dans le dictionnaire pour ce document uniquement. Si le document ne contient pas de dictionnaire des droits d’utilisation, le service des extensions d’Acrobat Reader DC en crée un. S’il contient déjà un dictionnaire, le service des extensions d’Acrobat Reader DC remplace les droits d’utilisation existants par ceux que vous spécifiez. Le dictionnaire spécifie les droits d’utilisation activés. Lorsqu’un utilisateur ouvre le document dans Adobe Reader, seuls les droits d’utilisation spécifiés dans le dictionnaire sont autorisés.

**Spécifier les droits d’utilisation à appliquer**

Les droits d’utilisation que vous pouvez définir sont déterminés par les informations d’identification que vous achetez auprès d’Adobe Systems Incorporated. Les informations d’identification permettent généralement de définir un groupe de droits d’utilisation connexes, tels que ceux relatifs aux formulaires interactifs. Chaque information d’identification permet de créer un certain nombre de documents PDF dont les droits sont activés. Les informations d’identification d’évaluation permettent de créer un nombre illimité de brouillons de documents.

>[!NOTE]
>
>Si vous tentez d’attribuer un droit d’utilisation non autorisé par vos informations d’identification, vous provoquerez une exception.

**Appliquer des droits d’utilisation au document PDF**

Pour appliquer des droits d’utilisation à un document PDF, vous référencez l’alias des informations d’identification que vous utilisez pour appliquer des droits d’utilisation (les informations d’identification sont généralement installées lors de l’installation d’AEM Forms). Vous devez également spécifier le document PDF auquel les droits d’utilisation sont appliqués. Pour plus d’informations sur la configuration d’informations d’identification, voir le guide d’installation et de déploiement de votre serveur d’applications.

**Enregistrer le document PDF dont les droits sont activés**

Une fois que le service des extensions d’Acrobat Reader DC a appliqué des droits d’utilisation à un document PDF, vous pouvez enregistrer ce document au format PDF.

**Voir également**

[Application de droits d’utilisation à l’aide de l’API Java](assigning-usage-rights.md#apply-usage-rights-using-the-java-api)

[Appliquer des droits d’utilisation à l’aide de l’API de service Web](assigning-usage-rights.md#apply-usage-rights-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Démarrage rapide de l’API du service Acrobat Reader DC Extensions](/help/forms/developing/acrobat-reader-dc-extensions-service.md#acrobat-reader-dc-extensions-service-java-api-quick-start-soap)

### Application de droits d’utilisation à l’aide de l’API Java {#apply-usage-rights-using-the-java-api}

Appliquez des droits d’utilisation à un document PDF à l’aide de l’API Acrobat Reader DC Extensions (Java) :

1. Inclure les fichiers de projet

   Incluez des fichiers JAR client, tels que adobe-reader-extensions-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un objet Client des extensions d’Acrobat Reader DC.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `ReaderExtensionsServiceClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`. 

1. Récupérez un document PDF.

   * Créez un `java.io.FileInputStream` objet représentant le document PDF à l’aide de son constructeur et transmettez une valeur de chaîne indiquant l’emplacement du document PDF.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Spécifiez les droits d’utilisation à appliquer.

   * Créez un `UsageRights` objet représentant les droits d’utilisation à l’aide de son constructeur.
   * Pour chaque droit d’utilisation à appliquer, appelez une méthode correspondante qui appartient à l’ `UsageRights` objet. Par exemple, pour ajouter le droit d’ `enableFormFillIn` utilisation, appelez la `UsageRights` méthode de l’objet et transmettez `enableFormFillIn` `true`. (Répétez cette étape pour chaque droit d’utilisation à appliquer).

1. Appliquez des droits d’utilisation au document PDF.

   * Créez un objet `ReaderExtensionsOptionSpec` en utilisant son constructeur. Cet objet contient des options d’exécution requises par le service des extensions d’Acrobat Reader DC. Lors de l’appel de ce constructeur, vous devez spécifier les valeurs suivantes :

      * Objet `UsageRights` contenant les droits d’utilisation à appliquer au document.
      * Valeur de chaîne qui spécifie un message que l’utilisateur voit lorsqu’un document PDF dont les droits sont activés est ouvert dans Adobe Reader 7.x. Ce message ne s’affiche pas dans Adobe Reader 8.0.
   * Appliquez des droits d’utilisation au document PDF en appelant la `ReaderExtensionsServiceClient` `applyUsageRights` méthode de l’objet et en transmettant les valeurs suivantes :

      * Objet `com.adobe.idp.Document` contenant le document PDF auquel les droits d’utilisation sont appliqués.
      * Valeur de chaîne qui spécifie l’alias des informations d’identification qui vous permet d’appliquer des droits d’utilisation.
      * Valeur string qui spécifie la valeur du mot de passe correspondant. (Ce paramètre est actuellement ignoré. Vous pouvez passer `null`.)
   * Objet `ReaderExtensionsOptionSpec` contenant des options d’exécution.
   La `applyUsageRights` méthode renvoie un `com.adobe.idp.Document` objet contenant le document PDF dont les droits sont activés.

1. Enregistrez le document PDF dont les droits sont activés.

   * Créez un objet `java.io.File` et assurez-vous que l’extension du fichier est .pdf.
   * Appelez la `com.adobe.idp.Document` méthode de l’ `copyToFile` objet pour copier le contenu de l’ `com.adobe.idp.Document` objet dans le fichier (veillez à utiliser l’ `com.adobe.idp.Document` objet renvoyé par la `applyUsageRights` méthode).

**Voir également**

[Application des droits d’utilisation aux documents PDF](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

[Démarrage rapide (mode SOAP):Application des droits d’utilisation à l’aide de l’API Java](/help/forms/developing/acrobat-reader-dc-extensions-service.md#quick-start-soap-mode-applying-usage-rights-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Appliquer des droits d’utilisation à l’aide de l’API de service Web {#apply-usage-rights-using-the-web-service-api}

Appliquez des droits d’utilisation à un document PDF à l’aide de l’API Acrobat Reader DC Extensions (service Web) :

1. Incluez des fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Veillez à utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/ReaderExtensionsService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un objet Client des extensions d’Acrobat Reader DC.

   * Create a `ReaderExtensionsServiceClient` object by using its default constructor.
   * Create a `ReaderExtensionsServiceClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/ReaderExtensionsService?blob=mtom`. Veillez à spécifier `?blob=mtom`.)
   * Créez un `System.ServiceModel.BasicHttpBinding` objet en obtenant la valeur du `ReaderExtensionsServiceClient.Endpoint.Binding` champ. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le `System.ServiceModel.BasicHttpBinding` champ de l’ `MessageEncoding` objet sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant les tâches suivantes :

      * Attribuez le nom d’utilisateur d’AEM forms au champ `ReaderExtensionsServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `ReaderExtensionsServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Récupérez un document PDF.

   * Créez un objet `BLOB` en utilisant son constructeur. L’ `BLOB` objet est utilisé pour stocker un document PDF auquel des droits d’utilisation sont appliqués.
   * Créez un `System.IO.FileStream` objet en appelant son constructeur et en transmettant une valeur de chaîne représentant l’emplacement du fichier PDF et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’ `System.IO.FileStream` objet. Vous pouvez déterminer la taille du tableau d’octets en obtenant la `System.IO.FileStream` `Length` propriété de l’objet.
   * Renseignez le tableau d’octets avec les données de flux en appelant la `System.IO.FileStream` `Read` méthode de l’objet. Passez le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’ `BLOB` objet en affectant sa `MTOM` propriété au contenu du tableau d’octets.

1. Spécifiez les droits d’utilisation à appliquer.

   * Créez un `UsageRights` objet représentant les droits d’utilisation à l’aide de son constructeur.
   * Pour chaque droit d’utilisation à appliquer, affectez la valeur `true` au membre de données correspondant qui appartient à l’ `UsageRights` objet. Par exemple, pour ajouter le droit `enableFormFillIn` d’utilisation, affectez `true` au membre `UsageRights` `enableFormFillIn` de données de l’objet. (Répétez cette étape pour chaque droit d’utilisation à appliquer).

1. Appliquez des droits d’utilisation au document PDF.

   * Créez un objet `ReaderExtensionsOptionSpec` en utilisant son constructeur. Cet objet contient des options d’exécution requises par le service des extensions d’Acrobat Reader DC.
   * Affectez l’ `UsageRights` objet au membre `ReaderExtensionsOptionSpec` de données de l’ `usageRights` objet.
   * Attribuez une valeur de chaîne qui spécifie le message qu’un utilisateur voit lorsqu’un document PDF dont les droits sont activés est ouvert dans Adobe Reader au membre `ReaderExtensionsOptionSpec` `message` de données de l’objet.
   * Appliquez des droits d’utilisation au document PDF en appelant la `ReaderExtensionsServiceClient` `applyUsageRights` méthode de l’objet et en transmettant les valeurs suivantes :

      * Objet `BLOB` contenant le document PDF auquel les droits d’utilisation sont appliqués.
      * Valeur de chaîne qui spécifie l’alias des informations d’identification qui vous permet d’appliquer des droits d’utilisation.
      * Valeur string qui spécifie la valeur du mot de passe correspondant. (Ce paramètre est actuellement ignoré. Vous pouvez passer `null`.)
   * Objet `ReaderExtensionsOptionSpec` contenant des options d’exécution.
   La `applyUsageRights` méthode renvoie un `BLOB` objet contenant le document PDF dont les droits sont activés.

1. Enregistrez le document PDF dont les droits sont activés.

   * Create a `System.IO.FileStream` object by invoking its constructor. Transmettez une valeur de chaîne représentant l’emplacement du fichier du document PDF dont les droits sont activés.
   * Créez un tableau d’octets qui stocke le contenu des données de l’ `BLOB` objet renvoyé par la `applyUsageRights` méthode. Renseignez le tableau d’octets en obtenant la valeur du membre `BLOB` `MTOM` de données de l’objet.
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * Ecrivez le contenu du tableau d’octets dans un fichier PDF en appelant la `System.IO.BinaryWriter` `Write` méthode de l’objet et en transmettant le tableau d’octets.

**Voir également**

[Application des droits d’utilisation aux documents PDF](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

[Appel d’AEM Forms à l’aide de MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Appel d’AEM Forms à l’aide de SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Suppression des droits d’utilisation des documents PDF {#removing-usage-rights-from-pdf-documents}

Vous pouvez supprimer des droits d’utilisation d’un document dont les droits sont activés. La suppression des droits d’utilisation d’un document PDF dont les droits sont activés est également nécessaire pour effectuer d’autres opérations AEM Forms sur ce document. Vous devez par exemple signer numériquement (ou certifier) un document PDF avant de définir ses droits d’utilisation. Par conséquent, si vous souhaitez effectuer des opérations sur un document dont les droits sont activés, vous devez supprimer les droits d’utilisation du document PDF, effectuer les autres opérations, telles que la signature numérique du document, puis réappliquer les droits d’utilisation au document.

>[!NOTE]
>
>For more information about the Acrobat Reader DC extensions service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary_of_steps-1}

Pour supprimer des droits d’utilisation d’un document PDF dont les droits sont activés, procédez comme suit :

1. Incluez des fichiers de projet.
1. Créez un objet Client des extensions d’Acrobat Reader DC.
1. Récupérez un document PDF dont les droits sont activés.
1. Supprimez les droits d’utilisation du document PDF.
1. Enregistrez le document PDF.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

**Création d’un objet client d’extensions d’Acrobat Reader DC**

Avant de pouvoir exécuter par programmation une opération du service d’extensions d’Acrobat Reader DC, vous devez créer un objet client du service d’extensions d’Acrobat Reader DC. Si vous utilisez l’API Java, créez un `ReaderExtensionsServiceClient` objet. Si vous utilisez l’API du service Web des extensions d’Acrobat Reader DC, créez un `ReaderExtensionsServiceService` objet.

**Récupération d’un document PDF dont les droits sont activés**

Récupérez un document PDF dont les droits sont activés afin de supprimer les droits d’utilisation.

**Suppression des droits d’utilisation du document PDF**

Après avoir récupéré un document PDF dont les droits sont activés, vous pouvez supprimer des droits d’utilisation. Une fois les droits d’utilisation supprimés, le document PDF ne comporte aucune fonctionnalité supplémentaire lors de son affichage dans Adobe Reader.

**Enregistrer le document PDF**

Vous pouvez enregistrer le document PDF qui ne contient plus les droits d’utilisation en tant que fichier PDF. Une fois enregistré au format PDF, le document PDF peut être affiché dans Adobe Reader ou Acrobat.

**Voir également**

[Suppression des droits d’utilisation à l’aide de l’API Java](assigning-usage-rights.md#remove-usage-rights-using-the-java-api)

[Suppression des droits d’utilisation à l’aide de l’API de service Web](assigning-usage-rights.md#remove-usage-rights-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Démarrage rapide de l’API du service Acrobat Reader DC Extensions](/help/forms/developing/acrobat-reader-dc-extensions-service.md#acrobat-reader-dc-extensions-service-java-api-quick-start-soap)

[Application des droits d’utilisation aux documents PDF](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

### Suppression des droits d’utilisation à l’aide de l’API Java {#remove-usage-rights-using-the-java-api}

Supprimez les droits d’utilisation d’un document PDF dont les droits sont activés à l’aide de l’API des extensions d’Acrobat Reader DC (Java) :

1. Incluez des fichiers de projet.

   Incluez des fichiers JAR client, tels que adobe-reader-extensions-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un objet Client des extensions d’Acrobat Reader DC.

   Créez un `ReaderExtensionsServiceClient` objet en utilisant son constructeur et en transmettant un `ServiceClientFactory` objet contenant des propriétés de connexion.

1. Récupérez un document PDF.

   * Créez un `java.io.FileInputStream` objet représentant le document PDF dont les droits sont activés à l’aide de son constructeur et transmettez une valeur de chaîne indiquant l’emplacement du document PDF.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Supprimez les droits d’utilisation du document PDF.

   Supprimez les droits d’utilisation du document PDF en appelant la `ReaderExtensionsServiceClient` méthode de l’objet et en transmettant l’ `removeUsageRights` `com.adobe.idp.Document` objet contenant le document PDF dont les droits sont activés. Cette méthode renvoie un `com.adobe.idp.Document` objet qui contient un document PDF sans droits d’utilisation.

1. Appliquez des droits d’utilisation au document PDF.

   * Create a `java.io.File` object and ensure that the file extension is .PDF.
   * Appelez la `Document` méthode de l’ `copyToFile` objet pour copier le contenu de l’ `Document` objet dans le fichier (veillez à utiliser l’ `Document` objet renvoyé par la `removeUsageRights` méthode).

**Voir également**

[Suppression des droits d’utilisation des documents PDF](assigning-usage-rights.md#removing-usage-rights-from-pdf-documents)

[Démarrage rapide (mode SOAP) : Suppression des droits d’utilisation d’un document PDF à l’aide de l’API Java](/help/forms/developing/acrobat-reader-dc-extensions-service.md#quick-start-soap-mode-removing-usage-rights-from-a-pdf-document-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Suppression des droits d’utilisation à l’aide de l’API de service Web {#remove-usage-rights-using-the-web-service-api}

Supprimez les droits d’utilisation d’un document PDF dont les droits sont activés à l’aide de l’API des extensions d’Acrobat Reader DC (service Web) :

1. Incluez des fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Veillez à utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/ReaderExtensionsService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un objet Client des extensions d’Acrobat Reader DC.

   * Create a `ReaderExtensionsServiceClient` object by using its default constructor.
   * Create a `ReaderExtensionsServiceClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/ReaderExtensionsService?blob=mtom`. Veillez à spécifier `?blob=mtom`.)
   * Créez un `System.ServiceModel.BasicHttpBinding` objet en obtenant la valeur du `ReaderExtensionsServiceClient.Endpoint.Binding` champ. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le `System.ServiceModel.BasicHttpBinding` champ de l’ `MessageEncoding` objet sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant les tâches suivantes :

      * Attribuez le nom d’utilisateur d’AEM forms au champ `ReaderExtensionsServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `ReaderExtensionsServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Récupérez un document PDF.

   * Créez un objet `BLOB` en utilisant son constructeur. L’ `BLOB` objet est utilisé pour stocker le document PDF dont les droits sont activés et dont les droits d’utilisation sont supprimés.
   * Créez un `System.IO.FileStream` objet en appelant son constructeur et en transmettant une valeur de chaîne représentant l’emplacement du fichier PDF et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’ `System.IO.FileStream` objet. Vous pouvez déterminer la taille du tableau d’octets en obtenant la `System.IO.FileStream` `Length` propriété de l’objet.
   * Renseignez le tableau d’octets avec les données de flux en appelant la `System.IO.FileStream` `Read` méthode de l’objet et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’ `BLOB` objet en affectant sa `MTOM` propriété au contenu du tableau d’octets.

1. Supprimez les droits d’utilisation du document PDF.

   Supprimez les droits d’utilisation du document PDF en appelant la `ReaderExtensionsServiceClient` méthode de l’objet et en transmettant l’ `removeUsageRights` `BLOB` objet contenant le document PDF dont les droits sont activés. Cette méthode renvoie un `BLOB` objet qui contient un document PDF sans droits d’utilisation.

1. Appliquez des droits d’utilisation au document PDF.

   * Créez un `System.IO.FileStream` objet en appelant son constructeur et en transmettant une valeur de chaîne représentant l’emplacement du fichier PDF.
   * Créez un tableau d’octets qui stocke le contenu des données de l’ `BLOB` objet renvoyé par la `removeUsageRights` méthode. Renseignez le tableau d’octets en obtenant la valeur du membre `BLOB` `MTOM` de données de l’objet.
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.

**Voir également**

[Suppression des droits d’utilisation des documents PDF](assigning-usage-rights.md#removing-usage-rights-from-pdf-documents)

[Appel d’AEM Forms à l’aide de MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Appel d’AEM Forms à l’aide de SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Récupération des informations d’identification {#retrieving-credential-information}

Vous pouvez récupérer des informations sur les informations d’identification utilisées pour appliquer des droits d’utilisation à un document PDF dont les droits sont activés. En récupérant les informations d’identification, vous pouvez obtenir des informations telles que la date à laquelle le certificat n’est plus valide.

>[!NOTE]
>
>For more information about the Acrobat Reader DC extensions service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary_of_steps-2}

Pour récupérer des informations sur les informations d’identification utilisées pour appliquer des droits d’utilisation à un document PDF, procédez comme suit :

1. Incluez des fichiers de projet.
1. Créez un objet Client des extensions d’Acrobat Reader DC.
1. Récupérez un document PDF dont les droits sont activés.
1. Récupérez des informations sur les informations d’identification.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

**Création d’un objet client d’extensions d’Acrobat Reader DC**

Avant de pouvoir exécuter par programmation une opération du service d’extensions d’Acrobat Reader DC, vous devez créer un objet client du service d’extensions d’Acrobat Reader DC. Si vous utilisez l’API Java, créez un `ReaderExtensionsServiceClient` objet. Si vous utilisez l’API du service Web des extensions d’Acrobat Reader DC, créez un `ReaderExtensionsServiceService` objet.

**Récupération d’un document PDF dont les droits sont activés**

Vous devez récupérer un document PDF dont les droits sont activés afin de récupérer des informations sur les informations d’identification. Vous pouvez également récupérer des informations sur une information d’identification en spécifiant son alias ; toutefois, si vous souhaitez récupérer des informations sur des informations d’identification utilisées pour appliquer des droits d’utilisation à un document PDF dont les droits sont activés, vous devez récupérer le document.

**Récupérer des informations sur les informations d’identification**

Après avoir récupéré un document PDF dont les droits sont activés, vous pouvez obtenir des informations sur les informations d’identification qui ont été utilisées pour lui appliquer des droits d’utilisation. Vous pouvez obtenir les informations suivantes sur les informations d’identification :

* Message affiché dans Adobe Reader à l’ouverture du document PDF dont les droits sont activés.
* Date à laquelle les informations d’identification ne sont plus valides.
* Date avant laquelle les informations d’identification ne sont pas valides.
* Droits d’utilisation définis pour ce document PDF dont les droits sont activés.
* Nombre d’utilisations des informations d’identification.

**Voir également**

[Suppression des droits d’utilisation à l’aide de l’API Java](assigning-usage-rights.md#remove-usage-rights-using-the-java-api)

[Suppression des droits d’utilisation à l’aide de l’API de service Web](assigning-usage-rights.md#remove-usage-rights-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Démarrage rapide de l’API du service Acrobat Reader DC Extensions](/help/forms/developing/acrobat-reader-dc-extensions-service.md#acrobat-reader-dc-extensions-service-java-api-quick-start-soap)

### Récupération des informations d’identification à l’aide de l’API Java {#retrieve-credential-information-using-the-java-api}

Récupérez les informations d’identification à l’aide de l’API des extensions d’Acrobat Reader DC (Java) :

1. Incluez des fichiers de projet.

   Incluez des fichiers JAR client, tels que adobe-reader-extensions-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un objet Client des extensions d’Acrobat Reader DC.

   Créez un `ReaderExtensionsServiceClient` objet en utilisant son constructeur et en transmettant un `ServiceClientFactory` objet contenant des propriétés de connexion.

1. Récupérez un document PDF.

   * Créez un `java.io.FileInputStream` objet représentant le document PDF dont les droits sont activés à l’aide de son constructeur et transmettez une valeur de chaîne indiquant l’emplacement du document PDF dont les droits sont activés.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Supprimez les droits d’utilisation du document PDF.

   * Récupérez des informations sur les informations d’identification utilisées pour appliquer des droits d’utilisation au document PDF en appelant la `ReaderExtensionsServiceClient` méthode de l’ `getDocumentUsageRights` objet et en transmettant l’ `com.adobe.idp.Document` objet contenant le document PDF dont les droits sont activés. Cette méthode renvoie un `GetUsageRightsResult` objet contenant des informations d’identification.
   * Récupérez la date à laquelle les informations d’identification ne sont plus valides en appelant la `GetUsageRightsResult` `getNotAfter` méthode de l’objet. Cette méthode renvoie un `java.util.Date` objet qui représente la date à laquelle les informations d’identification ne sont plus valides.
   * Récupérez le message affiché dans Adobe Reader lorsque le document PDF dont les droits sont activés est ouvert en appelant la `GetUsageRightsResult` `getMessage` méthode de l’objet. Cette méthode renvoie une valeur de chaîne qui représente le message.

**Voir également**

[Récupération des informations d’identification](assigning-usage-rights.md#retrieving-credential-information)

[Démarrage rapide (mode SOAP) : Récupération des informations d’identification à l’aide de l’API Java](/help/forms/developing/acrobat-reader-dc-extensions-service.md#quick-start-soap-mode-retrieving-credential-information-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Récupération des informations d’identification à l’aide de l’API du service Web {#retrieve-credential-information-using-the-web-service-api}

Récupérez les informations d’identification à l’aide de l’API des extensions d’Acrobat Reader DC (service Web) :

1. Incluez des fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Veillez à utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/ReaderExtensionsService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un objet Client des extensions d’Acrobat Reader DC.

   * Créez un `ReaderExtensionsServiceClient` objet à l’aide de son constructeur par défaut.
   * Create a `ReaderExtensionsServiceClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/ReaderExtensionsService?blob=mtom`. Veillez à spécifier `?blob=mtom`.)
   * Créez un `System.ServiceModel.BasicHttpBinding` objet en obtenant la valeur du `ReaderExtensionsServiceClient.Endpoint.Binding` champ. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le `System.ServiceModel.BasicHttpBinding` champ de l’ `MessageEncoding` objet sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant les tâches suivantes :

      * Attribuez le nom d’utilisateur d’AEM forms au champ `ReaderExtensionsServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `ReaderExtensionsServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Récupérez un document PDF.

   * Créez un objet `BLOB` en utilisant son constructeur. L’ `BLOB` objet est utilisé pour stocker un document PDF dont les droits sont activés.
   * Créez un `System.IO.FileStream` objet en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du fichier du document PDF dont les droits sont activés et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’ `System.IO.FileStream` objet. Vous pouvez déterminer la taille du tableau d’octets en obtenant la `System.IO.FileStream` `Length` propriété de l’objet.
   * Renseignez le tableau d’octets avec les données de flux en appelant la `System.IO.FileStream` `Read` méthode de l’objet et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’ `BLOB` objet en affectant sa `MTOM` propriété au contenu du tableau d’octets.

1. Supprimez les droits d’utilisation du document PDF.

   * Récupérez des informations sur les informations d’identification utilisées pour appliquer des droits d’utilisation au document PDF en appelant la `ReaderExtensionsServiceClient` méthode de l’ `getDocumentUsageRights` objet et en transmettant l’ `com.adobe.idp.Document` objet contenant le document PDF dont les droits sont activés. Cette méthode renvoie un `GetUsageRightsResult` objet contenant des informations d’identification.
   * Récupérez la date à laquelle les informations d’identification ne sont plus valides en obtenant la valeur du membre de `GetUsageRightsResult` `notAfter` données de l’objet. Le type de données de ce membre de données est `System.DateTime`.
   * Récupérez le message qui s’affiche lorsque le document PDF dont les droits sont activés est ouvert dans Adobe Reader en obtenant la valeur du membre `GetUsageRightsResult` `message` de données de l’objet. Le type de données de ce membre de données est une chaîne.
   * Récupérez le nombre d’utilisations des informations d’identification en obtenant la valeur du membre de `GetUsageRightsResult` `useCount` données de l’objet. Le type de données de ce membre de données est un entier.

**Voir également**

[Récupération des informations d’identification](assigning-usage-rights.md#retrieving-credential-information)

[Appel d’AEM Forms à l’aide de MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Appel d’AEM Forms à l’aide de SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
