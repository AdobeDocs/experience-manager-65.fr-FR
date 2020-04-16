---
title: Chiffrement et déchiffrement du PDF
seo-title: Chiffrement et déchiffrement du PDF
description: 'null'
seo-description: 'null'
uuid: 4e4e2716-c21f-4bfe-ae7a-7e91442414ef
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 5e4bda3a-5648-4c0f-b2f8-bdbebb88f537
translation-type: tm+mt
source-git-commit: f9389a06f9c2cd720919486765cee76257f272c3

---


# Chiffrement et déchiffrement du PDF {#encrypting-and-decrypting-pdf-documents}

**À propos du service Encryption**

Le service Encryption vous permet de chiffrer et de déchiffrer des  de. Lorsqu’un document est chiffré, son contenu devient illisible. Un utilisateur autorisé peut déchiffrer le document pour accéder à son contenu. Si un document PDF est chiffré avec un mot de passe, l’utilisateur doit spécifier le mot de passe d’ouverture pour pouvoir visualiser le document dans Adobe Reader ou Adobe Acrobat. De même, si un document PDF est chiffré avec un certificat, l’utilisateur doit déchiffrer le document PDF avec la clé publique correspondant au certificat (clé privée) qui a été utilisé pour chiffrer le document PDF.

Vous pouvez accomplir ces  à l’aide du service Encryption :

* Chiffrez un PDF avec un mot de passe. (voir [Chiffrement d’un PDF avec un mot de passe](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)).
* Chiffrez un PDF avec un certificat. (See [Encrypting PDF Documents with Certificates](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-certificates).)
* Supprimez le chiffrement avec mot de passe d’un  PDF. (Voir [Suppression du chiffrement](encrypting-decrypting-pdf-documents.md#removing-password-encryption)de mot de passe.)
* Supprimez le chiffrement avec certificat d’un  PDF. (Voir [Suppression du chiffrement basé sur les certificats](encrypting-decrypting-pdf-documents.md#removing-certificate-based-encryption).)
* Déverrouillez le PDF pour effectuer d’autres opérations de service. Par exemple, une fois qu’un PDF chiffré par mot de passe est déverrouillé, vous pouvez lui appliquer une signature numérique. (Voir [Déverrouillage des](encrypting-decrypting-pdf-documents.md#unlocking-encrypted-pdf-documents)PDF chiffrés.)
* Déterminez le type de chiffrement d’un  PDF sécurisé. (Voir [Détermination du type](encrypting-decrypting-pdf-documents.md#determining-encryption-type)de chiffrement.)

>[!NOTE]
>
>For more information about the Encryption service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Encrypting PDF Documents with a Password {#encrypting-pdf-documents-with-a-password}

Si vous chiffrez un document PDF avec un mot de passe, les utilisateurs devront indiquer ce même mot de passe pour pouvoir ouvrir le document PDF dans Adobe Reader ou Acrobat. Avant qu’une autre opération de pour AEM Forms (signer numérique un document PDF par exemple) puisse être exécutée sur le document, un document PDF chiffré par mot de passe doit être déverrouillé.

>[!NOTE]
>
>Si vous téléchargez un PDF chiffré dans le référentiel AEM Forms, il ne peut pas déchiffrer le PDF  ni extraire le contenu XDP. Il est recommandé de ne pas chiffrer un  avant de le télécharger dans le référentiel AEM Forms. (Voir [Ecriture de ressources](/help/forms/developing/aem-forms-repository.md#writing-resources).)

>[!NOTE]
>
>For more information about the Encryption service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary-of-steps}

Pour chiffrer un PDF avec un mot de passe, procédez comme suit :

1. Incluez des fichiers de projet.
1. Créez un objet API Client Encryption.
1. Obtenez un PDF à chiffrer.
1. Définissez les options d’exécution du chiffrement.
1. Ajouter le mot de passe.
1. Enregistrez le PDF chiffré en tant que fichier PDF.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

Les fichiers JAR suivants doivent être ajoutés au chemin de classe de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar (requis si AEM Forms est déployé sur JBoss)
* jbossall-client.jar (requis si AEM Forms est déployé sur JBoss)

**Création d’un objet API Client Encryption**

Pour exécuter par programmation une opération du service Encryption, vous devez créer un client du service Encryption.

**Obtenir un PDF à chiffrer**

Vous devez obtenir un PDF non chiffré pour chiffrer le  avec un mot de passe. Si vous tentez de sécuriser un PDF déjà chiffré, vous provoquez une exception.

**Définition des options d’exécution du chiffrement**

Pour chiffrer un PDF avec un mot de passe, vous spécifiez quatre valeurs, dont deux valeurs de mot de passe. La première valeur de mot de passe est utilisée pour chiffrer le  du PDF et doit être spécifiée lors de l’ouverture du  du PDF. La deuxième valeur de mot de passe, appelée mot de passe maître, est utilisée pour supprimer le chiffrement du PDF. Les valeurs de mot de passe sont sensibles à la casse et ces deux valeurs de mot de passe ne peuvent pas être identiques.

Vous devez spécifier les ressources  PDF à chiffrer. Vous pouvez chiffrer l’ensemble du PDF, tout sauf les métadonnées de l’ de ou simplement les pièces jointes de l’. Si vous chiffrez uniquement les pièces jointes du , un utilisateur est invité à saisir un mot de passe lorsqu’il tente d’accéder aux pièces jointes.

Lors du chiffrement d’un PDF, vous pouvez spécifier les autorisations associées au sécurisé . En spécifiant des autorisations, vous pouvez contrôler les actions qu’un utilisateur qui ouvre un PDF chiffré par mot de passe est autorisé à effectuer. Par exemple, pour extraire correctement les données de formulaire, vous devez définir les autorisations suivantes :

* PASSWORD_EDIT_ADD
* PASSWORD_EDIT_MODIFY

>[!NOTE]
>
>Les autorisations sont spécifiées en tant que valeurs `PasswordEncryptionPermission` .

**Ajouter le mot de passe**

Une fois que vous avez récupéré un PDF non sécurisé et défini les valeurs d’exécution du chiffrement, vous pouvez ajouter un mot de passe au  du PDF.

**Enregistrer le PDF chiffré en tant que fichier PDF**

Vous pouvez enregistrer le PDF chiffré par mot de passe au format PDF.

**Voir également**

[Chiffrer un PDF à l’aide de l’API Java](encrypting-decrypting-pdf-documents.md#encrypt-a-pdf-document-using-the-java-api)

[Chiffrement d’un PDF à l’aide de l’API du service Web](encrypting-decrypting-pdf-documents.md#encrypting-a-pdf-document-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[rapide de l’API du service de chiffrement](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[Chiffrement des PDF avec des certificats](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-certificates)

### Chiffrer un PDF à l’aide de l’API Java {#encrypt-a-pdf-document-using-the-java-api}

Chiffrez un PDF avec un mot de passe à l’aide de l’API de chiffrement (Java) :

1. Incluez des fichiers de projet.

   Incluez des fichiers JAR client, tels que adobe-encryptage-client.jar, dans le chemin de classe de votre projet Java.

1. Créez une API Client Encryption.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Create an `EncryptionServiceClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. Obtenez un PDF à chiffrer.

   * Créez un `java.io.FileInputStream` objet représentant le PDF à chiffrer à l’aide de son constructeur et transmettez une valeur de chaîne indiquant l’emplacement du  PDF.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Définissez les options d’exécution du chiffrement.

   * Create a `PasswordEncryptionOptionSpec` object by invoking its constructor.
   * Spécifiez les ressources de  PDF à chiffrer en appelant la `PasswordEncryptionOptionSpec` méthode de l’ `setEncryptOption` objet et en transmettant une `PasswordEncryptionOption` valeur  de qui spécifie les ressources de à chiffrer. Par exemple, pour chiffrer l’ensemble du  PDF, y compris ses métadonnées et ses pièces jointes, spécifiez `PasswordEncryptionOption.ALL`.
   * Créez un `java.util.List` objet qui stocke les autorisations de chiffrement à l’aide du `ArrayList` constructeur.
   * Spécifiez une autorisation en appelant la méthode `java.util.List` `add` de l’objet et en transmettant une valeur de  correspondant à l’autorisation que vous souhaitez définir. Par exemple, pour définir l’autorisation permettant à un utilisateur de copier des données situées dans le PDF, spécifiez `PasswordEncryptionPermission.PASSWORD_EDIT_COPY`. (Répétez cette étape pour chaque autorisation à définir).
   * Spécifiez l’option de compatibilité Acrobat en appelant la `PasswordEncryptionOptionSpec` `setCompatability` méthode de l’objet et en transmettant une valeur de  qui spécifie le niveau de compatibilité Acrobat. For example, you can specify `PasswordEncryptionCompatability.ACRO_7`.
   * Spécifiez la valeur du mot de passe qui permet à l’utilisateur d’ouvrir le PDF chiffré en appelant la `PasswordEncryptionOptionSpec` méthode de l’ `setDocumentOpenPassword` objet et en transmettant une valeur de chaîne représentant le mot de passe ouvert.
   * Spécifiez la valeur du mot de passe principal qui permet à un utilisateur de supprimer le chiffrement du PDF en appelant la `PasswordEncryptionOptionSpec` méthode de l’ `setPermissionPassword` objet et en transmettant une valeur de chaîne représentant le mot de passe principal.

1. Ajouter le mot de passe.

   Chiffrez le PDF  en appelant la `EncryptionServiceClient` `encryptPDFUsingPassword` méthode de l’objet et en transmettant les valeurs suivantes :

   * Objet `com.adobe.idp.Document` contenant le PDF à chiffrer avec le mot de passe.
   * Objet `PasswordEncryptionOptionSpec` contenant des options d’exécution de chiffrement.
   La `encryptPDFUsingPassword` méthode renvoie un `com.adobe.idp.Document` objet contenant un PDF chiffré par mot de passe.

1. Enregistrez le PDF chiffré en tant que fichier PDF.

   * Créez un objet `java.io.File` et assurez-vous que l’extension du fichier est .pdf.
   * Invoke the `com.adobe.idp.Document` object’s `copyToFile` method to copy the contents of the `com.adobe.idp.Document` object to the file. Assurez-vous d’utiliser l’objet `com.adobe.idp.Document` qui a été retourné par la méthode `encryptPDFUsingPassword`.

**Voir également**

[Résumé des étapes](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[rapide (mode SOAP) : Chiffrement d’un PDF à l’aide de l’API Java](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-encrypting-a-pdf-document-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Chiffrement d’un PDF à l’aide de l’API du service Web {#encrypting-a-pdf-document-using-the-web-service-api}

Chiffrez un PDF avec un mot de passe à l’aide de l’API Encryption (service Web) :

1. Incluez des fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Veillez à utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un objet API Client Encryption.

   * Créez un `EncryptionServiceClient` objet à l’aide de son constructeur par défaut.
   * Créez un `EncryptionServiceClient.Endpoint.Address` objet à l’aide du `System.ServiceModel.EndpointAddress` constructeur. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/EncryptionService?WSDL`). Vous n’avez pas besoin d’utiliser l’ `lc_version` attribut. Cet attribut est utilisé lorsque vous créez une référence de service.)
   * Créez un `System.ServiceModel.BasicHttpBinding` objet en obtenant la valeur du `EncryptionServiceClient.Endpoint.Binding` champ. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le `System.ServiceModel.BasicHttpBinding` champ de l’ `MessageEncoding` objet sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant le  suivant :

      * Attribuez le nom d’utilisateur d’AEM forms au champ `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Obtenez un PDF à chiffrer.

   * Créez un objet `BLOB` en utilisant son constructeur. L’ `BLOB` objet est utilisé pour stocker un PDF chiffré avec un mot de passe.
   * Créez un `System.IO.FileStream` objet en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du fichier du PDF à chiffrer et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’ `System.IO.FileStream` objet. Vous pouvez déterminer la taille du tableau d’octets en obtenant la `System.IO.FileStream` `Length` propriété de l’objet.
   * Renseignez le tableau d’octets avec les données de flux en appelant la `System.IO.FileStream` `Read` méthode de l’objet et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’ `BLOB` objet en affectant le contenu du tableau d’octets au membre `BLOB` `MTOM` de données de l’objet.

1. Définissez les options d’exécution du chiffrement.

   * Créez un objet `PasswordEncryptionOptionSpec` en utilisant son constructeur.
   * Spécifiez les ressources de  PDF à chiffrer en attribuant une `PasswordEncryptionOption` valeur  au membre `PasswordEncryptionOptionSpec` `encryptOption` de données de l’objet. Pour chiffrer l’intégralité du fichier PDF, y compris ses métadonnées et ses pièces jointes, affectez-lui `PasswordEncryptionOption.ALL` le.
   * Spécifiez l’option de compatibilité Acrobat en attribuant une `PasswordEncryptionCompatability` valeur  au membre `PasswordEncryptionOptionSpec` `compatability` de données de l’objet. Par exemple, affectez- `PasswordEncryptionCompatability.ACRO_7` vous à ce membre de données.
   * Spécifiez la valeur du mot de passe qui permet à l’utilisateur d’ouvrir le PDF chiffré en attribuant une valeur de chaîne représentant le mot de passe ouvert au membre `PasswordEncryptionOptionSpec` `documentOpenPassword` de données de l’objet.
   * Spécifiez la valeur du mot de passe qui permet à un utilisateur de supprimer le chiffrement du PDF en attribuant une valeur de chaîne représentant le mot de passe maître au membre de `PasswordEncryptionOptionSpec` `permissionPassword` données de l’objet.

1. Ajouter le mot de passe.

   Chiffrez le PDF  en appelant la `EncryptionServiceClient` `encryptPDFUsingPassword` méthode de l’objet et en transmettant les valeurs suivantes :

   * Objet `BLOB` contenant le PDF à chiffrer avec le mot de passe.
   * Objet `PasswordEncryptionOptionSpec` contenant des options d’exécution de chiffrement.
   La `encryptPDFUsingPassword` méthode renvoie un `BLOB` objet contenant un PDF chiffré par mot de passe.

1. Enregistrez le PDF chiffré en tant que fichier PDF.

   * Créez un `System.IO.FileStream` objet en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du fichier du PDF sécurisé.
   * Créez un tableau d’octets qui stocke le contenu des données de l’ `BLOB` objet renvoyé par la `encryptPDFUsingPassword` méthode. Renseignez le tableau d’octets en obtenant la valeur du membre `BLOB` `MTOM` de données de l’objet.
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * Ecrivez le contenu du tableau d’octets dans un fichier PDF en appelant la `System.IO.BinaryWriter` `Write` méthode de l’objet et en transmettant le tableau d’octets.

**Voir également**

[Résumé des étapes](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Appel d’AEM Forms à l’aide de MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Appel d’AEM Forms à l’aide de SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Encrypting PDF Documents with Certificates {#encrypting-pdf-documents-with-certificates}

Le chiffrement avec certificat vous permet de chiffrer un pour des spécifiques au moyen de la technologie de clé publique. Différents destinataires peuvent recevoir différents droits pour le document. De nombreux aspects de chiffrement sont possibles grâce à la technologie de clé publique. An algorithm is used to generate two large numbers, known as *keys*, that have the following properties:

* Une clé est utilisée pour chiffrer un ensemble de données. Par la suite, seule l’autre clé peut être utilisée pour déchiffrer les données.
* Il est impossible de distinguer une clé d’une autre.

L’une des clés agit comme la clé privée d’un utilisateur. Il est important que seul l’utilisateur ait accès à cette clé. L’autre clé est la clé publique de l’utilisateur, qui peut être partagée avec d’autres personnes.

Un certificat de clé publique contient la clé publique d’un utilisateur et des informations d’identification. Le format X.509 est utilisé pour le stockage de certificats. Les certificats sont généralement émis et signés numériquement par une autorité de certification, qui est une entité reconnue qui garantit la validité du certificat. Les certificats comportent une date d’expiration ; au-delà de cette date, ils ne sont plus valides. En outre, les listes de révocation des certificats (CRL) fournissent des informations sur les certificats révoqués avant leur date d’expiration. Les listes CRL sont modifiées régulièrement par des autorités de certification. Vous pouvez également récupérer l’état de révocation d’un certificat par l’intermédiaire du protocole OCSP (Online Certificate Status Protocol, protocole d’état de certificat en ligne) sur le réseau.

>[!NOTE]
>
>Si vous téléchargez un PDF chiffré dans le référentiel AEM Forms, il ne peut pas déchiffrer le PDF  ni extraire le contenu XDP. Il est recommandé de ne pas chiffrer un  avant de le télécharger dans le référentiel AEM Forms. (Voir [Ecriture de ressources](/help/forms/developing/aem-forms-repository.md#writing-resources).)

>[!NOTE]
>
>Avant de chiffrer un PDF avec un certificat, vous devez vous assurer d’ajouter le certificat à AEM Forms. Un certificat est ajouté à l’aide d’Administration Console ou par programmation à l’aide de l’API Trust Manager. (voir [Importation des informations d’identification à l’aide de l’API](/help/forms/developing/credentials.md#importing-credentials-by-using-the-trust-manager-api)Trust Manager).

>[!NOTE]
>
>For more information about the Encryption service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary_of_steps-1}

Pour chiffrer un PDF avec un certificat, procédez comme suit :

1. Incluez des fichiers de projet.
1. Créez un objet API Client Encryption.
1. Obtenez un PDF à chiffrer.
1. Référencez le certificat.
1. Définissez les options d’exécution du chiffrement.
1. Créez un PDF chiffré par certificat.
1. Enregistrez le PDF chiffré en tant que fichier PDF.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

Les fichiers JAR suivants doivent être ajoutés au chemin de classe de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar (requis si AEM Forms est déployé sur JBoss Application Server)
* jbossall-client.jar (requis si AEM Forms est déployé sur JBoss Application Server)

**Création d’un objet API Client Encryption**

Pour exécuter par programmation une opération du service Encryption, vous devez créer un client du service Encryption. Si vous utilisez l’API Java Encryption Service, créez un `EncrytionServiceClient` objet. Si vous utilisez l’API du service Web Encryption Service, créez un `EncryptionServiceService` objet.

**Obtenir un PDF à chiffrer**

Vous devez obtenir un PDF non chiffré pour le chiffrer. Si vous tentez de sécuriser un PDF déjà chiffré, une exception est générée.

**Référencer le certificat**

Pour chiffrer un PDF avec un certificat, référencez un certificat utilisé pour chiffrer un  PDF. Le certificat est un fichier .cer, un fichier .crt ou un fichier .pem. Un fichier PKCS#12 est utilisé pour stocker des clés privées avec les certificats correspondants.

Lors du chiffrement d’un PDF  d’un certificat, spécifiez les autorisations associées au  du sécurisé. En spécifiant des autorisations, vous pouvez contrôler les actions qu’un utilisateur qui ouvre un PDF chiffré par certificat peut effectuer.

**Définition des options d’exécution du chiffrement**

Spécifiez les ressources de PDF à chiffrer. Vous pouvez chiffrer l’ensemble du PDF, tout ce qui est , à l’exception des métadonnées du , ou uniquement les pièces jointes du.

**Création d’un PDF chiffré par certificat**

Après avoir récupéré un  PDF non sécurisé, référencé le certificat et défini les options d’exécution, vous pouvez créer un PDF chiffré par certificat . Une fois le PDF chiffré, vous avez besoin de la clé publique correspondante pour le déchiffrer.

**Enregistrer le PDF chiffré en tant que fichier PDF**

Vous pouvez enregistrer le PDF chiffré en tant que fichier PDF.

**Voir également**

[Chiffrer un PDF avec un certificat à l’aide de l’API Java](encrypting-decrypting-pdf-documents.md#encrypt-a-pdf-document-with-a-certificate-using-the-java-api)

[Chiffrer un PDF avec un certificat à l’aide de l’API du service Web](encrypting-decrypting-pdf-documents.md#encrypt-a-pdf-document-with-a-certificate-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[rapide de l’API du service de chiffrement](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[Chiffrement du PDF avec un mot de passe](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### Chiffrer un PDF avec un certificat à l’aide de l’API Java {#encrypt-a-pdf-document-with-a-certificate-using-the-java-api}

Chiffrez un PDF avec un certificat à l’aide de l’API de chiffrement (Java) :

1. Incluez des fichiers de projet.

   Incluez des fichiers JAR client, tels que adobe-encryptage-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un objet API Client Encryption.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Create an `EncryptionServiceClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. Obtenez un PDF à chiffrer.

   * Créez un `java.io.FileInputStream` objet représentant le PDF à chiffrer à l’aide de son constructeur et transmettez une valeur de chaîne indiquant l’emplacement du  PDF.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Référencez le certificat.

   * Créez un `java.util.List` objet qui stocke les informations d’autorisation à l’aide de son constructeur.
   * Spécifiez l’autorisation associée au chiffré en appelant la `java.util.List` méthode de l’ `add` objet et en transmettant une `CertificateEncryptionPermissions` valeur  qui représente les autorisations accordées à l’utilisateur qui ouvre la  PDF sécurisée. Par exemple, pour spécifier toutes les autorisations, transmettez `CertificateEncryptionPermissions.PKI_ALL_PERM`.
   * Créez un objet `Recipient` en utilisant son constructeur.
   * Créez un `java.io.FileInputStream` objet représentant le certificat utilisé pour chiffrer le PDF à l’aide de son constructeur et transmettez une valeur de chaîne indiquant l’emplacement du certificat.
   * Créez un `com.adobe.idp.Document` objet en utilisant son constructeur et en transmettant l’ `java.io.FileInputStream` objet qui représente le certificat.
   * Appelez la `Recipient` méthode de l’ `setX509Cert` objet et transmettez l’ `com.adobe.idp.Document` objet qui contient le certificat. (En outre, l’ `Recipient`objet peut avoir un alias de certificat Truststore ou une URL LDAP comme source de certificat.)
   * Créez un `CertificateEncryptionIdentity` objet qui stocke les informations d’autorisation et de certificat à l’aide de son constructeur.
   * Appelez la `CertificateEncryptionIdentity` méthode de l’ `setPerms` objet et transmettez l’ `java.util.List` objet qui stocke les informations d’autorisation.
   * Appelez la `CertificateEncryptionIdentity` méthode de l’ `setRecipient` objet et transmettez l’ `Recipient` objet qui stocke les informations de certificat.
   * Créez un `java.util.List` objet qui stocke les informations de certificat à l’aide de son constructeur.
   * Invoke the `java.util.List` object’s add method and pass the `CertificateEncryptionIdentity` object. (Cet `java.util.List` objet est transmis en tant que paramètre à la `encryptPDFUsingCertificates` méthode.)

1. Définissez les options d’exécution du chiffrement.

   * Create a `CertificateEncryptionOptionSpec` object by invoking its constructor.
   * Spécifiez les ressources de  PDF à chiffrer en appelant la `CertificateEncryptionOptionSpec` méthode de l’ `setOption` objet et en transmettant une `CertificateEncryptionOption` valeur  de qui spécifie les ressources de à chiffrer. Par exemple, pour chiffrer l’ensemble du  PDF, y compris ses métadonnées et ses pièces jointes, spécifiez `CertificateEncryptionOption.ALL`.
   * Spécifiez l’option de compatibilité Acrobat en appelant la `CertificateEncryptionOptionSpec` méthode de l’ `setCompat` objet et en transmettant une valeur de `CertificateEncryptionCompatibility` qui spécifie le niveau de compatibilité Acrobat. For example, you can specify `CertificateEncryptionCompatibility.ACRO_7`.

1. Créez un PDF chiffré par certificat.

   Chiffrez le PDF avec un certificat en appelant la `EncryptionServiceClient` `encryptPDFUsingCertificates` méthode de l’objet et en transmettant les valeurs suivantes :

   * Objet `com.adobe.idp.Document` contenant le PDF à chiffrer.
   * Objet `java.util.List` qui stocke les informations de certificat.
   * Objet `CertificateEncryptionOptionSpec` contenant des options d’exécution de chiffrement.
   La `encryptPDFUsingCertificates` méthode renvoie un `com.adobe.idp.Document` objet contenant un PDF chiffré par certificat.

1. Enregistrez le PDF chiffré en tant que fichier PDF.

   * Create a `java.io.File` object and ensure that the file name extension is .pdf.
   * Invoke the `com.adobe.idp.Document` object’s `copyToFile` method to copy the contents of the `com.adobe.idp.Document` object to the file. Assurez-vous d’utiliser l’objet `com.adobe.idp.Document` qui a été retourné par la méthode `encryptPDFUsingCertificates`.

**Voir également**

[Résumé des étapes](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[rapide (mode SOAP) : Chiffrement d’un PDF avec un certificat à l’aide de l’API Java](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-encrypting-a-pdf-document-with-a-certificate-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Chiffrer un PDF avec un certificat à l’aide de l’API du service Web {#encrypt-a-pdf-document-with-a-certificate-using-the-web-service-api}

Chiffrez un PDF avec un certificat à l’aide de l’API Encryption (service Web) :

1. Incluez des fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Veillez à utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un objet API Client Encryption.

   * Créez un `EncryptionServiceClient` objet à l’aide de son constructeur par défaut.
   * Créez un `EncryptionServiceClient.Endpoint.Address` objet à l’aide du `System.ServiceModel.EndpointAddress` constructeur. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/EncryptionService?WSDL`). Vous n’avez pas besoin d’utiliser l’ `lc_version` attribut. Cet attribut est utilisé lorsque vous créez une référence de service.)
   * Créez un `System.ServiceModel.BasicHttpBinding` objet en obtenant la valeur du `EncryptionServiceClient.Endpoint.Binding` champ. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le `System.ServiceModel.BasicHttpBinding` champ de l’ `MessageEncoding` objet sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant le  suivant :

      * Attribuez le nom d’utilisateur d’AEM forms au champ `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Obtenez un PDF à chiffrer.

   * Créez un objet `BLOB` en utilisant son constructeur. L’ `BLOB` objet est utilisé pour stocker un PDF chiffré avec un certificat.
   * Créez un `System.IO.FileStream` objet en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du fichier du PDF à chiffrer et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’ `System.IO.FileStream` objet. Vous pouvez déterminer la taille du tableau d’octets en obtenant la `System.IO.FileStream` `Length` propriété de l’objet.
   * Renseignez le tableau d’octets avec les données de flux en appelant la `System.IO.FileStream` `Read` méthode de l’objet et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’ `BLOB` objet en affectant sa `MTOM` propriété au contenu du tableau d’octets.

1. Référencez le certificat.

   * Créez un objet `Recipient` en utilisant son constructeur. Cet objet stocke les informations de certificat.
   * Créez un objet `BLOB` en utilisant son constructeur. Cet `BLOB` objet stocke le certificat qui chiffre le PDF.
   * Créez un `System.IO.FileStream` objet en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du fichier du certificat et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’ `System.IO.FileStream` objet. Vous pouvez déterminer la taille du tableau d’octets en obtenant la `System.IO.FileStream` `Length` propriété de l’objet.
   * Renseignez le tableau d’octets avec les données de flux en appelant la `System.IO.FileStream` `Read` méthode de l’objet et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’ `BLOB` objet en affectant le contenu du tableau d’octets au membre `BLOB` `MTOM` de données de l’objet.
   * Affectez l’ `BLOB` objet qui stocke le certificat au membre `Recipient` de données de l’ `x509Cert` objet.
   * Créez un `CertificateEncryptionIdentity` objet qui stocke les informations de certificat à l’aide de son constructeur.
   * Affectez l’ `Recipient` objet qui stocke le certificat au membre de données du de l’ `CertificateEncryptionIdentity`objet.
   * Créez un `Object` tableau et affectez l’ `CertificateEncryptionIdentity` objet au premier élément du `Object` tableau. Ce `Object` tableau est transmis en tant que paramètre à la `encryptPDFUsingCertificates` méthode.

1. Définissez les options d’exécution du chiffrement.

   * Créez un objet `CertificateEncryptionOptionSpec` en utilisant son constructeur.
   * Spécifiez les ressources de  PDF à chiffrer en attribuant une `CertificateEncryptionOption` valeur  au membre `CertificateEncryptionOptionSpec` `option` de données de l’objet. Pour chiffrer l’ensemble des  du PDF, y compris ses métadonnées et ses pièces jointes, affectez-les `CertificateEncryptionOption.ALL` à ce membre de données.
   * Spécifiez l’option de compatibilité Acrobat en attribuant une `CertificateEncryptionCompatibility` valeur  au membre `CertificateEncryptionOptionSpec` de données de l’ `compat` objet. Par exemple, affectez- `CertificateEncryptionCompatibility.ACRO_7` vous à ce membre de données.

1. Créez un PDF chiffré par certificat.

   Chiffrez le PDF avec un certificat en appelant la `EncryptionServiceService` `encryptPDFUsingCertificates` méthode de l’objet et en transmettant les valeurs suivantes :

   * Objet `BLOB` contenant le PDF à chiffrer.
   * Tableau `Object` contenant les informations de certificat.
   * Objet `CertificateEncryptionOptionSpec` contenant des options d’exécution de chiffrement.
   La `encryptPDFUsingCertificates` méthode renvoie un `BLOB` objet contenant un PDF chiffré par certificat.

1. Enregistrez le PDF chiffré en tant que fichier PDF.

   * Créez un `System.IO.FileStream` objet en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du fichier du PDF sécurisé.
   * Créez un tableau d’octets qui stocke le contenu des données de l’ `BLOB` objet renvoyé par la `encryptPDFUsingCertificates` méthode. Renseignez le tableau d’octets en obtenant la valeur du membre `BLOB` `binaryData` de données de l’objet.
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * Ecrivez le contenu du tableau d’octets dans un fichier PDF en appelant la `System.IO.BinaryWriter` `Write` méthode de l’objet et en transmettant le tableau d’octets.

**Voir également**

[Résumé des étapes](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Appel d’AEM Forms à l’aide de MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Appel d’AEM Forms à l’aide de SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Removing Certificate Based Encryption {#removing-certificate-based-encryption}

Le chiffrement avec certificat peut être supprimé d’un PDF afin que les utilisateurs puissent ouvrir le PDF  dans Adobe Reader ou Acrobat. Pour supprimer le chiffrement d’un PDF chiffré avec un certificat, une clé publique doit être référencée. Une fois le chiffrement supprimé d’un  PDF, il n’est plus sécurisé.

>[!NOTE]
>
>For more information about the Encryption service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary_of_steps-2}

Pour supprimer le chiffrement avec certificat d’un  PDF, procédez comme suit :

1. Incluez des fichiers de projet.
1. Créez un client de service de chiffrement.
1. Obtenez le  PDF chiffré.
1. Supprimez le chiffrement.
1. Enregistrez le  PDF au format PDF.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

Les fichiers JAR suivants doivent être ajoutés au chemin de classe de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar (requis si AEM Forms est déployé sur JBoss Application Server)
* jbossall-client.jar (requis si AEM Forms est déployé sur JBoss Application Server)

**Création d’un client de service de chiffrement**

Pour exécuter par programmation une opération du service Encryption, vous devez créer un client du service Encryption. Si vous utilisez l’API Java Encryption Service, créez un `EncrytionServiceClient` objet. Si vous utilisez l’API du service Web Encryption Service, créez un `EncryptionServiceService` objet.

**Obtention du PDF chiffré**

Vous devez obtenir un PDF chiffré pour supprimer le chiffrement basé sur un certificat. Si vous tentez de supprimer le chiffrement d’un PDF non chiffré, une exception est générée. De même, si vous tentez de supprimer le chiffrement avec certificat d’un chiffré par mot de passe, une exception est générée.

**Supprimer le chiffrement**

Pour supprimer le chiffrement avec certificat d’un PDF chiffré, vous avez besoin d’un PDF chiffré et d’une clé privée qui correspond à la clé utilisée pour chiffrer lePDF . La valeur d’alias de la clé privée est spécifiée lors de la suppression du chiffrement avec certificat d’un PDF chiffré. Pour plus d’informations sur la clé publique, voir [Chiffrement d’un PDF avec des certificats](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-certificates).

>[!NOTE]
>
>Une clé privée est stockée dans le Trust Store d’AEM Forms. Lorsqu’un certificat y est placé, une valeur d’alias est spécifiée.

**Enregistrer le PDF**

Une fois le chiffrement basé sur un certificat supprimé d’un PDF chiffré, vous pouvez enregistrer le PDF  au format PDF. Les utilisateurs peuvent ouvrir le  PDF dans Adobe Reader ou Acrobat.

**Voir également**

[Suppression du chiffrement avec certificat à l’aide de l’API Java](encrypting-decrypting-pdf-documents.md#remove-certificate-based-encryption-using-the-java-api)

[Suppression du chiffrement avec certificat à l’aide de l’API de service Web](encrypting-decrypting-pdf-documents.md#remove-certificate-based-encryption-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[rapide de l’API du service de chiffrement](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

### Suppression du chiffrement avec certificat à l’aide de l’API Java {#remove-certificate-based-encryption-using-the-java-api}

Supprimez le chiffrement avec certificat d’un PDF à l’aide de l’API de chiffrement (Java) :

1. Incluez des fichiers de projet.

   Incluez des fichiers JAR client, tels que adobe-encryptage-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un client de service de chiffrement.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Create an `EncryptionServiceClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. Obtenez le  PDF chiffré.

   * Créez un `java.io.FileInputStream` objet représentant le PDF chiffré en utilisant son constructeur et en transmettant une valeur de chaîne indiquant l’emplacement du PDF chiffré .
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Supprimez le chiffrement.

   Supprimez le chiffrement avec certificat du PDF en appelant la `EncryptionServiceClient` `removePDFCertificateSecurity` méthode de l’objet et en transmettant les valeurs suivantes :

   * Objet `com.adobe.idp.Document` contenant le  PDF chiffré.
   * Valeur de chaîne qui spécifie le nom d’alias de la clé privée qui correspond à la clé utilisée pour chiffrer le  PDf.
   La `removePDFCertificateSecurity` méthode renvoie un `com.adobe.idp.Document` objet contenant un  PDF non sécurisé.

1. Enregistrez le  PDF.

   * Créez un objet `java.io.File` et assurez-vous que l’extension du fichier est .pdf.
   * Invoke the `com.adobe.idp.Document` object’s `copyToFile` method to copy the contents of the `Document` object to the file. Assurez-vous d’utiliser l’objet `com.adobe.idp.Document` qui a été retourné par la méthode `removePDFCredentialSecurity`.

**Voir également**

[Résumé des étapes](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[rapide (mode SOAP) : Suppression du chiffrement avec certificat à l’aide de l’API Java](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-removing-certificate-based-encryption-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Suppression du chiffrement avec certificat à l’aide de l’API de service Web {#remove-certificate-based-encryption-using-the-web-service-api}

Supprimez le chiffrement avec certificat à l’aide de l’API Encryption (service Web) :

1. Incluez des fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Veillez à utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un client de service de chiffrement.

   * Créez un `EncryptionServiceClient` objet à l’aide de son constructeur par défaut.
   * Créez un `EncryptionServiceClient.Endpoint.Address` objet à l’aide du `System.ServiceModel.EndpointAddress` constructeur. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/EncryptionService?WSDL`). Vous n’avez pas besoin d’utiliser l’ `lc_version` attribut. Cet attribut est utilisé lorsque vous créez une référence de service.)
   * Créez un `System.ServiceModel.BasicHttpBinding` objet en obtenant la valeur du `EncryptionServiceClient.Endpoint.Binding` champ. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le `System.ServiceModel.BasicHttpBinding` champ de l’ `MessageEncoding` objet sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant le  suivant :

      * Attribuez le nom d’utilisateur d’AEM forms au champ `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Obtenez le  PDF chiffré.

   * Créez un objet `BLOB` en utilisant son constructeur. L’ `BLOB` objet est utilisé pour stocker le  PDF chiffré.
   * Créez un `System.IO.FileStream` objet en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du fichier du PDF chiffré et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’ `System.IO.FileStream` objet. Vous pouvez déterminer la taille du tableau d’octets en obtenant la `System.IO.FileStream` `Length` propriété de l’objet.
   * Renseignez le tableau d’octets avec les données de flux en appelant la `System.IO.FileStream` `Read` méthode de l’objet et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’ `BLOB` objet en affectant le contenu du tableau d’octets au membre `BLOB` `MTOM` de données de l’objet.

1. Supprimez le chiffrement.

   Appelez la méthode `EncryptionServiceClient` `removePDFCertificateSecurity` de l’objet et transmettez les valeurs suivantes :

   * Objet `BLOB` contenant des données de flux de fichiers représentant un PDF chiffré.
   * Valeur de chaîne qui spécifie le nom d’alias de la clé publique correspondant à la clé privée utilisée pour chiffrer le  PDf.
   La `removePDFCredentialSecurity` méthode renvoie un `BLOB` objet contenant un  PDF non sécurisé.

1. Enregistrez le  PDF.

   * Créez un `System.IO.FileStream` objet en appelant son constructeur et en transmettant une valeur de chaîne représentant l’emplacement du fichier du  PDF non sécurisé.
   * Créez un tableau d’octets qui stocke le contenu de l’ `BLOB` objet renvoyé par la `removePDFPasswordSecurity` méthode. Renseignez le tableau d’octets en obtenant la valeur du membre `BLOB` `MTOM` de données de l’objet.
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * Ecrivez le contenu du tableau d’octets dans un fichier PDF en appelant la `System.IO.BinaryWriter` `Write` méthode de l’objet et en transmettant le tableau d’octets.

**Voir également**

[Résumé des étapes](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Appel d’AEM Forms à l’aide de MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Appel d’AEM Forms à l’aide de SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Suppression du chiffrement de mot de passe {#removing-password-encryption}

Le chiffrement avec mot de passe peut être supprimé d’un PDF afin que les utilisateurs puissent ouvrir le PDF  dans Adobe Reader ou Acrobat sans avoir à spécifier de mot de passe. Une fois le chiffrement avec mot de passe supprimé d’un PDF, le n’est plus sécurisé.

>[!NOTE]
>
>For more information about the Encryption service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary_of_steps-3}

Pour supprimer le chiffrement avec mot de passe d’un  PDF, procédez comme suit :

1. Inclure les fichiers de projet
1. Créez un client de service de chiffrement.
1. Obtenez le  PDF chiffré.
1. Supprimez le mot de passe.
1. Enregistrez le  PDF au format PDF.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

Les fichiers JAR suivants doivent être ajoutés au chemin de classe de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar (requis si AEM Forms est déployé sur JBoss)
* jbossall-client.jar (requis si AEM Forms est déployé sur JBoss)

**Création d’un client de service de chiffrement**

Pour exécuter par programmation une opération du service Encryption, vous devez créer un client du service Encryption. Si vous utilisez l’API Java Encryption Service, créez un `EncrytionServiceClient` objet. Si vous utilisez l’API du service Web Encryption Service, créez un `EncryptionServiceService` objet.

**Obtention du PDF chiffré**

Vous devez obtenir un PDF chiffré pour supprimer le chiffrement avec mot de passe. Si vous tentez de supprimer le chiffrement d’un PDF non chiffré, une exception est générée.

**Supprimer le mot de passe**

Pour supprimer le chiffrement avec mot de passe d’un PDF chiffré, vous devez disposer d’un PDF chiffré et d’une valeur de mot de passe maître qui permet de supprimer le chiffrement de l’ PDF. Le mot de passe utilisé pour ouvrir un PDF chiffré par mot de passe ne peut pas être utilisé pour supprimer le chiffrement. Un mot de passe principal est spécifié lorsque le PDF est chiffré avec un mot de passe. (voir [Chiffrement d’un PDF avec un mot de passe](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)).

**Enregistrer le PDF**

Une fois que le service Encryption a supprimé le chiffrement avec mot de passe d’un PDF, vous pouvez enregistrer le PDF  sous forme de fichier PDF. Les utilisateurs peuvent ouvrir le PDF dans Adobe Reader ou Acrobat sans spécifier de mot de passe.

**Voir également**

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[rapide de l’API du service de chiffrement](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[Chiffrement du PDF avec un mot de passe](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### Suppression du chiffrement avec mot de passe à l’aide de l’API Java {#remove-password-based-encryption-using-the-java-api}

Supprimez le chiffrement avec mot de passe d’un PDF à l’aide de l’API de chiffrement (Java) :

1. Incluez des fichiers de projet.

   Incluez des fichiers JAR client, tels que adobe-encryptage-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un client de service de chiffrement.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Create an `EncryptionServiceClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. Obtenez le  PDF chiffré.

   * Créez un `java.io.FileInputStream` objet représentant le PDF chiffré en utilisant son constructeur et en transmettant une valeur de chaîne indiquant l’emplacement du PDF .
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Supprimez le mot de passe.

   Supprimez le chiffrement avec mot de passe du PDF en appelant la `EncryptionServiceClient` `removePDFPasswordSecurity` méthode de l’objet et en transmettant les valeurs suivantes :

   * Objet `com.adobe.idp.Document` contenant le PDF chiffré.
   * Valeur de chaîne qui spécifie la valeur du mot de passe maître utilisée pour supprimer le chiffrement du PDF.
   La `removePDFPasswordSecurity` méthode renvoie un `com.adobe.idp.Document` objet contenant un  PDF non sécurisé.

1. Enregistrez le  PDF.

   * Create a `java.io.File` object and ensure that the file name extension is .pdf.
   * Invoke the `com.adobe.idp.Document` object’s `copyToFile` method to copy the contents of the `Document` object to the file. Assurez-vous d’utiliser l’objet `Document` qui a été retourné par la méthode `removePDFPasswordSecurity`.

**Voir également**

[rapide (mode SOAP) : Suppression du chiffrement par mot de passe à l’aide de l’API Java](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-removing-password-based-encryption-using-the-java-api)

### Suppression du chiffrement avec mot de passe à l’aide de l’API du service Web {#remove-password-based-encryption-using-the-web-service-api}

Supprimez le chiffrement avec mot de passe à l’aide de l’API Encryption (service Web) :

1. Incluez des fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Veillez à utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un client de service de chiffrement.

   * Créez un `EncryptionServiceClient` objet à l’aide de son constructeur par défaut.
   * Créez un `EncryptionServiceClient.Endpoint.Address` objet à l’aide du `System.ServiceModel.EndpointAddress` constructeur. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/EncryptionService?WSDL`). Vous n’avez pas besoin d’utiliser l’ `lc_version` attribut. Cet attribut est utilisé lorsque vous créez une référence de service.)
   * Créez un `System.ServiceModel.BasicHttpBinding` objet en obtenant la valeur du `EncryptionServiceClient.Endpoint.Binding` champ. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le `System.ServiceModel.BasicHttpBinding` champ de l’ `MessageEncoding` objet sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant le  suivant :

      * Attribuez le nom d’utilisateur d’AEM forms au champ `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Obtenez le  PDF chiffré.

   * Créez un objet `BLOB` en utilisant son constructeur. L’ `BLOB` objet est utilisé pour stocker un PDF chiffré par mot de passe.
   * Créez un `System.IO.FileStream` objet en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du fichier du PDF chiffré et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’ `System.IO.FileStream` objet. Vous pouvez déterminer la taille du tableau d’octets en obtenant la `System.IO.FileStream` `Length` propriété de l’objet.
   * Renseignez le tableau d’octets avec les données de flux en appelant la `System.IO.FileStream` `Read` méthode de l’objet et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’ `BLOB` objet en affectant le contenu du tableau d’octets au membre `BLOB` `MTOM` de données de l’objet.

1. Supprimez le mot de passe.

   Appelez la méthode `EncryptionServiceService` `removePDFPasswordSecurity` de l’objet et transmettez les valeurs suivantes :

   * Objet `BLOB` contenant des données de flux de fichiers représentant un PDF chiffré.
   * Valeur de chaîne qui spécifie la valeur du mot de passe utilisée pour supprimer le chiffrement du PDF. Cette valeur est spécifiée lors du chiffrement du PDF avec un mot de passe.
   La `removePDFPasswordSecurity` méthode renvoie un `BLOB` objet contenant un  PDF non sécurisé.

1. Enregistrez le  PDF.

   * Créez un `System.IO.FileStream` objet en appelant son constructeur et en transmettant une valeur de chaîne représentant l’emplacement du fichier du  PDF non sécurisé.
   * Créez un tableau d’octets qui stocke le contenu de l’ `BLOB` objet renvoyé par la `removePDFPasswordSecurity` méthode. Renseignez le tableau d’octets en obtenant la valeur du membre `BLOB` `MTOM` de données de l’objet.
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * Ecrivez le contenu du tableau d’octets dans un fichier PDF en appelant la `System.IO.BinaryWriter` `Write` méthode de l’objet et en transmettant le tableau d’octets.

**Voir également**

[Appel d’AEM Forms à l’aide de MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Appel d’AEM Forms à l’aide de SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Déverrouillage du PDF chiffré {#unlocking-encrypted-pdf-documents}

Un PDF chiffré par mot de passe ou par certificat doit être déverrouillé avant qu’une autre opération AEM Forms ne puisse être effectuée sur celui-ci. Si vous tentez d’effectuer une opération sur un  PDF chiffré, vous générez une exception. Une fois que vous avez déverrouillé un PDF chiffré, vous pouvez y effectuer une ou plusieurs opérations. Ces opérations peuvent appartenir à d’autres services, tels qu’Acrobat Reader DC Extensions Service.

>[!NOTE]
>
>For more information about the Encryption service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary_of_steps-4}

Pour déverrouiller un PDF chiffré, procédez comme suit :

1. Incluez des fichiers de projet.
1. Créez un client de service de chiffrement.
1. Obtenez le  PDF chiffré.
1. Déverrouillez le .
1. Exécutez une opération AEM Forms.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

Les fichiers JAR suivants doivent être ajoutés au chemin de classe de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar (requis si AEM Forms est déployé sur JBoss Application Server)
* jbossall-client.jar (requis si AEM Forms est déployé sur JBoss Application Server)

**Création d’un client de service de chiffrement**

Pour exécuter par programmation une opération du service Encryption, vous devez créer un client du service Encryption. Si vous utilisez l’API Java Encryption Service, créez un `EncrytionServiceClient` objet. Si vous utilisez l’API du service Web Encryption Service, créez un `EncryptionServiceService` objet.

**Obtention du PDF chiffré**

Vous devez obtenir un PDF chiffré pour le déverrouiller. Si vous tentez de déverrouiller un PDF non chiffré, une exception est générée.

**Déverrouiller le**

Pour déverrouiller un PDF chiffré par mot de passe, vous avez besoin d’un PDF chiffré  et d’une valeur de mot de passe qui permet d’ouvrir un  PDF chiffré par mot de passe. Cette valeur est spécifiée lors du chiffrement du PDF avec un mot de passe. (voir [Chiffrement d’un PDF avec un mot de passe](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)).

Pour déverrouiller un PDF chiffré par certificat, vous devez disposer d’un PDF chiffré et de la valeur d’alias de la clé publique correspondant à la clé privée utilisée pour chiffrer le PDF.

**Exécution d’une opération AEM Forms**

Une fois qu’un PDF chiffré est déverrouillé, vous pouvez y effectuer une autre opération de service, par exemple lui appliquer des droits d’utilisation. Cette opération appartient au service Acrobat Reader DC Extensions.

**Voir également**

[Déverrouiller un PDF chiffré à l’aide de l’API Java](encrypting-decrypting-pdf-documents.md#unlock-an-encrypted-pdf-document-using-the-java-api)

[Déverrouiller un PDF chiffré à l’aide de l’API du service Web](encrypting-decrypting-pdf-documents.md#unlock-an-encrypted-pdf-document-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[rapide de l’API du service de chiffrement](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

### Déverrouiller un PDF chiffré à l’aide de l’API Java {#unlock-an-encrypted-pdf-document-using-the-java-api}

Déverrouillez un PDF chiffré à l’aide de l’API Encryption (Java) :

1. Incluez des fichiers de projet.

   Incluez des fichiers JAR client, tels que adobe-encryptage-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un client de service de chiffrement.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Create an `EncryptionServiceClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. Obtenez le  PDF chiffré.

   * Créez un `java.io.FileInputStream` objet représentant le PDF chiffré en utilisant son constructeur et en transmettant une valeur de chaîne indiquant l’emplacement du PDF chiffré .
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Déverrouillez le .

   Déverrouillez un PDF chiffré en appelant la méthode `EncryptionServiceClient` ou `unlockPDFUsingPassword` `unlockPDFUsingCredential` de l’objet.

   Pour déverrouiller un PDF chiffré avec un mot de passe, appelez la `unlockPDFUsingPassword` méthode et transmettez les valeurs suivantes :

   * Objet `com.adobe.idp.Document` contenant le PDF chiffré par mot de passe.
   * Valeur de chaîne qui spécifie la valeur du mot de passe utilisée pour ouvrir un PDF chiffré par mot de passe. Cette valeur est spécifiée lors du chiffrement du PDF avec un mot de passe.
   Pour déverrouiller un PDF chiffré avec un certificat, appelez la `unlockPDFUsingCredential` méthode et transmettez les valeurs suivantes :

   * A `com.adobe.idp.Document` object that contains the certificate-encrypted PDF document.
   * Valeur de chaîne qui spécifie le nom d’alias de la clé publique correspondant à la clé privée utilisée pour chiffrer le PDF.
   Les méthodes `unlockPDFUsingPassword` et `unlockPDFUsingCredential` renvoient toutes deux un `com.adobe.idp.Document` objet que vous transmettez à une autre méthode Java AEM Forms pour effectuer une opération.

1. Exécutez une opération AEM Forms.

   Effectuez une opération AEM Forms sur le  PDF déverrouillé pour répondre aux besoins de votre entreprise. Par exemple, si vous souhaitez appliquer des droits d’utilisation à un PDF déverrouillé, transmettez l’ `com.adobe.idp.Document` objet renvoyé par les méthodes `unlockPDFUsingPassword` ou `unlockPDFUsingCredential` à la `ReaderExtensionsServiceClient` `applyUsageRights` méthode de l’objet.

**Voir également**

[Résumé des étapes](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[rapide (mode SOAP) : Déverrouillage d’un PDF chiffré à l’aide de l’API](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-unlocking-an-encrypted-pdf-document-using-the-java-api) Java (mode SOAP)

[Application des droits d’utilisation aux PDF](/help/forms/developing/assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Déverrouiller un PDF chiffré à l’aide de l’API du service Web {#unlock-an-encrypted-pdf-document-using-the-web-service-api}

Déverrouillez un PDF chiffré à l’aide de l’API Encryption (service Web) :

1. Incluez des fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Veillez à utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un client de service de chiffrement.

   * Créez un `EncryptionServiceClient` objet à l’aide de son constructeur par défaut.
   * Créez un `EncryptionServiceClient.Endpoint.Address` objet à l’aide du `System.ServiceModel.EndpointAddress` constructeur. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/EncryptionService?WSDL`). Vous n’avez pas besoin d’utiliser l’ `lc_version` attribut. Cet attribut est utilisé lorsque vous créez une référence de service.)
   * Créez un `System.ServiceModel.BasicHttpBinding` objet en obtenant la valeur du `EncryptionServiceClient.Endpoint.Binding` champ. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le `System.ServiceModel.BasicHttpBinding` champ de l’ `MessageEncoding` objet sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant le  suivant :

      * Attribuez le nom d’utilisateur d’AEM forms au champ `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Obtenez un PDF chiffré.

   * Créez un objet `BLOB` en utilisant son constructeur.
   * Créez un `System.IO.FileStream` objet en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du fichier du PDF chiffré et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’ `System.IO.FileStream` objet. Vous pouvez déterminer la taille du tableau d’octets en obtenant la `System.IO.FileStream` `Length` propriété de l’objet.
   * Renseignez le tableau d’octets avec les données de flux en appelant la `System.IO.FileStream` `Read` méthode de l’objet et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’ `BLOB` objet en affectant le contenu du tableau d’octets au membre `BLOB` `MTOM` de données de l’objet.

1. Déverrouillez le .

   Déverrouillez un PDF chiffré en appelant la méthode `EncryptionServiceClient` ou `unlockPDFUsingPassword` `unlockPDFUsingCredential` de l’objet.

   Pour déverrouiller un PDF chiffré avec un mot de passe, appelez la `unlockPDFUsingPassword` méthode et transmettez les valeurs suivantes :

   * Objet `BLOB` contenant le PDF chiffré par mot de passe.
   * Valeur de chaîne qui spécifie la valeur du mot de passe utilisée pour ouvrir un PDF chiffré par mot de passe. Cette valeur est spécifiée lors du chiffrement du PDF avec un mot de passe.
   Pour déverrouiller un PDF chiffré avec un certificat, appelez la `unlockPDFUsingCredential` méthode et transmettez les valeurs suivantes :

   * A `BLOB` object that contains the certificate-encrypted PDF document.
   * Valeur de chaîne qui spécifie le nom d’alias de la clé publique correspondant à la clé privée utilisée pour chiffrer le  PDf.
   Les méthodes `unlockPDFUsingPassword` et `unlockPDFUsingCredential` renvoient toutes deux un `com.adobe.idp.Document` objet que vous transmettez à une autre méthode AEM Forms pour effectuer une opération.

1. Exécutez une opération AEM Forms.

   Effectuez une opération AEM Forms sur le  PDF déverrouillé pour répondre aux besoins de votre entreprise. Par exemple, si vous souhaitez appliquer des droits d’utilisation au  PDF déverrouillé, transmettez l’ `BLOB` objet renvoyé par les méthodes `unlockPDFUsingPassword` ou `unlockPDFUsingCredential` à la `ReaderExtensionsServiceClient` `applyUsageRights` méthode de l’objet.

**Voir également**

[Résumé des étapes](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Appel d’AEM Forms à l’aide de MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Appel d’AEM Forms à l’aide de SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Détermination du type de chiffrement {#determining-encryption-type}

Vous pouvez déterminer par programmation le type de chiffrement qui protège un PDF à l’aide de l’API Java Encryption Service ou de l’API du service Web Encryption Service. Il est parfois nécessaire de déterminer de manière dynamique si un PDF est chiffré et, dans l’affirmative, le type de chiffrement. Par exemple, vous pouvez déterminer si un PDF est protégé par un chiffrement avec mot de passe ou par une stratégie Rights Management.

Un PDF peut être protégé par les types de chiffrement suivants :

* Chiffrement par mot de passe
* Chiffrement basé sur un certificat
* Stratégie créée par le service Rights Management
* Autre type de chiffrement

>[!NOTE]
>
>For more information about the Encryption service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary_of_steps-5}

Pour déterminer le type de chiffrement qui protège un PDF, procédez comme suit :

1. Incluez des fichiers de projet.
1. Créez un client de service de chiffrement.
1. Obtenez le  PDF chiffré.
1. Déterminez le type de chiffrement.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

Les fichiers JAR suivants doivent être ajoutés au chemin de classe de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar (requis si AEM Forms est déployé sur JBoss Application Server)
* jbossall-client.jar (requis si AEM Forms est déployé sur JBoss Application Server)

**Création d’un client de service**

Pour exécuter par programmation une opération du service Encryption, vous devez créer un client du service Encryption. Si vous utilisez l’API Java Encryption Service, créez un `EncrytionServiceClient` objet. Si vous utilisez l’API du service Web Encryption Service, créez un `EncryptionServiceService` objet.

**Obtention du PDF chiffré**

Vous devez obtenir un PDF pour déterminer le type de chiffrement qui le protège.

**Détermination du type de chiffrement**

Vous pouvez déterminer le type de chiffrement qui protège un  PDF. Si le  PDF n’est pas protégé, le service Encryption vous informe que le PDF n’est pas sécurisé.

**Voir également**

[Détermination du type de chiffrement à l’aide de l’API Java](encrypting-decrypting-pdf-documents.md#determine-the-encryption-type-using-the-java-api)

[Détermination du type de chiffrement à l’aide de l’API du service Web](encrypting-decrypting-pdf-documents.md#determine-the-encryption-type-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[rapide de l’API du service de chiffrement](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[Protection des  par des stratégies](/help/forms/developing/protecting-documents-policies.md#protecting-documents-with-policies)

### Détermination du type de chiffrement à l’aide de l’API Java {#determine-the-encryption-type-using-the-java-api}

Déterminez le type de chiffrement qui protège un PDF à l’aide de l’API de chiffrement (Java) :

1. Incluez des fichiers de projet.

   Incluez des fichiers JAR client, tels que adobe-encryptage-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un client de service.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Create an `EncryptionServiceClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. Obtenez le  PDF chiffré.

   * Créez un `java.io.FileInputStream` objet représentant le PDF à l’aide de son constructeur et transmettez une valeur de chaîne indiquant l’emplacement du  du PDF.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Déterminez le type de chiffrement.

   * Déterminez le type de chiffrement en appelant la `EncryptionServiceClient` méthode de l’ `getPDFEncryption` objet et en transmettant l’ `com.adobe.idp.Document` objet contenant le  PDF. Cette méthode renvoie un `EncryptionTypeResult` objet.
   * Appelez la méthode `EncryptionTypeResult` `getEncryptionType` de l’objet. Cette méthode renvoie une valeur `EncryptionType` enum qui spécifie le type de chiffrement. Par exemple, si le PDF est protégé par un chiffrement avec mot de passe, cette méthode renvoie `EncryptionType.PASSWORD`.

**Voir également**

[Résumé des étapes](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[rapide (mode SOAP) : Détermination du type de chiffrement à l’aide de l’API Java](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-determining-encryption-type-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Détermination du type de chiffrement à l’aide de l’API du service Web {#determine-the-encryption-type-using-the-web-service-api}

Déterminez le type de chiffrement qui protège un PDF à l’aide de l’API Encryption (service Web) :

1. Incluez des fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Veillez à utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un client de service.

   * Créez un `EncryptionServiceClient` objet à l’aide de son constructeur par défaut.
   * Créez un `EncryptionServiceClient.Endpoint.Address` objet à l’aide du `System.ServiceModel.EndpointAddress` constructeur. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/EncryptionService?WSDL`). Vous n’avez pas besoin d’utiliser l’ `lc_version` attribut. Cet attribut est utilisé lorsque vous créez une référence de service.)
   * Créez un `System.ServiceModel.BasicHttpBinding` objet en obtenant la valeur du `EncryptionServiceClient.Endpoint.Binding` champ. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le `System.ServiceModel.BasicHttpBinding` champ de l’ `MessageEncoding` objet sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant le  suivant :

      * Attribuez le nom d’utilisateur d’AEM forms au champ `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Obtenez le  PDF chiffré.

   * Créez un objet `BLOB` en utilisant son constructeur.
   * Créez un `System.IO.FileStream` objet en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du fichier du PDF chiffré et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’ `System.IO.FileStream` objet. Vous pouvez déterminer la taille du tableau d’octets en obtenant la `System.IO.FileStream` `Length` propriété de l’objet.
   * Renseignez le tableau d’octets avec les données de flux en appelant la `System.IO.FileStream` `Read` méthode de l’objet et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’ `BLOB` objet en affectant le contenu du tableau d’octets au membre `BLOB` `MTOM` de données de l’objet.

1. Déterminez le type de chiffrement.

   * Appelez la `EncryptionServiceClient` méthode de l’ `getPDFEncryption` objet et transmettez l’ `BLOB` objet qui contient le  PDF. Cette méthode renvoie un `EncryptionTypeResult` objet.
   * Obtenez la valeur de la méthode `EncryptionTypeResult` `encryptionType` de données de l’objet. Par exemple, si le  PDF est protégé par un chiffrement avec mot de passe, la valeur de ce membre de données est `EncryptionType.PASSWORD`.

**Voir également**

[Résumé des étapes](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Appel d’AEM Forms à l’aide de MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Appel d’AEM Forms à l’aide de SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)