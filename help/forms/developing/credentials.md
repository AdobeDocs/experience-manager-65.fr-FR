---
title: Utiliser des informations d’identification
description: Importez des informations d’identification dans AEM Forms à l’aide des API Trust Manager et Java. Découvrez également comment supprimer des informations d’identification à l’aide de l’API Trust Manager et de l’API Java.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 1101c85a-6a90-471d-a7be-8d25765e84bf
solution: Experience Manager, Experience Manager Forms
source-git-commit: 872e2de411f51b5f0b26a2ff47cb49f01313d39f
workflow-type: tm+mt
source-wordcount: '1077'
ht-degree: 100%

---

# Utiliser des informations d’identification {#working-with-credentials}

**Les exemples et les échantillons de ce document sont réservés à l’environnement AEM Forms sur JEE.**

**À propos du service d’identification**

Les informations d’identification contiennent les informations de clé privée dont vous avez besoin pour signer ou identifier des documents. Un certificat correspond aux informations de clé publique que vous configurez pour l’approbation. AEM Forms utilise des certificats et des informations d’identification à plusieurs fins :

* Les extensions d’Acrobat Reader DC utilisent des informations d’identification pour activer les droits Adobe Reader des documents PDF (Consultez la section [Appliquer des droits d’utilisation aux documents PDF](/help/forms/developing/assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)).
* Le service Signature accède aux certificats et aux informations d’identification lors d’opérations telles que la signature numérique de documents PDF. (Consultez la section [Signer numériquement des documents PDF](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)).

Vous pouvez interagir par programmation avec le service d’identification à l’aide de l’API Java Trust Manager. Vous pouvez effectuer les tâches suivantes :

* [Importer des informations d’identification à l’aide de l’API Trust Manager](credentials.md#importing-credentials-by-using-the-trust-manager-api)
* [Supprimer des informations d’identification à l’aide de l’API Trust Manager](credentials.md#deleting-credentials-by-using-the-trust-manager-api)

>[!NOTE]
>
>Vous pouvez également importer et supprimer des certificats à l’aide de la console dʼadministration. (Consultez la section [Aide d’administration](https://www.adobe.com/go/learn_aemforms_admin_63_fr)).

## Importer des informations d’identification à l’aide de l’API Trust Manager {#importing-credentials-by-using-the-trust-manager-api}

Vous pouvez importer des informations d’identification par programmation dans AEM Forms à l’aide de l’API Trust Manager. Par exemple, vous pouvez importer des informations d’identification nécessaires pour signer un document PDF. (Consultez la section [Signer numériquement des documents PDF](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)).

Lors de l’importation d’informations d’identification, vous spécifiez un alias pour ces informations. Il est utilisé pour effectuer une opération dans AEM Forms nécessitant des informations d’identification. Une fois les informations d’identification importées, elles peuvent être affichées dans la console d’administration, comme illustré ci-dessous. Notez que l’alias des informations d’identification est *Sécurisé*.

![www_www_truststore](assets/ww_ww_truststore.png)

>[!NOTE]
>
>Vous ne pouvez pas importer d’informations d’identification dans AEM Forms à l’aide de services web.

### Résumé des étapes {#summary-of-steps}

Pour importer des informations d’identification dans AEM Forms, procédez comme suit :

1. Incluez les fichiers de projet.
1. Créez un client de service d’identification.
1. Référencez les informations d’identification.
1. Effectuez lʼopération dʼimportation.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services web, veillez à inclure les fichiers proxy.

Les fichiers JAR suivants doivent être ajoutés au chemin d’accès aux classes de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-truststore-client.jar
* adobe-utilities.jar (Requis si AEM Forms est déployé sur JBoss)
* jbossall-client.jar (Requis si AEM Forms est déployé sur JBoss)

Pour plus d’informations sur l’emplacement de ces fichiers JAR, consultez la section [Inclure des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Créer un client de service d’identification**

Avant de pouvoir importer des informations d’identification par programmation dans AEM Forms, vous devez créer un client de service d’identification. Pour plus d’informations, consultez la section [Définir des propriétés de connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

**Référencer les informations d’identification**

Référencez les informations d’identification à importer dans AEM Forms. Le démarrage rapide correspondant à cette section fait référence à un fichier P12 situé dans le système de fichiers.

**Effectuer lʼopération dʼimportation**

Après avoir référencé les informations d’identification, importez-les dans AEM Forms. Si l’importation des informations d’identification échoue, une exception est générée. Lors de l’importation d’informations d’identification, vous spécifiez un alias pour ces informations.

**Voir également**

[Importer des informations d’identification à l’aide de l’API Java](credentials.md#import-credentials-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Didacticiels de mise en route de l’API Credential Service](/help/forms/developing/credential-service-java-api-quick.md#credential-service-java-api-quick-start-soap)

[Supprimer des informations d’identification à l’aide de l’API Trust Manager](credentials.md#deleting-credentials-by-using-the-trust-manager-api)

### Importer des informations d’identification à l’aide de l’API Java {#import-credentials-using-the-java-api}

Importez des informations d’identification dans AEM Forms à l’aide de l’API Trust Manager (Java) :

1. Inclure les fichiers du projet

   Incluez les fichiers JAR du client, tels que adobe-truststore-client.jar, dans le chemin d’accès aux classes de votre projet Java.

1. Créer un client de service d’identification

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `CredentialServiceClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`. 

1. Référencer des informations d’identification

   * Créez un objet `java.io.FileInputStream` en utilisant son constructeur. Transmettez une valeur de chaîne qui spécifie l’emplacement des informations d’identification.
   * Créez un objet `com.adobe.idp.Document` qui stocke les informations d’identification à l’aide du constructeur `com.adobe.idp.Document`. Transmettez lʼobjet `java.io.FileInputStream` contenant les informations d’identification au constructeur.

1. Réaliser lʼopération dʼimportation

   * Créez un tableau de chaîne qui contient un élément. Attribuer la valeur `truststore.usage.type.sign` à l’élément.
   * Appelez la méthode `importCredential` de lʼobjet `CredentialServiceClient` et transmettez les valeurs suivantes :

      * Une valeur de chaîne qui spécifie la valeur de lʼalias pour les informations dʼidentification.
      * Lʼinstance `com.adobe.idp.Document` qui stocke les informations d’identification.
      * Une valeur de chaîne qui spécifie le mot de passe associé aux informations d’identification.
      * Le tableau de chaînes qui contient la valeur d’utilisation. Par exemple, vous pouvez spécifier la valeur suivante `truststore.usage.type.sign`. Pour importer des informations d’identification de Reader Extension, spécifiez `truststore.usage.type.lcre`.

**Voir également**

[Importer des informations d’identification à l’aide de l’API Trust Manager](credentials.md#importing-credentials-by-using-the-trust-manager-api)

[Didacticiel de mise en route (mode SOAP) : importer des informations d’identification à l’aide de l’API Java](/help/forms/developing/credential-service-java-api-quick.md#quick-start-soap-mode-importing-credentials-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Supprimer des informations d’identification à l’aide de l’API Trust Manager {#deleting-credentials-by-using-the-trust-manager-api}

Vous pouvez supprimer des informations d’identification par programmation à l’aide de l’API Trust Manager. Lors de la suppression d’informations d’identification, vous devez spécifier un alias qui correspond à ces informations. Une fois supprimées, les informations d’identification ne peuvent pas être utilisées pour réaliser une opération.

>[!NOTE]
>
>Vous ne pouvez pas supprimer d’informations d’identification dans AEM Forms à l’aide de services web.

### Résumé des étapes {#summary_of_steps-1}

Pour supprimer des informations d’identification, procédez comme suit :

1. Incluez les fichiers de projet.
1. Créez un client de service d’identification.
1. Effectuez l’opération de suppression.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Les fichiers JAR suivants doivent être ajoutés au chemin d’accès aux classes de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-truststore-client.jar
* adobe-utilities.jar (Requis si AEM Forms est déployé sur JBoss)
* jbossall-client.jar (Requis si AEM Forms est déployé sur JBoss)

Pour plus d’informations sur l’emplacement de ces fichiers JAR, consultez la section [Inclure des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Créer un client de service d’identification**

Avant de pouvoir supprimer des informations d’identification par programmation, créez un client de service d’intégration de données. Lors de la création d’un client de service, vous définissez les paramètres de connexion requis pour appeler un service. Pour plus d’informations, voir [Définition des propriétés de connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

**Exécuter l’opération de suppression**

Pour supprimer des informations d’identification, indiquez l’alias correspondant à ces informations d’identification. Si vous indiquez un alias qui n’existe pas, une exception est générée.

**Voir également**

[Importer des informations d’identification à l’aide de l’API Java](credentials.md#import-credentials-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Importer des informations d’identification à l’aide de l’API Java](credentials.md#import-credentials-using-the-java-api)

### Supprimer des informations d’identification à l’aide de l’API Java {#deleting-credentials-using-the-java-api}

Supprimez des informations d’identification d’AEM Forms à l’aide de l’API Trust Manager (Java) :

1. Inclure les fichiers du projet

   Incluez les fichiers JAR du client, tels que adobe-truststore-client.jar, dans le chemin d’accès aux classes de votre projet Java.

1. Créer un client de service d’identification

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `CredentialServiceClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`. 

1. Exécuter l’opération de suppression

   Appelez la méthode `deleteCredential` de l’objet `CredentialServiceClient` et transmettez une valeur de chaîne qui spécifie la valeur d’alias.

**Voir également**

[Supprimer des informations d’identification à l’aide de l’API Trust Manager](credentials.md#deleting-credentials-by-using-the-trust-manager-api)

[Démarrage rapide (mode SOAP) : supprimer des informations d’identification à l’aide de l’API Java](/help/forms/developing/credential-service-java-api-quick.md#quick-start-soap-mode-deleting-credentials-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
