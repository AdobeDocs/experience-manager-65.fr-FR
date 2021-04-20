---
title: Utilisation des informations d’identification
seo-title: Utilisation des informations d’identification
description: Importez les informations d’identification dans AEM Forms à l’aide de l’API Trust Manager et de l’API Java. En outre, découvrez comment supprimer des informations d’identification à l’aide de l’API Trust Manager et de l’API Java.
seo-description: Importez les informations d’identification dans AEM Forms à l’aide de l’API Trust Manager et de l’API Java. En outre, découvrez comment supprimer des informations d’identification à l’aide de l’API Trust Manager et de l’API Java.
uuid: b794428f-49bf-4a91-bc5f-d855881f4f38
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: bc06d9bd-af6c-47b1-b46f-aab990ef5816
role: Developer
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1117'
ht-degree: 11%

---


# Utilisation des informations d&#39;identification {#working-with-credentials}

**Les exemples et exemples de ce document ne concernent que l’environnement AEM Forms on JEE.**

**À propos du service d’informations d’identification**

Les informations d’identification contiennent les informations de clé privée dont vous avez besoin pour signer ou identifier des documents. Un certificat correspond aux informations de clé publique que vous configurez pour l’approbation. AEM Forms utilise des certificats et des informations d’identification à plusieurs fins :

* Les extensions d’Acrobat Reader DC utilisent des informations d’identification pour activer les droits Adobe Reader des documents PDF (Voir [Application des droits d’utilisation aux Documents PDF](/help/forms/developing/assigning-usage-rights.md#applying-usage-rights-to-pdf-documents).)
* Le service Signature accède aux certificats et aux informations d’identification lors d’opérations telles que la signature numérique de documents PDF. (Voir [Signature numérique de Documents PDF](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents).)

Vous pouvez interagir par programmation avec le service d’informations d’identification à l’aide de l’API Java Trust Manager. Vous pouvez effectuer les tâches suivantes :

* [Importation des informations d’identification à l’aide de l’API Trust Manager](credentials.md#importing-credentials-by-using-the-trust-manager-api)
* [Suppression des informations d’identification à l’aide de l’API Trust Manager](credentials.md#deleting-credentials-by-using-the-trust-manager-api)

>[!NOTE]
>
>Vous pouvez également importer et supprimer des certificats à l’aide d’Administration Console. (Voir [Aide à l&#39;administration.](https://www.adobe.com/go/learn_aemforms_admin_63))

## Importation des informations d’identification à l’aide de l’API Trust Manager {#importing-credentials-by-using-the-trust-manager-api}

Vous pouvez importer par programmation des informations d’identification dans AEM Forms à l’aide de l’API Trust Manager. Par exemple, vous pouvez importer des informations d’identification utilisées pour signer un document PDF. (Voir [Signature numérique de Documents PDF](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)).

Lors de l’importation d’informations d’identification, vous spécifiez un alias pour ces informations d’identification. L’alias est utilisé pour effectuer une opération Forms nécessitant des informations d’identification. Une fois importé, les informations d’identification peuvent être affichées dans Administration Console, comme le montre l’illustration suivante. Notez que l’alias des informations d’identification est *Secure*.

![ww_ww_truststore](assets/ww_ww_truststore.png)

>[!NOTE]
>
>Vous ne pouvez pas importer d’informations d’identification dans AEM Forms à l’aide de services Web.

### Résumé des étapes {#summary-of-steps}

Pour importer des informations d’identification dans AEM Forms, procédez comme suit :

1. Incluez des fichiers de projet.
1. Créez un client de service d’informations d’identification.
1. Référencez les informations d’identification.
1. Effectuez l’opération d’importation.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

Les fichiers JAR suivants doivent être ajoutés au chemin de classe de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-truststore-client.jar
* adobe-utilities.jar (requis si AEM Forms est déployé sur JBoss)
* jbossall-client.jar (requis si AEM Forms est déployé sur JBoss)

Pour plus d’informations sur l’emplacement de ces fichiers JAR, voir [Inclusion de fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Création d’un client de service d’informations d’identification**

Avant de pouvoir importer par programmation des informations d’identification dans AEM Forms, créez un client de service d’informations d’identification. Pour plus d’informations, voir [Définition des propriétés de connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

**Référence aux informations d’identification**

Référencez les informations d’identification que vous souhaitez importer dans AEM Forms. Le début rapide associé à cette section fait référence à un fichier P12 situé dans le système de fichiers.

**Exécution de l’opération d’importation**

Après avoir référencé les informations d’identification, importez-les dans AEM Forms. Si l’importation des informations d’identification échoue, une exception est levée. Lors de l’importation d’informations d’identification, vous spécifiez un alias pour ces informations d’identification.

**Voir également**

[Importation des informations d’identification à l’aide de l’API Java](credentials.md#import-credentials-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Débuts rapides de l’API Credential Service](/help/forms/developing/credential-service-java-api-quick.md#credential-service-java-api-quick-start-soap)

[Suppression des informations d’identification à l’aide de l’API Trust Manager](credentials.md#deleting-credentials-by-using-the-trust-manager-api)

### Importer des informations d’identification à l’aide de l’API Java {#import-credentials-using-the-java-api}

Importez des informations d’identification dans AEM Forms à l’aide de l’API Trust Manager (Java) :

1. Inclure les fichiers de projet

   Incluez des fichiers JAR client, tels que adobe-truststore-client.jar, dans le chemin de classe de votre projet Java.

1. Création d’un client de service d’informations d’identification

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `CredentialServiceClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`. 

1. Référence aux informations d’identification

   * Créez un objet `java.io.FileInputStream` en utilisant son constructeur. Transmettez une valeur de chaîne qui spécifie l’emplacement des informations d’identification.
   * Créez un objet `com.adobe.idp.Document` qui stocke les informations d’identification à l’aide du constructeur `com.adobe.idp.Document`. Transmettez l&#39;objet `java.io.FileInputStream` contenant les informations d&#39;identification au constructeur.

1. Exécution de l’opération d’importation

   * Créez un tableau de chaînes contenant un élément. Affectez la valeur `truststore.usage.type.sign` à l’élément.
   * Appelez la méthode `importCredential` de l’objet `CredentialServiceClient` et transmettez les valeurs suivantes :

      * Valeur de chaîne qui spécifie la valeur d’alias pour les informations d’identification.
      * Instance `com.adobe.idp.Document` qui stocke les informations d’identification.
      * Valeur de chaîne qui spécifie le mot de passe associé aux informations d’identification.
      * Tableau de chaînes contenant la valeur d’utilisation. Par exemple, vous pouvez spécifier cette valeur `truststore.usage.type.sign`. Pour importer des informations d’identification d’extension de Reader, spécifiez `truststore.usage.type.lcre`.

**Voir également**

[Importation des informations d’identification à l’aide de l’API Trust Manager](credentials.md#importing-credentials-by-using-the-trust-manager-api)

[Début rapide (mode SOAP) : Importation des informations d’identification à l’aide de l’API Java](/help/forms/developing/credential-service-java-api-quick.md#quick-start-soap-mode-importing-credentials-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Suppression des informations d’identification à l’aide de l’API Trust Manager {#deleting-credentials-by-using-the-trust-manager-api}

Vous pouvez supprimer par programmation des informations d’identification à l’aide de l’API Trust Manager. Lors de la suppression d’informations d’identification, vous spécifiez un alias correspondant aux informations d’identification. Une fois supprimée, les informations d’identification ne peuvent plus être utilisées pour effectuer une opération.

>[!NOTE]
>
>Vous ne pouvez pas supprimer d’informations d’identification dans AEM Forms à l’aide de services Web.

### Résumé des étapes {#summary_of_steps-1}

Pour supprimer des informations d’identification, procédez comme suit :

1. Incluez des fichiers de projet.
1. Créez un client de service d’informations d’identification.
1. Effectuez l’opération de suppression.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Les fichiers JAR suivants doivent être ajoutés au chemin de classe de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-truststore-client.jar
* adobe-utilities.jar (requis si AEM Forms est déployé sur JBoss)
* jbossall-client.jar (requis si AEM Forms est déployé sur JBoss)

Pour plus d’informations sur l’emplacement de ces fichiers JAR, voir [Inclusion de fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Création d’un client de service d’informations d’identification**

Avant de pouvoir supprimer par programmation des informations d’identification, créez un client de service d’intégration de données. Lors de la création d’un client de service, vous définissez les paramètres de connexion requis pour appeler un service. Pour plus d’informations, voir [Définition des propriétés de connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

**Exécution de l’opération de suppression**

Pour supprimer des informations d’identification, spécifiez l’alias correspondant aux informations d’identification. Si vous spécifiez un alias qui n’existe pas, une exception est générée.

**Voir également**

[Importation des informations d’identification à l’aide de l’API Java](credentials.md#import-credentials-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Importation des informations d’identification à l’aide de l’API Java](credentials.md#import-credentials-using-the-java-api)

### Suppression des informations d’identification à l’aide de l’API Java {#deleting-credentials-using-the-java-api}

Supprimez des informations d’identification d’AEM Forms à l’aide de l’API Trust Manager (Java) :

1. Inclure les fichiers de projet

   Incluez des fichiers JAR client, tels que adobe-truststore-client.jar, dans le chemin de classe de votre projet Java.

1. Création d’un client de service d’informations d’identification

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `CredentialServiceClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`. 

1. Exécution de l’opération de suppression

   Appelez la méthode `CredentialServiceClient` de l’objet `deleteCredential` et transmettez une valeur de chaîne qui spécifie la valeur d’alias.

**Voir également**

[Suppression des informations d’identification à l’aide de l’API Trust Manager](credentials.md#deleting-credentials-by-using-the-trust-manager-api)

[Début rapide (mode SOAP) : Suppression des informations d’identification à l’aide de l’API Java](/help/forms/developing/credential-service-java-api-quick.md#quick-start-soap-mode-deleting-credentials-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
