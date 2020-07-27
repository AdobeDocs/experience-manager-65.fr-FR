---
title: Protection des Documents avec des stratégies
seo-title: Protection des Documents avec des stratégies
description: 'null'
seo-description: 'null'
uuid: 6feb69ef-7b61-4d0b-8c87-d65d98bae9b5
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 9b1d2bf3-f28c-41b2-9026-1f3311556422
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '15466'
ht-degree: 4%

---


# Protection des Documents avec des stratégies {#protecting-documents-with-policies}

**À propos du service de sécurité Document**

Le service Document Security permet aux utilisateurs d’appliquer de manière dynamique des paramètres de confidentialité aux documents PDF Adobe et de conserver un contrôle sur les documents, quelle que soit leur diffusion.

Le service Document Security empêche la diffusion des informations au-delà de la portée de l’utilisateur en permettant à ce dernier de contrôler la manière dont les destinataires utilisent le document PDF protégé par une stratégie. Un utilisateur peut spécifier qui peut ouvrir un document, comment l’utiliser et contrôler le document une fois distribué. Un utilisateur peut également contrôler dynamiquement l’accès à un document protégé par une stratégie et peut même révoquer dynamiquement l’accès au document.

Le service Document Security protège également d&#39;autres types de fichiers tels que les fichiers Microsoft Word (fichiers DOC). Vous pouvez utiliser l&#39;API du client Document Security pour utiliser ces types de fichiers. Les versions suivantes sont prises en charge :

* Fichiers Microsoft Office 2003 (DOC, XLS, PPT)
* Fichiers Microsoft Office 2007 (fichiers DOCX, XLSX, PPTX)
* Fichiers PTC Pro/E

Pour plus de clarté, les deux sections suivantes traitent de la façon de travailler avec les documents Word :

* [Application de stratégies à des Documents Word](protecting-documents-policies.md#applying-policies-to-word-documents)
* [Suppression de stratégies des Documents Word](protecting-documents-policies.md#removing-policies-from-word-documents)

Vous pouvez exécuter ces tâches à l’aide du service Document Security :

* Créez des stratégies. Pour plus d’informations, voir [Création de stratégies](protecting-documents-policies.md#creating-policies).
* permet de modifier des stratégies. Pour plus d’informations, voir [Modification de stratégies](protecting-documents-policies.md#modifying-policies).
* supprimer des stratégies. Pour plus d’informations, voir [Suppression de stratégies](protecting-documents-policies.md#deleting-policies).
* Appliquer des stratégies aux documents PDF. Pour plus d’informations, voir [Application de stratégies à des Documents](protecting-documents-policies.md#applying-policies-to-pdf-documents)PDF.
* Supprimez les stratégies des documents PDF. Pour plus d’informations, voir [Suppression de stratégies de Documents](protecting-documents-policies.md#removing-policies-from-pdf-documents)PDF.
* Inspectez les documents protégés par une stratégie. Pour plus d’informations, voir [Inspection des Documents](protecting-documents-policies.md#inspecting-policy-protected-pdf-documents)PDF protégés par une stratégie.
* Révoquer l’accès aux documents PDF. Pour plus d’informations, voir [Révocation de l’accès aux Documents](protecting-documents-policies.md#revoking-access-to-documents).
* Rétablit l’accès aux documents révoqués. Pour plus d’informations, voir [Rétablissement de l’accès aux Documents](protecting-documents-policies.md#reinstating-access-to-revoked-documents)révoqués.
* Créez des filigranes. Pour plus d’informations, voir [Création de filigranes](protecting-documents-policies.md#creating-watermarks).
* Recherchez des événements. Pour plus d’informations, voir [Recherche de Événements](protecting-documents-policies.md#searching-for-events).

>[!NOTE]
>
>For more information about the Document Security service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Création de stratégies {#creating-policies}

Vous pouvez créer des stratégies par programmation à l’aide de l’API Java de Document Security ou de l’API de service Web. Une *stratégie* est un ensemble d’informations qui comprend les paramètres de sécurité de l’document, les utilisateurs autorisés et les droits d’utilisation. Vous pouvez créer et enregistrer autant de stratégies que vous le souhaitez à l’aide de paramètres de sécurité adaptés à différentes situations et à différents utilisateurs.

Les stratégies vous permettent d’effectuer les tâches suivantes :

* Spécifiez les personnes qui peuvent ouvrir le document. Les Destinataires peuvent appartenir à votre organisation ou être externes à celle-ci.
* Indiquez comment les destinataires peuvent utiliser le document. Vous pouvez restreindre l’accès à différentes fonctions d’Acrobat et d’Adobe Reader. Ces fonctionnalités permettent d’imprimer et de copier du texte, d’ajouter des signatures et d’ajouter des commentaires à un document.
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
>For more information about the Document Security service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

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
* espace de nommage.jar (si le AEM Forms est déployé sur JBoss)
* jaxb-api.jar (si le AEM Forms est déployé sur JBoss)
* jaxb-impl.jar (si le AEM Forms est déployé sur JBoss)
* jaxb-libs.jar (si le AEM Forms est déployé sur JBoss)
* jaxb-xjc.jar (si le AEM Forms est déployé sur JBoss)
* relaxngDatatype.jar (si le AEM Forms est déployé sur JBoss)
* xsdlib.jar (si le AEM Forms est déployé sur JBoss)
* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar
* jbossall-client.jar (utilisez un fichier JAR différent si le AEM Forms n’est pas déployé sur JBoss)

For information about the location of these JAR files, see [Including AEM Forms Java library files](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

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

* **AES256**: Représente l’algorithme de chiffrement AES avec une clé de 256 bits.
* **AES128**: Représente l’algorithme de chiffrement AES avec une clé de 128 bits.
* **NoEncryption :** Ne représente aucun chiffrement.

Lors de la spécification de l’ `NoEncryption` option, vous ne pouvez pas définir l’ `PlaintextMetadata` option sur `false`. Si vous tentez de le faire, une exception est levée.

>[!NOTE]
>
>Pour plus d’informations sur les autres attributs que vous pouvez définir, voir la description de l’ `Policy` interface dans le Guide de référence [de l’API](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)AEM Forms.

**Création d’une entrée de stratégie**

Une entrée de stratégie associe des entités, qui sont des groupes et des utilisateurs, et des autorisations à une stratégie. Une stratégie doit comporter au moins une entrée de stratégie. Supposons, par exemple, que vous effectuiez les tâches suivantes :

* Créez et enregistrez une entrée de stratégie qui permet à un groupe de ne vue qu&#39;un document en ligne et interdit aux destinataires de la copier.
* Joignez l’entrée de stratégie à la stratégie.
* Sécurisez un document avec la stratégie à l’aide d’Acrobat.

Ces actions ont pour conséquence que les destinataires ne peuvent que vue en ligne du document et ne peuvent pas le copier. Le document reste sécurisé jusqu&#39;à ce que la sécurité en soit supprimée.

**Enregistrer la stratégie**

Une nouvelle stratégie doit être enregistrée avant de pouvoir être utilisée. Après avoir enregistré une stratégie, vous pouvez l’utiliser pour protéger les documents.

### Création d’une stratégie à l’aide de l’API Java {#create-a-policy-using-the-java-api}

Créez une stratégie à l’aide de l’API Document Security (Java) :

1. Incluez des fichiers de projet.

   Incluez des fichiers JAR client, tels que adobe-rightsmanagement-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un objet API Client de sécurité Document.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `DocumentSecurityClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`. 

1. Définissez les attributs de la stratégie.

   * Créez un `Policy` objet en appelant la méthode `InfomodelObjectFactory` statique de l’ `createPolicy` objet. Cette méthode renvoie un `Policy` objet.
   * Définissez l’attribut name de la stratégie en appelant la `Policy` `setName` méthode de l’objet et en transmettant une valeur de chaîne qui spécifie le nom de la stratégie.
   * Définissez la description de la stratégie en appelant la `Policy` `setDescription` méthode de l’objet et en transmettant une valeur de chaîne qui spécifie la description de la stratégie.
   * Définissez le jeu de stratégies auquel appartient la nouvelle stratégie en appelant la `Policy` `setPolicySetName` méthode de l’objet et en transmettant une valeur de chaîne qui spécifie le nom du jeu de stratégies. (Vous pouvez spécifier `null` pour cette valeur de paramètre afin que la stratégie soit ajoutée au jeu de stratégies *Mes stratégies* .)
   * Créez la période de validité de la stratégie en appelant la `InfomodelObjectFactory` méthode statique de l’ `createValidityPeriod` objet. Cette méthode renvoie un `ValidityPeriod` objet.
   * Définissez le nombre de jours pendant lesquels un document protégé par une stratégie est accessible en appelant la `ValidityPeriod` `setRelativeExpirationDays` méthode de l’objet et en transmettant un entier spécifiant le nombre de jours.
   * Définissez la période de validité de la stratégie en appelant la `Policy` méthode de l’ `setValidityPeriod` objet et en transmettant l’ `ValidityPeriod` objet.

1. Créez une entrée de stratégie.

   * Créez une entrée de stratégie en appelant la `InfomodelObjectFactory` méthode statique de l’ `createPolicyEntry` objet. Cette méthode renvoie un `PolicyEntry` objet.
   * Spécifiez les autorisations de la stratégie en appelant la méthode statique de l’ `InfomodelObjectFactory` objet `createPermission` . Transmettez un membre de données statiques qui appartient à l’ `Permission` interface qui représente l’autorisation. Cette méthode renvoie un `Permission` objet. Par exemple, pour ajouter l’autorisation permettant aux utilisateurs de copier des données d’un document PDF protégé par une stratégie, transmettez `Permission.COPY`. (Répétez cette étape pour chaque autorisation d’ajout).
   * Ajoutez l’autorisation d’accès à l’entrée de stratégie en appelant la `PolicyEntry` méthode de l’ `addPermission` objet et en transmettant l’ `Permission` objet. (Répétez cette étape pour chaque `Permission` objet que vous avez créé).
   * Créez l’entité de sécurité de la stratégie en appelant la `InfomodelObjectFactory` méthode statique de l’ `createSpecialPrincipal` objet. Transmettez un membre de données qui appartient à l’ `InfomodelObjectFactory` objet qui représente l’entité de sécurité. Cette méthode renvoie un `Principal` objet. Par exemple, pour ajouter l’éditeur du document en tant que principal, transmettez `InfomodelObjectFactory.PUBLISHER_PRINCIPAL`.
   * Ajoutez l’entité de sécurité à l’entrée de stratégie en appelant la `PolicyEntry` méthode de l’objet et en transmettant l’ `setPrincipal``Principal` objet.
   * Ajoutez l’entrée de stratégie à la stratégie en appelant la `Policy` méthode de l’objet et en transmettant l’ `addPolicyEntry` `PolicyEntry` objet.

1. Enregistrez la stratégie.

   * Créez un `PolicyManager` objet en appelant la `DocumentSecurityClient` méthode de l’ `getPolicyManager` objet.
   * Enregistrez la stratégie en invoquant la `PolicyManager` `registerPolicy` méthode de l’objet et en transmettant les valeurs suivantes :

      * Objet `Policy` représentant la stratégie à enregistrer.
   * Valeur de chaîne qui représente le jeu de stratégies auquel appartient la stratégie.

   Si vous utilisez un compte d’administrateur AEM forms dans les paramètres de connexion pour créer l’ `DocumentSecurityClient` objet, spécifiez le nom du jeu de stratégies lorsque vous appelez la `registerPolicy` méthode. Si vous transmettez une `null` valeur pour le jeu de stratégies, la stratégie est créée dans le jeu de stratégies *Mes stratégies* des administrateurs.

   Si vous utilisez un utilisateur Document Security dans les paramètres de connexion, vous pouvez appeler la `registerPolicy` méthode surchargée qui accepte uniquement la stratégie. En d’autres termes, vous n’avez pas besoin de spécifier le nom du jeu de stratégies. Cependant, la stratégie est ajoutée au jeu de stratégies nommé *Mes stratégies*. Si vous ne souhaitez pas ajouter la nouvelle stratégie à ce jeu de stratégies, spécifiez un nom de jeu de stratégies lorsque vous appelez la `registerPolicy` méthode.

   >[!NOTE]
   >
   >Lors de la création d’une stratégie, référencez un jeu de stratégies existant. Si vous spécifiez un jeu de stratégies qui n’existe pas, une exception est générée.

Pour obtenir des exemples de code à l’aide du service Document Security, reportez-vous aux sections suivantes :

* &quot;Début rapide (mode SOAP) : Création d’une stratégie à l’aide de l’API Java&quot;

### Création d’une stratégie à l’aide de l’API de service Web {#create-a-policy-using-the-web-service-api}

Créez une stratégie à l’aide de l’API Document Security (service Web) :

1. Incluez des fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Assurez-vous d’utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant les AEM Forms.

1. Créez un objet API Client de sécurité Document.

   * Create a `DocumentSecurityServiceClient` object by using its default constructor.
   * Create a `DocumentSecurityServiceClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/RightsManagementService?WSDL`). Vous n’avez pas besoin d’utiliser l’ `lc_version` attribut. Cet attribut est utilisé lorsque vous créez une référence de service.)
   * Créez un `System.ServiceModel.BasicHttpBinding` objet en obtenant la valeur du `RightsManagementServiceClient.Endpoint.Binding` champ. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le `System.ServiceModel.BasicHttpBinding` champ de l’ `MessageEncoding` objet sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en exécutant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.


1. Définissez les attributs de la stratégie.

   * Créez un objet `PolicySpec` en utilisant son constructeur.
   * Définissez le nom de la stratégie en attribuant une valeur de chaîne au membre `PolicySpec` de données de l’ `name` objet.
   * Définissez la description de la stratégie en attribuant une valeur de chaîne au membre `PolicySpec` de données de l’ `description` objet.
   * Définissez le jeu de stratégies auquel la stratégie doit appartenir en attribuant une valeur de chaîne au membre `PolicySpec` de données de l’ `policySetName` objet. Vous devez spécifier un nom de jeu de stratégies existant. (Vous pouvez spécifier `null` pour cette valeur de paramètre afin que la stratégie soit ajoutée à *Mes stratégies*.)
   * Définissez la période d’ouverture hors connexion de la stratégie en attribuant une valeur entière au membre `PolicySpec` de données de l’ `offlineLeasePeriod` objet.
   * Définissez le membre `PolicySpec` `policyXml` de données de l’objet avec une valeur de chaîne qui représente les données XML PDRL. Pour effectuer cette tâche, créez un objet .NET `StreamReader` à l&#39;aide de son constructeur. Transmettez l’emplacement d’un fichier XML PDRL représentant la stratégie au `StreamReader` constructeur. Ensuite, appelez la `StreamReader` méthode de l’objet `ReadLine` et affectez la valeur renvoyée à une variable de chaîne. Effectuez une itération sur l’ `StreamReader` objet jusqu’à ce que la `ReadLine` méthode renvoie null. Affectez la variable de chaîne au membre `PolicySpec` de données de l’ `policyXml` objet.

1. Créez une entrée de stratégie.

   Il n’est pas nécessaire de créer une entrée de stratégie lors de la création d’une stratégie à l’aide de l’API du service Web Document Security. L&#39;entrée de stratégie est définie dans le document PDRL.

1. Enregistrez la stratégie.

   Enregistrez la stratégie en invoquant la `DocumentSecurityServiceClient` `registerPolicy` méthode de l’objet et en transmettant les valeurs suivantes :

   * Objet `PolicySpec` représentant la stratégie à enregistrer.
   * Valeur de chaîne qui représente le jeu de stratégies auquel appartient la stratégie. Vous pouvez spécifier une `null` valeur qui entraîne l’ajout de la stratégie au jeu de stratégies *MyPolices* .

   Si vous utilisez un compte d’administrateur AEM forms dans les paramètres de connexion pour créer l’ `DocumentSecurityClient` objet, spécifiez le nom du jeu de stratégies lorsque vous appelez la `registerPolicy` méthode.

   Si vous utilisez un utilisateur Document SecurityDocument Security dans les paramètres de connexion, vous pouvez appeler la `registerPolicy` méthode surchargée qui accepte uniquement la stratégie. En d’autres termes, vous n’avez pas besoin de spécifier le nom du jeu de stratégies. Cependant, la stratégie est ajoutée au jeu de stratégies nommé *Mes stratégies*. Si vous ne souhaitez pas ajouter la nouvelle stratégie à ce jeu de stratégies, spécifiez un nom de jeu de stratégies lorsque vous appelez la `registerPolicy` méthode.

   >[!NOTE]
   >
   >Lors de la création d’une stratégie et de la spécification d’un jeu de stratégies, veillez à spécifier un jeu de stratégies existant. Si vous spécifiez un jeu de stratégies qui n’existe pas, une exception est générée.

Pour obtenir des exemples de code à l’aide du service Document Security, reportez-vous aux Débuts rapides suivants :

* &quot;Début rapide (MTOM) : Création d’une stratégie à l’aide de l’API du service Web&quot;
* &quot;Quick Début (SwaRef) : Création d’une stratégie à l’aide de l’API du service Web&quot;

## Modification de stratégies {#modifying-policies}

Vous pouvez modifier une stratégie existante à l’aide de l’API Java Document Security ou de l’API de service Web. Pour apporter des modifications à une stratégie existante, vous devez la récupérer, la modifier, puis la mettre à jour sur le serveur. Supposons, par exemple, que vous récupériez une stratégie existante et étendiez sa période de validité. Avant que la modification ne prenne effet, vous devez mettre à jour la stratégie.

Vous pouvez modifier une stratégie lorsque les besoins de l’entreprise changent et que la stratégie ne reflète plus ces besoins. Au lieu de créer une nouvelle stratégie, vous pouvez simplement mettre à jour une stratégie existante.

Pour modifier les attributs de stratégie à l’aide d’un service Web (par exemple, à l’aide de classes proxy Java créées avec JAX-WS), vous devez vous assurer que la stratégie est enregistrée auprès du service Document Security. Vous pouvez ensuite référencer la stratégie existante à l’aide de la `PolicySpec.getPolicyXml` méthode et modifier les attributs de la stratégie à l’aide des méthodes applicables. Par exemple, vous pouvez modifier la période d’ouverture hors connexion en appelant la `PolicySpec.setOfflineLeasePeriod` méthode.

>[!NOTE]
>
>For more information about the Document Security service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

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

Avant de pouvoir exécuter par programmation une opération Document Security, vous devez créer un objet client de service Document Security. Si vous utilisez l’API Java, créez un `RightsManagementClient` objet. Si vous utilisez l’API du service Web Document Security, créez un `RightsManagementServiceService` objet.

**Récupération d’une stratégie existante**

Vous devez récupérer une stratégie existante pour la modifier. Pour récupérer une stratégie, spécifiez le nom de la stratégie et le jeu de stratégies auquel elle appartient. Si vous spécifiez une `null` valeur pour le nom du jeu de stratégies, la stratégie est récupérée à partir du jeu de stratégies *Mes stratégies* .

**Définir les attributs de la stratégie**

Pour modifier une stratégie, vous modifiez la valeur des attributs de stratégie. Le seul attribut de stratégie que vous ne pouvez pas modifier est l’attribut name. Par exemple, pour modifier la période d’ouverture hors connexion de la stratégie, vous pouvez modifier la valeur de l’attribut de période d’ouverture hors connexion de la stratégie.

Lors de la modification de la période d’ouverture hors connexion d’une stratégie à l’aide d’un service Web, le `offlineLeasePeriod` champ de l’ `PolicySpec` interface est ignoré. Pour mettre à jour la période d’ouverture hors connexion, modifiez l’ `OfflineLeasePeriod` élément dans le document XML PDRL. Référencez ensuite le document XML PDRL mis à jour en utilisant le membre `PolicySpec` `policyXML` de données de l’interface.

>[!NOTE]
>
>Pour plus d’informations sur les autres attributs que vous pouvez définir, voir la description de l’ `Policy` interface dans le Guide de référence [de l’API](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)AEM Forms.

**Mettre à jour la stratégie**

Avant que les modifications apportées à une stratégie ne prennent effet, vous devez mettre à jour la stratégie avec le service Document Security. Les modifications apportées aux stratégies qui protègent les documents sont mises à jour la prochaine fois que le document protégé par une stratégie est synchronisé avec le service Document Security.

### Modification des stratégies existantes à l’aide de l’API Java {#modify-existing-policies-using-the-java-api}

Modifiez une stratégie existante à l’aide de l’API Document Security (Java) :

1. Incluez des fichiers de projet.

   Incluez des fichiers JAR client, tels que adobe-rightsmanagement-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un objet API Client de sécurité Document.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `RightsManagementClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`. 

1. Récupérez une stratégie existante.

   * Créez un `PolicyManager` objet en appelant la `RightsManagementClient` méthode de l’ `getPolicyManager` objet.
   * Créez un `Policy` objet qui représente la stratégie à mettre à jour en appelant la `PolicyManager` méthode de l’ `getPolicy` objet et en transmettant les valeurs suivantes.&quot;

      * Valeur de chaîne qui représente le nom du jeu de stratégies auquel appartient la stratégie. Vous pouvez spécifier `null` si le jeu de `MyPolicies` stratégies est utilisé.
      * Valeur de chaîne qui représente le nom de la stratégie.

1. Définissez les attributs de la stratégie.

   Modifiez les attributs de la stratégie pour répondre aux besoins de votre entreprise. Par exemple, pour modifier la période d’ouverture hors connexion de la stratégie, appelez la `Policy` `setOfflineLeasePeriod` méthode de l’objet.

1. Mettez à jour la stratégie.

   Mettez à jour la stratégie en appelant la `PolicyManager` `updatePolicy` méthode de l’objet. Transmettez l’ `Policy` objet qui représente la stratégie à mettre à jour.

**Exemples de code**

Pour obtenir des exemples de code à l’aide du service Document Security, voir le Début rapide (mode SOAP) : Modification d’une stratégie à l’aide de la section API Java.

### Modification de stratégies existantes à l’aide de l’API de service Web {#modify-existing-policies-using-the-web-service-api}

Modifiez une stratégie existante à l’aide de l’API Document Security (service Web) :

1. Incluez des fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Assurez-vous d’utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant les AEM Forms.

1. Créez un objet API Client de sécurité Document.

   * Create a `RightsManagementServiceClient` object by using its default constructor.
   * Create a `RightsManagementServiceClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/RightsManagementService?WSDL`). Vous n’avez pas besoin d’utiliser l’ `lc_version` attribut. Cet attribut est utilisé lorsque vous créez une référence de service.)
   * Créez un `System.ServiceModel.BasicHttpBinding` objet en obtenant la valeur du `RightsManagementServiceClient.Endpoint.Binding` champ. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le `System.ServiceModel.BasicHttpBinding` champ de l’ `MessageEncoding` objet sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en exécutant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.


1. Récupérez une stratégie existante.

   Créez un `PolicySpec` objet représentant la stratégie à modifier en appelant la `RightsManagementServiceClient` méthode de l’ `getPolicy` objet et en transmettant les valeurs suivantes :

   * Valeur de chaîne qui spécifie le nom du jeu de stratégies auquel appartient la stratégie. Vous pouvez spécifier `null` si le jeu de `MyPolicies` stratégies est utilisé.
   * Valeur de chaîne qui spécifie le nom de la stratégie.

1. Définissez les attributs de la stratégie.

   Modifiez les attributs de la stratégie pour répondre aux besoins de votre entreprise.

1. Mettez à jour la stratégie.

   Mettez à jour la stratégie en appelant la `RightsManagementServiceClient` méthode de l’ `updatePolicyFromSDK` objet et en transmettant l’ `PolicySpec` objet qui représente la stratégie à mettre à jour.

**Exemples de code**

Pour obtenir des exemples de code à l’aide du service Document Security, reportez-vous aux Débuts rapides suivants :

* &quot;Début rapide (MTOM) : Modification d’une stratégie à l’aide de l’API du service Web&quot;
* &quot;Quick Début (SwaRef) : Modification d’une stratégie à l’aide de l’API du service Web&quot;

## Suppression de stratégies {#deleting-policies}

Vous pouvez supprimer une stratégie existante à l’aide de l’API Java Document Security ou de l’API de service Web. Une fois une stratégie supprimée, elle ne peut plus être utilisée pour protéger les documents. Cependant, les documents existants protégés par une stratégie qui utilisent la stratégie sont toujours protégés. Vous pouvez supprimer une stratégie lorsqu’une nouvelle stratégie devient disponible.

>[!NOTE]
>
>For more information about the Document Security service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary_of_steps-2}

Pour supprimer une stratégie existante, procédez comme suit :

1. Inclure les fichiers de projet
1. Créez un objet API Client de sécurité Document.
1. Supprimez la stratégie.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

**Création d’un objet API Client de sécurité Document**

Avant de pouvoir exécuter par programmation une opération du service Document Security, vous devez créer un objet client du service Document Security. Si vous utilisez l’API Java, créez un `RightsManagementClient` objet. Si vous utilisez l’API du service Web Document Security, créez un `RightsManagementServiceService` objet.

**Supprimer la stratégie**

Pour supprimer une stratégie, vous spécifiez la stratégie à supprimer et le jeu de stratégies auquel elle appartient. L’utilisateur dont les paramètres sont utilisés pour appeler des AEM Forms doit être autorisé à supprimer la stratégie ; dans le cas contraire, une exception se produit. De même, si vous tentez de supprimer une stratégie qui n’existe pas, une exception se produit.

### Suppression de stratégies à l’aide de l’API Java {#delete-policies-using-the-java-api}

Supprimez une stratégie à l’aide de l’API Document Security (Java) :

1. Incluez des fichiers de projet.

   Incluez des fichiers JAR client, tels que adobe-rightsmanagement-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un objet API Client de sécurité Document.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `RightsManagementClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`. 

1. Supprimez la stratégie.

   * Créez un `PolicyManager` objet en appelant la `RightsManagementClient` méthode de l’ `getPolicyManager` objet.
   * Supprimez la stratégie en appelant la `PolicyManager` `deletePolicy` méthode de l’objet et en transmettant les valeurs suivantes :

      * Valeur de chaîne qui spécifie le nom du jeu de stratégies auquel appartient la stratégie. Vous pouvez spécifier `null` si le jeu de `MyPolicies` stratégies est utilisé.
      * Valeur de chaîne qui spécifie le nom de la stratégie à supprimer.

**Exemples de code**

Pour obtenir des exemples de code à l’aide du service Document Security, reportez-vous aux Débuts rapides suivants :

* &quot;Début rapide (mode SOAP) : Suppression d’une stratégie à l’aide de l’API Java&quot;

### Suppression de stratégies à l’aide de l’API de service Web {#delete-policies-using-the-web-service-api}

Supprimez une stratégie à l’aide de l’API Document Security (service Web) :

1. Incluez des fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Assurez-vous d’utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant les AEM Forms.

1. Créez un objet API Client de sécurité Document.

   * Create a `RightsManagementServiceClient` object by using its default constructor.
   * Create a `RightsManagementServiceClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/RightsManagementService?WSDL`). Vous n’avez pas besoin d’utiliser l’ `lc_version` attribut. Cet attribut est utilisé lorsque vous créez une référence de service.)
   * Créez un `System.ServiceModel.BasicHttpBinding` objet en obtenant la valeur du `RightsManagementServiceClient.Endpoint.Binding` champ. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le `System.ServiceModel.BasicHttpBinding` champ de l’ `MessageEncoding` objet sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en exécutant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.


1. Supprimez la stratégie.

   Delete a policy by invoking the `RightsManagementServiceClient` object’s `deletePolicy` method and passing the following values:

   * Valeur de chaîne qui spécifie le nom du jeu de stratégies auquel appartient la stratégie. Vous pouvez spécifier `null` si le jeu de `MyPolicies` stratégies est utilisé.
   * Valeur de chaîne qui spécifie le nom de la stratégie à supprimer.

**Exemples de code**

Pour obtenir des exemples de code à l’aide du service Document Security, reportez-vous aux Débuts rapides suivants :

* &quot;Début rapide (MTOM) : Suppression d’une stratégie à l’aide de l’API du service Web&quot;
* &quot;Quick Début (SwaRef) : Suppression d’une stratégie à l’aide de l’API du service Web&quot;

## Application de stratégies à des Documents PDF {#applying-policies-to-pdf-documents}

Vous pouvez appliquer une stratégie à un document PDF afin de sécuriser le document. En appliquant une stratégie à un document PDF, vous restreignez l’accès au document. Vous ne pouvez pas appliquer une stratégie à un document si le document est déjà sécurisé avec une stratégie.

Pendant que le document est ouvert, vous pouvez également restreindre l’accès aux fonctions d’Acrobat et de Adobe Reader, notamment la possibilité d’imprimer et de copier du texte, d’apporter des modifications et d’ajouter des signatures et des commentaires à un document. En outre, vous pouvez révoquer un document PDF protégé par une stratégie lorsque vous ne souhaitez plus que les utilisateurs accèdent au document.

Vous pouvez contrôler l’utilisation d’un document protégé par une stratégie après l’avoir distribué. C&#39;est-à-dire, vous pouvez voir comment le document est utilisé et qui l&#39;utilise. Par exemple, vous pouvez savoir quand quelqu’un a ouvert le document.

>[!NOTE]
>
>For more information about the Document Security service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

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

Avant de pouvoir exécuter par programmation une opération du service Document Security, créez un objet client du service Document Security. Si vous utilisez l’API Java, créez un `DocumentSecurityClient` objet. Si vous utilisez l’API du service Web Document Security, créez un `DocumentSecurityServiceService` objet.

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

### Application d’une stratégie à un document PDF à l’aide de l’API Java {#apply-a-policy-to-a-pdf-document-using-the-java-api}

Appliquez une stratégie à un document PDF à l’aide de l’API Document Security (Java) :

1. Incluez des fichiers de projet.

   Incluez des fichiers JAR client, tels que adobe-rightsmanagement-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un objet API Client de sécurité Document.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `RightsManagementClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`. 

1. Récupérez un document PDF.

   * Créez un `java.io.FileInputStream` objet représentant le document PDF à l’aide de son constructeur. Transmettez une valeur de chaîne qui spécifie l’emplacement du document PDF.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Appliquez une stratégie existante au document PDF.

   * Créez un `DocumentManager` objet en appelant la `RightsManagementClient` méthode de l’ `getDocumentManager` objet.
   * Appliquez une stratégie au document PDF en appelant la `DocumentManager` `protectDocument` méthode de l’objet et en transmettant les valeurs suivantes :

      * Objet `com.adobe.idp.Document` contenant le document PDF auquel la stratégie est appliquée.
      * Valeur de chaîne qui spécifie le nom du document.
      * Valeur de chaîne qui spécifie le nom du jeu de stratégies auquel appartient la stratégie. Vous pouvez spécifier une `null` valeur qui entraîne l’utilisation du jeu de `MyPolicies` stratégies.
      * Valeur de chaîne qui spécifie le nom de la stratégie.
      * Valeur de chaîne qui représente le nom du domaine du gestionnaire d’utilisateurs de l’utilisateur qui est l’éditeur du document. Cette valeur de paramètre est facultative et peut être nulle (si ce paramètre est nul, la valeur de paramètre suivante doit être nulle).
      * Valeur de chaîne qui représente le nom canonique de l’utilisateur du gestionnaire d’utilisateurs qui est l’éditeur du document. Cette valeur de paramètre est facultative et peut être `null` (si ce paramètre est nul, la valeur de paramètre précédente doit être `null`).
      * Un paramètre `com.adobe.livecycle.rightsmanagement.Locale` qui représente le paramètre régional utilisé pour sélectionner le modèle MS Office. Cette valeur de paramètre est facultative et n’est pas utilisée pour les documents PDF. Pour sécuriser un document PDF, spécifiez `null`.

      La `protectDocument` méthode renvoie un `RMSecureDocumentResult` objet contenant le document PDF protégé par une stratégie.


1. Enregistrez le document PDF.

   * Appelez la méthode `RMSecureDocumentResult` de l’objet `getProtectedDoc` pour obtenir le document PDF protégé par une stratégie. Cette méthode renvoie un `com.adobe.idp.Document` objet.
   * Create a `java.io.File` object and ensure that the file extension is PDF.
   * Appelez la `com.adobe.idp.Document` méthode de l’ `copyToFile` objet pour copier le contenu de l’ `Document` objet dans le fichier (veillez à utiliser l’ `Document` objet renvoyé par la `getProtectedDoc` méthode).

**Exemples de code**

Pour obtenir des exemples de code à l’aide du service Document Security, reportez-vous aux Débuts rapides suivants :

* &quot;Début rapide (mode EJB) : Application d’une stratégie à un document PDF à l’aide de l’API Java&quot;
* &quot;Début rapide (mode SOAP) : Application d’une stratégie à un document PDF à l’aide de l’API Java&quot;

**Voir également**

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Application d’une stratégie à un document PDF à l’aide de l’API du service Web {#apply-a-policy-to-a-pdf-document-using-the-web-service-api}

Appliquez une stratégie à un document PDF à l’aide de l’API Document Security (service Web) :

1. Incluez des fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Assurez-vous d’utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant les AEM Forms.

1. Créez un objet API Client de sécurité Document.

   * Create a `RightsManagementServiceClient` object by using its default constructor.
   * Create a `RightsManagementServiceClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. Transmettez une valeur de chaîne qui spécifie le WSDL au service Forms (par exemple, `http://localhost:8080/soap/services/RightsManagementService?WSDL`). Vous n’avez pas besoin d’utiliser l’ `lc_version` attribut. Cet attribut est utilisé lorsque vous créez une référence de service.)
   * Créez un `System.ServiceModel.BasicHttpBinding` objet en obtenant la valeur du `RightsManagementServiceClient.Endpoint.Binding` champ. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le `System.ServiceModel.BasicHttpBinding` champ de l’ `MessageEncoding` objet sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en exécutant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.


1. Récupérez un document PDF.

   * Créez un objet `BLOB` en utilisant son constructeur. L’ `BLOB` objet est utilisé pour stocker un document PDF auquel une stratégie est appliquée.
   * Créez un `System.IO.FileStream` objet en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du fichier du document PDF et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’ `System.IO.FileStream` objet. Déterminez la taille du tableau d’octets en obtenant la `System.IO.FileStream` `Length` propriété de l’objet.
   * Renseignez le tableau d’octets avec les données de flux en appelant la `System.IO.FileStream` méthode de l’ `Read` objet. Passez le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’ `BLOB` objet en affectant son `MTOM` champ au contenu du tableau d’octets.

1. Appliquez une stratégie existante au document PDF.

   Appliquez une stratégie au document PDF en appelant la `RightsManagementServiceClient` `protectDocument` méthode de l’objet et en transmettant les valeurs suivantes :

   * Objet `BLOB` contenant le document PDF auquel la stratégie est appliquée.
   * Valeur de chaîne qui spécifie le nom du document.
   * Valeur de chaîne qui spécifie le nom du jeu de stratégies auquel appartient la stratégie. Vous pouvez spécifier une `null` valeur qui entraîne l’utilisation du jeu de `MyPolicies` stratégies.
   * Valeur de chaîne qui spécifie le nom de la stratégie.
   * Valeur de chaîne qui représente le nom du domaine du gestionnaire d’utilisateurs de l’utilisateur qui est l’éditeur du document. Cette valeur de paramètre est facultative et peut être nulle (si ce paramètre est nul, la valeur de paramètre suivante doit être `null`).
   * Valeur de chaîne qui représente le nom canonique de l’utilisateur du gestionnaire d’utilisateurs qui est l’éditeur du document. Cette valeur de paramètre est facultative et peut être nulle (si ce paramètre est nul, la valeur de paramètre précédente doit être `null`).
   * Valeur `RMLocale` spécifiant la valeur du paramètre régional (par exemple, `RMLocale.en`).
   * Paramètre de sortie de chaîne utilisé pour stocker la valeur de l’identifiant de stratégie.
   * Paramètre de sortie de chaîne utilisé pour stocker la valeur d’identificateur protégée par une stratégie.
   * Paramètre de sortie de chaîne utilisé pour stocker le type MIME (par exemple, `application/pdf`).

   La `protectDocument` méthode renvoie un `BLOB` objet contenant le document PDF protégé par une stratégie.

1. Enregistrez le document PDF.

   * Créez un `System.IO.FileStream` objet en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du fichier du document PDF protégé par une stratégie.
   * Créez un tableau d’octets qui stocke le contenu des données de l’ `BLOB` objet renvoyé par la `protectDocument` méthode. Renseignez le tableau d’octets en obtenant la valeur du membre `BLOB` de données de l’ `MTOM` objet.
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * Ecrivez le contenu du tableau d’octets dans un fichier PDF en appelant la méthode `System.IO.BinaryWriter` `Write` de l’objet et en transmettant le tableau d’octets.

**Exemples de code**

Pour obtenir des exemples de code à l’aide du service Document Security, reportez-vous aux Débuts rapides suivants :

* &quot;Début rapide (MTOM) : Application d’une stratégie à un document PDF à l’aide de l’API du service Web&quot;
* &quot;Quick Début (SwaRef) : Application d’une stratégie à un document PDF à l’aide de l’API du service Web&quot;

## Suppression de stratégies de Documents PDF {#removing-policies-from-pdf-documents}

Vous pouvez supprimer une stratégie d’un document protégé par une stratégie afin de supprimer la sécurité du document. Autrement dit, si vous ne voulez plus que le document soit protégé par une politique. Si vous souhaitez mettre à jour un document protégé par une stratégie à l’aide d’une nouvelle stratégie, il est plus efficace de changer de stratégie au lieu de la supprimer et d’ajouter la stratégie mise à jour.

>[!NOTE]
>
>For more information about the Document Security service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

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

Vous pouvez supprimer une stratégie d’un document PDF protégé par une stratégie, à condition qu’un administrateur soit spécifié dans les paramètres de connexion. Si ce n’est pas le cas, la stratégie utilisée pour sécuriser un document doit contenir l’ `SWITCH_POLICY` autorisation afin de supprimer une stratégie d’un document PDF. En outre, l’utilisateur spécifié dans les paramètres de connexion AEM Forms doit également disposer de cette autorisation. Dans le cas contraire, une exception est générée.

**Enregistrer le document PDF non sécurisé**

Une fois que le service Document Security a supprimé une stratégie d’un document PDF, vous pouvez enregistrer le document PDF non sécurisé en tant que fichier PDF.

**Voir également**

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Application de stratégies à des Documents PDF](protecting-documents-policies.md#applying-policies-to-pdf-documents)

### Suppression d’une stratégie d’un document PDF à l’aide de l’API Java {#remove-a-policy-from-a-pdf-document-using-the-java-api}

Supprimez une stratégie d’un document PDF protégé par une stratégie à l’aide de l’API Document Security (Java) :

1. Incluez des fichiers de projet.

   Incluez des fichiers JAR client, tels que adobe-rightsmanagement-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un objet API Client de sécurité Document.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `DocumentSecurityClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`. 

1. Récupérez un document PDF protégé par une stratégie.

   * Créez un `java.io.FileInputStream` objet qui représente le document PDF protégé par une stratégie en utilisant son constructeur et en transmettant une valeur de chaîne qui spécifie l’emplacement du document PDF.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Supprimez la stratégie du document PDF.

   * Créez un `DocumentManager` objet en appelant la `DocumentSecurityClient` méthode de l’ `getDocumentManager` objet.
   * Supprimez une stratégie du document PDF en appelant la `DocumentManager` méthode de l’objet et en transmettant l’ `removeSecurity` `com.adobe.idp.Document` objet contenant le document PDF protégé par une stratégie. Cette méthode renvoie un `com.adobe.idp.Document` objet contenant un document PDF non sécurisé.

1. Enregistrez le document PDF non sécurisé.

   * Create a `java.io.File` object and ensure that the file extension is PDF.
   * Appelez la `Document` méthode de l’ `copyToFile` objet pour copier le contenu de l’ `Document` objet dans le fichier (veillez à utiliser l’ `Document` objet renvoyé par la `removeSecurity` méthode).

**Exemples de code**

Pour obtenir des exemples de code à l’aide du service Document Security, reportez-vous aux Débuts rapides suivants :

* &quot;Début rapide (mode SOAP) : Suppression d’une stratégie d’un document PDF à l’aide de l’API Java&quot;

### Suppression d’une stratégie à l’aide de l’API de service Web {#remove-a-policy-using-the-web-service-api}

Supprimez une stratégie d’un document PDF protégé par une stratégie à l’aide de l’API Document Security (service Web) :

1. Incluez des fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Assurez-vous d’utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant les AEM Forms.

1. Créez un objet API Client de sécurité Document.

   * Create a `DocumentSecurityServiceClient` object by using its default constructor.
   * Create a `DocumentSecurityServiceClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/RightsManagementService?WSDL`). Vous n’avez pas besoin d’utiliser l’ `lc_version` attribut. Cet attribut est utilisé lorsque vous créez une référence de service.)
   * Créez un `System.ServiceModel.BasicHttpBinding` objet en obtenant la valeur du `DocumentSecurityServiceClient.Endpoint.Binding` champ. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le `System.ServiceModel.BasicHttpBinding` champ de l’ `MessageEncoding` objet sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en exécutant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.


1. Récupérez un document PDF protégé par une stratégie.

   * Créez un objet `BLOB` en utilisant son constructeur. L’ `BLOB` objet est utilisé pour stocker le document PDF protégé par une stratégie à partir duquel la stratégie est supprimée.
   * Créez un `System.IO.FileStream` objet en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du fichier du document PDF et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’ `System.IO.FileStream` objet. Vous pouvez déterminer la taille du tableau d’octets en obtenant la `System.IO.FileStream` `Length` propriété de l’objet.
   * Renseignez le tableau d’octets avec les données de flux en appelant la `System.IO.FileStream` `Read` méthode de l’objet et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’ `BLOB` objet en affectant son `MTOM` champ au contenu du tableau d’octets.

1. Supprimez la stratégie du document PDF.

   Supprimez la stratégie du document PDF en appelant la `DocumentSecurityServiceClient` méthode de l’objet et en transmettant l’ `removePolicySecurity` `BLOB` objet contenant le document PDF protégé par une stratégie. Cette méthode renvoie un `BLOB` objet contenant un document PDF non sécurisé.

1. Enregistrez le document PDF non sécurisé.

   * Créez un `System.IO.FileStream` objet en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du fichier du document PDF non sécurisé.
   * Créez un tableau d’octets qui stocke le contenu des données de l’ `BLOB` objet renvoyé par la `removePolicySecurity` méthode. Renseignez le tableau d’octets en obtenant la valeur du `BLOB` champ de l’ `MTOM` objet.
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.

**Exemples de code**

Pour obtenir des exemples de code à l’aide du service Document Security, reportez-vous aux Débuts rapides suivants :

* &quot;Début rapide (MTOM) : Suppression d’une stratégie d’un document PDF à l’aide de l’API du service Web&quot;
* &quot;Quick Début (SwaRef) : Suppression d’une stratégie d’un document PDF à l’aide de l’API du service Web&quot;

**Voir également**

[Appel de AEM Forms à l’aide de MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Appel de AEM Forms à l’aide de SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Révocation de l’accès aux Documents {#revoking-access-to-documents}

Vous pouvez révoquer l’accès à un document PDF protégé par une stratégie, de sorte que toutes les copies du document soient inaccessibles aux utilisateurs. Lorsqu’un utilisateur tente d’ouvrir un document PDF révoqué, il est redirigé vers une URL spécifiée où un document modifié peut être affiché. L’URL vers laquelle l’utilisateur est redirigé doit être spécifiée par programmation. Lorsque vous révoquez l’accès à un document, la modification prend effet lorsque l’utilisateur se synchronise avec le service Document Security en ouvrant le document protégé par une stratégie en ligne.

La possibilité de révoquer l’accès à un document offre une sécurité supplémentaire. Supposons, par exemple, qu’une version plus récente d’un document soit disponible et que vous ne souhaitiez plus que quiconque consulte la version obsolète. Dans ce cas, l&#39;accès à l&#39;ancien document peut être révoqué et personne ne peut vue le document à moins que l&#39;accès ne soit rétabli.

>[!NOTE]
>
>For more information about the Document Security service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

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

   * Créez un `java.io.FileInputStream` objet représentant le document PDF protégé par une stratégie en utilisant son constructeur et en transmettant une valeur de chaîne qui spécifie l’emplacement du document PDF.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Révoquer le document protégé par une stratégie

   * Créez un `DocumentManager` objet en appelant la `DocumentSecurityClient` méthode de l’ `getDocumentManager` objet.
   * Récupérez la valeur d’identifiant de licence du document protégé par une stratégie en appelant la `DocumentManager` méthode de l’ `getLicenseId` objet. Transmettez l’ `com.adobe.idp.Document` objet qui représente le document protégé par une stratégie. Cette méthode renvoie une valeur de chaîne qui représente la valeur de l’identifiant de licence.
   * Créez un `LicenseManager` objet en appelant la `DocumentSecurityClient` méthode de l’ `getLicenseManager` objet.
   * Révoquez le document protégé par une stratégie en appelant la `LicenseManager` `revokeLicense` méthode de l’objet et en transmettant les valeurs suivantes :

      * Valeur de chaîne qui spécifie la valeur d’identifiant de licence du document protégé par une stratégie (indiquez la valeur de retour de la `DocumentManager` méthode de l’ `getLicenseId` objet).
      * Membre de données statiques de l’ `License` interface qui spécifie le motif de révocation du document. Par exemple, vous pouvez spécifier `License.DOCUMENT_REVISED`.
      * Valeur `java.net.URL` spécifiant l’emplacement où se trouve un document révisé. Si vous ne souhaitez pas rediriger un utilisateur vers une autre URL, vous pouvez transmettre `null`.

**Exemples de code**

Pour obtenir des exemples de code à l’aide du service Document Security, reportez-vous aux Débuts rapides suivants :

* &quot;Début rapide (mode SOAP) : Révocation d’un document à l’aide de l’API Java&quot;

### Révoquer l’accès aux documents à l’aide de l’API du service Web {#revoke-access-to-documents-using-the-web-service-api}

Révoquez l’accès à un document PDF protégé par une stratégie à l’aide de l’API Document Security (service Web) :

1. Inclure les fichiers de projet

   Créez un projet Microsoft .NET qui utilise MTOM. Assurez-vous d’utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant les AEM Forms.

1. Création d’un objet API Client de sécurité Document

   * Create a `DocumentSecurityServiceClient` object by using its default constructor.
   * Create a `DocumentSecurityServiceClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/RightsManagementService?WSDL`). Vous n’avez pas besoin d’utiliser l’ `lc_version` attribut. Cet attribut est utilisé lorsque vous créez une référence de service.)
   * Créez un `System.ServiceModel.BasicHttpBinding` objet en obtenant la valeur du `DocumentSecurityServiceClient.Endpoint.Binding` champ. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le `System.ServiceModel.BasicHttpBinding` champ de l’ `MessageEncoding` objet sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en exécutant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.


1. Récupération d’un document PDF protégé par une stratégie

   * Créez un objet `BLOB` en utilisant son constructeur. L’ `BLOB` objet est utilisé pour stocker un document PDF protégé par une stratégie qui est révoqué.
   * Créez un `System.IO.FileStream` objet en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du fichier du document PDF protégé par une stratégie à révoquer et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’ `System.IO.FileStream` objet. Vous pouvez déterminer la taille du tableau d’octets en obtenant la `System.IO.FileStream` `Length` propriété de l’objet.
   * Renseignez le tableau d’octets avec les données de flux en appelant la `System.IO.FileStream` `Read` méthode de l’objet et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’ `BLOB` objet en affectant son `MTOM` champ au contenu du tableau d’octets.

1. Révoquer le document protégé par une stratégie

   * Récupérez la valeur d’identifiant de licence du document protégé par une stratégie en appelant la `DocumentSecurityServiceClient` méthode de l’ `getLicenseID` objet et en transmettant l’ `BLOB` objet qui représente le document protégé par une stratégie. Cette méthode renvoie une valeur de chaîne qui représente l’identifiant de licence.
   * Révoquez le document protégé par une stratégie en appelant la `DocumentSecurityServiceClient` `revokeLicense` méthode de l’objet et en transmettant les valeurs suivantes :

      * Valeur de chaîne qui spécifie la valeur d’identifiant de licence du document protégé par une stratégie (indiquez la valeur de retour de la `DocumentSecurityServiceService` méthode de l’ `getLicenseId` objet).
      * Membre de données statiques de l’ `Reason` enum qui spécifie la raison de la révocation du document. Par exemple, vous pouvez spécifier `Reason.DOCUMENT_REVISED`.
      * Valeur `string` spécifiant l’emplacement de l’URL vers lequel se trouve un document révisé. Si vous ne souhaitez pas rediriger un utilisateur vers une autre URL, vous pouvez transmettre `null`.

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
>For more information about the Document Security service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary_of_steps-6}

Pour rétablir l’accès à un document PDF révoqué, procédez comme suit :

1. Incluez des fichiers de projet.
1. Créez un objet API Client de sécurité Document.
1. Récupérez l’identifiant de licence du document PDF révoqué.
1. Rétablit l’accès au document PDF révoqué.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

**Création d’un objet API Client de sécurité Document**

Avant de pouvoir exécuter par programmation une opération du service Document Security, vous devez créer un objet client du service Document Security. Si vous utilisez l’API Java, créez un `DocumentSecurityClient` objet. Si vous utilisez l’API du service Web Document Security, créez un `DocumentSecurityServiceService` objet.

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

   * Créez un `java.io.FileInputStream` objet représentant le document PDF révoqué en utilisant son constructeur et en transmettant une valeur de chaîne indiquant l’emplacement du document PDF.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 
   * Créez un `DocumentManager` objet en appelant la `DocumentSecurityClient` méthode de l’ `getDocumentManager` objet.
   * Récupérez la valeur d’identifiant de licence du document révoqué en appelant la `DocumentManager` méthode de l’ `getLicenseId` objet et en transmettant l’ `com.adobe.idp.Document` objet qui représente le document révoqué. Cette méthode renvoie une valeur de chaîne qui représente l’identifiant de licence.

1. Rétablit l’accès au document PDF révoqué.

   * Créez un `LicenseManager` objet en appelant la `DocumentSecurityClient` méthode de l’ `getLicenseManager` objet.
   * Rétablissez l’accès au document PDF révoqué en appelant la `LicenseManager` `unrevokeLicense` méthode de l’objet et en transmettant la valeur d’identifiant de licence du document révoqué.

**Exemples de code**

Pour obtenir des exemples de code à l’aide du service Document Security, reportez-vous aux Débuts rapides suivants :

* &quot;Début rapide (mode SOAP) : Rétablissement de l’accès à un document révoqué à l’aide de l’API du service Web&quot;

### Rétablissement de l’accès aux documents révoqués à l’aide de l’API du service Web {#reinstate-access-to-revoked-documents-using-the-web-service-api}

Rétablissement de l’accès à un document révoqué à l’aide de l’API Document Security (service Web) :

1. Incluez des fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Assurez-vous d’utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant les AEM Forms.

1. Créez un objet API Client de sécurité Document.

   * Create a `DocumentSecurityServiceClient` object by using its default constructor.
   * Create a `DocumentSecurityServiceClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/RightsManagementService?WSDL`). Vous n’avez pas besoin d’utiliser l’ `lc_version` attribut. Cet attribut est utilisé lorsque vous créez une référence de service.)
   * Créez un `System.ServiceModel.BasicHttpBinding` objet en obtenant la valeur du `DocumentSecurityServiceClient.Endpoint.Binding` champ. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le `System.ServiceModel.BasicHttpBinding` champ de l’ `MessageEncoding` objet sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en exécutant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.


1. Récupérez l’identifiant de licence du document PDF révoqué.

   * Créez un objet `BLOB` en utilisant son constructeur. L’ `BLOB` objet est utilisé pour stocker un document PDF révoqué auquel l’accès est rétabli.
   * Créez un `System.IO.FileStream` objet en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du fichier du document PDF révoqué et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’ `System.IO.FileStream` objet. Vous pouvez déterminer la taille du tableau d’octets en obtenant la `System.IO.FileStream` `Length` propriété de l’objet.
   * Renseignez le tableau d’octets avec les données de flux en appelant la `System.IO.FileStream` `Read` méthode de l’objet et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’ `BLOB` objet en affectant son `MTOM` champ au contenu du tableau d’octets.

1. Rétablit l’accès au document PDF révoqué.

   * Récupérez la valeur d’identifiant de licence du document révoqué en appelant la `DocumentSecurityServiceClient` méthode de l’ `getLicenseID` objet et en transmettant l’ `BLOB` objet qui représente le document révoqué. Cette méthode renvoie une valeur de chaîne qui représente l’identifiant de licence.
   * Rétablissez l’accès au document PDF révoqué en appelant la `DocumentSecurityServiceClient` méthode de l’objet et en transmettant une valeur de chaîne qui spécifie la valeur d’identifiant de licence du document PDF révoqué (transmettez la valeur renvoyée de la `unrevokeLicense` méthode de l’ `DocumentSecurityServiceClient` `getLicenseId` objet).

**Exemples de code**

Pour obtenir des exemples de code à l’aide du service Document Security, reportez-vous aux Débuts rapides suivants :

* &quot;Début rapide (MTOM) : Rétablissement de l’accès à un document révoqué à l’aide de l’API du service Web&quot;
* &quot;Quick Début (SwaRef) : Rétablissement de l’accès à un document révoqué à l’aide de l’API du service Web&quot;

**Voir également**

[Appel de AEM Forms à l’aide de MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Appel de AEM Forms à l’aide de SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Inspection des Documents PDF protégés par une stratégie {#inspecting-policy-protected-pdf-documents}

Vous pouvez utiliser l’API Document Security Service (Java et service Web) pour inspecter les documents PDF protégés par une stratégie. L’inspection des documents PDF protégés par une stratégie renvoie des informations sur le document PDF protégé par une stratégie. Vous pouvez, par exemple, déterminer la stratégie utilisée pour sécuriser le document et la date à laquelle le document a été sécurisé.

Vous ne pouvez pas effectuer cette tâche si votre version de LiveCycle est 8.x ou une version antérieure. La prise en charge de l’inspection des documents protégés par une stratégie est ajoutée en AEM Forms. Si vous tentez d’inspecter un document protégé par une stratégie à l’aide de LiveCycle 8.x (ou version antérieure), une exception est générée.

>[!NOTE]
>
>For more information about the Document Security service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary_of_steps-7}

Pour inspecter un document PDF protégé par une stratégie, procédez comme suit :

1. Incluez des fichiers de projet.
1. Créez un objet API Client de sécurité Document.
1. Récupérez un document protégé par une stratégie à inspecter.
1. Obtenez des informations sur le document protégé par une stratégie.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

**Création d’un objet API Client de sécurité Document**

Avant de pouvoir exécuter par programmation une opération du service Document Security, créez un objet client du service Document Security. Si vous utilisez l’API Java, créez un `RightsManagementClient` objet. Si vous utilisez l’API du service Web Document Security, créez un `RightsManagementServiceService` objet.

**Récupération d’un document protégé par une stratégie pour l’inspection**

Pour inspecter un document protégé par une stratégie, récupérez-le. Si vous tentez d’inspecter un document non sécurisé avec une stratégie ou révoqué, une exception est générée.

**Inspecter le document**

Après avoir récupéré un document protégé par une stratégie, vous pouvez l’inspecter.

**Obtention d’informations sur le document protégé par une stratégie**

Après avoir examiné un document PDF protégé par une stratégie, vous pouvez obtenir des informations à son sujet. Par exemple, vous pouvez déterminer la stratégie utilisée pour sécuriser le document.

Si vous sécurisez un document avec une stratégie qui appartient à Mes stratégies, puis que vous appelez `RMInspectResult.getPolicysetName` ou `RMInspectResult.getPolicysetId`, la valeur null est renvoyée.

Si le document est sécurisé à l’aide d’une stratégie contenue dans un jeu de stratégies (autre que Mes stratégies), `RMInspectResult.getPolicysetName` puis `RMInspectResult.getPolicysetId` renvoie des chaînes valides.

**Voir également**

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Inspecter les Documents PDF protégés par une stratégie à l’aide de l’API Java {#inspect-policy-protected-pdf-documents-using-the-java-api}

Inspectez un document PDF protégé par une stratégie à l’aide de l’API Document Security Service (Java) :

1. Incluez des fichiers de projet.

   Incluez des fichiers JAR client, tels que adobe-rightsmanagement-client.jar, dans le chemin de classe de votre projet Java. Pour plus d’informations sur l’emplacement de ces fichiers, voir [Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

1. Créez un objet API Client de sécurité Document.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion. (Voir [Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
   * Créez un objet `RightsManagementClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`. 

1. Récupérez un document protégé par une stratégie à inspecter.

   * Créez un `java.io.FileInputStream` objet représentant le document PDF protégé par une stratégie à l’aide de son constructeur. Transmettez une valeur de chaîne qui spécifie l’emplacement du document PDF.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Inspectez le document.

   * Créez un `DocumentManager` objet en appelant la `RightsManagementClient` méthode de l’ `getDocumentManager` objet.
   * Inspectez le document protégé par une stratégie en appelant la `LicenseManager` méthode de l’ `inspectDocument` objet. Transmettez l’ `com.adobe.idp.Document` objet contenant le document PDF protégé par une stratégie. Cette méthode renvoie un `RMInspectResult` objet contenant des informations sur le document protégé par une stratégie.

1. Obtenez des informations sur le document protégé par une stratégie.

   Pour obtenir des informations sur le document protégé par une stratégie, appelez la méthode appropriée qui appartient à `RMInspectResult` l’objet. Par exemple, pour récupérer le nom de la stratégie, appelez la `RMInspectResult` méthode de l’ `getPolicyName` objet.

**Exemples de code**

Pour obtenir des exemples de code à l’aide du service Document Security, reportez-vous aux Débuts rapides suivants :

* &quot;Début rapide (mode SOAP) : Contrôle des documents PDF protégés par une stratégie à l’aide de l’API Java&quot;

### Inspecter les Documents PDF protégés par une stratégie à l’aide de l’API du service Web {#inspect-policy-protected-pdf-documents-using-the-web-service-api}

Inspectez un document PDF protégé par une stratégie à l’aide de l’API Document Security Service (service Web) :

1. Incluez des fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Assurez-vous d’utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant les AEM Forms.

1. Créez un objet API Client de sécurité Document.

   * Create a `RightsManagementServiceClient` object by using its default constructor.
   * Create a `RightsManagementServiceClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/RightsManagementService?WSDL`). Vous n’avez pas besoin d’utiliser l’ `lc_version` attribut. Cet attribut est utilisé lorsque vous créez une référence de service.)
   * Créez un `System.ServiceModel.BasicHttpBinding` objet en obtenant la valeur du `RightsManagementServiceClient.Endpoint.Binding` champ. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le `System.ServiceModel.BasicHttpBinding` champ de l’ `MessageEncoding` objet sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en exécutant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.


1. Récupérez un document protégé par une stratégie à inspecter.

   * Créez un objet `BLOB` en utilisant son constructeur. L’ `BLOB` objet est utilisé pour stocker un document PDF à inspecter.
   * Create a `System.IO.FileStream` object by invoking its constructor. Transmettez une valeur de chaîne qui représente l’emplacement du fichier du document PDF et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’ `System.IO.FileStream` objet. Vous pouvez déterminer la taille du tableau d’octets en obtenant la `System.IO.FileStream` `Length` propriété de l’objet.
   * Renseignez le tableau d’octets avec les données de flux en appelant la `System.IO.FileStream` méthode de l’ `Read` objet. Passez le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’ `BLOB` objet en affectant son `MTOM` champ au contenu du tableau d’octets.

1. Inspectez le document.

   Inspectez le document protégé par une stratégie en appelant la `RightsManagementServiceClient` méthode de l’ `inspectDocument` objet. Transmettez l’ `BLOB` objet contenant le document PDF protégé par une stratégie. Cette méthode renvoie un `RMInspectResult` objet contenant des informations sur le document protégé par une stratégie.

1. Obtenez des informations sur le document protégé par une stratégie.

   Pour obtenir des informations sur le document protégé par une stratégie, obtenez la valeur du champ approprié qui appartient à l’ `RMInspectResult` objet. Par exemple, pour récupérer le nom de la stratégie, obtenez la valeur du `RMInspectResult` champ de l’ `policyName` objet.

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
>For more information about the Document Security service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary_of_steps-8}

Pour créer un filigrane, procédez comme suit :

1. Incluez des fichiers de projet.
1. Créez un objet API Client de sécurité Document.
1. Définissez les attributs des filigranes.
1. Enregistrez le filigrane auprès du service Document Security.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

**Création d’un objet API Client de sécurité Document**

Avant de pouvoir exécuter par programmation une opération du service Document Security, vous devez créer un objet client du service Document Security. Si vous utilisez l’API Java, créez un `RightsManagementClient` objet. Si vous utilisez l’API du service Web Document Security, créez un `RightsManagementServiceService` objet.

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
   <td><p>Si cette valeur est spécifiée, elle <code>WaterBackCmd:IS_SIZE_ENABLED</code> doit être présente et la valeur doit être vraie. Si cet attribut n’est pas spécifié, le comportement par défaut est adapté à la page.</p></td>
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
   <td><p>Indique le texte personnalisé d’un filigrane. Si cette valeur est présente, elle <code>WaterBackCmd:IS_CUSTOMTEXT_ENABLED</code> doit également être présente et définie sur true.</p></td>
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

   Include client JAR files, such as the `adobe-rightsmanagement-client.jar`, in your Java project’s class path.

1. Créez un objet API Client de sécurité Document.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `RightsManagementClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`. 

1. Définition des attributs du filigrane

   * Créez un `Watermark` objet en appelant la méthode `InfomodelObjectFactory` statique de l’ `createWatermark` objet. Cette méthode renvoie un `Watermark` objet.
   * Définissez l’attribut name du filigrane en appelant la `Watermark` `setName` méthode de l’objet et en transmettant une valeur de chaîne qui spécifie le nom de la stratégie.
   * Définissez l’attribut d’arrière-plan du filigrane en appelant la `Watermark` méthode de l’objet et en transmettant `setBackground` `true`. En définissant cet attribut, le filigrane apparaît à l’arrière-plan du document.
   * Définissez l’attribut de texte personnalisé du filigrane en appelant la `Watermark` `setCustomText` méthode de l’objet et en transmettant une valeur de chaîne qui représente le texte du filigrane.
   * Définissez l’attribut d’opacité du filigrane en appelant la `Watermark` `setOpacity` méthode de l’objet et en transmettant un entier spécifiant le niveau d’opacité. La valeur 100 indique que le filigrane est complètement opaque et la valeur 0 indique que le filigrane est complètement transparent.

1. Enregistrez le filigrane.

   * Créez un `WatermarkManager` objet en appelant la `RightsManagementClient` méthode de l’ `getWatermarkManager` objet. Cette méthode renvoie un `WatermarkManager` objet.
   * Enregistrez le filigrane en appelant la `WatermarkManager` méthode de l’ `registerWatermark` objet et en transmettant l’objet `Watermark` qui représente le filigrane à enregistrer. Cette méthode renvoie une valeur de chaîne qui représente la valeur d’identification du filigrane.

**Exemples de code**

Pour obtenir des exemples de code à l’aide du service Document Security, reportez-vous aux Débuts rapides suivants :

* &quot;Début rapide (mode SOAP) : Création d’un filigrane à l’aide de l’API Java&quot;

### Création de filigranes à l’aide de l’API du service Web {#create-watermarks-using-the-web-service-api}

Créez un filigrane à l’aide de l’API Document Security (service Web) :

1. Créez un objet API Client de sécurité Document.

   Créez un projet Microsoft .NET qui utilise MTOM. Assurez-vous d’utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant les AEM Forms.

1. Créez un objet API Client de sécurité Document.

   * Create a `RightsManagementServiceClient` object by using its default constructor.
   * Create a `RightsManagementServiceClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/RightsManagementService?WSDL`). Vous n’avez pas besoin d’utiliser l’ `lc_version` attribut. Cet attribut est utilisé lorsque vous créez une référence de service.)
   * Créez un `System.ServiceModel.BasicHttpBinding` objet en obtenant la valeur du `RightsManagementServiceClient.Endpoint.Binding` champ. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le `System.ServiceModel.BasicHttpBinding` champ de l’ `MessageEncoding` objet sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en exécutant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.


1. Définissez les attributs du filigrane.

   * Créez un `WatermarkSpec` objet en appelant le `WatermarkSpec` constructeur.
   * Définissez le nom du filigrane en attribuant une valeur de chaîne au membre `WatermarkSpec` de données de l’ `name` objet.
   * Définissez l’ `id` attribut du filigrane en attribuant une valeur de chaîne au membre `WatermarkSpec` de données de l’ `id` objet.
   * Pour chaque propriété de filigrane à définir, créez un `MyMapOf_xsd_string_To_xsd_anyType_Item` objet distinct.
   * Définissez la valeur de clé en attribuant une valeur au membre `MyMapOf_xsd_string_To_xsd_anyType_Item` de données de l’ `key` objet (par exemple `WaterBackCmd:OPACITY)`).
   * Définissez la valeur en attribuant une valeur au membre `MyMapOf_xsd_string_To_xsd_anyType_Item` de données de l’ `value` objet (par exemple `.25`).
   * Create a `MyArrayOf_xsd_anyType` object. Pour chaque `MyMapOf_xsd_string_To_xsd_anyType_Item` objet, appelez la `MyArrayOf_xsd_anyType` méthode de l’ `Add` objet. Pass the `MyMapOf_xsd_string_To_xsd_anyType_Item` object.
   * Affectez l’ `MyArrayOf_xsd_anyType` objet au membre `WatermarkSpec` de données de l’ `values` objet.

1. Enregistrez le filigrane.

   Enregistrez le filigrane en appelant la `RightsManagementServiceClient` méthode de l’ `registerWatermark` objet et en transmettant l’objet `WatermarkSpec` qui représente le filigrane à enregistrer.

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
>For more information about the Document Security service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

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

Avant de pouvoir exécuter par programmation une opération du service Document Security, vous devez créer un objet client du service Document Security. Si vous utilisez l’API Java, créez un `DocumentSecurityClient` objet. Si vous utilisez l’API du service Web Document Security, créez un `DocumentSecurityServiceService` objet.

**Récupérer le filigrane à modifier**

Pour modifier un filigrane, vous devez récupérer un filigrane existant. Vous pouvez récupérer un filigrane en spécifiant son nom ou en spécifiant sa valeur d’identificateur.

**Définition des attributs des filigranes**

Pour modifier un filigrane existant, modifiez la valeur d’un ou de plusieurs attributs de filigrane. Lors de la mise à jour programmée d’un filigrane à l’aide d’un service Web, vous devez définir tous les attributs définis à l’origine, même si la valeur ne change pas. Supposons, par exemple, que les attributs de filigrane suivants soient définis : `WaterBackCmd:IS_USERID_ENABLED`, `WaterBackCmd:IS_CUSTOMTEXT_ENABLED`, `WaterBackCmd:OPACITY`et `WaterBackCmd:SRCTEXT`. Bien que le seul attribut à modifier soit `WaterBackCmd:OPACITY`celui-ci, vous devez définir les autres valeurs qui conviennent.

>[!NOTE]
>
>Lorsque vous utilisez l’API Java pour modifier un filigrane, vous n’avez pas besoin de spécifier tous les attributs. Définissez l’attribut de filigrane à modifier.

>[!NOTE]
>
>Pour plus d’informations sur les noms d’attributs de filigrane, voir [Création de filigranes](protecting-documents-policies.md#creating-watermarks).

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

   Créez un `WatermarkManager` objet en appelant la `DocumentSecurityClient` méthode de l’ `getWatermarkManager` objet et en transmettant une valeur de chaîne qui spécifie le nom du filigrane. Cette méthode renvoie un objet `Watermark` qui représente le filigrane à modifier.

1. Définissez les attributs du filigrane.

   Définissez l’attribut d’opacité du filigrane en appelant la `Watermark` `setOpacity` méthode de l’objet et en transmettant un entier spécifiant le niveau d’opacité. La valeur 100 indique que le filigrane est complètement opaque et la valeur 0 indique que le filigrane est complètement transparent.

   >[!NOTE]
   >
   >Cet exemple ne modifie que l&#39;attribut d&#39;opacité.

1. Mettez à jour le filigrane.

   * Mettez à jour le filigrane en appelant la `WatermarkManager` méthode de l’ `updateWatermark` objet et en transmettant l’ `Watermark` objet dont l’attribut a été modifié.

**Exemples de code**

Pour obtenir des exemples de code à l’aide du service Document Security, voir le Début rapide (mode SOAP) : Modification d’un filigrane à l’aide de la section API Java.

### Modification des filigranes à l’aide de l’API du service Web {#modify-watermarks-using-the-web-service-api}

Modifiez un filigrane à l’aide de l’API Document Security (service Web) :

1. Incluez des fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Assurez-vous d’utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant les AEM Forms.

1. Créez un objet API Client de sécurité Document.

   * Create a `DocumentSecurityServiceClient` object by using its default constructor.
   * Create a `RightsManagementServiceClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/DocumentSecurityService?WSDL`). Vous n’avez pas besoin d’utiliser l’ `lc_version` attribut. Cet attribut est utilisé lorsque vous créez une référence de service.)
   * Créez un `System.ServiceModel.BasicHttpBinding` objet en obtenant la valeur du `DocumentSecurityServiceClient.Endpoint.Binding` champ. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le `System.ServiceModel.BasicHttpBinding` champ de l’ `MessageEncoding` objet sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en exécutant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.


1. Récupérez le filigrane à modifier.

   Récupérez le filigrane à modifier en appelant la `DocumentSecurityServiceClient` `getWatermarkByName` méthode de l’objet. Transmettez une valeur de chaîne qui spécifie le nom du filigrane. Cette méthode renvoie un objet `WatermarkSpec` qui représente le filigrane à modifier.

1. Définissez les attributs du filigrane.

   * Pour chaque propriété de filigrane à mettre à jour, créez un `MyMapOf_xsd_string_To_xsd_anyType_Item` objet distinct.
   * Définissez la valeur de clé en attribuant une valeur au membre `MyMapOf_xsd_string_To_xsd_anyType_Item` de données de l’ `key` objet (par exemple `WaterBackCmd:OPACITY)`).
   * Définissez la valeur en attribuant une valeur au membre `MyMapOf_xsd_string_To_xsd_anyType_Item` de données de l’ `value` objet (par exemple `.50`).
   * Create a `MyArrayOf_xsd_anyType` object. Pour chaque `MyMapOf_xsd_string_To_xsd_anyType_Item` objet, appelez la `MyArrayOf_xsd_anyType` méthode de l’ `Add` objet. Pass the `MyMapOf_xsd_string_To_xsd_anyType_Item` object.
   * Affectez l’ `MyArrayOf_xsd_anyType` objet au membre `WatermarkSpec` de données de l’ `values` objet.

1. Mettez à jour le filigrane.

   Mettez à jour le filigrane en appelant la `DocumentSecurityServiceClient` méthode de l’ `updateWatermark` objet et en transmettant l’objet `WatermarkSpec` qui représente le filigrane à modifier.

**Exemples de code**

Pour obtenir des exemples de code à l’aide du service Document Security, reportez-vous au Début rapide suivant :

* &quot;Début rapide (MTOM) : Modification d’un filigrane à l’aide de l’API du service Web&quot;

## Recherche de Événements {#searching-for-events}

Le service Rights Management effectue le suivi des actions spécifiques à mesure qu’elles se produisent, telles que l’application d’une stratégie à un document, l’ouverture d’un document protégé par une stratégie et la révocation de l’accès aux documents. Le contrôle des Événements doit être activé pour le service Rights Management ou les événements ne sont pas suivis.

Les Événements tombent dans l’une des catégories suivantes :

* Les événements d’administrateur sont des actions liées à un administrateur, telles que la création d’un nouveau compte d’administrateur.
* Les événements de Document sont des actions liées à un document, telles que la fermeture d’un document protégé par une stratégie.
* Les événements de stratégie sont des actions liées à une stratégie, telles que la création d’une nouvelle stratégie.
* Les événements de service sont des actions liées au service Rights Management, telles que la synchronisation avec l’annuaire d’utilisateurs.

Vous pouvez rechercher des événements spécifiques à l’aide de l’API Java de Rights Management ou de l’API de service Web. En recherchant des événements, vous pouvez effectuer des tâches, comme la création d’un fichier journal de certains événements.

>[!NOTE]
>
>For more information about the Rights Management service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary_of_steps-10}

Pour rechercher un événement Rights Management, procédez comme suit :

1. Incluez des fichiers de projet.
1. Créez un objet API Client Rights Management.
1. Indiquez le événement pour lequel effectuer la recherche.
1. Recherchez le événement.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

**Création d’un objet API Client Rights Management**

Avant de pouvoir exécuter une opération de service Rights Management par programmation, vous devez créer un objet client de service Rights Management. Si vous utilisez l’API Java, créez un `DocumentSecurityClient` objet. Si vous utilisez l’API du service Web Rights Management, créez un `DocumentSecurityServiceService` objet.

**Spécifiez les événements à rechercher**

Vous devez spécifier le événement à rechercher. Vous pouvez, par exemple, rechercher le événement de création de la stratégie, qui se produit lors de la création d’une nouvelle stratégie.

**Rechercher le événement**

Après avoir spécifié le événement à rechercher, vous pouvez utiliser l’API Java de Rights Management ou l’API du service Web Rights Management pour rechercher le événement.

**Voir également**

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Rechercher des événements à l’aide de l’API Java {#search-for-events-using-the-java-api}

Recherchez des événements à l’aide de l’API Rights Management (Java) :

1. Inclure les fichiers de projet

   Incluez des fichiers JAR client, tels que adobe-rightsmanagement-client.jar, dans le chemin de classe de votre projet Java.

1. Création d’un objet API Client Rights Management

   Créez un `DocumentSecurityClient` objet en utilisant son constructeur et en transmettant un `ServiceClientFactory` objet contenant des propriétés de connexion.

1. Spécifiez les événements à rechercher

   * Créez un `EventManager` objet en appelant la `DocumentSecurityClient` méthode de l’ `getEventManager` objet. Cette méthode renvoie un `EventManager` objet.
   * Créez un `EventSearchFilter` objet en appelant son constructeur.
   * Spécifiez le événement pour lequel effectuer la recherche en appelant la `EventSearchFilter` méthode de l’ `setEventCode` objet et en transmettant un membre de données statique appartenant à la `EventManager` classe qui représente le événement pour lequel effectuer la recherche. Par exemple, pour rechercher le événement de création de stratégie, transmettez `EventManager.POLICY_CREATE_EVENT`.

   >[!NOTE]
   >
   >Vous pouvez définir d&#39;autres critères de recherche en appelant des méthodes `EventSearchFilter` d&#39;objet. Par exemple, appelez la `setUserName` méthode pour spécifier un utilisateur associé au événement.

1. Rechercher le événement

   Recherchez le événement en appelant la `EventManager` méthode de l’ `searchForEvents` objet et en transmettant l’ `EventSearchFilter` objet qui définit les critères de recherche du événement. Cette méthode renvoie un tableau d&#39; `Event` objets.

**Exemples de code**

Pour obtenir des exemples de code à l’aide du service Rights Management, voir les Débuts rapides suivants :

* &quot;Début rapide (SOAP) : Recherche de événements à l’aide de l’API Java&quot;

### Rechercher des événements à l’aide de l’API du service Web {#search-for-events-using-the-web-service-api}

Recherchez des événements à l’aide de l’API Rights Management (service Web) :

1. Inclure les fichiers de projet

   Créez un projet Microsoft .NET qui utilise MTOM. Assurez-vous d’utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant les AEM Forms.

1. Création d’un objet API Client Rights Management

   * Create a `DocumentSecurityServiceClient` object by using its default constructor.
   * Create a `DocumentSecurityServiceClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/RightsManagementService?WSDL`). Vous n’avez pas besoin d’utiliser l’ `lc_version` attribut. Cet attribut est utilisé lorsque vous créez une référence de service.)
   * Créez un `System.ServiceModel.BasicHttpBinding` objet en obtenant la valeur du `DocumentSecurityServiceClient.Endpoint.Binding` champ. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le `System.ServiceModel.BasicHttpBinding` champ de l’ `MessageEncoding` objet sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en exécutant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.


1. Spécifiez les événements à rechercher

   * Create an `EventSpec` object by using its constructor.
   * Spécifiez le début de la période au cours de laquelle le événement s’est produit en définissant le membre `EventSpec` de données de l’objet avec `firstTime.date` `DataTime` une instance qui représente le début de la période au cours de laquelle le événement s’est produit.
   * Affectez la valeur `true` au membre `EventSpec` de données de l’ `firstTime.dateSpecified` objet.
   * Spécifiez la fin de la période au cours de laquelle le événement s’est produit en définissant le membre `EventSpec` de données de l’objet avec `lastTime.date` `DataTime` une instance représentant la fin de la période au cours de laquelle le événement s’est produit.
   * Affectez la valeur `true` au membre `EventSpec` de données de l’ `lastTime.dateSpecified` objet.
   * Définissez le événement à rechercher en attribuant une valeur de chaîne au membre `EventSpec` de données de l’ `eventCode` objet. Le tableau suivant liste les valeurs numériques que vous pouvez affecter à cette propriété :

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
    <td><p>4000</p></td>
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
    <td><p>7000</p></td>
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

   Recherchez le événement en appelant la `DocumentSecurityServiceClient` méthode de l’ `searchForEvents` objet et en transmettant l’ `EventSpec` objet qui représente le événement pour lequel effectuer la recherche et le nombre maximal de résultats. Cette méthode renvoie une `MyArrayOf_xsd_anyType` collection dans laquelle chaque élément est une `AuditSpec` instance. A l’aide d’une `AuditSpec` instance, vous pouvez obtenir des informations sur le événement, telles que l’heure à laquelle il s’est produit. L&#39; `AuditSpec` instance contient un membre `timestamp` de données qui spécifie ces informations.

**Exemples de code**

Pour obtenir des exemples de code à l’aide du service Rights Management, voir les Débuts rapides suivants :

* &quot;Début rapide (MTOM) : Recherche de événements à l’aide de l’API du service Web&quot;
* &quot;Quick Début (SwaRef) : Recherche de événements à l’aide de l’API du service Web&quot;

**Voir également**

[Appel de AEM Forms à l’aide de MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Appel de AEM Forms à l’aide de SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Application de stratégies à des Documents Word {#applying-policies-to-word-documents}

Outre les documents PDF, le service Rights Management prend en charge d’autres formats de document, tels qu’un document Microsoft Word (DOC) et d’autres formats de fichier Microsoft Office. Par exemple, vous pouvez appliquer une stratégie à un document Word afin de la sécuriser. En appliquant une stratégie à un document Word, vous restreignez l’accès au document. Vous ne pouvez pas appliquer une stratégie à un document si le document est déjà sécurisé avec une stratégie.

Vous pouvez contrôler l’utilisation d’un document Word protégé par une stratégie après l’avoir distribué. C&#39;est-à-dire, vous pouvez voir comment le document est utilisé et qui l&#39;utilise. Par exemple, vous pouvez savoir quand quelqu’un a ouvert le document.

>[!NOTE]
>
>For more information about the Document Security service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

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

### Application d’une stratégie à un document Word à l’aide de l’API Java {#apply-a-policy-to-a-word-document-using-the-java-api}

Appliquez une stratégie à un document Word à l’aide de l’API Document Security (Java) :

1. Incluez des fichiers de projet.

   Incluez des fichiers JAR client, tels que adobe-rightsmanagement-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un objet API Client de sécurité Document.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `DocumentSecurityClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`. 

1. Récupérez un document Word.

   * Créez un `java.io.FileInputStream` objet qui représente le document Word en utilisant son constructeur et en transmettant une valeur de chaîne qui spécifie l&#39;emplacement du document Word.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Appliquez une stratégie existante au document Word.

   * Créez un `DocumentManager` objet en appelant la `DocumentSecurityClient` méthode de l’ `getDocumentManager` objet.
   * Appliquez une stratégie au document Word en appelant la `DocumentManager` `protectDocument` méthode de l’objet et en transmettant les valeurs suivantes :

      * Objet `com.adobe.idp.Document` contenant le document Word auquel la stratégie est appliquée.
      * Valeur de chaîne qui spécifie le nom du document.
      * Valeur de chaîne qui spécifie le nom du jeu de stratégies auquel appartient la stratégie. Vous pouvez spécifier une `null` valeur qui entraîne l’utilisation du jeu de `MyPolicies` stratégies.
      * Valeur de chaîne qui spécifie le nom de la stratégie.
      * Valeur de chaîne qui représente le nom du domaine du gestionnaire d’utilisateurs de l’utilisateur qui est l’éditeur du document. Cette valeur de paramètre est facultative et peut être nulle (si ce paramètre est nul, la valeur de paramètre suivante doit être nulle).
      * Valeur de chaîne qui représente le nom canonique de l’utilisateur du gestionnaire d’utilisateurs qui est l’éditeur du document. Cette valeur de paramètre est facultative et peut être `null` (si ce paramètre est `null`, la valeur de paramètre précédente doit être `null`).
      * Un paramètre `com.adobe.livecycle.rightsmanagement.Locale` qui représente le paramètre régional utilisé pour sélectionner le modèle MS Office. Cette valeur de paramètre est facultative et vous pouvez spécifier `null`.

      La `protectDocument` méthode renvoie un `RMSecureDocumentResult` objet qui contient le document Word protégé par une stratégie.


1. Enregistrez le document Word.

   * Appelez la méthode `RMSecureDocumentResult` de l’objet `getProtectedDoc` pour obtenir le document Word protégé par une stratégie. Cette méthode renvoie un `com.adobe.idp.Document` objet.
   * Create a `java.io.File` object and ensure that the file extension is DOC.
   * Appelez la `com.adobe.idp.Document` méthode de l’ `copyToFile` objet pour copier le contenu de l’ `Document` objet dans le fichier (veillez à utiliser l’ `Document` objet renvoyé par la `getProtectedDoc` méthode).

**Exemples de code**

Pour obtenir des exemples de code à l’aide du service Document Security, reportez-vous au Début rapide suivant :

* &quot;Début rapide (mode SOAP) : Application d’une stratégie à un document Word à l’aide de l’API Java&quot;

### Application d’une stratégie à un document Word à l’aide de l’API du service Web {#apply-a-policy-to-a-word-document-using-the-web-service-api}

Appliquez une stratégie à un document Word à l’aide de l’API Document Security (service Web) :

1. Incluez des fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Assurez-vous d’utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/DocumentSecurityService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant les AEM Forms.

1. Créez un objet API Client de sécurité Document.

   * Create a `DocumentSecurityServiceClient` object by using its default constructor.
   * Create a `DocumentSecurityServiceClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/DocumentSecurityService?WSDL`). Vous n’avez pas besoin d’utiliser l’ `lc_version` attribut. Cet attribut est utilisé lorsque vous créez une référence de service.)
   * Créez un `System.ServiceModel.BasicHttpBinding` objet en obtenant la valeur du `DocumentSecurityServiceClient.Endpoint.Binding` champ. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le `System.ServiceModel.BasicHttpBinding` champ de l’ `MessageEncoding` objet sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en exécutant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.


1. Récupérez un document Word.

   * Créez un objet `BLOB` en utilisant son constructeur. L’ `BLOB` objet est utilisé pour stocker un document Word auquel une stratégie est appliquée.
   * Créez un `System.IO.FileStream` objet en appelant son constructeur et en transmettant une valeur de chaîne qui représente l&#39;emplacement du fichier du document Word et le mode d&#39;ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’ `System.IO.FileStream` objet. Déterminez la taille du tableau d’octets en obtenant la `System.IO.FileStream` `Length` propriété de l’objet.
   * Renseignez le tableau d’octets avec les données de flux en appelant la `System.IO.FileStream` méthode de l’ `Read` objet. Passez le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’ `BLOB` objet en affectant son `MTOM` champ au contenu du tableau d’octets.

1. Appliquez une stratégie existante au document Word.

   Appliquez une stratégie au document Word en appelant la `DocumentSecurityServiceClient` `protectDocument` méthode de l’objet et en transmettant les valeurs suivantes :

   * Objet `BLOB` contenant le document Word auquel la stratégie est appliquée.
   * Valeur de chaîne qui spécifie le nom du document.
   * Valeur de chaîne qui spécifie le nom du jeu de stratégies auquel appartient la stratégie. Vous pouvez spécifier une `null` valeur qui entraîne l’utilisation du jeu de `MyPolicies` stratégies.
   * Valeur de chaîne qui spécifie le nom de la stratégie.
   * Valeur de chaîne qui représente le nom du domaine du gestionnaire d’utilisateurs de l’utilisateur qui est l’éditeur du document. Cette valeur de paramètre est facultative et peut être nulle (si ce paramètre est nul, la valeur de paramètre suivante doit être `null`).
   * Valeur de chaîne qui représente le nom canonique de l’utilisateur du gestionnaire d’utilisateurs qui est l’éditeur du document. Cette valeur de paramètre est facultative et peut être nulle (si ce paramètre est nul, la valeur de paramètre précédente doit être `null`).
   * Valeur `RMLocale` spécifiant la valeur du paramètre régional (par exemple, `RMLocale.en`).
   * Paramètre de sortie de chaîne utilisé pour stocker la valeur de l’identifiant de stratégie.
   * Paramètre de sortie de chaîne utilisé pour stocker la valeur d’identificateur protégée par une stratégie.
   * Paramètre de sortie de chaîne utilisé pour stocker le type MIME (par exemple, `application/doc`).

   La `protectDocument` méthode renvoie un `BLOB` objet qui contient le document Word protégé par une stratégie.

1. Enregistrez le document Word.

   * Créez un `System.IO.FileStream` objet en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du fichier du document Word protégé par une stratégie.
   * Créez un tableau d’octets qui stocke le contenu des données de l’ `BLOB` objet renvoyé par la `protectDocument` méthode. Renseignez le tableau d’octets en obtenant la valeur du membre `BLOB` de données de l’ `MTOM` objet.
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * Ecrivez le contenu du tableau d’octets dans un fichier Word en appelant la méthode `System.IO.BinaryWriter` `Write` de l’objet et en transmettant le tableau d’octets.

**Exemples de code**

Pour obtenir des exemples de code à l’aide du service Document Security, reportez-vous au Début rapide suivant :

* &quot;Début rapide (MTOM) : Application d’une stratégie à un document Word à l’aide de l’API du service Web&quot;

## Suppression de stratégies des Documents Word {#removing-policies-from-word-documents}

Vous pouvez supprimer une stratégie d’un document Word protégé par une stratégie afin de supprimer la sécurité du document. Autrement dit, si vous ne voulez plus que le document soit protégé par une politique. Si vous souhaitez mettre à jour un document Word protégé par une stratégie avec une nouvelle stratégie, il est plus efficace de changer de stratégie au lieu de la supprimer et d’ajouter la stratégie mise à jour.

>[!NOTE]
>
>For more information about the Document Security service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

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

Vous pouvez supprimer une stratégie d’un document Word protégé par une stratégie, à condition qu’un administrateur soit spécifié dans les paramètres de connexion. Dans le cas contraire, la stratégie utilisée pour sécuriser un document doit contenir l’ `SWITCH_POLICY` autorisation afin de supprimer une stratégie d’un document Word. En outre, l’utilisateur spécifié dans les paramètres de connexion AEM Forms doit également disposer de cette autorisation. Dans le cas contraire, une exception est générée.

**Enregistrer le document Word non sécurisé**

Une fois que le service Document Security a supprimé une stratégie d&#39;un document Word, vous pouvez enregistrer le document Word non sécurisé en tant que fichier DOC.

**Voir également**

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Application de stratégies à des Documents Word](protecting-documents-policies.md#applying-policies-to-word-documents)

### Suppression d’une stratégie d’un document Word à l’aide de l’API Java {#remove-a-policy-from-a-word-document-using-the-java-api}

Supprimez une stratégie d’un document Word protégé par une stratégie à l’aide de l’API Document Security (Java) :

1. Inclure les fichiers de projet

   Incluez des fichiers JAR client, tels que adobe-rightsmanagement-client.jar, dans le chemin de classe de votre projet Java.

1. Création d’un objet API Client de sécurité Document

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `RightsManagementClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`. 

1. Récupération d’un document Word protégé par une stratégie

   * Créez un `java.io.FileInputStream` objet qui représente le document Word protégé par une stratégie en utilisant son constructeur et en transmettant une valeur de chaîne qui spécifie l&#39;emplacement du document Word.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Supprimer la stratégie du document Word

   * Créez un `DocumentManager` objet en appelant la `RightsManagementClient` méthode de l’ `getDocumentManager` objet.
   * Supprimez une stratégie du document Word en appelant la `DocumentManager` méthode de l’objet et en transmettant l’ `removeSecurity` `com.adobe.idp.Document` objet contenant le document Word protégé par une stratégie. Cette méthode renvoie un `com.adobe.idp.Document` objet contenant un document Word non sécurisé.

1. Enregistrer le document Word non sécurisé

   * Create a `java.io.File` object and ensure that the file extension is DOC.
   * Appelez la `Document` méthode de l’ `copyToFile` objet pour copier le contenu de l’ `Document` objet dans le fichier (veillez à utiliser l’ `Document` objet renvoyé par la `removeSecurity` méthode).

**Exemples de code**

Pour obtenir des exemples de code à l’aide du service Document Security, reportez-vous au Début rapide suivant :

* &quot;Début rapide (mode SOAP) : Suppression d’une stratégie d’un document Word à l’aide de l’API Java&quot;

### Suppression d’une stratégie d’un document Word à l’aide de l’API du service Web {#remove-a-policy-from-a-word-document-using-the-web-service-api}

Supprimez une stratégie d’un document Word protégé par une stratégie à l’aide de l’API Document Security (service Web) :

1. Inclure les fichiers de projet

   Créez un projet Microsoft .NET qui utilise MTOM. Assurez-vous d’utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant les AEM Forms.

1. Création d’un objet API Client de sécurité Document

   * Create a `RightsManagementServiceClient` object by using its default constructor.
   * Create a `RightsManagementServiceClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/RightsManagementService?WSDL`). Vous n’avez pas besoin d’utiliser l’ `lc_version` attribut. Cet attribut est utilisé lorsque vous créez une référence de service.)
   * Créez un `System.ServiceModel.BasicHttpBinding` objet en obtenant la valeur du `RightsManagementServiceClient.Endpoint.Binding` champ. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le `System.ServiceModel.BasicHttpBinding` champ de l’ `MessageEncoding` objet sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en exécutant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.


1. Récupération d’un document Word protégé par une stratégie

   * Créez un objet `BLOB` en utilisant son constructeur. L’ `BLOB` objet est utilisé pour stocker le document Word protégé par une stratégie à partir duquel la stratégie est supprimée.
   * Créez un `System.IO.FileStream` objet en appelant son constructeur et en transmettant une valeur de chaîne qui représente l&#39;emplacement du fichier du document Word et le mode d&#39;ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’ `System.IO.FileStream` objet. Vous pouvez déterminer la taille du tableau d’octets en obtenant la `System.IO.FileStream` `Length` propriété de l’objet.
   * Renseignez le tableau d’octets avec les données de flux en appelant la `System.IO.FileStream` `Read` méthode de l’objet et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’ `BLOB` objet en affectant son `MTOM` champ au contenu du tableau d’octets.

1. Supprimer la stratégie du document Word

   Supprimez la stratégie du document Word en appelant la `RightsManagementServiceClient` méthode de l’objet et en transmettant l’ `removePolicySecurity` `BLOB` objet contenant le document Word protégé par une stratégie. Cette méthode renvoie un `BLOB` objet contenant un document Word non sécurisé.

1. Enregistrer le document Word non sécurisé

   * Créez un `System.IO.FileStream` objet en appelant son constructeur et en transmettant une valeur de chaîne qui représente l&#39;emplacement du fichier du document Word non sécurisé.
   * Créez un tableau d’octets qui stocke le contenu des données de l’ `BLOB` objet renvoyé par la `removePolicySecurity` méthode. Renseignez le tableau d’octets en obtenant la valeur du `BLOB` champ de l’ `MTOM` objet.
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.

**Exemples de code**

Pour obtenir des exemples de code à l’aide du service Document Security, reportez-vous au Début rapide suivant :

* &quot;Début rapide (MTOM) : Suppression d’une stratégie d’un document Word à l’aide de l’API du service Web&quot;

**Voir également**

[Appel de AEM Forms à l’aide de MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
