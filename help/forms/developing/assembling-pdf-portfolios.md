---
title: Assemblage de portfolios PDF
description: Assemblez un portfolio PDF afin de combiner plusieurs documents de différents types, notamment des fichiers Word, image et PDF. Vous pouvez assembler un portfolio PDF à l’aide d’une API Java et d’une API de service web.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: d2bd7c3e-4f75-4234-a7aa-ee8524430493
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,  Document Services
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '1815'
ht-degree: 100%

---

# Assemblage de portfolios PDF {#assembling-pdf-portfolios}

**Les exemples et les échantillons de ce document sont réservés à l’environnement AEM Forms sur JEE.**

Vous pouvez assembler un portfolio PDF à l’aide de l’API Java Assembler et de l’API de service web. Un portfolio permet de combiner plusieurs documents de différents types, notamment un fichier Word, des fichiers image (par exemple, un fichier jpeg) et des documents PDF. La disposition du portfolio peut être définie selon différents styles, comme la *Grille avec prévisualisation*, la disposition *Sur une image* ou encore *Rotation*.

La capture d’écran suivante représente un portfolio avec la disposition *Sur une image*.

![ap_ap_portfolio](assets/ap_ap_portfolio.png)

La création d’un portfolio PDF constitue une alternative zéro carbone à la transmission d’une collection de documents. Avec AEM Forms, vous pouvez créer des portfolios en appelant le service Assembler avec un document DDX structuré. Le document DDX suivant est un exemple de document DDX qui permet de créer un portfolio PDF.

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

Le document DXX doit contenir une balise `Portfolio` avec une balise `Navigator` imbriquée. Notez que la balise `<Resource name="navigator/image.xxx" source="myImage.png"/>` n’est nécessaire que si `myNavigator` est affecté comme navigateur de disposition onImage : `AdobeOnImage.nav`. Cette balise permet au service Assembler de sélectionner l’image à utiliser comme arrière-plan du portfolio. Ajoutez les balises `PackageFiles` et `File` pour définir le nom de fichier et le type MIME du fichier empaqueté.

>[!NOTE]
>
>Pour plus d’informations sur le service Assembler, consultez la section [Références des services pour AEM Forms](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

>[!NOTE]
>
>Pour plus d’informations sur les documents DDX, consultez la section [Guide de référence du service Assembler et de DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Résumé des étapes {#summary-of-steps}

Pour créer un portfolio PDF, procédez comme suit :

1. Incluez les fichiers de projet.
1. Créez un client Assembler PDF.
1. Référencez un document DX existant.
1. Référencez les documents requis.
1. Définissez les options d’exécution.
1. Assemblez le portfolio.
1. Enregistrez le portfolio assemblé.

**Inclusion des fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

Les fichiers JAR suivants doivent être ajoutés au chemin d’accès aux classes de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utility.jar (obligatoire si AEM Forms est déployé sur JBoss)
* jbossall-client.jar (obligatoire si AEM Forms est déployé sur JBoss)

**Créer un client PDF Assembler**

Avant de pouvoir effectuer une opération Assembler par programmation, créez un client de service Assembler.

**Référence à un document DDX existant**

Un document DDX doit être référencé afin de pouvoir assembler un portfolio PDF. Ce document DDX doit contenir les éléments `Portfolio`, `Navigator` et `PackageFiles`.

**Référence des documents requis**

Pour assembler un portfolio PDF, référencez tous les fichiers qui représentent les documents à assembler. Par exemple, transmettez tous les fichiers image spécifiés dans le document DDX au service Assembler. Notez que ces fichiers sont référencés dans le document DDX spécifié dans cette section : *myImage.png* et *saint_bernard.jpg*.

Lors de l’assemblage d’un portfolio PDF, transmettez un fichier NAV (un fichier de navigateur) au service Assembler. Le fichier NAV que vous transmettez au service Assembler dépend du type de portfolio PDF à créer. Par exemple, pour créer une disposition *Sur une image*, transmettez le fichier AdobeOnImage.nav. Les fichiers NAV se trouvent dans le dossier suivant :

`<Install folder>\Acrobat 9.0\Acrobat\Navigators`

Copiez le fichier NAV situé dans le répertoire d’installation d’Acrobat 9 (ou version ultérieure). Placez le fichier NAV à un emplacement accessible par votre application cliente. Tous les fichiers sont transmis au service Assembler dans un objet de collection Map.

>[!NOTE]
>
>Les didacticiels de mise en route traitant de lʼassemblage des portfolios PDF utilisent AdobeOnImage.nav.

**Définition des options d’exécution**

Vous pouvez définir des options d’exécution qui contrôlent le comportement du service Assembler lors de l’exécution d’une tâche. Par exemple, vous pouvez définir une option qui indique au service Assembler de continuer à traiter une tâche en cas d’erreur.

**Assemblage du portfolio**

Pour assembler un portfolio PDF, vous devez appeler lʼopération `invokeDDX`. Le service Assembler renvoie le portfolio PDF dans un objet de collection.

**Enregistrement du portfolio assemblé**

Un portfolio PDF est renvoyé dans un objet de collection. Effectuez une itération au sein de l’objet de collection et enregistrez le portfolio PDF au format PDF.

**Voir également**

[Assemblage d’un portfolio PDF à l’aide de l’API Java](#assemble-a-pdf-portfolio-using-the-java-api)

[Assemblage d’un portfolio PDF à l’aide de l’API de service web](#assemble-a-pdf-portfolio-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Assembler les documents PDF par programmation](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Assemblage d’un portfolio PDF à l’aide de l’API Java {#assemble-a-pdf-portfolio-using-the-java-api}

Assemblez un portfolio PDF à l’aide de l’API du service Assembler (Java) :

1. Incluez les fichiers de projet.

   Incluez les fichiers JAR clients, tels que adobe-assembler-client.jar, dans le chemin d’accès aux classes de votre projet Java.

1. Créez un client Assembler PDF.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `AssemblerServiceClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`.

1. Référencez un document DX existant.

   * Créez un objet `java.io.FileInputStream` qui représente le document DDX en utilisant son constructeur et en transmettant une valeur de chaîne qui spécifie l’emplacement du fichier DDX.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Référencez les documents requis.

   * Créez un objet `java.util.Map` qui sert à stocker les documents PDF d’entrée en utilisant un constructeur `HashMap`.
   * Créez un objet `java.io.FileInputStream` en utilisant son constructeur. Transmettez l’emplacement du fichier NAV requis (répétez cette tâche pour chaque fichier nécessaire à la création dʼun portfolio).
   * Créez un objet `com.adobe.idp.Document` et transmettez lʼobjet `java.io.FileInputStream` contenant le fichier NAV (répétez cette tâche pour chaque fichier nécessaire à la création dʼun portfolio).
   * Ajoutez une entrée à lʼobjet `java.util.Map` en appelant sa méthode `put` et en transmettant les arguments suivants :

      * Une valeur de chaîne qui représente le nom de la clé. Cette valeur doit correspondre à la valeur de l’élément source spécifié dans le document DDX. (répétez cette tâche pour chaque fichier nécessaire à la création dʼun portfolio).
      * Un objet `com.adobe.idp.Document` qui contient le document PDF. (répétez cette tâche pour chaque fichier nécessaire à la création dʼun portfolio).

1. Définissez les options d’exécution.

   * Créez un objet `AssemblerOptionSpec` qui stocke les options d’exécution en utilisant son constructeur.
   * Définissez les options d’exécution pour répondre à vos exigences professionnelles en appelant une méthode appartenant à l’objet `AssemblerOptionSpec`. Par exemple, pour demander au service Assembler de poursuivre le traitement dʼune tâche lorsquʼune erreur se produit, appelez la méthode `setFailOnError` de l’objet `AssemblerOptionSpec` et transmettez `false`.

1. Assemblez le portfolio.

   Appelez la méthode `invokeDDX` de lʼobjet `AssemblerServiceClient` et transmettez les valeurs requises suivantes :

   * Un objet `com.adobe.idp.Document` qui représente le document DDX à utiliser.
   * Un objet `java.util.Map` qui contient les fichiers nécessaires à la création dʼun portfolio PDF.
   * Un objet `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` qui spécifie les options d’exécution, y compris la police par défaut et le niveau du log de traitement.

   La méthode `invokeDDX` renvoie un objet `com.adobe.livecycle.assembler.client.AssemblerResult` contenant le portfolio PDF assemblé et toutes les exceptions survenues.

1. Enregistrez le portfolio assemblé.

   Pour obtenir le portfolio PDF, procédez comme suit :

   * Appelez la méthode `getDocuments` de lʼobjet `AssemblerResult`. Cette méthode renvoie un objet `java.util.Map`.
   * Effectuez une itération au sein de lʼobjet `java.util.Map` jusqu’à ce que vous trouviez lʼobjet `com.adobe.idp.Document` généré.
   * Invoquez la méthode `copyToFile` de lʼobjet `com.adobe.idp.Document` afin dʼextraire le portfolio PDF.

**Voir également**

[Didacticiel de mise en route (mode SOAP) : assemblage de portfolios PDF à l’aide de l’API Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-pdf-portfolios-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Assemblage d’un portfolio PDF à l’aide de l’API de service web {#assemble-a-pdf-portfolio-using-the-web-service-api}

Assemblez un portfolio PDF à l’aide de l’API du service Assembler (service web) :

1. Incluez les fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Veillez à utiliser la définition WSDL suivante lors de la définition d’une référence de service : `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un client Assembler PDF.

   * Créez un objet `AssemblerServiceClient` en utilisant son constructeur par défaut.
   * Créez un objet `AssemblerServiceClient.Endpoint.Address` en utilisant le constructeur `System.ServiceModel.EndpointAddress`. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/AssemblerService?blob=mtom`). Vous n’avez pas besoin d’utiliser l’attribut `lc_version`. Cet attribut est utilisé lorsque vous créez une référence de service.
   * Créez un objet `System.ServiceModel.BasicHttpBinding` en récupérant la valeur du champ `AssemblerServiceClient.Endpoint.Binding`. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le champ `MessageEncoding` de l’objet `System.ServiceModel.BasicHttpBinding` sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Référencez un document DX existant.

   * Créez un objet `BLOB` en utilisant son constructeur. L’objet `BLOB` est utilisé pour stocker le document DDX.
   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du document DDX et son mode d’ouverture.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `System.IO.FileStream`. Vous pouvez déterminer la taille du tableau d’octets en obtenant la propriété `Length` de l’objet `System.IO.FileStream`.
   * Renseignez le tableau d’octets avec le flux de données en appelant la méthode `Read` de l’objet `System.IO.FileStream`. Transmettez le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Remplissez lʼobjet `BLOB` en assignant à sa propriété `MTOM` le contenu du tableau dʼoctets.

1. Référencez les documents requis.

   * Pour chaque fichier d’entrée, créez un objet `BLOB` en utilisant son constructeur. Lʼobjet `BLOB` sert à stocker le fichier d’entrée.
   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du fichier d’entrée et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `System.IO.FileStream`. Vous pouvez déterminer la taille du tableau d’octets en obtenant la propriété `Length` de l’objet `System.IO.FileStream`.
   * Renseignez le tableau d’octets avec le flux de données en appelant la méthode `Read` de l’objet `System.IO.FileStream`. Transmettez le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez lʼobjet `BLOB` en attribuant à son champ `MTOM` le contenu du tableau dʼoctets.
   * Créez un objet `MyMapOf_xsd_string_To_xsd_anyType`. Cet objet de collection est utilisé pour stocker les fichiers d’entrée nécessaires à la création d’un portfolio PDF.
   * Pour chaque fichier d’entrée, créez un objet `MyMapOf_xsd_string_To_xsd_anyType_Item`.
   * Attribuez une valeur de chaîne qui représente le nom de la clé au champ `key` de lʼobjet `MyMapOf_xsd_string_To_xsd_anyType_Item`. Cette valeur doit correspondre à la valeur de l’élément spécifié dans le document DDX. (Répétez cette tâche pour chaque fichier d’entrée).
   * Affectez lʼobjet `BLOB` qui stocke le fichier dʼentrée au champ `value` de lʼobjet `MyMapOf_xsd_string_To_xsd_anyType_Item`. (Répétez cette tâche pour chaque document PDF d’entrée).
   * Ajoutez lʼobjet `MyMapOf_xsd_string_To_xsd_anyType_Item` à lʼobjet `MyMapOf_xsd_string_To_xsd_anyType`. Appelez la méthode `Add` de l’objet `MyMapOf_xsd_string_To_xsd_anyType` et transmettez l’objet `MyMapOf_xsd_string_To_xsd_anyType`. (Répétez cette tâche pour chaque document PDF d’entrée).

1. Définissez les options d’exécution.

   * Créez un objet `AssemblerOptionSpec` qui stocke les options d’exécution en utilisant son constructeur.
   * Définissez les options d’exécution pour répondre à vos exigences professionnelles en attribuant une valeur à un membre de données qui appartient à l’objet `AssemblerOptionSpec`. Par exemple, pour demander au service Assembler de poursuivre le traitement dʼune tâche lorsquʼune erreur se produit, affectez `false` au membre de données `failOnError` de lʼobjet `AssemblerOptionSpec`.

1. Assemblez le portfolio.

   Appelez la méthode `invokeDDX` de lʼobjet `AssemblerServiceClient` et transmettez les valeurs suivantes :

   * Objet `BLOB` représentant le document DDX.
   * Objet `MyMapOf_xsd_string_To_xsd_anyType` contenant les fichiers requis.
   * Un objet `AssemblerOptionSpec` qui spécifie les options d’exécution

   La méthode `invokeDDX` renvoie un objet `AssemblerResult` contenant les résultats de la tâche et toutes les exceptions survenues.

1. Enregistrez le portfolio assemblé.

   Pour obtenir le portfolio PDF nouvellement créé, procédez comme suit :

   * Accédez au champ `documents` de lʼobjet `AssemblerResult`, qui est un objet `Map` contenant les documents PDF générés.
   * Effectuez une itération sur l’objet `Map` pour obtenir chaque document généré. Convertissez ensuite l’élément `value` du membre de tableau en `BLOB`.
   * Extrayez les données binaires qui représentent le document PDF en accédant à la propriété `MTOM` de son objet `BLOB`. Cette opération renvoie un tableau d’octets que vous pouvez enregistrer dans un fichier PDF.

**Voir également**

[Appeler AEM Forms en utilisant MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Appel d’AEM Forms à l’aide de SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
