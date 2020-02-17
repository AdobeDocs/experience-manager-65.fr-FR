---
title: Assemblage de portfolios PDF
seo-title: Assemblage de portfolios PDF
description: 'null'
seo-description: 'null'
uuid: 1778c90b-9d26-466b-a7c7-401d737395e0
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 023f0d9e-bfde-4879-a839-085fadffb48e
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Assemblage de portfolios PDF {#assembling-pdf-portfolios}

Vous pouvez assembler un portfolio PDF à l’aide de l’API Java Assembler et du service Web. Un portfolio peut combiner plusieurs documents de différents types, y compris des fichiers Word, des fichiers image (par exemple, un fichier jpeg) et des documents PDF. La mise en page du portfolio peut être définie sur différents styles, comme la *grille avec aperçu*, la mise en page *Sur une image* ou même *Révolution*.

L’illustration suivante est une capture d’écran d’un portfolio avec une disposition de style *On an Image* .

![ap_ap_portfolio](assets/ap_ap_portfolio.png)

La création d’un portfolio PDF constitue une alternative sans papier à la transmission d’une collection de documents. AEM Forms vous permet de créer des portefeuilles en appelant le service Assembler avec un document DDX structuré. Le document DDX suivant est un exemple de document DDX qui crée un portfolio PDF.

```as3
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

Le document DXX doit contenir une `Portfolio` balise avec une `Navigator` balise imbriquée. Notez que la balise `<Resource name="navigator/image.xxx" source="myImage.png"/>` n’est nécessaire que si `myNavigator` elle est affectée en tant que navigateur de mise en page onImage : `AdobeOnImage.nav`. Cette balise permet au service Assembler de sélectionner l’image à utiliser comme arrière-plan du portefeuille. Incluez `PackageFiles` et `File` des balises pour définir le nom de fichier et le type MIME du fichier compressé.

>[!NOTE]
>
>For more information about the Assembler service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Pour plus d’informations sur un document DDX, voir [Assembler Service et Référence](https://www.adobe.com/go/learn_aemforms_ddx_63)DDX.

## Résumé des étapes {#summary-of-steps}

Pour créer un portfolio PDF, procédez comme suit :

1. Incluez des fichiers de projet.
1. Créez un client PDF Assembler.
1. Référencez un document DDX existant.
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
* adobe-utilities.jar (requis si AEM Forms est déployé sur JBoss)
* jbossall-client.jar (requis si AEM Forms est déployé sur JBoss)

**Création d’un client PDF Assembler**

Avant de pouvoir exécuter une opération Assembler par programmation, créez un client de service Assembler.

**Référence à un document DDX existant**

Un document DDX doit être référencé pour assembler un portfolio PDF. Ce document DDX doit contenir les éléments `Portfolio`, `Navigator` et `PackageFiles` .

**Référencer les documents requis**

Pour assembler un portfolio PDF, référencez tous les fichiers représentant les documents à assembler. Par exemple, transmettez tous les fichiers d’image spécifiés dans le document DDX au service Assembler. Notez que ces fichiers sont référencés dans le document DDX spécifié dans cette section : *myImage.png* et *saint_bernard.jpg*.

Lors de l’assemblage d’un portfolio PDF, transmettez un fichier NAV (fichier de navigateur) au service Assembler. Le fichier NAV que vous transmettez au service Assembler dépend du type de portfolio PDF à créer. Par exemple, pour créer une disposition *On a Image* , transmettez le fichier AdobeOnImage.nav. Vous pouvez localiser les fichiers NAV dans le dossier suivant :

`<Install folder>\Acrobat 9.0\Acrobat\Navigators`

Copiez le fichier NAV du répertoire d’installation d’Acrobat 9 (ou version ultérieure). Placez le fichier NAV à l’emplacement auquel votre application cliente peut accéder. Tous les fichiers sont transmis au service Assembler dans un objet de collection Map.

>[!NOTE]
>
>Les démarrages rapides associés à l’assemblage de portfolios PDF utilisent AdobeOnImage.nav.

**Définition des options d’exécution**

Vous pouvez définir des options d’exécution qui contrôlent le comportement du service Assembler lorsqu’il effectue une tâche. Par exemple, vous pouvez définir une option qui indique au service Assembler de poursuivre le traitement d’une tâche en cas d’erreur.

**Assemblage du portefeuille**

Pour assembler un portfolio PDF, appelez l’ `invokeDDX` opération. Le service Assembler renvoie le portfolio PDF dans un objet de collection.

**Enregistrer le portfolio assemblé**

Un portfolio PDF est renvoyé dans un objet de collection. Parcourez l’objet de collection et enregistrez le portfolio PDF au format PDF.

**Voir également**

[Assemblage d’un portfolio PDF à l’aide de l’API Java](#assemble-a-pdf-portfolio-using-the-java-api)

[Assemblage d’un portfolio PDF à l’aide de l’API du service Web](#assemble-a-pdf-portfolio-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Assemblage par programmation de documents PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Assemblage d’un portfolio PDF à l’aide de l’API Java {#assemble-a-pdf-portfolio-using-the-java-api}

Assemblage d’un portfolio PDF à l’aide de l’API Assembler Service (Java) :

1. Incluez des fichiers de projet.

   Incluez des fichiers JAR client, tels que adobe-assembler-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un client PDF Assembler.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Create an `AssemblerServiceClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. Référencez un document DDX existant.

   * Créez un `java.io.FileInputStream` objet qui représente le document DDX en utilisant son constructeur et en transmettant une valeur de chaîne qui spécifie l’emplacement du fichier DDX.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Référencez les documents requis.

   * Créez un `java.util.Map` objet utilisé pour stocker des documents PDF d’entrée à l’aide d’un `HashMap` constructeur.
   * Créez un objet `java.io.FileInputStream` en utilisant son constructeur. Transmettez l’emplacement du fichier NAV requis (répétez cette tâche pour chaque fichier requis pour créer un portfolio).
   * Créez un `com.adobe.idp.Document` objet et transmettez l’ `java.io.FileInputStream` objet qui contient le fichier NAV (répétez cette tâche pour chaque fichier requis pour créer un portfolio).
   * Ajoutez une entrée à l’ `java.util.Map` objet en appelant sa `put` méthode et en transmettant les arguments suivants :

      * Valeur de chaîne qui représente le nom de la clé. Cette valeur doit correspondre à la valeur de l’élément source spécifié dans le document DDX. (répétez cette tâche pour chaque fichier requis pour créer un portfolio).
      * Objet `com.adobe.idp.Document` contenant le document PDF. (répétez cette tâche pour chaque fichier requis pour créer un portfolio).

1. Définissez les options d’exécution.

   * Créez un `AssemblerOptionSpec` objet qui stocke les options d’exécution à l’aide de son constructeur.
   * Définissez des options d’exécution pour répondre aux besoins de votre entreprise en appelant une méthode qui appartient à l’ `AssemblerOptionSpec` objet. Par exemple, pour demander au service Assembler de poursuivre le traitement d’une tâche en cas d’erreur, appelez la `AssemblerOptionSpec` méthode de l’ `setFailOnError` objet et transmettez-la `false`.

1. Assemblez le portfolio.

   Appelez la méthode `AssemblerServiceClient` `invokeDDX` de l’objet et transmettez les valeurs requises suivantes :

   * Objet `com.adobe.idp.Document` représentant le document DDX à utiliser
   * Objet `java.util.Map` contenant les fichiers requis pour créer un portfolio PDF.
   * Objet `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` spécifiant les options d’exécution, notamment la police par défaut et le niveau du journal des tâches
   La `invokeDDX` méthode renvoie un `com.adobe.livecycle.assembler.client.AssemblerResult` objet contenant le portfolio PDF assemblé et les exceptions survenues.

1. Enregistrez le portfolio assemblé.

   Pour obtenir le portfolio PDF, procédez comme suit :

   * Appelez la méthode `AssemblerResult` `getDocuments` de l’objet. Cette méthode renvoie un `java.util.Map` objet.
   * Effectuez une itération sur l’ `java.util.Map` objet jusqu’à ce que vous trouviez l’ `com.adobe.idp.Document` objet résultant.
   * Appelez la méthode `com.adobe.idp.Document` `copyToFile` de l’objet pour extraire le portfolio PDF.

**Voir également**

[Démarrage rapide (mode SOAP) : Assemblage de portfolios PDF à l’aide de l’API Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-pdf-portfolios-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Assemblage d’un portfolio PDF à l’aide de l’API du service Web {#assemble-a-pdf-portfolio-using-the-web-service-api}

Assemblage d’un portfolio PDF à l’aide de l’API Assembler Service (service Web) :

1. Incluez des fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Veillez à utiliser la définition WSDL suivante lors de la définition d’une référence de service : `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un client PDF Assembler.

   * Créez un `AssemblerServiceClient` objet à l’aide de son constructeur par défaut.
   * Créez un `AssemblerServiceClient.Endpoint.Address` objet à l’aide du `System.ServiceModel.EndpointAddress` constructeur. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/AssemblerService?blob=mtom`). Vous n’avez pas besoin d’utiliser l’ `lc_version` attribut. Cet attribut est utilisé lorsque vous créez une référence de service.
   * Créez un `System.ServiceModel.BasicHttpBinding` objet en obtenant la valeur du `AssemblerServiceClient.Endpoint.Binding` champ. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le `System.ServiceModel.BasicHttpBinding` champ de l’ `MessageEncoding` objet sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant les tâches suivantes :

      * Attribuez le nom d’utilisateur d’AEM forms au champ `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Référencez un document DDX existant.

   * Créez un objet `BLOB` en utilisant son constructeur. L’ `BLOB` objet est utilisé pour stocker le document DDX.
   * Créez un `System.IO.FileStream` objet en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du fichier du document DDX et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’ `System.IO.FileStream` objet. Vous pouvez déterminer la taille du tableau d’octets en obtenant la `System.IO.FileStream` `Length` propriété de l’objet.
   * Renseignez le tableau d’octets avec les données de flux en appelant la `System.IO.FileStream` `Read` méthode de l’objet. Passez le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’ `BLOB` objet en affectant sa `MTOM` propriété au contenu du tableau d’octets.

1. Référencez les documents requis.

   * Pour chaque fichier d’entrée, créez un `BLOB` objet à l’aide de son constructeur. L’ `BLOB` objet est utilisé pour stocker le fichier d’entrée.
   * Créez un `System.IO.FileStream` objet en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du fichier d’entrée et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’ `System.IO.FileStream` objet. Vous pouvez déterminer la taille du tableau d’octets en obtenant la `System.IO.FileStream` `Length` propriété de l’objet.
   * Renseignez le tableau d’octets avec les données de flux en appelant la `System.IO.FileStream` `Read` méthode de l’objet. Passez le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’ `BLOB` objet en affectant son `MTOM` champ au contenu du tableau d’octets.
   * Create a `MyMapOf_xsd_string_To_xsd_anyType` object. Cet objet de collection permet de stocker les fichiers d’entrée nécessaires à la création d’un portfolio PDF.
   * Pour chaque fichier d’entrée, créez un `MyMapOf_xsd_string_To_xsd_anyType_Item` objet.
   * Attribuez une valeur de chaîne représentant le nom de la clé au `MyMapOf_xsd_string_To_xsd_anyType_Item` `key` champ de l’objet. Cette valeur doit correspondre à la valeur de l’élément spécifié dans le document DDX. (Effectuez cette tâche pour chaque fichier d’entrée.)
   * Affectez l’ `BLOB` objet qui stocke le fichier d’entrée au `MyMapOf_xsd_string_To_xsd_anyType_Item` `value` champ de l’objet. (Effectuez cette tâche pour chaque document PDF d’entrée.)
   * Ajoutez l’ `MyMapOf_xsd_string_To_xsd_anyType_Item` objet à l’ `MyMapOf_xsd_string_To_xsd_anyType` objet. Invoke the `MyMapOf_xsd_string_To_xsd_anyType` object&#39;s `Add` method and pass the `MyMapOf_xsd_string_To_xsd_anyType` object. (Effectuez cette tâche pour chaque document PDF d’entrée.)

1. Définissez les options d’exécution.

   * Créez un `AssemblerOptionSpec` objet qui stocke les options d’exécution à l’aide de son constructeur.
   * Définissez des options d’exécution pour répondre aux besoins de votre entreprise en attribuant une valeur à un membre de données qui appartient à l’ `AssemblerOptionSpec` objet. Par exemple, pour demander au service Assembler de poursuivre le traitement d’une tâche en cas d’erreur, affectez `false` au membre `AssemblerOptionSpec` `failOnError` de données de l’objet.

1. Assemblez le portfolio.

   Appelez la méthode `AssemblerServiceClient` `invokeDDX` de l’objet et transmettez les valeurs suivantes :

   * Objet `BLOB` représentant le document DDX
   * Objet `MyMapOf_xsd_string_To_xsd_anyType` contenant les fichiers requis
   * Objet `AssemblerOptionSpec` spécifiant les options d’exécution
   La `invokeDDX` méthode renvoie un `AssemblerResult` objet qui contient les résultats de la tâche et les exceptions survenues.

1. Enregistrez le portfolio assemblé.

   Pour obtenir le portfolio PDF nouvellement créé, procédez comme suit :

   * Accédez au `AssemblerResult` champ de l’ `documents` objet, qui est un `Map` objet contenant les documents PDF obtenus.
   * Effectuez une itération dans l’ `Map` objet pour obtenir chaque document cible. Jetez ensuite le numéro `value` de l’élément de tableau sur un `BLOB`.
   * Extrayez les données binaires qui représentent le document PDF en accédant à la `BLOB` `MTOM` propriété de son objet. Cette opération renvoie un tableau d’octets que vous pouvez écrire dans un fichier PDF.

**Voir également**

[Appel d’AEM Forms à l’aide de MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Appel d’AEM Forms à l’aide de SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
