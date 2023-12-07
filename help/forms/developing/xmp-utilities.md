---
title: Utiliser XMP Utilities
description: Utilisez les API Java et Web Service XMP Utilities pour importer des métadonnées XMP par programmation dans un document PDF et récupérer et enregistrer les métadonnées d’un document PDF.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: cff65f74-ba95-438e-88a4-5ec7d22aafba
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '1380'
ht-degree: 98%

---

# Utiliser XMP Utilities {#working-with-xmp-utilities}

**Les exemples et les échantillons de ce document sont réservés à l’environnement AEM Forms sur JEE.**

**À propos du service XMP Utilities**

Les documents PDF contiennent des métadonnées. Ce sont des informations sur le document qui se distinguent du contenu du document, telles que le texte et les graphiques. Adobe Extensible Metadata Platform (XMP) est un standard de gestion des métadonnées de document.

Le service XMP Utilities peut récupérer et enregistrer des métadonnées XMP à partir de documents PDF, et importer des métadonnées dans des documents PDF.

Vous pouvez accomplir les tâches suivantes à l’aide du service XMP Utilities :

* Importer des métadonnées dans des documents PDF. (Voir [Importer des métadonnées dans des documents PDF](xmp-utilities.md#importing-metadata-into-pdf-documents).)
* Exporter des métadonnées à partir de documents PDF. (Voir [Exporter des métadonnées à partir de documents PDF](xmp-utilities.md#exporting-metadata-from-pdf-documents).)

>[!NOTE]
>
>Pour plus d’informations sur le service XMP Utilities, voir [Références des services pour AEM Forms](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

## Importer des métadonnées dans des documents PDF {#importing-metadata-into-pdf-documents}

Vous pouvez utiliser les API Java et Web Service XMP Utilities pour importer des métadonnées XMP par programmation dans un document PDF. Les métadonnées fournissent des informations sur un document PDF, comme l’auteur du document et les mots-clés associés au document. Les métadonnées peuvent se trouver dans la boîte de dialogue Propriétés du document, comme illustré ci-dessous.

![ww_ww_metadatadialog](assets/ww_ww_metadatadialog.png)

Pour importer des métadonnées par programmation dans un document PDF, vous pouvez utiliser un document XML existant qui spécifie les valeurs de métadonnées ou vous pouvez utiliser un objet de type `XMPUtilityMetadata`. (Voir [Référence de l’API AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).)

>[!NOTE]
>
>Cette section explique comment utiliser un document XML pour importer des métadonnées dans un document PDF.

Le code XML suivant contient des valeurs de métadonnées qui correspondent à l’illustration précédente. Par exemple, notez les éléments en gras qui spécifient les mots-clés.

```xml
 <?xpacket begin="?" id="W5M0MpCehiHzreSzNTczkc9d"?>
 <x:xmpmeta xmlns:x="adobe:ns:meta/" x:xmptk="Adobe XMP Core 4.2-jc015 52.349034, 2008 Jun 20 00:30:39-PDT (debug)">
       <rdf:RDF xmlns:rdf="https://www.w3.org/1999/02/22-rdf-syntax-ns#">
          <rdf:Description rdf:about=""
                xmlns:xmp="https://ns.adobe.com/xap/1.0/">
             <xmp:MetadataDate>2008-10-22T10:52:21-04:00</xmp:MetadataDate>
             <xmp:CreatorTool>AEM Forms</xmp:CreatorTool>
             <xmp:ModifyDate>2008-10-22T10:52:21-04:00</xmp:ModifyDate>
             <xmp:CreateDate>2008-02-13T11:00:18-05:00</xmp:CreateDate>
          </rdf:Description>
          <rdf:Description rdf:about=""
                xmlns:pdf="https://ns.adobe.com/pdf/1.3/">
             <pdf:Producer>AEM Forms</pdf:Producer>
             <pdf:Keywords>keyword1, keyword2, keyword3,keyword4</pdf:Keywords>
          </rdf:Description>
          <rdf:Description rdf:about=""
                xmlns:xmpMM="https://ns.adobe.com/xap/1.0/mm/">
             <xmpMM:DocumentID>uuid:1cce1f84-331e-4d8d-8538-15441c271dd7</xmpMM:DocumentID>
             <xmpMM:InstanceID>uuid:cdda0ca6-7c91-4771-9dc9-796c8fe59350</xmpMM:InstanceID>
          </rdf:Description>
          <rdf:Description rdf:about=""
                >
             <dc:format>application/pdf</dc:format>
             <dc:description>
                <rdf:Alt>
                   <rdf:li xml:lang="x-default">Adobe Designer Sample</rdf:li>
                </rdf:Alt>
             </dc:description>
             <dc:title>
                <rdf:Alt>
                   <rdf:li xml:lang="x-default">Grant Application</rdf:li>
                </rdf:Alt>
             </dc:title>
             <dc:creator>
                <rdf:Seq>
                   <rdf:li>Tony Blue</rdf:li>
                </rdf:Seq>
             </dc:creator>
             <dc:subject>
                <rdf:Bag>
                   <rdf:li>keyword1</rdf:li>
                   <rdf:li>keyword2</rdf:li>
                   <rdf:li>keyword3</rdf:li>
                   <rdf:li>keyword4</rdf:li>
                </rdf:Bag>
             </dc:subject>
          </rdf:Description>
          <rdf:Description rdf:about=""
                xmlns:desc="https://ns.adobe.com/xfa/promoted-desc/">
             <desc:version rdf:parseType="Resource">
                <rdf:value>1.0</rdf:value>
                <desc:ref>/template/subform[1]</desc:ref>
             </desc:version>
             <desc:contact rdf:parseType="Resource">
                <rdf:value>Adobe Systems Incorporated</rdf:value>
                <desc:ref>/template/subform[1]</desc:ref>
             </desc:contact>
          </rdf:Description>
       </rdf:RDF>
 </x:xmpmeta>
```

>[!NOTE]
>
>Pour plus d’informations sur le service XMP Utilities, voir [Références des services pour AEM Forms](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

### Résumé des étapes {#summary-of-steps}

Pour importer des métadonnées XMP dans un document PDF, procédez comme suit :

1. Incluez les fichiers de projet.
1. Créez un client XMPUtilityService.
1. Appelez l’opération d’importation de métadonnées XMP.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

**Créer un client XMPUtilityService**

Avant d’effectuer une opération XMP Utilities par programmation, vous devez créer un client XMPUtilityService. Avec l’API Java, vous pouvez y parvenir en créant un objet `XMPUtilityServiceClient`. Avec l’API Web Service, vous pouvez y parvenir en utilisant un objet `XMPUtilityServiceService`.

**Appeler l’opération d’importation de métadonnées XMP**

Après avoir créé le client de service, vous pouvez appeler l’une des opérations d’importation de métadonnées XMP pour importer les métadonnées XMP dans le document PDF spécifié.

**Voir également**

[Importer des métadonnées XMP à l’aide de l’API Java](xmp-utilities.md#import-xmp-metadata-using-the-java-api)

[Importer des métadonnées XMP à l’aide de l’API Web Service](xmp-utilities.md#importing-xmp-metadata-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Importer des métadonnées XMP à l’aide de l’API Java {#import-xmp-metadata-using-the-java-api}

Importez des métadonnées XMP à l’aide de l’API XMP Utilities (Java) :

1. Inclure les fichiers du projet

   Incluez les fichiers JAR clients, tels qu’adobe-livecycle-client.jar, dans le chemin d’accès aux classes du projet Java.

   >[!NOTE]
   >
   >Le fichier adobe-pdfutility-client.jar contient des classes qui vous permettent d’appeler le service XMP Utilities par programmation.

1. Créer un client XMPUtilityService

   Créez un objet `XMPUtilityServiceClient` en utilisant son constructeur et en transmettant un objet `ServiceClientFactory` contenant des propriétés de connexion.

1. Appeler l’opération d’importation de métadonnées XMP

   Pour modifier les métadonnées XMP, appelez l’une des méthodes suivantes de l’objet `XMPUtilityServiceClient` : `importMetadata` ou `importXMP`.

   Si vous utilisez la méthode `importMetadata`, transmettez les valeurs suivantes :

   * Objet `com.adobe.idp.Document` représentant le fichier PDF.
   * Objet `XMPUtilityMetadata` contenant les métadonnées à importer.

   Si vous utilisez la méthode `importXMP`, transmettez les valeurs suivantes :

   * Objet `com.adobe.idp.Document` représentant le fichier PDF.
   * Objet `com.adobe.idp.Document` représentant un fichier XML qui contient les métadonnées à importer.

   Dans les deux cas, la valeur renvoyée est un objet `com.adobe.idp.Document` qui représente le fichier PDF avec les métadonnées nouvellement importées. Vous pouvez ensuite enregistrer cet objet sur le disque.

**Voir également**

[Importer des métadonnées dans des documents PDF](xmp-utilities.md#importing-metadata-into-pdf-documents)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Importer des métadonnées XMP à l’aide de l’API Web Service {#importing-xmp-metadata-using-the-web-service-api}

Pour importer des métadonnées XMP par programmation à l’aide de l’API Web Service Utilities, effectuez les tâches suivantes :

1. Inclure les fichiers du projet

   * Créez un assemblage client Microsoft .NET qui utilise le fichier WSDL du service XMP Utilities. (Voir [Appeler AEM Forms à l’aide du codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding).)
   * Référencez l’assemblage client Microsoft .NET. (Voir [Créer un assemblage client .NET à l’aide du codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding).)

1. Créer un client XMPUtilityService

   Créez un objet `XMPUtilityServiceService` en utilisant le constructeur de classe proxy.

1. Appeler l’opération d’importation de métadonnées XMP

   Pour modifier les métadonnées XMP, appelez l’une des méthodes suivantes de l’objet `XMPUtilityServiceService` : `importMetadata` ou `importXMP`.

   Si vous utilisez la méthode `importMetadata`, transmettez les valeurs suivantes :

   * Objet `BLOB` représentant le fichier PDF.
   * Objet `XMPUtilityMetadata` contenant les métadonnées à importer.

   Si vous utilisez la méthode `importXMP`, transmettez les valeurs suivantes :

   * Objet `BLOB` représentant le fichier PDF.
   * Objet `BLOB` représentant un fichier XML qui contient les métadonnées à importer.

   Dans les deux cas, la valeur renvoyée est un objet `BLOB` qui représente le fichier PDF avec les métadonnées nouvellement importées. Vous pouvez ensuite enregistrer cet objet sur le disque.

**Voir également**

[Importer des métadonnées dans des documents PDF](xmp-utilities.md#importing-metadata-into-pdf-documents)

<!--REVIEW: [Quick Start (Base64): Importing XMP metadata using the web service API](unresolvedlink-lc-qs-xmp-utilities-xu.xml#ws624e3cba99b79e12e69a9941333732bac8-7be8.2)-->

[Appeler AEM Forms en utilisant le codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Créer un assemblage client .NET utilisant le codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## Exporter des métadonnées à partir de documents PDF {#exporting-metadata-from-pdf-documents}

Vous pouvez utiliser les API Java et Web Service XMP Utilities pour récupérer et enregistrer des métadonnées XMP par programmation à partir d’un document PDF.

>[!NOTE]
>
>Pour plus d’informations sur le service XMP Utilities, voir [Références des services pour AEM Forms](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

### Résumé des étapes {#summary_of_steps-1}

Pour exporter les métadonnées XMP d’un document PDF, procédez comme suit :

1. Incluez les fichiers de projet.
1. Créez un client XMPUtilityService.
1. Appelez l’opération d’exportation des métadonnées XMP.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

**Créer un client XMPUtilityService**

Avant d’effectuer une opération XMP Utilities par programmation, vous devez créer un client XMPUtilityService. Avec l’API Java, vous pouvez y parvenir en créant un objet `XMPUtilityServiceClient`. Avec l’API Web Service, cette opération s’effectue à l’aide d’un objet `XMPUtilityServiceService`.

**Appeler l’opération d’exportation des métadonnées XMP**

Après avoir créé le client de service, vous pouvez appeler l’une des opérations d’exportation de métadonnées XMP, qui peut être utilisée pour examiner les métadonnées XMP ou les enregistrer sur le disque.

**Voir également**

[Importer des métadonnées XMP à l’aide de l’API Java](xmp-utilities.md#import-xmp-metadata-using-the-java-api)

[Importer des métadonnées XMP à l’aide de l’API Web Service](xmp-utilities.md#importing-xmp-metadata-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Exporter des métadonnées XMP à l’aide de l’API Java {#export-xmp-metadata-using-the-java-api}

Exportez des métadonnées XMP à l’aide de l’API XMP Utilities (Java) :

1. Inclure les fichiers du projet

   Incluez les fichiers JAR clients, tels qu’adobe-livecycle-client.jar, dans le chemin d’accès aux classes du projet Java.

   >[!NOTE]
   >
   >Le fichier adobe-pdfutility-client.jar contient des classes qui vous permettent d’appeler le service XMP Utility par programmation.

1. Créer un client XMPUtilityService

   Créez un objet `XMPUtilityServiceClient` en utilisant son constructeur et en transmettant un objet `ServiceClientFactory` contenant des propriétés de connexion.

1. Appeler l’opération d’importation de métadonnées XMP

   Pour examiner les métadonnées XMP, appelez la méthode `exportMetadata` de l’objet `XMPUtilityServiceClient` et transmettez un objet `com.adobe.idp.Document` qui représente le fichier PDF. La méthode renvoie un objet `XMPUtilityMetadata` contenant les métadonnées récupérées.

   Pour récupérer et enregistrer les métadonnées XMP, appelez la méthode `exportXMP` de l’objet `XMPUtilityServiceClient` et transmettez un objet `com.adobe.idp.Document` qui représente le fichier PDF. La méthode renvoie un objet `com.adobe.idp.Document` qui contient les métadonnées récupérées, que vous pouvez ensuite enregistrer sur le disque en tant que fichier XML.

**Voir également**

[Exporter des métadonnées à partir de documents PDF](xmp-utilities.md#exporting-metadata-from-pdf-documents)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Exporter des métadonnées XMP à l’aide de l’API Web Service {#export-xmp-metadata-using-the-web-service-api}

Exportez des métadonnées XMP à l’aide de l’API XMP Utilities (Web Service) :

1. Inclure les fichiers du projet

   * Créez un assemblage client Microsoft .NET qui utilise le fichier WSDL du service XMP Utilities.
   * Référencez l’assemblage client Microsoft .NET.

1. Créer un client XMPUtilityService

   Créez un objet `XMPUtilityServiceService` en utilisant le constructeur de classe proxy.

1. Appeler l’opération d’importation de métadonnées XMP

   Pour examiner les métadonnées XMP, appelez la méthode `exportMetadata` de l’objet `XMPUtilityServiceClient` et transmettez un objet `BLOB` qui représente le fichier PDF. La méthode renvoie un objet `XMPUtilityMetadata` contenant les métadonnées récupérées.

   Pour récupérer et enregistrer les métadonnées XMP, appelez la méthode `exportXMP` de l’objet `XMPUtilityServiceClient` et transmettez un objet `BLOB` qui représente le fichier PDF. La méthode renvoie un objet `BLOB` qui contient les métadonnées récupérées, que vous pouvez ensuite enregistrer sur le disque en tant que fichier XML.

**Voir également**

[Exporter des métadonnées à partir de documents PDF](xmp-utilities.md#exporting-metadata-from-pdf-documents)

[Appeler AEM Forms en utilisant le codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Créer un assemblage client .NET utilisant le codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)
