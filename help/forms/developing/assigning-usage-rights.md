---
title: Attribution des droits d’utilisation
description: Utilisez l’API client Java Extensions Acrobat Reader DC et l’API de service web pour appliquer et supprimer des droits d’utilisation des documents PDF.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 6af148eb-427a-4b54-9c5f-8750736882d8
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '3897'
ht-degree: 97%

---

# Attribution des droits d’utilisation {#assigning-usage-rights}

**Les exemples et les échantillons de ce document sont réservés à l’environnement AEM Forms sur JEE.**

## À propos du service Extensions Acrobat Reader DC {#about-the-acrobat-reader-dc-extensions-service}

Le service Extensions Acrobat Reader DC permet à votre entreprise de partager facilement des documents PDF interactifs en étendant les fonctionnalités d’Adobe Reader. Le service Extensions Acrobat Reader DC prend entièrement en charge tout document PDF, y compris PDF 1.7. Il fonctionne avec Adobe Reader 7.0 et versions ultérieures. Le service dote un document PDF de droits d’utilisation qui activent des fonctions généralement non indisponibles à l’ouverture d’un document PDF dans Adobe Reader. Les utilisateurs tiers n’ont pas besoin de disposer d’un logiciel supplémentaire ni de modules externes pour utiliser les documents dotés de droits d’utilisation.

Vous pouvez accomplir ces tâches à l’aide du service Extensions Acrobat Reader DC :

* Appliquez des droits d’utilisation aux documents PDF. Pour plus d’informations, voir [Appliquer des droits d’utilisation aux documents PDF](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents).
* Supprimez les droits d’utilisation des documents PDF. Pour plus d’informations, voir [Supprimer des droits d’utilisation des documents PDF](assigning-usage-rights.md#removing-usage-rights-from-pdf-documents).
* Récupérez les informations d’identification. Pour plus d’informations, voir [Récupérer des informations d’identification](assigning-usage-rights.md#retrieving-credential-information).

>[!NOTE]
>
>Pour plus d’informations sur le service Extensions Acrobat Reader DC, voir [Référence des services pour AEM Forms](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

## Appliquer des droits d’utilisation aux documents PDF {#applying-usage-rights-to-pdf-documents}

Vous pouvez appliquer des droits d’utilisation aux documents PDF à l’aide de l’API client Java Extensions Reader et Web Service. Les droits d’utilisation appartiennent à la fonctionnalité disponible par défaut dans Acrobat mais non dans Adobe Reader, telle que la capacité à ajouter des commentaires à un formulaire ou à remplir des champs de formulaire et enregistrer ce dernier. Les documents de PDF auxquels des droits d’utilisation sont appliqués sont appelés des documents dont les droits sont activés. Un utilisateur qui ouvre un document dont les droits sont activés dans Adobe Reader peut effectuer des opérations qui sont activées pour ce document spécifique.

>[!NOTE]
>
>Lors de l’application de droits d’utilisation aux documents PDF à l’aide de la méthode `applyUsageRights`, qui fait partie de l’API Java, vous pouvez définir le paramètre `isModeFinal` de l’objet `ReaderExtensionsOptionSpec` sur `false`. Le compteur de formulaires traités n’est alors pas mis à jour et les performances s’en trouvent améliorées. Si vous n’avez pas besoin de mettre à jour le compteur de formulaires, il est recommandé de définir le paramètre `isModeFinal` sur `false`.

>[!NOTE]
>
>Pour plus d’informations sur le service Extensions Acrobat Reader DC, voir [Référence des services pour AEM Forms](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

### Résumé des étapes {#summary-of-steps}

Pour appliquer des droits d’utilisation à un document PDF, procédez comme suit :

1. Incluez les fichiers de projet.
1. Créez un objet Client des extensions Acrobat Reader DC.
1. Récupérez un document PDF.
1. Spécifiez les droits d’utilisation à appliquer.
1. Appliquez les droits d’utilisation au document PDF.
1. Enregistrez le document PDF défini avec des droits d’utilisation.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services web, veillez à inclure les fichiers proxy.

**Créer un objet client Extensions Acrobat Reader DC**

Pour effectuer par programmation une opération de service Extensions Acrobat Reader DC, vous devez créer un objet client de service Extensions Acrobat Reader DC. Si vous utilisez l’API Java Extensions Acrobat Reader DC, créez un objet `ReaderExtensionsServiceClient`. Si vous utilisez l’API Web Service Extensions Acrobat Reader DC, créez un objet `ReaderExtensionsServiceService`.

**Récupérer un document PDF**

Récupérez un document de PDF pour appliquer des droits d’utilisation. Les documents PDF définis avec des droits d’utilisation contiennent un dictionnaire de droits d’utilisation. Lorsqu’Adobe Reader ouvre un document contenant un tel dictionnaire, il active uniquement les droits d’utilisation spécifiés dans le dictionnaire pour ce document. Si le document ne contient pas de dictionnaire des droits d’utilisation, le service Extensions Acrobat Reader DC en crée un. S’il contient déjà un dictionnaire, le service Extensions Acrobat Reader DC remplace les droits d’utilisation existants par ceux que vous spécifiez. Le dictionnaire spécifie les droits d’utilisation activés. Lorsqu’un utilisateur ouvre le document dans Adobe Reader, seuls les droits d’utilisation spécifiés dans le dictionnaire sont autorisés.

**Spécifier des droits d’utilisation à appliquer**

Les droits d’utilisation que vous pouvez définir sont déterminés par des informations d’identification que vous pouvez acheter à Adobe Systems Incorporated. Les informations d’identification permettent généralement de définir un groupe de droits d’utilisation associés, tels que ceux relatifs aux formulaires interactifs. Chaque information d’identification permet de créer un certain nombre de documents PDF définis avec des droits d’utilisation. Des informations d’identification d’évaluation permettent de créer un nombre illimité de brouillons de documents.

>[!NOTE]
>
>Si vous tentez d’attribuer un droit d’utilisation non autorisé par vos informations d’identification, une exception sera déclenchée.

**Appliquer des droits d’utilisation au document PDF**

Pour appliquer des droits d’utilisation à un document PDF, référencez l’alias des informations d’identification que vous utilisez pour appliquer des droits d’utilisation (les informations d’identification sont généralement installées lors de l’installation d’AEM Forms). Vous devez également spécifier le document PDF auquel des droits d’utilisation sont appliqués. Pour plus d’informations sur la configuration d’informations d’identification, consultez le guide d’installation et de déploiement de votre serveur d’applications.

**Enregistrer le document PDF dont les droits d’utilisation ont été activés**

Une fois que le service d’extensions Acrobat Reader DC a appliqué des droits d’utilisation à un document PDF, vous pouvez enregistrer le document PDF avec droits d’utilisation sous forme de fichier PDF.

**Voir également**

[Appliquer des droits d’utilisation à l’aide de l’API Java](assigning-usage-rights.md#apply-usage-rights-using-the-java-api)

[Appliquer les droits d’utilisation à l’aide de l’API Web Service](assigning-usage-rights.md#apply-usage-rights-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Démarrages rapides de l’API du service des extensions Acrobat Reader DC](/help/forms/developing/acrobat-reader-dc-extensions-service.md#acrobat-reader-dc-extensions-service-java-api-quick-start-soap)

### Appliquer des droits d’utilisation à l’aide de l’API Java {#apply-usage-rights-using-the-java-api}

Appliquez des droits d’utilisation à un document PDF à l’aide de l’API des extensions Acrobat Reader DC (Java) :

1. Inclure les fichiers du projet

   Incluez les fichiers JAR du client, tels qu’adobe-livecycle-client.jar, dans le chemin d’accès aux classes de votre projet Java.

1. Créez un objet Client des extensions Acrobat Reader DC.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `ReaderExtensionsServiceClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`. 

1. Récupérez un document PDF.

   * Créez un objet `java.io.FileInputStream` qui représente le document PDF en utilisant son constructeur et en transmettant une valeur de chaîne qui spécifie l’emplacement du document PDF.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Spécifiez les droits d’utilisation à appliquer.

   * Créez un objet `UsageRights` qui représente les droits d’utilisation à l’aide de son constructeur.
   * Pour chaque droit d’utilisation à appliquer, appelez une méthode correspondante qui appartient à l’objet `UsageRights`. Par exemple, pour ajouter le droit d’utilisation `enableFormFillIn`, appelez la méthode `enableFormFillIn` de l’objet `UsageRights` et transmettez `true`. (Répétez cette étape pour chaque droit d’utilisation à appliquer).

1. Appliquez les droits d’utilisation au document PDF.

   * Créez un objet `ReaderExtensionsOptionSpec` en utilisant son constructeur. Cet objet contient les options d’exécution requises par le service Extensions Acrobat Reader DC. Lorsque vous appelez ce constructeur, vous devez spécifier les valeurs suivantes :

      * Objet `UsageRights` contenant les droits d’utilisation à appliquer au document.
      * Valeur de chaîne qui spécifie un message que l’utilisateur voit lorsque le document PDF avec droits d’utilisation est ouvert dans Adobe Reader 7.x. Ce message n’est pas affiché dans Adobe Reader 8.0.

   * Appliquez des droits d’utilisation au document PDF en appelant la méthode `applyUsageRights` de l’objet `ReaderExtensionsServiceClient` et en transmettant les valeurs suivantes :

      * Objet `com.adobe.idp.Document` contenant le document PDF auquel les droits d’utilisation sont appliqués.
      * Valeur de chaîne spécifiant l’alias des informations d’identification qui vous permettent d’appliquer les droits d’utilisation.
      * Valeur string qui spécifie la valeur du mot de passe correspondant. (Actuellement, ce paramètre est ignoré. Vous pouvez transmettre `null`.)

   * Objet `ReaderExtensionsOptionSpec` contenant les options d’exécution.

   La méthode `applyUsageRights` renvoie un objet `com.adobe.idp.Document` qui contient le document PDF dont les droits sont activés.

1. Enregistrez le document PDF défini avec des droits d’utilisation.

   * Créez un objet `java.io.File` et assurez-vous que l’extension du fichier est .pdf.
   * Appelez la méthode `copyToFile` de l’objet `com.adobe.idp.Document` pour copier le contenu de l’objet `com.adobe.idp.Document` dans le fichier (assurez-vous d’utiliser l’objet `com.adobe.idp.Document` qui a été renvoyé par la méthode `applyUsageRights`).

**Voir également**

[Appliquer des droits d’utilisation aux documents PDF](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

[Didacticiel de mise en route (mode SOAP) : appliquer des droits d’utilisation à l’aide de l’API Java](/help/forms/developing/acrobat-reader-dc-extensions-service.md#quick-start-soap-mode-applying-usage-rights-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Appliquer les droits d’utilisation à l’aide de l’API Web Service {#apply-usage-rights-using-the-web-service-api}

Appliquez des droits d’utilisation à un document PDF à l’aide de l’API d’extensions Acrobat Reader DC (Web Service) :

1. Incluez les fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Veillez à utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/ReaderExtensionsService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un objet Client des extensions Acrobat Reader DC.

   * Créez un objet `ReaderExtensionsServiceClient` en utilisant son constructeur par défaut.
   * Créez un objet `ReaderExtensionsServiceClient.Endpoint.Address` en utilisant le constructeur `System.ServiceModel.EndpointAddress`. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple `http://localhost:8080/soap/services/ReaderExtensionsService?blob=mtom`. Assurez-vous de spécifier `?blob=mtom`).
   * Créez un objet `System.ServiceModel.BasicHttpBinding` en récupérant la valeur du champ `ReaderExtensionsServiceClient.Endpoint.Binding`. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le champ `MessageEncoding` de l’objet `System.ServiceModel.BasicHttpBinding` sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `ReaderExtensionsServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `ReaderExtensionsServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Récupérez un document PDF.

   * Créez un objet `BLOB` en utilisant son constructeur. L’objet `BLOB` sert à stocker un document PDF auquel des droits d’utilisation sont appliqués.
   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur de chaîne représentant l’emplacement du document PDF et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `System.IO.FileStream`. Vous pouvez déterminer la taille du tableau d’octets en obtenant la propriété `Length` de l’objet `System.IO.FileStream`.
   * Renseignez le tableau d’octets avec le flux de données en appelant la méthode `Read` de l’objet `System.IO.FileStream`. Transmettez le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’objet `BLOB` en affectant à sa propriété `MTOM` le contenu du tableau d’octets.

1. Spécifiez les droits d’utilisation à appliquer.

   * Créez un objet `UsageRights` représentant les droits d’utilisation à l’aide de son constructeur.
   * Pour chaque droit d’utilisation à appliquer, affectez la valeur `true` au membre de données correspondant appartenant à l’objet `UsageRights`. Par exemple, pour ajouter le droit d’utilisation `enableFormFillIn`, affectez `true` au membre de données `enableFormFillIn` de l’objet `UsageRights`. (Répétez cette étape pour chaque droit d’utilisation à appliquer).

1. Appliquez les droits d’utilisation au document PDF.

   * Créez un objet `ReaderExtensionsOptionSpec` en utilisant son constructeur. Cet objet contient des options d’exécution requises par le service Extensions Acrobat Reader DC.
   * Affectez l’objet `UsageRights` au membre de données `usageRights` de l’objet `ReaderExtensionsOptionSpec`.
   * Affectez une valeur de chaîne spécifiant le message qu’un utilisateur voit lorsqu’un document PDF défini avec des droits d’utilisation est ouvert dans Adobe Reader au membre de données `message` de l’objet `ReaderExtensionsOptionSpec`.
   * Appliquez des droits d’utilisation au document PDF en appelant la méthode `applyUsageRights` de l’objet `ReaderExtensionsServiceClient` et en transmettant les valeurs suivantes :

      * Objet `BLOB` contenant le document PDF auquel les droits d’utilisation sont appliqués.
      * Valeur de chaîne spécifiant l’alias des informations d’identification qui vous permettent d’appliquer les droits d’utilisation.
      * Valeur string qui spécifie la valeur du mot de passe correspondant. (Actuellement, ce paramètre est ignoré. Vous pouvez transmettre `null`.)

   * Objet `ReaderExtensionsOptionSpec` contenant les options d’exécution.

   La méthode `applyUsageRights` renvoie un objet `BLOB` qui contient le document PDF dont les droits sont activés.

1. Enregistrez le document PDF défini avec des droits d’utilisation.

   * Créez un objet `System.IO.FileStream` en utilisant son constructeur. Transmettez une valeur de chaîne représentant l’emplacement du document PDF défini avec des droits d’utilisation.
   * Créez un tableau d’octets qui stocke le contenu des données de l’objet `BLOB` qui a été renvoyé par la méthode `applyUsageRights`. Renseignez le tableau d’octets en obtenant la valeur du membre de données `MTOM` de l’objet `BLOB`.
   * Créez un objet `System.IO.BinaryWriter` en utilisant son constructeur et en transmettant l’objet `System.IO.FileStream`.
   * Écrivez le contenu du tableau d’octets dans un fichier PDF en appelant la méthode `Write` de l’objet `System.IO.BinaryWriter` et en transmettant le tableau d’octets.

**Voir également**

[Appliquer des droits d’utilisation aux documents PDF](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

[Appeler AEM Forms en utilisant MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Appel d’AEM Forms à l’aide de SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Suppression des droits d’utilisation des documents PDF {#removing-usage-rights-from-pdf-documents}

Vous pouvez supprimer des droits d’utilisation d’un document défini avec des droits d’utilisation. La suppression des droits d’utilisation d’un document de PDF dont les droits sont activés est également nécessaire pour effectuer d’autres opérations AEM Forms sur celui-ci. Vous devez par exemple signer numériquement (ou certifier) un document PDF avant de définir ses droits d’utilisation. Par conséquent, pour effectuer des opérations sur un document défini avec des droits d’utilisation, vous devez supprimer les droits du document PDF, effectuer les autres opérations, comme la signature numérique d’un document, puis réappliquer des droits d’utilisation à ce document.

>[!NOTE]
>
>Pour plus d’informations sur le service Extensions Acrobat Reader DC, voir [Référence des services pour AEM Forms](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

### Résumé des étapes {#summary_of_steps-1}

Pour supprimer des droits d’utilisation d’un document PDF défini avec des droits d’utilisation, procédez comme suit :

1. Incluez les fichiers de projet.
1. Créez un objet Client des extensions Acrobat Reader DC.
1. Récupérez un document PDF dont les droits sont activés.
1. Supprimez les droits d’utilisation du document PDF.
1. Enregistrez le formulaire PDF.

**Inclure des fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services web, veillez à inclure les fichiers proxy.

**Créer un objet client Extensions Acrobat Reader DC**

Avant d’effectuer par programmation une opération de service d’extensions Acrobat Reader DC, vous devez créer un objet client de service d’extensions Acrobat Reader DC. Si vous utilisez l’API Java, créez un objet `ReaderExtensionsServiceClient`. Si vous utilisez l’API Web Service Extensions Acrobat Reader DC, créez un objet `ReaderExtensionsServiceService`.

**Récupérer un document PDF défini avec des droits d’utilisation**

Récupérez un document de PDF dont les droits sont activés pour supprimer les droits d’utilisation.

**Supprimer des droits d’utilisation du document PDF**

Après avoir récupéré un document PDF défini avec des droits d’utilisation, vous pouvez supprimer les droits d’utilisation. Une fois les droits d’utilisation supprimés, le document PDF ne comporte aucune fonctionnalité supplémentaire lors de son affichage dans Adobe Reader.

**Enregistrer un document PDF**

Vous pouvez enregistrer le document PDF ne contenant plus de droits d’utilisation en tant que fichier PDF. Une fois enregistré en tant que fichier PDF, le document PDF peut être visualisé dans Adobe Reader ou Acrobat.

**Voir également**

[Supprimer des droits d’utilisation à l’aide de l’API Java](assigning-usage-rights.md#remove-usage-rights-using-the-java-api)

[Supprimer les droits d’utilisation à l’aide de l’API Web Service](assigning-usage-rights.md#remove-usage-rights-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Démarrages rapides de l’API du service Extensions Acrobat Reader DC](/help/forms/developing/acrobat-reader-dc-extensions-service.md#acrobat-reader-dc-extensions-service-java-api-quick-start-soap)

[Appliquer des droits d’utilisation aux documents PDF](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

### Supprimer des droits d’utilisation à l’aide de l’API Java {#remove-usage-rights-using-the-java-api}

Supprimez les droits d’utilisation d’un document PDF dont les droits sont activés à l’aide de l’API des extensions Acrobat Reader DC (Java) :

1. Incluez les fichiers de projet.

   Incluez les fichiers JAR client, tels qu’adobe-livecycle-client.jar, dans le chemin d’accès aux classes de votre projet Java.

1. Créez un objet Client des extensions Acrobat Reader DC.

   Créez un objet `ReaderExtensionsServiceClient` en utilisant son constructeur et en transmettant un objet `ServiceClientFactory` contenant des propriétés de connexion.

1. Récupérez un document PDF.

   * Créez un objet `java.io.FileInputStream` qui représente le document PDF dont les droits sont activés en utilisant son constructeur et en transmettant une valeur de chaîne qui spécifie l’emplacement du document PDF.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Supprimez les droits d’utilisation du document PDF.

   Supprimez les droits d’utilisation du document PDF en appelant la méthode `removeUsageRights` de l’objet `ReaderExtensionsServiceClient` et en transmettant l’objet `com.adobe.idp.Document` qui contient le document PDF dont les droits sont activés. Cette méthode renvoie un objet `com.adobe.idp.Document` qui contient un document PDF ne disposant pas de droits d’utilisation.

1. Appliquez les droits d’utilisation au document PDF.

   * Créez un objet `java.io.File` et assurez-vous que l’extension du fichier est .PDF.
   * Appelez la méthode `copyToFile` de l’objet `Document` pour copier le contenu de l’objet `Document` dans le fichier (assurez-vous d’utiliser l’objet `Document` qui a été renvoyé par la méthode `removeUsageRights`).

**Voir également**

[Suppression des droits d’utilisation des documents PDF](assigning-usage-rights.md#removing-usage-rights-from-pdf-documents)

[Didacticiel de mise en route (mode SOAP) : supprimer des droits d’utilisation d’un document PDF à l’aide de l’API Java](/help/forms/developing/acrobat-reader-dc-extensions-service.md#quick-start-soap-mode-removing-usage-rights-from-a-pdf-document-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Supprimer les droits d’utilisation à l’aide de l’API Web Service {#remove-usage-rights-using-the-web-service-api}

Supprimez les droits d’utilisation d’un document PDF dont les droits sont activés à l’aide de l’API des extensions Acrobat Reader DC (Web Service) :

1. Incluez les fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Veillez à utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/ReaderExtensionsService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un objet Client des extensions Acrobat Reader DC.

   * Créez un objet `ReaderExtensionsServiceClient` en utilisant son constructeur par défaut.
   * Créez un objet `ReaderExtensionsServiceClient.Endpoint.Address` en utilisant le constructeur `System.ServiceModel.EndpointAddress`. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple `http://localhost:8080/soap/services/ReaderExtensionsService?blob=mtom`. Assurez-vous de spécifier `?blob=mtom`).
   * Créez un objet `System.ServiceModel.BasicHttpBinding` en récupérant la valeur du champ `ReaderExtensionsServiceClient.Endpoint.Binding`. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le champ `MessageEncoding` de l’objet `System.ServiceModel.BasicHttpBinding` sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `ReaderExtensionsServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `ReaderExtensionsServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Récupérez un document PDF.

   * Créez un objet `BLOB` en utilisant son constructeur. L’objet `BLOB` sert à stocker le document PDF défini avec des droits d’utilisation et à partir duquel les droits d’utilisation sont supprimés.
   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur de chaîne représentant l’emplacement du document PDF et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `System.IO.FileStream`. Vous pouvez déterminer la taille du tableau d’octets en obtenant la propriété `Length` de l’objet `System.IO.FileStream`.
   * Renseignez le tableau d’octets avec les données de diffusion en appelant la méthode `Read` de l’objet `System.IO.FileStream` et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’objet `BLOB` en affectant sa propriété `MTOM` au contenu du tableau d’octets.

1. Supprimez les droits d’utilisation du document PDF.

   Supprimez les droits d’utilisation du document PDF en appelant la méthode `removeUsageRights` de l’objet `ReaderExtensionsServiceClient` et en transmettant l’objet `BLOB` qui contient le document PDF dont les droits sont activés. Cette méthode renvoie un objet `BLOB` qui contient un document PDF ne disposant pas de droits d’utilisation.

1. Appliquez les droits d’utilisation au document PDF.

   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur de chaîne représentant l’emplacement du fichier du PDF.
   * Créez un tableau d’octets qui stocke le contenu des données de l’objet `BLOB` qui a été renvoyé par la méthode `removeUsageRights`. Renseignez le tableau d’octets en obtenant la valeur du membre de données `MTOM` de l’objet `BLOB`.
   * Créez un objet `System.IO.BinaryWriter` en appelant son constructeur et en transmettant l’objet `System.IO.FileStream`.

**Voir également**

[Suppression des droits d’utilisation des documents PDF](assigning-usage-rights.md#removing-usage-rights-from-pdf-documents)

[Appeler AEM Forms en utilisant MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Appel d’AEM Forms à l’aide de SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Récupérer des informations d’identification {#retrieving-credential-information}

Vous pouvez récupérer des informations sur les informations d’identification utilisées pour appliquer des droits d’utilisation à un document PDF dont les droits sont activés. En récupérant des informations sur des informations d’identification, vous pouvez obtenir des informations telles que la date à laquelle le certificat n’est plus valide.

>[!NOTE]
>
>Pour plus d’informations sur le service Extensions Acrobat Reader DC, voir [Référence des services pour AEM Forms](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

### Résumé des étapes {#summary_of_steps-2}

Pour récupérer des informations sur les informations d’identification utilisées pour appliquer des droits d’utilisation à un document PDF, procédez comme suit :

1. Incluez les fichiers de projet.
1. Créez un objet Client des extensions Acrobat Reader DC.
1. Récupérez un document PDF dont les droits sont activés.
1. Récupérez des informations sur les informations d’identification.

**Inclure des fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services web, veillez à inclure les fichiers proxy.

**Créer un objet client Extensions Acrobat Reader DC**

Avant d’effectuer par programmation une opération de service d’extensions Acrobat Reader DC, vous devez créer un objet client de service d’extensions Acrobat Reader DC. Si vous utilisez l’API Java, créez un objet `ReaderExtensionsServiceClient`. Si vous utilisez l’API Web Service Extensions Acrobat Reader DC, créez un objet `ReaderExtensionsServiceService`.

**Récupérer un document PDF défini avec des droits d’utilisation**

Récupérez un document de PDF dont les droits sont activés pour récupérer des informations sur les informations d’identification. Vous pouvez également récupérer des informations sur une information d’identification en spécifiant son alias. Toutefois, si vous souhaitez récupérer des informations sur des informations d’identification qui ont été utilisées pour appliquer des droits d’utilisation à un document PDF spécifique dont les droits sont activés, vous devez récupérer le document.

**Récupérer des informations sur les informations d’identification**

Après avoir récupéré un document PDF dont les droits sont activés, vous pouvez obtenir des informations sur les informations d’identification qui ont été utilisées pour lui appliquer des droits d’utilisation. Vous pouvez obtenir les informations d’identification suivantes :

* Message affiché dans Adobe Reader à l’ouverture du document PDF dont les droits sont activés.
* Date à laquelle les informations d’identification ne sont plus valides.
* Date avant laquelle les informations d’identification ne sont pas valides.
* Droits d’utilisation définis pour ce document PDF dont les droits sont activés.
* Nombre de fois que les informations d’identification ont été utilisées.

**Voir également**

[Supprimer des droits d’utilisation à l’aide de l’API Java](assigning-usage-rights.md#remove-usage-rights-using-the-java-api)

[Supprimer les droits d’utilisation à l’aide de l’API Web Service](assigning-usage-rights.md#remove-usage-rights-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Démarrages rapides de l’API du service Extensions Acrobat Reader DC](/help/forms/developing/acrobat-reader-dc-extensions-service.md#acrobat-reader-dc-extensions-service-java-api-quick-start-soap)

### Récupérer des informations d’identification à l’aide de l’API Java {#retrieve-credential-information-using-the-java-api}

Récupérez les informations d’identification à l’aide de l’API Extensions Acrobat Reader DC (Java) :

1. Incluez les fichiers de projet.

   Incluez les fichiers JAR client, tels qu’adobe-livecycle-client.jar, dans le chemin d’accès aux classes de votre projet Java.

1. Créez un objet Client des extensions Acrobat Reader DC.

   Créez un objet `ReaderExtensionsServiceClient` en utilisant son constructeur et en transmettant un objet `ServiceClientFactory` contenant des propriétés de connexion.

1. Récupérez un document PDF.

   * Créez un objet `java.io.FileInputStream` qui représentent le document PDF dont les droits sont activés en utilisant son constructeur et en transmettant une valeur de chaîne qui spécifie l’emplacement du document PDF dont les droits sont activés.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Supprimez les droits d’utilisation du document PDF.

   * Récupérez les informations relatives aux informations d’identification utilisées pour appliquer les droits d’utilisation au document PDF en appelant la méthode `getDocumentUsageRights` de l’objet `ReaderExtensionsServiceClient` et en transmettant l’objet `com.adobe.idp.Document` qui contient le document PDF dont les droits sont activés. Cette méthode renvoie un objet `GetUsageRightsResult` qui contient des informations d’identification.
   * Récupérez la date après laquelle les informations d’identification ne sont plus valides en appelant la méthode `getNotAfter` de l’objet `GetUsageRightsResult`. Cette méthode renvoie un objet `java.util.Date` qui représente la date après laquelle les informations d’identification ne sont plus valides.
   * Récupérez le message qui s’affiche dans Adobe Reader lors de l’ouverture d’un document PDF dont les droits sont activés en appelant la méthode `getMessage` de l’objet `GetUsageRightsResult`. Cette méthode renvoie une valeur de chaîne qui représente le message.

**Voir également**

[Récupérer des informations d’identification](assigning-usage-rights.md#retrieving-credential-information)

[Didacticiel de mise en route (mode SOAP) : récupérer des informations d’identification à l’aide de l’API Java](/help/forms/developing/acrobat-reader-dc-extensions-service.md#quick-start-soap-mode-retrieving-credential-information-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Récupérer des informations d’identification à l’aide de l’API Web Service {#retrieve-credential-information-using-the-web-service-api}

Récupérez les informations d’identification à l’aide de l’API des extensions Acrobat Reader DC (Web Service) :

1. Incluez les fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Veillez à utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/ReaderExtensionsService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un objet Client des extensions Acrobat Reader DC.

   * Créez un objet `ReaderExtensionsServiceClient` en utilisant son constructeur par défaut.
   * Créez un objet `ReaderExtensionsServiceClient.Endpoint.Address` en utilisant le constructeur `System.ServiceModel.EndpointAddress`. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple `http://localhost:8080/soap/services/ReaderExtensionsService?blob=mtom`. Assurez-vous de spécifier `?blob=mtom`).
   * Créez un objet `System.ServiceModel.BasicHttpBinding` en récupérant la valeur du champ `ReaderExtensionsServiceClient.Endpoint.Binding`. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le champ `MessageEncoding` de l’objet `System.ServiceModel.BasicHttpBinding` sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `ReaderExtensionsServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `ReaderExtensionsServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Récupérez un document PDF.

   * Créez un objet `BLOB` en utilisant son constructeur. L’objet `BLOB` est utilisé pour stocker un document de PDF dont les droits sont activés.
   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du fichier du document PDF dont les droits sont activés et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `System.IO.FileStream`. Vous pouvez déterminer la taille du tableau d’octets en obtenant la propriété `Length` de l’objet `System.IO.FileStream`.
   * Renseignez le tableau d’octets avec les données de diffusion en appelant la méthode `Read` de l’objet `System.IO.FileStream` et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’objet `BLOB` en affectant sa propriété `MTOM` au contenu du tableau d’octets.

1. Supprimez les droits d’utilisation du document PDF.

   * Récupérez des informations sur les informations d’identification utilisées pour appliquer des droits d’utilisation au document PDF en appelant la méthode `getDocumentUsageRights` de l’objet `ReaderExtensionsServiceClient` et en transmettant l’objet `com.adobe.idp.Document` contenant le document PDF dont les droits sont activés. Cette méthode renvoie un objet `GetUsageRightsResult` contenant des informations d’identification.
   * Récupérez la date après laquelle les informations d’identification ne sont plus valides en obtenant la valeur du membre de données `notAfter` de l’objet `GetUsageRightsResult`. Le type de données de ce membre de données est `System.DateTime`.
   * Récupérez le message qui s’affiche lorsque le document PDF dont les droits sont activés est ouvert dans Adobe Reader en obtenant la valeur du membre de données `message` de l’objet `GetUsageRightsResult`. Le type de données de ce membre de données est une chaîne.
   * Récupérez le nombre de fois où les informations d’identification sont utilisées en obtenant la valeur du membre de données `useCount` de l’objet `GetUsageRightsResult`. Le type de données de ce membre de données est un entier.

**Voir également**

[Récupérer des informations d’identification](assigning-usage-rights.md#retrieving-credential-information)

[Appeler AEM Forms en utilisant MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Appel d’AEM Forms à l’aide de SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
