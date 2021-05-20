---
title: Assemblage de Portfolios PDF
seo-title: Assemblage de Portfolios PDF
description: Assemblez un portfolio PDF pour combiner plusieurs documents de différents types, y compris des fichiers Word, images et PDF. Vous pouvez assembler un portfolio PDF à l’aide d’une API Java et d’une API Web Service.
seo-description: Assemblez un portfolio PDF pour combiner plusieurs documents de différents types, y compris des fichiers Word, images et PDF. Vous pouvez assembler un portfolio PDF à l’aide d’une API Java et d’une API Web Service.
uuid: 1778c90b-9d26-466b-a7c7-401d737395e0
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 023f0d9e-bfde-4879-a839-085fadffb48e
role: Developer
exl-id: d2bd7c3e-4f75-4234-a7aa-ee8524430493
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1865'
ht-degree: 3%

---

# Assemblage de Portfolios PDF {#assembling-pdf-portfolios}

**Les exemples et les exemples de ce document sont réservés à l’environnement AEM Forms on JEE.**

Vous pouvez assembler un Portfolio PDF à l’aide de l’API Java Assembler et de l’API Web Service. Un portfolio peut combiner plusieurs documents de différents types, y compris un fichier Word, des fichiers image (par exemple, un fichier jpeg) et des documents PDF. La mise en page du portfolio peut être définie sur différents styles, comme la *Grille avec aperçu*, la *sur une mise en page Image* ou même la *Révolution*.

L’illustration suivante est une capture d’écran d’un portfolio avec une disposition de style *Sur une image*.

![ap_ap_portfolio](assets/ap_ap_portfolio.png)

La création d’un Portfolio PDF constitue une alternative sans papier à la transmission d’une collection de documents. Avec AEM Forms, vous pouvez créer des portefeuilles en appelant le service Assembler avec un document DDX structuré. Le document DDX suivant est un exemple de document DDX qui crée un Portfolio PDF.

```xml
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
     <PDF result="portfolio1.pdf">
         <Portfolio>
             <Navigator source="myNavigator">
                 <Resource name="navigator/image.xxx" source="myImage.png"/>
             </Navigator>
         </Portfolio>
         <PackageFiles source="dog1"  >
              <FieldData name="X">72</FieldData>
             <FieldData name="Y">72</FieldData>
             <File filename="saint_bernard.jpg" mimetype="image/jpeg"/>
         </PackageFiles>
         <PackageFiles source="dog2"  >
             <FieldData name="X">120</FieldData>
             <FieldData name="Y">216</FieldData>
             <File filename="greyhound.pdf"/>
         </PackageFiles>
     </PDF>
 </DDX>
```

Le document DXX doit contenir une balise `Portfolio` avec une balise `Navigator` imbriquée. Notez que la balise `<Resource name="navigator/image.xxx" source="myImage.png"/>` n’est nécessaire que si `myNavigator` est affecté en tant que navigateur de mise en page onImage : `AdobeOnImage.nav`. Cette balise permet au service Assembler de sélectionner l’image à utiliser comme arrière-plan du portfolio. Insérez des balises `PackageFiles` et `File` pour définir le nom de fichier et le type MIME du fichier empaqueté.

>[!NOTE]
>
>Pour plus d’informations sur le service Assembler, voir [Référence des services pour AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Pour plus d’informations sur un document DDX, voir [Guide de référence du service Assembler et de DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Résumé des étapes {#summary-of-steps}

Pour créer un Portfolio PDF, procédez comme suit :

1. Inclure les fichiers de projet.
1. Créez un client PDF Assembler.
1. Référencez un document DX existant.
1. Référencez les documents requis.
1. Définissez les options d’exécution.
1. Assemblez le portfolio.
1. Enregistrez le portfolio assemblé.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

Les fichiers JAR suivants doivent être ajoutés au chemin de classe de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utility.jar (obligatoire si AEM Forms est déployé sur JBoss)
* jbossall-client.jar (obligatoire si AEM Forms est déployé sur JBoss)

**Création d’un client PDF Assembler**

Avant de pouvoir effectuer une opération Assembler par programmation, créez un client de service Assembler.

**Référence à un document DDX existant**

Un document DDX doit être référencé pour assembler un Portfolio PDF. Ce document DDX doit contenir les éléments `Portfolio`, `Navigator` et `PackageFiles` .

**Référencer les documents requis**

Pour assembler un Portfolio PDF, référencez tous les fichiers représentant les documents à assembler. Par exemple, transmettez tous les fichiers image spécifiés dans le document DDX au service Assembler. Notez que ces fichiers sont référencés dans le document DDX spécifié dans cette section : *myImage.png* et *saint_bernard.jpg*.

Lors de l’assemblage d’un Portfolio PDF, transmettez un fichier NAV (un fichier de navigateur) au service Assembler. Le fichier NAV que vous transmettez au service Assembler dépend du type de Portfolio PDF à créer. Par exemple, pour créer une disposition *Sur une image*, transmettez le fichier AdobeOnImage.nav . Vous pouvez localiser les fichiers NAV dans le dossier suivant :

`<Install folder>\Acrobat 9.0\Acrobat\Navigators`

Copiez le fichier NAV du répertoire d’installation d’Acrobat 9 (ou version ultérieure). Placez le fichier NAV à un emplacement accessible par votre application cliente. Tous les fichiers sont transmis au service Assembler dans un objet de collection Map.

>[!NOTE]
>
>Les démarrages rapides associés à l’assemblage de Portfolios PDF utilisent AdobeOnImage.nav.

**Définition des options d’exécution**

Vous pouvez définir des options d’exécution qui contrôlent le comportement du service Assembler lors de l’exécution d’une tâche. Par exemple, vous pouvez définir une option qui indique au service Assembler de continuer à traiter une tâche en cas d’erreur.

**Assemblage du portfolio**

Pour assembler un Portfolio PDF, appelez l’opération `invokeDDX`. Le service Assembler renvoie le Portfolio PDF dans un objet de collection.

**Enregistrer le portfolio assemblé**

Un Portfolio PDF est renvoyé dans un objet de collection. Effectuez une itération sur l’objet de collection et enregistrez le Portfolio PDF en tant que fichier PDF.

**Voir également**

[Assemblage d’un Portfolio PDF à l’aide de l’API Java](#assemble-a-pdf-portfolio-using-the-java-api)

[Assemblage d’un Portfolio PDF à l’aide de l’API du service Web](#assemble-a-pdf-portfolio-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Assemblage de documents PDF par programmation](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Assemblage d’un Portfolio PDF à l’aide de l’API Java {#assemble-a-pdf-portfolio-using-the-java-api}

Assemblez un Portfolio PDF à l’aide de l’API Assembler Service (Java) :

1. Inclure les fichiers de projet.

   Incluez des fichiers JAR client, tels que adobe-assembler-client.jar, dans le chemin d’accès à la classe de votre projet Java.

1. Créez un client PDF Assembler.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `AssemblerServiceClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`.

1. Référencez un document DX existant.

   * Créez un objet `java.io.FileInputStream` qui représente le document DDX en utilisant son constructeur et en transmettant une valeur string qui spécifie l’emplacement du fichier DDX.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Référencez les documents requis.

   * Créez un objet `java.util.Map` utilisé pour stocker des documents PDF d’entrée à l’aide d’un constructeur `HashMap`.
   * Créez un objet `java.io.FileInputStream` en utilisant son constructeur. Transmettez l’emplacement du fichier NAV requis (répétez cette tâche pour chaque fichier requis pour créer un portfolio).
   * Créez un objet `com.adobe.idp.Document` et transmettez l’objet `java.io.FileInputStream` contenant le fichier NAV (répétez cette tâche pour chaque fichier requis pour créer un portfolio).
   * Ajoutez une entrée à l’objet `java.util.Map` en appelant sa méthode `put` et en transmettant les arguments suivants :

      * Une valeur string qui représente le nom de la clé. Cette valeur doit correspondre à la valeur de l’élément source spécifié dans le document DDX. (répétez cette tâche pour chaque fichier requis pour créer un portfolio).
      * Objet `com.adobe.idp.Document` contenant le document PDF. (répétez cette tâche pour chaque fichier requis pour créer un portfolio).

1. Définissez les options d’exécution.

   * Créez un objet `AssemblerOptionSpec` qui stocke les options d’exécution à l’aide de son constructeur.
   * Définissez les options d’exécution pour répondre aux besoins de votre entreprise en appelant une méthode appartenant à l’objet `AssemblerOptionSpec` . Par exemple, pour demander au service Assembler de continuer à traiter une tâche en cas d’erreur, appelez la méthode `setFailOnError` de l’objet `false` et transmettez `AssemblerOptionSpec`.

1. Assemblez le portfolio.

   Appelez la méthode `invokeDDX` de l’objet `AssemblerServiceClient` et transmettez les valeurs requises suivantes :

   * Objet `com.adobe.idp.Document` représentant le document DDX à utiliser
   * Objet `java.util.Map` contenant les fichiers nécessaires à la création d’un Portfolio PDF.
   * Objet `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` qui spécifie les options d’exécution, y compris la police par défaut et le niveau de journalisation de la tâche

   La méthode `invokeDDX` renvoie un objet `com.adobe.livecycle.assembler.client.AssemblerResult` contenant le Portfolio PDF assemblé et toutes les exceptions qui se sont produites.

1. Enregistrez le portfolio assemblé.

   Pour obtenir le Portfolio PDF, procédez comme suit :

   * Appelez la méthode `getDocuments` de l’objet `AssemblerResult`. Cette méthode renvoie un objet `java.util.Map` .
   * Effectuez une itération sur l’objet `java.util.Map` jusqu’à ce que vous trouviez l’objet `com.adobe.idp.Document` résultant.
   * Appelez la méthode `copyToFile` de l’objet `com.adobe.idp.Document` pour extraire le Portfolio PDF.

**Voir également**

[Démarrage rapide (mode SOAP) : Assemblage de Portfolios PDF à l’aide de l’API Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-pdf-portfolios-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Assemblage d’un Portfolio PDF à l’aide de l’API de service Web {#assemble-a-pdf-portfolio-using-the-web-service-api}

Assemblez un Portfolio PDF à l’aide de l’API Assembler Service (service Web) :

1. Inclure les fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Assurez-vous d’utiliser la définition WSDL suivante lors de la définition d’une référence de service : `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un client PDF Assembler.

   * Créez un objet `AssemblerServiceClient` à l’aide de son constructeur par défaut.
   * Créez un objet `AssemblerServiceClient.Endpoint.Address` à l’aide du constructeur `System.ServiceModel.EndpointAddress`. Transmettez une valeur string qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/AssemblerService?blob=mtom`). Vous n’avez pas besoin d’utiliser l’attribut `lc_version`. Cet attribut est utilisé lorsque vous créez une référence de service.
   * Créez un objet `System.ServiceModel.BasicHttpBinding` en obtenant la valeur du champ `AssemblerServiceClient.Endpoint.Binding`. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le champ `MessageEncoding` de l’objet `System.ServiceModel.BasicHttpBinding` sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Référencez un document DX existant.

   * Créez un objet `BLOB` en utilisant son constructeur. L’objet `BLOB` est utilisé pour stocker le document DDX.
   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur string qui représente l’emplacement du fichier du document DDX et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `System.IO.FileStream`. Vous pouvez déterminer la taille du tableau d’octets en obtenant la propriété `System.IO.FileStream` de l’objet `Length`.
   * Renseignez le tableau d’octets avec les données de diffusion en appelant la méthode `Read` de l’objet `System.IO.FileStream`. Transmettez le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’objet `BLOB` en attribuant sa propriété `MTOM` avec le contenu du tableau d’octets.

1. Référencez les documents requis.

   * Pour chaque fichier d’entrée, créez un objet `BLOB` à l’aide de son constructeur. L’objet `BLOB` est utilisé pour stocker le fichier d’entrée.
   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur string qui représente l’emplacement du fichier d’entrée et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `System.IO.FileStream`. Vous pouvez déterminer la taille du tableau d’octets en obtenant la propriété `System.IO.FileStream` de l’objet `Length`.
   * Renseignez le tableau d’octets avec les données de diffusion en appelant la méthode `Read` de l’objet `System.IO.FileStream`. Transmettez le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’objet `BLOB` en attribuant son champ `MTOM` avec le contenu du tableau d’octets.
   * Créez un objet `MyMapOf_xsd_string_To_xsd_anyType` . Cet objet de collection est utilisé pour stocker les fichiers d’entrée nécessaires à la création d’un Portfolio PDF.
   * Pour chaque fichier d’entrée, créez un objet `MyMapOf_xsd_string_To_xsd_anyType_Item` .
   * Attribuez une valeur string qui représente le nom de la clé au champ `key` de l’objet `MyMapOf_xsd_string_To_xsd_anyType_Item`. Cette valeur doit correspondre à la valeur de l’élément spécifié dans le document DDX. (Effectuez cette tâche pour chaque fichier d’entrée.)
   * Affectez l’objet `BLOB` qui stocke le fichier d’entrée dans le champ `value` de l’objet `MyMapOf_xsd_string_To_xsd_anyType_Item`. (Effectuez cette tâche pour chaque document PDF d’entrée.)
   * Ajoutez l’objet `MyMapOf_xsd_string_To_xsd_anyType_Item` à l’objet `MyMapOf_xsd_string_To_xsd_anyType`. Appelez la méthode `Add` de l’objet `MyMapOf_xsd_string_To_xsd_anyType` et transmettez l’objet `MyMapOf_xsd_string_To_xsd_anyType` . (Effectuez cette tâche pour chaque document PDF d’entrée.)

1. Définissez les options d’exécution.

   * Créez un objet `AssemblerOptionSpec` qui stocke les options d’exécution à l’aide de son constructeur.
   * Définissez des options d’exécution pour répondre aux besoins de votre entreprise en attribuant une valeur à un membre de données qui appartient à l’objet `AssemblerOptionSpec`. Par exemple, pour demander au service Assembler de continuer à traiter une tâche en cas d’erreur, affectez `false` au membre de données `failOnError` de l’objet `AssemblerOptionSpec`.

1. Assemblez le portfolio.

   Appelez la méthode `invokeDDX` de l’objet `AssemblerServiceClient` et transmettez les valeurs suivantes :

   * Objet `BLOB` représentant le document DDX
   * Objet `MyMapOf_xsd_string_To_xsd_anyType` contenant les fichiers requis
   * Objet `AssemblerOptionSpec` spécifiant les options d’exécution

   La méthode `invokeDDX` renvoie un objet `AssemblerResult` contenant les résultats de la tâche et toutes les exceptions qui se sont produites.

1. Enregistrez le portfolio assemblé.

   Pour obtenir le Portfolio PDF nouvellement créé, procédez comme suit :

   * Accédez au champ `documents` de l’objet `AssemblerResult`, qui est un objet `Map` contenant les documents PDF obtenus.
   * Effectuez une itération sur l’objet `Map` pour obtenir chaque document généré. Ensuite, convertissez le `value` de ce membre de tableau en `BLOB`.
   * Extrayez les données binaires qui représentent le document PDF en accédant à la propriété `MTOM` de l’objet `BLOB`. Cette opération renvoie un tableau d’octets que vous pouvez écrire dans un fichier PDF.

**Voir également**

[Appel d’AEM Forms à l’aide de MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Appel d’AEM Forms à l’aide de SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
