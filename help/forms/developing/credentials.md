---
title: Utilisation des informations d’identification
seo-title: Utilisation des informations d’identification
description: Importez des informations d’identification dans AEM Forms à l’aide de l’API Trust Manager et de l’API Java. En outre, découvrez comment supprimer des informations d’identification à l’aide de l’API Trust Manager et de l’API Java.
seo-description: Importez des informations d’identification dans AEM Forms à l’aide de l’API Trust Manager et de l’API Java. En outre, découvrez comment supprimer des informations d’identification à l’aide de l’API Trust Manager et de l’API Java.
uuid: b794428f-49bf-4a91-bc5f-d855881f4f38
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: bc06d9bd-af6c-47b1-b46f-aab990ef5816
role: Developer
exl-id: 1101c85a-6a90-471d-a7be-8d25765e84bf
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1116'
ht-degree: 11%

---

# Utilisation des informations d’identification {#working-with-credentials}

**Les exemples et les exemples de ce document sont réservés à l’environnement AEM Forms on JEE.**

**À propos du service d’identification**

Les informations d’identification contiennent les informations de clé privée dont vous avez besoin pour signer ou identifier des documents. Un certificat correspond aux informations de clé publique que vous configurez pour l’approbation. AEM Forms utilise des certificats et des informations d’identification à plusieurs fins :

* Les extensions d’Acrobat Reader DC utilisent des informations d’identification pour activer les droits Adobe Reader des documents PDF (Voir [Application de droits d’utilisation aux documents PDF](/help/forms/developing/assigning-usage-rights.md#applying-usage-rights-to-pdf-documents).)
* Le service Signature accède aux certificats et aux informations d’identification lors d’opérations telles que la signature numérique de documents PDF. (Voir [Signature numérique de documents PDF](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents).)

Vous pouvez interagir par programmation avec le service d’informations d’identification à l’aide de l’API Java Trust Manager. Vous pouvez effectuer les tâches suivantes :

* [Importation des informations d’identification à l’aide de l’API Trust Manager](credentials.md#importing-credentials-by-using-the-trust-manager-api)
* [Suppression d’informations d’identification à l’aide de l’API Trust Manager](credentials.md#deleting-credentials-by-using-the-trust-manager-api)

>[!NOTE]
>
>Vous pouvez également importer et supprimer des certificats à l’aide d’Administration Console. (Voir [Aide à l’administration.](https://www.adobe.com/go/learn_aemforms_admin_63))

## Importation des informations d’identification à l’aide de l’API Trust Manager {#importing-credentials-by-using-the-trust-manager-api}

Vous pouvez importer des informations d’identification par programmation dans AEM Forms à l’aide de l’API Trust Manager. Par exemple, vous pouvez importer les informations d’identification utilisées pour signer un document PDF. (Voir [Signature numérique de documents PDF](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)).

Lors de l’importation d’informations d’identification, vous spécifiez un alias pour ces informations. L’alias est utilisé pour effectuer une opération Forms nécessitant des informations d’identification. Une fois les informations d’identification importées, elles peuvent être affichées dans la console d’administration, comme illustré ci-dessous. Notez que l’alias des informations d’identification est *Secure*.

![www_www_truststore](assets/ww_ww_truststore.png)

>[!NOTE]
>
>Vous ne pouvez pas importer d’informations d’identification dans AEM Forms à l’aide de services web.

### Résumé des étapes {#summary-of-steps}

Pour importer des informations d’identification dans AEM Forms, procédez comme suit :

1. Inclure les fichiers de projet.
1. Créez un client de service d’identification.
1. Référencez les informations d’identification.
1. Effectuez l&#39;opération d&#39;import.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services web, veillez à inclure les fichiers proxy.

Les fichiers JAR suivants doivent être ajoutés au chemin d’accès aux classes de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-truststore-client.jar
* adobe-utility.jar (Obligatoire si AEM Forms est déployé sur JBoss)
* jbossall-client.jar (requis si AEM Forms est déployé sur JBoss)

Pour plus d’informations sur l’emplacement de ces fichiers JAR, voir [Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Création d’un client de service d’identification**

Avant de pouvoir importer des informations d’identification par programmation dans AEM Forms, créez un client de service d’informations d’identification. Pour plus d’informations, voir [Définition des propriétés de connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

**Référence des informations d’identification**

Référencez les informations d’identification que vous souhaitez importer dans AEM Forms. Le démarrage rapide associé à cette section fait référence à un fichier P12 situé dans le système de fichiers.

**Effectuer l&#39;opération d&#39;import**

Après avoir référencé les informations d’identification, importez-les dans AEM Forms. Si l’importation des informations d’identification échoue, une exception est générée. Lors de l’importation d’informations d’identification, vous spécifiez un alias pour ces informations.

**Voir également**

[Importation des informations d’identification à l’aide de l’API Java](credentials.md#import-credentials-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Démarrages rapides de l’API Credential Service](/help/forms/developing/credential-service-java-api-quick.md#credential-service-java-api-quick-start-soap)

[Suppression d’informations d’identification à l’aide de l’API Trust Manager](credentials.md#deleting-credentials-by-using-the-trust-manager-api)

### Importer des informations d’identification à l’aide de l’API Java {#import-credentials-using-the-java-api}

Importez des informations d’identification dans AEM Forms à l’aide de l’API Trust Manager (Java) :

1. Inclure les fichiers de projet

   Incluez les fichiers JAR client, tels que adobe-truststore-client.jar, dans le chemin de classe de votre projet Java.

1. Création d’un client de service d’identification

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `CredentialServiceClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`. 

1. Référence des informations d’identification

   * Créez un objet `java.io.FileInputStream` en utilisant son constructeur. Transmettez une valeur string qui spécifie l’emplacement des informations d’identification.
   * Créez un objet `com.adobe.idp.Document` qui stocke les informations d’identification à l’aide du constructeur `com.adobe.idp.Document`. Transmettez l’objet `java.io.FileInputStream` contenant les informations d’identification au constructeur.

1. Effectuer l&#39;opération d&#39;import

   * Créez un tableau de chaîne contenant un élément . Attribuez la valeur `truststore.usage.type.sign` à l’élément .
   * Appelez la méthode `importCredential` de l’objet `CredentialServiceClient` et transmettez les valeurs suivantes :

      * Une valeur string qui spécifie la valeur alias pour les informations d’identification.
      * Instance `com.adobe.idp.Document` qui stocke les informations d’identification.
      * Une valeur string qui spécifie le mot de passe associé aux informations d’identification.
      * Tableau de chaînes contenant la valeur d’utilisation. Par exemple, vous pouvez spécifier cette valeur `truststore.usage.type.sign`. Pour importer des informations d’identification d’extension de Reader, spécifiez `truststore.usage.type.lcre`.

**Voir également**

[Importation des informations d’identification à l’aide de l’API Trust Manager](credentials.md#importing-credentials-by-using-the-trust-manager-api)

[Démarrage rapide (mode SOAP) : Importation des informations d’identification à l’aide de l’API Java](/help/forms/developing/credential-service-java-api-quick.md#quick-start-soap-mode-importing-credentials-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Suppression des informations d’identification à l’aide de l’API Trust Manager {#deleting-credentials-by-using-the-trust-manager-api}

Vous pouvez supprimer des informations d’identification par programmation à l’aide de l’API Trust Manager. Lors de la suppression d’informations d’identification, vous spécifiez un alias correspondant à ces informations. Une fois supprimées, les informations d’identification ne peuvent pas être utilisées pour effectuer une opération.

>[!NOTE]
>
>Vous ne pouvez pas supprimer d’informations d’identification dans AEM Forms à l’aide de services web.

### Résumé des étapes {#summary_of_steps-1}

Pour supprimer des informations d’identification, procédez comme suit :

1. Inclure les fichiers de projet.
1. Créez un client de service d’identification.
1. Effectuez l’opération de suppression.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Les fichiers JAR suivants doivent être ajoutés au chemin d’accès aux classes de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-truststore-client.jar
* adobe-utility.jar (Obligatoire si AEM Forms est déployé sur JBoss)
* jbossall-client.jar (requis si AEM Forms est déployé sur JBoss)

Pour plus d’informations sur l’emplacement de ces fichiers JAR, voir [Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Création d’un client de service d’identification**

Avant de pouvoir supprimer des informations d’identification par programmation, créez un client de service d’intégration de données. Lors de la création d’un client de service, vous définissez les paramètres de connexion requis pour appeler un service. Pour plus d’informations, voir [Définition des propriétés de connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

**Exécution de l’opération de suppression**

Pour supprimer des informations d’identification, spécifiez l’alias correspondant aux informations d’identification. Si vous spécifiez un alias qui n’existe pas, une exception est générée.

**Voir également**

[Importation des informations d’identification à l’aide de l’API Java](credentials.md#import-credentials-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Importation des informations d’identification à l’aide de l’API Java](credentials.md#import-credentials-using-the-java-api)

### Suppression des informations d’identification à l’aide de l’API Java {#deleting-credentials-using-the-java-api}

Supprimez des informations d’identification d’AEM Forms à l’aide de l’API Trust Manager (Java) :

1. Inclure les fichiers de projet

   Incluez les fichiers JAR client, tels que adobe-truststore-client.jar, dans le chemin de classe de votre projet Java.

1. Création d’un client de service d’identification

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `CredentialServiceClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`. 

1. Exécution de l’opération de suppression

   Appelez la méthode `deleteCredential` de l’objet `CredentialServiceClient` et transmettez une valeur string qui spécifie la valeur d’alias.

**Voir également**

[Suppression d’informations d’identification à l’aide de l’API Trust Manager](credentials.md#deleting-credentials-by-using-the-trust-manager-api)

[Démarrage rapide (mode SOAP) : Suppression des informations d’identification à l’aide de l’API Java](/help/forms/developing/credential-service-java-api-quick.md#quick-start-soap-mode-deleting-credentials-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
