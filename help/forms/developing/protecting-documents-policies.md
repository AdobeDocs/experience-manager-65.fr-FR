---
title: Protéger des documents à lʼaide de politiques
description: Utilisez le service Document Security pour appliquer de manière dynamique les paramètres de confidentialité aux documents Adobe PDF et pour conserver le contrôle sur les documents. Le service Document Security permet également aux utilisateurs de contrôler la manière dont les destinataires utilisent le document PDF protégé par une politique.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: ff42579e-6aaf-433d-8b5d-9e9dd0957250
source-git-commit: 38f0496d9340fbcf383a2d39dba8efcbdcd20c6f
workflow-type: tm+mt
source-wordcount: '15464'
ht-degree: 82%

---

# Protéger des documents à lʼaide de politiques {#protecting-documents-with-policies}

**Les exemples et les échantillons de ce document sont réservés à l’environnement AEM Forms sur JEE.**

**À propos du service Document Security**

Le service Document Security permet aux utilisateurs d’appliquer de manière dynamique des paramètres de confidentialité aux documents Adobe PDF et de garder le contrôle sur ces documents, quelle que soit leur diffusion.

Le service Document Security empêche la diffusion des informations au-delà de la portée de l’utilisateur en permettant aux utilisateurs de garder un contrôle sur la manière dont les destinataires utilisent le document de PDF protégé par une stratégie. Un utilisateur peut spécifier les personnes autorisées à ouvrir un document, limiter son utilisation et le surveiller après distribution. Un utilisateur peut également contrôler de manière dynamique l’accès à un document protégé par une politique et même révoquer dynamiquement l’accès au document.

Le service Document Security protège également d’autres types de fichiers tels que les fichiers Microsoft Word (fichiers DOC). Vous pouvez utiliser l’API client Document Security pour utiliser ces types de fichiers. Les versions ci-dessous sont prises en charge :

* Fichiers Microsoft Office 2003 (fichiers DOC, XLS, PPT)
* Fichiers Microsoft Office 2007 (fichiers DOCX, XLSX, PPTX)
* Fichiers PTC Pro/E

Pour plus dʼinformations, les deux sections suivantes expliquent comment utiliser les documents Word :

* [Appliquer des politiques à des documents Word](protecting-documents-policies.md#applying-policies-to-word-documents)
* [Supprimer des politiques de documents Word](protecting-documents-policies.md#removing-policies-from-word-documents)

Les tâches suivantes peuvent être accomplies à l’aide du service Document Security :

* Créer des politiques. Pour plus d’informations, consultez la section [Créer des politiques](protecting-documents-policies.md#creating-policies).
* Modifier des politiques. Pour plus d’informations, consultez la section [Modifier des politiques](protecting-documents-policies.md#modifying-policies).
* Supprimer des politiques. Pour plus d’informations, consultez la section [Supprimer des politiques](protecting-documents-policies.md#deleting-policies).
* Appliquer des politiques à des documents PDF. Pour plus d’informations, consultez la section [Appliquer des politiques à des documents PDF](protecting-documents-policies.md#applying-policies-to-pdf-documents).
* Supprimer des politiques de documents PDF. Pour plus d’informations, consultez la section [Supprimer des politiques de documents PDF](protecting-documents-policies.md#removing-policies-from-pdf-documents).
* Inspecter des documents protégés par une politique. Pour plus d’informations, consultez la section [Inspecter des documents PDF protégés par une politique](protecting-documents-policies.md#inspecting-policy-protected-pdf-documents).
* Révoquer l’accès aux documents PDF. Pour plus d’informations, consultez la section [Révoquer l’accès aux documents](protecting-documents-policies.md#revoking-access-to-documents).
* Rétablir l’accès aux documents révoqués. Pour plus d’informations, consultez la section [Rétablir l’accès aux documents révoqués](protecting-documents-policies.md#reinstating-access-to-revoked-documents).
* Créer des filigranes. Pour plus d’informations, consultez la section [Créer des filigranes](protecting-documents-policies.md#creating-watermarks).
* Rechercher des événements. Pour plus d’informations, consultez la section [Rechercher des événements](protecting-documents-policies.md#searching-for-events).

>[!NOTE]
>
>Pour plus d’informations sur le service Document Security, consultez la section [Références des services pour AEM Forms](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

## Créer des politiques {#creating-policies}

Vous pouvez créer des politiques par programmation à l’aide de l’API Java Document Security ou de l’API de service web. Une *politique* est un ensemble d’informations qui comprend les paramètres de Document Security, les utilisateurs autorisés et les droits d’utilisation. Vous pouvez créer et enregistrer un nombre illimité de politiques à l’aide des paramètres de sécurité appropriés pour différents utilisateurs et situations.

Les politiques vous permettent d’effectuer les tâches suivantes :

* Indiquez les personnes autorisées à ouvrir le document. Les destinataires peuvent être internes ou externes à votre organisation.
* Indiquez comment les destinataires peuvent utiliser le document. Vous pouvez restreindre l’accès à différentes fonctionnalités d’Acrobat et d’Adobe Reader. Ces fonctionnalités permettent d’imprimer et de copier du texte et d’ajouter des signatures ou des commentaires à un document.
* Modifiez à tout moment les paramètres d’accès et de sécurité, même après la distribution du document protégé par une politique.
* Surveillez l’utilisation du document après sa distribution. Vous pouvez voir comment le document est utilisé et qui l’utilise. Par exemple, vous pouvez savoir quand quelqu’un a ouvert le document.

### Créer une politique à l’aide de services web {#creating-a-policy-using-web-services}

Lors de la création d’une politique à l’aide de l’API de service web, référencez un fichier XML Portable Document Rights Language (PDRL) existant qui décrit la politique. Les autorisations de politique et le mandant sont définis dans le document PDRL. Le document XML suivant est un exemple de document PDRL.

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
>Pour plus d’informations sur le service Document Security, voir [Référence des services pour AEM Forms](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

### Résumé des étapes {#summary-of-steps}

Pour créer une politique, procédez comme suit :

1. Incluez les fichiers de projet.
1. Créez un objet API client Document Security.
1. Définissez les attributs de la stratégie.
1. Créez une entrée de politique.
1. Enregistrez la politique.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services web, veillez à inclure les fichiers proxy.

Les fichiers JAR suivants doivent être ajoutés au chemin d’accès aux classes de votre projet :

* adobe-rightsmanagement-client.jar
* namespace.jar (si AEM Forms est déployé sur JBoss)
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

Pour plus d’informations à propos de l’emplacement de ces fichiers JAR, voir [Inclure des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Créer un objet API client Document Security**

Avant d’effectuer par programmation une opération de service Document Security, créez un objet client de service Document Security.

**Définition des attributs de la stratégie**

Pour créer une politique, définissez des attributs de politique. Un attribut obligatoire est le nom de la politique. Les noms des politiques doivent être uniques pour chaque jeu de politiques. Un jeu de politiques est simplement un ensemble de politiques. Deux politiques peuvent porter le même nom si elles appartiennent à des jeux de politiques distincts. Toutefois, deux politiques d’un seul jeu ne peuvent pas avoir le même nom de politique.

La période de validité est un autre attribut utile à définir. Une période de validité est la période pendant laquelle un document protégé par une politique est accessible aux destinataires autorisés. Si vous ne définissez pas cet attribut, la politique est toujours valide.

Une période de validité peut être définie sur l’une des options suivantes :

* Nombre défini de jours pendant lesquels le document est accessible à partir de l’heure de publication du document.
* Date de fin après laquelle le document n’est plus accessible.
* Période spécifique pour laquelle le document est accessible.
* Toujours valide

Vous pouvez spécifier uniquement une date de début, ce qui entraîne la validité de la politique après la date de début. Si vous indiquez uniquement une date de fin, la politique est valide jusqu’à la date de fin. Cependant, une exception est générée si aucune date de début et date de fin n’est définie.

Lors de la définition d’attributs appartenant à une politique, vous pouvez également définir des paramètres de chiffrement. Ces paramètres de chiffrement prennent effet lorsque la politique est appliquée à un document. Vous pouvez spécifier les valeurs de chiffrement suivantes :

* **AES256** : représente l’algorithme de chiffrement AES avec une clé de 256 bits.
* **AES128** : représente l’algorithme de chiffrement AES avec une clé de 128 bits.
* **Aucun chiffrement :** représente aucun chiffrement.

Lors de la spécification de l’option `NoEncryption`, vous ne pouvez pas définir l’option `PlaintextMetadata` à `false`. Si vous tentez de le faire, une exception est générée.

>[!NOTE]
>
>Pour plus d’informations sur les autres attributs que vous pouvez définir, voir la description de l’interface `Policy` dans [Référence de l’API AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Créer un jeu de politiques**

Une entrée de politique associe des entités, qui sont des groupes et des utilisateurs, ainsi que des autorisations à une politique. Une politique doit comporter au moins une entrée de politique. Supposons, par exemple, que vous effectuez les tâches suivantes :

* Créez et enregistrez une entrée de politique qui permet à un groupe d’afficher uniquement un document en ligne et interdit aux destinataires de le copier.
* Associez l’entrée de politique à la politique.
* Sécurisez un document avec la politique à l’aide d’Acrobat.

Grâce à ces actions, les destinataires ne peuvent consulter le document qu’en ligne et ne peuvent pas le copier. Le document reste sécurisé jusqu’à ce que la sécurité soit supprimée.

**Enregistrer la politique**

Une nouvelle politique doit être enregistrée avant de pouvoir être utilisée. Après avoir enregistré une politique, vous pouvez l’utiliser pour protéger les documents.

### Créer une politique à l’aide de l’API Java {#create-a-policy-using-the-java-api}

Créez une politique à l’aide de l’API Document Security (Java) :

1. Incluez les fichiers de projet.

   Incluez les fichiers JAR client, tels que adobe-rightsmanagement-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un objet API client Document Security.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `DocumentSecurityClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`. 

1. Définissez les attributs de la stratégie.

   * Créez un `Policy` en appelant la méthode `InfomodelObjectFactory` statique de l’objet `createPolicy` . Cette méthode renvoie un objet `Policy`.
   * Définissez l’attribut name de la stratégie en appelant la variable `Policy` de `setName` et transmission d’une valeur string qui spécifie le nom de la stratégie.
   * Définissez la description de la stratégie en appelant la fonction `Policy` de `setDescription` et transmission d’une valeur string qui spécifie la description de la stratégie.
   * Spécifiez le jeu de stratégies auquel appartient la nouvelle stratégie en appelant la fonction `Policy` de `setPolicySetName` et transmission d’une valeur string qui spécifie le nom du jeu de stratégies. (Vous pouvez spécifier `null` pour cette valeur de paramètre qui entraîne l’ajout de la politique au jeu de politiques *Mes politiques*.)
   * Créez la période de validité de la stratégie en appelant la variable `InfomodelObjectFactory` statique de l’objet `createValidityPeriod` . Cette méthode renvoie un objet `ValidityPeriod`.
   * Définissez le nombre de jours pendant lesquels un document protégé par une stratégie est accessible en appelant la variable `ValidityPeriod` de `setRelativeExpirationDays` et transmettre une valeur entière qui spécifie le nombre de jours.
   * Définissez la période de validité de la stratégie en appelant la variable `Policy` de `setValidityPeriod` et transmission de la méthode `ValidityPeriod` .

1. Créez une entrée de politique.

   * Créez une entrée de stratégie en appelant la méthode `InfomodelObjectFactory` statique de l’objet `createPolicyEntry` . Cette méthode renvoie un objet `PolicyEntry`.
   * Spécifiez les autorisations de la stratégie en appelant la fonction `InfomodelObjectFactory` statique de l’objet `createPermission` . Transmettez un membre de données statique qui appartient à l’interface `Permission` qui représente l’autorisation. Cette méthode renvoie un objet `Permission`. Par exemple, pour ajouter l’autorisation qui permet aux utilisateurs de copier des données d’un document PDF protégé par une politique, transmettez `Permission.COPY`. (Répétez cette étape pour chaque autorisation à ajouter).
   * Ajoutez l’autorisation à l’entrée de stratégie en appelant la méthode `PolicyEntry` de `addPermission` et transmission de la méthode `Permission` . (Répétez cette étape pour chaque objet `Permission` que vous avez créé).
   * Créez l’entité de stratégie en appelant la méthode `InfomodelObjectFactory` statique de l’objet `createSpecialPrincipal` . Transmettez un membre de données qui appartient à l’objet `InfomodelObjectFactory` qui représente le principal. Cette méthode renvoie un objet `Principal`. Par exemple, pour ajouter l’éditeur du document en tant qu’entité principale, transmettez `InfomodelObjectFactory.PUBLISHER_PRINCIPAL`.
   * Ajoutez l’entité de sécurité à l’entrée de stratégie en appelant la méthode `PolicyEntry` de `setPrincipal`et transmission de la méthode `Principal` .
   * Ajoutez l’entrée de stratégie à la stratégie en appelant la méthode `Policy` de `addPolicyEntry` et transmission de la méthode `PolicyEntry` .

1. Enregistrez la politique.

   * Créez un `PolicyManager` en appelant la méthode `DocumentSecurityClient` de `getPolicyManager` .
   * Enregistrez la stratégie en appelant la méthode `PolicyManager` de `registerPolicy` et transmission des valeurs suivantes :

      * Objet `Policy` représentant la politique à enregistrer.

   * Valeur de chaîne représentant le jeu de politiques auquel appartient la politique.

   Si vous utilisez un compte administrateur d’AEM forms dans les paramètres de connexion pour créer la variable `DocumentSecurityClient` , puis spécifiez le nom du jeu de stratégies lorsque vous appelez la variable `registerPolicy` . Si vous transmettez une valeur `null` pour le jeu de politiques, la politique est créée dans le jeu de politiques *Mes politiques* au niveau administrateur.

   Si vous utilisez un utilisateur Document Security dans les paramètres de connexion, vous pouvez appeler la méthode `registerPolicy` surchargée qui accepte uniquement la politique. En d’autres termes, vous n’avez pas besoin de spécifier le nom du jeu de politiques. Cependant, la politique est ajoutée au jeu de politiques nommé *Mes politiques*. Si vous ne souhaitez pas ajouter la nouvelle politique à ce jeu de politiques, indiquez un nom de jeu de politiques lorsque vous appelez la méthode `registerPolicy`.

   >[!NOTE]
   >
   >Lors de la création d’une politique, référencez un jeu de politiques existant. Si vous spécifiez un jeu de politiques qui n’existe pas, une exception est générée.

Pour obtenir des exemples de code à l’aide du service Document Security, reportez-vous aux sections suivantes :

* « Démarrage rapide (mode SOAP) : créer une politique à l’aide de l’API Java »

### Créer une politique à l’aide de l’API Web Service {#create-a-policy-using-the-web-service-api}

Créez une politique à l’aide de l’API Document Security (Web Service) :

1. Incluez les fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Veillez à utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` avec l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un objet API client Document Security.

   * Créez un objet `DocumentSecurityServiceClient` en utilisant son constructeur par défaut.
   * Créez un objet `DocumentSecurityServiceClient.Endpoint.Address` en utilisant le constructeur `System.ServiceModel.EndpointAddress`. Transmettez une valeur string qui spécifie le WSDL au service AEM Forms (par exemple `http://localhost:8080/soap/services/RightsManagementService?WSDL`). Vous n’avez pas besoin d’utiliser l’attribut `lc_version`. Cet attribut est utilisé lorsque vous créez une référence de service.)
   * Créez un objet `System.ServiceModel.BasicHttpBinding` en obtenant la valeur du champ `RightsManagementServiceClient.Endpoint.Binding`. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez la variable `System.ServiceModel.BasicHttpBinding` de `MessageEncoding` champ à `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.

   * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Définissez les attributs de la stratégie.

   * Créez un objet `PolicySpec` en utilisant son constructeur.
   * Définissez le nom de la stratégie en attribuant une valeur de chaîne au `PolicySpec` de `name` membre de données.
   * Définissez la description de la stratégie en attribuant une valeur de chaîne à la variable `PolicySpec` de `description` membre de données.
   * Spécifiez le jeu de stratégies auquel appartient la stratégie en attribuant une valeur string à la variable `PolicySpec` de `policySetName` membre de données. Spécifiez un nom de jeu de stratégies existant. (Vous pouvez spécifier `null` pour cette valeur de paramètre qui entraîne l’ajout de la politique à *Mes politiques*.)
   * Définissez la période d’ouverture hors connexion de la stratégie en attribuant une valeur entière à la variable `PolicySpec` de `offlineLeasePeriod` membre de données.
   * Définissez la variable `PolicySpec` de `policyXml` membre de données avec une valeur string qui représente les données XML PDRL. Pour effectuer cette tâche, créez un objet `StreamReader` .NET en utilisant son constructeur. Transmettez l’emplacement d’un fichier XML PDRL qui représente la politique au constructeur `StreamReader`. Ensuite, appelez la fonction `StreamReader` de `ReadLine` et affecter la valeur renvoyée à une variable string . Effectuez une itération à l’aide de l’objet `StreamReader` jusqu’à ce que la méthode `ReadLine` renvoie une valeur nulle. Affectez la variable string à la variable `PolicySpec` de `policyXml` membre de données.

1. Créez une entrée de politique.

   Il n’est pas nécessaire de créer une entrée de politique lors de la création d’une politique à l’aide de l’API Web Service Document Security. L’entrée de politique est définie dans le document PDRL.

1. Enregistrez la politique.

   Enregistrez la stratégie en appelant la méthode `DocumentSecurityServiceClient` de `registerPolicy` et transmission des valeurs suivantes :

   * Objet `PolicySpec` représentant la politique à enregistrer.
   * Valeur string représentant le jeu de politiques auquel appartient la politique. Vous pouvez définir une valeur `null` qui entraîne l’ajout de la politique au jeu de politiques *Mes politiques*.

   Si vous utilisez un compte administrateur d’AEM forms dans les paramètres de connexion pour créer la variable `DocumentSecurityClient` , spécifiez le nom du jeu de stratégies lors de l’appel de la variable `registerPolicy` .

   Si vous utilisez un utilisateur Document Security dans les paramètres de connexion, vous pouvez appeler la méthode de surcharge `registerPolicy` qui accepte uniquement la politique. En d’autres termes, vous n’avez pas besoin de spécifier le nom du jeu de politiques. Cependant, la politique est ajoutée au jeu de politiques nommé *Mes politiques*. Si vous ne souhaitez pas ajouter la nouvelle politique à ce jeu de politiques, indiquez un nom de jeu de politiques lorsque vous appelez la méthode `registerPolicy`.

   >[!NOTE]
   >
   >Lors de la création d’une politique et de la définition d’un jeu de politiques, assurez-vous de spécifier un jeu de politiques existant. Si vous spécifiez un jeu de politiques qui n’existe pas, une exception est générée.

Pour obtenir des exemples de code à l’aide du service Document Security, reportez-vous aux tutoriels de démarrage rapide suivants :

* « Démarrage rapide (MTOM) : créer une politique à l’aide de l’API de service web »
* « Démarrage rapide (SwaRef) : créer une politique à l’aide de l’API de service web »

## Modifier les politiques {#modifying-policies}

Vous pouvez modifier une politique existante à l’aide de l’API Java Document Security ou de l’API Web Service. Pour modifier une stratégie existante, vous devez la récupérer, la modifier, puis la mettre à jour sur le serveur. Supposons, par exemple, que vous récupérez une politique existante et que vous étendez sa période de validité. Avant que la modification ne prenne effet, vous devez mettre la politique à jour.

Vous pouvez modifier une politique lorsque les besoins de l’entreprise changent et que la politique ne reflète plus ces besoins. Au lieu de créer une stratégie, vous pouvez simplement mettre à jour une stratégie existante.

Pour modifier les attributs de politique à l’aide d’un service web (par exemple à l’aide de classes proxy Java créées avec JAX-WS), vous devez vous assurer que la politique est enregistrée auprès du service Document Security. Vous pouvez ensuite référencer la politique existante à l’aide de la méthode `PolicySpec.getPolicyXml` et modifier les attributs de politique à l’aide des méthodes applicables. Par exemple, vous pouvez modifier la période d’ouverture hors connexion en appelant la méthode `PolicySpec.setOfflineLeasePeriod`.

>[!NOTE]
>
>Pour plus d’informations sur le service Forms, voir [Référence des services pour AEM Forms](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

### Résumé des étapes {#summary_of_steps-1}

Pour modifier une politique existante, procédez comme suit :

1. Incluez les fichiers de projet.
1. Créez un objet API client Document Security.
1. Récupérez une politique existante.
1. Modifiez les attributs de politique.
1. Mettez à jour la politique.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services web, veillez à inclure les fichiers proxy.

**Créer un objet API client Document Security**

Avant d’effectuer une opération de service Document Security par programmation, vous devez créer un objet client de service Document Security. Si vous utilisez l’API Java, créez un objet `RightsManagementClient`. Si vous utilisez l’API Web Service Document Security, créez un objet `RightsManagementServiceService`.

**Récupérer une politique existante**

Récupérez une stratégie existante pour la modifier. Pour récupérer une politique, spécifiez le nom de la politique et le jeu de politiques auquel elle appartient. Si vous spécifiez une valeur `null` pour le nom du jeu de politiques, la politique est récupérée à partir du jeu de politiques *Mes politiques*.

**Définition des attributs de la stratégie**

Pour modifier une politique, vous modifiez la valeur des attributs de politique. Le seul attribut de politique que vous ne pouvez pas modifier est l’attribut name. Par exemple, pour modifier la période d’ouverture hors connexion de la stratégie, vous pouvez modifier la valeur de l’attribut de période d’ouverture hors connexion de la stratégie.

Lors de la modification de la période d’ouverture hors connexion d’une stratégie à l’aide d’un service Web, la variable `offlineLeasePeriod` sur le champ `PolicySpec` est ignorée. Pour mettre à jour la période d’ouverture hors connexion, modifiez l’élément `OfflineLeasePeriod` dans le document XML PDRL. Référencez ensuite le document XML PDRL mis à jour à l’aide du `PolicySpec` interface d’ `policyXML` membre de données.

>[!NOTE]
>
>Pour plus d’informations sur les autres attributs que vous pouvez définir, voir la description de l’interface `Policy` dans [Référence de l’API AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Mettre à jour la politique**

Avant que les modifications apportées à une politique ne prennent effet, vous devez mettre à jour la politique avec le service Document Security. Les modifications apportées aux politiques qui protègent des documents sont mises à jour la prochaine fois que le document protégé par une politique sera synchronisé avec le service Document Security.

### Modifier les politiques existantes à l’aide de l’API Java {#modify-existing-policies-using-the-java-api}

Modifiez une politique existante à l’aide de l’API Document Security (Java) :

1. Incluez les fichiers de projet.

   Incluez les fichiers JAR client, tels que adobe-rightsmanagement-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un objet API client Document Security.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `RightsManagementClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`. 

1. Récupérez une politique existante.

   * Créez un `PolicyManager` en appelant la méthode `RightsManagementClient` de `getPolicyManager` .
   * Créez un `Policy` qui représente la stratégie à mettre à jour en appelant la fonction `PolicyManager` de `getPolicy` et transmission des valeurs suivantes&quot;

      * Valeur de chaîne représentant le nom du jeu de politiques auquel appartient la politique. Vous pouvez indiquer `null`, ce qui entraîne l’utilisation du jeu de politiques `MyPolicies`.
      * Valeur de chaîne représentant le nom de la politique.

1. Définissez les attributs de la stratégie.

   Modifiez les attributs de la stratégie pour répondre aux besoins de votre entreprise. Par exemple, pour modifier la période d’ouverture hors connexion de la stratégie, appelez la variable `Policy` de `setOfflineLeasePeriod` .

1. Mettez à jour la politique.

   Mettez à jour la stratégie en appelant `PolicyManager` de `updatePolicy` . Transmettez l’objet `Policy` qui représente la politique à mettre à jour.

**Exemples de code**

Pour obtenir des exemples de code à l’aide du service Document Security, reportez-vous à la section Démarrage rapide (mode SOAP) : modifier une politique à l’aide de la section API Java.

### Modifier les politiques existantes à l’aide de l’API Web Service {#modify-existing-policies-using-the-web-service-api}

Modifiez une politique existante à l’aide de l’API Document Security (Web Service) :

1. Incluez les fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Veillez à utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` avec l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un objet API client Document Security.

   * Créez un objet `RightsManagementServiceClient` en utilisant son constructeur par défaut.
   * Créez un objet `RightsManagementServiceClient.Endpoint.Address` en utilisant le constructeur `System.ServiceModel.EndpointAddress`. Transmettez une valeur string qui spécifie le WSDL au service AEM Forms (par exemple `http://localhost:8080/soap/services/RightsManagementService?WSDL`). Vous n’avez pas besoin d’utiliser l’attribut `lc_version`. Cet attribut est utilisé lorsque vous créez une référence de service.)
   * Créez un objet `System.ServiceModel.BasicHttpBinding` en obtenant la valeur du champ `RightsManagementServiceClient.Endpoint.Binding`. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez la variable `System.ServiceModel.BasicHttpBinding` de `MessageEncoding` champ à `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.

   * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Récupérez une politique existante.

   Créez un `PolicySpec` qui représente la stratégie à modifier en appelant la variable `RightsManagementServiceClient` de `getPolicy` et transmission des valeurs suivantes :

   * Une valeur de chaîne qui spécifie le nom du jeu de politiques auquel appartient la politique. Vous pouvez indiquer `null` qui entraîne l’utilisation du jeu de politiques `MyPolicies`.
   * Une valeur de chaîne qui spécifie le nom de la politique.

1. Définissez les attributs de la stratégie.

   Modifiez les attributs de la stratégie pour répondre aux besoins de votre entreprise.

1. Mettez à jour la politique.

   Mettez à jour la stratégie en appelant la méthode `RightsManagementServiceClient` de `updatePolicyFromSDK` et transmission de la méthode `PolicySpec` qui représente la stratégie à mettre à jour.

**Exemples de code**

Pour obtenir des exemples de code à l’aide du service Document Security, reportez-vous aux tutoriels de démarrage rapide suivants :

* « Démarrage rapide (MTOM) : modifier une politique à l’aide de l’API de service Web »
* « Démarrage rapide (SwaRef) : modifier une politique à l’aide de l’API de service web »

## Supprimer des politiques {#deleting-policies}

Vous pouvez supprimer une politique existante à l’aide de l’API Java Document Security ou de l’API de service Web. Une fois une politique supprimée, elle ne peut plus être utilisée pour protéger les documents. Toutefois, les documents existants protégés par une politique qui utilisent la politique restent protégés. Vous pouvez supprimer une politique lorsqu’une politique plus récente est disponible.

>[!NOTE]
>
>Pour plus d’informations sur le service Document Security, voir [Références des services pour AEM Forms](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

### Résumé des étapes {#summary_of_steps-2}

Pour supprimer une politique existante, procédez comme suit :

1. Inclure les fichiers du projet
1. Créez un objet API client Document Security.
1. Supprimez la politique.

**Inclure les fichiers du projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services web, veillez à inclure les fichiers proxy.

**Créer un objet API client Document Security**

Avant d’effectuer par programmation une opération de service Document Security, vous devez créer un objet client de service Document Security. Si vous utilisez l’API Java, créez un objet `RightsManagementClient`. Si vous utilisez l’API du service Web Document Security, créez un objet `RightsManagementServiceService`.

**Supprimer la politique**

Pour supprimer une politique, vous spécifiez la politique à supprimer et le jeu de politiques auquel elle appartient. L’utilisateur dont les paramètres sont utilisés pour appeler AEM Forms doit être autorisé à supprimer la politique. Dans le cas contraire, une exception se produit. De même, si vous tentez de supprimer une politique qui n’existe pas, une exception se produit.

### Supprimer des politiques à l’aide de l’API Java {#delete-policies-using-the-java-api}

Supprimez une politique à l’aide de l’API Document Security (Java) :

1. Incluez les fichiers de projet.

   Incluez les fichiers JAR client, tels que adobe-rightsmanagement-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un objet API client Document Security.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `RightsManagementClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`. 

1. Supprimez la politique.

   * Créez un `PolicyManager` en appelant la méthode `RightsManagementClient` de `getPolicyManager` .
   * Supprimez la stratégie en appelant la méthode `PolicyManager` de `deletePolicy` et transmission des valeurs suivantes :

      * Une valeur de chaîne qui spécifie le nom du jeu de politiques auquel appartient la politique. Vous pouvez indiquer `null` qui entraîne le jeu de politiques `MyPolicies` utilisé.
      * Une valeur de chaîne qui indique le nom de la politique à supprimer.

**Exemples de code**

Pour obtenir des exemples de code à l’aide du service Document Security, reportez-vous aux tutoriels de démarrage rapide suivants :

* « Démarrage rapide (mode SOAP) : créer une politique à l’aide de l’API Java »

### Supprimer des politiques à l’aide de l’API de service web {#delete-policies-using-the-web-service-api}

Supprimez une politique à l’aide de l’API Document Security (service web) :

1. Incluez les fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Veillez à utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` avec l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un objet API client Document Security.

   * Créez un objet `RightsManagementServiceClient` en utilisant son constructeur par défaut.
   * Créez un objet `RightsManagementServiceClient.Endpoint.Address` en utilisant le constructeur `System.ServiceModel.EndpointAddress`. Transmettez une valeur string qui spécifie le WSDL au service AEM Forms (par exemple `http://localhost:8080/soap/services/RightsManagementService?WSDL`). Vous n’avez pas besoin d’utiliser l’attribut `lc_version`. Cet attribut est utilisé lorsque vous créez une référence de service.)
   * Créez un objet `System.ServiceModel.BasicHttpBinding` en obtenant la valeur du champ `RightsManagementServiceClient.Endpoint.Binding`. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez la variable `System.ServiceModel.BasicHttpBinding` de `MessageEncoding` champ à `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.

   * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Supprimez la politique.

   Pour supprimer une stratégie, appelez la méthode `RightsManagementServiceClient` de `deletePolicy` et transmission des valeurs suivantes :

   * Une valeur de chaîne qui spécifie le nom du jeu de politiques auquel appartient la politique. Vous pouvez indiquer `null` qui entraîne le jeu de politiques `MyPolicies` utilisé.
   * Une valeur de chaîne qui indique le nom de la politique à supprimer.

**Exemples de code**

Pour obtenir des exemples de code à l’aide du service Document Security, reportez-vous aux tutoriels de démarrage rapide suivants :

* « Démarrage rapide (MTOM) : supprimer une politique à l’aide de l’API de service web »
* « Démarrage rapide (SwaRef) : supprimer une politique à l’aide de l’API de service web »

## Appliquer des politiques à des documents PDF {#applying-policies-to-pdf-documents}

Vous pouvez appliquer une stratégie à un document PDF pour protéger le document. L’application d’une politique à un document PDF permet de restreindre l’accès au document. Vous ne pouvez pas appliquer de politique à un document si celui-ci est déjà protégé par une autre politique.

Lorsque le document est ouvert, vous pouvez également restreindre l’accès aux fonctionnalités d’Acrobat et d’Adobe Reader, notamment la possibilité d’imprimer et de copier du texte, d’y apporter des modifications et d’y ajouter des signatures et des commentaires. En outre, vous pouvez révoquer un document PDF protégé par une politique lorsque vous ne souhaitez plus que les utilisateurs accèdent au document.

Vous pouvez contrôler l’utilisation d’un document protégé par une politique après sa distribution. En d’autres termes, vous pouvez voir comment le document est utilisé et qui l’utilise. Par exemple, vous pouvez savoir quand un utilisateur a ouvert le document.

>[!NOTE]
>
>Pour plus d’informations sur le service Document Security, voir [Références des services pour AEM Forms](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

### Résumé des étapes {#summary_of_steps-3}

Pour appliquer une politique à un document PDF, procédez comme suit :

1. Incluez les fichiers de projet.
1. Créez un objet API client Document Security.
1. Récupérez un document PDF auquel une politique est appliquée.
1. Appliquez une politique existante au document PDF.
1. Enregistrez le document PDF protégé par une politique.

**Inclure des fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services web, veillez à inclure les fichiers proxy.

**Créer un objet API client Document Security**

Avant d’effectuer par programmation une opération du service Document Security, créez un objet client du service Document Security. Si vous utilisez l’API Java, créez un objet `DocumentSecurityClient`. Si vous utilisez l’API de service web Document Security, créez un objet `DocumentSecurityServiceService`.

**Récupérer un document PDF**

Vous pouvez récupérer un document de PDF pour appliquer une stratégie. Une fois que vous avez appliqué une politique au document PDF, l’accès au document est restreint aux utilisateurs. Par exemple, si la politique ne permet pas l’ouverture du document hors ligne, les utilisateurs doivent être en ligne pour pouvoir ouvrir le document.

**Appliquer une politique existante au document PDF**

Pour appliquer une politique à un document PDF, référencez une politique existante et indiquez à quel jeu de politiques elle appartient. L’utilisateur qui définit les propriétés de connexion doit avoir accès à la politique spécifiée. Dans le cas contraire, une exception se produit.

**Enregistrer le document PDF**

Une fois que le service Document Security a appliqué une politique à un document PDF, vous pouvez enregistrer le document PDF protégé par une politique en tant que fichier PDF.

**Voir également**

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Révoquer l’accès à des documents](protecting-documents-policies.md#revoking-access-to-documents)

### Appliquer une politique à un document PDF à l’aide de l’API Java {#apply-a-policy-to-a-pdf-document-using-the-java-api}

Appliquez une politique à un document PDF à l’aide de l’API Document Security (Java) :

1. Incluez les fichiers de projet.

   Incluez les fichiers JAR client, tels que adobe-rightsmanagement-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un objet API client Document Security.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `RightsManagementClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`. 

1. Récupérez un document PDF.

   * Créez un objet `java.io.FileInputStream` représentant le document PDF à l’aide de son constructeur. Transmettez une valeur de chaîne qui spécifie l’emplacement du document PDF.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Appliquez une politique existante au document PDF.

   * Créez un `DocumentManager` en appelant la méthode `RightsManagementClient` de `getDocumentManager` .
   * Appliquez une stratégie au document du PDF en appelant la méthode `DocumentManager` de `protectDocument` et transmission des valeurs suivantes :

      * L’objet `com.adobe.idp.Document` contenant le document PDF auquel la politique est appliquée.
      * Une valeur de chaîne indiquant le nom du document.
      * Une valeur de chaîne représentant le nom du jeu de politiques auquel la politique appartient. Vous pouvez définir une valeur `null` qui entraîne le jeu de politiques `MyPolicies` utilisé.
      * Une valeur de chaîne qui spécifie le nom de la politique.
      * Une valeur de chaîne représentant le nom du domaine User Manager de l’utilisateur qui est l’éditeur du document. Cette valeur de paramètre est facultative et peut être une valeur null (si ce paramètre est null, la valeur de paramètre suivante doit être null).
      * Une valeur de chaîne représentant le nom canonique de l’utilisateur User Manager qui est l’éditeur du document. Cette valeur de paramètre est facultative et peut être `null` (si ce paramètre est null, la valeur du paramètre précédent doit être `null`).
      * Une valeur `com.adobe.livecycle.rightsmanagement.Locale` représentant le paramètre régional utilisé pour sélectionner le modèle MS Office. Cette valeur de paramètre est facultative et n’est pas utilisée pour les documents PDF. Pour protéger un document PDF, indiquez `null`.

     La méthode `protectDocument` renvoie un objet `RMSecureDocumentResult` contenant le document PDF protégé par une politique.

1. Enregistrez le formulaire PDF.

   * Appeler la variable `RMSecureDocumentResult` de `getProtectedDoc` pour obtenir le document de PDF protégé par une stratégie. Cette méthode renvoie un objet `com.adobe.idp.Document`.
   * Créez un objet `java.io.File` et s’assure que l’extension du fichier est PDF.
   * Appeler la variable `com.adobe.idp.Document` de `copyToFile` pour copier le contenu de la méthode `Document` dans le fichier (assurez-vous d’utiliser la variable `Document` qui a été renvoyé par l’objet `getProtectedDoc` ).

**Exemples de code**

Pour obtenir des exemples de code à l’aide du service Document Security, reportez-vous aux tutoriels de démarrage rapide suivants :

* « Démarrage rapide (mode EJB) : appliquer une politique à un document PDF à l’aide de l’API Java »
* « Démarrage rapide (mode SOAP) : appliquer une politique à un document PDF à l’aide de l’API Java »

**Voir également**

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Appliquer une politique à un document PDF à l’aide de l’API de service web {#apply-a-policy-to-a-pdf-document-using-the-web-service-api}

Pour appliquer une politique à un document PDF à l’aide de l’API Document Security (service web), procédez comme suit :

1. Incluez les fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Veillez à utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` avec l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un objet API client Document Security.

   * Créez un objet `RightsManagementServiceClient` en utilisant son constructeur par défaut.
   * Créez un objet `RightsManagementServiceClient.Endpoint.Address` en utilisant le constructeur `System.ServiceModel.EndpointAddress`. Transmettez une valeur de chaîne indiquant le WSDL au service Forms (par exemple, `http://localhost:8080/soap/services/RightsManagementService?WSDL`). Il n’est pas nécessaire d’utiliser l’attribut `lc_version`. Cet attribut est utilisé lorsque vous créez une référence de service.)
   * Créez un objet `System.ServiceModel.BasicHttpBinding` en obtenant la valeur du champ `RightsManagementServiceClient.Endpoint.Binding`. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez la variable `System.ServiceModel.BasicHttpBinding` de `MessageEncoding` champ à `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.

   * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Récupérez un document PDF.

   * Créez un objet `BLOB` en utilisant son constructeur. L’objet `BLOB` sert à stocker un document PDF auquel une politique est appliquée.
   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur de chaîne représentant l’emplacement du document PDF et son mode d’ouverture.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `System.IO.FileStream`. Déterminez la taille du tableau d’octets en obtenant la variable `System.IO.FileStream` de `Length` .
   * Renseignez le tableau d’octets avec les données de diffusion en appelant la variable `System.IO.FileStream` de `Read` . Transmettez le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’objet `BLOB` en attribuant à son champ `MTOM` le contenu du tableau d’octets.

1. Appliquez une politique existante au document PDF.

   Appliquez une stratégie au document du PDF en appelant la méthode `RightsManagementServiceClient` de `protectDocument` et transmission des valeurs suivantes :

   * L’objet `BLOB` contenant le document PDF auquel la politique est appliquée.
   * Une valeur de chaîne indiquant le nom du document.
   * Une valeur de chaîne représentant le nom du jeu de politiques auquel la politique appartient. Vous pouvez définir une valeur `null` qui entraîne le jeu de politiques `MyPolicies` utilisé.
   * Une valeur de chaîne qui spécifie le nom de la politique.
   * Une valeur de chaîne représentant le nom du domaine User Manager de l’utilisateur qui est l’éditeur du document. Cette valeur de paramètre est facultative et peut être définie sur null (si ce paramètre est défini sur null, la valeur du paramètre suivant doit être `null`).
   * Une valeur de chaîne représentant le nom canonique de l’utilisateur User Manager qui est l’éditeur du document. Cette valeur de paramètre est facultative et peut être définie sur null (si ce paramètre est défini sur null, la valeur du paramètre précédent doit être `null`).
   * Une valeur `RMLocale` spécifiant la valeur du paramètre régional (par exemple, `RMLocale.en`).
   * Un paramètre de sortie de chaîne utilisé pour stocker la valeur de l’identifiant de politique.
   * Un paramètre de sortie de chaîne utilisé pour stocker la valeur de l’identifiant protégée par une politique.
   * Un paramètre de sortie de chaîne utilisé pour stocker le type MIME (par exemple, `application/pdf`).

   La méthode `protectDocument` renvoie un objet `BLOB` contenant le document PDF protégé par une politique.

1. Enregistrez le formulaire PDF.

   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur de chaîne représentant l’emplacement du document PDF protégé par une politique.
   * Créez un tableau d’octets qui stocke le contenu des données de l’objet `BLOB` renvoyé par la méthode `protectDocument`. Renseignez le tableau d’octets en obtenant la valeur de la variable `BLOB` de `MTOM` membre de données.
   * Créez un objet `System.IO.BinaryWriter` en utilisant son constructeur et en transmettant l’objet `System.IO.FileStream`.
   * Ecrivez le contenu du tableau d’octets dans un fichier de PDF en appelant la méthode `System.IO.BinaryWriter` de `Write` et transmission du tableau d’octets.

**Exemples de code**

Pour obtenir des exemples de code à l’aide du service Document Security, reportez-vous aux tutoriels de démarrage rapide suivants :

* « Démarrage rapide (MTOM) : appliquer une politique à un document PDF à l’aide de l’API de service web »
* « Démarrage rapide (SwaRef) : appliquer une politique à un document PDF à l’aide de l’API de service web »

## Supprimer des politiques des documents PDF {#removing-policies-from-pdf-documents}

Vous pouvez supprimer une stratégie d’un document protégé par une stratégie pour supprimer la protection du document. Effectuez cette opération si vous ne souhaitez plus que le document soit protégé par une politique. Si vous souhaitez mettre à jour un document protégé par une politique avec une nouvelle politique, au lieu de supprimer la politique et d’ajouter la politique mise à jour, il est préférable de changer de politique.

>[!NOTE]
>
>Pour plus d’informations sur le service Document Security, consultez la section [Références des services pour AEM Forms](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

### Résumé des étapes {#summary_of_steps-4}

Pour supprimer une politique d’un document PDF protégé par une politique, procédez comme suit :

1. Inclure les fichiers du projet
1. Créez un objet API client Document Security.
1. Récupérez un document PDF protégé par une politique.
1. Supprimez la politique du document PDF.
1. Enregistrez le document PDF non sécurisé.

**Inclure des fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services web, veillez à inclure les fichiers proxy.

**Créer un objet API client Document Security**

Avant d’effectuer par programmation une opération de service Document Security, créez un objet client de service Document Security.

**Récupérer un document PDF protégé par une politique**

Vous pouvez récupérer un document de PDF protégé par une stratégie pour supprimer une stratégie. Si vous tentez de supprimer une politique d’un document PDF qui n’est pas protégé par une politique, une exception est générée.

**Supprimer la politique du document PDF**

Vous pouvez supprimer une politique d’un document PDF protégé par une politique à condition qu’un administrateur soit indiqué dans les paramètres de connexion. Si ce n’est pas le cas, la stratégie utilisée pour protéger un document doit contenir la variable `SWITCH_POLICY` autorisation de supprimer une stratégie d’un document de PDF. En outre, l’utilisateur spécifié dans les paramètres de connexion AEM Forms doit également disposer de cette autorisation. Dans le cas contraire, une exception est générée.

**Enregistrer un document PDF non sécurisé**

Une fois que le service Document Security a supprimé une politique d’un document PDF, vous pouvez enregistrer le document PDF non protégé en tant que fichier PDF.

**Voir également**

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Appliquer des politiques à des documents PDF](protecting-documents-policies.md#applying-policies-to-pdf-documents)

### Supprimer une politique d’un document PDF à l’aide de l’API Java {#remove-a-policy-from-a-pdf-document-using-the-java-api}

Pour supprimer une politique d’un document PDF protégé par une politique à l’aide de l’API Document Security (Java), procédez comme suit :

1. Incluez les fichiers de projet.

   Incluez les fichiers JAR client, tels que adobe-rightsmanagement-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un objet API client Document Security.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `DocumentSecurityClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`. 

1. Récupérez un document PDF protégé par une politique.

   * Créez un objet `java.io.FileInputStream` représentant le document PDF protégé par une politique en utilisant son constructeur et en transmettant une valeur de chaîne qui spécifie l’emplacement du document PDF.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Supprimez la politique du document PDF.

   * Créez un `DocumentManager` en appelant la méthode `DocumentSecurityClient` de `getDocumentManager` .
   * Supprimez une stratégie du document du PDF en appelant la méthode `DocumentManager` de `removeSecurity` et transmission de la méthode `com.adobe.idp.Document` contenant le document de PDF protégé par une stratégie. Cette méthode renvoie un objet `com.adobe.idp.Document` contenant un document PDF non sécurisé.

1. Enregistrez le document PDF non sécurisé.

   * Créez un objet `java.io.File` et assurez-vous que l’extension du fichier est PDF.
   * Appeler la variable `Document` de `copyToFile` pour copier le contenu de la méthode `Document` dans le fichier (assurez-vous d’utiliser la variable `Document` qui a été renvoyé par l’objet `removeSecurity` ).

**Exemples de code**

Pour obtenir des exemples de code à l’aide du service Document Security, reportez-vous aux tutoriels de démarrage rapide suivants :

* « Démarrage rapide (mode SOAP) : appliquer une politique à un document PDF à l’aide de l’API Java »

### Supprimer une politique à l’aide de l’API de service web {#remove-a-policy-using-the-web-service-api}

Pour supprimer une politique d’un document PDF protégé par une politique à l’aide de l’API Document Security (service web), procédez comme suit :

1. Incluez les fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Veillez à utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` avec l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un objet API client Document Security.

   * Créez un objet `DocumentSecurityServiceClient` en utilisant son constructeur par défaut.
   * Créez un objet `DocumentSecurityServiceClient.Endpoint.Address` en utilisant le constructeur `System.ServiceModel.EndpointAddress`. Transmettez une valeur string qui spécifie le WSDL au service AEM Forms (par exemple `http://localhost:8080/soap/services/RightsManagementService?WSDL`). Vous n’avez pas besoin d’utiliser l’attribut `lc_version`. Cet attribut est utilisé lorsque vous créez une référence de service.)
   * Créez un objet `System.ServiceModel.BasicHttpBinding` en obtenant la valeur du champ `DocumentSecurityServiceClient.Endpoint.Binding`. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez la variable `System.ServiceModel.BasicHttpBinding` de `MessageEncoding` champ à `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.

   * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Récupérez un document PDF protégé par une politique.

   * Créez un objet `BLOB` en utilisant son constructeur. L’objet `BLOB` sert à stocker le document PDF protégé par une politique à partir duquel la politique est supprimée.
   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur de chaîne représentant l’emplacement du document PDF et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `System.IO.FileStream`. Vous pouvez déterminer la taille du tableau d’octets en obtenant la variable `System.IO.FileStream` de `Length` .
   * Renseignez le tableau d’octets avec les données de diffusion en appelant la variable `System.IO.FileStream` de `Read` et transmettre le tableau byte, la position de départ et la longueur du flux à lire.
   * Renseignez l’objet `BLOB` en attribuant à son champ `MTOM` le contenu du tableau d’octets.

1. Supprimez la politique du document PDF.

   Supprimez la stratégie du document du PDF en appelant la méthode `DocumentSecurityServiceClient` de `removePolicySecurity` et transmission de la méthode `BLOB` contenant le document de PDF protégé par une stratégie. Cette méthode renvoie un objet `BLOB` contenant un document PDF non sécurisé.

1. Enregistrez le document PDF non sécurisé.

   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur de chaîne représentant l’emplacement du document PDF non sécurisé.
   * Créez un tableau d’octets qui stocke le contenu des données de l’objet `BLOB` renvoyé par la méthode `removePolicySecurity`. Renseignez le tableau d’octets en obtenant la valeur de la variable `BLOB` de `MTOM` champ .
   * Créez un objet `System.IO.BinaryWriter` en utilisant son constructeur et en transmettant l’objet `System.IO.FileStream`.

**Exemples de code**

Pour obtenir des exemples de code à l’aide du service Document Security, reportez-vous aux tutoriels de démarrage rapide suivants :

* « Démarrage rapide (MTOM) : supprimer une politique d’un document PDF à l’aide de l’API de service web »
* « Démarrage rapide (SwaRef) : supprimer une politique d’un document PDF à l’aide de l’API de service web »

**Voir également**

[Appeler AEM Forms en utilisant MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Appel d’AEM Forms à l’aide de SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Révoquer l’accès à des documents {#revoking-access-to-documents}

Vous pouvez révoquer l’accès à un document PDF protégé par une politique, ce qui rend toutes les copies du document inaccessibles aux utilisateurs. Lorsqu’un utilisateur tente d’ouvrir un document PDF révoqué, il est redirigé vers une URL spécifique où un document révisé peut être consulté. L’URL vers laquelle l’utilisateur est redirigé doit être spécifiée par programme. Lorsque vous révoquez l’accès à un document, la modification prend effet lors de la synchronisation suivante de l’utilisateur avec le service Document Security, à l’ouverture du document en ligne protégé par une politique.

La possibilité de révoquer l’accès à un document offre une sécurité supplémentaire. Supposons, par exemple, qu’une version plus récente d’un document soit disponible et que vous ne souhaitiez plus que quiconque consulte la version obsolète. Dans ce cas, l’accès à l’ancien document peut être révoqué, et personne ne peut afficher le document à moins que l’accès ne soit rétabli.

>[!NOTE]
>
>Pour plus d’informations sur le service Document Security, voir [Références des services pour AEM Forms](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

### Résumé des étapes {#summary_of_steps-5}

Pour révoquer un document protégé par une politique, procédez comme suit :

1. Incluez les fichiers de projet.
1. Créez un objet API client Document Security.
1. Récupérez un document PDF protégé par une politique.
1. Révoquez le document protégé par une politique.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services web, veillez à inclure les fichiers proxy.

**Créer un objet API client Document Security**

Avant d’effectuer une opération de service Document Security par programme, vous devez créer un objet client de service Document Security.

**Récupérer un document PDF protégé par une politique**

Récupérez un document de PDF protégé par une stratégie pour le révoquer. Vous ne pouvez pas révoquer un document qui a déjà été révoqué ou qui n’est pas un document protégé par une politique.

Si vous connaissez la valeur de l’identifiant de licence du document PDF protégé par une politique, il n’est pas nécessaire de récupérer ce dernier. Cependant, dans la plupart des cas, vous devez récupérer le document du PDF pour obtenir la valeur de l’identifiant de licence.

**Révoquer le document protégé par une politique**

Pour révoquer un document protégé par une politique, spécifiez l’identifiant de licence du document en question. En outre, vous pouvez spécifier l’URL d’un document que l’utilisateur peut afficher lorsqu’il tente d’ouvrir le document révoqué. En d’autres termes, supposons qu’un document obsolète soit révoqué. Lorsqu’un utilisateur tente d’ouvrir ce document révoqué, il voit un document mis à jour à la place.

>[!NOTE]
>
>Si vous tentez de révoquer un document déjà révoqué, une exception est générée.

**Voir également**

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Appliquer des politiques à des documents PDF](protecting-documents-policies.md#applying-policies-to-pdf-documents)

[Rétablir l’accès aux documents révoqués](protecting-documents-policies.md#reinstating-access-to-revoked-documents)

### Révoquer l’accès aux documents à l’aide de l’API Java {#revoke-access-to-documents-using-the-java-api}

Révoquez l’accès à un document PDF protégé par une politique à l’aide de l’API Document Security (Java) :

1. Inclure les fichiers du projet

   Incluez les fichiers JAR client, tels que adobe-rightsmanagement-client.jar, dans le chemin de classe de votre projet Java.

1. Créer un objet API client Document Security

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `DocumentSecurityClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`. 

1. Récupérer un document PDF protégé par une politique

   * Créez un objet `java.io.FileInputStream` représentant le document PDF protégé par une politique en utilisant son constructeur et en transmettant une valeur de chaîne qui spécifie l’emplacement du document PDF.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Révoquer le document protégé par une politique

   * Créez un `DocumentManager` en appelant la méthode `DocumentSecurityClient` de `getDocumentManager` .
   * Récupérez la valeur de l’identifiant de licence du document protégé par une stratégie en appelant la fonction `DocumentManager` de `getLicenseId` . Transmettez l’objet `com.adobe.idp.Document` représentant le document protégé par une politique. Cette méthode renvoie une valeur string qui représente la valeur de l’identifiant de licence.
   * Créez un `LicenseManager` en appelant la méthode `DocumentSecurityClient` de `getLicenseManager` .
   * Révoquez le document protégé par une stratégie en appelant la fonction `LicenseManager` de `revokeLicense` et transmission des valeurs suivantes :

      * Une valeur string qui spécifie la valeur d’identifiant de licence du document protégé par une stratégie (spécifiez la valeur renvoyée par la propriété `DocumentManager` de `getLicenseId` ).
      * Membre de données statique de l’interface `License` spécifiant le motif de révocation du document. Par exemple, vous pouvez spécifier `License.DOCUMENT_REVISED`.
      * Valeur `java.net.URL` spécifiant l’emplacement vers lequel se trouve un document modifié. Si vous ne souhaitez pas rediriger un utilisateur vers une autre URL, vous pouvez transmettre `null`.

**Exemples de code**

Pour obtenir des exemples de code à l’aide du service Document Security, reportez-vous aux tutoriels de démarrage rapide suivants :

* « Démarrage rapide (mode SOAP) : révoquer un document à l’aide de l’API Java »

### Révoquer l’accès aux documents à l’aide de l’API Web Service {#revoke-access-to-documents-using-the-web-service-api}

Révoquez l’accès à un document PDF protégé par une politique à l’aide de l’API Document Security (Web Service) :

1. Inclure les fichiers du projet

   Créez un projet Microsoft .NET qui utilise MTOM. Veillez à utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Créer un objet API client Document Security

   * Créez un objet `DocumentSecurityServiceClient` en utilisant son constructeur par défaut.
   * Créez un objet `DocumentSecurityServiceClient.Endpoint.Address` en utilisant le constructeur `System.ServiceModel.EndpointAddress`. Transmettez une valeur string qui spécifie le WSDL au service AEM Forms (par exemple `http://localhost:8080/soap/services/RightsManagementService?WSDL`). Vous n’avez pas besoin d’utiliser l’attribut `lc_version`. Cet attribut est utilisé lorsque vous créez une référence de service.)
   * Créez un objet `System.ServiceModel.BasicHttpBinding` en obtenant la valeur du champ `DocumentSecurityServiceClient.Endpoint.Binding`. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez la variable `System.ServiceModel.BasicHttpBinding` de `MessageEncoding` champ à `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.

   * Affectez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Récupérer un document PDF protégé par une politique

   * Créez un objet `BLOB` en utilisant son constructeur. L’objet `BLOB` sert à stocker un document PDF protégé par une politique révoqué.
   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur de chaîne représentant l’emplacement du document PDF protégé par une politique à révoquer et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `System.IO.FileStream`. Vous pouvez déterminer la taille du tableau d’octets en obtenant la variable `System.IO.FileStream` de `Length` .
   * Renseignez le tableau d’octets avec les données de diffusion en appelant la variable `System.IO.FileStream` de `Read` et transmettre le tableau byte, la position de départ et la longueur du flux à lire.
   * Renseignez l’objet `BLOB` en attribuant à son champ `MTOM` le contenu du tableau d’octets.

1. Révoquer le document protégé par une politique

   * Récupérez la valeur de l’identifiant de licence du document protégé par une stratégie en appelant la fonction `DocumentSecurityServiceClient` de `getLicenseID` et transmission de la méthode `BLOB` qui représente le document protégé par une stratégie. Cette méthode renvoie une valeur de chaîne représentant l’identifiant de licence.
   * Révoquez le document protégé par une stratégie en appelant la fonction `DocumentSecurityServiceClient` de `revokeLicense` et transmission des valeurs suivantes :

      * Une valeur string qui spécifie la valeur d’identifiant de licence du document protégé par une stratégie (spécifiez la valeur renvoyée par la propriété `DocumentSecurityServiceService` de `getLicenseId` ).
      * Membre de données statique de l’énumération `Reason` indiquant le motif de révocation du document. Par exemple, vous pouvez spécifier `Reason.DOCUMENT_REVISED`.
      * Valeur `string` indiquant l’emplacement URL vers lequel se trouve un document modifié. Si vous ne souhaitez pas rediriger un utilisateur vers une autre URL, vous pouvez transmettre `null`.

**Exemples de code**

Pour obtenir des exemples de code à l’aide du service Document Security, reportez-vous aux tutoriels de démarrage rapide suivants :

* « Démarrage rapide (MTOM) : révoquer un document à l’aide de l’API de service web »
* « Démarrage rapide (SwaRef) : révoquer un document à l’aide de l’API de service web »

**Voir également**

[Supprimer des politiques de documents Word](protecting-documents-policies.md#removing-policies-from-word-documents)

[Appeler AEM Forms en utilisant MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Appel d’AEM Forms à l’aide de SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Rétablir l’accès aux documents révoqués {#reinstating-access-to-revoked-documents}

Vous pouvez rétablir l’accès à un document PDF révoqué, ce qui rend toutes les copies du document révoqué accessibles aux utilisateurs. Lorsqu’un utilisateur ouvre un document restauré qui a été révoqué, il peut consulter le document.

>[!NOTE]
>
>Pour plus d’informations sur le service Document Security, voir [Référence des services pour AEM Forms](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

### Résumé des étapes {#summary_of_steps-6}

Pour rétablir l’accès à un document PDF révoqué, procédez comme suit :

1. Incluez les fichiers de projet.
1. Créez un objet API client Document Security.
1. Récupérez l’identifiant de licence du document PDF révoqué.
1. Rétablissez l’accès au document PDF révoqué.

**Inclure des fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services web, veillez à inclure les fichiers proxy.

**Créer un objet API client Document Security**

Avant d’effectuer par programmation une opération de service Document Security, vous devez créer un objet client de service Document Security. Si vous utilisez l’API Java, créez un objet `DocumentSecurityClient`. Si vous utilisez l’API de service web Document Security, créez un objet `DocumentSecurityServiceService`.

**Récupérer l’identifiant de licence du document PDF révoqué**

Récupérez l’identifiant de licence du document de PDF révoqué pour rétablir un document de PDF révoqué. Une fois que vous avez obtenu la valeur d’identifiant de licence, vous pouvez restaurer un document révoqué. Si vous tentez de restaurer un document qui n’est pas révoqué, une exception est générée.

**Rétablir l’accès au document PDF révoqué**

Pour rétablir l’accès à un document PDF révoqué, vous devez indiquer l’identifiant de licence du document révoqué. Si vous tentez de rétablir l’accès à un document PDF qui n’est pas révoqué, une exception est générée.

**Voir également**

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Appliquer des politiques à des documents PDF](protecting-documents-policies.md#applying-policies-to-pdf-documents)

[Révoquer l’accès à des documents](protecting-documents-policies.md#revoking-access-to-documents)

### Rétablir l’accès aux documents révoqués à l’aide de l’API Java {#reinstate-access-to-revoked-documents-using-the-java-api}

Rétablissez l’accès à un document révoqué à l’aide de l’API Document Security (Java) :

1. Incluez les fichiers de projet.

   Incluez les fichiers JAR client, tels que adobe-rightsmanagement-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un objet API client Document Security.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `DocumentSecurityClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`. 

1. Récupérez l’identifiant de licence du document PDF révoqué.

   * Créez un objet `java.io.FileInputStream` qui représente le document PDF révoqué en utilisant son constructeur et en transmettant une valeur string spécifiant l’emplacement du document PDF.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 
   * Créez un `DocumentManager` en appelant la méthode `DocumentSecurityClient` de `getDocumentManager` .
   * Récupérez la valeur de l’identifiant de licence du document révoqué en appelant la fonction `DocumentManager` de `getLicenseId` et transmission de la méthode `com.adobe.idp.Document` qui représente le document révoqué. Cette méthode renvoie une valeur string qui représente l’identifiant de licence.

1. Rétablissez l’accès au document PDF révoqué.

   * Créez un `LicenseManager` en appelant la méthode `DocumentSecurityClient` de `getLicenseManager` .
   * Rétablissez l’accès au document du PDF révoqué en appelant la méthode `LicenseManager` de `unrevokeLicense` et transmission de la valeur d’identifiant de licence du document révoqué.

**Exemples de code**

Pour obtenir des exemples de code à l’aide du service Document Security, reportez-vous aux tutoriels de démarrage rapide suivants :

* « Démarrage rapide (mode SOAP) : rétablir l’accès à un document révoqué à l’aide de l’API de service web »

### Rétablir l’accès aux documents révoqués à l’aide de l’API Web Service {#reinstate-access-to-revoked-documents-using-the-web-service-api}

Rétablissez l’accès à un document révoqué à l’aide de l’API Document Security (Web Service) :

1. Incluez les fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Veillez à utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` avec l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un objet API client Document Security.

   * Créez un objet `DocumentSecurityServiceClient` en utilisant son constructeur par défaut.
   * Créez un objet `DocumentSecurityServiceClient.Endpoint.Address` en utilisant le constructeur `System.ServiceModel.EndpointAddress`. Transmettez une valeur string qui spécifie le WSDL au service AEM Forms (par exemple `http://localhost:8080/soap/services/RightsManagementService?WSDL`). Vous n’avez pas besoin d’utiliser l’attribut `lc_version`. Cet attribut est utilisé lorsque vous créez une référence de service.)
   * Créez un objet `System.ServiceModel.BasicHttpBinding` en obtenant la valeur du champ `DocumentSecurityServiceClient.Endpoint.Binding`. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez la variable `System.ServiceModel.BasicHttpBinding` de `MessageEncoding` champ à `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.

   * Affectez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Récupérez l’identifiant de licence du document PDF révoqué.

   * Créez un objet `BLOB` en utilisant son constructeur. L’objet `BLOB` sert à stocker un document PDF révoqué auquel l’accès est rétabli.
   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur string qui représente l’emplacement du document PDF révoqué et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `System.IO.FileStream`. Vous pouvez déterminer la taille du tableau d’octets en obtenant la variable `System.IO.FileStream` de `Length` .
   * Renseignez le tableau d’octets avec les données de diffusion en appelant la variable `System.IO.FileStream` de `Read` et transmettre le tableau byte, la position de départ et la longueur du flux à lire.
   * Renseignez l’objet `BLOB` en attribuant à son champ `MTOM` le contenu du tableau d’octets.

1. Rétablissez l’accès au document PDF révoqué.

   * Récupérez la valeur de l’identifiant de licence du document révoqué en appelant la fonction `DocumentSecurityServiceClient` de `getLicenseID` et transmission de la méthode `BLOB` qui représente le document révoqué. Cette méthode renvoie une valeur de chaîne représentant l’identifiant de licence.
   * Rétablissez l’accès au document du PDF révoqué en appelant la méthode `DocumentSecurityServiceClient` de `unrevokeLicense` et transmission d’une valeur string qui spécifie la valeur d’identifiant de licence du document de PDF révoqué (transmettez la valeur de retour de la fonction `DocumentSecurityServiceClient` de `getLicenseId` ).

**Exemples de code**

Pour obtenir des exemples de code à l’aide du service Document Security, reportez-vous aux tutoriels de démarrage rapide suivants :

* « Démarrage rapide (MTOM) : rétablir l’accès à un document révoqué à l’aide de l’API de service web »
* « Démarrage rapide (SwaRef) : rétablir l’accès à un document révoqué à l’aide de l’API de service web »

**Voir également**

[Appeler AEM Forms en utilisant MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Appel d’AEM Forms à l’aide de SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Inspecter des documents PDF protégés par une politique {#inspecting-policy-protected-pdf-documents}

Vous pouvez utiliser l’API du service Document Security (Java et service web) pour inspecter les documents PDF protégés par une politique. L’inspection des documents PDF protégés par une politique renvoie des informations sur le document PDF protégé par une politique. Vous pouvez, par exemple, déterminer la politique utilisée pour protéger le document et la date à laquelle le document a été protégé.

Vous ne pouvez pas effectuer cette tâche si vous posséder LiveCycle version 8.x ou antérieure. AEM Forms prend en charge de l’inspection des documents protégés par une politique. Si vous tentez d’inspecter un document protégé par une politique à l’aide de LiveCycle version 8.x ou antérieure, une exception est générée.

>[!NOTE]
>
>Pour plus d’informations sur le service Document Security, consultez la section [Références des services pour AEM Forms](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

### Résumé des étapes {#summary_of_steps-7}

Pour inspecter un document PDF protégé par une politique, procédez comme suit :

1. Incluez les fichiers de projet.
1. Créez un objet API client Document Security.
1. Récupérez un document protégé par une politique à inspecter.
1. Obtenez des informations sur le document protégé par une politique.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services web, veillez à inclure les fichiers proxy.

**Créer un objet API client Document Security**

Avant d’effectuer par programmation une opération du service Document Security, créez un objet client du service Document Security. Si vous utilisez l’API Java, créez un objet `RightsManagementClient`. Si vous utilisez l’API de service web Document Security, créez un objet `RightsManagementServiceService`.

**Récupérer un document protégé par une politique à inspecter**

Pour inspecter un document protégé par une politique, récupérez-le. Si vous tentez d’inspecter un document non protégé par une politique ou révoqué, une exception est générée.

**Inspecter le document**

Une fois quʼun document protégé par une stratégie est récupéré, vous pouvez l’inspecter.

**Obtenir des informations sur le document protégé par une politique**

Une fois que vous avez inspecté un document PDF protégé par une politique, vous pouvez obtenir des informations à son sujet. Vous pouvez, par exemple, déterminer la politique utilisée pour protéger le document.

Si vous sécurisez un document avec une politique qui appartient à Mes politiques, puis appelez `RMInspectResult.getPolicysetName` ou `RMInspectResult.getPolicysetId`, une valeur nulle est renvoyée.

Si le document est protégé à l’aide d’une politique contenue dans un jeu de politiques (autre que Mes politiques), alors `RMInspectResult.getPolicysetName` et `RMInspectResult.getPolicysetId` renvoient des chaînes valides.

**Voir également**

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Inspecter des documents PDF protégés par une politique à l’aide de l’API Java {#inspect-policy-protected-pdf-documents-using-the-java-api}

Pour inspecter un document PDF protégé par une politique à l’aide de l’API du service Document Security (Java), procédez comme suit :

1. Incluez les fichiers de projet.

   Incluez les fichiers JAR client, tels que adobe-rightsmanagement-client.jar, dans le chemin de classe de votre projet Java. Pour plus d’informations sur l’emplacement de ces fichiers, voir [Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

1. Créez un objet API client Document Security.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion. (Voir [Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
   * Créez un objet `RightsManagementClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`. 

1. Récupérez un document protégé par une politique à inspecter.

   * Créez un objet `java.io.FileInputStream` qui représente le document PDF protégé par une politique à l’aide de son constructeur. Transmettez une valeur de chaîne qui spécifie l’emplacement du document PDF.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Inspectez le document.

   * Créez un `DocumentManager` en appelant la méthode `RightsManagementClient` de `getDocumentManager` .
   * Inspect du document protégé par une stratégie en appelant la méthode `LicenseManager` de `inspectDocument` . Transmettez l’objet `com.adobe.idp.Document` contenant le document PDF protégé par une politique. Cette méthode renvoie un objet `RMInspectResult` contenant des informations sur le document protégé par une politique.

1. Obtenez des informations sur le document protégé par une politique.

   Pour obtenir des informations sur le document protégé par une politique, appelez la méthode appropriée appartenant à l’objet `RMInspectResult`. Par exemple, pour récupérer le nom de la stratégie, appelez la méthode `RMInspectResult` de `getPolicyName` .

**Exemples de code**

Pour obtenir des exemples de code à l’aide du service Document Security, reportez-vous aux tutoriels de démarrage rapide suivants :

* « Démarrage rapide (mode SOAP) : inspecter des documents PDF protégés par une politique à l’aide de l’API Java »

### Inspecter des documents PDF protégés par une politique à l’aide de l’API de service web {#inspect-policy-protected-pdf-documents-using-the-web-service-api}

Pour inspecter un document PDF protégé par une politique à l’aide de l’API du service Document Security (service web), procédez comme suit :

1. Incluez les fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Veillez à utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` avec l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un objet API client Document Security.

   * Créez un objet `RightsManagementServiceClient` en utilisant son constructeur par défaut.
   * Créez un objet `RightsManagementServiceClient.Endpoint.Address` en utilisant le constructeur `System.ServiceModel.EndpointAddress`. Transmettez une valeur string qui spécifie le WSDL au service AEM Forms (par exemple `http://localhost:8080/soap/services/RightsManagementService?WSDL`). Vous n’avez pas besoin d’utiliser l’attribut `lc_version`. Cet attribut est utilisé lorsque vous créez une référence de service.)
   * Créez un objet `System.ServiceModel.BasicHttpBinding` en obtenant la valeur du champ `RightsManagementServiceClient.Endpoint.Binding`. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez la variable `System.ServiceModel.BasicHttpBinding` de `MessageEncoding` champ à `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.

   * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Récupérez un document protégé par une politique à inspecter.

   * Créez un objet `BLOB` en utilisant son constructeur. L’objet `BLOB` sert à stocker un document PDF à inspecter.
   * Créez un objet `System.IO.FileStream` en appelant son constructeur. Transmettez une valeur de chaîne qui représente l’emplacement du document PDF et son mode d’ouverture.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `System.IO.FileStream`. Vous pouvez déterminer la taille du tableau d’octets en obtenant la variable `System.IO.FileStream` de `Length` .
   * Renseignez le tableau d’octets avec les données de diffusion en appelant la variable `System.IO.FileStream` de `Read` . Transmettez le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’objet `BLOB` en attribuant à son champ `MTOM` le contenu du tableau d’octets.

1. Inspectez le document.

   Inspect du document protégé par une stratégie en appelant la méthode `RightsManagementServiceClient` de `inspectDocument` . Transmettez l’objet `BLOB` contenant le document PDF protégé par une politique. Cette méthode renvoie un objet `RMInspectResult` contenant des informations sur le document protégé par une politique.

1. Obtenez des informations sur le document protégé par une politique.

   Pour obtenir des informations sur le document protégé par une politique, obtenez la valeur du champ approprié qui appartient à l’objet `RMInspectResult`. Par exemple, pour récupérer le nom de la stratégie, obtenez la valeur de la variable `RMInspectResult` de `policyName` champ .

**Exemples de code**

Pour obtenir des exemples de code à l’aide du service Document Security, reportez-vous aux tutoriels de démarrage rapide suivants :

* « Démarrage rapide (MTOM) : inspecter des documents PDF protégés par une politique à l’aide de l’API de service web »
* « Démarrage rapide (SwaRef) : inspecter des documents PDF protégés par une politique à l’aide de l’API de service web »

**Voir également**

[Appeler AEM Forms en utilisant MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Appel d’AEM Forms à l’aide de SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Créer des filigranes {#creating-watermarks}

Les filigranes permettent d’assurer la sécurité d’un document en lʼidentifiant de manière unique et en contrôlant la violation des droits d’auteur. Par exemple, vous pouvez créer et placer un filigrane qui indique Confidentiel sur toutes les pages d’un document. Une fois un filigrane créé, vous pouvez l’inclure dans une politique. En d’autres termes, vous pouvez définir l’attribut de filigrane de la stratégie avec le filigrane nouvellement créé. Une fois qu’une politique contenant un filigrane est appliquée à un document, le filigrane apparaît dans le document protégé par la politique.

>[!NOTE]
>
>Seuls les utilisateurs disposant de droits d’administrateur Document Security peuvent créer des filigranes. En d’autres termes, vous devez spécifier cet utilisateur lorsque vous définissez les paramètres de connexion requis pour créer un objet client de service Document Security.

>[!NOTE]
>
>Pour plus d’informations sur le service Document Security, voir [Références des services pour AEM Forms](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

### Résumé des étapes {#summary_of_steps-8}

Pour créer un filigrane, procédez comme suit :

1. Incluez les fichiers de projet.
1. Créez un objet API client Document Security.
1. Définissez les attributs du filigrane.
1. Enregistrez le filigrane avec le service Document Security.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services web, veillez à inclure les fichiers proxy.

**Créer un objet API client Document Security**

Avant d’effectuer par programmation une opération de service Document Security, vous devez créer un objet client de service Document Security. Si vous utilisez l’API Java, créez un objet `RightsManagementClient`. Si vous utilisez l’API de service web Document Security, créez un objet `RightsManagementServiceService`.

**Définir les attributs du filigrane**

Pour créer un filigrane, vous devez définir des attributs de filigrane. L’attribut name doit toujours être défini. Outre l’attribut name, vous devez définir au moins l’un des attributs suivants :

* Texte personnalisé
* DateIncluded
* UserIdIncluded
* UserNameIncluded

Le tableau suivant répertorie les paires clé-valeur requises lors de la création d’un filigrane à l’aide des services web.

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
   <td><p>Si cette valeur est définie sur « true », la valeur du texte personnalisé doit être spécifiée à l’aide de <code>WaterBackCmd:SRCTEXT</code>.</p></td>
   <td><p>True ou false</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:OPACITY</code></p></td>
   <td><p>Indique l’opacité du filigrane. La valeur par défaut est 0,5 si elle n’est pas spécifiée.</p></td>
   <td><p>Valeur comprise entre 0.0 et 1.0.</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:ROTATION</code></p></td>
   <td><p>Indique la rotation du filigrane. La valeur par défaut est 0 degré.</p></td>
   <td><p>Valeur comprise entre 0 et 359.</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:SCALE</code></p></td>
   <td><p>Si cette valeur est spécifiée, l’attribut <code>WaterBackCmd:IS_SIZE_ENABLED</code> doit être présent et la valeur doit être « true ». Si cet attribut n’est pas spécifié, le comportement par défaut est adapté à la page.</p></td>
   <td><p>Valeur supérieure à 0.0 et inférieure ou égale à 1.0.</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:HORIZ_ALIGN</code></p></td>
   <td><p>Indique l’alignement horizontal du filigrane. La valeur par défaut est « centre ».</p></td>
   <td><p>gauche, centre ou droite</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:VERT_ALIGN</code></p></td>
   <td><p>Indique l’alignement vertical du filigrane. La valeur par défaut est « centre ».</p></td>
   <td><p>haut, centre ou bas</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:IS_USE_BACKGROUND</code></p></td>
   <td><p>Indique si le filigrane est en arrière-plan. La valeur par défaut est false. </p></td>
   <td><p>True ou false</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:IS_SIZE_ENABLED</code></p></td>
   <td><p>Valeur « true » si une échelle personnalisée est spécifiée. Si cette valeur est définie sur « true », SCALE doit également être spécifié. Si cette valeur est définie sur « false », la valeur par défaut est adaptée à la page.</p></td>
   <td><p>True ou false</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:SRCTEXT</code></p></td>
   <td><p>Indique le texte personnalisé d’un filigrane. Si cette valeur est présente, alors l’attribut <code>WaterBackCmd:IS_CUSTOMTEXT_ENABLED</code> doit également être présent et défini sur « true ».</p></td>
   <td><p>True ou false</p></td>
  </tr>
 </tbody>
</table>

L’un des attributs suivants doit être défini pour tous les filigranes :

* `WaterBackCmd:IS_USERNAME_ENABLED`
* `WaterBackCmd:IS_USERID_ENABLED`
* `WaterBackCmd:IS_CURRENTDATE_ENABLED`
* `WaterBackCmd:IS_CUSTOMTEXT_ENABLED`

Tous les autres attributs sont facultatifs.

**Enregistrer le filigrane**

Un nouveau filigrane doit être enregistré auprès du service Document Security pour pouvoir être utilisé. Une fois quʼun filigrane est enregistré, vous pouvez l’utiliser dans les politiques.

**Voir également**

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Appliquer des politiques à des documents PDF](protecting-documents-policies.md#applying-policies-to-pdf-documents)

### Créer des filigranes à l’aide de l’API Java {#create-watermarks-using-the-java-api}

Créer un filigrane à l’aide de l’API Document Security (Java) :

1. Incluez les fichiers de projet.

   Inclure les fichiers JAR client, tels que `adobe-rightsmanagement-client.jar`, dans le chemin de classe de votre projet Java.

1. Créez un objet API client Document Security.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `RightsManagementClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`. 

1. Définir les attributs du filigrane

   * Créez un `Watermark` en appelant la méthode `InfomodelObjectFactory` statique de l’objet `createWatermark` . Cette méthode renvoie un objet `Watermark`.
   * Définissez l’attribut name du filigrane en appelant la variable `Watermark` de `setName` et transmission d’une valeur string qui spécifie le nom de la stratégie.
   * Définissez l’attribut d’arrière-plan du filigrane en appelant la fonction `Watermark` de `setBackground` méthode et transmission `true`. En définissant cet attribut, le filigrane apparaît à l’arrière-plan du document.
   * Définissez l’attribut de texte personnalisé du filigrane en appelant la fonction `Watermark` de `setCustomText` et transmission d’une valeur string qui représente le texte du filigrane.
   * Définissez l’attribut d’opacité du filigrane en appelant la variable `Watermark` de `setOpacity` et transmettre une valeur entière qui spécifie le niveau d’opacité. Une valeur de 100 indique que le filigrane est complètement opaque et une valeur de 0 indique que le filigrane est complètement transparent.

1. Enregistrez le filigrane.

   * Créez un `WatermarkManager` en appelant la méthode `RightsManagementClient` de `getWatermarkManager` . Cette méthode renvoie un objet `WatermarkManager`.
   * Enregistrez le filigrane en appelant la méthode `WatermarkManager` de `registerWatermark` et transmission de la méthode `Watermark` qui représente le filigrane à enregistrer. Cette méthode renvoie une valeur string qui représente la valeur d’identification du filigrane.

**Exemples de code**

Pour obtenir des exemples de code à l’aide du service Document Security, reportez-vous aux tutoriels de démarrage rapide suivants :

* « Démarrage rapide (mode SOAP) : créer un filigrane à l’aide de l’API Java »

### Créer des filigranes à l’aide de l’API de service Web {#create-watermarks-using-the-web-service-api}

Créez un filigrane à l’aide de l’API Document Security (service Web) :

1. Créez un objet API client Document Security.

   Créez un projet Microsoft .NET qui utilise MTOM. Veillez à utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` avec l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un objet API client Document Security.

   * Créez un objet `RightsManagementServiceClient` en utilisant son constructeur par défaut.
   * Créez un objet `RightsManagementServiceClient.Endpoint.Address` en utilisant le constructeur `System.ServiceModel.EndpointAddress`. Transmettez une valeur string qui spécifie le WSDL au service AEM Forms (par exemple `http://localhost:8080/soap/services/RightsManagementService?WSDL`). Vous n’avez pas besoin d’utiliser l’attribut `lc_version`. Cet attribut est utilisé lorsque vous créez une référence de service.)
   * Créez un objet `System.ServiceModel.BasicHttpBinding` en obtenant la valeur du champ `RightsManagementServiceClient.Endpoint.Binding`. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez la variable `System.ServiceModel.BasicHttpBinding` de `MessageEncoding` champ à `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.

   * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Définissez les attributs du filigrane.

   * Créez un objet `WatermarkSpec` en appelant le constructeur `WatermarkSpec`.
   * Définissez le nom du filigrane en attribuant une valeur de chaîne à la variable `WatermarkSpec` de `name` membre de données.
   * Définition du filigrane `id` en attribuant une valeur de chaîne à la variable `WatermarkSpec` de `id` membre de données.
   * Pour chaque propriété de filigrane à définir, créez un objet `MyMapOf_xsd_string_To_xsd_anyType_Item` distinct.
   * Définissez la valeur de clé en attribuant une valeur à la variable `MyMapOf_xsd_string_To_xsd_anyType_Item` de `key` membre de données (par exemple, `WaterBackCmd:OPACITY)`.
   * Définissez la valeur en attribuant une valeur à la variable `MyMapOf_xsd_string_To_xsd_anyType_Item` de `value` membre de données (par exemple, `.25`).
   * Créez un objet `MyArrayOf_xsd_anyType`. Pour chaque `MyMapOf_xsd_string_To_xsd_anyType_Item` , appelez l’objet `MyArrayOf_xsd_anyType` de `Add` . Transmettez l’objet `MyMapOf_xsd_string_To_xsd_anyType_Item`.
   * Attribuez le `MyArrayOf_xsd_anyType` vers l’objet `WatermarkSpec` de `values` membre de données.

1. Enregistrez le filigrane.

   Enregistrez le filigrane en appelant la méthode `RightsManagementServiceClient` de `registerWatermark` et transmission de la méthode `WatermarkSpec` qui représente le filigrane à enregistrer.

**Exemples de code**

Pour obtenir des exemples de code à l’aide du service Document Security, reportez-vous aux tutoriels de démarrage rapide suivants :

* « Démarrage rapide (MTOM) : créer un filigrane à l’aide de l’API de service web »
* « Démarrage rapide (SwaRef) : créer un filigrane à l’aide de l’API de service web »

**Voir également**

[Appeler AEM Forms en utilisant MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Appel d’AEM Forms à l’aide de SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Modifier des filigranes {#modifying-watermarks}

Vous pouvez modifier un filigrane existant à l’aide de l’API Java Document Security ou de l’API de service Web. Pour modifier un filigrane existant, vous devez le récupérer, modifier ses attributs, puis le mettre à jour sur le serveur. Supposons, par exemple, que vous récupériez un filigrane et que vous modifiiez son attribut d’opacité. Avant que la modification ne prenne effet, vous devez mettre à jour le filigrane.

Lorsque vous modifiez un filigrane, la modification a une incidence sur les documents futurs auxquels le filigrane est appliqué. En d’autres termes, les documents PDF existants contenant le filigrane ne sont pas affectés.

>[!NOTE]
>
>Seuls les utilisateurs disposant de privilèges d’administration Document Security peuvent modifier les filigranes. En d’autres termes, vous devez spécifier cet utilisateur lorsque vous définissez les paramètres de connexion requis pour créer un objet client de service Document Security.

>[!NOTE]
>
>Pour plus d’informations sur le service Document Security, voir [Références des services pour AEM Forms](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

### Résumé des étapes {#summary_of_steps-9}

Pour modifier un filigrane, procédez comme suit :

1. Incluez les fichiers de projet.
1. Créez un objet API client Document Security.
1. Récupérez le filigrane à modifier.
1. Définissez les attributs du filigrane.
1. Mettez à jour le filigrane.

**Inclure les fichiers du projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services web, veillez à inclure les fichiers proxy.

**Créer un objet API client Document Security**

Avant d’effectuer par programmation une opération de service Document Security, vous devez créer un objet client de service Document Security. Si vous utilisez l’API Java, créez un objet `DocumentSecurityClient`. Si vous utilisez l’API du service Web Document Security, créez un objet `DocumentSecurityServiceService`.

**Récupérer le filigrane à modifier**

Pour modifier un filigrane, vous devez récupérer un filigrane existant. Vous pouvez récupérer un filigrane en spécifiant son nom ou sa valeur d’identifiant.

**Définir les attributs du filigrane**

Pour modifier un filigrane existant, modifiez la valeur d’un ou de plusieurs attributs du filigrane. Lors de la mise à jour par programmation d’un filigrane à l’aide d’un service Web, vous devez définir tous les attributs qui ont été définis à l’origine, même si la valeur ne change pas. Par exemple, supposons que les attributs de filigrane suivants soient définis : `WaterBackCmd:IS_USERID_ENABLED`, `WaterBackCmd:IS_CUSTOMTEXT_ENABLED`, `WaterBackCmd:OPACITY` et `WaterBackCmd:SRCTEXT`. Bien que le seul attribut que vous souhaitez modifier soit `WaterBackCmd:OPACITY`, vous devez également définir les autres valeurs.

>[!NOTE]
>
>Lorsque vous utilisez l’API Java pour modifier un filigrane, vous n’avez pas besoin de spécifier tous les attributs. Définissez l’attribut du filigrane que vous souhaitez modifier.

>[!NOTE]
>
>Pour plus d’informations sur les noms des attributs du filigrane, voir [Créer des filigranes](protecting-documents-policies.md#creating-watermarks).

**Mettre à jour le filigrane**

Après avoir modifié les attributs d’un filigrane, vous devez le mettre à jour.

**Voir également**

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Créer des filigranes](protecting-documents-policies.md#creating-watermarks)

### Modifier des filigranes en utilisant l’API Java {#modify-watermarks-using-the-java-api}

Modifiez un filigrane en utilisant l’API Document Security (Java) :

1. Incluez les fichiers de projet.

   Incluez les fichiers JAR client, tels que adobe-rightsmanagement-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un objet API client Document Security.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `DocumentSecurityClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`. 

1. Récupérez le filigrane à modifier.

   Créez un `WatermarkManager` en appelant la méthode `DocumentSecurityClient` de `getWatermarkManager` et transmettez une valeur string qui spécifie le nom du filigrane. Cette méthode renvoie un objet `Watermark` qui représente le filigrane à modifier.

1. Définissez les attributs du filigrane.

   Définissez l’attribut d’opacité du filigrane en appelant la variable `Watermark` de `setOpacity` et transmettre une valeur entière qui spécifie le niveau d’opacité. Une valeur de 100 indique que le filigrane est complètement opaque et une valeur de 0 indique que le filigrane est complètement transparent.

   >[!NOTE]
   >
   >Cet exemple ne modifie que l’attribut d’opacité.

1. Mettez à jour le filigrane.

   * Mettez à jour le filigrane en appelant la méthode `WatermarkManager` de `updateWatermark` et transmettez la méthode `Watermark` dont l’attribut a été modifié.

**Exemples de code**

Pour des exemples de code utilisant le service Document Security, reportez-vous à la section Démarrage rapide (mode SOAP) : modifier un filigrane à l’aide de l’API Java.

### Modifier des filigranes à l’aide de l’API Web Service {#modify-watermarks-using-the-web-service-api}

Modifiez un filigrane à l’aide de l’API de Document Security (Web Service) :

1. Incluez les fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Veillez à utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` avec l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un objet API client Document Security.

   * Créez un objet `DocumentSecurityServiceClient` en utilisant son constructeur par défaut.
   * Créez un objet `RightsManagementServiceClient.Endpoint.Address` en utilisant le constructeur `System.ServiceModel.EndpointAddress`. Transmettez une valeur string qui spécifie le WSDL au service AEM Forms (par exemple `http://localhost:8080/soap/services/DocumentSecurityService?WSDL`). Vous n’avez pas besoin d’utiliser l’attribut `lc_version`. Cet attribut est utilisé lorsque vous créez une référence de service.)
   * Créez un objet `System.ServiceModel.BasicHttpBinding` en obtenant la valeur du champ `DocumentSecurityServiceClient.Endpoint.Binding`. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez la variable `System.ServiceModel.BasicHttpBinding` de `MessageEncoding` champ à `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.

   * Affectez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Récupérez le filigrane à modifier.

   Récupérez le filigrane à modifier en appelant la fonction `DocumentSecurityServiceClient` de `getWatermarkByName` . Transmettez une valeur string qui spécifie le nom du filigrane. Cette méthode renvoie un objet `WatermarkSpec` qui représente le filigrane à modifier.

1. Définissez les attributs du filigrane.

   * Pour chaque propriété de filigrane à mettre à jour, créez un objet `MyMapOf_xsd_string_To_xsd_anyType_Item` à part.
   * Définissez la valeur de clé en attribuant une valeur à la variable `MyMapOf_xsd_string_To_xsd_anyType_Item` de `key` membre de données (par exemple, `WaterBackCmd:OPACITY)`.
   * Définissez la valeur en attribuant une valeur à la variable `MyMapOf_xsd_string_To_xsd_anyType_Item` de `value` membre de données (par exemple, `.50`).
   * Créez un objet `MyArrayOf_xsd_anyType`. Pour chaque `MyMapOf_xsd_string_To_xsd_anyType_Item` , appelez l’objet `MyArrayOf_xsd_anyType` de `Add` . Transmettez l’objet `MyMapOf_xsd_string_To_xsd_anyType_Item`.
   * Attribuez le `MyArrayOf_xsd_anyType` vers l’objet `WatermarkSpec` de `values` membre de données.

1. Mettez à jour le filigrane.

   Mettez à jour le filigrane en appelant la méthode `DocumentSecurityServiceClient` de `updateWatermark` et transmission de la méthode `WatermarkSpec` qui représente le filigrane à modifier.

**Exemples de code**

Pour obtenir des exemples de code à l’aide du service Document Security, reportez-vous au tutoriel de démarrage rapide suivant :

* « Démarrage rapide (MTOM) : modifier un filigrane à l’aide de l’API de service web »

## Rechercher des événements {#searching-for-events}

Le service Rights Management effectue le suivi d’actions spécifiques au fur et à mesure qu’elles se produisent, telles que l’application d’une politique à un document, l’ouverture d’un document protégé par une politique et la révocation de l’accès aux documents. Le contrôle des événements doit être activé pour le service Rights Management. Dans le cas contraire, les événements ne seront pas suivis.

Les événements appartiennent à l’une des catégories suivantes :

* Les événements d’administrateur sont des actions liées à un administrateur, comme la création d’un compte administrateur.
* Les événements de document sont des actions liées à un document, telles que la fermeture d’un document protégé par une politique.
* Les événements de stratégie sont des actions liées à une stratégie, comme la création d’une stratégie.
* Les événements de service sont des actions liées au service Rights Management, telles que la synchronisation avec le répertoire des utilisateurs.

Vous pouvez rechercher des événements spécifiques à l’aide de l’API Java Rights Management ou de l’API de service web. En recherchant des événements, vous pouvez effectuer des tâches, comme la création dʼun fichier journal de certains événements.

>[!NOTE]
>
>Pour plus d’informations sur le service Rights Management, consultez la section [Références des services pour AEM Forms](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

### Résumé des étapes {#summary_of_steps-10}

Pour rechercher un événement Rights Management, procédez comme suit :

1. Incluez les fichiers de projet.
1. Créez un objet API client Rights Management.
1. Spécifiez l’événement à rechercher.
1. Recherchez l’événement.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services web, veillez à inclure les fichiers proxy.

**Créer un objet API client Rights Management**

Avant de pouvoir effectuer par programmation une opération de service Rights Management, vous devez créer un objet client de service Rights Management. Si vous utilisez l’API Java, créez un objet `DocumentSecurityClient`. Si vous utilisez l’API de service web Rights Management, créez un objet `DocumentSecurityServiceService`.

**Définir les événements à rechercher**

Indiquez l’événement à rechercher. Vous pouvez, par exemple, rechercher l’événement de création de politique qui se produit lors de la création d’une politique.

**Rechercher l’événement**

Une fois que vous avez spécifié l’événement à rechercher, vous pouvez utiliser l’API Java Rights Management ou l’API de service web Rights Management pour rechercher l’événement.

**Voir également**

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Rechercher des événements à l’aide de l’API Java {#search-for-events-using-the-java-api}

Pour rechercher des événements à l’aide de l’API Rights Management (Java), procédez comme suit :

1. Inclure les fichiers du projet

   Incluez les fichiers JAR client, tels que adobe-rightsmanagement-client.jar, dans le chemin de classe de votre projet Java.

1. Créer un objet API client Rights Management

   Créez un objet `DocumentSecurityClient` en utilisant son constructeur et en transmettant un objet `ServiceClientFactory` contenant des propriétés de connexion.

1. Définir les événements à rechercher

   * Créez un `EventManager` en appelant la méthode `DocumentSecurityClient` de `getEventManager` . Cette méthode renvoie un objet `EventManager`.
   * Créez un objet `EventSearchFilter` en appelant son constructeur.
   * Indiquez l’événement pour lequel effectuer une recherche en appelant la variable `EventSearchFilter` de `setEventCode` et transmission d’un membre de données statique qui appartient à la méthode `EventManager` qui représente l’événement pour lequel effectuer une recherche. Par exemple, pour rechercher l’événement de création de politique, transmettez `EventManager.POLICY_CREATE_EVENT`.

   >[!NOTE]
   >
   >Vous pouvez définir des critères de recherche supplémentaires en appelant les méthodes de l’objet `EventSearchFilter`. Par exemple, appelez la méthode `setUserName` pour spécifier un utilisateur associé à l’événement.

1. Rechercher l’événement

   Recherchez l’événement en appelant la fonction `EventManager` de `searchForEvents` et transmission de la méthode `EventSearchFilter` qui définit les critères de recherche d’événement. Cette méthode renvoie un tableau d’objets `Event`.

**Exemples de code**

Pour obtenir des exemples de code à l’aide du service Rights Management, reportez-vous aux tutoriels de démarrage rapide suivants :

* « Démarrage rapide ( SOAP) : rechercher des événements à l’aide de l’API Java »

### Rechercher des événements à l’aide de l’API de service web {#search-for-events-using-the-web-service-api}

Pour rechercher des événements à l’aide de l’API Rights Management (service web), procédez comme suit :

1. Inclure les fichiers du projet

   Créez un projet Microsoft .NET qui utilise MTOM. Veillez à utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Créer un objet API client Rights Management

   * Créez un objet `DocumentSecurityServiceClient` en utilisant son constructeur par défaut.
   * Créez un objet `DocumentSecurityServiceClient.Endpoint.Address` en utilisant le constructeur `System.ServiceModel.EndpointAddress`. Transmettez une valeur string qui spécifie le WSDL au service AEM Forms (par exemple `http://localhost:8080/soap/services/RightsManagementService?WSDL`). Vous n’avez pas besoin d’utiliser l’attribut `lc_version`. Cet attribut est utilisé lorsque vous créez une référence de service.)
   * Créez un objet `System.ServiceModel.BasicHttpBinding` en obtenant la valeur du champ `DocumentSecurityServiceClient.Endpoint.Binding`. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez la variable `System.ServiceModel.BasicHttpBinding` de `MessageEncoding` champ à `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.

   * Affectez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Définir les événements à rechercher

   * Créez un objet `EventSpec` en utilisant son constructeur.
   * Spécifiez le début de la période au cours de laquelle l’événement s’est produit en définissant la variable `EventSpec` de `firstTime.date` membre de données avec `DataTime` qui représente le début de la période au cours de laquelle l’événement s’est produit.
   * Attribuer la valeur `true` à la fonction `EventSpec` de `firstTime.dateSpecified` membre de données.
   * Indiquez la fin de la période au cours de laquelle l’événement s’est produit en définissant la variable `EventSpec` de `lastTime.date` membre de données avec `DataTime` qui représente la fin de la période au cours de laquelle l’événement s’est produit.
   * Attribuer la valeur `true` à la fonction `EventSpec` de `lastTime.dateSpecified` membre de données.
   * Définissez l’événement à rechercher en attribuant une valeur de chaîne à la variable `EventSpec` de `eventCode` membre de données. Le tableau suivant répertorie les valeurs numériques que vous pouvez attribuer à cette propriété :

   <table>
    <thead>
    <tr>
    <th><p>Type d’événement</p></th>
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

1. Rechercher l’événement

   Recherchez l’événement en appelant la fonction `DocumentSecurityServiceClient` de `searchForEvents` et transmission de la méthode `EventSpec` qui représente l’événement pour lequel effectuer une recherche et le nombre maximal de résultats. Cette méthode renvoie une collection `MyArrayOf_xsd_anyType` où chaque élément est une instance `AuditSpec`. En utilisant une instance `AuditSpec`, vous pouvez obtenir des informations sur l’événement, telles que l’heure à laquelle il s’est produit. L’instance `AuditSpec` contient un membre de données `timestamp` qui spécifie ces informations.

**Exemples de code**

Pour obtenir des exemples de code à l’aide du service Rights Management, reportez-vous aux tutoriels de démarrage rapide suivants :

* « Démarrage rapide (MTOM) : rechercher des événements à l’aide de l’API de service web »
* « Démarrage rapide (SwaRef) : rechercher des événements à l’aide de l’API de service web »

**Voir également**

[Appeler AEM Forms en utilisant MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Appel d’AEM Forms à l’aide de SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Appliquer des politiques à des documents Word {#applying-policies-to-word-documents}

Outre les documents PDF, le service Rights Management prend en charge d’autres formats de document, tels que les documents Microsoft Word (fichier DOC) et d’autres formats de fichier Microsoft Office. Vous pouvez, par exemple, appliquer une stratégie à un document Word pour le protéger. En appliquant une politique à un document Word, vous restreignez l’accès au document. Vous ne pouvez pas appliquer de politique à un document si celui-ci est déjà protégé par une autre politique.

Vous pouvez surveiller l’utilisation d’un document Word protégé par une politique après sa distribution. En d’autres termes, vous pouvez voir comment le document est utilisé et qui l’utilise. Par exemple, vous pouvez savoir quand un utilisateur a ouvert le document.

>[!NOTE]
>
>Pour plus d’informations sur le service Document Security, voir [Références des services pour AEM Forms](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

### Résumé des étapes {#summary_of_steps-11}

Pour appliquer une politique à un document Word, procédez comme suit :

1. Incluez les fichiers de projet.
1. Créez un objet API client Document Security.
1. Récupérez un document Word auquel une politique est appliquée.
1. Appliquez une politique existante au document Word.
1. Enregistrez le document Word protégé par une politique.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services web, veillez à inclure les fichiers proxy.

**Créer un objet API client Document Security**

Avant d’effectuer une opération de service Document Security par programme, vous devez créer un objet client de service Document Security.

**Récupérer un document Word**

Récupérez un document Word pour appliquer une stratégie. Une fois que vous avez appliqué une politique au document Word, les utilisateurs sont restreints lors de l’utilisation du document. Par exemple, si la politique ne permet pas l’ouverture du document hors ligne, les utilisateurs doivent être en ligne pour pouvoir ouvrir le document.

**Appliquer une politique existante au document Word**

Pour appliquer une politique à un document Word, vous devez référencer une politique existante et spécifier à quel jeu de politiques elle appartient. L’utilisateur qui définit les propriétés de connexion doit avoir accès à la politique spécifiée. Dans le cas contraire, une exception se produit.

**Enregistrer le document Word**

Une fois que le service Document Security a appliqué une politique à un document Word, vous pouvez enregistrer le document Word protégé par une politique en tant que fichier DOC.

**Voir également**

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Révoquer l’accès à des documents](protecting-documents-policies.md#revoking-access-to-documents)

### Appliquer une politique à un document Word à l’aide de l’API Java {#apply-a-policy-to-a-word-document-using-the-java-api}

Appliquez une politique à un document Word à l’aide de l’API Document Security (Java) :

1. Incluez les fichiers de projet.

   Incluez les fichiers JAR client, tels que adobe-rightsmanagement-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un objet API client Document Security.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `DocumentSecurityClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`. 

1. Récupérez un document Word.

   * Créez un objet `java.io.FileInputStream` qui représente le document Word en utilisant son constructeur et en transmettant une valeur string qui spécifie l’emplacement du document Word.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Appliquez une politique existante au document Word.

   * Créez un `DocumentManager` en appelant la méthode `DocumentSecurityClient` de `getDocumentManager` .
   * Appliquez une stratégie au document Word en appelant la méthode `DocumentManager` de `protectDocument` et transmission des valeurs suivantes :

      * Objet `com.adobe.idp.Document` contenant le document Word auquel s’applique la politique.
      * Une valeur de chaîne indiquant le nom du document.
      * Une valeur de chaîne représentant le nom du jeu de politiques auquel la politique appartient. Vous pouvez définir une valeur `null` qui entraîne le jeu de politiques `MyPolicies` utilisé.
      * Une valeur de chaîne qui spécifie le nom de la politique.
      * Une valeur de chaîne représentant le nom du domaine User Manager de l’utilisateur qui est l’éditeur du document. Cette valeur de paramètre est facultative et peut être une valeur null (si ce paramètre est null, la valeur de paramètre suivante doit être null).
      * Une valeur de chaîne représentant le nom canonique de l’utilisateur User Manager qui est l’éditeur du document. Cette valeur de paramètre est facultative et peut être `null` (si ce paramètre est `null`, alors la valeur du paramètre précédent doit être `null`).
      * `com.adobe.livecycle.rightsmanagement.Locale` représentant le paramètre régional utilisé pour sélectionner le modèle MS Office. Cette valeur de paramètre est facultative et vous pouvez spécifier `null`.

     La méthode `protectDocument` renvoie un objet `RMSecureDocumentResult` contenant le document Word protégé par une politique.

1. Enregistrez le document Word.

   * Appeler la variable `RMSecureDocumentResult` de `getProtectedDoc` pour obtenir le document Word protégé par une stratégie. Cette méthode renvoie un objet `com.adobe.idp.Document`.
   * Créez un objet `java.io.File` et assurez-vous que l’extension du fichier est DOC.
   * Appeler la variable `com.adobe.idp.Document` de `copyToFile` pour copier le contenu de la méthode `Document` dans le fichier (assurez-vous d’utiliser la variable `Document` qui a été renvoyé par l’objet `getProtectedDoc` ).

**Exemples de code**

Pour obtenir des exemples de code à l’aide du service Document Security, reportez-vous au tutoriel de démarrage rapide suivant :

* « Démarrage rapide (mode SOAP) : appliquer une politique à un document Word à l’aide de l’API Java »

### Appliquer une politique à un document Word à l’aide de l’API Web Service {#apply-a-policy-to-a-word-document-using-the-web-service-api}

Appliquez une politique à un document Word à l’aide de l’API Document Security (Web Service) :

1. Incluez les fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Veillez à utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/DocumentSecurityService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` avec l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un objet API client Document Security.

   * Créez un objet `DocumentSecurityServiceClient` en utilisant son constructeur par défaut.
   * Créez un objet `DocumentSecurityServiceClient.Endpoint.Address` en utilisant le constructeur `System.ServiceModel.EndpointAddress`. Transmettez une valeur string qui spécifie le WSDL au service AEM Forms (par exemple `http://localhost:8080/soap/services/DocumentSecurityService?WSDL`). Vous n’avez pas besoin d’utiliser l’attribut `lc_version`. Cet attribut est utilisé lorsque vous créez une référence de service.)
   * Créez un objet `System.ServiceModel.BasicHttpBinding` en obtenant la valeur du champ `DocumentSecurityServiceClient.Endpoint.Binding`. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez la variable `System.ServiceModel.BasicHttpBinding` de `MessageEncoding` champ à `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.

   * Affectez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Récupérez un document Word.

   * Créez un objet `BLOB` en utilisant son constructeur. L’objet `BLOB` sert à stocker un document Word auquel une politique est appliquée.
   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur de chaîne représentant l’emplacement du document Word et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `System.IO.FileStream`. Déterminez la taille du tableau d’octets en obtenant la variable `System.IO.FileStream` de `Length` .
   * Renseignez le tableau d’octets avec les données de diffusion en appelant la variable `System.IO.FileStream` de `Read` . Transmettez le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’objet `BLOB` en attribuant à son champ `MTOM` le contenu du tableau d’octets.

1. Appliquez une politique existante au document Word.

   Appliquez une stratégie au document Word en appelant la méthode `DocumentSecurityServiceClient` de `protectDocument` et transmission des valeurs suivantes :

   * Objet `BLOB` contenant le document Word auquel s’applique la politique.
   * Une valeur de chaîne indiquant le nom du document.
   * Une valeur de chaîne représentant le nom du jeu de politiques auquel la politique appartient. Vous pouvez définir une valeur `null` qui entraîne le jeu de politiques `MyPolicies` utilisé.
   * Une valeur de chaîne qui spécifie le nom de la politique.
   * Une valeur de chaîne représentant le nom du domaine User Manager de l’utilisateur qui est l’éditeur du document. Cette valeur de paramètre est facultative et peut être définie sur null (si ce paramètre est défini sur null, la valeur du paramètre suivant doit être `null`).
   * Une valeur de chaîne représentant le nom canonique de l’utilisateur User Manager qui est l’éditeur du document. Cette valeur de paramètre est facultative et peut être définie sur null (si ce paramètre est défini sur null, la valeur du paramètre précédent doit être `null`).
   * Une valeur `RMLocale` spécifiant la valeur du paramètre régional (par exemple, `RMLocale.en`).
   * Un paramètre de sortie de chaîne utilisé pour stocker la valeur de l’identifiant de politique.
   * Un paramètre de sortie de chaîne utilisé pour stocker la valeur de l’identifiant protégée par une politique.
   * Paramètre de sortie de chaîne utilisé pour stocker le type MIME (par exemple `application/doc`).

   La méthode `protectDocument` renvoie un objet `BLOB` contenant le document Word protégé par une politique.

1. Enregistrez le document Word.

   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur de chaîne représentant l’emplacement du document Word protégé par une politique.
   * Créez un tableau d’octets qui stocke le contenu des données de l’objet `BLOB` renvoyé par la méthode `protectDocument`. Renseignez le tableau d’octets en obtenant la valeur de la variable `BLOB` de `MTOM` membre de données.
   * Créez un objet `System.IO.BinaryWriter` en utilisant son constructeur et en transmettant l’objet `System.IO.FileStream`.
   * Ecrivez le contenu du tableau d’octets dans un fichier Word en appelant la méthode `System.IO.BinaryWriter` de `Write` et transmission du tableau d’octets.

**Exemples de code**

Pour obtenir des exemples de code à l’aide du service Document Security, reportez-vous au tutoriel de démarrage rapide suivant :

* « Démarrage rapide (MTOM) : appliquer une politique à un document Word à l’aide de l’API de service web »

## Supprimer des politiques de documents Word {#removing-policies-from-word-documents}

Vous pouvez supprimer une stratégie d’un document Word protégé par une stratégie pour supprimer la protection du document. Effectuez cette opération si vous ne souhaitez plus que le document soit protégé par une politique. Si vous souhaitez mettre à jour un document Word protégé par une politique avec une nouvelle politique, au lieu de supprimer la politique et d’ajouter la politique mise à jour, il est préférable de changer de politique.

>[!NOTE]
>
>Pour plus d’informations sur le service Document Security, voir [Référence des services pour AEM Forms](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

### Résumé des étapes {#summary_of_steps-12}

Pour supprimer une politique d’un document Word protégé par une politique, procédez comme suit :

1. Inclure les fichiers du projet
1. Créez un objet API client Document Security.
1. Récupérez un document Word protégé par une politique.
1. Supprimez la politique du document Word.
1. Enregistrez le(s) document(s) Word non sécurisé(s).

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services web, veillez à inclure les fichiers proxy.

**Créer un objet API client Document Security**

Avant d’effectuer par programmation une opération de service Document Security, créez un objet client de service Document Security.

**Récupérer un document Word protégé par une politique**

Récupérez un document Word protégé par une stratégie pour supprimer une stratégie. Si vous tentez de supprimer une politique d’un document Word qui n’est pas protégé par une politique, une exception est générée.

**Supprimer la politique du document Word**

Vous pouvez supprimer une politique d’un document Word protégé par une politique à condition qu’un administrateur soit spécifié dans les paramètres de connexion. Si ce n’est pas le cas, la stratégie utilisée pour protéger un document doit contenir la variable `SWITCH_POLICY` autorisation de supprimer une stratégie d’un document Word. En outre, l’utilisateur spécifié dans les paramètres de connexion AEM Forms doit également disposer de cette autorisation. Dans le cas contraire, une exception est générée.

**Enregistrer le document Word non protégé**

Une fois que le service Document Security a supprimé une politique d’un document Word, vous pouvez enregistrer le document Word non sécurisé au format DOC.

**Voir également**

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Appliquer des politiques à des documents Word](protecting-documents-policies.md#applying-policies-to-word-documents)

### Supprimer une politique d’un document Word à l’aide de l’API Java {#remove-a-policy-from-a-word-document-using-the-java-api}

Pour supprimer une politique d’un document Word protégé par une politique à l’aide de l’API Document Security (Java), procédez comme suit :

1. Inclure les fichiers du projet

   Incluez les fichiers JAR client, tels que adobe-rightsmanagement-client.jar, dans le chemin de classe de votre projet Java.

1. Créer un objet API client Document Security

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `RightsManagementClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`. 

1. Récupérer un document Word protégé par une politique

   * Créez un objet `java.io.FileInputStream` qui représente le document Word protégé par une politique en utilisant son constructeur et en transmettant une valeur de chaîne qui spécifie l’emplacement du document Word.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Supprimer la politique du document Word

   * Créez un `DocumentManager` en appelant la méthode `RightsManagementClient` de `getDocumentManager` .
   * Supprimez une stratégie du document Word en appelant la méthode `DocumentManager` de `removeSecurity` et transmission de la méthode `com.adobe.idp.Document` contenant le document Word protégé par une stratégie. Cette méthode renvoie un objet `com.adobe.idp.Document` qui contient un document Word non sécurisé.

1. Enregistrer le document Word non sécurisé

   * Créez un objet `java.io.File` et assurez-vous que l’extension du fichier est DOC.
   * Appeler la variable `Document` de `copyToFile` pour copier le contenu de la méthode `Document` dans le fichier (assurez-vous d’utiliser la variable `Document` qui a été renvoyé par l’objet `removeSecurity` ).

**Exemples de code**

Pour obtenir des exemples de code à l’aide du service Document Security, reportez-vous au tutoriel de démarrage rapide suivant :

* « Démarrage rapide (mode SOAP) : supprimer une politique d’un document Word à l’aide de l’API Java »

### Supprimer une politique d’un document Word à l’aide de l’API de service web {#remove-a-policy-from-a-word-document-using-the-web-service-api}

Pour supprimer une politique d’un document Word protégé par une politique en utilisant l’API Document Security (service web), procédez comme suit :

1. Inclure les fichiers du projet

   Créez un projet Microsoft .NET qui utilise MTOM. Veillez à utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Créer un objet API client Document Security

   * Créez un objet `RightsManagementServiceClient` en utilisant son constructeur par défaut.
   * Créez un objet `RightsManagementServiceClient.Endpoint.Address` en utilisant le constructeur `System.ServiceModel.EndpointAddress`. Transmettez une valeur string qui spécifie le WSDL au service AEM Forms (par exemple `http://localhost:8080/soap/services/RightsManagementService?WSDL`). Vous n’avez pas besoin d’utiliser l’attribut `lc_version`. Cet attribut est utilisé lorsque vous créez une référence de service.)
   * Créez un objet `System.ServiceModel.BasicHttpBinding` en obtenant la valeur du champ `RightsManagementServiceClient.Endpoint.Binding`. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez la variable `System.ServiceModel.BasicHttpBinding` de `MessageEncoding` champ à `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.

   * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Récupérer un document Word protégé par une politique

   * Créez un objet `BLOB` en utilisant son constructeur. L’objet `BLOB` est utilisé pour enregistrer le document Word protégé par une politique et dont la politique est supprimée.
   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur de chaîne représentant l’emplacement du fichier Word et son mode d’ouverture.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `System.IO.FileStream`. Vous pouvez déterminer la taille du tableau d’octets en obtenant la variable `System.IO.FileStream` de `Length` .
   * Renseignez le tableau d’octets avec les données de diffusion en appelant la variable `System.IO.FileStream` de `Read` et transmettre le tableau byte, la position de départ et la longueur du flux à lire.
   * Renseignez l’objet `BLOB` en attribuant le contenu du tableau d’octets à son champ `MTOM`.

1. Supprimer la politique du document Word

   Supprimez la stratégie du document Word en appelant la méthode `RightsManagementServiceClient` de `removePolicySecurity` et transmission de la méthode `BLOB` contenant le document Word protégé par une stratégie. Cette méthode renvoie un objet `BLOB` qui contient un document Word non sécurisé.

1. Enregistrer le document Word non sécurisé

   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du fichier Word non protégé.
   * Créez un tableau d’octets qui stocke le contenu des données de l’objet `BLOB` renvoyé par la méthode `removePolicySecurity`. Renseignez le tableau d’octets en obtenant la valeur de la variable `BLOB` de `MTOM` champ .
   * Créez un objet `System.IO.BinaryWriter` en utilisant son constructeur et en transmettant l’objet `System.IO.FileStream`.

**Exemples de code**

Pour obtenir des exemples de code à l’aide du service Document Security, reportez-vous au tutoriel de démarrage rapide suivant :

* « Démarrage rapide (MTOM) : supprimer une politique d’un document Word à l’aide de l’API de service web »

**Voir également**

[Appeler AEM Forms en utilisant MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
