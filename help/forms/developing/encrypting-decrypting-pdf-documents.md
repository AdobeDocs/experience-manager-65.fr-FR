---
title: Chiffrement et déchiffrement de documents PDF
seo-title: Chiffrement et déchiffrement de documents PDF
description: Utilisez le service Encryption pour chiffrer et déchiffrer des documents. Les tâches du service Encryption incluent le chiffrement d’un document PDF avec un mot de passe, le chiffrement d’un document PDF avec un certificat, la suppression du chiffrement avec mot de passe d’un document PDF, la suppression du chiffrement avec certificat d’un document PDF, le déverrouillage du document PDF de sorte que d’autres opérations de service puissent être effectuées et la détermination du type de chiffrement d’un document PDF sécurisé.
seo-description: Utilisez le service Encryption pour chiffrer et déchiffrer des documents. Les tâches du service Encryption incluent le chiffrement d’un document PDF avec un mot de passe, le chiffrement d’un document PDF avec un certificat, la suppression du chiffrement avec mot de passe d’un document PDF, la suppression du chiffrement avec certificat d’un document PDF, le déverrouillage du document PDF de sorte que d’autres opérations de service puissent être effectuées et la détermination du type de chiffrement d’un document PDF sécurisé.
uuid: 4e4e2716-c21f-4bfe-ae7a-7e91442414ef
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 5e4bda3a-5648-4c0f-b2f8-bdbebb88f537
role: Developer
exl-id: d3cbca7f-9277-4d61-b198-abf4bb008f15
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '8258'
ht-degree: 8%

---

# Chiffrement et déchiffrement des documents PDF {#encrypting-and-decrypting-pdf-documents}

**Les exemples et les exemples de ce document sont réservés à l’environnement AEM Forms on JEE.**

**À propos du service Encryption**

Le service Encryption permet de chiffrer et de déchiffrer des documents. Lorsqu’un document est chiffré, son contenu devient illisible. Un utilisateur autorisé peut déchiffrer le document pour accéder à son contenu. Si un document PDF est chiffré avec un mot de passe, l’utilisateur doit spécifier le mot de passe d’ouverture pour pouvoir visualiser le document dans Adobe Reader ou Adobe Acrobat. De même, si un document PDF est chiffré avec un certificat, l’utilisateur doit déchiffrer le document PDF avec la clé publique correspondant au certificat (clé privée) qui a été utilisé pour chiffrer le document PDF.

Vous pouvez accomplir ces tâches à l’aide du service Encryption :

* Chiffrez un document PDF avec un mot de passe. (Voir [Chiffrement de documents PDF avec un mot de passe](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password).)
* Chiffrez un document PDF avec un certificat. (Voir [Chiffrement de documents PDF avec des certificats](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-certificates).)
* Supprimez le chiffrement avec mot de passe d’un document PDF. (Voir [Suppression du chiffrement de mot de passe](encrypting-decrypting-pdf-documents.md#removing-password-encryption).)
* Supprimez le chiffrement avec certificat d’un document PDF. (Voir [Suppression du chiffrement basé sur un certificat](encrypting-decrypting-pdf-documents.md#removing-certificate-based-encryption).)
* Déverrouillez le document PDF afin que d’autres opérations de service puissent être effectuées. Par exemple, après le déverrouillage d’un document PDF chiffré par mot de passe, vous pouvez lui appliquer une signature numérique. (Voir [Déverrouillage de documents PDF chiffrés](encrypting-decrypting-pdf-documents.md#unlocking-encrypted-pdf-documents).)
* Permet de déterminer le type de chiffrement d’un document PDF sécurisé. (Voir [Détermination du type de chiffrement](encrypting-decrypting-pdf-documents.md#determining-encryption-type).)

>[!NOTE]
>
>Pour plus d’informations sur le service Encryption, voir [Référence des services pour AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Chiffrement de documents PDF avec un mot de passe {#encrypting-pdf-documents-with-a-password}

Si vous chiffrez un document PDF avec un mot de passe, les utilisateurs devront indiquer ce même mot de passe pour pouvoir ouvrir le document PDF dans Adobe Reader ou Acrobat. Avant qu’une autre opération de pour AEM Forms (signer numérique un document PDF par exemple) puisse être exécutée sur le document, un document PDF chiffré par mot de passe doit être déverrouillé.

>[!NOTE]
>
>Si vous téléchargez un document PDF chiffré dans le référentiel AEM Forms, il ne peut pas déchiffrer le document PDF et extraire le contenu XDP. Il est recommandé de ne pas chiffrer un document avant de le charger dans le référentiel AEM Forms. (Voir [Écriture de ressources](/help/forms/developing/aem-forms-repository.md#writing-resources).)

>[!NOTE]
>
>Pour plus d’informations sur le service Encryption, voir [Référence des services pour AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary-of-steps}

Pour chiffrer un document PDF avec un mot de passe, procédez comme suit :

1. Inclure les fichiers de projet.
1. Créez un objet API client Encryption.
1. Obtenez un document PDF à chiffrer.
1. Définissez les options d’exécution de chiffrement.
1. Ajoutez le mot de passe.
1. Enregistrez le document PDF chiffré en tant que fichier PDF.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

Les fichiers JAR suivants doivent être ajoutés au chemin de classe de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utility.jar (obligatoire si AEM Forms est déployé sur JBoss)
* jbossall-client.jar (obligatoire si AEM Forms est déployé sur JBoss)

**Création d’un objet API client Encryption**

Pour effectuer par programmation une opération de service Encryption, vous devez créer un client de service Encryption.

**Obtention d’un document PDF à chiffrer**

Vous devez obtenir un document PDF non chiffré pour chiffrer le document avec un mot de passe. Si vous tentez de sécuriser un document PDF déjà chiffré, une exception est générée.

**Définition des options d’exécution de chiffrement**

Pour chiffrer un document PDF avec un mot de passe, vous spécifiez quatre valeurs, dont deux valeurs de mot de passe. La première valeur de mot de passe est utilisée pour chiffrer le document PDF et doit être spécifiée lors de l’ouverture du document PDF. La deuxième valeur de mot de passe, appelée mot de passe principal, est utilisée pour supprimer le chiffrement du document PDF. Les valeurs de mot de passe sont sensibles à la casse. Ces deux valeurs de mot de passe ne peuvent pas être les mêmes.

Vous devez spécifier les ressources de document PDF à chiffrer. Vous pouvez chiffrer l’intégralité du document PDF, à l’exception des métadonnées du document ou uniquement des pièces jointes du document. Si vous chiffrez uniquement les pièces jointes du document, un utilisateur est invité à saisir un mot de passe lorsqu’il tente d’accéder aux pièces jointes.

Lors du chiffrement d’un document PDF, vous pouvez spécifier les autorisations associées au document sécurisé. En spécifiant les autorisations, vous pouvez contrôler les actions qu’un utilisateur qui ouvre un document PDF chiffré par mot de passe est autorisé à effectuer. Par exemple, pour extraire les données de formulaire avec succès, vous devez définir les autorisations suivantes :

* PASSWORD_EDIT_ADD
* PASSWORD_EDIT_MODIFY

>[!NOTE]
>
>Les autorisations sont spécifiées en tant que valeurs d’énumération `PasswordEncryptionPermission`.

**Ajouter le mot de passe**

Après avoir récupéré un document PDF non sécurisé et défini les valeurs d’exécution du chiffrement, vous pouvez ajouter un mot de passe au document PDF.

**Enregistrement du document PDF chiffré en tant que fichier PDF**

Vous pouvez enregistrer le document PDF chiffré par mot de passe en tant que fichier PDF.

**Voir également**

[Chiffrer un document PDF à l’aide de l’API Java](encrypting-decrypting-pdf-documents.md#encrypt-a-pdf-document-using-the-java-api)

[Chiffrement d’un document PDF à l’aide de l’API du service Web](encrypting-decrypting-pdf-documents.md#encrypting-a-pdf-document-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Démarrages rapides de l’API du service Encryption](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[Chiffrement de documents PDF avec certificat](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-certificates)

### Chiffrer un document PDF à l’aide de l’API Java {#encrypt-a-pdf-document-using-the-java-api}

Chiffrez un document PDF avec un mot de passe à l’aide de l’API Encryption (Java) :

1. Inclure les fichiers de projet.

   Incluez les fichiers JAR client, tels que adobe-encryption-client.jar, dans le chemin d’accès de classe de votre projet Java.

1. Créez une API client Encryption.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `EncryptionServiceClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`.

1. Obtenez un document PDF à chiffrer.

   * Créez un objet `java.io.FileInputStream` qui représente le document PDF à chiffrer en utilisant son constructeur et en transmettant une valeur string qui spécifie l’emplacement du document PDF.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Définissez les options d’exécution de chiffrement.

   * Créez un objet `PasswordEncryptionOptionSpec` en appelant son constructeur.
   * Spécifiez les ressources de document PDF à chiffrer en appelant la méthode `PasswordEncryptionOptionSpec` de l’objet `setEncryptOption` et en transmettant une valeur d’énumération `PasswordEncryptionOption` qui spécifie les ressources de document à chiffrer. Par exemple, pour chiffrer l’intégralité du document PDF, y compris ses métadonnées et ses pièces jointes, spécifiez `PasswordEncryptionOption.ALL`.
   * Créez un objet `java.util.List` qui stocke les autorisations de chiffrement à l’aide du constructeur `ArrayList`.
   * Spécifiez une autorisation en appelant la méthode `java.util.List` de l’objet `add` et en transmettant une valeur d’énumération correspondant à l’autorisation que vous souhaitez définir. Par exemple, pour définir l’autorisation qui permet à un utilisateur de copier des données situées dans le document PDF, spécifiez `PasswordEncryptionPermission.PASSWORD_EDIT_COPY`. (Répétez cette étape pour chaque autorisation à définir).
   * Spécifiez l’option de compatibilité Acrobat en appelant la méthode `setCompatability` de l’objet `PasswordEncryptionOptionSpec` et en transmettant une valeur d’énumération spécifiant le niveau de compatibilité Acrobat. Par exemple, vous pouvez spécifier `PasswordEncryptionCompatability.ACRO_7`.
   * Indiquez la valeur du mot de passe qui permet à l’utilisateur d’ouvrir le document PDF chiffré en appelant la méthode `PasswordEncryptionOptionSpec` de l’objet `setDocumentOpenPassword` et en transmettant une valeur string qui représente le mot de passe ouvert.
   * Indiquez la valeur du mot de passe principal qui permet à un utilisateur de supprimer le chiffrement du document PDF en appelant la méthode `PasswordEncryptionOptionSpec` de l’objet `setPermissionPassword` et en transmettant une valeur string qui représente le mot de passe principal.

1. Ajoutez le mot de passe.

   Chiffrez le document PDF en appelant la méthode `encryptPDFUsingPassword` de l’objet `EncryptionServiceClient` et en transmettant les valeurs suivantes :

   * Objet `com.adobe.idp.Document` contenant le document PDF à chiffrer avec le mot de passe.
   * Objet `PasswordEncryptionOptionSpec` contenant les options d’exécution de chiffrement.

   La méthode `encryptPDFUsingPassword` renvoie un objet `com.adobe.idp.Document` contenant un document PDF chiffré par mot de passe.

1. Enregistrez le document PDF chiffré en tant que fichier PDF.

   * Créez un objet `java.io.File` et assurez-vous que l’extension du fichier est .pdf.
   * Appelez la méthode `copyToFile` de l’objet `com.adobe.idp.Document` pour copier le contenu de l’objet `com.adobe.idp.Document` dans le fichier. Assurez-vous d’utiliser l’objet `com.adobe.idp.Document` qui a été retourné par la méthode `encryptPDFUsingPassword`.

**Voir également**

[Résumé des étapes](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Démarrage rapide (mode SOAP) : Chiffrement d’un document PDF à l’aide de l’API Java](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-encrypting-a-pdf-document-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Chiffrement d’un document PDF à l’aide de l’API de service Web {#encrypting-a-pdf-document-using-the-web-service-api}

Chiffrez un document PDF avec un mot de passe à l’aide de l’API Encryption (service Web) :

1. Inclure les fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Assurez-vous d’utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un objet API client Encryption.

   * Créez un objet `EncryptionServiceClient` à l’aide de son constructeur par défaut.
   * Créez un objet `EncryptionServiceClient.Endpoint.Address` à l’aide du constructeur `System.ServiceModel.EndpointAddress`. Transmettez une valeur string qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/EncryptionService?WSDL`). Vous n’avez pas besoin d’utiliser l’attribut `lc_version`. Cet attribut est utilisé lorsque vous créez une référence de service.)
   * Créez un objet `System.ServiceModel.BasicHttpBinding` en obtenant la valeur du champ `EncryptionServiceClient.Endpoint.Binding`. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le champ `MessageEncoding` de l’objet `System.ServiceModel.BasicHttpBinding` sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Obtenez un document PDF à chiffrer.

   * Créez un objet `BLOB` en utilisant son constructeur. L’objet `BLOB` est utilisé pour stocker un document PDF chiffré avec un mot de passe.
   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur string qui représente l’emplacement du fichier du document PDF à chiffrer et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `System.IO.FileStream`. Vous pouvez déterminer la taille du tableau d’octets en obtenant la propriété `System.IO.FileStream` de l’objet `Length`.
   * Renseignez le tableau d’octets avec les données de flux en appelant la méthode `System.IO.FileStream` de l’objet `Read` et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’objet `BLOB` en attribuant le contenu du tableau d’octets au membre de données `MTOM` de l’objet `BLOB`.

1. Définissez les options d’exécution de chiffrement.

   * Créez un objet `PasswordEncryptionOptionSpec` en utilisant son constructeur.
   * Spécifiez les ressources de document PDF à chiffrer en attribuant une valeur d’énumération `PasswordEncryptionOption` au membre de données `encryptOption` de l’objet `PasswordEncryptionOptionSpec`. Pour chiffrer l’intégralité du PDF, y compris ses métadonnées et ses pièces jointes, affectez `PasswordEncryptionOption.ALL` à ce membre de données.
   * Spécifiez l’option de compatibilité Acrobat en attribuant une valeur d’énumération `PasswordEncryptionCompatability` au membre de données `compatability` de l’objet `PasswordEncryptionOptionSpec`. Par exemple, affectez `PasswordEncryptionCompatability.ACRO_7` à ce membre de données.
   * Indiquez la valeur du mot de passe qui permet à l’utilisateur d’ouvrir le document PDF chiffré en attribuant une valeur string qui représente le mot de passe d’ouverture au membre de données `documentOpenPassword` de l’objet.`PasswordEncryptionOptionSpec`
   * Indiquez la valeur du mot de passe qui permet à un utilisateur de supprimer le chiffrement du document PDF en attribuant une valeur string qui représente le mot de passe principal au membre de données `permissionPassword` de l’objet `PasswordEncryptionOptionSpec`.

1. Ajoutez le mot de passe.

   Chiffrez le document PDF en appelant la méthode `encryptPDFUsingPassword` de l’objet `EncryptionServiceClient` et en transmettant les valeurs suivantes :

   * Objet `BLOB` contenant le document PDF à chiffrer avec le mot de passe.
   * Objet `PasswordEncryptionOptionSpec` contenant les options d’exécution de chiffrement.

   La méthode `encryptPDFUsingPassword` renvoie un objet `BLOB` contenant un document PDF chiffré par mot de passe.

1. Enregistrez le document PDF chiffré en tant que fichier PDF.

   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur string qui représente l’emplacement du fichier du document PDF sécurisé.
   * Créez un tableau d’octets qui stocke le contenu des données de l’objet `BLOB` renvoyé par la méthode `encryptPDFUsingPassword`. Renseignez le tableau d’octets en obtenant la valeur du membre de données `MTOM` de l’objet `BLOB`.
   * Créez un objet `System.IO.BinaryWriter` en appelant son constructeur et en transmettant l’objet `System.IO.FileStream`.
   * Ecrivez le contenu du tableau d’octets dans un fichier PDF en appelant la méthode `System.IO.BinaryWriter` de l’objet `Write` et en transmettant le tableau d’octets.

**Voir également**

[Résumé des étapes](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Appel d’AEM Forms à l’aide de MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Appel d’AEM Forms à l’aide de SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Chiffrement de documents PDF avec des certificats {#encrypting-pdf-documents-with-certificates}

Le chiffrement avec certificat permet de chiffrer un document pour des destinataires spécifiques au moyen de la technologie de clé publique. Différents destinataires peuvent recevoir différents droits pour le document. De nombreux aspects de chiffrement sont possibles grâce à la technologie de clé publique. Un algorithme est utilisé pour générer deux grands nombres, appelés *keys*, qui possèdent les propriétés suivantes :

* Une clé est utilisée pour chiffrer un ensemble de données. Par la suite, seule l’autre clé peut être utilisée pour déchiffrer les données.
* Il est impossible de distinguer une clé d’une autre.

L’une des clés agit comme la clé privée d’un utilisateur. Il est important que seul l’utilisateur ait accès à cette clé. L’autre clé est la clé publique de l’utilisateur, qui peut être partagée avec d’autres utilisateurs.

Un certificat de clé publique contient la clé publique et les informations d’identification d’un utilisateur. Le format X.509 est utilisé pour le stockage de certificats. Les certificats sont généralement émis et signés numériquement par une autorité de certification, qui est une entité reconnue qui garantit la validité du certificat. Les certificats comportent une date d’expiration ; au-delà de cette date, ils ne sont plus valides. En outre, les listes de révocation des certificats (CRL) fournissent des informations sur les certificats révoqués avant leur date d’expiration. Les listes CRL sont modifiées régulièrement par des autorités de certification. Vous pouvez également récupérer l’état de révocation d’un certificat par l’intermédiaire du protocole OCSP (Online Certificate Status Protocol, protocole d’état de certificat en ligne) sur le réseau.

>[!NOTE]
>
>Si vous téléchargez un document PDF chiffré dans le référentiel AEM Forms, il ne peut pas déchiffrer le document PDF et extraire le contenu XDP. Il est recommandé de ne pas chiffrer un document avant de le charger dans le référentiel AEM Forms. (Voir [Écriture de ressources](/help/forms/developing/aem-forms-repository.md#writing-resources).)

>[!NOTE]
>
>Avant de chiffrer un document PDF avec un certificat, vous devez vous assurer d’ajouter le certificat à AEM Forms. Un certificat est ajouté à l’aide d’Administration Console ou par programmation à l’aide de l’API Trust Manager. (Voir [Importation des informations d’identification à l’aide de l’API Trust Manager](/help/forms/developing/credentials.md#importing-credentials-by-using-the-trust-manager-api).)

>[!NOTE]
>
>Pour plus d’informations sur le service Encryption, voir [Référence des services pour AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary_of_steps-1}

Pour chiffrer un document PDF avec un certificat, procédez comme suit :

1. Inclure les fichiers de projet.
1. Créez un objet API client Encryption.
1. Obtenez un document PDF à chiffrer.
1. Référencez le certificat.
1. Définissez les options d’exécution de chiffrement.
1. Créez un document PDF chiffré par certificat.
1. Enregistrez le document PDF chiffré en tant que fichier PDF.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

Les fichiers JAR suivants doivent être ajoutés au chemin de classe de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utility.jar (obligatoire si AEM Forms est déployé sur JBoss Application Server)
* jbossall-client.jar (obligatoire si AEM Forms est déployé sur JBoss Application Server)

**Création d’un objet API client Encryption**

Pour effectuer par programmation une opération de service Encryption, vous devez créer un client de service Encryption. Si vous utilisez l’API Java Encryption Service, créez un objet `EncrytionServiceClient` . Si vous utilisez l’API du service Web Encryption Service, créez un objet `EncryptionServiceService` .

**Obtention d’un document PDF à chiffrer**

Vous devez obtenir un document PDF non chiffré pour le chiffrer. Si vous tentez de sécuriser un document PDF déjà chiffré, une exception est générée.

**Référence au certificat**

Pour chiffrer un document PDF avec un certificat, référencez un certificat utilisé pour chiffrer un document PDF. Le certificat est un fichier .cer, un fichier .crt ou un fichier .pem. Un fichier PKCS#12 est utilisé pour stocker des clés privées avec les certificats correspondants.

Lors du chiffrement d’un document PDF avec un certificat, spécifiez les autorisations associées au document sécurisé. En spécifiant des autorisations, vous pouvez contrôler les actions qu’un utilisateur qui ouvre un document PDF chiffré par certificat peut effectuer.

**Définition des options d’exécution de chiffrement**

Spécifiez les ressources de document PDF à chiffrer. Vous pouvez chiffrer l’intégralité du document PDF, tout sauf les métadonnées du document ou uniquement les pièces jointes du document.

**Création d’un document PDF chiffré par certificat**

Après avoir récupéré un document PDF non sécurisé, référencé le certificat et défini les options d’exécution, vous pouvez créer un document PDF chiffré par certificat. Une fois le document PDF chiffré, vous avez besoin de la clé publique correspondante pour le déchiffrer.

**Enregistrement du document PDF chiffré en tant que fichier PDF**

Vous pouvez enregistrer le document PDF chiffré en tant que fichier PDF.

**Voir également**

[Chiffrer un document PDF avec un certificat à l’aide de l’API Java](encrypting-decrypting-pdf-documents.md#encrypt-a-pdf-document-with-a-certificate-using-the-java-api)

[Chiffrer un document PDF avec un certificat à l’aide de l’API de service Web](encrypting-decrypting-pdf-documents.md#encrypt-a-pdf-document-with-a-certificate-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Démarrages rapides de l’API du service Encryption](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[Chiffrement de documents PDF avec un mot de passe](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### Chiffrer un document PDF avec un certificat à l’aide de l’API Java {#encrypt-a-pdf-document-with-a-certificate-using-the-java-api}

Chiffrez un document PDF avec un certificat à l’aide de l’API Encryption (Java) :

1. Inclure les fichiers de projet.

   Incluez les fichiers JAR client, tels que adobe-encryption-client.jar, dans le chemin d’accès de classe de votre projet Java.

1. Créez un objet API client Encryption.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `EncryptionServiceClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`.

1. Obtenez un document PDF à chiffrer.

   * Créez un objet `java.io.FileInputStream` qui représente le document PDF à chiffrer en utilisant son constructeur et en transmettant une valeur string qui spécifie l’emplacement du document PDF.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Référencez le certificat.

   * Créez un objet `java.util.List` qui stocke les informations d’autorisation à l’aide de son constructeur.
   * Spécifiez l’autorisation associée au document chiffré en appelant la méthode `java.util.List` de l’objet `add` et en transmettant une valeur d’énumération `CertificateEncryptionPermissions` qui représente les autorisations accordées à l’utilisateur qui ouvre le document PDF sécurisé. Par exemple, pour spécifier toutes les autorisations, transmettez `CertificateEncryptionPermissions.PKI_ALL_PERM`.
   * Créez un objet `Recipient` en utilisant son constructeur.
   * Créez un objet `java.io.FileInputStream` qui représente le certificat utilisé pour chiffrer le document PDF à l’aide de son constructeur et transmettre une valeur string qui spécifie l’emplacement du certificat.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream` qui représente le certificat.
   * Appelez la méthode `setX509Cert` de l’objet `Recipient` et transmettez l’objet `com.adobe.idp.Document` contenant le certificat. (En outre, l’objet `Recipient`peut avoir un alias de certificat Truststore ou une URL LDAP comme source de certificat.)
   * Créez un objet `CertificateEncryptionIdentity` qui stocke les informations d’autorisation et de certificat à l’aide de son constructeur.
   * Appelez la méthode `setPerms` de l’objet `CertificateEncryptionIdentity` et transmettez l’objet `java.util.List` qui stocke les informations d’autorisation.
   * Appelez la méthode `setRecipient` de l’objet `CertificateEncryptionIdentity` et transmettez l’objet `Recipient` qui stocke les informations de certificat.
   * Créez un objet `java.util.List` qui stocke les informations de certificat à l’aide de son constructeur.
   * Appelez la méthode add de l’objet `java.util.List` et transmettez l’objet `CertificateEncryptionIdentity` . (Cet objet `java.util.List` est transmis en paramètre à la méthode `encryptPDFUsingCertificates` .)

1. Définissez les options d’exécution de chiffrement.

   * Créez un objet `CertificateEncryptionOptionSpec` en appelant son constructeur.
   * Spécifiez les ressources de document PDF à chiffrer en appelant la méthode `CertificateEncryptionOptionSpec` de l’objet `setOption` et en transmettant une valeur d’énumération `CertificateEncryptionOption` qui spécifie les ressources de document à chiffrer. Par exemple, pour chiffrer l’intégralité du document PDF, y compris ses métadonnées et ses pièces jointes, spécifiez `CertificateEncryptionOption.ALL`.
   * Spécifiez l’option de compatibilité Acrobat en appelant la méthode `setCompat` de l’objet `CertificateEncryptionOptionSpec` et en transmettant une valeur d’énumération `CertificateEncryptionCompatibility` qui spécifie le niveau de compatibilité Acrobat. Par exemple, vous pouvez spécifier `CertificateEncryptionCompatibility.ACRO_7`.

1. Créez un document PDF chiffré par certificat.

   Chiffrez le document PDF avec un certificat en appelant la méthode `encryptPDFUsingCertificates` de l’objet `EncryptionServiceClient` et en transmettant les valeurs suivantes :

   * Objet `com.adobe.idp.Document` contenant le document PDF à chiffrer.
   * Objet `java.util.List` qui stocke les informations sur le certificat.
   * Objet `CertificateEncryptionOptionSpec` contenant les options d’exécution de chiffrement.

   La méthode `encryptPDFUsingCertificates` renvoie un objet `com.adobe.idp.Document` contenant un document PDF chiffré par certificat.

1. Enregistrez le document PDF chiffré en tant que fichier PDF.

   * Créez un objet `java.io.File` et assurez-vous que l’extension de nom de fichier est .pdf.
   * Appelez la méthode `copyToFile` de l’objet `com.adobe.idp.Document` pour copier le contenu de l’objet `com.adobe.idp.Document` dans le fichier. Assurez-vous d’utiliser l’objet `com.adobe.idp.Document` qui a été retourné par la méthode `encryptPDFUsingCertificates`.

**Voir également**

[Résumé des étapes](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Démarrage rapide (mode SOAP) : Chiffrement d’un document PDF avec un certificat à l’aide de l’API Java](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-encrypting-a-pdf-document-with-a-certificate-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Chiffrer un document PDF avec un certificat à l’aide de l’API de service Web {#encrypt-a-pdf-document-with-a-certificate-using-the-web-service-api}

Chiffrez un document PDF avec un certificat à l’aide de l’API Encryption (service Web) :

1. Inclure les fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Assurez-vous d’utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un objet API client Encryption.

   * Créez un objet `EncryptionServiceClient` à l’aide de son constructeur par défaut.
   * Créez un objet `EncryptionServiceClient.Endpoint.Address` à l’aide du constructeur `System.ServiceModel.EndpointAddress`. Transmettez une valeur string qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/EncryptionService?WSDL`). Vous n’avez pas besoin d’utiliser l’attribut `lc_version`. Cet attribut est utilisé lorsque vous créez une référence de service.)
   * Créez un objet `System.ServiceModel.BasicHttpBinding` en obtenant la valeur du champ `EncryptionServiceClient.Endpoint.Binding`. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le champ `MessageEncoding` de l’objet `System.ServiceModel.BasicHttpBinding` sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Obtenez un document PDF à chiffrer.

   * Créez un objet `BLOB` en utilisant son constructeur. L’objet `BLOB` est utilisé pour stocker un document PDF chiffré avec un certificat.
   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur string qui représente l’emplacement du fichier du document PDF à chiffrer et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `System.IO.FileStream`. Vous pouvez déterminer la taille du tableau d’octets en obtenant la propriété `System.IO.FileStream` de l’objet `Length`.
   * Renseignez le tableau d’octets avec les données de flux en appelant la méthode `System.IO.FileStream` de l’objet `Read` et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’objet `BLOB` en attribuant sa propriété `MTOM` avec le contenu du tableau d’octets.

1. Référencez le certificat.

   * Créez un objet `Recipient` en utilisant son constructeur. Cet objet stocke les informations de certificat.
   * Créez un objet `BLOB` en utilisant son constructeur. Cet objet `BLOB` stocke le certificat qui chiffre le document PDF.
   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur string qui représente l’emplacement du fichier du certificat et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `System.IO.FileStream`. Vous pouvez déterminer la taille du tableau d’octets en obtenant la propriété `System.IO.FileStream` de l’objet `Length`.
   * Renseignez le tableau d’octets avec les données de flux en appelant la méthode `System.IO.FileStream` de l’objet `Read` et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’objet `BLOB` en attribuant le contenu du tableau d’octets au membre de données `MTOM` de l’objet `BLOB`.
   * Affectez l’objet `BLOB` qui stocke le certificat au membre de données `x509Cert` de l’objet `Recipient`.
   * Créez un objet `CertificateEncryptionIdentity` qui stocke les informations de certificat à l’aide de son constructeur.
   * Affectez l’objet `Recipient` qui stocke le certificat au membre de données de destinataire de l’objet `CertificateEncryptionIdentity`.
   * Créez un tableau `Object` et affectez l’objet `CertificateEncryptionIdentity` au premier élément du tableau `Object`. Ce tableau `Object` est transmis en tant que paramètre à la méthode `encryptPDFUsingCertificates` .

1. Définissez les options d’exécution de chiffrement.

   * Créez un objet `CertificateEncryptionOptionSpec` en utilisant son constructeur.
   * Spécifiez les ressources de document PDF à chiffrer en attribuant une valeur d’énumération `CertificateEncryptionOption` au membre de données `option` de l’objet `CertificateEncryptionOptionSpec`. Pour chiffrer l’intégralité du document PDF, y compris ses métadonnées et ses pièces jointes, affectez `CertificateEncryptionOption.ALL` à ce membre de données.
   * Spécifiez l’option de compatibilité Acrobat en attribuant une valeur d’énumération `CertificateEncryptionCompatibility` au membre de données `compat` de l’objet `CertificateEncryptionOptionSpec`. Par exemple, affectez `CertificateEncryptionCompatibility.ACRO_7` à ce membre de données.

1. Créez un document PDF chiffré par certificat.

   Chiffrez le document PDF avec un certificat en appelant la méthode `encryptPDFUsingCertificates` de l’objet `EncryptionServiceService` et en transmettant les valeurs suivantes :

   * Objet `BLOB` contenant le document PDF à chiffrer.
   * Le tableau `Object` qui stocke les informations sur le certificat.
   * Objet `CertificateEncryptionOptionSpec` contenant les options d’exécution de chiffrement.

   La méthode `encryptPDFUsingCertificates` renvoie un objet `BLOB` contenant un document PDF chiffré par certificat.

1. Enregistrez le document PDF chiffré en tant que fichier PDF.

   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur string qui représente l’emplacement du fichier du document PDF sécurisé.
   * Créez un tableau d’octets qui stocke le contenu des données de l’objet `BLOB` renvoyé par la méthode `encryptPDFUsingCertificates`. Renseignez le tableau d’octets en obtenant la valeur du membre de données `binaryData` de l’objet `BLOB`.
   * Créez un objet `System.IO.BinaryWriter` en appelant son constructeur et en transmettant l’objet `System.IO.FileStream`.
   * Ecrivez le contenu du tableau d’octets dans un fichier PDF en appelant la méthode `System.IO.BinaryWriter` de l’objet `Write` et en transmettant le tableau d’octets.

**Voir également**

[Résumé des étapes](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Appel d’AEM Forms à l’aide de MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Appel d’AEM Forms à l’aide de SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Suppression du chiffrement avec certificat {#removing-certificate-based-encryption}

Le chiffrement avec certificat peut être supprimé d’un document PDF afin que les utilisateurs puissent ouvrir le document PDF dans Adobe Reader ou Acrobat. Pour supprimer le chiffrement d’un document PDF chiffré avec un certificat, une clé publique doit être référencée. Une fois le chiffrement supprimé d’un document PDF, il n’est plus sécurisé.

>[!NOTE]
>
>Pour plus d’informations sur le service Encryption, voir [Référence des services pour AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary_of_steps-2}

Pour supprimer le chiffrement avec certificat d’un document PDF, procédez comme suit :

1. Inclure les fichiers de projet.
1. Créez un client de service de chiffrement.
1. Obtenez le document PDF chiffré.
1. Supprimez le chiffrement.
1. Enregistrez le document PDF au format PDF.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

Les fichiers JAR suivants doivent être ajoutés au chemin de classe de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utility.jar (obligatoire si AEM Forms est déployé sur JBoss Application Server)
* jbossall-client.jar (obligatoire si AEM Forms est déployé sur JBoss Application Server)

**Création d’un client de service de chiffrement**

Pour effectuer par programmation une opération de service Encryption, vous devez créer un client de service Encryption. Si vous utilisez l’API Java Encryption Service, créez un objet `EncrytionServiceClient` . Si vous utilisez l’API du service Web Encryption Service, créez un objet `EncryptionServiceService` .

**Obtention du document PDF chiffré**

Vous devez obtenir un document PDF chiffré pour supprimer le chiffrement avec certificat. Si vous tentez de supprimer le chiffrement d’un document PDF non chiffré, une exception est générée. De même, si vous tentez de supprimer le chiffrement avec certificat d’un document chiffré par mot de passe, une exception est générée.

**Supprimer le chiffrement**

Pour supprimer le chiffrement avec certificat d’un document PDF chiffré, vous devez disposer à la fois d’un document PDF chiffré et d’une clé privée correspondant à la clé utilisée pour chiffrer le document PDF. La valeur d’alias de la clé privée est spécifiée lors de la suppression du chiffrement avec certificat d’un document PDF chiffré. Pour plus d’informations sur la clé publique, voir [Chiffrement des documents PDF avec des certificats](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-certificates).

>[!NOTE]
>
>Une clé privée est stockée dans le Trust Store d’AEM Forms. Lorsqu’un certificat y est placé, une valeur d’alias est spécifiée.

**Enregistrement du document PDF**

Une fois le chiffrement avec certificat supprimé d’un document PDF chiffré, vous pouvez enregistrer le document PDF en tant que fichier PDF. Les utilisateurs peuvent ouvrir le document PDF dans Adobe Reader ou Acrobat.

**Voir également**

[Suppression d’un chiffrement avec certificat à l’aide de l’API Java](encrypting-decrypting-pdf-documents.md#remove-certificate-based-encryption-using-the-java-api)

[Suppression d’un chiffrement avec certificat à l’aide de l’API de service Web](encrypting-decrypting-pdf-documents.md#remove-certificate-based-encryption-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Démarrages rapides de l’API du service Encryption](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

### Supprimer le chiffrement avec certificat à l’aide de l’API Java {#remove-certificate-based-encryption-using-the-java-api}

Supprimez le chiffrement avec certificat d’un document PDF à l’aide de l’API Encryption (Java) :

1. Inclure les fichiers de projet.

   Incluez les fichiers JAR client, tels que adobe-encryption-client.jar, dans le chemin d’accès de classe de votre projet Java.

1. Créez un client de service de chiffrement.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `EncryptionServiceClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`.

1. Obtenez le document PDF chiffré.

   * Créez un objet `java.io.FileInputStream` qui représente le document PDF chiffré en utilisant son constructeur et en transmettant une valeur string qui spécifie l’emplacement du document PDF chiffré.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Supprimez le chiffrement.

   Supprimez le chiffrement avec certificat du document PDF en appelant la méthode `removePDFCertificateSecurity` de l’objet `EncryptionServiceClient` et en transmettant les valeurs suivantes :

   * Objet `com.adobe.idp.Document` contenant le document PDF chiffré.
   * Une valeur string qui spécifie le nom d’alias de la clé privée qui correspond à la clé utilisée pour chiffrer le document PDFf.

   La méthode `removePDFCertificateSecurity` renvoie un objet `com.adobe.idp.Document` contenant un document PDF non sécurisé.

1. Enregistrez le document PDF.

   * Créez un objet `java.io.File` et assurez-vous que l’extension du fichier est .pdf.
   * Appelez la méthode `copyToFile` de l’objet `com.adobe.idp.Document` pour copier le contenu de l’objet `Document` dans le fichier. Assurez-vous d’utiliser l’objet `com.adobe.idp.Document` qui a été retourné par la méthode `removePDFCredentialSecurity`.

**Voir également**

[Résumé des étapes](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Démarrage rapide (mode SOAP) : Suppression d’un chiffrement avec certificat à l’aide de l’API Java](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-removing-certificate-based-encryption-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Supprimer le chiffrement avec certificat à l’aide de l’API de service Web {#remove-certificate-based-encryption-using-the-web-service-api}

Supprimez le chiffrement avec certificat à l’aide de l’API Encryption (service Web) :

1. Inclure les fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Assurez-vous d’utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un client de service de chiffrement.

   * Créez un objet `EncryptionServiceClient` à l’aide de son constructeur par défaut.
   * Créez un objet `EncryptionServiceClient.Endpoint.Address` à l’aide du constructeur `System.ServiceModel.EndpointAddress`. Transmettez une valeur string qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/EncryptionService?WSDL`). Vous n’avez pas besoin d’utiliser l’attribut `lc_version`. Cet attribut est utilisé lorsque vous créez une référence de service.)
   * Créez un objet `System.ServiceModel.BasicHttpBinding` en obtenant la valeur du champ `EncryptionServiceClient.Endpoint.Binding`. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le champ `MessageEncoding` de l’objet `System.ServiceModel.BasicHttpBinding` sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Obtenez le document PDF chiffré.

   * Créez un objet `BLOB` en utilisant son constructeur. L’objet `BLOB` est utilisé pour stocker le document PDF chiffré.
   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur string qui représente l’emplacement du fichier du document PDF chiffré et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `System.IO.FileStream`. Vous pouvez déterminer la taille du tableau d’octets en obtenant la propriété `System.IO.FileStream` de l’objet `Length`.
   * Renseignez le tableau d’octets avec les données de flux en appelant la méthode `System.IO.FileStream` de l’objet `Read` et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’objet `BLOB` en attribuant le contenu du tableau d’octets au membre de données `MTOM` de l’objet `BLOB`.

1. Supprimez le chiffrement.

   Appelez la méthode `removePDFCertificateSecurity` de l’objet `EncryptionServiceClient` et transmettez les valeurs suivantes :

   * Objet `BLOB` contenant des données de flux de fichiers qui représentent un document PDF chiffré.
   * Une valeur string qui spécifie le nom d’alias de la clé publique qui correspond à la clé privée utilisée pour chiffrer le document PDFf.

   La méthode `removePDFCredentialSecurity` renvoie un objet `BLOB` contenant un document PDF non sécurisé.

1. Enregistrez le document PDF.

   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur string qui représente l’emplacement du fichier du document PDF non sécurisé.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `BLOB` renvoyé par la méthode `removePDFPasswordSecurity`. Renseignez le tableau d’octets en obtenant la valeur du membre de données `MTOM` de l’objet `BLOB`.
   * Créez un objet `System.IO.BinaryWriter` en appelant son constructeur et en transmettant l’objet `System.IO.FileStream`.
   * Ecrivez le contenu du tableau d’octets dans un fichier PDF en appelant la méthode `System.IO.BinaryWriter` de l’objet `Write` et en transmettant le tableau d’octets.

**Voir également**

[Résumé des étapes](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Appel d’AEM Forms à l’aide de MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Appel d’AEM Forms à l’aide de SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Suppression du chiffrement par mot de passe {#removing-password-encryption}

Le chiffrement avec mot de passe peut être supprimé d’un document PDF afin que les utilisateurs puissent ouvrir le document PDF dans Adobe Reader ou Acrobat sans avoir à spécifier de mot de passe. Une fois le chiffrement avec mot de passe supprimé d’un document PDF, le document n’est plus sécurisé.

>[!NOTE]
>
>Pour plus d’informations sur le service Encryption, voir [Référence des services pour AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary_of_steps-3}

Pour supprimer le chiffrement avec mot de passe d’un document PDF, procédez comme suit :

1. Inclure les fichiers de projet
1. Créez un client de service de chiffrement.
1. Obtenez le document PDF chiffré.
1. Supprimez le mot de passe.
1. Enregistrez le document PDF au format PDF.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

Les fichiers JAR suivants doivent être ajoutés au chemin de classe de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utility.jar (obligatoire si AEM Forms est déployé sur JBoss)
* jbossall-client.jar (obligatoire si AEM Forms est déployé sur JBoss)

**Création d’un client de service de chiffrement**

Pour effectuer par programmation une opération de service Encryption, vous devez créer un client de service Encryption. Si vous utilisez l’API Java Encryption Service, créez un objet `EncrytionServiceClient` . Si vous utilisez l’API du service Web Encryption Service, créez un objet `EncryptionServiceService` .

**Obtention du document PDF chiffré**

Vous devez obtenir un document PDF chiffré pour supprimer le chiffrement avec mot de passe. Si vous tentez de supprimer le chiffrement d’un document PDF non chiffré, une exception est générée.

**Suppression du mot de passe**

Pour supprimer le chiffrement avec mot de passe d’un document PDF chiffré, vous avez besoin d’un document PDF chiffré et d’une valeur de mot de passe maître utilisée pour supprimer le chiffrement du document PDF. Le mot de passe utilisé pour ouvrir un document PDF chiffré par mot de passe ne peut pas être utilisé pour supprimer le chiffrement. Un mot de passe principal est spécifié lorsque le document PDF est chiffré avec un mot de passe. (Voir [Chiffrement de documents PDF avec un mot de passe](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password).)

**Enregistrement du document PDF**

Une fois que le service Encryption a supprimé le chiffrement avec mot de passe d’un document PDF, vous pouvez enregistrer le document PDF en tant que fichier PDF. Les utilisateurs peuvent ouvrir le document PDF dans Adobe Reader ou Acrobat sans spécifier de mot de passe.

**Voir également**

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Démarrages rapides de l’API du service Encryption](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[Chiffrement de documents PDF avec un mot de passe](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### Supprimer le chiffrement avec mot de passe à l’aide de l’API Java {#remove-password-based-encryption-using-the-java-api}

Supprimez le chiffrement avec mot de passe d’un document PDF à l’aide de l’API Encryption (Java) :

1. Inclure les fichiers de projet.

   Incluez les fichiers JAR client, tels que adobe-encryption-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un client de service de chiffrement.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `EncryptionServiceClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`.

1. Obtenez le document PDF chiffré.

   * Créez un objet `java.io.FileInputStream` qui représente le document PDF chiffré en utilisant son constructeur et en transmettant une valeur string qui spécifie l’emplacement du document PDF.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Supprimez le mot de passe.

   Supprimez le chiffrement avec mot de passe du document PDF en appelant la méthode `removePDFPasswordSecurity` de l’objet `EncryptionServiceClient` et en transmettant les valeurs suivantes :

   * Objet `com.adobe.idp.Document` contenant le document PDF chiffré.
   * Une valeur string qui spécifie la valeur du mot de passe principal utilisé pour supprimer le chiffrement du document PDF.

   La méthode `removePDFPasswordSecurity` renvoie un objet `com.adobe.idp.Document` contenant un document PDF non sécurisé.

1. Enregistrez le document PDF.

   * Créez un objet `java.io.File` et assurez-vous que l’extension de nom de fichier est .pdf.
   * Appelez la méthode `copyToFile` de l’objet `com.adobe.idp.Document` pour copier le contenu de l’objet `Document` dans le fichier. Assurez-vous d’utiliser l’objet `Document` qui a été retourné par la méthode `removePDFPasswordSecurity`.

**Voir également**

[Démarrage rapide (mode SOAP) : Suppression du chiffrement avec mot de passe à l’aide de l’API Java](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-removing-password-based-encryption-using-the-java-api)

### Supprimer le chiffrement avec mot de passe à l’aide de l’API de service Web {#remove-password-based-encryption-using-the-web-service-api}

Supprimez le chiffrement avec mot de passe à l’aide de l’API Encryption (service Web) :

1. Inclure les fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Assurez-vous d’utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un client de service de chiffrement.

   * Créez un objet `EncryptionServiceClient` à l’aide de son constructeur par défaut.
   * Créez un objet `EncryptionServiceClient.Endpoint.Address` à l’aide du constructeur `System.ServiceModel.EndpointAddress`. Transmettez une valeur string qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/EncryptionService?WSDL`). Vous n’avez pas besoin d’utiliser l’attribut `lc_version`. Cet attribut est utilisé lorsque vous créez une référence de service.)
   * Créez un objet `System.ServiceModel.BasicHttpBinding` en obtenant la valeur du champ `EncryptionServiceClient.Endpoint.Binding`. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le champ `MessageEncoding` de l’objet `System.ServiceModel.BasicHttpBinding` sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Obtenez le document PDF chiffré.

   * Créez un objet `BLOB` en utilisant son constructeur. L’objet `BLOB` est utilisé pour stocker un document PDF chiffré par mot de passe.
   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur string qui représente l’emplacement du fichier du document PDF chiffré et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `System.IO.FileStream`. Vous pouvez déterminer la taille du tableau d’octets en obtenant la propriété `System.IO.FileStream` de l’objet `Length`.
   * Renseignez le tableau d’octets avec les données de flux en appelant la méthode `System.IO.FileStream` de l’objet `Read` et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’objet `BLOB` en attribuant le contenu du tableau d’octets au membre de données `MTOM` de l’objet `BLOB`.

1. Supprimez le mot de passe.

   Appelez la méthode `removePDFPasswordSecurity` de l’objet `EncryptionServiceService` et transmettez les valeurs suivantes :

   * Objet `BLOB` contenant des données de flux de fichiers qui représentent un document PDF chiffré.
   * Une valeur string qui spécifie la valeur de mot de passe utilisée pour supprimer le chiffrement du document PDF. Cette valeur est spécifiée lors du chiffrement du document PDF avec un mot de passe.

   La méthode `removePDFPasswordSecurity` renvoie un objet `BLOB` contenant un document PDF non sécurisé.

1. Enregistrez le document PDF.

   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur string qui représente l’emplacement du fichier du document PDF non sécurisé.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `BLOB` renvoyé par la méthode `removePDFPasswordSecurity`. Renseignez le tableau d’octets en obtenant la valeur du membre de données `MTOM` de l’objet `BLOB`.
   * Créez un objet `System.IO.BinaryWriter` en appelant son constructeur et en transmettant l’objet `System.IO.FileStream`.
   * Ecrivez le contenu du tableau d’octets dans un fichier PDF en appelant la méthode `System.IO.BinaryWriter` de l’objet `Write` et en transmettant le tableau d’octets.

**Voir également**

[Appel d’AEM Forms à l’aide de MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Appel d’AEM Forms à l’aide de SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Déverrouillage des documents PDF chiffrés {#unlocking-encrypted-pdf-documents}

Un document PDF chiffré par mot de passe ou par certificat doit être déverrouillé avant qu’une autre opération AEM Forms puisse être effectuée sur celui-ci. Si vous tentez d’effectuer une opération sur un document PDF chiffré, vous allez générer une exception. Après avoir déverrouillé un document PDF chiffré, vous pouvez y effectuer une ou plusieurs opérations. Ces opérations peuvent appartenir à d’autres services, tels que le service d’extensions Acrobat Reader DC.

>[!NOTE]
>
>Pour plus d’informations sur le service Encryption, voir [Référence des services pour AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary_of_steps-4}

Pour déverrouiller un document PDF chiffré, procédez comme suit :

1. Inclure les fichiers de projet.
1. Créez un client de service de chiffrement.
1. Obtenez le document PDF chiffré.
1. Déverrouillez le document.
1. Exécutez une opération AEM Forms.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

Les fichiers JAR suivants doivent être ajoutés au chemin de classe de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utility.jar (obligatoire si AEM Forms est déployé sur JBoss Application Server)
* jbossall-client.jar (obligatoire si AEM Forms est déployé sur JBoss Application Server)

**Création d’un client de service de chiffrement**

Pour effectuer par programmation une opération de service Encryption, vous devez créer un client de service Encryption. Si vous utilisez l’API Java Encryption Service, créez un objet `EncrytionServiceClient` . Si vous utilisez l’API du service Web Encryption Service, créez un objet `EncryptionServiceService` .

**Obtention du document PDF chiffré**

Vous devez obtenir un document PDF chiffré pour le déverrouiller. Si vous tentez de déverrouiller un document PDF non chiffré, une exception est générée.

**Déverrouiller le document**

Pour déverrouiller un document PDF chiffré par mot de passe, vous avez besoin d’un document PDF chiffré et d’une valeur de mot de passe utilisée pour ouvrir un document PDF chiffré par mot de passe. Cette valeur est spécifiée lors du chiffrement du document PDF avec un mot de passe. (Voir [Chiffrement de documents PDF avec un mot de passe](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password).)

Pour déverrouiller un document PDF chiffré par certificat, vous devez disposer à la fois d’un document PDF chiffré et de la valeur d’alias de la clé publique correspondant à la clé privée utilisée pour chiffrer le document PDF.

**Exécution d’une opération AEM Forms**

Une fois qu’un document PDF chiffré est déverrouillé, vous pouvez y effectuer une autre opération de service, par exemple lui appliquer des droits d’utilisation. Cette opération appartient au service Acrobat Reader DC Extensions.

**Voir également**

[Déverrouiller un document PDF chiffré à l’aide de l’API Java](encrypting-decrypting-pdf-documents.md#unlock-an-encrypted-pdf-document-using-the-java-api)

[Déverrouiller un document PDF chiffré à l’aide de l’API du service Web ;](encrypting-decrypting-pdf-documents.md#unlock-an-encrypted-pdf-document-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Démarrages rapides de l’API du service Encryption](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

### Déverrouillez un document PDF chiffré à l’aide de l’API Java {#unlock-an-encrypted-pdf-document-using-the-java-api}.

Déverrouillez un document PDF chiffré à l’aide de l’API Encryption (Java) :

1. Inclure les fichiers de projet.

   Incluez les fichiers JAR client, tels que adobe-encryption-client.jar, dans le chemin d’accès de classe de votre projet Java.

1. Créez un client de service de chiffrement.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `EncryptionServiceClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`.

1. Obtenez le document PDF chiffré.

   * Créez un objet `java.io.FileInputStream` qui représente le document PDF chiffré en utilisant son constructeur et en transmettant une valeur string qui spécifie l’emplacement du document PDF chiffré.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Déverrouillez le document.

   Déverrouillez un document PDF chiffré en appelant la méthode `EncryptionServiceClient` de l’objet `unlockPDFUsingPassword` ou `unlockPDFUsingCredential`.

   Pour déverrouiller un document PDF chiffré avec un mot de passe, appelez la méthode `unlockPDFUsingPassword` et transmettez les valeurs suivantes :

   * Objet `com.adobe.idp.Document` contenant le document PDF chiffré par mot de passe.
   * Une valeur string qui spécifie la valeur de mot de passe utilisée pour ouvrir un document PDF chiffré par mot de passe. Cette valeur est spécifiée lors du chiffrement du document PDF avec un mot de passe.

   Pour déverrouiller un document PDF chiffré avec un certificat, appelez la méthode `unlockPDFUsingCredential` et transmettez les valeurs suivantes :

   * Objet `com.adobe.idp.Document` contenant le document PDF chiffré par certificat.
   * Une valeur string qui spécifie le nom d’alias de la clé publique qui correspond à la clé privée utilisée pour chiffrer le document PDF.

   Les méthodes `unlockPDFUsingPassword` et `unlockPDFUsingCredential` renvoient toutes deux un objet `com.adobe.idp.Document` que vous transmettez à une autre méthode Java AEM Forms pour effectuer une opération.

1. Exécutez une opération AEM Forms.

   Exécutez une opération AEM Forms sur le document PDF déverrouillé pour répondre aux besoins de votre entreprise. Par exemple, si vous souhaitez appliquer des droits d’utilisation à un document PDF déverrouillé, transmettez l’objet `com.adobe.idp.Document` renvoyé par les méthodes `unlockPDFUsingPassword` ou `unlockPDFUsingCredential` à la méthode `ReaderExtensionsServiceClient` de l’objet `applyUsageRights`.

**Voir également**

[Résumé des étapes](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Démarrage rapide (mode SOAP) : Déverrouillage d’un document PDF chiffré à l’aide de l’API Java](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-unlocking-an-encrypted-pdf-document-using-the-java-api)  (mode SOAP)

[Application des droits d’utilisation aux documents PDF](/help/forms/developing/assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Déverrouillez un document PDF chiffré à l’aide de l’API de service Web {#unlock-an-encrypted-pdf-document-using-the-web-service-api}

Déverrouillez un document PDF chiffré à l’aide de l’API Encryption (service Web) :

1. Inclure les fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Assurez-vous d’utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un client de service de chiffrement.

   * Créez un objet `EncryptionServiceClient` à l’aide de son constructeur par défaut.
   * Créez un objet `EncryptionServiceClient.Endpoint.Address` à l’aide du constructeur `System.ServiceModel.EndpointAddress`. Transmettez une valeur string qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/EncryptionService?WSDL`). Vous n’avez pas besoin d’utiliser l’attribut `lc_version`. Cet attribut est utilisé lorsque vous créez une référence de service.)
   * Créez un objet `System.ServiceModel.BasicHttpBinding` en obtenant la valeur du champ `EncryptionServiceClient.Endpoint.Binding`. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le champ `MessageEncoding` de l’objet `System.ServiceModel.BasicHttpBinding` sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Obtenir un document PDF chiffré.

   * Créez un objet `BLOB` en utilisant son constructeur.
   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur string qui représente l’emplacement du fichier du document PDF chiffré et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `System.IO.FileStream`. Vous pouvez déterminer la taille du tableau d’octets en obtenant la propriété `System.IO.FileStream` de l’objet `Length`.
   * Renseignez le tableau d’octets avec les données de flux en appelant la méthode `System.IO.FileStream` de l’objet `Read` et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’objet `BLOB` en attribuant le contenu du tableau d’octets au membre de données `MTOM` de l’objet `BLOB`.

1. Déverrouillez le document.

   Déverrouillez un document PDF chiffré en appelant la méthode `EncryptionServiceClient` de l’objet `unlockPDFUsingPassword` ou `unlockPDFUsingCredential`.

   Pour déverrouiller un document PDF chiffré avec un mot de passe, appelez la méthode `unlockPDFUsingPassword` et transmettez les valeurs suivantes :

   * Objet `BLOB` contenant le document PDF chiffré par mot de passe.
   * Une valeur string qui spécifie la valeur de mot de passe utilisée pour ouvrir un document PDF chiffré par mot de passe. Cette valeur est spécifiée lors du chiffrement du document PDF avec un mot de passe.

   Pour déverrouiller un document PDF chiffré avec un certificat, appelez la méthode `unlockPDFUsingCredential` et transmettez les valeurs suivantes :

   * Objet `BLOB` contenant le document PDF chiffré par certificat.
   * Une valeur string qui spécifie le nom d’alias de la clé publique qui correspond à la clé privée utilisée pour chiffrer le document PDFf.

   Les méthodes `unlockPDFUsingPassword` et `unlockPDFUsingCredential` renvoient toutes deux un objet `com.adobe.idp.Document` que vous transmettez à une autre méthode AEM Forms pour effectuer une opération.

1. Exécutez une opération AEM Forms.

   Exécutez une opération AEM Forms sur le document PDF déverrouillé pour répondre aux besoins de votre entreprise. Par exemple, si vous souhaitez appliquer des droits d’utilisation au document PDF déverrouillé, transmettez l’objet `BLOB` renvoyé par les méthodes `unlockPDFUsingPassword` ou `unlockPDFUsingCredential` à la méthode `ReaderExtensionsServiceClient` de l’objet `applyUsageRights`.

**Voir également**

[Résumé des étapes](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Appel d’AEM Forms à l’aide de MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Appel d’AEM Forms à l’aide de SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Définition du type de chiffrement {#determining-encryption-type}

Vous pouvez déterminer par programmation le type de chiffrement qui protège un document PDF à l’aide de l’API Java Encryption Service ou de l’API du service Web Encryption Service. Il est parfois nécessaire de déterminer de manière dynamique si un document PDF est chiffré et, le cas échéant, le type de chiffrement. Par exemple, vous pouvez déterminer si un document PDF est protégé par un chiffrement avec mot de passe ou par une stratégie de Rights Management.

Un document PDF peut être protégé par les types de chiffrement suivants :

* Cryptage par mot de passe
* Cryptage basé sur un certificat
* Une stratégie créée par le service de Rights Management
* Autre type de cryptage

>[!NOTE]
>
>Pour plus d’informations sur le service Encryption, voir [Référence des services pour AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary_of_steps-5}

Pour déterminer le type de chiffrement qui protège un document PDF, procédez comme suit :

1. Inclure les fichiers de projet.
1. Créez un client de service de chiffrement.
1. Obtenez le document PDF chiffré.
1. Déterminez le type de chiffrement.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

Les fichiers JAR suivants doivent être ajoutés au chemin de classe de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utility.jar (obligatoire si AEM Forms est déployé sur JBoss Application Server)
* jbossall-client.jar (obligatoire si AEM Forms est déployé sur JBoss Application Server)

**Création d’un client de service**

Pour effectuer par programmation une opération de service Encryption, vous devez créer un client de service Encryption. Si vous utilisez l’API Java Encryption Service, créez un objet `EncrytionServiceClient` . Si vous utilisez l’API du service Web Encryption Service, créez un objet `EncryptionServiceService` .

**Obtention du document PDF chiffré**

Vous devez obtenir un document PDF pour déterminer le type de chiffrement qui le protège.

**Déterminer le type de chiffrement**

Vous pouvez déterminer le type de chiffrement qui protège un document PDF. Si le document PDF n’est pas protégé, le service Encryption vous informe que le document PDF n’est pas sécurisé.

**Voir également**

[Déterminer le type de chiffrement à l’aide de l’API Java](encrypting-decrypting-pdf-documents.md#determine-the-encryption-type-using-the-java-api)

[Déterminer le type de chiffrement à l’aide de l’API de service Web](encrypting-decrypting-pdf-documents.md#determine-the-encryption-type-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Démarrages rapides de l’API du service Encryption](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[Protection des documents avec des stratégies](/help/forms/developing/protecting-documents-policies.md#protecting-documents-with-policies)

### Déterminez le type de chiffrement à l’aide de l’API Java {#determine-the-encryption-type-using-the-java-api}

Déterminez le type de chiffrement qui protège un document PDF à l’aide de l’API Encryption (Java) :

1. Inclure les fichiers de projet.

   Incluez les fichiers JAR client, tels que adobe-encryption-client.jar, dans le chemin d’accès de classe de votre projet Java.

1. Créez un client de service.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `EncryptionServiceClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`.

1. Obtenez le document PDF chiffré.

   * Créez un objet `java.io.FileInputStream` qui représente le document PDF en utilisant son constructeur et en transmettant une valeur string qui spécifie l’emplacement du document PDF.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Déterminez le type de chiffrement.

   * Déterminez le type de chiffrement en appelant la méthode `EncryptionServiceClient` de l’objet `getPDFEncryption` et en transmettant l’objet `com.adobe.idp.Document` contenant le document PDF. Cette méthode renvoie un objet `EncryptionTypeResult` .
   * Appelez la méthode `getEncryptionType` de l’objet `EncryptionTypeResult`. Cette méthode renvoie une valeur d’énumération `EncryptionType` qui spécifie le type de chiffrement. Par exemple, si le document PDF est protégé par chiffrement avec mot de passe, cette méthode renvoie `EncryptionType.PASSWORD`.

**Voir également**

[Résumé des étapes](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Démarrage rapide (mode SOAP) : Détermination du type de chiffrement à l’aide de l’API Java](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-determining-encryption-type-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Déterminer le type de chiffrement à l’aide de l’API de service Web {#determine-the-encryption-type-using-the-web-service-api}

Déterminez le type de chiffrement qui protège un document PDF à l’aide de l’API Encryption (service Web) :

1. Inclure les fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Assurez-vous d’utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un client de service.

   * Créez un objet `EncryptionServiceClient` à l’aide de son constructeur par défaut.
   * Créez un objet `EncryptionServiceClient.Endpoint.Address` à l’aide du constructeur `System.ServiceModel.EndpointAddress`. Transmettez une valeur string qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/EncryptionService?WSDL`). Vous n’avez pas besoin d’utiliser l’attribut `lc_version`. Cet attribut est utilisé lorsque vous créez une référence de service.)
   * Créez un objet `System.ServiceModel.BasicHttpBinding` en obtenant la valeur du champ `EncryptionServiceClient.Endpoint.Binding`. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le champ `MessageEncoding` de l’objet `System.ServiceModel.BasicHttpBinding` sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Obtenez le document PDF chiffré.

   * Créez un objet `BLOB` en utilisant son constructeur.
   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur string qui représente l’emplacement du fichier du document PDF chiffré et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `System.IO.FileStream`. Vous pouvez déterminer la taille du tableau d’octets en obtenant la propriété `System.IO.FileStream` de l’objet `Length`.
   * Renseignez le tableau d’octets avec les données de flux en appelant la méthode `System.IO.FileStream` de l’objet `Read` et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’objet `BLOB` en attribuant le contenu du tableau d’octets au membre de données `MTOM` de l’objet `BLOB`.

1. Déterminez le type de chiffrement.

   * Appelez la méthode `getPDFEncryption` de l’objet `EncryptionServiceClient` et transmettez l’objet `BLOB` contenant le document PDF. Cette méthode renvoie un objet `EncryptionTypeResult` .
   * Obtenez la valeur de la méthode de données `encryptionType` de l’objet `EncryptionTypeResult`. Par exemple, si le document PDF est protégé par chiffrement avec mot de passe, la valeur de ce membre de données est `EncryptionType.PASSWORD`.

**Voir également**

[Résumé des étapes](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Appel d’AEM Forms à l’aide de MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Appel d’AEM Forms à l’aide de SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
