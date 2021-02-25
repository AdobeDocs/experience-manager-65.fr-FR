---
title: Protection des Documents avec des stratégies
seo-title: Protection des Documents avec des stratégies
description: Utilisez le service Document Security pour appliquer dynamiquement les paramètres de confidentialité aux documents Adobe PDF et pour conserver le contrôle des documents. Le service Document Security permet également aux utilisateurs de contrôler la manière dont les destinataires utilisent le document PDF protégé par une stratégie.
seo-description: Utilisez le service Document Security pour appliquer dynamiquement les paramètres de confidentialité aux documents Adobe PDF et pour conserver le contrôle des documents. Le service Document Security permet également aux utilisateurs de contrôler la manière dont les destinataires utilisent le document PDF protégé par une stratégie.
uuid: 6feb69ef-7b61-4d0b-8c87-d65d98bae9b5
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 9b1d2bf3-f28c-41b2-9026-1f3311556422
translation-type: tm+mt
source-git-commit: 9cf46a26d2aa2e41b924a4de89cf8ab5fdeeefc6
workflow-type: tm+mt
source-wordcount: '15558'
ht-degree: 4%

---


# Protection des Documents avec des stratégies {#protecting-documents-with-policies}

**Les exemples et exemples de ce document ne concernent que l’environnement AEM Forms on JEE.**

**À propos du service de sécurité Document**

Le service Document Security permet aux utilisateurs d&#39;appliquer de manière dynamique des paramètres de confidentialité aux documents Adobe PDF et de garder le contrôle sur les documents, quelle que soit leur diffusion.

Le service Document Security empêche la diffusion des informations au-delà de la portée de l’utilisateur en permettant à ce dernier de contrôler la manière dont les destinataires utilisent le document PDF protégé par une stratégie. Un utilisateur peut spécifier qui peut ouvrir un document, comment l’utiliser et contrôler le document une fois distribué. Un utilisateur peut également contrôler dynamiquement l’accès à un document protégé par une stratégie et peut même révoquer dynamiquement l’accès au document.

Le service Document Security protège également d&#39;autres types de fichiers tels que les fichiers Microsoft Word (fichiers DOC). Vous pouvez utiliser l&#39;API du client Document Security pour utiliser ces types de fichiers. Les versions suivantes sont prises en charge :

* Fichiers Microsoft Office 2003 (DOC, XLS, PPT)
* Fichiers Microsoft Office 2007 (fichiers DOCX, XLSX, PPTX)
* Fichiers PTC Pro/E

Pour plus de clarté, les deux sections suivantes traitent de la façon de travailler avec les documents Word :

* [Application de stratégies à des Documents Word](protecting-documents-policies.md#applying-policies-to-word-documents)
* [Suppression de stratégies des Documents Word](protecting-documents-policies.md#removing-policies-from-word-documents)

Vous pouvez exécuter ces tâches à l’aide du service Document Security :

* Créez des stratégies. Pour plus d&#39;informations, voir [Création de stratégies](protecting-documents-policies.md#creating-policies).
* permet de modifier des stratégies. Pour plus d&#39;informations, voir [Modification des stratégies](protecting-documents-policies.md#modifying-policies).
* supprimer des stratégies. Pour plus d&#39;informations, voir [Suppression de stratégies](protecting-documents-policies.md#deleting-policies).
* Appliquer des stratégies aux documents PDF. Pour plus d’informations, voir [Application de stratégies aux Documents PDF](protecting-documents-policies.md#applying-policies-to-pdf-documents).
* Supprimez les stratégies des documents PDF. Pour plus d’informations, voir [Suppression de stratégies des Documents PDF](protecting-documents-policies.md#removing-policies-from-pdf-documents).
* Documents Inspect protégés par une stratégie. Pour plus d’informations, voir [Inspection des Documents PDF protégés par une stratégie](protecting-documents-policies.md#inspecting-policy-protected-pdf-documents).
* Révoquer l’accès aux documents PDF. Pour plus d’informations, voir [Révocation de l’accès aux Documents](protecting-documents-policies.md#revoking-access-to-documents).
* Rétablit l’accès aux documents révoqués. Pour plus d&#39;informations, voir [Rétablissement de l&#39;accès aux Documents révoqués](protecting-documents-policies.md#reinstating-access-to-revoked-documents).
* Créez des filigranes. Pour plus d’informations, voir [Création de filigranes](protecting-documents-policies.md#creating-watermarks).
* Recherchez des événements. Pour plus d’informations, voir [Recherche de Événements](protecting-documents-policies.md#searching-for-events).

>[!NOTE]
>
>Pour plus d&#39;informations sur le service Document Security, consultez le [Guide de référence des services pour AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Création de stratégies {#creating-policies}

Vous pouvez créer des stratégies par programmation à l’aide de l’API Java de Document Security ou de l’API de service Web. Une *stratégie* est un ensemble d&#39;informations qui comprend les paramètres de sécurité du document, les utilisateurs autorisés et les droits d&#39;utilisation. Vous pouvez créer et enregistrer autant de stratégies que vous le souhaitez à l’aide de paramètres de sécurité adaptés à différentes situations et à différents utilisateurs.

Les stratégies vous permettent d’effectuer les tâches suivantes :

* Spécifiez les personnes qui peuvent ouvrir le document. Les destinataires peuvent appartenir à votre organisation ou être externes à celle-ci.
* Indiquez comment les destinataires peuvent utiliser le document. Vous pouvez restreindre l’accès à différentes fonctionnalités Acrobat et Adobe Reader. Ces fonctionnalités permettent d’imprimer et de copier du texte, d’ajouter des signatures et d’ajouter des commentaires à un document.
* Modifiez les paramètres d’accès et de sécurité à tout moment, même après avoir distribué le document protégé par une stratégie.
* Surveillez l’utilisation du document après sa distribution. Vous pouvez voir comment le document est utilisé et qui l’utilise. Par exemple, vous pouvez déterminer quand quelqu’un a ouvert le document.

### Création d’une stratégie à l’aide de services Web {#creating-a-policy-using-web-services}

Lors de la création d’une stratégie à l’aide de l’API de service Web, référencez un fichier XML PDRL (Portable Document Rights Language) qui décrit la stratégie. Les autorisations de stratégie et le principal sont définis dans le document PDRL. Le document XML suivant est un exemple de document PDRL.

```xml
 <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
 <Policy PolicyInstanceVersion="1" PolicyID="5DA3F847-DE76-F9CC-63EA-49A8D59154DE" PolicyCreationTime="2004-08-30T00:02:28.294+00:00" PolicyType="1" PolicySchemaVersion="1.0" PolicyName="SDK Test Policy -4344050357301573237" PolicyDescription="An SDK Test policy" xmlns="https://www.adobe.com/schema/1.0/pdrl">
       <PolicyEntry>
          <ns1:Permission PermissionName="com.adobe.aps.onlineOpen" Access="ALLOW" xmlns:ns1="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns2:Permission PermissionName="com.adobe.aps.offlineOpen" Access="ALLOW" xmlns:ns2="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns3:Permission PermissionName="com.adobe.aps.pdf.editNotes" Access="ALLOW" xmlns:ns3="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns4:Permission PermissionName="com.adobe.aps.pdf.fillAndSign" Access="ALLOW" xmlns:ns4="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
          <Principal PrincipalNameType="SYSTEM">
             <PrincipalDomain>EDC_SPECIAL</PrincipalDomain>
 
             <PrincipalName>all_internal_users</PrincipalName>
          </Principal>
       </PolicyEntry>
       <PolicyEntry>
          <ns5:Permission PermissionName="com.adobe.aps.onlineOpen" Access="ALLOW" xmlns:ns5="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns6:Permission PermissionName="com.adobe.aps.offlineOpen" Access="ALLOW" xmlns:ns6="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns7:Permission PermissionName="com.adobe.aps.pdf.copy" Access="ALLOW" xmlns:ns7="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns8:Permission PermissionName="com.adobe.aps.pdf.printLow" Access="ALLOW" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" xmlns:ns8="https://www.adobe.com/schema/1.0/pdrl" />
 
          <ns9:Permission PermissionName="com.adobe.aps.policySwitch" Access="ALLOW" xmlns:ns9="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns10:Permission PermissionName="com.adobe.aps.revoke" Access="ALLOW" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" xmlns:ns10="https://www.adobe.com/schema/1.0/pdrl" />
 
          <ns11:Permission PermissionName="com.adobe.aps.pdf.edit" Access="ALLOW" xmlns:ns11="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns12:Permission PermissionName="com.adobe.aps.pdf.editNotes" Access="ALLOW" xmlns:ns12="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns13:Permission PermissionName="com.adobe.aps.pdf.fillAndSign" Access="ALLOW" xmlns:ns13="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns14:Permission PermissionName="com.adobe.aps.pdf.printHigh" Access="ALLOW" xmlns:ns14="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <Principal PrincipalNameType="SYSTEM">
             <PrincipalDomain>EDC_SPECIAL</PrincipalDomain>
 
             <PrincipalName>publisher</PrincipalName>
          </Principal>
       </PolicyEntry>
 
       <OfflineLeasePeriod>
          <Duration>P31D</Duration>
       </OfflineLeasePeriod>
 
       <AuditSettings isTracked="true" />
 
       <PolicyValidityPeriod isAbsoluteTime="false">
          <ValidityPeriodRelative>
             <NotBeforeRelative>PT0S</NotBeforeRelative>
 
             <NotAfterRelative>P20D</NotAfterRelative>
          </ValidityPeriodRelative>
       </PolicyValidityPeriod>
 </Policy>
 
```

>[!NOTE]
>
>Pour plus d&#39;informations sur le service Document Security, consultez le [Guide de référence des services pour AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary-of-steps}

Pour créer une stratégie, procédez comme suit :

1. Incluez des fichiers de projet.
1. Créez un objet API Client de sécurité Document.
1. Définissez les attributs de la stratégie.
1. Créez une entrée de stratégie.
1. Enregistrez la stratégie.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

Les fichiers JAR suivants doivent être ajoutés au chemin de classe de votre projet :

* adobe-rightsmanagement-client.jar
* espace de nommage.jar (si AEM Forms est déployé sur JBoss)
* jaxb-api.jar (si AEM Forms est déployé sur JBoss)
* jaxb-impl.jar (si AEM Forms est déployé sur JBoss)
* jaxb-libs.jar (si AEM Forms est déployé sur JBoss)
* jaxb-xjc.jar (si AEM Forms est déployé sur JBoss)
* relaxngDatatype.jar (si AEM Forms est déployé sur JBoss)
* xsdlib.jar (si AEM Forms est déployé sur JBoss)
* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar
* jbossall-client.jar (utilisez un fichier JAR différent si AEM Forms n’est pas déployé sur JBoss)

Pour plus d’informations sur l’emplacement de ces fichiers JAR, voir [Inclusion de fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Création d’un objet API Client de sécurité Document**

Avant de pouvoir exécuter par programmation une opération du service Document Security, créez un objet client du service Document Security.

**Définir les attributs de la stratégie**

Pour créer une stratégie, définissez des attributs de stratégie. Un attribut obligatoire est le nom de la stratégie. Les noms de stratégie doivent être uniques pour chaque jeu de stratégies. Un jeu de stratégies est simplement un ensemble de stratégies. Il peut y avoir deux stratégies portant le même nom si elles appartiennent à des jeux de stratégies distincts. Toutefois, deux stratégies d’un même jeu de stratégies ne peuvent pas avoir le même nom de stratégie.

Un autre attribut utile à définir est la période de validité. Une période de validité est la période pendant laquelle un document protégé par une stratégie est accessible aux destinataires autorisés. Si vous ne définissez pas cet attribut, la stratégie est toujours valide.

Une période de validité peut être définie sur l’une des options suivantes :

* Nombre défini de jours pendant lesquels le document est accessible à partir du moment où le document est publié.
* Date de fin après laquelle le document n&#39;est pas accessible
* Période spécifique pour laquelle le document est accessible
* Toujours valide

Vous pouvez spécifier uniquement une date de début, ce qui signifie que la stratégie est valide après la date de début. Si vous indiquez uniquement une date de fin, la stratégie est valide jusqu’à la date de fin. Cependant, une exception est générée si aucune date de début et une date de fin n’est définie.

Lors de la définition d’attributs appartenant à une stratégie, vous pouvez également définir des paramètres de chiffrement. Ces paramètres de chiffrement prennent effet lorsque la stratégie est appliquée à un document. Vous pouvez spécifier les valeurs de chiffrement suivantes :

* **AES256** : Représente l’algorithme de chiffrement AES avec une clé de 256 bits.
* **AES128** : Représente l’algorithme de chiffrement AES avec une clé de 128 bits.
* **NoEncryption : ne** représente aucun chiffrement.

Lors de la spécification de l&#39;option `NoEncryption`, vous ne pouvez pas définir l&#39;option `PlaintextMetadata` sur `false`. Si vous tentez de le faire, une exception est levée.

>[!NOTE]
>
>Pour plus d&#39;informations sur les autres attributs que vous pouvez définir, consultez la description de l&#39;interface `Policy` dans la [Référence de l&#39;API AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Création d’une entrée de stratégie**

Une entrée de stratégie associe des entités, qui sont des groupes et des utilisateurs, et des autorisations à une stratégie. Une stratégie doit comporter au moins une entrée de stratégie. Supposons, par exemple, que vous effectuiez les tâches suivantes :

* Créez et enregistrez une entrée de stratégie qui permet à un groupe de ne vue qu&#39;un document en ligne et interdit aux destinataires de la copier.
* Joignez l’entrée de stratégie à la stratégie.
* Sécurisez un document avec la stratégie en utilisant Acrobat.

Ces actions ont pour conséquence que les destinataires ne peuvent que vue en ligne du document et ne peuvent pas le copier. Le document reste sécurisé jusqu&#39;à ce que la sécurité en soit supprimée.

**Enregistrer la stratégie**

Une nouvelle stratégie doit être enregistrée avant de pouvoir être utilisée. Après avoir enregistré une stratégie, vous pouvez l’utiliser pour protéger les documents.

### Créez une stratégie à l’aide de l’API Java {#create-a-policy-using-the-java-api}

Créez une stratégie à l’aide de l’API Document Security (Java) :

1. Incluez des fichiers de projet.

   Incluez des fichiers JAR client, tels que adobe-rightsmanagement-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un objet API Client de sécurité Document.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `DocumentSecurityClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`. 

1. Définissez les attributs de la stratégie.

   * Créez un objet `Policy` en appelant la méthode statique `InfomodelObjectFactory` de l&#39;objet `createPolicy`. Cette méthode renvoie un objet `Policy`.
   * Définissez l’attribut name de la stratégie en appelant la méthode `Policy` de l’objet `setName` et en transmettant une valeur de chaîne qui spécifie le nom de la stratégie.
   * Définissez la description de la stratégie en appelant la méthode `Policy` de l&#39;objet `setDescription` et en transmettant une valeur de chaîne qui spécifie la description de la stratégie.
   * Définissez le jeu de stratégies auquel appartient la nouvelle stratégie en appelant la méthode `Policy` de l&#39;objet `setPolicySetName` et en transmettant une valeur de chaîne qui spécifie le nom du jeu de stratégies. (Vous pouvez spécifier `null` pour cette valeur de paramètre afin que la stratégie soit ajoutée au jeu de stratégies *Mes stratégies*.)
   * Créez la période de validité de la stratégie en appelant la méthode statique `createValidityPeriod` de l’objet `InfomodelObjectFactory`. Cette méthode renvoie un objet `ValidityPeriod`.
   * Définissez le nombre de jours pendant lesquels un document protégé par une stratégie est accessible en appelant la méthode `ValidityPeriod` de l’objet `setRelativeExpirationDays` et en transmettant un nombre entier spécifiant le nombre de jours.
   * Définissez la période de validité de la stratégie en appelant la méthode `Policy` de l&#39;objet `setValidityPeriod` et en transmettant l&#39;objet `ValidityPeriod`.

1. Créez une entrée de stratégie.

   * Créez une entrée de stratégie en appelant la méthode statique `createPolicyEntry` de l&#39;objet `InfomodelObjectFactory`. Cette méthode renvoie un objet `PolicyEntry`.
   * Spécifiez les autorisations de la stratégie en appelant la méthode `InfomodelObjectFactory` statique `createPermission` de l’objet. Transmettez un membre de données statiques qui appartient à l&#39;interface `Permission` qui représente l&#39;autorisation. Cette méthode renvoie un objet `Permission`. Par exemple, pour ajouter l’autorisation permettant aux utilisateurs de copier des données d’un document PDF protégé par une stratégie, transmettez `Permission.COPY`. (Répétez cette étape pour chaque autorisation d’ajout).
   * Ajoutez l&#39;autorisation d&#39;accès à l&#39;entrée de stratégie en appelant la méthode `PolicyEntry` de l&#39;objet `addPermission` et en transmettant l&#39;objet `Permission`. (Répétez cette étape pour chaque objet `Permission` que vous avez créé).
   * Créez le principal de stratégie en appelant la méthode statique `createSpecialPrincipal` de l&#39;objet `InfomodelObjectFactory`. Transmettez un membre de données qui appartient à l&#39;objet `InfomodelObjectFactory` qui représente l&#39;entité de sécurité. Cette méthode renvoie un objet `Principal`. Par exemple, pour ajouter l’éditeur du document en tant que principal, transmettez `InfomodelObjectFactory.PUBLISHER_PRINCIPAL`.
   * Ajoutez l&#39;entité de sécurité à l&#39;entrée de stratégie en appelant la méthode `PolicyEntry` de l&#39;objet `setPrincipal`et en transmettant l&#39;objet `Principal`.
   * Ajoutez l&#39;entrée de stratégie à la stratégie en appelant la méthode `Policy` de l&#39;objet `addPolicyEntry` et en transmettant l&#39;objet `PolicyEntry`.

1. Enregistrez la stratégie.

   * Créez un objet `PolicyManager` en appelant la méthode `DocumentSecurityClient` de l&#39;objet `getPolicyManager`.
   * Enregistrez la stratégie en appelant la méthode `registerPolicy` de l&#39;objet `PolicyManager` et en transmettant les valeurs suivantes :

      * Objet `Policy` représentant la stratégie à enregistrer.
   * Valeur de chaîne qui représente le jeu de stratégies auquel appartient la stratégie.

   Si vous utilisez un compte d’administrateur AEM forms dans les paramètres de connexion pour créer l’objet `DocumentSecurityClient`, indiquez le nom du jeu de stratégies lorsque vous appelez la méthode `registerPolicy`. Si vous transmettez une valeur `null` pour le jeu de stratégies, la stratégie est créée dans le jeu de stratégies *Mes stratégies* des administrateurs.

   Si vous utilisez un utilisateur Document Security dans les paramètres de connexion, vous pouvez appeler la méthode `registerPolicy` surchargée qui accepte uniquement la stratégie. En d’autres termes, vous n’avez pas besoin de spécifier le nom du jeu de stratégies. Cependant, la stratégie est ajoutée au jeu de stratégies nommé *Mes stratégies*. Si vous ne souhaitez pas ajouter la nouvelle stratégie à ce jeu de stratégies, spécifiez un nom de jeu de stratégies lorsque vous appelez la méthode `registerPolicy`.

   >[!NOTE]
   >
   >Lors de la création d’une stratégie, référencez un jeu de stratégies existant. Si vous spécifiez un jeu de stratégies qui n’existe pas, une exception est générée.

Pour obtenir des exemples de code à l’aide du service Document Security, reportez-vous aux sections suivantes :

* &quot;Début rapide (mode SOAP) : Création d’une stratégie à l’aide de l’API Java&quot;

### Créez une stratégie à l’aide de l’API de service Web {#create-a-policy-using-the-web-service-api}

Créez une stratégie à l’aide de l’API Document Security (service Web) :

1. Incluez des fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Assurez-vous d’utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un objet API Client de sécurité Document.

   * Créez un objet `DocumentSecurityServiceClient` en utilisant son constructeur par défaut.
   * Créez un objet `DocumentSecurityServiceClient.Endpoint.Address` en utilisant le constructeur `System.ServiceModel.EndpointAddress`. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/RightsManagementService?WSDL`). Vous n&#39;avez pas besoin d&#39;utiliser l&#39;attribut `lc_version`. Cet attribut est utilisé lorsque vous créez une référence de service.)
   * Créez un objet `System.ServiceModel.BasicHttpBinding` en obtenant la valeur du champ `RightsManagementServiceClient.Endpoint.Binding`. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le champ `MessageEncoding` de l’objet `System.ServiceModel.BasicHttpBinding` sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en exécutant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * Affectez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Affectez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.


1. Définissez les attributs de la stratégie.

   * Créez un objet `PolicySpec` en utilisant son constructeur.
   * Définissez le nom de la stratégie en attribuant une valeur de chaîne au membre de données `name` de l&#39;objet `PolicySpec`.
   * Définissez la description de la stratégie en attribuant une valeur de chaîne au membre de données `description` de l&#39;objet `PolicySpec`.
   * Définissez le jeu de stratégies auquel la stratégie doit appartenir en attribuant une valeur de chaîne au membre de données `policySetName` de l&#39;objet `PolicySpec`. Vous devez spécifier un nom de jeu de stratégies existant. (Vous pouvez spécifier `null` pour cette valeur de paramètre afin que la stratégie soit ajoutée à *Mes stratégies*.)
   * Définissez la période d’ouverture hors connexion de la stratégie en attribuant une valeur entière au membre de données `offlineLeasePeriod` de l’objet `PolicySpec`.
   * Définissez le membre de données `policyXml` de l’objet `PolicySpec` avec une valeur de chaîne qui représente les données XML PDRL. Pour exécuter cette tâche, créez un objet .NET `StreamReader` à l&#39;aide de son constructeur. Transférez l&#39;emplacement d&#39;un fichier XML PDRL représentant la stratégie au constructeur `StreamReader`. Ensuite, appelez la méthode `StreamReader` de l’objet `ReadLine` et affectez la valeur renvoyée à une variable de chaîne. Effectuez une itération sur l’objet `StreamReader` jusqu’à ce que la méthode `ReadLine` renvoie null. Affectez la variable string au membre de données `policyXml` de l’objet `PolicySpec`.

1. Créez une entrée de stratégie.

   Il n’est pas nécessaire de créer une entrée de stratégie lors de la création d’une stratégie à l’aide de l’API du service Web Document Security. L&#39;entrée de stratégie est définie dans le document PDRL.

1. Enregistrez la stratégie.

   Enregistrez la stratégie en appelant la méthode `registerPolicy` de l&#39;objet `DocumentSecurityServiceClient` et en transmettant les valeurs suivantes :

   * Objet `PolicySpec` représentant la stratégie à enregistrer.
   * Valeur de chaîne qui représente le jeu de stratégies auquel appartient la stratégie. Vous pouvez spécifier une valeur `null` qui entraîne l’ajout de la stratégie au jeu de stratégies *MyPolices*.

   Si vous utilisez un compte d’administrateur AEM forms dans les paramètres de connexion pour créer l’objet `DocumentSecurityClient`, spécifiez le nom du jeu de stratégies lorsque vous appelez la méthode `registerPolicy`.

   Si vous utilisez un utilisateur Document SecurityDocument Security dans les paramètres de connexion, vous pouvez appeler la méthode `registerPolicy` surchargée qui accepte uniquement la stratégie. En d’autres termes, vous n’avez pas besoin de spécifier le nom du jeu de stratégies. Cependant, la stratégie est ajoutée au jeu de stratégies nommé *Mes stratégies*. Si vous ne souhaitez pas ajouter la nouvelle stratégie à ce jeu de stratégies, spécifiez un nom de jeu de stratégies lorsque vous appelez la méthode `registerPolicy`.

   >[!NOTE]
   >
   >Lors de la création d’une stratégie et de la spécification d’un jeu de stratégies, veillez à spécifier un jeu de stratégies existant. Si vous spécifiez un jeu de stratégies qui n’existe pas, une exception est générée.

Pour obtenir des exemples de code à l’aide du service Document Security, reportez-vous aux Débuts rapides suivants :

* &quot;Début rapide (MTOM) : Création d’une stratégie à l’aide de l’API du service Web&quot;
* &quot;Quick Début (SwaRef) : Création d’une stratégie à l’aide de l’API du service Web&quot;

## Modification de stratégies {#modifying-policies}

Vous pouvez modifier une stratégie existante à l’aide de l’API Java Document Security ou de l’API de service Web. Pour apporter des modifications à une stratégie existante, vous devez la récupérer, la modifier, puis la mettre à jour sur le serveur. Supposons, par exemple, que vous récupériez une stratégie existante et étendiez sa période de validité. Avant que la modification ne prenne effet, vous devez mettre à jour la stratégie.

Vous pouvez modifier une stratégie lorsque les besoins de l’entreprise changent et que la stratégie ne reflète plus ces besoins. Au lieu de créer une nouvelle stratégie, vous pouvez simplement mettre à jour une stratégie existante.

Pour modifier les attributs de stratégie à l’aide d’un service Web (par exemple, à l’aide de classes proxy Java créées avec JAX-WS), vous devez vous assurer que la stratégie est enregistrée auprès du service Document Security. Vous pouvez ensuite référencer la stratégie existante à l&#39;aide de la méthode `PolicySpec.getPolicyXml` et modifier les attributs de la stratégie à l&#39;aide des méthodes applicables. Par exemple, vous pouvez modifier la période d’ouverture hors connexion en appelant la méthode `PolicySpec.setOfflineLeasePeriod`.

>[!NOTE]
>
>Pour plus d&#39;informations sur le service Document Security, consultez le [Guide de référence des services pour AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary_of_steps-1}

Pour modifier une stratégie existante, procédez comme suit :

1. Incluez des fichiers de projet.
1. Créez un objet API Client de sécurité Document.
1. Récupérez une stratégie existante.
1. Modifiez les attributs des stratégies.
1. Mettez à jour la stratégie.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

**Création d’un objet API Client de sécurité Document**

Avant de pouvoir exécuter par programmation une opération Document Security, vous devez créer un objet client de service Document Security. Si vous utilisez l’API Java, créez un objet `RightsManagementClient`. Si vous utilisez l&#39;API du service Web Document Security, créez un objet `RightsManagementServiceService`.

**Récupération d’une stratégie existante**

Vous devez récupérer une stratégie existante pour la modifier. Pour récupérer une stratégie, spécifiez le nom de la stratégie et le jeu de stratégies auquel elle appartient. Si vous spécifiez une valeur `null` pour le nom du jeu de stratégies, la stratégie est récupérée à partir du jeu de stratégies *Mes stratégies*.

**Définir les attributs de la stratégie**

Pour modifier une stratégie, vous modifiez la valeur des attributs de stratégie. Le seul attribut de stratégie que vous ne pouvez pas modifier est l’attribut name. Par exemple, pour modifier la période d’ouverture hors connexion de la stratégie, vous pouvez modifier la valeur de l’attribut de période d’ouverture hors connexion de la stratégie.

Lors de la modification de la période d’ouverture hors connexion d’une stratégie à l’aide d’un service Web, le champ `offlineLeasePeriod` de l’interface `PolicySpec` est ignoré. Pour mettre à jour la période d’ouverture hors connexion, modifiez l’élément `OfflineLeasePeriod` dans le document XML PDRL. Faites ensuite référence au document XML PDRL mis à jour en utilisant le membre de données `policyXML` de l&#39;interface `PolicySpec`.

>[!NOTE]
>
>Pour plus d&#39;informations sur les autres attributs que vous pouvez définir, consultez la description de l&#39;interface `Policy` dans la [Référence de l&#39;API AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Mettre à jour la stratégie**

Avant que les modifications apportées à une stratégie ne prennent effet, vous devez mettre à jour la stratégie avec le service Document Security. Les modifications apportées aux stratégies qui protègent les documents sont mises à jour la prochaine fois que le document protégé par une stratégie est synchronisé avec le service Document Security.

### Modifier les stratégies existantes à l’aide de l’API Java {#modify-existing-policies-using-the-java-api}

Modifiez une stratégie existante à l’aide de l’API Document Security (Java) :

1. Incluez des fichiers de projet.

   Incluez des fichiers JAR client, tels que adobe-rightsmanagement-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un objet API Client de sécurité Document.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `RightsManagementClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`. 

1. Récupérez une stratégie existante.

   * Créez un objet `PolicyManager` en appelant la méthode `RightsManagementClient` de l&#39;objet `getPolicyManager`.
   * Créez un objet `Policy` qui représente la stratégie à mettre à jour en appelant la méthode `PolicyManager` de l&#39;objet `getPolicy` et en transmettant les valeurs suivantes.&quot;

      * Valeur de chaîne qui représente le nom du jeu de stratégies auquel appartient la stratégie. Vous pouvez spécifier `null` pour que le jeu de stratégies `MyPolicies` soit utilisé.
      * Valeur de chaîne qui représente le nom de la stratégie.

1. Définissez les attributs de la stratégie.

   Modifiez les attributs de la stratégie pour répondre aux besoins de votre entreprise. Par exemple, pour modifier la période d’ouverture hors connexion de la stratégie, appelez la méthode `Policy` de l’objet `setOfflineLeasePeriod`.

1. Mettez à jour la stratégie.

   Mettez à jour la stratégie en appelant la méthode `updatePolicy` de l&#39;objet `PolicyManager`. Transmettez l&#39;objet `Policy` qui représente la stratégie à mettre à jour.

**Exemples de code**

Pour obtenir des exemples de code à l’aide du service Document Security, voir le Début rapide (mode SOAP) : Modification d’une stratégie à l’aide de la section API Java.

### Modifier les stratégies existantes à l’aide de l’API de service Web {#modify-existing-policies-using-the-web-service-api}

Modifiez une stratégie existante à l’aide de l’API Document Security (service Web) :

1. Incluez des fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Assurez-vous d’utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un objet API Client de sécurité Document.

   * Créez un objet `RightsManagementServiceClient` en utilisant son constructeur par défaut.
   * Créez un objet `RightsManagementServiceClient.Endpoint.Address` en utilisant le constructeur `System.ServiceModel.EndpointAddress`. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/RightsManagementService?WSDL`). Vous n&#39;avez pas besoin d&#39;utiliser l&#39;attribut `lc_version`. Cet attribut est utilisé lorsque vous créez une référence de service.)
   * Créez un objet `System.ServiceModel.BasicHttpBinding` en obtenant la valeur du champ `RightsManagementServiceClient.Endpoint.Binding`. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le champ `MessageEncoding` de l’objet `System.ServiceModel.BasicHttpBinding` sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en exécutant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * Affectez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Affectez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.


1. Récupérez une stratégie existante.

   Créez un objet `PolicySpec` qui représente la stratégie à modifier en appelant la méthode `RightsManagementServiceClient` de l&#39;objet `getPolicy` et en transmettant les valeurs suivantes :

   * Valeur de chaîne qui spécifie le nom du jeu de stratégies auquel appartient la stratégie. Vous pouvez spécifier `null` pour que le jeu de stratégies `MyPolicies` soit utilisé.
   * Valeur de chaîne qui spécifie le nom de la stratégie.

1. Définissez les attributs de la stratégie.

   Modifiez les attributs de la stratégie pour répondre aux besoins de votre entreprise.

1. Mettez à jour la stratégie.

   Mettez à jour la stratégie en appelant la méthode `RightsManagementServiceClient` de l&#39;objet `updatePolicyFromSDK` et en transmettant l&#39;objet `PolicySpec` représentant la stratégie à mettre à jour.

**Exemples de code**

Pour obtenir des exemples de code à l’aide du service Document Security, reportez-vous aux Débuts rapides suivants :

* &quot;Début rapide (MTOM) : Modification d’une stratégie à l’aide de l’API du service Web&quot;
* &quot;Quick Début (SwaRef) : Modification d’une stratégie à l’aide de l’API du service Web&quot;

## Suppression de stratégies {#deleting-policies}

Vous pouvez supprimer une stratégie existante à l’aide de l’API Java Document Security ou de l’API de service Web. Une fois une stratégie supprimée, elle ne peut plus être utilisée pour protéger les documents. Cependant, les documents existants protégés par une stratégie qui utilisent la stratégie sont toujours protégés. Vous pouvez supprimer une stratégie lorsqu’une nouvelle stratégie devient disponible.

>[!NOTE]
>
>Pour plus d&#39;informations sur le service Document Security, consultez le [Guide de référence des services pour AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary_of_steps-2}

Pour supprimer une stratégie existante, procédez comme suit :

1. Inclure les fichiers de projet
1. Créez un objet API Client de sécurité Document.
1. Supprimez la stratégie.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

**Création d’un objet API Client de sécurité Document**

Avant de pouvoir exécuter par programmation une opération du service Document Security, vous devez créer un objet client du service Document Security. Si vous utilisez l’API Java, créez un objet `RightsManagementClient`. Si vous utilisez l&#39;API du service Web Document Security, créez un objet `RightsManagementServiceService`.

**Supprimer la stratégie**

Pour supprimer une stratégie, vous spécifiez la stratégie à supprimer et le jeu de stratégies auquel elle appartient. L’utilisateur dont les paramètres sont utilisés pour appeler AEM Forms doit être autorisé à supprimer la stratégie ; dans le cas contraire, une exception se produit. De même, si vous tentez de supprimer une stratégie qui n’existe pas, une exception se produit.

### Supprimer des stratégies à l’aide de l’API Java {#delete-policies-using-the-java-api}

Supprimez une stratégie à l’aide de l’API Document Security (Java) :

1. Incluez des fichiers de projet.

   Incluez des fichiers JAR client, tels que adobe-rightsmanagement-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un objet API Client de sécurité Document.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `RightsManagementClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`. 

1. Supprimez la stratégie.

   * Créez un objet `PolicyManager` en appelant la méthode `RightsManagementClient` de l&#39;objet `getPolicyManager`.
   * Supprimez la stratégie en appelant la méthode `deletePolicy` de l&#39;objet `PolicyManager` et en transmettant les valeurs suivantes :

      * Valeur de chaîne qui spécifie le nom du jeu de stratégies auquel appartient la stratégie. Vous pouvez spécifier `null` pour que le jeu de stratégies `MyPolicies` soit utilisé.
      * Valeur de chaîne qui spécifie le nom de la stratégie à supprimer.

**Exemples de code**

Pour obtenir des exemples de code à l’aide du service Document Security, reportez-vous aux Débuts rapides suivants :

* &quot;Début rapide (mode SOAP) : Suppression d’une stratégie à l’aide de l’API Java&quot;

### Supprimer des stratégies à l’aide de l’API de service Web {#delete-policies-using-the-web-service-api}

Supprimez une stratégie à l’aide de l’API Document Security (service Web) :

1. Incluez des fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Assurez-vous d’utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un objet API Client de sécurité Document.

   * Créez un objet `RightsManagementServiceClient` en utilisant son constructeur par défaut.
   * Créez un objet `RightsManagementServiceClient.Endpoint.Address` en utilisant le constructeur `System.ServiceModel.EndpointAddress`. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/RightsManagementService?WSDL`). Vous n&#39;avez pas besoin d&#39;utiliser l&#39;attribut `lc_version`. Cet attribut est utilisé lorsque vous créez une référence de service.)
   * Créez un objet `System.ServiceModel.BasicHttpBinding` en obtenant la valeur du champ `RightsManagementServiceClient.Endpoint.Binding`. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le champ `MessageEncoding` de l’objet `System.ServiceModel.BasicHttpBinding` sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en exécutant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * Affectez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Affectez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.


1. Supprimez la stratégie.

   Supprimez une stratégie en appelant la méthode `deletePolicy` de l&#39;objet `RightsManagementServiceClient` et en transmettant les valeurs suivantes :

   * Valeur de chaîne qui spécifie le nom du jeu de stratégies auquel appartient la stratégie. Vous pouvez spécifier `null` pour que le jeu de stratégies `MyPolicies` soit utilisé.
   * Valeur de chaîne qui spécifie le nom de la stratégie à supprimer.

**Exemples de code**

Pour obtenir des exemples de code à l’aide du service Document Security, reportez-vous aux Débuts rapides suivants :

* &quot;Début rapide (MTOM) : Suppression d’une stratégie à l’aide de l’API du service Web&quot;
* &quot;Quick Début (SwaRef) : Suppression d’une stratégie à l’aide de l’API du service Web&quot;

## Application de stratégies à des Documents PDF {#applying-policies-to-pdf-documents}

Vous pouvez appliquer une stratégie à un document PDF afin de sécuriser le document. En appliquant une stratégie à un document PDF, vous restreignez l’accès au document. Vous ne pouvez pas appliquer une stratégie à un document si le document est déjà sécurisé avec une stratégie.

Pendant que le document est ouvert, vous pouvez également restreindre l’accès aux fonctionnalités Acrobat et Adobe Reader, y compris la possibilité d’imprimer et de copier du texte, d’apporter des modifications et d’ajouter des signatures et des commentaires à un document. En outre, vous pouvez révoquer un document PDF protégé par une stratégie lorsque vous ne souhaitez plus que les utilisateurs accèdent au document.

Vous pouvez contrôler l’utilisation d’un document protégé par une stratégie après l’avoir distribué. C&#39;est-à-dire, vous pouvez voir comment le document est utilisé et qui l&#39;utilise. Par exemple, vous pouvez savoir quand quelqu’un a ouvert le document.

>[!NOTE]
>
>Pour plus d&#39;informations sur le service Document Security, consultez le [Guide de référence des services pour AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary_of_steps-3}

Pour appliquer une stratégie à un document PDF, procédez comme suit :

1. Incluez des fichiers de projet.
1. Créez un objet API Client de sécurité Document.
1. Récupérez un document PDF auquel une stratégie est appliquée.
1. Appliquez une stratégie existante au document PDF.
1. Enregistrez le document PDF protégé par une stratégie.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

**Création d’un objet API Client de sécurité Document**

Avant de pouvoir exécuter par programmation une opération du service Document Security, créez un objet client du service Document Security. Si vous utilisez l’API Java, créez un objet `DocumentSecurityClient`. Si vous utilisez l&#39;API du service Web Document Security, créez un objet `DocumentSecurityServiceService`.

**Récupération d’un document PDF**

Vous pouvez récupérer un document PDF afin d’appliquer une stratégie. Une fois que vous avez appliqué une stratégie au document PDF, les utilisateurs sont limités lors de l’utilisation du document. Par exemple, si la stratégie ne permet pas l’ouverture du document hors ligne, les utilisateurs doivent être en ligne pour ouvrir le document.

**Appliquer une stratégie existante au document PDF**

Pour appliquer une stratégie à un document PDF, référencez une stratégie existante et indiquez à quel jeu de stratégies elle appartient. L’utilisateur qui définit les propriétés de connexion doit avoir accès à la stratégie spécifiée. Dans le cas contraire, une exception se produit.

**Enregistrer le document PDF**

Une fois que le service Document Security a appliqué une stratégie à un document PDF, vous pouvez enregistrer le document PDF protégé par une stratégie en tant que fichier PDF.

**Voir également**

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Révocation de l’accès aux Documents](protecting-documents-policies.md#revoking-access-to-documents)

### Appliquer une stratégie à un document PDF à l’aide de l’API Java {#apply-a-policy-to-a-pdf-document-using-the-java-api}

Appliquez une stratégie à un document PDF à l’aide de l’API Document Security (Java) :

1. Incluez des fichiers de projet.

   Incluez des fichiers JAR client, tels que adobe-rightsmanagement-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un objet API Client de sécurité Document.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `RightsManagementClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`. 

1. Récupérez un document PDF.

   * Créez un objet `java.io.FileInputStream` qui représente le document PDF à l’aide de son constructeur. Transmettez une valeur de chaîne qui spécifie l’emplacement du document PDF.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Appliquez une stratégie existante au document PDF.

   * Créez un objet `DocumentManager` en appelant la méthode `RightsManagementClient` de l&#39;objet `getDocumentManager`.
   * Appliquez une stratégie au document PDF en appelant la méthode `DocumentManager` de l’objet `protectDocument` et en transmettant les valeurs suivantes :

      * Objet `com.adobe.idp.Document` contenant le document PDF auquel la stratégie est appliquée.
      * Valeur de chaîne qui spécifie le nom du document.
      * Valeur de chaîne qui spécifie le nom du jeu de stratégies auquel appartient la stratégie. Vous pouvez spécifier une valeur `null` qui se traduit par l&#39;utilisation du jeu de stratégies `MyPolicies`.
      * Valeur de chaîne qui spécifie le nom de la stratégie.
      * Valeur de chaîne qui représente le nom du domaine du gestionnaire d’utilisateurs de l’utilisateur qui est l’éditeur du document. Cette valeur de paramètre est facultative et peut être nulle (si ce paramètre est nul, la valeur de paramètre suivante doit être nulle).
      * Valeur de chaîne qui représente le nom canonique de l’utilisateur du gestionnaire d’utilisateurs qui est l’éditeur du document. Cette valeur de paramètre est facultative et peut être `null` (si ce paramètre est nul, la valeur de paramètre précédente doit être `null`).
      * `com.adobe.livecycle.rightsmanagement.Locale` qui représente le paramètre régional utilisé pour sélectionner le modèle MS Office. Cette valeur de paramètre est facultative et n’est pas utilisée pour les documents PDF. Pour sécuriser un document PDF, spécifiez `null`.

      La méthode `protectDocument` renvoie un objet `RMSecureDocumentResult` contenant le document PDF protégé par une stratégie.


1. Enregistrez le document PDF.

   * Appelez la méthode `RMSecureDocumentResult` de l’objet `getProtectedDoc` pour obtenir le document PDF protégé par une stratégie. Cette méthode renvoie un objet `com.adobe.idp.Document`.
   * Créez un objet `java.io.File` et assurez-vous que l’extension de fichier est PDF.
   * Appelez la méthode `com.adobe.idp.Document` de l&#39;objet `copyToFile` pour copier le contenu de l&#39;objet `Document` dans le fichier (veillez à utiliser l&#39;objet `Document` renvoyé par la méthode `getProtectedDoc`).

**Exemples de code**

Pour obtenir des exemples de code à l’aide du service Document Security, reportez-vous aux Débuts rapides suivants :

* &quot;Début rapide (mode EJB) : Application d’une stratégie à un document PDF à l’aide de l’API Java&quot;
* &quot;Début rapide (mode SOAP) : Application d’une stratégie à un document PDF à l’aide de l’API Java&quot;

**Voir également**

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Appliquer une stratégie à un document PDF à l’aide de l’API de service Web {#apply-a-policy-to-a-pdf-document-using-the-web-service-api}

Appliquez une stratégie à un document PDF à l’aide de l’API Document Security (service Web) :

1. Incluez des fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Assurez-vous d’utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un objet API Client de sécurité Document.

   * Créez un objet `RightsManagementServiceClient` en utilisant son constructeur par défaut.
   * Créez un objet `RightsManagementServiceClient.Endpoint.Address` en utilisant le constructeur `System.ServiceModel.EndpointAddress`. Transmettez une valeur de chaîne qui spécifie le WSDL au service Forms (par exemple, `http://localhost:8080/soap/services/RightsManagementService?WSDL`). Vous n&#39;avez pas besoin d&#39;utiliser l&#39;attribut `lc_version`. Cet attribut est utilisé lorsque vous créez une référence de service.)
   * Créez un objet `System.ServiceModel.BasicHttpBinding` en obtenant la valeur du champ `RightsManagementServiceClient.Endpoint.Binding`. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le champ `MessageEncoding` de l’objet `System.ServiceModel.BasicHttpBinding` sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en exécutant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * Affectez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Affectez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.


1. Récupérez un document PDF.

   * Créez un objet `BLOB` en utilisant son constructeur. L’objet `BLOB` permet de stocker un document PDF auquel une stratégie est appliquée.
   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du fichier du document PDF et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `System.IO.FileStream`. Déterminez la taille du tableau d’octets en obtenant la propriété `System.IO.FileStream` de l’objet `Length`.
   * Renseignez le tableau d’octets avec les données de flux en appelant la méthode `System.IO.FileStream` de l’objet `Read`. Passez le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’objet `BLOB` en attribuant son champ `MTOM` au contenu du tableau d’octets.

1. Appliquez une stratégie existante au document PDF.

   Appliquez une stratégie au document PDF en appelant la méthode `RightsManagementServiceClient` de l’objet `protectDocument` et en transmettant les valeurs suivantes :

   * Objet `BLOB` contenant le document PDF auquel la stratégie est appliquée.
   * Valeur de chaîne qui spécifie le nom du document.
   * Valeur de chaîne qui spécifie le nom du jeu de stratégies auquel appartient la stratégie. Vous pouvez spécifier une valeur `null` qui se traduit par l&#39;utilisation du jeu de stratégies `MyPolicies`.
   * Valeur de chaîne qui spécifie le nom de la stratégie.
   * Valeur de chaîne qui représente le nom du domaine du gestionnaire d’utilisateurs de l’utilisateur qui est l’éditeur du document. Cette valeur de paramètre est facultative et peut être nulle (si ce paramètre est nul, la valeur de paramètre suivante doit être `null`).
   * Valeur de chaîne qui représente le nom canonique de l’utilisateur du gestionnaire d’utilisateurs qui est l’éditeur du document. Cette valeur de paramètre est facultative et peut être nulle (si ce paramètre est nul, la valeur de paramètre précédente doit être `null`).
   * Valeur `RMLocale` qui spécifie la valeur du paramètre régional (par exemple, `RMLocale.en`).
   * Paramètre de sortie de chaîne utilisé pour stocker la valeur de l’identifiant de stratégie.
   * Paramètre de sortie de chaîne utilisé pour stocker la valeur d’identificateur protégée par une stratégie.
   * Paramètre de sortie de chaîne utilisé pour stocker le type MIME (par exemple, `application/pdf`).

   La méthode `protectDocument` renvoie un objet `BLOB` contenant le document PDF protégé par une stratégie.

1. Enregistrez le document PDF.

   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du fichier du document PDF protégé par une stratégie.
   * Créez un tableau d’octets qui stocke le contenu des données de l’objet `BLOB` renvoyé par la méthode `protectDocument`. Renseignez le tableau d’octets en obtenant la valeur du membre de données `MTOM` de l’objet `BLOB`.
   * Créez un objet `System.IO.BinaryWriter` en appelant son constructeur et en transmettant l&#39;objet `System.IO.FileStream`.
   * Ecrivez le contenu du tableau d’octets dans un fichier PDF en appelant la méthode `System.IO.BinaryWriter` de l’objet `Write` et en transmettant le tableau d’octets.

**Exemples de code**

Pour obtenir des exemples de code à l’aide du service Document Security, reportez-vous aux Débuts rapides suivants :

* &quot;Début rapide (MTOM) : Application d’une stratégie à un document PDF à l’aide de l’API du service Web&quot;
* &quot;Quick Début (SwaRef) : Application d’une stratégie à un document PDF à l’aide de l’API du service Web&quot;

## Suppression de stratégies des Documents PDF {#removing-policies-from-pdf-documents}

Vous pouvez supprimer une stratégie d’un document protégé par une stratégie afin de supprimer la sécurité du document. Autrement dit, si vous ne voulez plus que le document soit protégé par une politique. Si vous souhaitez mettre à jour un document protégé par une stratégie à l’aide d’une nouvelle stratégie, il est plus efficace de changer de stratégie au lieu de la supprimer et d’ajouter la stratégie mise à jour.

>[!NOTE]
>
>Pour plus d&#39;informations sur le service Document Security, consultez le [Guide de référence des services pour AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary_of_steps-4}

Pour supprimer une stratégie d’un document PDF protégé par une stratégie, procédez comme suit :

1. Inclure les fichiers de projet
1. Créez un objet API Client de sécurité Document.
1. Récupérez un document PDF protégé par une stratégie.
1. Supprimez la stratégie du document PDF.
1. Enregistrez le document PDF non sécurisé.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

**Création d’un objet API Client de sécurité Document**

Avant de pouvoir exécuter par programmation une opération du service Document Security, créez un objet client du service Document Security.

**Récupération d’un document PDF protégé par une stratégie**

Vous pouvez récupérer un document PDF protégé par une stratégie afin de supprimer une stratégie. Si vous tentez de supprimer une stratégie d’un document PDF qui n’est pas protégé par une stratégie, vous provoquerez une exception.

**Supprimer la stratégie du document PDF**

Vous pouvez supprimer une stratégie d’un document PDF protégé par une stratégie, à condition qu’un administrateur soit spécifié dans les paramètres de connexion. Si ce n’est pas le cas, la stratégie utilisée pour sécuriser un document doit contenir l’autorisation `SWITCH_POLICY` afin de supprimer une stratégie d’un document PDF. En outre, l’utilisateur spécifié dans les paramètres de connexion AEM Forms doit également disposer de cette autorisation. Dans le cas contraire, une exception est générée.

**Enregistrer le document PDF non sécurisé**

Une fois que le service Document Security a supprimé une stratégie d’un document PDF, vous pouvez enregistrer le document PDF non sécurisé en tant que fichier PDF.

**Voir également**

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Application de stratégies à des Documents PDF](protecting-documents-policies.md#applying-policies-to-pdf-documents)

### Supprimer une stratégie d’un document PDF à l’aide de l’API Java {#remove-a-policy-from-a-pdf-document-using-the-java-api}

Supprimez une stratégie d’un document PDF protégé par une stratégie à l’aide de l’API Document Security (Java) :

1. Incluez des fichiers de projet.

   Incluez des fichiers JAR client, tels que adobe-rightsmanagement-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un objet API Client de sécurité Document.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `DocumentSecurityClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`. 

1. Récupérez un document PDF protégé par une stratégie.

   * Créez un objet `java.io.FileInputStream` qui représente le document PDF protégé par une stratégie en utilisant son constructeur et en transmettant une valeur de chaîne qui spécifie l’emplacement du document PDF.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Supprimez la stratégie du document PDF.

   * Créez un objet `DocumentManager` en appelant la méthode `DocumentSecurityClient` de l&#39;objet `getDocumentManager`.
   * Supprimez une stratégie du document PDF en appelant la méthode `DocumentManager` de l’objet `removeSecurity` et en transmettant l’objet `com.adobe.idp.Document` contenant le document PDF protégé par une stratégie. Cette méthode renvoie un objet `com.adobe.idp.Document` contenant un document PDF non sécurisé.

1. Enregistrez le document PDF non sécurisé.

   * Créez un objet `java.io.File` et assurez-vous que l’extension de fichier est PDF.
   * Appelez la méthode `Document` de l&#39;objet `copyToFile` pour copier le contenu de l&#39;objet `Document` dans le fichier (veillez à utiliser l&#39;objet `Document` renvoyé par la méthode `removeSecurity`).

**Exemples de code**

Pour obtenir des exemples de code à l’aide du service Document Security, reportez-vous aux Débuts rapides suivants :

* &quot;Début rapide (mode SOAP) : Suppression d’une stratégie d’un document PDF à l’aide de l’API Java&quot;

### Supprimer une stratégie à l’aide de l’API de service Web {#remove-a-policy-using-the-web-service-api}

Supprimez une stratégie d’un document PDF protégé par une stratégie à l’aide de l’API Document Security (service Web) :

1. Incluez des fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Assurez-vous d’utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un objet API Client de sécurité Document.

   * Créez un objet `DocumentSecurityServiceClient` en utilisant son constructeur par défaut.
   * Créez un objet `DocumentSecurityServiceClient.Endpoint.Address` en utilisant le constructeur `System.ServiceModel.EndpointAddress`. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/RightsManagementService?WSDL`). Vous n&#39;avez pas besoin d&#39;utiliser l&#39;attribut `lc_version`. Cet attribut est utilisé lorsque vous créez une référence de service.)
   * Créez un objet `System.ServiceModel.BasicHttpBinding` en obtenant la valeur du champ `DocumentSecurityServiceClient.Endpoint.Binding`. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le champ `MessageEncoding` de l’objet `System.ServiceModel.BasicHttpBinding` sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en exécutant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * Affectez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Affectez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.


1. Récupérez un document PDF protégé par une stratégie.

   * Créez un objet `BLOB` en utilisant son constructeur. L’objet `BLOB` permet de stocker le document PDF protégé par une stratégie à partir duquel la stratégie est supprimée.
   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du fichier du document PDF et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `System.IO.FileStream`. Vous pouvez déterminer la taille du tableau d’octets en obtenant la propriété `System.IO.FileStream` de l’objet `Length`.
   * Renseignez le tableau d’octets avec les données de flux en appelant la méthode `System.IO.FileStream` de l’objet `Read` et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’objet `BLOB` en attribuant son champ `MTOM` au contenu du tableau d’octets.

1. Supprimez la stratégie du document PDF.

   Supprimez la stratégie du document PDF en appelant la méthode `DocumentSecurityServiceClient` de l’objet `removePolicySecurity` et en transmettant l’objet `BLOB` contenant le document PDF protégé par une stratégie. Cette méthode renvoie un objet `BLOB` contenant un document PDF non sécurisé.

1. Enregistrez le document PDF non sécurisé.

   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du fichier du document PDF non sécurisé.
   * Créez un tableau d’octets qui stocke le contenu des données de l’objet `BLOB` renvoyé par la méthode `removePolicySecurity`. Renseignez le tableau d’octets en obtenant la valeur du champ `BLOB` de l’objet `MTOM`.
   * Créez un objet `System.IO.BinaryWriter` en appelant son constructeur et en transmettant l&#39;objet `System.IO.FileStream`.

**Exemples de code**

Pour obtenir des exemples de code à l’aide du service Document Security, reportez-vous aux Débuts rapides suivants :

* &quot;Début rapide (MTOM) : Suppression d’une stratégie d’un document PDF à l’aide de l’API du service Web&quot;
* &quot;Quick Début (SwaRef) : Suppression d’une stratégie d’un document PDF à l’aide de l’API du service Web&quot;

**Voir également**

[Appel de AEM Forms à l’aide de MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Appel de AEM Forms à l’aide de SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Révocation de l&#39;accès aux Documents {#revoking-access-to-documents}

Vous pouvez révoquer l’accès à un document PDF protégé par une stratégie, de sorte que toutes les copies du document soient inaccessibles aux utilisateurs. Lorsqu’un utilisateur tente d’ouvrir un document PDF révoqué, il est redirigé vers une URL spécifiée où un document modifié peut être affiché. L’URL vers laquelle l’utilisateur est redirigé doit être spécifiée par programmation. Lorsque vous révoquez l’accès à un document, la modification prend effet lorsque l’utilisateur se synchronise avec le service Document Security en ouvrant le document protégé par une stratégie en ligne.

La possibilité de révoquer l’accès à un document offre une sécurité supplémentaire. Supposons, par exemple, qu’une version plus récente d’un document soit disponible et que vous ne souhaitiez plus que quiconque consulte la version obsolète. Dans ce cas, l&#39;accès à l&#39;ancien document peut être révoqué et personne ne peut vue le document à moins que l&#39;accès ne soit rétabli.

>[!NOTE]
>
>Pour plus d&#39;informations sur le service Document Security, consultez le [Guide de référence des services pour AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary_of_steps-5}

Pour révoquer un document protégé par une stratégie, procédez comme suit :

1. Incluez des fichiers de projet.
1. Créez un objet API Client de sécurité Document.
1. Récupérez un document PDF protégé par une stratégie.
1. Révoquez le document protégé par une stratégie.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

**Création d’un objet API Client de sécurité Document**

Avant de pouvoir exécuter par programmation une opération du service Document Security, vous devez créer un objet client du service Document Security.

**Récupération d’un document PDF protégé par une stratégie**

Vous devez récupérer un document PDF protégé par une stratégie pour le révoquer. Vous ne pouvez pas révoquer un document qui a déjà été révoqué ou qui n’est pas un document protégé par une stratégie.

Si vous connaissez la valeur d’identifiant de licence du document protégé par une stratégie, il n’est pas nécessaire de récupérer le document PDF protégé par une stratégie. Cependant, dans la plupart des cas, vous devrez récupérer le document PDF pour obtenir la valeur d’identifiant de licence.

**Révoquer le document protégé par une stratégie**

Pour révoquer un document protégé par une stratégie, spécifiez l’identifiant de licence du document protégé par une stratégie. En outre, vous pouvez spécifier l’URL d’un document que l’utilisateur peut vue lorsqu’il tente d’ouvrir le document révoqué. En d&#39;autres termes, supposons qu&#39;un document obsolète soit révoqué. Lorsqu’un utilisateur tente d’ouvrir le document révoqué, un document mis à jour s’affiche au lieu du document révoqué.

>[!NOTE]
>
>Si vous tentez de révoquer un document déjà révoqué, une exception est levée.

**Voir également**

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Application de stratégies à des Documents PDF](protecting-documents-policies.md#applying-policies-to-pdf-documents)

[Rétablissement de l&#39;accès aux Documents révoqués](protecting-documents-policies.md#reinstating-access-to-revoked-documents)

### Révoquer l’accès aux documents à l’aide de l’API Java {#revoke-access-to-documents-using-the-java-api}

Révoquez l’accès à un document PDF protégé par une stratégie à l’aide de l’API Document Security (Java) :

1. Inclure les fichiers de projet

   Incluez des fichiers JAR client, tels que adobe-rightsmanagement-client.jar, dans le chemin de classe de votre projet Java.

1. Création d’un objet API Client de sécurité Document

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `DocumentSecurityClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`. 

1. Récupération d’un document PDF protégé par une stratégie

   * Créez un objet `java.io.FileInputStream` représentant le document PDF protégé par une stratégie en utilisant son constructeur et en transmettant une valeur de chaîne qui spécifie l’emplacement du document PDF.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Révoquer le document protégé par une stratégie

   * Créez un objet `DocumentManager` en appelant la méthode `DocumentSecurityClient` de l&#39;objet `getDocumentManager`.
   * Récupérez la valeur d&#39;identifiant de licence du document protégé par une stratégie en appelant la méthode `DocumentManager` de l&#39;objet `getLicenseId`. Transmettez l&#39;objet `com.adobe.idp.Document` qui représente le document protégé par une stratégie. Cette méthode renvoie une valeur de chaîne qui représente la valeur de l’identifiant de licence.
   * Créez un objet `LicenseManager` en appelant la méthode `DocumentSecurityClient` de l&#39;objet `getLicenseManager`.
   * Révoquez le document protégé par une stratégie en appelant la méthode `LicenseManager` de l’objet `revokeLicense` et en transmettant les valeurs suivantes :

      * Valeur de chaîne qui spécifie la valeur d’identifiant de licence du document protégé par une stratégie (spécifiez la valeur de retour de la méthode `DocumentManager` de l’objet `getLicenseId`).
      * Membre de données statiques de l&#39;interface `License` qui spécifie la raison de la révocation du document. Par exemple, vous pouvez spécifier `License.DOCUMENT_REVISED`.
      * Valeur `java.net.URL` qui spécifie l&#39;emplacement où se trouve un document révisé. Si vous ne souhaitez pas rediriger un utilisateur vers une autre URL, vous pouvez transmettre `null`.

**Exemples de code**

Pour obtenir des exemples de code à l’aide du service Document Security, reportez-vous aux Débuts rapides suivants :

* &quot;Début rapide (mode SOAP) : Révocation d’un document à l’aide de l’API Java&quot;

### Révoquer l’accès aux documents à l’aide de l’API de service Web {#revoke-access-to-documents-using-the-web-service-api}

Révoquez l’accès à un document PDF protégé par une stratégie à l’aide de l’API Document Security (service Web) :

1. Inclure les fichiers de projet

   Créez un projet Microsoft .NET qui utilise MTOM. Assurez-vous d’utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Création d’un objet API Client de sécurité Document

   * Créez un objet `DocumentSecurityServiceClient` en utilisant son constructeur par défaut.
   * Créez un objet `DocumentSecurityServiceClient.Endpoint.Address` en utilisant le constructeur `System.ServiceModel.EndpointAddress`. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/RightsManagementService?WSDL`). Vous n&#39;avez pas besoin d&#39;utiliser l&#39;attribut `lc_version`. Cet attribut est utilisé lorsque vous créez une référence de service.)
   * Créez un objet `System.ServiceModel.BasicHttpBinding` en obtenant la valeur du champ `DocumentSecurityServiceClient.Endpoint.Binding`. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le champ `MessageEncoding` de l’objet `System.ServiceModel.BasicHttpBinding` sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en exécutant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * Affectez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Affectez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.


1. Récupération d’un document PDF protégé par une stratégie

   * Créez un objet `BLOB` en utilisant son constructeur. L’objet `BLOB` est utilisé pour stocker un document PDF protégé par une stratégie qui est révoqué.
   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du fichier du document PDF protégé par une stratégie à révoquer et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `System.IO.FileStream`. Vous pouvez déterminer la taille du tableau d’octets en obtenant la propriété `System.IO.FileStream` de l’objet `Length`.
   * Renseignez le tableau d’octets avec les données de flux en appelant la méthode `System.IO.FileStream` de l’objet `Read` et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’objet `BLOB` en attribuant son champ `MTOM` au contenu du tableau d’octets.

1. Révoquer le document protégé par une stratégie

   * Récupérez la valeur d&#39;identifiant de licence du document protégé par une stratégie en appelant la méthode `DocumentSecurityServiceClient` de l&#39;objet `getLicenseID` et en transmettant l&#39;objet `BLOB` qui représente le document protégé par une stratégie. Cette méthode renvoie une valeur de chaîne qui représente l’identifiant de licence.
   * Révoquez le document protégé par une stratégie en appelant la méthode `DocumentSecurityServiceClient` de l’objet `revokeLicense` et en transmettant les valeurs suivantes :

      * Valeur de chaîne qui spécifie la valeur d’identifiant de licence du document protégé par une stratégie (spécifiez la valeur de retour de la méthode `DocumentSecurityServiceService` de l’objet `getLicenseId`).
      * Membre de données statiques de l&#39;énumération `Reason` qui spécifie la raison de la révocation du document. Par exemple, vous pouvez spécifier `Reason.DOCUMENT_REVISED`.
      * Valeur `string` qui spécifie l’emplacement de l’URL vers lequel se trouve un document révisé. Si vous ne souhaitez pas rediriger un utilisateur vers une autre URL, vous pouvez transmettre `null`.

**Exemples de code**

Pour obtenir des exemples de code à l’aide du service Document Security, reportez-vous aux Débuts rapides suivants :

* &quot;Début rapide (MTOM) : Révocation d’un document à l’aide de l’API du service Web&quot;
* &quot;Quick Début (SwaRef) : Révocation d’un document à l’aide de l’API du service Web&quot;

**Voir également**

[Suppression de stratégies des Documents Word](protecting-documents-policies.md#removing-policies-from-word-documents)

[Appel de AEM Forms à l’aide de MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Appel de AEM Forms à l’aide de SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Rétablissement de l&#39;accès aux Documents révoqués {#reinstating-access-to-revoked-documents}

Vous pouvez rétablir l’accès à un document PDF révoqué, de sorte que toutes les copies du document révoqué soient accessibles aux utilisateurs. Lorsqu’un utilisateur ouvre un document restauré qui a été révoqué, il peut vue le document.

>[!NOTE]
>
>Pour plus d&#39;informations sur le service Document Security, consultez le [Guide de référence des services pour AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary_of_steps-6}

Pour rétablir l’accès à un document PDF révoqué, procédez comme suit :

1. Incluez des fichiers de projet.
1. Créez un objet API Client de sécurité Document.
1. Récupérez l’identifiant de licence du document PDF révoqué.
1. Rétablit l’accès au document PDF révoqué.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

**Création d’un objet API Client de sécurité Document**

Avant de pouvoir exécuter par programmation une opération du service Document Security, vous devez créer un objet client du service Document Security. Si vous utilisez l’API Java, créez un objet `DocumentSecurityClient`. Si vous utilisez l&#39;API du service Web Document Security, créez un objet `DocumentSecurityServiceService`.

**Récupérer l’identifiant de licence du document PDF révoqué**

Pour rétablir un document PDF révoqué, vous devez récupérer l’identifiant de licence du document PDF révoqué. Après avoir obtenu la valeur d’identifiant de licence, vous pouvez rétablir un document révoqué. Si vous tentez de rétablir un document qui n’est pas révoqué, vous provoquerez une exception.

**Rétablissement de l’accès au document PDF révoqué**

Pour rétablir l’accès à un document PDF révoqué, vous devez indiquer l’identifiant de licence du document révoqué. Si vous tentez de rétablir l’accès à un document PDF qui n’est pas révoqué, vous provoquerez une exception.

**Voir également**

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Application de stratégies à des Documents PDF](protecting-documents-policies.md#applying-policies-to-pdf-documents)

[Révocation de l’accès aux Documents](protecting-documents-policies.md#revoking-access-to-documents)

### Rétablissement de l’accès aux documents révoqués à l’aide de l’API Java {#reinstate-access-to-revoked-documents-using-the-java-api}

Rétablissement de l’accès à un document révoqué à l’aide de l’API Document Security (Java) :

1. Incluez des fichiers de projet.

   Incluez des fichiers JAR client, tels que adobe-rightsmanagement-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un objet API Client de sécurité Document.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `DocumentSecurityClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`. 

1. Récupérez l’identifiant de licence du document PDF révoqué.

   * Créez un objet `java.io.FileInputStream` qui représente le document PDF révoqué en utilisant son constructeur et en transmettant une valeur de chaîne qui spécifie l’emplacement du document PDF.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 
   * Créez un objet `DocumentManager` en appelant la méthode `DocumentSecurityClient` de l&#39;objet `getDocumentManager`.
   * Récupérez la valeur d&#39;identifiant de licence du document révoqué en appelant la méthode `DocumentManager` de l&#39;objet `getLicenseId` et en transmettant l&#39;objet `com.adobe.idp.Document` qui représente le document révoqué. Cette méthode renvoie une valeur de chaîne qui représente l’identifiant de licence.

1. Rétablit l’accès au document PDF révoqué.

   * Créez un objet `LicenseManager` en appelant la méthode `DocumentSecurityClient` de l&#39;objet `getLicenseManager`.
   * Rétablissez l’accès au document PDF révoqué en appelant la méthode `LicenseManager` de l’objet `unrevokeLicense` et en transmettant la valeur d’identifiant de licence du document révoqué.

**Exemples de code**

Pour obtenir des exemples de code à l’aide du service Document Security, reportez-vous aux Débuts rapides suivants :

* &quot;Début rapide (mode SOAP) : Rétablissement de l’accès à un document révoqué à l’aide de l’API du service Web&quot;

### Rétablissement de l’accès aux documents révoqués à l’aide de l’API de service Web {#reinstate-access-to-revoked-documents-using-the-web-service-api}

Rétablissement de l’accès à un document révoqué à l’aide de l’API Document Security (service Web) :

1. Incluez des fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Assurez-vous d’utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un objet API Client de sécurité Document.

   * Créez un objet `DocumentSecurityServiceClient` en utilisant son constructeur par défaut.
   * Créez un objet `DocumentSecurityServiceClient.Endpoint.Address` en utilisant le constructeur `System.ServiceModel.EndpointAddress`. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/RightsManagementService?WSDL`). Vous n&#39;avez pas besoin d&#39;utiliser l&#39;attribut `lc_version`. Cet attribut est utilisé lorsque vous créez une référence de service.)
   * Créez un objet `System.ServiceModel.BasicHttpBinding` en obtenant la valeur du champ `DocumentSecurityServiceClient.Endpoint.Binding`. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le champ `MessageEncoding` de l’objet `System.ServiceModel.BasicHttpBinding` sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en exécutant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * Affectez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Affectez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.


1. Récupérez l’identifiant de licence du document PDF révoqué.

   * Créez un objet `BLOB` en utilisant son constructeur. L’objet `BLOB` est utilisé pour stocker un document PDF révoqué auquel l’accès est rétabli.
   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du fichier du document PDF révoqué et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `System.IO.FileStream`. Vous pouvez déterminer la taille du tableau d’octets en obtenant la propriété `System.IO.FileStream` de l’objet `Length`.
   * Renseignez le tableau d’octets avec les données de flux en appelant la méthode `System.IO.FileStream` de l’objet `Read` et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’objet `BLOB` en attribuant son champ `MTOM` au contenu du tableau d’octets.

1. Rétablit l’accès au document PDF révoqué.

   * Récupérez la valeur d&#39;identifiant de licence du document révoqué en appelant la méthode `DocumentSecurityServiceClient` de l&#39;objet `getLicenseID` et en transmettant l&#39;objet `BLOB` qui représente le document révoqué. Cette méthode renvoie une valeur de chaîne qui représente l’identifiant de licence.
   * Rétablissez l’accès au document PDF révoqué en appelant la méthode `DocumentSecurityServiceClient` de l’objet `unrevokeLicense` et en transmettant une valeur de chaîne qui spécifie la valeur d’identifiant de licence du document PDF révoqué (transmettez la valeur de retour de la méthode `DocumentSecurityServiceClient` de l’objet `getLicenseId`).

**Exemples de code**

Pour obtenir des exemples de code à l’aide du service Document Security, reportez-vous aux Débuts rapides suivants :

* &quot;Début rapide (MTOM) : Rétablissement de l’accès à un document révoqué à l’aide de l’API du service Web&quot;
* &quot;Quick Début (SwaRef) : Rétablissement de l’accès à un document révoqué à l’aide de l’API du service Web&quot;

**Voir également**

[Appel de AEM Forms à l’aide de MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Appel de AEM Forms à l’aide de SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Inspection des Documents PDF protégés par une stratégie {#inspecting-policy-protected-pdf-documents}

Vous pouvez utiliser l’API Document Security Service (Java et service Web) pour inspecter les documents PDF protégés par une stratégie. L’inspection des documents PDF protégés par une stratégie renvoie des informations sur le document PDF protégé par une stratégie. Vous pouvez, par exemple, déterminer la stratégie utilisée pour sécuriser le document et la date à laquelle le document a été sécurisé.

Vous ne pouvez pas effectuer cette tâche si votre version de LiveCycle est 8.x ou une version antérieure. La prise en charge de l’inspection des documents protégés par une stratégie est ajoutée à AEM Forms. Si vous tentez d’inspecter un document protégé par une stratégie à l’aide de LiveCycle 8.x (ou version antérieure), une exception est générée.

>[!NOTE]
>
>Pour plus d&#39;informations sur le service Document Security, consultez le [Guide de référence des services pour AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary_of_steps-7}

Pour inspecter un document PDF protégé par une stratégie, procédez comme suit :

1. Incluez des fichiers de projet.
1. Créez un objet API Client de sécurité Document.
1. Récupérez un document protégé par une stratégie à inspecter.
1. Obtenez des informations sur le document protégé par une stratégie.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

**Création d’un objet API Client de sécurité Document**

Avant de pouvoir exécuter par programmation une opération du service Document Security, créez un objet client du service Document Security. Si vous utilisez l’API Java, créez un objet `RightsManagementClient`. Si vous utilisez l&#39;API du service Web Document Security, créez un objet `RightsManagementServiceService`.

**Récupération d’un document protégé par une stratégie pour l’inspection**

Pour inspecter un document protégé par une stratégie, récupérez-le. Si vous tentez d’inspecter un document non sécurisé avec une stratégie ou révoqué, une exception est générée.

**Inspect, le document**

Après avoir récupéré un document protégé par une stratégie, vous pouvez l’inspecter.

**Obtention d’informations sur le document protégé par une stratégie**

Après avoir examiné un document PDF protégé par une stratégie, vous pouvez obtenir des informations à son sujet. Par exemple, vous pouvez déterminer la stratégie utilisée pour sécuriser le document.

Si vous sécurisez un document avec une stratégie qui appartient à Mes stratégies, puis que vous appelez `RMInspectResult.getPolicysetName` ou `RMInspectResult.getPolicysetId`, la valeur null est renvoyée.

Si le document est sécurisé à l’aide d’une stratégie contenue dans un jeu de stratégies (autre que Mes stratégies), `RMInspectResult.getPolicysetName` et `RMInspectResult.getPolicysetId` renvoient des chaînes valides.

**Voir également**

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Documents PDF protégés par une stratégie Inspect à l’aide de l’API Java {#inspect-policy-protected-pdf-documents-using-the-java-api}

Inspect un document PDF protégé par une stratégie à l’aide de l’API Document Security Service (Java) :

1. Incluez des fichiers de projet.

   Incluez des fichiers JAR client, tels que adobe-rightsmanagement-client.jar, dans le chemin de classe de votre projet Java. Pour plus d’informations sur l’emplacement de ces fichiers, voir [Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

1. Créez un objet API Client de sécurité Document.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion. (Voir [Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
   * Créez un objet `RightsManagementClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`. 

1. Récupérez un document protégé par une stratégie à inspecter.

   * Créez un objet `java.io.FileInputStream` qui représente le document PDF protégé par une stratégie en utilisant son constructeur. Transmettez une valeur de chaîne qui spécifie l’emplacement du document PDF.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Inspect le document.

   * Créez un objet `DocumentManager` en appelant la méthode `RightsManagementClient` de l&#39;objet `getDocumentManager`.
   * Inspect le document protégé par une stratégie en appelant la méthode `LicenseManager` de l’objet `inspectDocument`. Transmettez l’objet `com.adobe.idp.Document` contenant le document PDF protégé par une stratégie. Cette méthode renvoie un objet `RMInspectResult` contenant des informations sur le document protégé par une stratégie.

1. Obtenez des informations sur le document protégé par une stratégie.

   Pour obtenir des informations sur le document protégé par une stratégie, appelez la méthode appropriée qui appartient à l&#39;objet `RMInspectResult`. Par exemple, pour récupérer le nom de la stratégie, appelez la méthode `RMInspectResult` de l’objet `getPolicyName`.

**Exemples de code**

Pour obtenir des exemples de code à l’aide du service Document Security, reportez-vous aux Débuts rapides suivants :

* &quot;Début rapide (mode SOAP) : Contrôle des documents PDF protégés par une stratégie à l’aide de l’API Java&quot;

### Documents PDF protégés par une stratégie Inspect à l’aide de l’API du service Web {#inspect-policy-protected-pdf-documents-using-the-web-service-api}

Inspect un document PDF protégé par une stratégie à l’aide de l’API Document Security Service (service Web) :

1. Incluez des fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Assurez-vous d’utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un objet API Client de sécurité Document.

   * Créez un objet `RightsManagementServiceClient` en utilisant son constructeur par défaut.
   * Créez un objet `RightsManagementServiceClient.Endpoint.Address` en utilisant le constructeur `System.ServiceModel.EndpointAddress`. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/RightsManagementService?WSDL`). Vous n&#39;avez pas besoin d&#39;utiliser l&#39;attribut `lc_version`. Cet attribut est utilisé lorsque vous créez une référence de service.)
   * Créez un objet `System.ServiceModel.BasicHttpBinding` en obtenant la valeur du champ `RightsManagementServiceClient.Endpoint.Binding`. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le champ `MessageEncoding` de l’objet `System.ServiceModel.BasicHttpBinding` sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en exécutant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * Affectez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Affectez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.


1. Récupérez un document protégé par une stratégie à inspecter.

   * Créez un objet `BLOB` en utilisant son constructeur. L&#39;objet `BLOB` est utilisé pour stocker un document PDF à inspecter.
   * Créez un objet `System.IO.FileStream` en appelant son constructeur. Transmettez une valeur de chaîne qui représente l’emplacement du fichier du document PDF et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `System.IO.FileStream`. Vous pouvez déterminer la taille du tableau d’octets en obtenant la propriété `System.IO.FileStream` de l’objet `Length`.
   * Renseignez le tableau d’octets avec les données de flux en appelant la méthode `System.IO.FileStream` de l’objet `Read`. Passez le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’objet `BLOB` en attribuant son champ `MTOM` au contenu du tableau d’octets.

1. Inspect le document.

   Inspect le document protégé par une stratégie en appelant la méthode `RightsManagementServiceClient` de l’objet `inspectDocument`. Transmettez l’objet `BLOB` contenant le document PDF protégé par une stratégie. Cette méthode renvoie un objet `RMInspectResult` contenant des informations sur le document protégé par une stratégie.

1. Obtenez des informations sur le document protégé par une stratégie.

   Pour obtenir des informations sur le document protégé par une stratégie, obtenez la valeur du champ approprié qui appartient à l&#39;objet `RMInspectResult`. Par exemple, pour récupérer le nom de la stratégie, obtenez la valeur du champ `RMInspectResult` de l’objet `policyName`.

**Exemples de code**

Pour obtenir des exemples de code à l’aide du service Document Security, reportez-vous aux Débuts rapides suivants :

* &quot;Début rapide (MTOM) : Contrôle des documents PDF protégés par une stratégie à l’aide de l’API du service Web&quot;
* &quot;Quick Début (SwaRef) : Contrôle des documents PDF protégés par une stratégie à l’aide de l’API du service Web&quot;

**Voir également**

[Appel de AEM Forms à l’aide de MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Appel de AEM Forms à l’aide de SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Création de filigranes {#creating-watermarks}

Les filigranes permettent d&#39;assurer la sécurité d&#39;un document en identifiant de manière unique le document et en contrôlant la violation du droit d&#39;auteur. Par exemple, vous pouvez créer et placer un filigrane qui indique Confidentiel sur toutes les pages d’un document. Une fois un filigrane créé, vous pouvez l’inclure dans une stratégie. En d’autres termes, vous pouvez définir l’attribut de filigrane de la stratégie avec le nouveau filigrane créé. Une fois qu’une stratégie contenant un filigrane est appliquée à un document, le filigrane apparaît dans le document protégé par une stratégie.

>[!NOTE]
>
>Seuls les utilisateurs disposant de droits d’administrateur Document Security peuvent créer des filigranes. En d’autres termes, vous devez spécifier un tel utilisateur lors de la définition des paramètres de connexion requis pour créer un objet client du service Document Security.

>[!NOTE]
>
>Pour plus d&#39;informations sur le service Document Security, consultez le [Guide de référence des services pour AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary_of_steps-8}

Pour créer un filigrane, procédez comme suit :

1. Incluez des fichiers de projet.
1. Créez un objet API Client de sécurité Document.
1. Définissez les attributs des filigranes.
1. Enregistrez le filigrane auprès du service Document Security.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

**Création d’un objet API Client de sécurité Document**

Avant de pouvoir exécuter par programmation une opération du service Document Security, vous devez créer un objet client du service Document Security. Si vous utilisez l’API Java, créez un objet `RightsManagementClient`. Si vous utilisez l&#39;API du service Web Document Security, créez un objet `RightsManagementServiceService`.

**Définition des attributs des filigranes**

Pour créer un filigrane, vous devez définir des attributs de filigrane. L&#39;attribut name doit toujours être défini. Outre l’attribut name, vous devez définir au moins l’un des attributs suivants :

* Texte personnalisé
* DateInclus
* UserIdIncluded
* UserNameIncluded

Le tableau suivant liste les paires clé/valeur requises lors de la création d’un filigrane à l’aide des services Web.

<table>
 <thead>
  <tr>
   <th><p>Nom de la clé</p></th>
   <th><p>Description</p></th>
   <th><p>Valeur</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p><code>WaterBackCmd:IS_USERNAME_ENABLED</code></p></td>
   <td><p>Indique si le nom d’utilisateur de l’utilisateur qui ouvre le document fait partie du filigrane.</p></td>
   <td><p>True ou false</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:IS_USERID_ENABLED</code></p></td>
   <td><p>Indique si l’identification de l’utilisateur ouvrant le document fait partie du filigrane.</p></td>
   <td><p>True ou false</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:IS_CURRENTDATE_ENABLED</code></p></td>
   <td><p>Indique si la date actuelle fait partie du filigrane.</p></td>
   <td><p>True ou false</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:IS_CUSTOMTEXT_ENABLED</code></p></td>
   <td><p>Si cette valeur est true, la valeur du texte personnalisé doit être spécifiée à l’aide de <code>WaterBackCmd:SRCTEXT</code>.</p></td>
   <td><p>True ou false</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:OPACITY</code></p></td>
   <td><p>Indique l’opacité du filigrane. La valeur par défaut est 0,5 si elle n’est pas spécifiée.</p></td>
   <td><p>Valeur comprise entre 0.0 et 1.0.</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:ROTATION</code></p></td>
   <td><p>Indique la rotation du filigrane. La valeur par défaut est 0 degré.</p></td>
   <td><p>Valeur comprise entre 0 et 359.</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:SCALE</code></p></td>
   <td><p>Si cette valeur est spécifiée, <code>WaterBackCmd:IS_SIZE_ENABLED</code> doit être présent et la valeur doit être true. Si cet attribut n’est pas spécifié, le comportement par défaut est adapté à la page.</p></td>
   <td><p>Valeur supérieure à 0.0 et inférieure ou égale à 1.0.</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:HORIZ_ALIGN</code></p></td>
   <td><p>Indique l’alignement horizontal du filigrane. La valeur par défaut est center.</p></td>
   <td><p>gauche, centre ou droite</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:VERT_ALIGN</code></p></td>
   <td><p>Indique l’alignement vertical du filigrane. La valeur par défaut est center.</p></td>
   <td><p>haut, centre ou bas</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:IS_USE_BACKGROUND</code></p></td>
   <td><p>Indique si le filigrane est un arrière-plan. La valeur par défaut est false. </p></td>
   <td><p>True ou false</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:IS_SIZE_ENABLED</code></p></td>
   <td><p>True si une échelle personnalisée est spécifiée. Si cette valeur est vraie, SCALE doit également être spécifié. Si cette valeur est définie sur false, la valeur par défaut est ajustée à la page.</p></td>
   <td><p>True ou false</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:SRCTEXT</code></p></td>
   <td><p>Indique le texte personnalisé d’un filigrane. Si cette valeur est présente, <code>WaterBackCmd:IS_CUSTOMTEXT_ENABLED</code> doit également être présent et définie sur true.</p></td>
   <td><p>True ou false</p></td>
  </tr>
 </tbody>
</table>

L’un des attributs suivants doit être défini pour tous les filigranes :

* `WaterBackCmd:IS_USERNAME_ENABLED`
* `WaterBackCmd:IS_USERID_ENABLED`
* `WaterBackCmd:IS_CURRENTDATE_ENABLED`
* `WaterBackCmd:IS_CUSTOMTEXT_ENABLED`

Tous les autres attributs sont facultatifs.

**Enregistrement du filigrane**

Un nouveau filigrane doit être enregistré auprès du service Document Security avant de pouvoir être utilisé. Après avoir enregistré un filigrane, vous pouvez l’utiliser dans les stratégies.

**Voir également**

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Application de stratégies à des Documents PDF](protecting-documents-policies.md#applying-policies-to-pdf-documents)

### Création de filigranes à l’aide de l’API Java {#create-watermarks-using-the-java-api}

Créez un filigrane à l’aide de l’API Document Security (Java) :

1. Incluez des fichiers de projet.

   Incluez les fichiers JAR client, tels que `adobe-rightsmanagement-client.jar`, dans le chemin de classe de votre projet Java.

1. Créez un objet API Client de sécurité Document.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `RightsManagementClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`. 

1. Définition des attributs du filigrane

   * Créez un objet `Watermark` en appelant la méthode statique `InfomodelObjectFactory` de l&#39;objet `createWatermark`. Cette méthode renvoie un objet `Watermark`.
   * Définissez l’attribut name du filigrane en appelant la méthode `Watermark` de l’objet `setName` et en transmettant une valeur de chaîne qui spécifie le nom de la stratégie.
   * Définissez l’attribut d’arrière-plan du filigrane en appelant la méthode `Watermark` de l’objet `setBackground` et en transmettant `true`. En définissant cet attribut, le filigrane apparaît à l’arrière-plan du document.
   * Définissez l’attribut de texte personnalisé du filigrane en appelant la méthode `Watermark` de l’objet `setCustomText` et en transmettant une valeur de chaîne qui représente le texte du filigrane.
   * Définissez l’attribut d’opacité du filigrane en appelant la méthode `Watermark` de l’objet `setOpacity` et en transmettant un entier spécifiant le niveau d’opacité. La valeur 100 indique que le filigrane est complètement opaque et la valeur 0 indique que le filigrane est complètement transparent.

1. Enregistrez le filigrane.

   * Créez un objet `WatermarkManager` en appelant la méthode `RightsManagementClient` de l&#39;objet `getWatermarkManager`. Cette méthode renvoie un objet `WatermarkManager`.
   * Enregistrez le filigrane en appelant la méthode `WatermarkManager` de l&#39;objet `registerWatermark` et en transmettant l&#39;objet `Watermark` représentant le filigrane à enregistrer. Cette méthode renvoie une valeur de chaîne qui représente la valeur d’identification du filigrane.

**Exemples de code**

Pour obtenir des exemples de code à l’aide du service Document Security, reportez-vous aux Débuts rapides suivants :

* &quot;Début rapide (mode SOAP) : Création d’un filigrane à l’aide de l’API Java&quot;

### Création de filigranes à l’aide de l’API du service Web {#create-watermarks-using-the-web-service-api}

Créez un filigrane à l’aide de l’API Document Security (service Web) :

1. Créez un objet API Client de sécurité Document.

   Créez un projet Microsoft .NET qui utilise MTOM. Assurez-vous d’utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un objet API Client de sécurité Document.

   * Créez un objet `RightsManagementServiceClient` en utilisant son constructeur par défaut.
   * Créez un objet `RightsManagementServiceClient.Endpoint.Address` en utilisant le constructeur `System.ServiceModel.EndpointAddress`. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/RightsManagementService?WSDL`). Vous n&#39;avez pas besoin d&#39;utiliser l&#39;attribut `lc_version`. Cet attribut est utilisé lorsque vous créez une référence de service.)
   * Créez un objet `System.ServiceModel.BasicHttpBinding` en obtenant la valeur du champ `RightsManagementServiceClient.Endpoint.Binding`. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le champ `MessageEncoding` de l’objet `System.ServiceModel.BasicHttpBinding` sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en exécutant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * Affectez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Affectez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.


1. Définissez les attributs du filigrane.

   * Créez un objet `WatermarkSpec` en appelant le constructeur `WatermarkSpec`.
   * Définissez le nom du filigrane en attribuant une valeur de chaîne au membre de données `name` de l&#39;objet `WatermarkSpec`.
   * Définissez l’attribut `id` du filigrane en attribuant une valeur de chaîne au membre de données `WatermarkSpec` de l’objet `id`.
   * Pour chaque propriété de filigrane à définir, créez un objet `MyMapOf_xsd_string_To_xsd_anyType_Item` distinct.
   * Définissez la valeur de clé en attribuant une valeur au membre de données `key` de l’objet `MyMapOf_xsd_string_To_xsd_anyType_Item` (par exemple, `WaterBackCmd:OPACITY)`.
   * Définissez la valeur en attribuant une valeur au membre de données `value` de l’objet `MyMapOf_xsd_string_To_xsd_anyType_Item` (par exemple, `.25`).
   * Créez un objet `MyArrayOf_xsd_anyType`. Pour chaque objet `MyMapOf_xsd_string_To_xsd_anyType_Item`, appelez la méthode `MyArrayOf_xsd_anyType` de l&#39;objet `Add`. Transmettez l&#39;objet `MyMapOf_xsd_string_To_xsd_anyType_Item`.
   * Affectez l&#39;objet `MyArrayOf_xsd_anyType` au membre de données `WatermarkSpec` de l&#39;objet `values`.

1. Enregistrez le filigrane.

   Enregistrez le filigrane en appelant la méthode `RightsManagementServiceClient` de l&#39;objet `registerWatermark` et en transmettant l&#39;objet `WatermarkSpec` représentant le filigrane à enregistrer.

**Exemples de code**

Pour obtenir des exemples de code à l’aide du service Document Security, reportez-vous aux Débuts rapides suivants :

* &quot;Début rapide (MTOM) : Création d’un filigrane à l’aide de l’API du service Web&quot;
* &quot;Quick Début (SwaRef) : Création d’un filigrane à l’aide de l’API du service Web&quot;

**Voir également**

[Appel de AEM Forms à l’aide de MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Appel de AEM Forms à l’aide de SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Modification des filigranes {#modifying-watermarks}

Vous pouvez modifier un filigrane existant à l’aide de l’API Java Document Security ou de l’API de service Web. Pour apporter des modifications à un filigrane existant, récupérez-le, modifiez ses attributs, puis mettez-le à jour sur le serveur. Supposons, par exemple, que vous récupériez un filigrane et que vous modifiez son attribut d’opacité. Avant que la modification ne prenne effet, vous devez mettre à jour le filigrane.

Lorsque vous modifiez un filigrane, la modification a un impact sur les documents futurs auxquels le filigrane est appliqué. En d’autres termes, les documents PDF existants qui contiennent le filigrane ne sont pas affectés.

>[!NOTE]
>
>Seuls les utilisateurs disposant de droits d’administrateur Document Security peuvent modifier les filigranes. En d’autres termes, vous devez spécifier un tel utilisateur lors de la définition des paramètres de connexion requis pour créer un objet client du service Document Security.

>[!NOTE]
>
>Pour plus d&#39;informations sur le service Document Security, consultez le [Guide de référence des services pour AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary_of_steps-9}

Pour modifier un filigrane, procédez comme suit :

1. Incluez des fichiers de projet.
1. Créez un objet API Client de sécurité Document.
1. Récupérez le filigrane à modifier.
1. Définissez les attributs des filigranes.
1. Mettez à jour le filigrane.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

**Création d’un objet API Client de sécurité Document**

Avant de pouvoir exécuter par programmation une opération du service Document Security, vous devez créer un objet client du service Document Security. Si vous utilisez l’API Java, créez un objet `DocumentSecurityClient`. Si vous utilisez l&#39;API du service Web Document Security, créez un objet `DocumentSecurityServiceService`.

**Récupérer le filigrane à modifier**

Pour modifier un filigrane, vous devez récupérer un filigrane existant. Vous pouvez récupérer un filigrane en spécifiant son nom ou en spécifiant sa valeur d’identificateur.

**Définition des attributs des filigranes**

Pour modifier un filigrane existant, modifiez la valeur d’un ou de plusieurs attributs de filigrane. Lors de la mise à jour programmée d’un filigrane à l’aide d’un service Web, vous devez définir tous les attributs définis à l’origine, même si la valeur ne change pas. Supposons, par exemple, que les attributs de filigrane suivants soient définis : `WaterBackCmd:IS_USERID_ENABLED`, `WaterBackCmd:IS_CUSTOMTEXT_ENABLED`, `WaterBackCmd:OPACITY` et `WaterBackCmd:SRCTEXT`. Bien que le seul attribut à modifier soit `WaterBackCmd:OPACITY`, vous devez définir les autres valeurs.

>[!NOTE]
>
>Lorsque vous utilisez l’API Java pour modifier un filigrane, vous n’avez pas besoin de spécifier tous les attributs. Définissez l’attribut de filigrane à modifier.

>[!NOTE]
>
>Pour plus d’informations sur les noms d’attributs du filigrane, voir [Création de filigranes](protecting-documents-policies.md#creating-watermarks).

**Mise à jour du filigrane**

Après avoir modifié les attributs d’un filigrane, vous devez le mettre à jour.

**Voir également**

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Création de filigranes](protecting-documents-policies.md#creating-watermarks)

### Modification des filigranes à l’aide de l’API Java {#modify-watermarks-using-the-java-api}

Modifiez un filigrane à l’aide de l’API Document Security (Java) :

1. Incluez des fichiers de projet.

   Incluez des fichiers JAR client, tels que adobe-rightsmanagement-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un objet API Client de sécurité Document.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `DocumentSecurityClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`. 

1. Récupérez le filigrane à modifier.

   Créez un objet `WatermarkManager` en appelant la méthode `DocumentSecurityClient` de l&#39;objet `getWatermarkManager` et transmettez une valeur de chaîne qui spécifie le nom du filigrane. Cette méthode renvoie un objet `Watermark` qui représente le filigrane à modifier.

1. Définissez les attributs du filigrane.

   Définissez l’attribut d’opacité du filigrane en appelant la méthode `Watermark` de l’objet `setOpacity` et en transmettant un entier spécifiant le niveau d’opacité. La valeur 100 indique que le filigrane est complètement opaque et la valeur 0 indique que le filigrane est complètement transparent.

   >[!NOTE]
   >
   >Cet exemple ne modifie que l&#39;attribut d&#39;opacité.

1. Mettez à jour le filigrane.

   * Mettez à jour le filigrane en appelant la méthode `WatermarkManager` de l&#39;objet `updateWatermark` et en transmettant l&#39;objet `Watermark` dont l&#39;attribut a été modifié.

**Exemples de code**

Pour obtenir des exemples de code à l’aide du service Document Security, voir le Début rapide (mode SOAP) : Modification d’un filigrane à l’aide de la section API Java.

### Modification des filigranes à l’aide de l’API du service Web {#modify-watermarks-using-the-web-service-api}

Modifiez un filigrane à l’aide de l’API Document Security (service Web) :

1. Incluez des fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Assurez-vous d’utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un objet API Client de sécurité Document.

   * Créez un objet `DocumentSecurityServiceClient` en utilisant son constructeur par défaut.
   * Créez un objet `RightsManagementServiceClient.Endpoint.Address` en utilisant le constructeur `System.ServiceModel.EndpointAddress`. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/DocumentSecurityService?WSDL`). Vous n&#39;avez pas besoin d&#39;utiliser l&#39;attribut `lc_version`. Cet attribut est utilisé lorsque vous créez une référence de service.)
   * Créez un objet `System.ServiceModel.BasicHttpBinding` en obtenant la valeur du champ `DocumentSecurityServiceClient.Endpoint.Binding`. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le champ `MessageEncoding` de l’objet `System.ServiceModel.BasicHttpBinding` sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en exécutant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * Affectez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Affectez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.


1. Récupérez le filigrane à modifier.

   Récupérez le filigrane à modifier en appelant la méthode `DocumentSecurityServiceClient` de l’objet `getWatermarkByName`. Transmettez une valeur de chaîne qui spécifie le nom du filigrane. Cette méthode renvoie un objet `WatermarkSpec` qui représente le filigrane à modifier.

1. Définissez les attributs du filigrane.

   * Pour chaque propriété de filigrane à mettre à jour, créez un objet `MyMapOf_xsd_string_To_xsd_anyType_Item` distinct.
   * Définissez la valeur de clé en attribuant une valeur au membre de données `key` de l’objet `MyMapOf_xsd_string_To_xsd_anyType_Item` (par exemple, `WaterBackCmd:OPACITY)`.
   * Définissez la valeur en attribuant une valeur au membre de données `value` de l’objet `MyMapOf_xsd_string_To_xsd_anyType_Item` (par exemple, `.50`).
   * Créez un objet `MyArrayOf_xsd_anyType`. Pour chaque objet `MyMapOf_xsd_string_To_xsd_anyType_Item`, appelez la méthode `MyArrayOf_xsd_anyType` de l&#39;objet `Add`. Transmettez l&#39;objet `MyMapOf_xsd_string_To_xsd_anyType_Item`.
   * Affectez l&#39;objet `MyArrayOf_xsd_anyType` au membre de données `WatermarkSpec` de l&#39;objet `values`.

1. Mettez à jour le filigrane.

   Mettez à jour le filigrane en appelant la méthode `DocumentSecurityServiceClient` de l&#39;objet `updateWatermark` et en transmettant l&#39;objet `WatermarkSpec` représentant le filigrane à modifier.

**Exemples de code**

Pour obtenir des exemples de code à l’aide du service Document Security, reportez-vous au Début rapide suivant :

* &quot;Début rapide (MTOM) : Modification d’un filigrane à l’aide de l’API du service Web&quot;

## Recherche de Événements {#searching-for-events}

Le service de Rights Management effectue le suivi d’actions spécifiques à mesure qu’elles se produisent, telles que l’application d’une stratégie à un document, l’ouverture d’un document protégé par une stratégie et la révocation de l’accès aux documents. Le contrôle des événements doit être activé pour le service de Rights Management ou les événements ne sont pas suivis.

Les événements tombent dans l’une des catégories suivantes :

* Les événements d’administrateur sont des actions liées à un administrateur, telles que la création d’un nouveau compte d’administrateur.
* Les événements de document sont des actions liées à un document, telles que la fermeture d’un document protégé par une stratégie.
* Les événements de stratégie sont des actions liées à une stratégie, telles que la création d’une nouvelle stratégie.
* Les événements de service sont des actions liées au service Rights Management, telles que la synchronisation avec l’annuaire d’utilisateurs.

Vous pouvez rechercher des événements spécifiques en utilisant l’API Java Rights Management ou l’API de service Web. En recherchant des événements, vous pouvez effectuer des tâches, comme la création d’un fichier journal de certains événements.

>[!NOTE]
>
>Pour plus d’informations sur le service de Rights Management, voir [Guide de référence des services pour AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary_of_steps-10}

Pour rechercher un événement de Rights Management, procédez comme suit :

1. Incluez des fichiers de projet.
1. Créez un objet API Client Rights Management.
1. Indiquez le événement pour lequel effectuer la recherche.
1. Recherchez le événement.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

**Création d’un objet API Client Rights Management**

Avant de pouvoir exécuter une opération de service de Rights Management par programmation, vous devez créer un objet client de service de Rights Management. Si vous utilisez l’API Java, créez un objet `DocumentSecurityClient`. Si vous utilisez l’API du service Web Rights Management, créez un objet `DocumentSecurityServiceService`.

**Spécifiez les événements à rechercher**

Vous devez spécifier le événement à rechercher. Vous pouvez, par exemple, rechercher le événement de création de la stratégie, qui se produit lors de la création d’une nouvelle stratégie.

**Rechercher le événement**

Après avoir spécifié le événement à rechercher, vous pouvez utiliser l’API Java Rights Management ou l’API du service Web Rights Management pour rechercher le événement.

**Voir également**

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Rechercher des événements à l’aide de l’API Java {#search-for-events-using-the-java-api}

Recherchez des événements à l’aide de l’API Rights Management (Java) :

1. Inclure les fichiers de projet

   Incluez des fichiers JAR client, tels que adobe-rightsmanagement-client.jar, dans le chemin de classe de votre projet Java.

1. Création d’un objet API Client Rights Management

   Créez un objet `DocumentSecurityClient` en utilisant son constructeur et en transmettant un objet `ServiceClientFactory` contenant des propriétés de connexion.

1. Spécifiez les événements à rechercher

   * Créez un objet `EventManager` en appelant la méthode `DocumentSecurityClient` de l&#39;objet `getEventManager`. Cette méthode renvoie un objet `EventManager`.
   * Créez un objet `EventSearchFilter` en appelant son constructeur.
   * Spécifiez le événement pour lequel effectuer la recherche en appelant la méthode `EventSearchFilter` de l&#39;objet `setEventCode` et en transmettant un membre de données statique appartenant à la classe `EventManager` qui représente le événement pour lequel effectuer la recherche. Par exemple, pour rechercher le événement de création de stratégie, transmettez `EventManager.POLICY_CREATE_EVENT`.

   >[!NOTE]
   >
   >Vous pouvez définir des critères de recherche supplémentaires en appelant les méthodes d&#39;objet `EventSearchFilter`. Par exemple, appelez la méthode `setUserName` pour spécifier un utilisateur associé au événement.

1. Rechercher le événement

   Recherchez le événement en appelant la méthode `EventManager` de l&#39;objet `searchForEvents` et en transmettant l&#39;objet `EventSearchFilter` qui définit les critères de recherche de événement. Cette méthode renvoie un tableau d&#39;objets `Event`.

**Exemples de code**

Pour obtenir des exemples de code à l’aide du service Rights Management, reportez-vous aux Débuts rapides suivants :

* &quot;Début rapide (SOAP) : Recherche de événements à l’aide de l’API Java&quot;

### Rechercher des événements à l’aide de l’API de service Web {#search-for-events-using-the-web-service-api}

Recherchez des événements à l’aide de l’API du Rights Management (service Web) :

1. Inclure les fichiers de projet

   Créez un projet Microsoft .NET qui utilise MTOM. Assurez-vous d’utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Création d’un objet API Client Rights Management

   * Créez un objet `DocumentSecurityServiceClient` en utilisant son constructeur par défaut.
   * Créez un objet `DocumentSecurityServiceClient.Endpoint.Address` en utilisant le constructeur `System.ServiceModel.EndpointAddress`. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/RightsManagementService?WSDL`). Vous n&#39;avez pas besoin d&#39;utiliser l&#39;attribut `lc_version`. Cet attribut est utilisé lorsque vous créez une référence de service.)
   * Créez un objet `System.ServiceModel.BasicHttpBinding` en obtenant la valeur du champ `DocumentSecurityServiceClient.Endpoint.Binding`. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le champ `MessageEncoding` de l’objet `System.ServiceModel.BasicHttpBinding` sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en exécutant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * Affectez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Affectez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.


1. Spécifiez les événements à rechercher

   * Créez un objet `EventSpec` en utilisant son constructeur.
   * Spécifiez le début de la période au cours de laquelle le événement s’est produit en définissant le membre de données `firstTime.date` de l’objet `EventSpec` avec l’instance `DataTime` qui représente le début de la période au moment où le événement s’est produit.
   * Affectez la valeur `true` au membre de données `firstTime.dateSpecified` de l’objet `EventSpec`.
   * Spécifiez la fin de la période au cours de laquelle le événement s’est produit en définissant le membre de données `lastTime.date` de l’objet `EventSpec` avec l’instance `DataTime` qui représente la fin de la période au moment où le événement s’est produit.
   * Affectez la valeur `true` au membre de données `lastTime.dateSpecified` de l’objet `EventSpec`.
   * Définissez le événement à rechercher en attribuant une valeur de chaîne au membre de données `eventCode` de l&#39;objet `EventSpec`. Le tableau suivant liste les valeurs numériques que vous pouvez affecter à cette propriété :

   <table>
    <thead>
    <tr>
    <th><p>Type d'événement</p></th>
    <th><p>Valeur</p></th>
    </tr>
    </thead>
    <tbody>
    <tr>
    <td><p><code>ALL_EVENTS</code></p></td>
    <td><p>999</p></td>
    </tr>
    <tr>
    <td><p><code>USER_CHANGE_PASSWORD_EVENT</code></p></td>
    <td><p>1000</p></td>
    </tr>
    <tr>
    <td><p><code>USER_REGISTER_EVENT</code></p></td>
    <td><p>1001</p></td>
    </tr>
    <tr>
    <td><p><code>USER_PREREGISTER_EVENT</code></p></td>
    <td><p>1002</p></td>
    </tr>
    <tr>
    <td><p><code>USER_ACTIVATE_EVENT</code></p></td>
    <td><p>1003</p></td>
    </tr>
    <tr>
    <td><p><code>USER_DEACTIVATE_EVENT</code></p></td>
    <td><p>1004</p></td>
    </tr>
    <tr>
    <td><p><code>USER_AUTHENTICATE_EVENT</code></p></td>
    <td><p>1005</p></td>
    </tr>
    <tr>
    <td><p><code>USER_AUTHENTICATE_DENY_EVENT </code></p></td>
    <td><p>1006</p></td>
    </tr>
    <tr>
    <td><p><code>USER_ACCOUNT_LOCK_EVENT</code></p></td>
    <td><p>1007</p></td>
    </tr>
    <tr>
    <td><p><code>USER_DELETE_EVENT </code></p></td>
    <td><p>1008</p></td>
    </tr>
    <tr>
    <td><p><code>USER_UPDATE_PROFILE_EVENT </code></p></td>
    <td><p>1009</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_VIEW_EVENT </code></p></td>
    <td><p>2000</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_PRINT_LOW_EVENT </code></p></td>
    <td><p>2001</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_PRINT_HIGH_EVENT </code></p></td>
    <td><p>2002</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_SIGN_EVENT </code></p></td>
    <td><p>2003</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_ADD_ANNOTATION_EVENT </code></p></td>
    <td><p>2004</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_FORM_FILL_EVENT </code></p></td>
    <td><p>2005</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_CLOSE_EVENT </code></p></td>
    <td><p>2006</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_MODIFY_EVENT </code></p></td>
    <td><p>2007</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_CHANGE_SECURITY_HANDLER_EVENT </code></p></td>
    <td><p>2008</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_SWITCH_POLICY_EVENT </code></p></td>
    <td><p>2009</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_REVOKE_EVENT </code></p></td>
    <td><p>2010</p></td>
    </tr>
    <tr>
    <td><p><code>$1</code></p></td>
    <td><p>2011</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_SECURE_EVENT </code></p></td>
    <td><p>2012</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_UNKNOWN_CLIENT_EVENT </code></p></td>
    <td><p>2013</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_CHANGE_REVOKE_URL_EVENT </code></p></td>
    <td><p>2014</p></td>
    </tr>
    <tr>
    <td><p><code>POLICY_CHANGE_EVENT </code></p></td>
    <td><p>3000</p></td>
    </tr>
    <tr>
    <td><p><code>POLICY_ENABLE_EVENT </code></p></td>
    <td><p>3001</p></td>
    </tr>
    <tr>
    <td><p><code>POLICY_DISABLE_EVENT </code></p></td>
    <td><p>3002</p></td>
    </tr>
    <tr>
    <td><p><code>POLICY_CREATE_EVENT </code></p></td>
    <td><p>3003</p></td>
    </tr>
    <tr>
    <td><p><code>POLICY_DELETE_EVENT </code></p></td>
    <td><p>3004</p></td>
    </tr>
    <tr>
    <td><p><code>POLICY_CHANGE_OWNER_EVENT </code></p></td>
    <td><p>3005</p></td>
    </tr>
    <tr>
    <td><p><code>SERVER_CLIENT_SYNC_EVENT </code></p></td>
    <td><p>4 000</p></td>
    </tr>
    <tr>
    <td><p><code>SERVER_SYNC_DIR_INFO_EVENT </code></p></td>
    <td><p>4001</p></td>
    </tr>
    <tr>
    <td><p><code>SERVER_SYNC_DIR_COMPLETE_EVENT </code></p></td>
    <td><p>4002</p></td>
    </tr>
    <tr>
    <td><p><code>SERVER_VERSION_MISMATCH_EVENT </code></p></td>
    <td><p>4003</p></td>
    </tr>
    <tr>
    <td><p><code>SERVER_CONFIG_CHANGE_EVENT </code></p></td>
    <td><p>4004</p></td>
    </tr>
    <tr>
    <td><p><code>SERVER_ENABLE_OFFLINE_ACCESS_EVENT </code></p></td>
    <td><p>4005</p></td>
    </tr>
    <tr>
    <td><p><code>ADMIN_ADD_EVENT </code></p></td>
    <td><p>5 000</p></td>
    </tr>
    <tr>
    <td><p><code>ADMIN_DELETE_EVENT </code></p></td>
    <td><p>5001</p></td>
    </tr>
    <tr>
    <td><p><code>ADMIN_EDIT_EVENT </code></p></td>
    <td><p>5002</p></td>
    </tr>
    <tr>
    <td><p><code>ADMIN_ACTIVATE_EVENT </code></p></td>
    <td><p>5003</p></td>
    </tr>
    <tr>
    <td><p><code>ADMIN_DEACTIVATE_EVENT </code></p></td>
    <td><p>5004</p></td>
    </tr>
    <tr>
    <td><p><code>ERROR_DIRECTORY_SERVICE_EVENT </code></p></td>
    <td><p>6 000</p></td>
    </tr>
    <tr>
    <td><p><code>CREATED_POLICYSET_EVENT</code></p></td>
    <td><p>7 000</p></td>
    </tr>
    <tr>
    <td><p><code>DELETED_POLICYSET_EVENT</code></p></td>
    <td><p>7001</p></td>
    </tr>
    <tr>
    <td><p><code>MODIFIED_POLICYSET_EVENT</code></p></td>
    <td><p>7002</p></td>
    </tr>
    </tbody>
    </table>

1. Rechercher le événement

   Recherchez le événement en appelant la méthode `DocumentSecurityServiceClient` de l’objet `searchForEvents` et en transmettant l’objet `EventSpec` qui représente le événement pour lequel effectuer la recherche et le nombre maximal de résultats. Cette méthode renvoie une collection `MyArrayOf_xsd_anyType` où chaque élément est une instance `AuditSpec`. A l&#39;aide d&#39;une instance `AuditSpec`, vous pouvez obtenir des informations sur le événement, telles que l&#39;heure à laquelle il s&#39;est produit. L&#39;instance `AuditSpec` contient un membre de données `timestamp` qui spécifie ces informations.

**Exemples de code**

Pour obtenir des exemples de code à l’aide du service Rights Management, reportez-vous aux Débuts rapides suivants :

* &quot;Début rapide (MTOM) : Recherche de événements à l’aide de l’API du service Web&quot;
* &quot;Quick Début (SwaRef) : Recherche de événements à l’aide de l’API du service Web&quot;

**Voir également**

[Appel de AEM Forms à l’aide de MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Appel de AEM Forms à l’aide de SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Application de stratégies aux Documents Word {#applying-policies-to-word-documents}

Outre les documents PDF, le service Rights Management prend en charge d’autres formats de document, tels qu’un document Microsoft Word (DOC) et d’autres formats de fichier Microsoft Office. Par exemple, vous pouvez appliquer une stratégie à un document Word afin de la sécuriser. En appliquant une stratégie à un document Word, vous restreignez l’accès au document. Vous ne pouvez pas appliquer une stratégie à un document si le document est déjà sécurisé avec une stratégie.

Vous pouvez contrôler l’utilisation d’un document Word protégé par une stratégie après l’avoir distribué. C&#39;est-à-dire, vous pouvez voir comment le document est utilisé et qui l&#39;utilise. Par exemple, vous pouvez savoir quand quelqu’un a ouvert le document.

>[!NOTE]
>
>Pour plus d&#39;informations sur le service Document Security, consultez le [Guide de référence des services pour AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary_of_steps-11}

Pour appliquer une stratégie à un document Word, procédez comme suit :

1. Incluez des fichiers de projet.
1. Créez un objet API Client de sécurité Document.
1. Récupérez un document Word auquel une stratégie est appliquée.
1. Appliquez une stratégie existante au document Word.
1. Enregistrez le document Word protégé par une stratégie.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

**Création d’un objet API Client de sécurité Document**

Avant de pouvoir exécuter par programmation une opération du service Document Security, vous devez créer un objet client du service Document Security.

**Récupération d’un document Word**

Vous devez récupérer un document Word pour appliquer une stratégie. Une fois que vous avez appliqué une stratégie au document Word, les utilisateurs sont limités lors de l’utilisation du document. Par exemple, si la stratégie ne permet pas l’ouverture du document hors ligne, les utilisateurs doivent être en ligne pour ouvrir le document.

**Appliquer une stratégie existante au document Word**

Pour appliquer une stratégie à un document Word, vous devez référencer une stratégie existante et spécifier à quel jeu de stratégies elle appartient. L’utilisateur qui définit les propriétés de connexion doit avoir accès à la stratégie spécifiée. Dans le cas contraire, une exception se produit.

**Enregistrer le document Word**

Une fois que le service Document Security a appliqué une stratégie à un document Word, vous pouvez enregistrer le document Word protégé par une stratégie en tant que fichier DOC.

**Voir également**

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Révocation de l’accès aux Documents](protecting-documents-policies.md#revoking-access-to-documents)

### Appliquer une stratégie à un document Word à l’aide de l’API Java {#apply-a-policy-to-a-word-document-using-the-java-api}

Appliquez une stratégie à un document Word à l’aide de l’API Document Security (Java) :

1. Incluez des fichiers de projet.

   Incluez des fichiers JAR client, tels que adobe-rightsmanagement-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un objet API Client de sécurité Document.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `DocumentSecurityClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`. 

1. Récupérez un document Word.

   * Créez un objet `java.io.FileInputStream` qui représente le document Word en utilisant son constructeur et en transmettant une valeur de chaîne qui spécifie l&#39;emplacement du document Word.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Appliquez une stratégie existante au document Word.

   * Créez un objet `DocumentManager` en appelant la méthode `DocumentSecurityClient` de l&#39;objet `getDocumentManager`.
   * Appliquez une stratégie au document Word en appelant la méthode `DocumentManager` de l&#39;objet `protectDocument` et en transmettant les valeurs suivantes :

      * Objet `com.adobe.idp.Document` contenant le document Word auquel la stratégie est appliquée.
      * Valeur de chaîne qui spécifie le nom du document.
      * Valeur de chaîne qui spécifie le nom du jeu de stratégies auquel appartient la stratégie. Vous pouvez spécifier une valeur `null` qui se traduit par l&#39;utilisation du jeu de stratégies `MyPolicies`.
      * Valeur de chaîne qui spécifie le nom de la stratégie.
      * Valeur de chaîne qui représente le nom du domaine du gestionnaire d’utilisateurs de l’utilisateur qui est l’éditeur du document. Cette valeur de paramètre est facultative et peut être nulle (si ce paramètre est nul, la valeur de paramètre suivante doit être nulle).
      * Valeur de chaîne qui représente le nom canonique de l’utilisateur du gestionnaire d’utilisateurs qui est l’éditeur du document. Cette valeur de paramètre est facultative et peut être `null` (si ce paramètre est `null`, la valeur de paramètre précédente doit être `null`).
      * `com.adobe.livecycle.rightsmanagement.Locale` qui représente le paramètre régional utilisé pour sélectionner le modèle MS Office. Cette valeur de paramètre est facultative et vous pouvez spécifier `null`.

      La méthode `protectDocument` renvoie un objet `RMSecureDocumentResult` contenant le document Word protégé par une stratégie.


1. Enregistrez le document Word.

   * Appelez la méthode `RMSecureDocumentResult` de l’objet `getProtectedDoc` pour obtenir le document Word protégé par une stratégie. Cette méthode renvoie un objet `com.adobe.idp.Document`.
   * Créez un objet `java.io.File` et assurez-vous que l&#39;extension de fichier est DOC.
   * Appelez la méthode `com.adobe.idp.Document` de l&#39;objet `copyToFile` pour copier le contenu de l&#39;objet `Document` dans le fichier (veillez à utiliser l&#39;objet `Document` renvoyé par la méthode `getProtectedDoc`).

**Exemples de code**

Pour obtenir des exemples de code à l’aide du service Document Security, reportez-vous au Début rapide suivant :

* &quot;Début rapide (mode SOAP) : Application d’une stratégie à un document Word à l’aide de l’API Java&quot;

### Appliquer une stratégie à un document Word à l’aide de l’API du service Web {#apply-a-policy-to-a-word-document-using-the-web-service-api}

Appliquez une stratégie à un document Word à l’aide de l’API Document Security (service Web) :

1. Incluez des fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Assurez-vous d’utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/DocumentSecurityService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un objet API Client de sécurité Document.

   * Créez un objet `DocumentSecurityServiceClient` en utilisant son constructeur par défaut.
   * Créez un objet `DocumentSecurityServiceClient.Endpoint.Address` en utilisant le constructeur `System.ServiceModel.EndpointAddress`. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/DocumentSecurityService?WSDL`). Vous n&#39;avez pas besoin d&#39;utiliser l&#39;attribut `lc_version`. Cet attribut est utilisé lorsque vous créez une référence de service.)
   * Créez un objet `System.ServiceModel.BasicHttpBinding` en obtenant la valeur du champ `DocumentSecurityServiceClient.Endpoint.Binding`. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le champ `MessageEncoding` de l’objet `System.ServiceModel.BasicHttpBinding` sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en exécutant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * Affectez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Affectez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.


1. Récupérez un document Word.

   * Créez un objet `BLOB` en utilisant son constructeur. L&#39;objet `BLOB` permet de stocker un document Word auquel une stratégie est appliquée.
   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur de chaîne qui représente l&#39;emplacement du fichier du document Word et le mode d&#39;ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `System.IO.FileStream`. Déterminez la taille du tableau d’octets en obtenant la propriété `System.IO.FileStream` de l’objet `Length`.
   * Renseignez le tableau d’octets avec les données de flux en appelant la méthode `System.IO.FileStream` de l’objet `Read`. Passez le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’objet `BLOB` en attribuant son champ `MTOM` au contenu du tableau d’octets.

1. Appliquez une stratégie existante au document Word.

   Appliquez une stratégie au document Word en appelant la méthode `DocumentSecurityServiceClient` de l&#39;objet `protectDocument` et en transmettant les valeurs suivantes :

   * Objet `BLOB` contenant le document Word auquel la stratégie est appliquée.
   * Valeur de chaîne qui spécifie le nom du document.
   * Valeur de chaîne qui spécifie le nom du jeu de stratégies auquel appartient la stratégie. Vous pouvez spécifier une valeur `null` qui se traduit par l&#39;utilisation du jeu de stratégies `MyPolicies`.
   * Valeur de chaîne qui spécifie le nom de la stratégie.
   * Valeur de chaîne qui représente le nom du domaine du gestionnaire d’utilisateurs de l’utilisateur qui est l’éditeur du document. Cette valeur de paramètre est facultative et peut être nulle (si ce paramètre est nul, la valeur de paramètre suivante doit être `null`).
   * Valeur de chaîne qui représente le nom canonique de l’utilisateur du gestionnaire d’utilisateurs qui est l’éditeur du document. Cette valeur de paramètre est facultative et peut être nulle (si ce paramètre est nul, la valeur de paramètre précédente doit être `null`).
   * Valeur `RMLocale` qui spécifie la valeur du paramètre régional (par exemple, `RMLocale.en`).
   * Paramètre de sortie de chaîne utilisé pour stocker la valeur de l’identifiant de stratégie.
   * Paramètre de sortie de chaîne utilisé pour stocker la valeur d’identificateur protégée par une stratégie.
   * Paramètre de sortie de chaîne utilisé pour stocker le type MIME (par exemple, `application/doc`).

   La méthode `protectDocument` renvoie un objet `BLOB` contenant le document Word protégé par une stratégie.

1. Enregistrez le document Word.

   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur de chaîne qui représente l&#39;emplacement du fichier du document Word protégé par une stratégie.
   * Créez un tableau d’octets qui stocke le contenu des données de l’objet `BLOB` renvoyé par la méthode `protectDocument`. Renseignez le tableau d’octets en obtenant la valeur du membre de données `MTOM` de l’objet `BLOB`.
   * Créez un objet `System.IO.BinaryWriter` en appelant son constructeur et en transmettant l&#39;objet `System.IO.FileStream`.
   * Ecrivez le contenu du tableau d’octets dans un fichier Word en appelant la méthode `System.IO.BinaryWriter` de l’objet `Write` et en transmettant le tableau d’octets.

**Exemples de code**

Pour obtenir des exemples de code à l’aide du service Document Security, reportez-vous au Début rapide suivant :

* &quot;Début rapide (MTOM) : Application d’une stratégie à un document Word à l’aide de l’API du service Web&quot;

## Suppression de stratégies des Documents Word {#removing-policies-from-word-documents}

Vous pouvez supprimer une stratégie d’un document Word protégé par une stratégie afin de supprimer la sécurité du document. Autrement dit, si vous ne voulez plus que le document soit protégé par une politique. Si vous souhaitez mettre à jour un document Word protégé par une stratégie avec une nouvelle stratégie, il est plus efficace de changer de stratégie au lieu de la supprimer et d’ajouter la stratégie mise à jour.

>[!NOTE]
>
>Pour plus d&#39;informations sur le service Document Security, consultez le [Guide de référence des services pour AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary_of_steps-12}

Pour supprimer une stratégie d’un document Word protégé par une stratégie, procédez comme suit :

1. Inclure les fichiers de projet
1. Créez un objet API Client de sécurité Document.
1. Récupérez un document Word protégé par une stratégie.
1. Supprimez la stratégie du document Word.
1. Enregistrer le document Word non sécurisé.s

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

**Création d’un objet API Client de sécurité Document**

Avant de pouvoir exécuter par programmation une opération du service Document Security, créez un objet client du service Document Security.

**Récupération d’un document Word protégé par une stratégie**

Pour supprimer une stratégie, vous devez récupérer un document Word protégé par une stratégie. Si vous tentez de supprimer une stratégie d’un document Word qui n’est pas protégé par une stratégie, vous provoquerez une exception.

**Supprimer la stratégie du document Word**

Vous pouvez supprimer une stratégie d’un document Word protégé par une stratégie, à condition qu’un administrateur soit spécifié dans les paramètres de connexion. Dans le cas contraire, la stratégie utilisée pour sécuriser un document doit contenir l&#39;autorisation `SWITCH_POLICY` pour supprimer une stratégie d&#39;un document Word. En outre, l’utilisateur spécifié dans les paramètres de connexion AEM Forms doit également disposer de cette autorisation. Dans le cas contraire, une exception est générée.

**Enregistrer le document Word non sécurisé**

Une fois que le service Document Security a supprimé une stratégie d&#39;un document Word, vous pouvez enregistrer le document Word non sécurisé en tant que fichier DOC.

**Voir également**

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Application de stratégies à des Documents Word](protecting-documents-policies.md#applying-policies-to-word-documents)

### Supprimez une stratégie d&#39;un document Word à l&#39;aide de l&#39;API Java {#remove-a-policy-from-a-word-document-using-the-java-api}

Supprimez une stratégie d’un document Word protégé par une stratégie à l’aide de l’API Document Security (Java) :

1. Inclure les fichiers de projet

   Incluez des fichiers JAR client, tels que adobe-rightsmanagement-client.jar, dans le chemin de classe de votre projet Java.

1. Création d’un objet API Client de sécurité Document

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `RightsManagementClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`. 

1. Récupération d’un document Word protégé par une stratégie

   * Créez un objet `java.io.FileInputStream` qui représente le document Word protégé par une stratégie en utilisant son constructeur et en transmettant une valeur de chaîne qui spécifie l&#39;emplacement du document Word.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Supprimer la stratégie du document Word

   * Créez un objet `DocumentManager` en appelant la méthode `RightsManagementClient` de l&#39;objet `getDocumentManager`.
   * Supprimez une stratégie du document Word en appelant la méthode `DocumentManager` de l&#39;objet `removeSecurity` et en transmettant l&#39;objet `com.adobe.idp.Document` contenant le document Word protégé par une stratégie. Cette méthode renvoie un objet `com.adobe.idp.Document` contenant un document Word non sécurisé.

1. Enregistrer le document Word non sécurisé

   * Créez un objet `java.io.File` et assurez-vous que l&#39;extension de fichier est DOC.
   * Appelez la méthode `Document` de l&#39;objet `copyToFile` pour copier le contenu de l&#39;objet `Document` dans le fichier (veillez à utiliser l&#39;objet `Document` renvoyé par la méthode `removeSecurity`).

**Exemples de code**

Pour obtenir des exemples de code à l’aide du service Document Security, reportez-vous au Début rapide suivant :

* &quot;Début rapide (mode SOAP) : Suppression d’une stratégie d’un document Word à l’aide de l’API Java&quot;

### Supprimez une stratégie d’un document Word à l’aide de l’API de service Web {#remove-a-policy-from-a-word-document-using-the-web-service-api}.

Supprimez une stratégie d’un document Word protégé par une stratégie à l’aide de l’API Document Security (service Web) :

1. Inclure les fichiers de projet

   Créez un projet Microsoft .NET qui utilise MTOM. Assurez-vous d’utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Création d’un objet API Client de sécurité Document

   * Créez un objet `RightsManagementServiceClient` en utilisant son constructeur par défaut.
   * Créez un objet `RightsManagementServiceClient.Endpoint.Address` en utilisant le constructeur `System.ServiceModel.EndpointAddress`. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/RightsManagementService?WSDL`). Vous n&#39;avez pas besoin d&#39;utiliser l&#39;attribut `lc_version`. Cet attribut est utilisé lorsque vous créez une référence de service.)
   * Créez un objet `System.ServiceModel.BasicHttpBinding` en obtenant la valeur du champ `RightsManagementServiceClient.Endpoint.Binding`. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le champ `MessageEncoding` de l’objet `System.ServiceModel.BasicHttpBinding` sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en exécutant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * Affectez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Affectez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.


1. Récupération d’un document Word protégé par une stratégie

   * Créez un objet `BLOB` en utilisant son constructeur. L&#39;objet `BLOB` est utilisé pour stocker le document Word protégé par une stratégie à partir duquel la stratégie est supprimée.
   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur de chaîne qui représente l&#39;emplacement du fichier du document Word et le mode d&#39;ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `System.IO.FileStream`. Vous pouvez déterminer la taille du tableau d’octets en obtenant la propriété `System.IO.FileStream` de l’objet `Length`.
   * Renseignez le tableau d’octets avec les données de flux en appelant la méthode `System.IO.FileStream` de l’objet `Read` et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’objet `BLOB` en attribuant son champ `MTOM` au contenu du tableau d’octets.

1. Supprimer la stratégie du document Word

   Supprimez la stratégie du document Word en appelant la méthode `RightsManagementServiceClient` de l&#39;objet `removePolicySecurity` et en transmettant l&#39;objet `BLOB` contenant le document Word protégé par une stratégie. Cette méthode renvoie un objet `BLOB` contenant un document Word non sécurisé.

1. Enregistrer le document Word non sécurisé

   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur de chaîne qui représente l&#39;emplacement du fichier du document Word non sécurisé.
   * Créez un tableau d’octets qui stocke le contenu des données de l’objet `BLOB` renvoyé par la méthode `removePolicySecurity`. Renseignez le tableau d’octets en obtenant la valeur du champ `BLOB` de l’objet `MTOM`.
   * Créez un objet `System.IO.BinaryWriter` en appelant son constructeur et en transmettant l&#39;objet `System.IO.FileStream`.

**Exemples de code**

Pour obtenir des exemples de code à l’aide du service Document Security, reportez-vous au Début rapide suivant :

* &quot;Début rapide (MTOM) : Suppression d’une stratégie d’un document Word à l’aide de l’API du service Web&quot;

**Voir également**

[Appel de AEM Forms à l’aide de MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
