---
title: Attribution des droits d’utilisation
seo-title: Attribution des droits d’utilisation
description: Utilisez l’API du client Java des extensions Acrobat Reader DC et l’API du service Web pour appliquer et supprimer des droits d’utilisation des documents PDF.
seo-description: Utilisez l’API du client Java des extensions Acrobat Reader DC et l’API du service Web pour appliquer et supprimer des droits d’utilisation des documents PDF.
uuid: 8c2020df-ea3c-49fa-916f-38a458f40d2b
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 9e8db506-9ace-4e1f-8a7b-c4e9b15dde7e
role: Developer
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '3952'
ht-degree: 7%

---


# Attribution des droits d&#39;utilisation {#assigning-usage-rights}

**Les exemples et exemples de ce document ne concernent que l’environnement AEM Forms on JEE.**

## À propos du service des extensions Acrobat Reader DC {#about-the-acrobat-reader-dc-extensions-service}

Le service Acrobat Reader DC Extensions permet à votre entreprise de partager facilement des documents PDF interactifs en étendant les fonctionnalités de Adobe Reader. Le service Acrobat Reader DC Extensions prend entièrement en charge tout document PDF, jusqu’à PDF 1.7 inclus. Il fonctionne avec Adobe Reader 7.0 et versions ultérieures. Le service ajoute des droits d’utilisation à un document PDF, en activant des fonctions qui ne sont généralement pas disponibles à l’ouverture d’un document PDF à l’aide de Adobe Reader. Les utilisateurs tiers n’ont pas besoin de logiciels ou de modules complémentaires supplémentaires pour travailler avec les documents dotés de droits d’utilisation.

Vous pouvez effectuer ces tâches à l’aide du service Acrobat Reader DC Extensions :

* Appliquer des droits d’utilisation aux documents PDF. Pour plus d’informations, voir [Application des droits d’utilisation aux Documents PDF](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents).
* Supprimez les droits d’utilisation des documents PDF. Pour plus d’informations, voir [Suppression des droits d’utilisation des Documents PDF](assigning-usage-rights.md#removing-usage-rights-from-pdf-documents).
* Récupérez les informations d’identification. Pour plus d’informations, voir [Récupération des informations d’identification](assigning-usage-rights.md#retrieving-credential-information).

>[!NOTE]
>
>Pour plus d’informations sur le service des extensions Acrobat Reader DC, voir [Guide de référence des services pour AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Application des droits d’utilisation aux Documents PDF {#applying-usage-rights-to-pdf-documents}

Vous pouvez appliquer des droits d’utilisation aux documents PDF à l’aide de l’API client Java Extensions Acrobat Reader DC et du service Web. Les droits d’utilisation appartiennent à la fonctionnalité disponible par défaut dans Acrobat mais non dans Adobe Reader, telle que la capacité à ajouter des commentaires à un formulaire ou à remplir des champs de formulaire et enregistrer ce dernier. Les documents PDF dotés de droits d’utilisation sont appelés des documents dont les droits sont activés. Un utilisateur qui ouvre un document dont les droits sont activés dans Adobe Reader peut effectuer les opérations autorisées pour ce document spécifique.

>[!NOTE]
>
>Lorsque vous appliquez des droits d’utilisation aux documents PDF à l’aide de la méthode `applyUsageRights`, qui fait partie de l’API Java, vous pouvez définir le paramètre `isModeFinal` de l’objet `ReaderExtensionsOptionSpec` sur `false`. Le compteur traité des formulaires n’est donc pas mis à jour et les performances s’en trouvent améliorées. Si la mise à jour du compteur traité de formulaires ne vous préoccupe pas, il est recommandé de définir le paramètre `isModeFinal` sur `false`.

>[!NOTE]
>
>Pour plus d’informations sur le service des extensions Acrobat Reader DC, voir [Guide de référence des services pour AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary-of-steps}

Pour appliquer des droits d’utilisation à un document PDF, procédez comme suit :

1. Incluez des fichiers de projet.
1. Créez un objet Client d’extensions Acrobat Reader DC.
1. Récupérez un document PDF.
1. Spécifiez les droits d’utilisation à appliquer.
1. Appliquez des droits d’utilisation au document PDF.
1. Enregistrez le document PDF dont les droits sont activés.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

**Création d’un objet Client d’extensions Acrobat Reader DC**

Pour exécuter par programmation une opération de service d’extensions Acrobat Reader DC, vous devez créer un objet client de service d’extensions Acrobat Reader DC. Si vous utilisez l’API Java des extensions Acrobat Reader DC, créez un objet `ReaderExtensionsServiceClient`. Si vous utilisez l’API du service Web des extensions Acrobat Reader DC, créez un objet `ReaderExtensionsServiceService`.

**Récupération d’un document PDF**

Vous devez récupérer un document PDF pour appliquer des droits d’utilisation. Les documents PDF dont les droits sont activés contiennent un dictionnaire de droits d’utilisation. Lorsque Adobe Reader ouvre un document contenant un tel dictionnaire, il active les droits d’utilisation spécifiés dans le dictionnaire pour ce document uniquement. Si le document ne contient pas de dictionnaire de droits d’utilisation, le service Acrobat Reader DC Extensions en crée un. S’il contient déjà un dictionnaire, le service des extensions Acrobat Reader DC remplace les droits d’utilisation existants par ceux que vous spécifiez. Le dictionnaire spécifie les droits d’utilisation activés. Lorsqu’un utilisateur ouvre le document dans Adobe Reader, seuls les droits d’utilisation spécifiés dans le dictionnaire sont autorisés.

**Spécifier les droits d’utilisation à appliquer**

Les droits d’utilisation que vous pouvez définir sont déterminés par les informations d’identification que vous achetez à Adobe Systems Incorporated. En règle générale, les informations d’identification permettent de définir un groupe de droits d’utilisation connexes, tels que ceux relatifs aux formulaires interactifs. Chaque information d’identification permet de créer un certain nombre de documents PDF dont les droits sont activés. Les informations d’identification d’évaluation permettent de créer un nombre illimité de documents préliminaires.

>[!NOTE]
>
>Si vous tentez d’attribuer un droit d’utilisation non autorisé par vos informations d’identification, vous provoquerez une exception.

**Appliquer des droits d’utilisation au document PDF**

Pour appliquer des droits d’utilisation à un document PDF, vous référencez l’alias des informations d’identification que vous utilisez pour appliquer des droits d’utilisation (les informations d’identification sont généralement installées lors de l’installation de AEM Forms). Vous devez également spécifier le document PDF auquel les droits d’utilisation sont appliqués. Pour plus d’informations sur la configuration d’informations d’identification, voir le guide d’installation et de déploiement de votre serveur d’applications.

**Enregistrer le document PDF dont les droits sont activés**

Une fois que le service Acrobat Reader DC Extensions applique des droits d’utilisation à un document PDF, vous pouvez enregistrer le document PDF dont les droits sont activés en tant que fichier PDF.

**Voir également**

[Appliquer les droits d’utilisation à l’aide de l’API Java](assigning-usage-rights.md#apply-usage-rights-using-the-java-api)

[Appliquer des droits d’utilisation à l’aide de l’API de service Web](assigning-usage-rights.md#apply-usage-rights-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[débuts rapides de l’API du service Acrobat Reader DC Extensions](/help/forms/developing/acrobat-reader-dc-extensions-service.md#acrobat-reader-dc-extensions-service-java-api-quick-start-soap)

### Appliquer les droits d’utilisation à l’aide de l’API Java {#apply-usage-rights-using-the-java-api}

Appliquez des droits d’utilisation à un document PDF à l’aide de l’API Acrobat Reader DC Extensions (Java) :

1. Inclure les fichiers de projet

   Incluez des fichiers JAR client, tels que adobe-reader-extensions-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un objet Client d’extensions Acrobat Reader DC.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `ReaderExtensionsServiceClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`. 

1. Récupérez un document PDF.

   * Créez un objet `java.io.FileInputStream` qui représente le document PDF en utilisant son constructeur et en transmettant une valeur de chaîne qui spécifie l’emplacement du document PDF.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Spécifiez les droits d’utilisation à appliquer.

   * Créez un objet `UsageRights` qui représente les droits d&#39;utilisation à l&#39;aide de son constructeur.
   * Pour chaque droit d&#39;utilisation à appliquer, appelez une méthode correspondante qui appartient à l&#39;objet `UsageRights`. Par exemple, pour ajouter le droit d’utilisation `enableFormFillIn`, appelez la méthode `UsageRights` de l’objet `enableFormFillIn` et transmettez `true`. (Répétez cette étape pour chaque droit d’utilisation à appliquer).

1. Appliquez des droits d’utilisation au document PDF.

   * Créez un objet `ReaderExtensionsOptionSpec` en utilisant son constructeur. Cet objet contient des options d’exécution requises par le service des extensions Acrobat Reader DC. Lorsque vous appelez ce constructeur, vous devez spécifier les valeurs suivantes :

      * Objet `UsageRights` contenant les droits d&#39;utilisation à appliquer au document.
      * Valeur de chaîne qui spécifie un message que l’utilisateur voit lorsqu’un document PDF doté de droits d’utilisation est ouvert dans Adobe Reader 7.x. Ce message n’est pas affiché dans Adobe Reader 8.0.
   * Appliquez des droits d’utilisation au document PDF en appelant la méthode `ReaderExtensionsServiceClient` de l’objet `applyUsageRights` et en transmettant les valeurs suivantes :

      * Objet `com.adobe.idp.Document` contenant le document PDF auquel les droits d’utilisation sont appliqués.
      * Valeur de chaîne qui spécifie l’alias des informations d’identification qui vous permet d’appliquer des droits d’utilisation.
      * Valeur string qui spécifie la valeur du mot de passe correspondant. (Actuellement, ce paramètre est ignoré. Vous pouvez transmettre `null`.)
   * Objet `ReaderExtensionsOptionSpec` contenant les options d&#39;exécution.

   La méthode `applyUsageRights` renvoie un objet `com.adobe.idp.Document` contenant le document PDF dont les droits sont activés.

1. Enregistrez le document PDF dont les droits sont activés.

   * Créez un objet `java.io.File` et assurez-vous que l’extension du fichier est .pdf.
   * Appelez la méthode `com.adobe.idp.Document` de l&#39;objet `copyToFile` pour copier le contenu de l&#39;objet `com.adobe.idp.Document` dans le fichier (veillez à utiliser l&#39;objet `com.adobe.idp.Document` renvoyé par la méthode `applyUsageRights`).

**Voir également**

[Application des droits d’utilisation aux Documents PDF](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

[Début rapide (mode SOAP) : application de droits d’utilisation à l’aide de l’API Java](/help/forms/developing/acrobat-reader-dc-extensions-service.md#quick-start-soap-mode-applying-usage-rights-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Appliquer des droits d’utilisation à l’aide de l’API de service Web {#apply-usage-rights-using-the-web-service-api}

Appliquez des droits d’utilisation à un document PDF à l’aide de l’API Acrobat Reader DC Extensions (service Web) :

1. Incluez des fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Assurez-vous d’utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/ReaderExtensionsService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un objet Client d’extensions Acrobat Reader DC.

   * Créez un objet `ReaderExtensionsServiceClient` en utilisant son constructeur par défaut.
   * Créez un objet `ReaderExtensionsServiceClient.Endpoint.Address` en utilisant le constructeur `System.ServiceModel.EndpointAddress`. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/ReaderExtensionsService?blob=mtom`. Veillez à spécifier `?blob=mtom`.)
   * Créez un objet `System.ServiceModel.BasicHttpBinding` en obtenant la valeur du champ `ReaderExtensionsServiceClient.Endpoint.Binding`. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le champ `MessageEncoding` de l’objet `System.ServiceModel.BasicHttpBinding` sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en exécutant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `ReaderExtensionsServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `ReaderExtensionsServiceClient.ClientCredentials.UserName.Password`.
      * Affectez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Affectez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Récupérez un document PDF.

   * Créez un objet `BLOB` en utilisant son constructeur. L’objet `BLOB` permet de stocker un document PDF auquel des droits d’utilisation sont appliqués.
   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du fichier du document PDF et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `System.IO.FileStream`. Vous pouvez déterminer la taille du tableau d’octets en obtenant la propriété `System.IO.FileStream` de l’objet `Length`.
   * Renseignez le tableau d’octets avec les données de flux en appelant la méthode `System.IO.FileStream` de l’objet `Read`. Passez le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’objet `BLOB` en attribuant sa propriété `MTOM` au contenu du tableau d’octets.

1. Spécifiez les droits d’utilisation à appliquer.

   * Créez un objet `UsageRights` qui représente les droits d&#39;utilisation à l&#39;aide de son constructeur.
   * Pour chaque droit d&#39;utilisation à appliquer, affectez la valeur `true` au membre de données correspondant qui appartient à l&#39;objet `UsageRights`. Par exemple, pour ajouter le droit d’utilisation `enableFormFillIn`, affectez `true` au membre de données `UsageRights` de l’objet `enableFormFillIn`. (Répétez cette étape pour chaque droit d’utilisation à appliquer).

1. Appliquez des droits d’utilisation au document PDF.

   * Créez un objet `ReaderExtensionsOptionSpec` en utilisant son constructeur. Cet objet contient des options d’exécution requises par le service des extensions Acrobat Reader DC.
   * Affectez l&#39;objet `UsageRights` au membre de données `ReaderExtensionsOptionSpec` de l&#39;objet `usageRights`.
   * Attribuez une valeur de chaîne qui spécifie le message qu’un utilisateur voit lorsqu’un document PDF doté de droits est ouvert dans Adobe Reader au membre de données `message` de l’objet `ReaderExtensionsOptionSpec`.
   * Appliquez des droits d’utilisation au document PDF en appelant la méthode `ReaderExtensionsServiceClient` de l’objet `applyUsageRights` et en transmettant les valeurs suivantes :

      * Objet `BLOB` contenant le document PDF auquel les droits d’utilisation sont appliqués.
      * Valeur de chaîne qui spécifie l’alias des informations d’identification qui vous permet d’appliquer des droits d’utilisation.
      * Valeur string qui spécifie la valeur du mot de passe correspondant. (Actuellement, ce paramètre est ignoré. Vous pouvez transmettre `null`.)
   * Objet `ReaderExtensionsOptionSpec` contenant les options d&#39;exécution.

   La méthode `applyUsageRights` renvoie un objet `BLOB` contenant le document PDF dont les droits sont activés.

1. Enregistrez le document PDF dont les droits sont activés.

   * Créez un objet `System.IO.FileStream` en appelant son constructeur. Transmettez une valeur de chaîne qui représente l’emplacement du fichier du document PDF dont les droits sont activés.
   * Créez un tableau d’octets qui stocke le contenu des données de l’objet `BLOB` renvoyé par la méthode `applyUsageRights`. Renseignez le tableau d’octets en obtenant la valeur du membre de données `MTOM` de l’objet `BLOB`.
   * Créez un objet `System.IO.BinaryWriter` en appelant son constructeur et en transmettant l&#39;objet `System.IO.FileStream`.
   * Ecrivez le contenu du tableau d’octets dans un fichier PDF en appelant la méthode `System.IO.BinaryWriter` de l’objet `Write` et en transmettant le tableau d’octets.

**Voir également**

[Application des droits d’utilisation aux Documents PDF](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

[Appel de AEM Forms à l’aide de MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Appel de AEM Forms à l’aide de SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Suppression des droits d’utilisation des Documents PDF {#removing-usage-rights-from-pdf-documents}

Vous pouvez supprimer des droits d’utilisation d’un document dont les droits sont activés. Il est également nécessaire de supprimer les droits d’utilisation d’un document PDF doté de droits d’utilisation pour effectuer d’autres opérations AEM Forms sur ce . Vous devez par exemple signer numériquement (ou certifier) un document PDF avant de définir ses droits d’utilisation. Par conséquent, si vous souhaitez effectuer des opérations sur un document doté de droits d’utilisation, vous devez supprimer les droits d’utilisation du document PDF, effectuer les autres opérations, telles que la signature numérique du document, puis réappliquer les droits d’utilisation au document.

>[!NOTE]
>
>Pour plus d’informations sur le service des extensions Acrobat Reader DC, voir [Guide de référence des services pour AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary_of_steps-1}

Pour supprimer des droits d’utilisation d’un document PDF dont les droits sont activés, procédez comme suit :

1. Incluez des fichiers de projet.
1. Créez un objet Client d’extensions Acrobat Reader DC.
1. Récupérez un document PDF dont les droits sont activés.
1. Supprimez les droits d’utilisation du document PDF.
1. Enregistrez le document PDF.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

**Création d’un objet Client d’extensions Acrobat Reader DC**

Avant de pouvoir exécuter une opération de service d’extensions Acrobat Reader DC par programmation, vous devez créer un objet client de service d’extensions Acrobat Reader DC. Si vous utilisez l’API Java, créez un objet `ReaderExtensionsServiceClient`. Si vous utilisez l’API du service Web des extensions Acrobat Reader DC, créez un objet `ReaderExtensionsServiceService`.

**Récupération d’un document PDF dont les droits sont activés**

Récupérez un document PDF dont les droits sont activés afin de supprimer les droits d’utilisation.

**Suppression des droits d’utilisation du document PDF**

Après avoir récupéré un document PDF doté de droits d’utilisation, vous pouvez supprimer des droits d’utilisation. Une fois les droits d’utilisation supprimés, le document PDF ne comporte aucune fonctionnalité supplémentaire lors de son affichage dans Adobe Reader.

**Enregistrer le document PDF**

Vous pouvez enregistrer le document PDF qui ne contient plus de droits d’utilisation en tant que fichier PDF. Une fois enregistré en tant que fichier PDF, le document PDF peut être affiché dans Adobe Reader ou Acrobat.

**Voir également**

[Suppression des droits d’utilisation à l’aide de l’API Java](assigning-usage-rights.md#remove-usage-rights-using-the-java-api)

[Suppression des droits d’utilisation à l’aide de l’API de service Web](assigning-usage-rights.md#remove-usage-rights-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[débuts rapides de l’API du service Acrobat Reader DC Extensions](/help/forms/developing/acrobat-reader-dc-extensions-service.md#acrobat-reader-dc-extensions-service-java-api-quick-start-soap)

[Application des droits d’utilisation aux Documents PDF](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

### Supprimer les droits d&#39;utilisation à l&#39;aide de l&#39;API Java {#remove-usage-rights-using-the-java-api}

Supprimez les droits d’utilisation d’un document PDF dont les droits sont activés à l’aide de l’API des extensions Acrobat Reader DC (Java) :

1. Incluez des fichiers de projet.

   Incluez des fichiers JAR client, tels que adobe-reader-extensions-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un objet Client d’extensions Acrobat Reader DC.

   Créez un objet `ReaderExtensionsServiceClient` en utilisant son constructeur et en transmettant un objet `ServiceClientFactory` contenant des propriétés de connexion.

1. Récupérez un document PDF.

   * Créez un objet `java.io.FileInputStream` représentant le document PDF dont les droits sont activés à l’aide de son constructeur et transmettez une valeur de chaîne indiquant l’emplacement du document PDF.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Supprimez les droits d’utilisation du document PDF.

   Supprimez les droits d’utilisation du document PDF en appelant la méthode `ReaderExtensionsServiceClient` de l’objet `removeUsageRights` et en transmettant l’objet `com.adobe.idp.Document` contenant le document PDF dont les droits sont activés. Cette méthode renvoie un objet `com.adobe.idp.Document` contenant un document PDF sans droits d’utilisation.

1. Appliquez des droits d’utilisation au document PDF.

   * Créez un objet `java.io.File` et assurez-vous que l’extension de fichier est .PDF.
   * Appelez la méthode `Document` de l&#39;objet `copyToFile` pour copier le contenu de l&#39;objet `Document` dans le fichier (veillez à utiliser l&#39;objet `Document` renvoyé par la méthode `removeUsageRights`).

**Voir également**

[Suppression des droits d’utilisation des Documents PDF](assigning-usage-rights.md#removing-usage-rights-from-pdf-documents)

[Début rapide (mode SOAP) : Suppression des droits d’utilisation d’un document PDF à l’aide de l’API Java](/help/forms/developing/acrobat-reader-dc-extensions-service.md#quick-start-soap-mode-removing-usage-rights-from-a-pdf-document-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Supprimer les droits d’utilisation à l’aide de l’API de service Web {#remove-usage-rights-using-the-web-service-api}

Supprimez les droits d’utilisation d’un document PDF dont les droits sont activés à l’aide de l’API des extensions Acrobat Reader DC (service Web) :

1. Incluez des fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Assurez-vous d’utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/ReaderExtensionsService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un objet Client d’extensions Acrobat Reader DC.

   * Créez un objet `ReaderExtensionsServiceClient` en utilisant son constructeur par défaut.
   * Créez un objet `ReaderExtensionsServiceClient.Endpoint.Address` en utilisant le constructeur `System.ServiceModel.EndpointAddress`. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/ReaderExtensionsService?blob=mtom`. Veillez à spécifier `?blob=mtom`.)
   * Créez un objet `System.ServiceModel.BasicHttpBinding` en obtenant la valeur du champ `ReaderExtensionsServiceClient.Endpoint.Binding`. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le champ `MessageEncoding` de l’objet `System.ServiceModel.BasicHttpBinding` sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en exécutant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `ReaderExtensionsServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `ReaderExtensionsServiceClient.ClientCredentials.UserName.Password`.
      * Affectez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Affectez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Récupérez un document PDF.

   * Créez un objet `BLOB` en utilisant son constructeur. L’objet `BLOB` est utilisé pour stocker le document PDF dont les droits d’utilisation sont supprimés.
   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du fichier du document PDF et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `System.IO.FileStream`. Vous pouvez déterminer la taille du tableau d’octets en obtenant la propriété `System.IO.FileStream` de l’objet `Length`.
   * Renseignez le tableau d’octets avec les données de flux en appelant la méthode `System.IO.FileStream` de l’objet `Read` et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’objet `BLOB` en attribuant sa propriété `MTOM` au contenu du tableau d’octets.

1. Supprimez les droits d’utilisation du document PDF.

   Supprimez les droits d’utilisation du document PDF en appelant la méthode `ReaderExtensionsServiceClient` de l’objet `removeUsageRights` et en transmettant l’objet `BLOB` contenant le document PDF dont les droits sont activés. Cette méthode renvoie un objet `BLOB` contenant un document PDF sans droits d’utilisation.

1. Appliquez des droits d’utilisation au document PDF.

   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du fichier PDF.
   * Créez un tableau d’octets qui stocke le contenu des données de l’objet `BLOB` renvoyé par la méthode `removeUsageRights`. Renseignez le tableau d’octets en obtenant la valeur du membre de données `MTOM` de l’objet `BLOB`.
   * Créez un objet `System.IO.BinaryWriter` en appelant son constructeur et en transmettant l&#39;objet `System.IO.FileStream`.

**Voir également**

[Suppression des droits d’utilisation des Documents PDF](assigning-usage-rights.md#removing-usage-rights-from-pdf-documents)

[Appel de AEM Forms à l’aide de MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Appel de AEM Forms à l’aide de SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Récupération des informations d&#39;identification {#retrieving-credential-information}

Vous pouvez récupérer des informations sur les informations d’identification utilisées pour appliquer des droits d’utilisation à un document PDF doté de droits d’utilisation. En récupérant des informations sur les informations d’identification, vous pouvez obtenir des informations telles que la date à laquelle le certificat n’est plus valide.

>[!NOTE]
>
>Pour plus d’informations sur le service des extensions Acrobat Reader DC, voir [Guide de référence des services pour AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary_of_steps-2}

Pour récupérer des informations sur les informations d’identification utilisées pour appliquer des droits d’utilisation à un document PDF, procédez comme suit :

1. Incluez des fichiers de projet.
1. Créez un objet Client d’extensions Acrobat Reader DC.
1. Récupérez un document PDF dont les droits sont activés.
1. Récupérez des informations sur les informations d’identification.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

**Création d’un objet Client d’extensions Acrobat Reader DC**

Avant de pouvoir exécuter une opération de service d’extensions Acrobat Reader DC par programmation, vous devez créer un objet client de service d’extensions Acrobat Reader DC. Si vous utilisez l’API Java, créez un objet `ReaderExtensionsServiceClient`. Si vous utilisez l’API du service Web des extensions Acrobat Reader DC, créez un objet `ReaderExtensionsServiceService`.

**Récupération d’un document PDF dont les droits sont activés**

Vous devez récupérer un document PDF dont les droits sont activés afin de récupérer des informations sur les informations d’identification. Vous pouvez également récupérer des informations sur les informations d’identification en spécifiant son alias ; toutefois, si vous souhaitez récupérer des informations sur des informations d’identification qui ont été utilisées pour appliquer des droits d’utilisation à un document PDF dont les droits sont activés, vous devez récupérer le document.

**Récupérer des informations sur les informations d’identification**

Après avoir récupéré un document PDF doté de droits, vous pouvez obtenir des informations sur les informations d’identification utilisées pour lui appliquer des droits d’utilisation. Vous pouvez obtenir les informations d’identification suivantes :

* Message affiché dans Adobe Reader à l’ouverture du document PDF dont les droits sont activés.
* Date à laquelle les informations d’identification ne sont plus valides.
* Date avant laquelle les informations d’identification ne sont pas valides.
* Droits d’utilisation définis pour ce document PDF dont les droits sont activés.
* Nombre d’utilisation des informations d’identification.

**Voir également**

[Suppression des droits d’utilisation à l’aide de l’API Java](assigning-usage-rights.md#remove-usage-rights-using-the-java-api)

[Suppression des droits d’utilisation à l’aide de l’API de service Web](assigning-usage-rights.md#remove-usage-rights-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[débuts rapides de l’API du service Acrobat Reader DC Extensions](/help/forms/developing/acrobat-reader-dc-extensions-service.md#acrobat-reader-dc-extensions-service-java-api-quick-start-soap)

### Récupérer les informations d’identification à l’aide de l’API Java {#retrieve-credential-information-using-the-java-api}

Récupérez les informations d’identification à l’aide de l’API des extensions Acrobat Reader DC (Java) :

1. Incluez des fichiers de projet.

   Incluez des fichiers JAR client, tels que adobe-reader-extensions-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un objet Client d’extensions Acrobat Reader DC.

   Créez un objet `ReaderExtensionsServiceClient` en utilisant son constructeur et en transmettant un objet `ServiceClientFactory` contenant des propriétés de connexion.

1. Récupérez un document PDF.

   * Créez un objet `java.io.FileInputStream` représentant le document PDF dont les droits sont activés à l’aide de son constructeur et transmettez une valeur de chaîne qui spécifie l’emplacement du document PDF dont les droits sont activés.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Supprimez les droits d’utilisation du document PDF.

   * Récupérez des informations sur les informations d’identification utilisées pour appliquer des droits d’utilisation au document PDF en appelant la méthode `ReaderExtensionsServiceClient` de l’objet `getDocumentUsageRights` et en transmettant l’objet `com.adobe.idp.Document` contenant le document PDF dont les droits sont activés. Cette méthode renvoie un objet `GetUsageRightsResult` contenant des informations d’identification.
   * Récupérez la date à laquelle les informations d’identification ne sont plus valides en appelant la méthode `GetUsageRightsResult` de l’objet `getNotAfter`. Cette méthode renvoie un objet `java.util.Date` qui représente la date à laquelle les informations d’identification ne sont plus valides.
   * Récupérez le message qui s’affiche en Adobe Reader lorsque le document PDF dont les droits sont activés est ouvert en appelant la méthode `GetUsageRightsResult` de l’objet `getMessage`. Cette méthode renvoie une valeur de chaîne qui représente le message.

**Voir également**

[Récupération des informations d’identification](assigning-usage-rights.md#retrieving-credential-information)

[Début rapide (mode SOAP) : Récupération des informations d’identification à l’aide de l’API Java](/help/forms/developing/acrobat-reader-dc-extensions-service.md#quick-start-soap-mode-retrieving-credential-information-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Récupérer les informations d’identification à l’aide de l’API de service Web {#retrieve-credential-information-using-the-web-service-api}

Récupérez les informations d’identification à l’aide de l’API des extensions Acrobat Reader DC (service Web) :

1. Incluez des fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Assurez-vous d’utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/ReaderExtensionsService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un objet Client d’extensions Acrobat Reader DC.

   * Créez un objet `ReaderExtensionsServiceClient` en utilisant son constructeur par défaut.
   * Créez un objet `ReaderExtensionsServiceClient.Endpoint.Address` en utilisant le constructeur `System.ServiceModel.EndpointAddress`. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/ReaderExtensionsService?blob=mtom`. Veillez à spécifier `?blob=mtom`.)
   * Créez un objet `System.ServiceModel.BasicHttpBinding` en obtenant la valeur du champ `ReaderExtensionsServiceClient.Endpoint.Binding`. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le champ `MessageEncoding` de l’objet `System.ServiceModel.BasicHttpBinding` sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en exécutant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `ReaderExtensionsServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `ReaderExtensionsServiceClient.ClientCredentials.UserName.Password`.
      * Affectez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Affectez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Récupérez un document PDF.

   * Créez un objet `BLOB` en utilisant son constructeur. L’objet `BLOB` est utilisé pour stocker un document PDF dont les droits sont activés.
   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du fichier du document PDF dont les droits sont activés et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `System.IO.FileStream`. Vous pouvez déterminer la taille du tableau d’octets en obtenant la propriété `System.IO.FileStream` de l’objet `Length`.
   * Renseignez le tableau d’octets avec les données de flux en appelant la méthode `System.IO.FileStream` de l’objet `Read` et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’objet `BLOB` en attribuant sa propriété `MTOM` au contenu du tableau d’octets.

1. Supprimez les droits d’utilisation du document PDF.

   * Récupérez des informations sur les informations d’identification utilisées pour appliquer des droits d’utilisation au document PDF en appelant la méthode `ReaderExtensionsServiceClient` de l’objet `getDocumentUsageRights` et en transmettant l’objet `com.adobe.idp.Document` contenant le document PDF dont les droits sont activés. Cette méthode renvoie un objet `GetUsageRightsResult` contenant des informations d’identification.
   * Récupérez la date à laquelle les informations d’identification ne sont plus valides en obtenant la valeur du membre de données `GetUsageRightsResult` de l’objet `notAfter`. Le type de données de ce membre de données est `System.DateTime`.
   * Récupérez le message qui s’affiche lorsque le document PDF doté de droits est ouvert dans Adobe Reader en obtenant la valeur du membre de données `GetUsageRightsResult` de l’objet `message`. Le type de données de ce membre de données est une chaîne.
   * Récupérez le nombre d’utilisation des informations d’identification en obtenant la valeur du membre de données `GetUsageRightsResult` de l’objet `useCount`. Le type de données de ce membre de données est un entier.

**Voir également**

[Récupération des informations d’identification](assigning-usage-rights.md#retrieving-credential-information)

[Appel de AEM Forms à l’aide de MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Appel de AEM Forms à l’aide de SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
