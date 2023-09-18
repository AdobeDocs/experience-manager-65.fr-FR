---
title: Connecter AEM Forms à Adobe LiveCycle
description: Le connecteur de LiveCycle Adobe Experience Manager (AEM) vous permet de démarrer les services Acrobat LiveCycle ES4 à partir d’AEM applications et de workflows.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
role: Admin
exl-id: 562f8a22-cbab-4915-bc0d-da9bea7d18fa
source-git-commit: ab3d016c7c9c622be361596137b150d8719630bd
workflow-type: tm+mt
source-wordcount: '1026'
ht-degree: 20%

---

# Connecter AEM Forms à Adobe LiveCycle {#connecting-aem-forms-with-adobe-livecycle}

Le connecteur de LiveCycle Adobe Experience Manager (AEM) permet un appel transparent des services Acrobat Adobe LiveCycle ES4 depuis AEM applications web et les workflows. LiveCycle fournit un SDK client riche qui permet aux applications client de démarrer des services LiveCycle à l’aide des API Java™. AEM LiveCycle Connector simplifie l’utilisation de ces API dans l’environnement OSGi.

## Connexion du serveur AEM à Adobe LiveCycle {#connecting-aem-server-to-adobe-livecycle}

AEM LiveCycle Connector fait partie du [package de module complémentaire AEM Forms](/help/forms/using/installing-configuring-aem-forms-osgi.md). Après avoir installé le module complémentaire AEM Forms, procédez comme suit pour ajouter les détails du serveur de LiveCycle à la console web AEM.

1. Dans le gestionnaire de configuration de la console web AEM, recherchez le composant de configuration du SDK client du LiveCycle Adobe.
1. Cliquez sur le composant pour modifier l’URL du serveur de configuration, le nom d’utilisateur et le mot de passe.
1. Vérifiez les paramètres et cliquez sur **Enregistrer**.

Bien que les propriétés soient explicites, les plus importantes sont les suivantes :

* **URL du serveur** : indique l’URL du serveur LiveCycle. Si vous souhaitez que LiveCycle et AEM communiquent via https, démarrez AEM avec la JVM suivante.

  ```java
  argument
   -Djavax.net.ssl.trustStore=<<em>path to LC keystore</em>>
  ```

  option.

* **Nom d’utilisateur**- Indique le nom d’utilisateur du compte utilisé pour établir la communication entre AEM et le LiveCycle. Le compte est un compte utilisateur de LiveCycle disposant des autorisations nécessaires pour démarrer les services Acrobat.
* **Mot de passe** : indique le mot de passe.
* **Nom du service** - Indique les services démarrés à l’aide des informations d’identification fournies dans les champs Nom d’utilisateur et Mot de passe . Par défaut, aucune information d’identification n’est transmise lors du démarrage des services LiveCycle.

## Démarrage de Document Services {#starting-document-services}

Les applications clientes peuvent démarrer par programmation des services LiveCycle à l’aide d’une API Java™, de services web, d’Remoting et de REST. Pour les clients Java™, l’application peut utiliser le SDK LiveCycle. Le SDK LiveCycle fournit une API Java™ pour démarrer ces services à distance. Par exemple, pour convertir un document Microsoft® Word en PDF, le client lance GeneratePDFService. Le flux d’appel se compose des étapes suivantes :

1. Créez une instance ServiceClientFactory .
1. Chaque service fournit une classe de client. Pour démarrer un service, créez une instance client du service.
1. Démarrez le service et traitez le résultat.

AEM LiveCycle Connector simplifie le flux en exposant ces instances client en tant que services OSGi accessibles par des moyens OSGi standard. Le connecteur LiveCycle offre les fonctionnalités suivantes :

* Instances de client en tant que service OSGi : les clients conditionnés en tant que lots OSGI sont répertoriés dans la variable [Liste des services Acrobat](/help/forms/using/aem-livecycle-connector.md#p-document-services-list-p) . Chaque jar client enregistre l’instance client en tant que service OSGi auprès du registre de services OSGi.
* Propagation des informations d’identification de l’utilisateur : les détails de connexion requis pour se connecter au serveur de LiveCycle sont gérés de manière centralisée.
* Service ServiceClientFactory : pour démarrer les processus, l’application cliente peut accéder à l’instance ServiceClientFactory.

### Démarrage via les références de service du registre de services OSGi {#starting-via-service-references-from-osgi-service-registry}

Pour démarrer un service exposé depuis AEM, procédez comme suit :

1. Déterminez les dépendances maven. Ajoutez la dépendance au fichier jar client requis dans votre fichier maven pom.xml. Ajoutez au minimum une dépendance aux jars adobe-livecycle-client et adobe-usermanager-client.

   ```xml
   <dependency>
     <groupId>com.adobe.livecycle</groupId>
     <artifactId>adobe-livecycle-client</artifactId>
     <version>11.0.0</version>
   </dependency>
   <dependency>
     <groupId>com.adobe.livecycle</groupId>
     <artifactId>adobe-usermanager-client</artifactId>
     <version>11.0.0</version>
   </dependency>
   <dependency>
     <groupId>com.adobe.livecycle</groupId>
     <artifactId>adobe-cq-integration-api</artifactId>
     <version>11.0.0</version>
   </dependency>
   ```

   Pour démarrer un service, ajoutez une dépendance Maven correspondante pour le service. Pour obtenir la liste des dépendances, voir [Liste des services Acrobat](/help/forms/using/aem-livecycle-connector.md#p-document-services-list-p). Pour le service Generate PDF, par exemple, ajoutez la dépendance suivante :

   ```xml
   <dependency>
     <groupId>com.adobe.livecycle</groupId>
     <artifactId>adobe-generatepdf-client</artifactId>
     <version>11.0.0</version>
   </dependency>
   ```

1. Obtenez la référence du service. Ajoutez une poignée à l’instance de service. Si vous rédigez une classe Java™, vous pouvez utiliser les annotations de services déclaratifs.

   ```java
   import com.adobe.livecycle.generatepdf.client.GeneratePdfServiceClient;
   import com.adobe.livecycle.generatepdf.client.CreatePDFResult;
   import com.adobe.idp.Document;
   
   @Reference
   GeneratePdfServiceClient generatePDF;
   ...
   
   Resource r = resourceResolver.getResource("/path/tp/docx");
   Document sourceDoc = new Document(r.adaptTo(InputStream.class));
   CreatePDFResult result = generatePDF.createPDF2(
                       sourceDoc,
                       extension, //inputFileExtension
                       null, //fileTypeSettings
                       null, //pdfSettings
                       null, //securitySettings
                       settingsDoc, //settingsDoc
                       null //xmpDoc
               );
   ```

   Le fragment de code ci-dessus lance l’API createPDF de GeneratePdfServiceClient pour convertir un document en PDF. Vous pouvez effectuer un appel similaire dans un JSP à l’aide du code suivant. La principale différence réside dans le fait que le code suivant utilise Sling ScriptHelper pour accéder à GeneratePdfServiceClient.

   ```jsp
   <%@ page import="com.adobe.livecycle.generatepdf.client.GeneratePdfServiceClient" %>
   <%@ page import="com.adobe.livecycle.generatepdf.client.CreatePDFResult" %>
   <%@ page import="com.adobe.idp.Document" %>
   
   GeneratePdfServiceClient generatePDF = sling.getService(GeneratePdfServiceClient.class);
   Document sourceDoc = ...
   CreatePDFResult result = generatePDF.createPDF2(
                       sourceDoc,
                       extension, //inputFileExtension
                       null, //fileTypeSettings
                       null, //pdfSettings
                       null, //securitySettings
                       settingsDoc, //settingsDoc
                       null //xmpDoc
               );
   ```

### Démarrage via ServiceClientFactory {#starting-via-serviceclientfactory}

La classe ServiceClientFactory est parfois requise. pour appeler des processus, par exemple.

```java
import com.adobe.livecycle.dsc.clientsdk.ServiceClientFactoryProvider;
import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;

@Reference
ServiceClientFactoryProvider scfProvider;

...
ServiceClientFactory scf = scfProvider.getDefaultServiceClientFactory();
...
```

## Prise en charge de RunAs {#runas-support}

La plupart des services Acrobat en LiveCycle nécessitent une authentification. Vous pouvez utiliser l’une des options suivantes pour démarrer ces services sans fournir d’informations d’identification explicites dans le code :

### Configuration de la liste autorisée {#allowlist-configuration}

La configuration du SDK client LiveCycle contient un paramètre sur les noms de service. Cette configuration est une liste de services pour lesquels la logique d’appel utilise des informations d’identification d’administrateur prêtes à l’emploi. Par exemple, si vous ajoutez des services DirectoryManager (faisant partie de l’API User Management) à cette liste, tout code client peut directement utiliser le service. En outre, la couche d’appel transmet automatiquement les informations d’identification configurées dans le cadre de la demande envoyée au serveur de LiveCycle.

### RunAsManager {#runasmanager}

Dans le cadre de l’intégration, un nouveau service RunAsManager est fourni. Il vous permet de contrôler par programmation les informations d’identification à utiliser lors de l’appel du serveur de LiveCycle.

```java
import com.adobe.livecycle.dsc.clientsdk.security.PasswordCredential;
import com.adobe.livecycle.dsc.clientsdk.security.PrivilegedAction;
import com.adobe.livecycle.dsc.clientsdk.security.RunAsManager;
import com.adobe.idp.dsc.registry.component.ComponentRegistry;

@Reference
private RunAsManager runAsManager;

List<Component> components = runAsManager.doPrivileged(new PrivilegedAction<List<Component>>() {
            public List<Component> run() {
                return componentRegistry.getComponents();
            }
        });
assertNotNull(components);
```

Si vous souhaitez transmettre des informations d’identification différentes, vous pouvez utiliser la méthode surchargée qui prend une instance PasswordCredential.

```java
PasswordCredential credential = new PasswordCredential("administrator","password");
List<Component> components = runAsManager.doPrivileged(new PrivilegedAction<List<Component>>() {
    public List<Component> run() {
        return componentRegistry.getComponents();
    }
},credential);
```

### Propriété InvocationRequest {#invocationrequest-property}

Si vous appelez un processus ou utilisez directement la classe ServiceClientFactory et créez une InvocationRequest, vous pouvez spécifier une propriété pour indiquer que la couche d’appel doit utiliser les informations d’identification configurées.

```java
import com.adobe.idp.dsc.InvocationResponse
import com.adobe.idp.dsc.InvocationRequest
import com.adobe.livecycle.dsc.clientsdk.ServiceClientFactoryProvider
import com.adobe.idp.dsc.clientsdk.ServiceClientFactory
import com.adobe.livecycle.dsc.clientsdk.InvocationProperties

ServiceClientFactoryProvider scfp = sling.getService(ServiceClientFactoryProvider.class)
ServiceClientFactory serviceClientFactory = scfp.getDefaultServiceClientFactory()
InvocationRequest ir = serviceClientFactory.createInvocationRequest("sample/LetterSubmissionProcess", "invoke", new HashMap(), true);

//Here we are invoking the request with system user
ir.setProperty(InvocationProperties.INVOKER_TYPE,InvocationProperties.INVOKER_TYPE_SYSTEM)

InvocationResponse response = serviceClientFactory.getServiceClient().invoke(ir);
```

## Liste des services Acrobat {#document-services-list}

### Groupe d’API du SDK client Adobe LiveCycle {#adobe-livecycle-client-sdk-api-bundle}

Les services suivants sont disponibles :

* com.adobe.idp.um.api.AuthenticationManager
* com.adobe.idp.um.api.DirectoryManager
* com.adobe.idp.um.api.AuthorizationManager
* com.adobe.idp.dsc.registry.service.ServiceRegistry
* com.adobe.idp.dsc.registry.component.ComponentRegistry

#### Dépendances Maven {#maven-dependencies}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-livecycle-client</artifactId>
  <version>11.0.0</version>
</dependency>
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-usermanager-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Groupe de SDK client Adobe LiveCycle {#adobe-livecycle-client-sdk-bundle}

Les services suivants sont disponibles :

* com.adobe.livecycle.dsc.clientsdk.security.RunAsManager
* com.adobe.livecycle.dsc.clientsdk.ServiceClientFactoryProvider

#### Dépendances Maven {#maven-dependencies-1}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-livecycle-cq-integration-api</artifactId>
  <version>1.1.10</version>
</dependency>
```

### Groupe du client TaskManager Adobe LiveCycle {#adobe-livecycle-taskmanager-client-bundle}

Les services suivants sont disponibles :

* com.adobe.idp.taskmanager.dsc.client.task.TaskManager
* com.adobe.idp.taskmanager.dsc.client.TaskManagerQueryService
* com.adobe.idp.taskmanager.dsc.client.queuemanager.QueueManager
* com.adobe.idp.taskmanager.dsc.client.emailsettings.EmailSettingService
* com.adobe.idp.taskmanager.dsc.client.endpoint.TaskManagerEndpointClient
* com.adobe.idp.taskmanager.dsc.client.userlist.UserlistService

#### Dépendances Maven {#maven-dependencies-2}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-taskmanager-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Groupe client Adobe LiveCycle Workflow {#adobe-livecycle-workflow-client-bundle}

Le service suivant est disponible :

* com.adobe.idp.workflow.client.WorkflowServiceClient

#### Dépendances Maven {#maven-dependencies-3}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-workflow-client-sdk</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Groupe du client Adobe LiveCycle PDF Generator {#adobe-livecycle-pdf-generator-client-bundle}

Le service suivant est disponible :

* com.adobe.livecycle.generatepdf.client.GeneratePdfServiceClient

#### Dépendances Maven {#maven-dependencies-4}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-generatepdf-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Groupe du client Adobe LiveCycle Application Manager {#adobe-livecycle-application-manager-client-bundle}

Les services suivants sont disponibles :

* com.adobe.idp.applicationmanager.service.ApplicationManager
* com.adobe.livecycle.applicationmanager.client.ApplicationManager
* com.adobe.livecycle.design.service.DesigntimeService

#### Dépendances Maven {#maven-dependencies-5}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-applicationmanager-client-sdk</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Groupe du client Assembler Adobe LiveCycle {#adobe-livecycle-assembler-client-bundle}

Le service suivant est disponible :

* com.adobe.livecycle.assembler.client.AssemblerServiceClient

#### Dépendances Maven {#maven-dependencies-6}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-assembler-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Groupe du client d’intégration de données de LiveCycle d’Adobe {#adobe-livecycle-form-data-integration-client-bundle}

Le service suivant est disponible :

* com.adobe.livecycle.formdataintegration.client.FormDataIntegrationClient

#### Dépendances Maven {#maven-dependencies-7}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-formdataintegration-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Groupe du client Adobe LiveCycle Forms {#adobe-livecycle-forms-client-bundle}

Le service suivant est disponible :

* com.adobe.livecycle.formsservice.client.FormsServiceClient

#### Dépendances Maven {#maven-dependencies-8}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-forms-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Groupe du client Adobe LiveCycle Output {#adobe-livecycle-output-client-bundle}

Le service suivant est disponible : 

* com.adobe.livecycle.output.client.OutputClient

#### Dépendances Maven {#maven-dependencies-9}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-output-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Groupe du client Adobe LiveCycle Reader Extensions {#adobe-livecycle-reader-extensions-client-bundle}

Le service suivant est disponible :

* com.adobe.livecycle.readerextensions.client.ReaderExtensionsServiceClient

#### Dépendances Maven {#maven-dependencies-10}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-reader-extensions-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Groupe du client Adobe LiveCycle Rights Manager {#adobe-livecycle-rights-manager-client-bundle}

Les services suivants sont disponibles :

* com.adobe.livecycle.rightsmanagement.client.DocumentManager
* com.adobe.livecycle.rightsmanagement.client.EventManager
* com.adobe.livecycle.rightsmanagement.client.ExternalUserManager
* com.adobe.livecycle.rightsmanagement.client.LicenseManager
* com.adobe.livecycle.rightsmanagement.client.WatermarkManager
* com.adobe.livecycle.rightsmanagement.client.PolicyManager
* com.adobe.livecycle.rightsmanagement.client.AbstractPolicyManager

#### Dépendances Maven {#maven-dependencies-11}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-rightsmanagement-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Groupe du client Adobe LiveCycle Signatures {#adobe-livecycle-signatures-client-bundle}

Le service suivant est disponible : 

* com.adobe.livecycle.signatures.client.SignatureServiceClientInterface

#### Dépendances Maven {#maven-dependencies-12}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-signatures-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Groupe du client Adobe LiveCycle Truststore {#adobe-livecycle-truststore-client-bundle}

Les services suivants sont disponibles :

* com.adobe.truststore.dsc.TrustConfigurationService
* com.adobe.truststore.dsc.CRLService
* com.adobe.truststore.dsc.CredentialService
* com.adobe.truststore.dsc.CertificateService

#### Dépendances Maven {#maven-dependencies-13}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-truststore-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Groupe du client du référentiel de LiveCycle Adobe {#adobe-livecycle-repository-client-bundle}

Les services suivants sont disponibles :

* com.adobe.repository.bindings.ResourceRepository
* com.adobe.repository.bindings.ResourceSynchronizer

#### Dépendances Maven {#maven-dependencies-14}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-repository-client</artifactId>
  <version>11.0.0</version>
</dependency>
```
