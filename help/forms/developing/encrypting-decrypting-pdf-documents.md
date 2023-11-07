---
title: Chiffrer et déchiffrer des documents PDF
seo-title: Encrypting and Decrypting PDF Documents
description: Utilisez le service Encryption pour chiffrer et déchiffrer des documents. Les tâches du service Encryption incluent le chiffrement de documents PDF par mot de passe, le chiffrement de documents PDF par certificat, la suppression du chiffrement par mot de passe de documents PDF, la suppression du chiffrement par certificat de documents PDF, le déverrouillage de documents PDF afin que d’autres opérations de service puissent être effectuées et la détermination du type de chiffrement de documents PDF sécurisés.
seo-description: Use the Encryption service to encrypt and decrypt documents. The Encryption service tasks include encrypting a PDF document with a password, encrypting a PDF document with a certificate, removing password-based encryption from a PDF document, removing certificate-based encryption from a PDF document, unlocking the PDF document so that other service operations can be performed, and determining the encryption type of a secured PDF document.
uuid: 4e4e2716-c21f-4bfe-ae7a-7e91442414ef
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 5e4bda3a-5648-4c0f-b2f8-bdbebb88f537
role: Developer
exl-id: d3cbca7f-9277-4d61-b198-abf4bb008f15
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '8184'
ht-degree: 97%

---

# Chiffrer et déchiffrer des documents PDF {#encrypting-and-decrypting-pdf-documents}

**Les exemples et les échantillons de ce document sont réservés à l’environnement AEM Forms sur JEE.**

**À propos du service Encryption**

Le service Encryption vous donne la possibilité de chiffrer et de déchiffrer des documents. Lorsqu’un document est chiffré, son contenu devient illisible. Un utilisateur autorisé peut déchiffrer le document pour accéder au contenu. Si un document PDF est chiffré avec un mot de passe, l’utilisateur doit spécifier le mot de passe d’ouverture pour pouvoir visualiser le document dans Adobe Reader ou Adobe Acrobat. De même, si un document de PDF est chiffré avec un certificat, l’utilisateur doit déchiffrer le document de PDF avec la clé publique correspondant au certificat (clé privée) utilisé pour chiffrer le document de PDF.

Vous pouvez accomplir les tâches suivantes à l’aide du service Encryption :

* Chiffrez un document de PDF avec un mot de passe. (Voir [Chiffrer des documents PDF avec un mot de passe](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password).)
* Chiffrez un document PDF avec un certificat. (Voir [Chiffrer des documents PDF avec des certificats](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-certificates).)
* Supprimez le chiffrement par mot de passe d’un document PDF. (Voir [Supprimer le chiffrement par mot de passe](encrypting-decrypting-pdf-documents.md#removing-password-encryption).)
* Supprimez le chiffrement par certificat d’un document PDF. (Voir [Supprimer le chiffrement par certificat](encrypting-decrypting-pdf-documents.md#removing-certificate-based-encryption).)
* Déverrouillez le document PDF afin que d’autres opérations de service puissent être effectuées. Par exemple, après le déverrouillage d’un document PDF chiffré par mot de passe, vous pouvez lui appliquer une signature numérique. (Voir [Déverrouiller un document PDF chiffré](encrypting-decrypting-pdf-documents.md#unlocking-encrypted-pdf-documents).)
* Déterminez le type de chiffrement d’un document PDF sécurisé. (Voir [Déterminer le type de chiffrement](encrypting-decrypting-pdf-documents.md#determining-encryption-type).)

>[!NOTE]
>
>Pour plus d’informations sur le service Encryption, voir [Références des services pour AEM Forms](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

## Chiffrer des documents PDF avec un mot de passe {#encrypting-pdf-documents-with-a-password}

Si vous chiffrez un document PDF avec un mot de passe, les utilisateurs devront indiquer ce même mot de passe pour pouvoir ouvrir le document PDF dans Adobe Reader ou Acrobat. Avant qu’une autre opération de pour AEM Forms (signer numérique un document PDF par exemple) puisse être exécutée sur le document, un document PDF chiffré par mot de passe doit être déverrouillé.

>[!NOTE]
>
>Si vous téléchargez un document PDF chiffré dans le référentiel AEM Forms, ce dernier ne pourra pas déchiffrer le document PDF et extraire le contenu XDP. Il est recommandé de ne pas chiffrer un document avant de le charger dans le référentiel AEM Forms. (Voir [Écriture de ressources](/help/forms/developing/aem-forms-repository.md#writing-resources).)

>[!NOTE]
>
>Pour plus d’informations sur le service Encryption, voir [Références des services pour AEM Forms](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

### Résumé des étapes {#summary-of-steps}

Pour chiffrer un document PDF avec un mot de passe, procédez comme suit :

1. Incluez les fichiers de projet.
1. Créez un objet API client Encryption.
1. Obtenez un document PDF à chiffrer.
1. Définissez les options d’exécution du chiffrement.
1. Ajoutez le mot de passe.
1. Enregistrez le document PDF chiffré en tant que fichier PDF.

**Inclure des fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

Les fichiers JAR suivants doivent être ajoutés au chemin d’accès aux classes de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utility.jar (obligatoire si AEM Forms est déployé sur JBoss)
* jbossall-client.jar (obligatoire si AEM Forms est déployé sur JBoss)

**Créer un objet API client Encryption**

Pour effectuer par programmation une opération de service Encryption, vous devez créer un client de service Encryption.

**Obtenir un document PDF à chiffrer**

Vous devez obtenir un document PDF non chiffré pour chiffrer le document avec un mot de passe. Si vous essayez de sécuriser un document PDF déjà chiffré, une exception sera générée.

**Définir les options d’exécution du chiffrement**

Pour chiffrer un document PDF avec un mot de passe, vous devez indiquer quatre valeurs, dont deux valeurs de mot de passe. La première valeur de mot de passe est utilisée pour chiffrer le document PDF et doit être indiquée lors de l’ouverture du document PDF. La deuxième valeur de mot de passe, encore appelée valeur de mot de passe principale, est utilisée pour supprimer le chiffrement du document PDF. Les valeurs de mot de passe sont sensibles à la casse et ces deux valeurs de mot de passe ne peuvent pas être identiques.

Spécifiez les ressources de document PDF à chiffrer. Vous pouvez chiffrer l’intégralité du document PDF, à l’exception des métadonnées du document, ou uniquement des pièces jointes du document. Si vous chiffrez uniquement les pièces jointes du document, l’utilisateur est invité à saisir un mot de passe lorsqu’il essaie d’accéder aux pièces jointes.

Lors du chiffrement d’un document PDF, vous pouvez indiquer les autorisations associées au document sécurisé. En spécifiant les autorisations, vous pouvez contrôler les actions qu’un utilisateur qui ouvre un document PDF chiffré par mot de passe est autorisé à effectuer. Par exemple, pour extraire les données de formulaire avec succès, vous devez définir les autorisations suivantes :

* PASSWORD_EDIT_ADD
* PASSWORD_EDIT_MODIFY

>[!NOTE]
>
>Les autorisations sont spécifiées comme valeurs d’énumération `PasswordEncryptionPermission`.

**Ajouter le mot de passe**

Après avoir récupéré un document PDF non sécurisé et défini les valeurs d’exécution du chiffrement, vous pouvez ajouter un mot de passe au document PDF.

**Enregistrer le document PDF chiffré en tant que fichier PDF**

Vous pouvez enregistrer le document PDF chiffré par mot de passe en tant que fichier PDF.

**Voir également**

[Chiffrer un document PDF à l’aide de l’API Java](encrypting-decrypting-pdf-documents.md#encrypt-a-pdf-document-using-the-java-api)

[Chiffrer un document PDF à l’aide de l’API de service web](encrypting-decrypting-pdf-documents.md#encrypting-a-pdf-document-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Démarrages rapides de l’API du service Encryption](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[Chiffrer des documents PDF avec des certificats](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-certificates)

### Chiffrer un document PDF à l’aide de l’API Java {#encrypt-a-pdf-document-using-the-java-api}

Chiffrez un document PDF avec un mot de passe à l’aide de l’API Encryption (Java) :

1. Incluez les fichiers de projet.

   Incluez des fichiers JAR clients, tels que adobe-livecycle-client.jar, dans le chemin d’accès aux classes de votre projet Java.

1. Créez une API client Encryption.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `EncryptionServiceClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`.

1. Obtenez un document PDF à chiffrer.

   * Créez un objet `java.io.FileInputStream` représentant le document PDF à chiffrer en utilisant son constructeur et en transmettant une valeur de chaîne indiquant l’emplacement du document PDF.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Définissez les options d’exécution du chiffrement.

   * Créez un objet `PasswordEncryptionOptionSpec` en appelant son constructeur.
   * Indiquez les ressources du document PDF à chiffrer en appelant la méthode `setEncryptOption` de l’objet `PasswordEncryptionOptionSpec` et en transmettant une valeur d’énumération `PasswordEncryptionOption` spécifiant les ressources du document à chiffrer. Par exemple, pour chiffrer un document PDF entier, y compris ses métadonnées et ses pièces jointes, spécifiez `PasswordEncryptionOption.ALL`.
   * Créez un objet `java.util.List` qui stocke les autorisations de chiffrement à l’aide du constructeur `ArrayList`.
   * Spécifiez une autorisation en appelant la méthode `add` de l’objet `java.util.List` et en transmettant une valeur d’énumération correspondant à l’autorisation que vous souhaitez définir. Par exemple, pour définir l’autorisation qui permet à un utilisateur de copier des données dans le document du PDF, spécifiez `PasswordEncryptionPermission.PASSWORD_EDIT_COPY`. (Répétez cette étape pour chaque autorisation à définir).
   * Spécifiez l’option de compatibilité Acrobat en appelant la méthode `setCompatability` de l’objet `PasswordEncryptionOptionSpec` et en transmettant une valeur d’énumération indiquant le niveau de compatibilité Acrobat. Par exemple, vous pouvez spécifier `PasswordEncryptionCompatability.ACRO_7`.
   * Indiquez la valeur de mot de passe qui permet à l’utilisateur d’ouvrir le document PDF chiffré en appelant la méthode `setDocumentOpenPassword` de l’objet `PasswordEncryptionOptionSpec` et en transmettant une valeur de chaîne qui représente le mot de passe ouvert.
   * Indiquez la valeur de mot de passe principal qui permet à l’utilisateur de supprimer le chiffrement du document PDF en appelant la méthode `setPermissionPassword` de l’objet `PasswordEncryptionOptionSpec` et en transmettant une valeur de chaîne qui représente le mot de passe principal.

1. Ajoutez le mot de passe.

   Chiffrez le document PDF en appelant la méthode `encryptPDFUsingPassword` de l’objet `EncryptionServiceClient` et en transmettant les valeurs suivantes :

   * L’objet `com.adobe.idp.Document` contenant le document PDF à chiffrer avec le mot de passe.
   * L’objet `PasswordEncryptionOptionSpec` contenant les options d’exécution du chiffrement.

   La méthode `encryptPDFUsingPassword` renvoie un objet `com.adobe.idp.Document` contenant un document PDF chiffré par mot de passe.

1. Enregistrez le document PDF chiffré en tant que fichier PDF.

   * Créez un objet `java.io.File` et assurez-vous que l’extension du fichier est .pdf.
   * Appelez la méthode `copyToFile` de l’objet `com.adobe.idp.Document` pour copier le contenu de l’objet `com.adobe.idp.Document` dans le fichier. Assurez-vous d’utiliser l’objet `com.adobe.idp.Document` qui a été retourné par la méthode `encryptPDFUsingPassword`.

**Voir également**

[Résumé des étapes](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Démarrage rapide (mode SOAP) : chiffrement d’un document PDF à l’aide de l’API Java](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-encrypting-a-pdf-document-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Chiffrer un document PDF à l’aide de l’API de service web {#encrypting-a-pdf-document-using-the-web-service-api}

Chiffrez un document PDF avec un mot de passe à l’aide de l’API Encryption (service Web) :

1. Incluez les fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Veillez à utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un objet API client Encryption.

   * Créez un objet `EncryptionServiceClient` en utilisant son constructeur par défaut.
   * Créez un objet `EncryptionServiceClient.Endpoint.Address` en utilisant le constructeur `System.ServiceModel.EndpointAddress`. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/EncryptionService?WSDL`). Vous n’avez pas besoin d’utiliser l’attribut `lc_version`. Cet attribut est utilisé lorsque vous créez une référence de service.)
   * Créez un objet `System.ServiceModel.BasicHttpBinding` en obtenant la valeur du champ `EncryptionServiceClient.Endpoint.Binding`. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le champ `MessageEncoding` de l’objet `System.ServiceModel.BasicHttpBinding` sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Obtenez un document PDF à chiffrer.

   * Créez un objet `BLOB` en utilisant son constructeur. L’objet `BLOB` sert à stocker un document PDF chiffré avec un mot de passe.
   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du fichier du document PDF à chiffrer et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `System.IO.FileStream`. Vous pouvez déterminer la taille du tableau d’octets en obtenant la propriété `Length` de l’objet `System.IO.FileStream`.
   * Renseignez le tableau d’octets avec les données du flux en appelant la méthode `Read` de lʼobjet `System.IO.FileStream` et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’objet `BLOB` en attribuant le contenu du tableau d’octets au membre de données `MTOM` de l’objet `BLOB`.

1. Définissez les options d’exécution du chiffrement.

   * Créez un objet `PasswordEncryptionOptionSpec` en utilisant son constructeur.
   * Spécifiez les ressources du document PDF à chiffrer en attribuant une valeur d’énumération `PasswordEncryptionOption` au membre de données `encryptOption` de l’objet `PasswordEncryptionOptionSpec`. Pour chiffrer le PDF entier, y compris ses métadonnées et ses pièces jointes, attribuez `PasswordEncryptionOption.ALL` à ce membre de données.
   * Définissez l’option de compatibilité Acrobat en attribuant une valeur d’énumération `PasswordEncryptionCompatability` au membre de données `compatability` de l’objet `PasswordEncryptionOptionSpec`. Par exemple, attribuez `PasswordEncryptionCompatability.ACRO_7` à ce membre de données.
   * Indiquez la valeur de mot de passe qui permet à l’utilisateur d’ouvrir le document PDF chiffré en attribuant une valeur de chaîne représentant le mot de passe d’ouverture au membre de données `documentOpenPassword` de l’objet `PasswordEncryptionOptionSpec`.
   * Indiquez la valeur de mot de passe qui permet à l’utilisateur de supprimer le chiffrement du document PDF en attribuant une valeur de chaîne représentant le mot de passe principal au membre de données `permissionPassword` de l’objet `PasswordEncryptionOptionSpec`.

1. Ajoutez le mot de passe.

   Chiffrez le document PDF en appelant la méthode `encryptPDFUsingPassword` de l’objet `EncryptionServiceClient` et en transmettant les valeurs suivantes :

   * L’objet `BLOB` contenant le document PDF à chiffrer avec le mot de passe.
   * L’objet `PasswordEncryptionOptionSpec` contenant les options d’exécution du chiffrement.

   La méthode `encryptPDFUsingPassword` renvoie un objet `BLOB` contenant un document PDF chiffré par mot de passe.

1. Enregistrez le document PDF chiffré en tant que fichier PDF.

   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur de chaîne représentant l’emplacement du document PDF sécurisé.
   * Créez un tableau d’octets qui stocke le contenu des données de l’objet `BLOB` qui a été renvoyé par la méthode `encryptPDFUsingPassword`. Renseignez le tableau d’octets en obtenant la valeur du membre de données `MTOM` de l’objet `BLOB`.
   * Créez un objet `System.IO.BinaryWriter` en utilisant son constructeur et en transmettant l’objet `System.IO.FileStream`.
   * Écrivez le contenu du tableau d’octets dans un fichier PDF en appelant la méthode `Write` de l’objet `System.IO.BinaryWriter` et en transmettant le tableau d’octets.

**Voir également**

[Résumé des étapes](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Appeler AEM Forms en utilisant MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Appel d’AEM Forms à l’aide de SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Chiffrer des documents PDF avec des certificats {#encrypting-pdf-documents-with-certificates}

Le chiffrement par certificat vous permet de chiffrer le document pour des destinataires spécifiques utilisant la technologie de clé publique. Différents destinataires peuvent recevoir différents droits pour le document. De nombreux aspects de chiffrement sont possibles grâce à la technologie de clé publique. Un algorithme est utilisé pour générer deux grands nombres, encore appelés *clés* possédant les propriétés suivantes :

* Une clé est utilisée pour chiffrer un ensemble de données. Par la suite, seule l’autre clé peut être utilisée pour déchiffrer les données.
* Il est impossible de distinguer une clé d’une autre.

L’une des clés fait office de clé privée pour l’utilisateur. Il est important que seul l’utilisateur ait accès à cette clé. L’autre clé est la clé publique de l’utilisateur, qui peut être partagée avec d’autres utilisateurs.

Un certificat de clé publique contient la clé publique d’un utilisateur et ses données d’identification. Le format X.509 est utilisé pour le stockage des certificats. Les certificats sont généralement émis et signés numériquement par une autorité de certification, qui est une entité reconnue qui fournit une mesure de confiance dans la validité du certificat. Les certificats comportent une date d’expiration ; au-delà de cette date, ils ne sont plus valides. En outre, les listes de révocation des certificats (CRL) fournissent des informations sur les certificats révoqués avant leur date d’expiration. Les listes CRL sont publiées régulièrement par les autorités de certification. L’état de révocation d’un certificat peut également être récupéré via le protocole OCSP (Online Certificate Status Protocol) sur le réseau.

>[!NOTE]
>
>Si vous téléchargez un document PDF chiffré dans le référentiel AEM Forms, ce dernier ne pourra pas déchiffrer le document PDF et extraire le contenu XDP. Il est recommandé de ne pas chiffrer un document avant de le charger dans le référentiel AEM Forms. (Voir [Écriture de ressources](/help/forms/developing/aem-forms-repository.md#writing-resources).)

>[!NOTE]
>
>Avant de chiffrer un document PDF avec un certificat, vous devez vérifier que vous ajoutez le certificat à AEM Forms. Un certificat est ajouté à l’aide de la console d’administration ou par programmation à l’aide de l’API Trust Manager. (Voir [Importation des informations d’identification à l’aide de l’API Trust Manager](/help/forms/developing/credentials.md#importing-credentials-by-using-the-trust-manager-api).)

>[!NOTE]
>
>Pour plus d’informations sur le service Forms, voir [Références des services pour AEM Forms](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

### Résumé des étapes {#summary_of_steps-1}

Pour chiffrer un document PDF avec un certificat, procédez comme suit :

1. Incluez les fichiers de projet.
1. Créez un objet API client Encryption.
1. Obtenez un document PDF à chiffrer.
1. Référencez le certificat.
1. Définissez les options d’exécution du chiffrement.
1. Créez un document PDF chiffré par certificat.
1. Enregistrez le document PDF chiffré en tant que fichier PDF.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

Les fichiers JAR suivants doivent être ajoutés au chemin d’accès aux classes de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar (obligatoire si AEM Forms est déployé sur JBoss Application Server)
* jbossall-client.jar (obligatoire si AEM Forms est déployé sur JBoss Application Server)

**Créer un objet API client Encryption**

Pour effectuer par programmation une opération de service Encryption, vous devez créer un client de service Encryption. Si vous utilisez l’API Java Encryption Service, créez un objet `EncrytionServiceClient`. Si vous utilisez l’API Web Service Encryption Service, créez un objet `EncryptionServiceService`.

**Obtenir un document PDF à chiffrer**

Pour chiffrer, vous devez obtenir un document PDF non chiffré. Si vous tentez de sécuriser un document PDF déjà chiffré, une exception est générée.

**Référencer le certificat**

Pour chiffrer un document PDF avec un certificat, référencez un certificat utilisé pour chiffrer un document PDF. Le certificat est un fichier .cer, un fichier .crt ou un fichier .pem. Un fichier PKCS#12 est utilisé pour stocker des clés privées avec les certificats correspondants.

Lors du chiffrement d’un document PDF avec un certificat, spécifiez les autorisations associées au document sécurisé. En spécifiant les autorisations, vous pouvez contrôler les actions qu’un utilisateur qui ouvre un document PDF chiffré par certificat peut effectuer.

**Définir les options d’exécution de chiffrement**

Spécifiez les ressources de document PDF à chiffrer. Vous pouvez chiffrer l’intégralité du document PDF, à l’exception des métadonnées du document ou uniquement de ses pièces jointes.

**Créer un document PDF chiffré par certificat**

Après avoir récupéré un document PDF non sécurisé, référencé le certificat et défini les options d’exécution, vous pouvez créer un document PDF chiffré par certificat. Une fois le document PDF chiffré, vous avez besoin de la clé publique correspondante pour le déchiffrer.

**Enregistrer le document PDF chiffré en tant que fichier PDF**

Vous pouvez enregistrer le document PDF chiffré en tant que fichier PDF.

**Voir également**

[Chiffrer un document PDF avec un certificat à l’aide de l’API Java](encrypting-decrypting-pdf-documents.md#encrypt-a-pdf-document-with-a-certificate-using-the-java-api)

[Chiffrer un document PDF avec un certificat à l’aide de l’API Web Service](encrypting-decrypting-pdf-documents.md#encrypt-a-pdf-document-with-a-certificate-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Démarrages rapides de l’API du service Encryption](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[Chiffrer des documents PDF avec un mot de passe](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### Chiffrer un document PDF avec un certificat à l’aide de l’API Java {#encrypt-a-pdf-document-with-a-certificate-using-the-java-api}

Chiffrez un document PDF avec un certificat à l’aide de l’API Encryption (Java) :

1. Incluez les fichiers de projet.

   Incluez des fichiers JAR clients, tels que adobe-livecycle-client.jar, dans le chemin d’accès aux classes de votre projet Java.

1. Créez un objet API client Encryption.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `EncryptionServiceClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`.

1. Obtenez un document PDF à chiffrer.

   * Créez un objet `java.io.FileInputStream` représentant le document PDF à chiffrer en utilisant son constructeur et en transmettant une valeur de chaîne indiquant l’emplacement du document PDF.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Référencez le certificat.

   * Créez un objet `java.util.List` qui stocke les informations d’autorisation à l’aide de son constructeur.
   * Spécifiez l’autorisation associée au document chiffré en appelant la méthode `add` de l’objet `java.util.List` et en transmettant une valeur d’énumération `CertificateEncryptionPermissions` qui représente les autorisations accordées à l’utilisateur ouvrant le document PDF sécurisé. Par exemple, pour spécifier toutes les autorisations, transmettez `CertificateEncryptionPermissions.PKI_ALL_PERM`.
   * Créez un objet `Recipient` en utilisant son constructeur.
   * Créez un objet `java.io.FileInputStream` qui représente le certificat utilisé pour chiffrer le document PDF en utilisant son constructeur et en transmettant une valeur string qui spécifie l’emplacement du certificat.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream` qui représente le certificat.
   * Appelez la méthode `setX509Cert` de l’objet `Recipient` et transmettez l’objet `com.adobe.idp.Document` contenant le certificat. (En outre, l’objet `Recipient` peut avoir un alias de certificat Truststore ou une URL LDAP comme source de certificat.)
   * Créez un objet `CertificateEncryptionIdentity` qui stocke les informations d’autorisation et de certificat à l’aide de son constructeur.
   * Appelez la méthode `setPerms` de l’objet `CertificateEncryptionIdentity` et transmettez l’objet `java.util.List` qui stocke les informations d’autorisation.
   * Appelez la méthode `setRecipient` de l’objet `CertificateEncryptionIdentity` et transmettez l’objet `Recipient` qui stocke les informations sur le certificat.
   * Créez un objet `java.util.List` qui stocke les informations de certificat à l’aide de son constructeur.
   * Appelez la méthode Ajouter de l’objet `java.util.List` et transmettez l’objet `CertificateEncryptionIdentity`. (Cet objet `java.util.List` est transmis en tant que paramètre à la méthode `encryptPDFUsingCertificates`.)

1. Définissez les options d’exécution du chiffrement.

   * Créez un objet `CertificateEncryptionOptionSpec` en appelant son constructeur.
   * Indiquez les ressources du document PDF à chiffrer en appelant la méthode `setOption` de l’objet `CertificateEncryptionOptionSpec` et en transmettant une valeur d’énumération `CertificateEncryptionOption` spécifiant les ressources du document à chiffrer. Par exemple, pour chiffrer l’intégralité du document PDF, y compris ses métadonnées et ses pièces jointes, spécifiez `CertificateEncryptionOption.ALL`.
   * Spécifiez l’option de compatibilité Acrobat en appelant la méthode `setCompat` de l’objet `CertificateEncryptionOptionSpec` et en transmettant une valeur d’énumération `CertificateEncryptionCompatibility` spécifiant le niveau de compatibilité Acrobat. Par exemple, vous pouvez spécifier `CertificateEncryptionCompatibility.ACRO_7`.

1. Créez un document PDF chiffré par certificat.

   Chiffrez le document PDF avec un certificat en appelant la méthode `encryptPDFUsingCertificates` de l’objet `EncryptionServiceClient` et en transmettant les valeurs suivantes :

   * Objet `com.adobe.idp.Document` contenant le document PDF à chiffrer.
   * Objet `java.util.List` stockant les informations sur le certificat.
   * Objet `CertificateEncryptionOptionSpec` contenant les options d’exécution de chiffrement.

   La méthode `encryptPDFUsingCertificates` renvoie un objet `com.adobe.idp.Document` contenant un document PDF chiffré par certificat.

1. Enregistrez le document PDF chiffré en tant que fichier PDF.

   * Créez un objet `java.io.File` et assurez-vous que l’extension du nom du fichier est .pdf.
   * Appelez la méthode `copyToFile` de l’objet `com.adobe.idp.Document` pour copier le contenu de l’objet `com.adobe.idp.Document` dans le fichier. Assurez-vous d’utiliser l’objet `com.adobe.idp.Document` qui a été retourné par la méthode `encryptPDFUsingCertificates`.

**Voir également**

[Résumé des étapes](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Démarrage rapide (mode SOAP) : chiffrer un document PDF avec un certificat à l’aide de l’API Java.](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-encrypting-a-pdf-document-with-a-certificate-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Chiffrer un document PDF avec un certificat à l’aide de l’API Web Service {#encrypt-a-pdf-document-with-a-certificate-using-the-web-service-api}

Chiffrez un document PDF avec un certificat à l’aide de l’API Encryption (Web Service) :

1. Incluez les fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Veillez à utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un objet API client Encryption.

   * Créez un objet `EncryptionServiceClient` en utilisant son constructeur par défaut.
   * Créez un objet `EncryptionServiceClient.Endpoint.Address` en utilisant le constructeur `System.ServiceModel.EndpointAddress`. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/EncryptionService?WSDL`). Vous n’avez pas besoin d’utiliser l’attribut `lc_version`. Cet attribut est utilisé lorsque vous créez une référence de service.)
   * Créez un objet `System.ServiceModel.BasicHttpBinding` en obtenant la valeur du champ `EncryptionServiceClient.Endpoint.Binding`. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le champ `MessageEncoding` de l’objet `System.ServiceModel.BasicHttpBinding` sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Obtenez un document PDF à chiffrer.

   * Créez un objet `BLOB` en utilisant son constructeur. L’objet `BLOB` sert à stocker un document PDF chiffré avec un certificat.
   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur string qui représente l’emplacement du fichier du document PDF à chiffrer et son mode d’ouverture.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `System.IO.FileStream`. Vous pouvez déterminer la taille du tableau d’octets en obtenant la propriété `Length` de l’objet `System.IO.FileStream`.
   * Renseignez le tableau d’octets avec les données de diffusion en appelant la méthode `Read` de l’objet `System.IO.FileStream` et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’objet `BLOB` en attribuant sa propriété `MTOM` avec le contenu du tableau d’octets.

1. Référencez le certificat.

   * Créez un objet `Recipient` en utilisant son constructeur. Cet objet stocke les informations de certificat.
   * Créez un objet `BLOB` en utilisant son constructeur. Cet objet `BLOB` stocke le certificat qui chiffre le document PDF.
   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur string qui représente l’emplacement du fichier du certificat et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `System.IO.FileStream`. Vous pouvez déterminer la taille du tableau d’octets en obtenant la propriété `Length` de l’objet `System.IO.FileStream`.
   * Renseignez le tableau d’octets avec les données du flux en appelant la méthode `Read` de lʼobjet `System.IO.FileStream` et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’objet `BLOB` en attribuant le contenu du tableau d’octets au membre de données `MTOM` de l’objet `BLOB`.
   * Affectez l’objet `BLOB` qui stocke le certificat au membre de données `x509Cert` de l’objet `Recipient`.
   * Créez un objet `CertificateEncryptionIdentity` qui stocke les informations de certificat à l’aide de son constructeur.
   * Affectez l’objet `Recipient` qui stocke le certificat dans le membre de données du destinataire de l’objet `CertificateEncryptionIdentity`.
   * Créez un tableau `Object` et affectez l’objet `CertificateEncryptionIdentity` au premier élément du tableau `Object`. Ce tableau `Object` est transmis en tant que paramètre à la méthode `encryptPDFUsingCertificates`.

1. Définissez les options d’exécution du chiffrement.

   * Créez un objet `CertificateEncryptionOptionSpec` en utilisant son constructeur.
   * Spécifiez les ressources du document PDF à chiffrer en attribuant une valeur d’énumération `CertificateEncryptionOption` au membre de données `option` de l’objet `CertificateEncryptionOptionSpec`. Pour chiffrer l’intégralité du document PDF, y compris ses métadonnées et ses pièces jointes, affectez `CertificateEncryptionOption.ALL` à ce membre de données.
   * Définissez l’option de compatibilité Acrobat en attribuant une valeur d’énumération `CertificateEncryptionCompatibility` au membre de données `compat` de l’objet `CertificateEncryptionOptionSpec`. Par exemple, affectez `CertificateEncryptionCompatibility.ACRO_7` à ce membre de données.

1. Créez un document PDF chiffré par certificat.

   Chiffrez le document PDF avec un certificat en appelant la méthode `encryptPDFUsingCertificates` de l’objet `EncryptionServiceService` et en transmettant les valeurs suivantes :

   * Objet `BLOB` contenant le document PDF à chiffrer.
   * Tableau `Object` stockant les informations du certificat.
   * Objet `CertificateEncryptionOptionSpec` contenant les options d’exécution de chiffrement.

   La méthode `encryptPDFUsingCertificates` renvoie un objet `BLOB` contenant un document PDF chiffré par certificat.

1. Enregistrez le document PDF chiffré en tant que fichier PDF.

   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur de chaîne représentant l’emplacement du document PDF sécurisé.
   * Créez un tableau d’octets qui stocke le contenu des données de l’objet `BLOB` qui a été renvoyé par la méthode `encryptPDFUsingCertificates`. Renseignez le tableau d’octets en obtenant la valeur du membre de données `binaryData` de l’objet `BLOB`.
   * Créez un objet `System.IO.BinaryWriter` en utilisant son constructeur et en transmettant l’objet `System.IO.FileStream`.
   * Écrivez le contenu du tableau d’octets dans un fichier PDF en appelant la méthode `Write` de l’objet `System.IO.BinaryWriter` et en transmettant le tableau d’octets.

**Voir également**

[Résumé des étapes](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Appeler AEM Forms en utilisant MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Appel d’AEM Forms à l’aide de SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Supprimer un chiffrement avec certificat {#removing-certificate-based-encryption}

Vous pouvez supprimer le chiffrement avec certificat d’un document PDF afin que les utilisateurs puissent ouvrir le document PDF dans Adobe Reader ou Acrobat. Pour supprimer le chiffrement d’un document PDF chiffré avec un certificat, une clé publique doit être référencée. Une fois le chiffrement par mot de passe du document PDF supprimé, celui-ci n’est plus sécurisé.

>[!NOTE]
>
>Pour plus d’informations sur le service Encryption, voir [Référence des services pour AEM Forms](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

### Résumé des étapes {#summary_of_steps-2}

Pour supprimer le chiffrement avec certificat d’un document PDF, procédez comme suit :

1. Incluez les fichiers de projet.
1. Créez un client de service de chiffrement.
1. Prenez le document PDF chiffré.
1. Supprimez le chiffrement.
1. Enregistrez le document PDF au format PDF.

**Inclure des fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

Les fichiers JAR suivants doivent être ajoutés au chemin d’accès aux classes de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar (obligatoire si AEM Forms est déployé sur JBoss Application Server)
* jbossall-client.jar (obligatoire si AEM Forms est déployé sur JBoss Application Server)

**Créer un client de service de chiffrement**

Pour effectuer par programmation une opération de service Encryption, vous devez créer un client de service Encryption. Si vous utilisez l’API Java Encryption Service, créez un objet `EncrytionServiceClient`. Si vous utilisez l’API de service web Encryption Service, créez un objet `EncryptionServiceService`.

**Obtenir le document PDF chiffré**

Vous devez obtenir un document PDF chiffré pour supprimer le chiffrement avec certificat. Si vous tentez de supprimer le chiffrement d’un document PDF non chiffré, une exception est générée. De même, si vous tentez de supprimer le chiffrement avec certificat d’un document chiffré par mot de passe, une exception est générée.

**Supprimer le chiffrement**

Pour supprimer le chiffrement avec certificat d’un document PDF chiffré, vous avez besoin d’un document PDF chiffré et d’une clé privée correspondant à celle utilisée pour chiffrer le document PDF. La valeur de l’alias de la clé privée est spécifiée lors de la suppression du chiffrement avec certificat d’un document PDF chiffré. Pour plus d’informations sur la clé publique, consultez la section [Chiffrer des documents PDF au moyen de certificats](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-certificates).

>[!NOTE]
>
>Une clé privée est stockée dans le Trust Store d’AEM Forms. Lorsqu’un certificat y est déposé, une valeur d’alias est spécifiée.

**Enregistrer le document PDF**

Une fois le chiffrement au moyen dʼun certificat supprimé d’un document PDF chiffré, vous pouvez enregistrer le document PDF au format PDF. Les utilisateurs peuvent ouvrir le document PDF dans Adobe Reader ou Acrobat.

**Voir également**

[Supprimer le chiffrement avec certificat à l’aide de l’API Java](encrypting-decrypting-pdf-documents.md#remove-certificate-based-encryption-using-the-java-api)

[Supprimer le chiffrement avec certificat à l’aide de l’API de service web](encrypting-decrypting-pdf-documents.md#remove-certificate-based-encryption-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Démarrages rapides de l’API du service Encryption](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

### Supprimer le chiffrement avec certificat à l’aide de l’API Java {#remove-certificate-based-encryption-using-the-java-api}

Supprimez le chiffrement avec certificat d’un document PDF à l’aide de l’API Encryption (Java) :

1. Incluez les fichiers de projet.

   Incluez des fichiers JAR clients, tels que adobe-livecycle-client.jar, dans le chemin d’accès aux classes de votre projet Java.

1. Créez un client de service de chiffrement.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `EncryptionServiceClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`.

1. Prenez le document PDF chiffré.

   * Créez un objet `java.io.FileInputStream` représentant le document PDF chiffré en utilisant son constructeur et en transmettant une valeur de chaîne qui spécifie l’emplacement du document PDF chiffré.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Supprimez le chiffrement.

   Supprimez le chiffrement avec certificat du document PDF en appelant la méthode `removePDFCertificateSecurity` de lʼobjet `EncryptionServiceClient` et transmettez les valeurs suivantes :

   * Lʼobjet `com.adobe.idp.Document` contenant le document PDF chiffré.
   * Une valeur de chaîne qui spécifie le nom d’alias de la clé privée qui correspond à la clé utilisée pour chiffrer le document PDF.

   La méthode `removePDFCertificateSecurity` renvoie un objet `com.adobe.idp.Document` contenant un document PDF non sécurisé.

1. Enregistrez le formulaire PDF.

   * Créez un objet `java.io.File` et assurez-vous que l’extension du fichier est .pdf.
   * Appelez la méthode `copyToFile` de l’objet `com.adobe.idp.Document` pour copier le contenu de l’objet `Document` dans le fichier. Assurez-vous d’utiliser l’objet `com.adobe.idp.Document` qui a été retourné par la méthode `removePDFCredentialSecurity`.

**Voir également**

[Résumé des étapes](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Didacticiel de mise en route (mode SOAP) : supprimer un chiffrement avec certificat à l’aide de l’API Java](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-removing-certificate-based-encryption-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Supprimer le chiffrement avec certificat à l’aide de l’API de service web {#remove-certificate-based-encryption-using-the-web-service-api}

Supprimez le chiffrement avec certificat à l’aide de l’API Encryption (service web) :

1. Incluez les fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Veillez à utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un client de service de chiffrement.

   * Créez un objet `EncryptionServiceClient` en utilisant son constructeur par défaut.
   * Créez un objet `EncryptionServiceClient.Endpoint.Address` en utilisant le constructeur `System.ServiceModel.EndpointAddress`. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/EncryptionService?WSDL`). Vous n’avez pas besoin d’utiliser l’attribut `lc_version`. Cet attribut est utilisé lorsque vous créez une référence de service.)
   * Créez un objet `System.ServiceModel.BasicHttpBinding` en obtenant la valeur du champ `EncryptionServiceClient.Endpoint.Binding`. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le champ `MessageEncoding` de l’objet `System.ServiceModel.BasicHttpBinding` sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Prenez le document PDF chiffré.

   * Créez un objet `BLOB` en utilisant son constructeur. Lʼobjet `BLOB` sert à stocker le document PDF chiffré.
   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur de chaîne qui indique l’emplacement du fichier du document PDF chiffré et son mode d’ouverture.
   * Créez un tableau d’octets qui stocke le contenu de lʼobjet `System.IO.FileStream`. Vous pouvez déterminer la taille du tableau d’octets en obtenant la propriété `Length` de l’objet `System.IO.FileStream`.
   * Renseignez le tableau d’octets avec les données du flux en appelant la méthode `Read` de lʼobjet `System.IO.FileStream` et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez lʼobjet `BLOB` en affectant le contenu du tableau dʼoctets au membre de données `MTOM` de lʼobjet `BLOB`.

1. Supprimez le chiffrement.

   Appelez la méthode `removePDFCertificateSecurity` de lʼobjet `EncryptionServiceClient` et transmettez les valeurs suivantes :

   * Lʼobjet `BLOB` qui contient des données de flux de fichiers représentant un document PDF chiffré.
   * Une valeur de chaîne qui spécifie le nom d’alias de la clé publique qui correspond à la clé privée utilisée pour chiffrer le document PDF.

   La méthode `removePDFCredentialSecurity` renvoie un objet `BLOB` contenant un document PDF non sécurisé.

1. Enregistrez le formulaire PDF.

   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du fichier du document PDF non sécurisé.
   * Créez un tableau d’octets qui stocke le contenu de lʼobjet `BLOB` renvoyé par la méthode `removePDFPasswordSecurity`. Renseignez le tableau d’octets en obtenant la valeur du membre de données `MTOM` de l’objet `BLOB`.
   * Créez un objet `System.IO.BinaryWriter` en utilisant son constructeur et en transmettant l’objet `System.IO.FileStream`.
   * Écrivez le contenu du tableau d’octets dans un fichier PDF en appelant la méthode `Write` de l’objet `System.IO.BinaryWriter` et en transmettant le tableau d’octets.

**Voir également**

[Résumé des étapes](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Appeler AEM Forms en utilisant MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Appel d’AEM Forms à l’aide de SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Supprimer le chiffrement avec mot de passe {#removing-password-encryption}

Supprimez le chiffrement avec mot de passe d’un document PDF et permettez ainsi aux utilisateurs d’ouvrir le document PDF dans Adobe Reader ou Acrobat sans avoir besoin de saisir de mot de passe. Une fois le chiffrement avec mot de passe du document PDF supprimé, celui-ci n’est plus sécurisé.

>[!NOTE]
>
>Pour plus d’informations sur le service Forms, consultez la section [Références des services pour AEM Forms](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

### Résumé des étapes {#summary_of_steps-3}

Pour supprimer le chiffrement avec mot de passe d’un document PDF, procédez comme suit :

1. Inclure les fichiers du projet
1. Créez un client de service de chiffrement.
1. Prenez le document PDF chiffré.
1. Supprimez le mot de passe.
1. Enregistrez le document PDF au format PDF.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services web, veillez à inclure les fichiers proxy.

Les fichiers JAR suivants doivent être ajoutés au chemin d’accès aux classes de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utility.jar (obligatoire si AEM Forms est déployé sur JBoss)
* jbossall-client.jar (obligatoire si AEM Forms est déployé sur JBoss)

**Créer un client de service de chiffrement**

Pour effectuer par programmation une opération de service Encryption, vous devez créer un client de service Encryption. Si vous utilisez l’API Java Encryption Service, créez un objet `EncrytionServiceClient`. Si vous utilisez l’API de service web Encryption Service, créez un objet `EncryptionServiceService`.

**Obtenir le document PDF chiffré**

Vous devez obtenir un document PDF chiffré pour supprimer le chiffrement avec mot de passe. Si vous tentez de supprimer le chiffrement d’un document PDF non chiffré, une exception est générée.

**Supprimer le mot de passe**

Pour supprimer le chiffrement avec mot de passe d’un document PDF chiffré, vous avez besoin, dʼune part, d’un document PDF chiffré et, dʼautre part, d’une valeur de mot de passe principal, capable de supprimer le chiffrement du document PDF. Le mot de passe utilisé pour ouvrir un document PDF chiffré avec mot de passe ne peut pas être utilisé pour supprimer le chiffrement. Un mot de passe principal est spécifié lorsque le document PDF est chiffré avec un mot de passe. (Consultez la section [Chiffrer des documents PDF avec un mot de passe](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)).

**Enregistrer le document PDF**

Une fois que le service Encryption a supprimé le chiffrement avec mot de passe d’un document PDF, vous pouvez enregistrer le document PDF au format PDF. Les utilisateurs peuvent ouvrir le document PDF dans Adobe Reader ou Acrobat sans avoir besoin de saisir de mot de passe.

**Voir également**

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Démarrages rapides de l’API du service Encryption](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[Chiffrer des documents PDF avec un mot de passe](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### Supprimer le chiffrement avec mot de passe à l’aide de l’API Java {#remove-password-based-encryption-using-the-java-api}

Supprimez le chiffrement avec mot de passe d’un document PDF à l’aide de l’API Encryption (Java) :

1. Incluez les fichiers de projet.

   Incluez les fichiers JAR du client, tels que adobe-encryption-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un client de service de chiffrement.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `EncryptionServiceClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`.

1. Prenez le document PDF chiffré.

   * Créez un objet `java.io.FileInputStream` qui représente le document PDF chiffré en utilisant son constructeur et en transmettant une valeur de chaîne qui indique l’emplacement du document PDF.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Supprimez le mot de passe.

   Supprimez le chiffrement par mot de passe du document PDF en appelant la méthode `removePDFPasswordSecurity` de l’objet `EncryptionServiceClient` et en transmettant les valeurs suivantes :

   * Un objet `com.adobe.idp.Document` contenant le document PDF chiffré.
   * Une valeur de chaîne qui spécifie la valeur de mot de passe principal utilisé pour supprimer le chiffrement du document PDF.

   La méthode `removePDFPasswordSecurity` renvoie un objet `com.adobe.idp.Document` contenant un document PDF non sécurisé.

1. Enregistrez le formulaire PDF.

   * Créez un objet `java.io.File` et assurez-vous que l’extension du fichier est .pdf.
   * Appelez la méthode `copyToFile` de l’objet `com.adobe.idp.Document` pour copier le contenu de l’objet `Document` dans le fichier. Assurez-vous d’utiliser l’objet `Document` qui a été retourné par la méthode `removePDFPasswordSecurity`.

**Voir également**

[Démarrage rapide (mode SOAP) : supprimer le chiffrement par mot de passe à l’aide de l’API Java](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-removing-password-based-encryption-using-the-java-api)

### Supprimer le chiffrement par mot de passe à l’aide de l’API de service web {#remove-password-based-encryption-using-the-web-service-api}

Supprimez le chiffrement par mot de passe à l’aide de l’API Encryption (service web) :

1. Incluez les fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Veillez à utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un client de service de chiffrement.

   * Créez un objet `EncryptionServiceClient` en utilisant son constructeur par défaut.
   * Créez un objet `EncryptionServiceClient.Endpoint.Address` en utilisant le constructeur `System.ServiceModel.EndpointAddress`. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/EncryptionService?WSDL`). Vous n’avez pas besoin d’utiliser l’attribut `lc_version`. Cet attribut est utilisé lorsque vous créez une référence de service.)
   * Créez un objet `System.ServiceModel.BasicHttpBinding` en obtenant la valeur du champ `EncryptionServiceClient.Endpoint.Binding`. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le champ `MessageEncoding` de l’objet `System.ServiceModel.BasicHttpBinding` sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Prenez le document PDF chiffré.

   * Créez un objet `BLOB` en utilisant son constructeur. L’objet `BLOB` sert à stocker un document PDF chiffré par mot de passe.
   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur de chaîne représentant l’emplacement du document PDF chiffré et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de lʼobjet `System.IO.FileStream`. Vous pouvez déterminer la taille du tableau d’octets en obtenant la propriété `Length` de l’objet `System.IO.FileStream`.
   * Renseignez le tableau d’octets avec les données du flux en appelant la méthode `Read` de lʼobjet `System.IO.FileStream` et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’objet `BLOB` en attribuant le contenu du tableau d’octets au membre de données `MTOM` de l’objet `BLOB`.

1. Supprimez le mot de passe.

   Appelez la méthode `removePDFPasswordSecurity` de l’objet `EncryptionServiceService` et transmettez les valeurs suivantes :

   * L’objet `BLOB` qui contient des données de flux de fichiers représentant un document PDF chiffré.
   * Une valeur de chaîne qui indique la valeur de mot de passe utilisée pour supprimer le chiffrement du document PDF. Cette valeur est spécifiée lors du chiffrement du document PDF avec un mot de passe.

   La méthode `removePDFPasswordSecurity` renvoie un objet `BLOB` contenant un document PDF non sécurisé.

1. Enregistrez le formulaire PDF.

   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du fichier du document PDF non sécurisé.
   * Créez un tableau d’octets qui stocke le contenu de lʼobjet `BLOB` renvoyé par la méthode `removePDFPasswordSecurity`. Renseignez le tableau d’octets en obtenant la valeur du membre de données `MTOM` de l’objet `BLOB`.
   * Créez un objet `System.IO.BinaryWriter` en utilisant son constructeur et en transmettant l’objet `System.IO.FileStream`.
   * Écrivez le contenu du tableau d’octets dans un fichier PDF en appelant la méthode `Write` de l’objet `System.IO.BinaryWriter` et en transmettant le tableau d’octets.

**Voir également**

[Appeler AEM Forms en utilisant MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Appel d’AEM Forms à l’aide de SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Déverrouiller des documents PDF chiffrés {#unlocking-encrypted-pdf-documents}

Un document PDF chiffré par mot de passe ou par certificat doit être déverrouillé avant qu’une autre opération AEM Forms puisse être effectuée sur ce dernier. Si vous tentez d’effectuer une opération sur un document PDF chiffré, vous allez générer une exception. Après avoir déverrouillé un document PDF chiffré, vous pouvez y effectuer une ou plusieurs opérations. Ces opérations peuvent appartenir à d’autres services, tels que le service Extensions Acrobat Reader DC.

>[!NOTE]
>
>Pour plus d’informations sur le service Encryption, consultez la section [Références des services pour AEM Forms](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

### Résumé des étapes {#summary_of_steps-4}

Pour déverrouiller un document PDF chiffré, procédez comme suit :

1. Incluez les fichiers de projet.
1. Créez un client de service de chiffrement.
1. Prenez le document PDF chiffré.
1. Déverrouillez le document.
1. Exécutez une opération AEM Forms.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services web, veillez à inclure les fichiers proxy.

Les fichiers JAR suivants doivent être ajoutés au chemin d’accès aux classes de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar (obligatoire si AEM Forms est déployé sur JBoss Application Server)
* jbossall-client.jar (obligatoire si AEM Forms est déployé sur JBoss Application Server)

**Créer un client de service de chiffrement**

Pour effectuer par programmation une opération de service Encryption, vous devez créer un client de service Encryption. Si vous utilisez l’API Java Encryption Service, créez un objet `EncrytionServiceClient`. Si vous utilisez l’API de service web Encryption Service, créez un objet `EncryptionServiceService`.

**Obtenir le document PDF chiffré**

Vous devez obtenir un document de PDF chiffré pour le déverrouiller. Si vous tentez de déverrouiller un document PDF non chiffré, une exception est générée.

**Déverrouiller le document**

Pour déverrouiller un document PDF chiffré avec mot de passe, vous avez besoin, dʼune part, d’un document PDF chiffré et, dʼautre part, d’une valeur de mot de passe, capable dʼouvrir un document PDF chiffré avec mot de passe. Cette valeur est spécifiée lors du chiffrement du document PDF avec un mot de passe. (Consultez la section [Chiffrer des documents PDF avec un mot de passe](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)).

Pour déverrouiller un document PDF chiffré avec certificat, vous avez besoin d’un document PDF chiffré ainsi que de la valeur de l’alias de la clé publique qui correspond à la clé privée utilisée pour chiffrer le document PDF.

**Exécuter une opération AEM Forms**

Une fois un document PDF chiffré déverrouillé, vous pouvez effectuer une autre opération de service sur celui-ci, comme lʼapplication de droits dʼutilisation. Cette opération appartient au service Extensions Acrobat Reader DC.

**Voir également**

[Déverrouiller un document PDF chiffré à l’aide de l’API Java](encrypting-decrypting-pdf-documents.md#unlock-an-encrypted-pdf-document-using-the-java-api)

[Déverrouiller un document PDF chiffré à l’aide de l’API de service web](encrypting-decrypting-pdf-documents.md#unlock-an-encrypted-pdf-document-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Démarrages rapides de l’API du service Encryption](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

### Déverrouiller un document PDF chiffré à l’aide de l’API Java {#unlock-an-encrypted-pdf-document-using-the-java-api}

Déverrouillez un document PDF chiffré à l’aide de l’API Encryption (Java) :

1. Incluez les fichiers de projet.

   Incluez des fichiers JAR clients, tels que adobe-livecycle-client.jar, dans le chemin d’accès aux classes de votre projet Java.

1. Créez un client de service de chiffrement.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `EncryptionServiceClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`.

1. Prenez le document PDF chiffré.

   * Créez un objet `java.io.FileInputStream` représentant le document PDF chiffré en utilisant son constructeur et en transmettant une valeur de chaîne qui spécifie l’emplacement du document PDF chiffré.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Déverrouillez le document.

   Déverrouillez un document PDF chiffré en appelant la méthode `unlockPDFUsingPassword` ou `unlockPDFUsingCredential` de lʼobjet `EncryptionServiceClient`.

   Pour déverrouiller un document PDF chiffré avec un mot de passe, appelez la méthode `unlockPDFUsingPassword` et transmettez les valeurs suivantes :

   * Un objet `com.adobe.idp.Document` contenant le document PDF chiffré avec mot de passe.
   * Une valeur de chaîne qui indique la valeur de mot de passe utilisée pour ouvrir un document PDF chiffré par mot de passe. Cette valeur est spécifiée lors du chiffrement du document PDF avec un mot de passe.

   Pour déverrouiller un document PDF chiffré avec un certificat, appelez la méthode `unlockPDFUsingCredential` et transmettez les valeurs suivantes :

   * Un objet `com.adobe.idp.Document` qui contient le document PDF chiffré avec certificat.
   * Une valeur de chaîne qui spécifie le nom d’alias de la clé publique qui correspond à la clé privée utilisée pour chiffrer le document PDF.

   Les deux méthodes `unlockPDFUsingPassword` et `unlockPDFUsingCredential` renvoient un objet `com.adobe.idp.Document`, que vous transmettez à une autre méthode Java AEM Forms pour effectuer une opération.

1. Effectuez une opération AEM Forms.

   Effectuez une opération AEM Forms sur le document PDF déverrouillé pour répondre aux besoins de votre entreprise. Par exemple, si vous souhaitez appliquer des droits d’utilisation à un document PDF déverrouillé, transmettez lʼobjet `com.adobe.idp.Document`, renvoyé par la méthode `unlockPDFUsingPassword` ou `unlockPDFUsingCredential`, à la méthode `applyUsageRights` de lʼobjet `ReaderExtensionsServiceClient`.

**Voir également**

[Résumé des étapes](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Didacticiel de mise en route (mode SOAP) : déverrouiller un document PDF chiffré à l’aide de l’API Java](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-unlocking-an-encrypted-pdf-document-using-the-java-api) (mode SOAP)

[Appliquer des droits d’utilisation aux documents PDF](/help/forms/developing/assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Déverrouiller un document PDF chiffré à l’aide de l’API de service web {#unlock-an-encrypted-pdf-document-using-the-web-service-api}

Déverrouillez un document PDF chiffré à l’aide de l’API Encryption (service web) :

1. Incluez les fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Veillez à utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un client de service de chiffrement.

   * Créez un objet `EncryptionServiceClient` en utilisant son constructeur par défaut.
   * Créez un objet `EncryptionServiceClient.Endpoint.Address` en utilisant le constructeur `System.ServiceModel.EndpointAddress`. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/EncryptionService?WSDL`). Vous n’avez pas besoin d’utiliser l’attribut `lc_version`. Cet attribut est utilisé lorsque vous créez une référence de service.)
   * Créez un objet `System.ServiceModel.BasicHttpBinding` en obtenant la valeur du champ `EncryptionServiceClient.Endpoint.Binding`. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le champ `MessageEncoding` de l’objet `System.ServiceModel.BasicHttpBinding` sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Obtenez un document PDF chiffré.

   * Créez un objet `BLOB` en utilisant son constructeur.
   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du fichier du document PDF chiffré et son mode d’ouverture.
   * Créez un tableau d’octets qui stocke le contenu de lʼobjet `System.IO.FileStream`. Vous pouvez déterminer la taille du tableau d’octets en obtenant la propriété `Length` de l’objet `System.IO.FileStream`.
   * Renseignez le tableau d’octets avec les données du flux en appelant la méthode `Read` de lʼobjet `System.IO.FileStream` et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’objet `BLOB` en attribuant le contenu du tableau d’octets au membre de données `MTOM` de l’objet `BLOB`.

1. Déverrouillez le document.

   Déverrouillez un document PDF chiffré en appelant la méthode `unlockPDFUsingPassword` ou `unlockPDFUsingCredential` de lʼobjet `EncryptionServiceClient`.

   Pour déverrouiller un document PDF chiffré avec un mot de passe, appelez la méthode `unlockPDFUsingPassword` et transmettez les valeurs suivantes :

   * Un objet `BLOB` contenant le document PDF chiffré avec mot de passe.
   * Une valeur de chaîne qui indique la valeur de mot de passe utilisée pour ouvrir un document PDF chiffré par mot de passe. Cette valeur est spécifiée lors du chiffrement du document PDF avec un mot de passe.

   Pour déverrouiller un document PDF chiffré avec un certificat, appelez la méthode `unlockPDFUsingCredential` et transmettez les valeurs suivantes :

   * Un objet `BLOB` contenant le document PDF chiffré par certificat.
   * Une valeur de chaîne qui spécifie le nom d’alias de la clé publique qui correspond à la clé privée utilisée pour chiffrer le document PDF.

   Les méthodes `unlockPDFUsingPassword` et `unlockPDFUsingCredential` renvoient un objet `com.adobe.idp.Document` que vous transmettez à une autre méthode AEM Forms pour effectuer une opération.

1. Effectuez une opération AEM Forms.

   Effectuez une opération AEM Forms sur le document PDF déverrouillé pour répondre aux besoins de votre entreprise. Par exemple, si vous souhaitez appliquer des droits d’utilisation au document PDF déverrouillé, transmettez l’objet `BLOB` qui est renvoyé par l’une des méthodes `unlockPDFUsingPassword` et `unlockPDFUsingCredential` à la méthode `applyUsageRights` de l’objet `ReaderExtensionsServiceClient`.

**Voir également**

[Résumé des étapes](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Appeler AEM Forms en utilisant MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Appel d’AEM Forms à l’aide de SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Déterminer le type de chiffrement {#determining-encryption-type}

Vous pouvez déterminer par programmation le type de chiffrement qui protège un document PDF à l’aide de l’API Java Encryption Service ou de l’API de service web Encryption Service. Il est parfois nécessaire de déterminer de manière dynamique si un document PDF est chiffré et, le cas échéant, le type de chiffrement. Vous pouvez, par exemple, déterminer si un document PDF est protégé par un chiffrement avec mot de passe ou par une politique de Rights Management.

Un document PDF peut être protégé par les types de chiffrement suivants :

* Chiffrement par mot de passe
* Chiffrement par certificat
* Une politique créée par le service de Rights Management
* Autre type de chiffrement

>[!NOTE]
>
>Pour plus d’informations sur le service Encryption, voir [Références des services pour AEM Forms](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

### Résumé des étapes {#summary_of_steps-5}

Pour déterminer le type de chiffrement qui protège un document PDF, procédez comme suit :

1. Incluez les fichiers de projet.
1. Créez un client de service de chiffrement.
1. Prenez le document PDF chiffré.
1. Déterminez le type de chiffrement.

**Inclure des fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

Les fichiers JAR suivants doivent être ajoutés au chemin d’accès aux classes de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar (obligatoire si AEM Forms est déployé sur JBoss Application Server)
* jbossall-client.jar (obligatoire si AEM Forms est déployé sur JBoss Application Server)

**Créer un client de service**

Pour effectuer par programmation une opération de service Encryption, vous devez créer un client de service Encryption. Si vous utilisez l’API Java Encryption Service, créez un objet `EncrytionServiceClient`. Si vous utilisez l’API de service web Encryption Service, créez un objet `EncryptionServiceService`.

**Obtenir le document PDF chiffré**

Vous devez obtenir un document PDF pour déterminer le type de chiffrement qui le protège.

**Déterminer le type de chiffrement**

Vous pouvez déterminer le type de chiffrement qui protège un document PDF. Si le document PDF n’est pas protégé, le service Encryption vous informe que le document PDF n’est pas sécurisé.

**Voir également**

[Déterminer le type de chiffrement à l’aide de l’API Java](encrypting-decrypting-pdf-documents.md#determine-the-encryption-type-using-the-java-api)

[Déterminer le type de chiffrement à l’aide de l’API de service web](encrypting-decrypting-pdf-documents.md#determine-the-encryption-type-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Démarrages rapides de l’API du service Encryption](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[Protéger des documents à lʼaide de politiques](/help/forms/developing/protecting-documents-policies.md#protecting-documents-with-policies)

### Déterminer le type de chiffrement à l’aide de l’API Java {#determine-the-encryption-type-using-the-java-api}

Déterminez le type de chiffrement qui protège un document PDF à l’aide de l’API Encryption (Java) :

1. Incluez les fichiers de projet.

   Incluez des fichiers JAR clients, tels que adobe-livecycle-client.jar, dans le chemin d’accès aux classes de votre projet Java.

1. Créez un client de service.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `EncryptionServiceClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`.

1. Prenez le document PDF chiffré.

   * Créez un objet `java.io.FileInputStream` qui représente le document PDF en utilisant son constructeur et en transmettant une valeur de chaîne qui indique l’emplacement du document PDF.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Déterminez le type de chiffrement.

   * Déterminez le type de chiffrement en appelant la méthode `getPDFEncryption` de lʼobjet `EncryptionServiceClient` et en transmettant lʼobjet `com.adobe.idp.Document` contenant le document PDF. Cette méthode renvoie un objet `EncryptionTypeResult`.
   * Appelez la méthode `getEncryptionType` de lʼobjet `EncryptionTypeResult`. Cette méthode renvoie une valeur ENUM `EncryptionType` qui spécifie le type de chiffrement. Par exemple, si le document PDF est chiffré par un mot de passe, cette méthode renvoie la valeur `EncryptionType.PASSWORD`.

**Voir également**

[Résumé des étapes](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Didacticiel de mise en route (mode SOAP) : déterminer le type de chiffrement à l’aide de l’API Java](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-determining-encryption-type-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Déterminer le type de chiffrement à l’aide de l’API de service web {#determine-the-encryption-type-using-the-web-service-api}

Déterminez le type de chiffrement qui protège un document PDF à l’aide de l’API Encryption (service web) :

1. Incluez les fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Veillez à utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un client de service.

   * Créez un objet `EncryptionServiceClient` en utilisant son constructeur par défaut.
   * Créez un objet `EncryptionServiceClient.Endpoint.Address` en utilisant le constructeur `System.ServiceModel.EndpointAddress`. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/EncryptionService?WSDL`). Vous n’avez pas besoin d’utiliser l’attribut `lc_version`. Cet attribut est utilisé lorsque vous créez une référence de service.)
   * Créez un objet `System.ServiceModel.BasicHttpBinding` en obtenant la valeur du champ `EncryptionServiceClient.Endpoint.Binding`. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le champ `MessageEncoding` de l’objet `System.ServiceModel.BasicHttpBinding` sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Prenez le document PDF chiffré.

   * Créez un objet `BLOB` en utilisant son constructeur.
   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du fichier du document PDF chiffré et son mode d’ouverture.
   * Créez un tableau d’octets qui stocke le contenu de lʼobjet `System.IO.FileStream`. Vous pouvez déterminer la taille du tableau d’octets en obtenant la propriété `Length` de l’objet `System.IO.FileStream`.
   * Renseignez le tableau d’octets avec les données du flux en appelant la méthode `Read` de lʼobjet `System.IO.FileStream` et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez lʼobjet `BLOB` en attribuant le contenu du tableau d’octets au membre de données `MTOM` de lʼobjet `BLOB`.

1. Déterminez le type de chiffrement.

   * Appelez la méthode `getPDFEncryption` de lʼobjet `EncryptionServiceClient` et transmettez lʼobjet `BLOB` contenant le document PDF. Cette méthode renvoie un objet `EncryptionTypeResult`.
   * Obtenez la valeur de la méthode de données `encryptionType` de lʼobjet `EncryptionTypeResult`. Par exemple, si le document PDF est protégé à lʼaide dʼun chiffrement par mot de passe, la valeur de ce membre de données est `EncryptionType.PASSWORD`.

**Voir également**

[Résumé des étapes](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Appeler AEM Forms en utilisant MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Appel d’AEM Forms à l’aide de SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
