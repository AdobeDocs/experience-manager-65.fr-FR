---
title: Utilisation des utilitaires XMP
seo-title: Utilisation des utilitaires XMP
description: Utilisez les API Javascript et Web Service de XMP Utilitaires pour importer par programmation XMP métadonnées dans un document PDF et récupérer et enregistrer des métadonnées de XMP à partir d’un document PDF.
seo-description: Utilisez les API Javascript et Web Service de XMP Utilitaires pour importer par programmation XMP métadonnées dans un document PDF et récupérer et enregistrer des métadonnées de XMP à partir d’un document PDF.
uuid: 90ce6cef-efe1-456a-8e0c-5ba90249dda0
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 01d5677f-5c87-4a6e-987b-8eda9acc0b27
role: Developer
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1438'
ht-degree: 3%

---


# Utilisation de XMP Utilitaires {#working-with-xmp-utilities}

**Les exemples et exemples de ce document ne concernent que l’environnement AEM Forms on JEE.**

**À propos du service XMP Utilities**

Les documents PDF contiennent des métadonnées, c’est-à-dire des informations sur le document qui se distinguent du contenu du document, telles que du texte et des graphiques. Adobe Extensible Metadata Platform (XMP) est une norme de gestion des métadonnées de document.

Le service Utilitaires XMP peut récupérer et enregistrer XMP métadonnées des documents PDF, et importer des métadonnées de XMP dans des documents PDF.

Vous pouvez exécuter ces tâches à l’aide du service XMP Utilitaires :

* Importez des métadonnées dans des documents PDF. (Voir [Importation de métadonnées dans des Documents PDF](xmp-utilities.md#importing-metadata-into-pdf-documents).)
* Exportez des métadonnées à partir de documents PDF. (Voir [Exportation de métadonnées à partir de Documents PDF](xmp-utilities.md#exporting-metadata-from-pdf-documents).)

>[!NOTE]
>
>Pour plus d&#39;informations sur le service XMP Utilities, voir [Guide de référence des services pour AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Importation de métadonnées dans des Documents PDF {#importing-metadata-into-pdf-documents}

Vous pouvez utiliser les API XMP Utilitaires Java et de service Web pour importer par programmation XMP métadonnées dans un document PDF. Les métadonnées fournissent des informations sur un document PDF tel que l’auteur du document et les mots-clés associés au document. Les métadonnées se trouvent dans la boîte de dialogue Propriétés du Document du document, comme le montre l’illustration suivante.

![ww_ww_metadatadialog](assets/ww_ww_metadatadialog.png)

Pour importer par programmation des métadonnées dans un document PDF, vous pouvez utiliser un document XML existant qui spécifie les valeurs de métadonnées ou vous pouvez utiliser un objet de type `XMPUtilityMetadata`. (Voir [Référence de l’API AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).)

>[!NOTE]
>
>Cette section explique comment utiliser un document XML pour importer des métadonnées dans un document PDF.

Le code XML suivant contient des valeurs de métadonnées correspondant à l’illustration précédente. Par exemple, notez les éléments en gras, qui spécifient les mots-clés.

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
>Pour plus d&#39;informations sur le service XMP Utilities, voir [Guide de référence des services pour AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary-of-steps}

Pour importer XMP métadonnées dans un document PDF, procédez comme suit :

1. Incluez des fichiers de projet.
1. Créez un client XMPUtilityService.
1. Appelez l’opération d’importation des métadonnées XMP.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

**Création d’un client XMPUtilityService**

Avant de pouvoir exécuter une opération XMP Utilitaires par programmation, vous devez créer un client XMPUtilityService. Avec l’API Java, cela se fait en créant un objet `XMPUtilityServiceClient`. Avec l’API du service Web, cela se fait en utilisant un objet `XMPUtilityServiceService`.

**Appeler l’opération d’importation des métadonnées XMP**

Après avoir créé le client de service, vous pouvez appeler l’une des opérations d’importation de métadonnées XMP pour importer les métadonnées XMP dans le document PDF spécifié.

**Voir également**

[Importer des métadonnées XMP à l’aide de l’API Java](xmp-utilities.md#import-xmp-metadata-using-the-java-api)

[Importation de métadonnées XMP à l’aide de l’API du service Web](xmp-utilities.md#importing-xmp-metadata-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Importer XMP métadonnées à l’aide de l’API Java {#import-xmp-metadata-using-the-java-api}

Importez XMP métadonnées à l’aide de l’API XMP Utilities (Java) :

1. Inclure les fichiers de projet

   Incluez des fichiers JAR client, tels que adobe-pdfutility-client.jar, dans le chemin de classe de votre projet Java.

   >[!NOTE]
   >
   >Le fichier adobe-pdfutility-client.jar contient des classes qui vous permettent d’appeler par programmation le service XMP Utilitaires.

1. Création d’un client XMPUtilityService

   Créez un objet `XMPUtilityServiceClient` en utilisant son constructeur et en transmettant un objet `ServiceClientFactory` contenant des propriétés de connexion.

1. Appeler l’opération d’importation des métadonnées XMP

   Pour modifier les métadonnées XMP, appelez la méthode `XMPUtilityServiceClient` de l’objet `importMetadata` ou sa méthode `importXMP`.

   Si vous utilisez la méthode `importMetadata`, transmettez les valeurs suivantes :

   * Objet `com.adobe.idp.Document` représentant le fichier PDF.
   * Objet `XMPUtilityMetadata` contenant les métadonnées à importer.

   Si vous utilisez la méthode `importXMP`, transmettez les valeurs suivantes :

   * Objet `com.adobe.idp.Document` représentant le fichier PDF.
   * Objet `com.adobe.idp.Document` représentant un fichier XML contenant les métadonnées à importer.

   Dans les deux cas, la valeur renvoyée est un objet `com.adobe.idp.Document` qui représente le fichier PDF avec les métadonnées nouvellement importées. Vous pouvez ensuite enregistrer cet objet sur le disque.

**Voir également**

[Importation de métadonnées dans des Documents PDF](xmp-utilities.md#importing-metadata-into-pdf-documents)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Importation de XMP métadonnées à l’aide de l’API du service Web {#importing-xmp-metadata-using-the-web-service-api}

Pour importer par programmation des métadonnées XMP à l’aide de l’API du service Web XMP Utilities, effectuez les tâches suivantes :

1. Inclure les fichiers de projet

   * Créez un assembly client Microsoft .NET qui consomme le fichier WSDL du service XMP Utilities. (Voir [Appel d’AEM Forms à l’aide de l’encodage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding).)
   * Référencez l&#39;assembly client Microsoft .NET. (Voir [Création d&#39;un assembly client .NET utilisant l&#39;encodage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding).)

1. Création d’un client XMPUtilityService

   Créez un objet `XMPUtilityServiceService` en utilisant votre constructeur de classe proxy.

1. Appeler l’opération d’importation des métadonnées XMP

   Pour modifier les métadonnées XMP, appelez la méthode `XMPUtilityServiceService` de l’objet `importMetadata` ou sa méthode `importXMP`.

   Si vous utilisez la méthode `importMetadata`, transmettez les valeurs suivantes :

   * Objet `BLOB` représentant le fichier PDF.
   * Objet `XMPUtilityMetadata` contenant les métadonnées à importer.

   Si vous utilisez la méthode `importXMP`, transmettez les valeurs suivantes :

   * Objet `BLOB` représentant le fichier PDF.
   * Objet `BLOB` représentant un fichier XML contenant les métadonnées à importer.

   Dans les deux cas, la valeur renvoyée est un objet `BLOB` qui représente le fichier PDF avec les métadonnées nouvellement importées. Vous pouvez ensuite enregistrer cet objet sur le disque.

**Voir également**

[Importation de métadonnées dans des Documents PDF](xmp-utilities.md#importing-metadata-into-pdf-documents)

<!--REVIEW: [Quick Start (Base64): Importing XMP metadata using the web service API](unresolvedlink-lc-qs-xmp-utilities-xu.xml#ws624e3cba99b79e12e69a9941333732bac8-7be8.2)-->

[Appel de AEM Forms à l’aide du codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Création d&#39;un assembly client .NET utilisant le codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## Exportation de métadonnées à partir de Documents PDF {#exporting-metadata-from-pdf-documents}

Vous pouvez utiliser les API Java et Web Utilities de XMP pour récupérer et enregistrer par programmation des métadonnées XMP à partir d’un document PDF.

>[!NOTE]
>
>Pour plus d&#39;informations sur le service XMP Utilities, voir [Guide de référence des services pour AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary_of_steps-1}

Pour exporter XMP métadonnées d’un document PDF, procédez comme suit :

1. Incluez des fichiers de projet.
1. Créez un client XMPUtilityService.
1. Appelez l’opération d’exportation des métadonnées XMP.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

**Création d’un client XMPUtilityService**

Avant de pouvoir exécuter une opération XMP Utilitaires par programmation, vous devez créer un client XMPUtilityService. Avec l&#39;API Java, cela est réalisé en créant un objet `XMPUtilityServiceClient`. Avec l’API du service Web, cela se fait à l’aide d’un objet `XMPUtilityServiceService`.

**Appeler l’opération d’exportation des métadonnées XMP**

Après avoir créé le client de service, vous pouvez appeler l’une des opérations d’exportation de métadonnées XMP, qui peut être utilisée pour examiner les métadonnées XMP ou les enregistrer sur le disque.

**Voir également**

[Importer des métadonnées XMP à l’aide de l’API Java](xmp-utilities.md#import-xmp-metadata-using-the-java-api)

[Importation de métadonnées XMP à l’aide de l’API du service Web](xmp-utilities.md#importing-xmp-metadata-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Exporter XMP métadonnées à l’aide de l’API Java {#export-xmp-metadata-using-the-java-api}

Exportez XMP métadonnées à l’aide de l’API XMP Utilities (Java) :

1. Inclure les fichiers de projet

   Incluez des fichiers JAR client, tels que adobe-pdfutility-client.jar, dans le chemin de classe de votre projet Java.

   >[!NOTE]
   >
   >Le fichier adobe-pdfutility-client.jar contient des classes qui vous permettent d’appeler par programmation le service XMP Utility.

1. Création d’un client XMPUtilityService

   Créez un objet `XMPUtilityServiceClient` en utilisant son constructeur et en transmettant un objet `ServiceClientFactory` contenant des propriétés de connexion.

1. Appeler l’opération d’importation des métadonnées XMP

   Pour examiner les métadonnées XMP, appelez la méthode `XMPUtilityServiceClient` de l’objet `exportMetadata` et transmettez un objet `com.adobe.idp.Document` qui représente le fichier PDF. La méthode renvoie un objet `XMPUtilityMetadata` contenant les métadonnées récupérées.

   Pour récupérer et enregistrer les métadonnées XMP, appelez la méthode `XMPUtilityServiceClient` de l’objet `exportXMP` et transmettez un objet `com.adobe.idp.Document` qui représente le fichier PDF. La méthode renvoie un objet `com.adobe.idp.Document` contenant les métadonnées récupérées, que vous pouvez ensuite enregistrer sur le disque sous forme de fichier XML.

**Voir également**

[Exportation de métadonnées à partir de Documents PDF](xmp-utilities.md#exporting-metadata-from-pdf-documents)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Exporter XMP métadonnées à l’aide de l’API du service Web {#export-xmp-metadata-using-the-web-service-api}

Exportez XMP métadonnées à l’aide de l’API XMP Utilities (service Web) :

1. Inclure les fichiers de projet

   * Créez un assembly client Microsoft .NET qui consomme le fichier WSDL du service XMP Utilities.
   * Référencez l&#39;assembly client Microsoft .NET.

1. Création d’un client XMPUtilityService

   Créez un objet `XMPUtilityServiceService` en utilisant votre constructeur de classe proxy.

1. Appeler l’opération d’importation des métadonnées XMP

   Pour examiner les métadonnées XMP, appelez la méthode `XMPUtilityServiceClient` de l’objet `exportMetadata` et transmettez un objet `BLOB` qui représente le fichier PDF. La méthode renvoie un objet `XMPUtilityMetadata` contenant les métadonnées récupérées.

   Pour récupérer et enregistrer les métadonnées XMP, appelez la méthode `XMPUtilityServiceClient` de l’objet `exportXMP` et transmettez un objet `BLOB` qui représente le fichier PDF. La méthode renvoie un objet `BLOB` contenant les métadonnées récupérées, que vous pouvez ensuite enregistrer sur le disque sous forme de fichier XML.

**Voir également**

[Exportation de métadonnées à partir de Documents PDF](xmp-utilities.md#exporting-metadata-from-pdf-documents)

[Appel de AEM Forms à l’aide du codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Création d&#39;un assembly client .NET utilisant le codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)
