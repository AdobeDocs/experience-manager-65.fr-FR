---
title: Assemblage de  PDF avec des signets
seo-title: Assemblage de  PDF avec des signets
description: 'null'
seo-description: 'null'
uuid: a306d2a6-0b12-4eb3-bff4-968a33417486
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 9f4711a8-033c-4051-ab41-65a26838899b
translation-type: tm+mt
source-git-commit: e3f700b52446505224fa4b4688d439750a66f471

---


# Assemblage de  PDF avec des signets {#assembling-pdf-documents-with-bookmarks}

Vous pouvez assembler un PDF qui contient des signets. Supposons, par exemple, que vous disposiez d’un PDF qui ne contient aucun signet et que vous souhaitiez le modifier en fournissant des signets. Le service Assembler vous permet de lui transmettre un PDF qui ne contient pas de signets et de récupérer un PDF qui contient des signets.

Les signets contiennent les propriétés suivantes :

* Titre qui s’affiche sous forme de texte à l’écran.
* Action qui spécifie ce qui se produit lorsqu’un utilisateur clique sur le signet. L’action type d’un signet consiste à se déplacer vers un autre emplacement du actuel ou à ouvrir un autre  PDF, bien que d’autres actions puissent être spécifiées.

Aux fins de cette discussion, supposons que le DDX suivant soit utilisé.

```as3
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
       <PDF result="FinalDoc.pdf">
          <PDF source="Loan.pdf">
             <Bookmarks source="doc2" />
          </PDF>
       </PDF>
 </DDX>
```

Dans ce  DDX, notez que la valeur est affectée à l’attribut source `Loan.pdf`. Ce DDX  spécifie qu’un seul PDF est transmis au service Assembler. Lors de l’assemblage d’un PDF  de signets, vous devez spécifier un XML de signets qui décrit les signets dans l’ de résultats. Pour spécifier un  XML de signet, assurez-vous que l’ `Bookmarks` élément est spécifié dans votre  DDX.

Dans cet exemple de  DDX, l’ `Bookmarks` élément spécifie `doc2` comme valeur. Cette valeur indique que la carte d’entrée transmise au service Assembler contient une clé nommée `doc2`. La valeur de la `doc2` clé est une `com.adobe.idp.Document` valeur qui représente le XML du signet. (Voir &quot;Langage des signets&quot; dans le Guide de référence [du service](https://www.adobe.com/go/learn_aemforms_ddx_63)Assembler et du DDX.)

Cette rubrique utilise le langage de signets XML suivant pour assembler un PDF contenant des signets.

```as3
 <?xml version="1.0" encoding="UTF-8"?>
 <Bookmarks xmlns="https://ns.adobe.com/pdf/bookmarks" version="1.0">
       <Bookmark>
          <Action>
             <Launch NewWindow="true">
                <File Name="C:\Adobe\LoanDetails.pdf" />
             </Launch>
          </Action>
         <Title>Open the Loan document</Title>
       </Bookmark>
 <Bookmark>
          <Action>
             <Launch>
                <Win Name="C:\WINDOWS\notepad.exe" />
             </Launch>
          </Action>
     <Title>Launch NotePad</Title>
       </Bookmark>
 </Bookmarks>
```

Dans ce XML de signets, notez l’élément Action qui définit l’action exécutée lorsqu’un utilisateur clique sur le signet. Sous l’élément Action se trouve l’élément Launch qui lance des applications, telles que NotePad, et ouvre des fichiers, tels que des fichiers PDF. Pour ouvrir un fichier PDF, vous devez utiliser l’élément Fichier qui spécifie le fichier à ouvrir. Par exemple, dans le fichier XML du signet spécifié dans cette section, le nom du fichier ouvert est LoanDetails.pdf.

>[!NOTE]
>
>Pour plus d’informations sur les actions prises en charge, voir &quot; `Action` element&quot; dans le Guide de référence [du service](https://www.adobe.com/go/learn_aemforms_ddx_63)Assembler et du DDX.

Compte tenu du  DDX spécifié dans cette section et du fichier XML de signet comme entrée, le service Assembler assemble un PDF  qui contient les signets suivants.

![aw_aw_bmark](assets/aw_aw_bmark.png)

Lorsqu&#39;un utilisateur clique sur le signet *Ouvrir les détails* du prêt, le fichier LoanDetails.pdf est ouvert. De même, lorsque l’utilisateur clique sur le signet *Lancer NotePad* , NotePad est démarré.

>[!NOTE]
>
>Avant de lire cette section, nous vous recommandons de vous familiariser avec l’assemblage de PDF à l’aide du service Assembler. Cette section ne traite pas des concepts, tels que la création d’un objet de collection contenant des  d’entrée ou l’apprentissage de l’extraction des résultats de l’objet de collection renvoyé. (Voir [Assemblage par programmation de](/help/forms/developing/programmatically-assembling-pdf-documents.md#programmatically-assembling-pdf-documents)PDF.)

>[!NOTE]
>
>For more information about the Assembler service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Pour plus d’informations sur un  DDX, voir [Service Assembler et Référence](https://www.adobe.com/go/learn_aemforms_ddx_63)DDX.

## Résumé des étapes {#summary-of-steps}

Pour assembler un  PDF contenant des signets, effectuez l’ de suivante :

1. Incluez des fichiers de projet.
1. Créez un client PDF Assembler.
1. Référencez un  DDX existant.
1. Référencez un PDF auquel des signets sont ajoutés.
1. Référencez les  XML du signet.
1. Ajouter l’ PDF et lesignet XML à une collection Map.
1. Définissez les options d’exécution.
1. Assemblez le  PDF.
1. Enregistrez le PDF qui contient des signets.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

Les fichiers JAR suivants doivent être ajoutés au chemin de classe de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (requis si AEM Forms est déployé sur JBoss)
* jbossall-client.jar (requis si AEM Forms est déployé sur JBoss)

si AEM Forms est déployé sur un serveur d’applications J2EE pris en charge autre que JBoss, vous devez remplacer les fichiers adobe-utilities.jar et jbossall-client.jar par des fichiers JAR spécifiques au serveur d’applications J2EE sur lequel AEM Forms est déployé. For information about the location of all AEM Forms JAR files, see [Including AEM Forms Java library files](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Création d’un client PDF Assembler**

Avant de pouvoir exécuter une opération Assembler par programmation, vous devez créer un client de service Assembler.

**Référencer un DDX existant**

Un  DDX doit être référencé pour assembler un  PDF. Ce DDX doit contenir l’ `Bookmarks` élément qui demande au service Assembler d’assembler un PDF contenant des signets. (Voir le  DDX illustré plus haut dans cette section pour un exemple.)

**Référence à un PDF auquel des signets sont ajoutés**

Référencez un PDF auquel des signets sont ajoutés. Peu importe que le PDF référencé  déjà contient des signets. Si l’ `Bookmarks` élément est un enfant de l’élément source PDF, les signets remplaceront ceux qui existent déjà dans la source PDF. Toutefois, si vous souhaitez conserver les signets existants, assurez-vous qu’ `Bookmarks` il s’agit d’un frère de l’élément source PDF. Prenons l’exemple suivant :

```as3
 <PDF result="foo">
      <PDF source="inDoc"/>
      <Bookmarks source="doc2"/>
 </PDF>
```

**Référence au XML de signets**

Pour assembler un PDF contenant de nouveaux signets, vous devez référencer un XML de signets. Le XML du signet est transmis au service Assembler dans l’objet de collection Map. (Voir le XML en signet illustré plus haut dans cette section pour un exemple.)

>[!NOTE]
>
>Voir &quot;Langue des signets&quot; dans le Guide de référence [du service](https://www.adobe.com/go/learn_aemforms_ddx_63)Assembler et du DDX.

**Ajouter l’ PDF et lesignet XML de l’ à une collection Map**

Vous devez ajouter le PDF auquel les signets sont ajoutés et le XML de signets à la collection Map. Par conséquent, l’objet de collection Map contient deux éléments : un PDF et le XML de signets.

**Définition des options d’exécution**

Vous pouvez définir des options d’exécution qui contrôlent le comportement du service Assembler lorsqu’il effectue une tâche. Par exemple, vous pouvez définir une option qui indique au service Assembler de poursuivre le traitement d’une tâche en cas d’erreur. Pour plus d’informations sur les options d’exécution que vous pouvez définir, voir la référence de `AssemblerOptionSpec` classe dans Référence [API](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)AEM Forms.

**Assemblage du PDF**

Pour assembler un  PDF contenant de nouveaux signets, utilisez l’ `invokeDDX` opération du service Assembler. La raison pour laquelle vous devez utiliser l’ `invokeDDX` opération par rapport à d’autres opérations du service Assembler, telles `invokeOneDocument` que les opérations du service Assembler, est que le service Assembler nécessite un XML en signet transmis dans l’objet de collection Map. Cet objet est un paramètre de l’ `invokeDDX` opération.

**Enregistrer le PDF contenant des signets**

Vous devez extraire les résultats de l’objet de mappage renvoyé et enregistrer le PDF correspondant. (voir la section &quot;Extraction des résultats&quot; dans [Assemblage par programmation de](/help/forms/developing/programmatically-assembling-pdf-documents.md)PDF).

**Voir également**

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Assemblage par programmation de PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Assemblage de  PDF avec des signets à l’aide de l’API Java {#assemble-pdf-documents-with-bookmarks-using-the-java-api}

Assemblage d’un PDF avec des signets à l’aide de l’API du service Assembler (Java) :

1. Incluez des fichiers de projet.

   Incluez des fichiers JAR client, tels que adobe-assembler-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un client PDF Assembler.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion. (Voir [Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
   * Create an `AssemblerServiceClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. Référencez un  DDX existant.

   * Créez un `java.io.FileInputStream` objet qui représente le  DDX en utilisant son constructeur et en transmettant une valeur de chaîne qui spécifie l’emplacement du fichier DDX.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Référencez un PDF auquel des signets sont ajoutés.

   * Créez un `java.io.FileInputStream` objet en utilisant son constructeur et en transmettant l’emplacement du PDF.
   * Créez un `com.adobe.idp.Document` objet à l’aide de son constructeur et transmettez l’ `java.io.FileInputStream` objet qui contient le  PDF.

1. Référencez les  XML du signet.

   * Créez un `java.io.FileInputStream` objet à l’aide de son constructeur et en transmettant l’emplacement du fichier XML représentant le XML du signet.
   * Créez un `com.adobe.idp.Document` objet et transmettez l’ `java.io.FileInputStream` objet contenant le  PDF.

1. Ajouter l’ PDF et lesignet XML à une collection Map.

   * Créez un `java.util.Map` objet utilisé pour stocker le  PDF d’entrée et le XML de signets.
   * Ajouter le PDF d’entrée  en appelant la `java.util.Map` `put` méthode de l’objet et en transmettant les arguments suivants :

      * Valeur de chaîne qui représente le nom de la clé. Cette valeur doit correspondre à la valeur de l’élément source PDF spécifié dans le  DDX.
      * Objet `com.adobe.idp.Document` contenant le  PDF d’entrée.
   * Ajouter le XML du signet  en appelant la `java.util.Map` `put` méthode de l’objet et en transmettant les arguments suivants :

      * Valeur de chaîne qui représente le nom de la clé. Cette valeur doit correspondre à la valeur de l’élément source Signets spécifié dans le  DDX.
      * Objet `com.adobe.idp.Document` contenant le  XML du signet.


1. Définissez les options d’exécution.

   * Créez un `AssemblerOptionSpec` objet qui stocke les options d’exécution à l’aide de son constructeur.
   * Définissez des options d’exécution pour répondre aux besoins de votre entreprise en appelant une méthode qui appartient à l’ `AssemblerOptionSpec` objet. Par exemple, pour demander au service Assembler de poursuivre le traitement d’une tâche en cas d’erreur, appelez la `AssemblerOptionSpec` méthode de l’ `setFailOnError` objet et transmettez-la `false`.

1. Assemblez le  PDF.

   Appelez la méthode `AssemblerServiceClient` `invokeDDX` de l’objet et transmettez les valeurs requises suivantes :

   * Objet `com.adobe.idp.Document` représentant le DDX  à utiliser
   * Objet `java.util.Map` contenant à la fois le  PDF d’entrée et le XML de signets.
   * Objet `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` spécifiant les options d’exécution, notamment la police par défaut et le niveau du journal des tâches
   La `invokeDDX` méthode renvoie un `com.adobe.livecycle.assembler.client.AssemblerResult` objet qui contient les résultats de la tâche et les exceptions survenues.

1. Enregistrez le PDF qui contient des signets.

   Pour obtenir le nouveau  PDF, effectuez les actions suivantes :

   * Appelez la méthode `AssemblerResult` `getDocuments` de l’objet. Renvoie un `java.util.Map` objet.
   * Effectuez une itération sur l’ `java.util.Map` objet jusqu’à ce que vous trouviez l’ `com.adobe.idp.Document` objet résultant. (Vous pouvez utiliser l’élément de résultat PDF spécifié dans le  DDX pour obtenir le  de.)
   * Appelez la méthode `com.adobe.idp.Document` `copyToFile` de l’objet pour extraire le PDF.

**Voir également**

[rapide (mode SOAP) : Assemblage de  PDF avec des signets à l’aide de l’API Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-pdf-documents-with-bookmarks-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Assemblage de  PDF avec des signets à l’aide de l’API du service Web {#assemble-pdf-documents-with-bookmarks-using-the-web-service-api}

Assemblez un PDF  de signets à l’aide de l’API du service Assembler (service Web) :

1. Incluez des fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Veillez à utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un client PDF Assembler.

   * Créez un `AssemblerServiceClient` objet à l’aide de son constructeur par défaut.
   * Créez un `AssemblerServiceClient.Endpoint.Address` objet à l’aide du `System.ServiceModel.EndpointAddress` constructeur. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/AssemblerService?blob=mtom`). Vous n’avez pas besoin d’utiliser l’ `lc_version` attribut. Cet attribut est utilisé lorsque vous créez une référence de service.
   * Créez un `System.ServiceModel.BasicHttpBinding` objet en obtenant la valeur du `AssemblerServiceClient.Endpoint.Binding` champ. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le `System.ServiceModel.BasicHttpBinding` champ de l’ `MessageEncoding` objet sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant le  suivant :

      * Attribuez le nom d’utilisateur d’AEM forms au champ `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Référencez un  DDX existant.

   * Créez un objet `BLOB` en utilisant son constructeur. L’ `BLOB` objet est utilisé pour stocker le  DDX.
   * Créez un `System.IO.FileStream` objet en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du fichier du  DDX et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’ `System.IO.FileStream` objet. Vous pouvez déterminer la taille du tableau d’octets en obtenant la `System.IO.FileStream` `Length` propriété de l’objet.
   * Renseignez le tableau d’octets avec les données de flux en appelant la `System.IO.FileStream` `Read` méthode de l’objet et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’ `BLOB` objet en affectant son `MTOM` champ au contenu du tableau d’octets.

1. Référencez un PDF auquel des signets sont ajoutés.

   * Créez un objet `BLOB` en utilisant son constructeur. L’ `BLOB` objet est utilisé pour stocker le PDF d’entrée.
   * Créez un `System.IO.FileStream` objet en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du fichier du PDF d’entrée et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’ `System.IO.FileStream` objet. Vous pouvez déterminer la taille du tableau d’octets en obtenant la `System.IO.FileStream` `Length` propriété de l’objet.
   * Renseignez le tableau d’octets avec les données de flux en appelant la `System.IO.FileStream` `Read` méthode de l’objet et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’ `BLOB` objet en affectant son `MTOM` champ au contenu du tableau d’octets.

1. Référencez les  XML du signet.

   * Créez un objet `BLOB` en utilisant son constructeur. L’ `BLOB` objet est utilisé pour stocker le XML du signet.
   * Créez un `System.IO.FileStream` objet en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du fichier du PDF d’entrée et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’ `System.IO.FileStream` objet. Vous pouvez déterminer la taille du tableau d’octets en obtenant la `System.IO.FileStream` `Length` propriété de l’objet.
   * Renseignez le tableau d’octets avec les données de flux en appelant la `System.IO.FileStream` `Read` méthode de l’objet et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’ `BLOB` objet en affectant son `MTOM` champ au contenu du tableau d’octets.

1. Ajouter l’ PDF et lesignet XML à une collection Map.

   * Create a `MyMapOf_xsd_string_To_xsd_anyType` object. Cet objet de collection est utilisé pour stocker le  PDF d’entrée et le XML de signets.
   * Pour chaque  PDF d’entrée et le XML de signets, créez un `MyMapOf_xsd_string_To_xsd_anyType_Item` objet.
   * Attribuez une valeur de chaîne représentant le nom de la clé au `MyMapOf_xsd_string_To_xsd_anyType_Item` `key` champ de l’objet. Cette valeur doit correspondre à la valeur de l’élément source PDF spécifié dans le  DDX.
   * Affectez l’ `BLOB` objet qui stocke le  PDF au `MyMapOf_xsd_string_To_xsd_anyType_Item` `value` champ de l’objet.
   * Ajouter l’ `MyMapOf_xsd_string_To_xsd_anyType_Item` objet à l’ `MyMapOf_xsd_string_To_xsd_anyType` objet. Invoke the `MyMapOf_xsd_string_To_xsd_anyType` object&#39;s `Add` method and pass the `MyMapOf_xsd_string_To_xsd_anyType` object. (Effectuez ce  pour chaque  PDF d’entrée et pour chaque  XML de signet.)

1. Définissez les options d’exécution.

   * Créez un `AssemblerOptionSpec` objet qui stocke les options d’exécution à l’aide de son constructeur.
   * Définissez des options d’exécution pour répondre aux besoins de votre entreprise en attribuant une valeur à un membre de données qui appartient à l’ `AssemblerOptionSpec` objet. Par exemple, pour demander au service Assembler de poursuivre le traitement d’une tâche en cas d’erreur, affectez `false` au membre `AssemblerOptionSpec` `failOnError` de données de l’objet.

1. Assemblez le  PDF.

   Appelez la méthode `AssemblerServiceClient` `invokeDDX` de l’objet et transmettez les valeurs suivantes :

   * Objet `BLOB` représentant le DDX 
   * Le `MyMapOf_xsd_string_To_xsd_anyType` tableau qui contient le d’entrée 
   * Objet `AssemblerOptionSpec` spécifiant les options d’exécution
   La `invokeDDX` méthode renvoie un `AssemblerResult` objet qui contient les résultats de la tâche et toutes les exceptions qui peuvent s’être produites.

1. Enregistrez le PDF qui contient des signets.

   Pour obtenir le nouveau  PDF, effectuez les actions suivantes :

   * Accédez au `AssemblerResult` champ de l’ `documents` objet, qui est un `Map` objet contenant le  PDF obtenu.
   * Effectuez une itération sur l’ `Map` objet jusqu’à ce que vous trouviez la clé qui correspond au nom du  de résultant. Jetez ensuite le numéro `value` de l’élément de tableau sur un `BLOB`.
   * Extrayez les données binaires qui représentent le PDF en accédant au `BLOB` champ de son `MTOM` objet. Cette opération renvoie un tableau d’octets que vous pouvez écrire dans un fichier PDF.

**Voir également**

[Appel d’AEM Forms à l’aide de MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
