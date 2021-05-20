---
title: Gestion des utilisateurs
seo-title: Gestion des utilisateurs
description: Utilisez l’API User Management pour créer des applications clientes capables de gérer les rôles, les autorisations et les entités (qui peuvent être des utilisateurs ou des groupes), ainsi que d’authentifier les utilisateurs.
seo-description: Utilisez l’API User Management pour créer des applications clientes capables de gérer les rôles, les autorisations et les entités (qui peuvent être des utilisateurs ou des groupes), ainsi que d’authentifier les utilisateurs.
uuid: 68d8a0bc-6e3d-4286-ba5c-534dcf58cb84
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 95804bff-9e6f-4807-aae4-790bd9e7cb57
role: Developer
exl-id: d7c5bb84-a988-4b2e-a587-f4e5b50fea58
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '6257'
ht-degree: 4%

---

# Gestion des utilisateurs {#managing-users}

**Les exemples et les exemples de ce document sont réservés à l’environnement AEM Forms on JEE.**

**Gestion des utilisateurs**

Vous pouvez utiliser l’API User Management pour créer des applications clientes qui peuvent gérer des rôles, des autorisations et des entités (qui peuvent être des utilisateurs ou des groupes), ainsi que authentifier des utilisateurs. L’API de gestion des utilisateurs se compose des API AEM Forms suivantes :

* API du service Directory Manager
* API du service Authentication Manager
* API du service Authorization Manager

User Management vous permet d’affecter, de supprimer et de déterminer des rôles et des autorisations. Il vous permet également d’affecter, de supprimer et de interroger des domaines, des utilisateurs et des groupes. Enfin, vous pouvez utiliser User Management pour authentifier les utilisateurs.

Dans [Ajout d’utilisateurs](users.md#adding-users) , vous comprendrez comment ajouter des utilisateurs par programmation. Cette section utilise l’API du service Directory Manager.

Dans [Suppression d’utilisateurs](users.md#deleting-users) , vous comprendrez comment supprimer des utilisateurs par programmation. Cette section utilise l’API du service Directory Manager.

Dans [Gestion des utilisateurs et des groupes](users.md#managing-users-and-groups) , vous comprendrez la différence entre un utilisateur local et un utilisateur d’annuaire, et vous verrez des exemples d’utilisation des API Java et de service Web pour gérer par programmation les utilisateurs et les groupes. Cette section utilise l’API du service Directory Manager.

Dans [Gestion des rôles et des autorisations](users.md#managing-roles-and-permissions), vous découvrirez les rôles et les autorisations du système, ce que vous pouvez faire par programmation pour les augmenter, ainsi que des exemples d’utilisation des API Java et de service Web pour gérer par programmation les rôles et les autorisations. Cette section utilise à la fois l’API du service Directory Manager et l’API du service Authorization Manager.

Dans [Authentification des utilisateurs](users.md#authenticating-users), vous trouverez des exemples d’utilisation des API Java et de service Web pour authentifier par programmation les utilisateurs. Cette section utilise l’API du service Authorization Manager.

**Comprendre le processus d’authentification**

User Management fournit une fonctionnalité d’authentification intégrée et vous permet également de la connecter à votre propre fournisseur d’authentification. Lorsque User Management reçoit une demande d’authentification (par exemple, un utilisateur tente de se connecter), il transmet les informations utilisateur au fournisseur d’authentification pour l’authentification. User Management reçoit les résultats du fournisseur d’authentification après l’authentification de l’utilisateur.

Le diagramme suivant montre l’interaction entre un utilisateur final qui tente de se connecter, User Management et le fournisseur d’authentification.

![mu_mu_umauth_process](assets/mu_mu_umauth_process.png)

Le tableau suivant décrit chaque étape du processus d’authentification.

<table>
 <thead>
  <tr>
   <th><p>Étape</p></th>
   <th><p>Description</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>1</p></td>
   <td><p>Un utilisateur tente de se connecter à un service qui appelle User Management. L’utilisateur spécifie un nom d’utilisateur et un mot de passe. </p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>User Management envoie le nom d’utilisateur et le mot de passe, ainsi que des informations de configuration, au fournisseur d’authentification.</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>Le fournisseur d’authentification se connecte à la boutique d’utilisateurs et authentifie l’utilisateur.</p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>Le fournisseur d’authentification renvoie les résultats à User Management.</p></td>
  </tr>
  <tr>
   <td><p>5</p></td>
   <td><p>User Management permet à l’utilisateur de se connecter ou lui refuse l’accès au produit.</p></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Si le fuseau horaire du serveur est différent du fuseau horaire du client, lors de l’utilisation du WSDL pour le service AEM Forms Generate PDF sur une pile SOAP native à l’aide d’un client .NET sur une grappe de serveurs d’applications WebSphere, l’erreur d’authentification User Management suivante peut se produire :

`[com.adobe.idp.um.webservices.WSSecurityHandler] errorCode:12803 errorCodeHEX:0x3203 message:WSSecurityHandler: UM authenticate returns exception : An error was discovered processing the <wsse:Security> header. (WSSecurityEngine: Invalid timestamp The security semantics of message have expired).`

**Présentation de la gestion des annuaires**

User Management est fourni avec un fournisseur de service d’annuaire (le DirectoryManagerService) qui prend en charge les connexions aux répertoires LDAP. Si votre entreprise utilise un référentiel non LDAP pour stocker des enregistrements d’utilisateurs, vous pouvez créer votre propre fournisseur de services d’annuaire qui fonctionne avec votre référentiel.

Les fournisseurs de services d’annuaire récupèrent les enregistrements d’une banque d’utilisateurs à la demande de User Management. User Management met régulièrement en cache les enregistrements d’utilisateurs et de groupes dans la base de données afin d’améliorer les performances.

Le fournisseur de services d’annuaire peut être utilisé pour synchroniser la base de données User Management avec la banque d’utilisateurs. Cette étape permet de s’assurer que toutes les informations de l’annuaire des utilisateurs et tous les enregistrements d’utilisateur et de groupe sont à jour.

En outre, le service DirectoryManager vous permet de créer et de gérer des domaines. Les domaines définissent différentes bases d’utilisateurs. Les limites d’un domaine sont généralement définies en fonction de la structure de votre organisation ou de la configuration de votre banque d’utilisateurs. Les domaines User Management fournissent des paramètres de configuration que les fournisseurs d’authentification et les fournisseurs de services d’annuaire utilisent.

Dans la configuration XML que User Management exporte, le noeud racine dont la valeur d’attribut est `Domains` contient un élément XML pour chaque domaine défini pour User Management. Chacun de ces éléments contient d’autres éléments qui définissent les aspects du domaine associés à des prestataires spécifiques.

**Comprendre les valeurs objectSID**

Lors de l’utilisation de Principale Directory, il est important de comprendre qu’une valeur `objectSID` n’est pas un attribut unique sur plusieurs domaines. Cette valeur stocke l’identifiant de sécurité d’un objet. Dans un environnement de plusieurs domaines (une arborescence de domaines, par exemple), la valeur `objectSID` peut être différente.

Une valeur `objectSID` changerait si un objet est déplacé d’un domaine Principal Directory vers un autre domaine. Certains objets ont la même valeur `objectSID` n’importe où dans le domaine. Par exemple, les groupes tels que BUILTIN\Administrators, BUILTIN\Power Users, etc., auront la même valeur `objectSID` indépendamment des domaines. Ces valeurs `objectSID` sont bien connues.

## Ajout d’utilisateurs {#adding-users}

Vous pouvez utiliser l’API Directory Manager Service (Java et service Web) pour ajouter des utilisateurs par programmation à AEM Forms. Après avoir ajouté un utilisateur, vous pouvez l’utiliser lors d’une opération de service nécessitant un utilisateur. Par exemple, vous pouvez affecter une tâche au nouvel utilisateur.

### Résumé des étapes {#summary-of-steps}

Pour ajouter un utilisateur, procédez comme suit :

1. Inclure les fichiers de projet.
1. Créez un client DirectoryManagerService .
1. Définissez les informations sur l’utilisateur.
1. Ajoutez l’utilisateur à AEM Forms.
1. Vérifiez que l’utilisateur est ajouté.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, incluez les fichiers proxy.

**Création d’un client DirectoryManagerService**

Avant d’effectuer une opération de service Directory Manager par programmation, créez un client API Directory Manager Service.

**Définition des informations utilisateur**

Lorsque vous ajoutez un nouvel utilisateur à l’aide de l’API Directory Manager Service, définissez les informations de cet utilisateur. En règle générale, lorsque vous ajoutez un nouvel utilisateur, vous définissez les valeurs suivantes :

* **Nom** de domaine : Domaine auquel appartient l’utilisateur (par exemple,  `DefaultDom`).
* **Valeur** de l&#39;identifiant utilisateur : La valeur d’identifiant de l’utilisateur (par exemple,  `wblue`).
* **Type** de entité de sécurité : Le type d’utilisateur (par exemple, vous pouvez spécifier  `USER)`.
* **Prénom** : Nom donné à l’utilisateur (par exemple,  `Wendy`).
* **Nom** de famille : Nom de famille de l’utilisateur (par exemple,  `Blue)`.
* **Paramètres régionaux** : Informations sur les paramètres régionaux pour l’utilisateur.

**Ajout de l’utilisateur à AEM Forms**

Après avoir défini les informations utilisateur, vous pouvez ajouter l’utilisateur à AEM Forms. Pour ajouter un utilisateur, appelez la méthode `DirectoryManagerServiceClient` de l’objet `createLocalUser`.

**Vérification de l’ajout de l’utilisateur**

Vous pouvez vérifier que l’utilisateur a été ajouté pour vous assurer qu’aucun problème ne s’est produit. Localisez le nouvel utilisateur à l’aide de la valeur de l’identifiant de l’utilisateur.

**Voir également**

[Ajout d’utilisateurs à l’aide de l’API Java](users.md#add-users-using-the-java-api)

[Ajout d’utilisateurs à l’aide de l’API de service Web](users.md#add-users-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Suppression d’utilisateurs](users.md#deleting-users)

### Ajout d’utilisateurs à l’aide de l’API Java {#add-users-using-the-java-api}

Ajoutez des utilisateurs à l’aide de l’API du service Directory Manager (Java) :

1. Inclure les fichiers de projet.

   Incluez les fichiers JAR client, tels que adobe-usermanager-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un client DirectoryManagerServices .

   Créez un objet `DirectoryManagerServiceClient` en utilisant son constructeur et en transmettant un objet `ServiceClientFactory` contenant des propriétés de connexion.

1. Définissez les informations sur l’utilisateur.

   * Créez un objet `UserImpl` en utilisant son constructeur.
   * Définissez le nom demain en appelant la méthode `UserImpl` de l’objet `setDomainName`. Transmettez une valeur string qui spécifie le nom de domaine.
   * Définissez le type principal en appelant la méthode `UserImpl` de l’objet `setPrincipalType`. Transmettez une valeur string qui spécifie le type d’utilisateur. Par exemple, vous pouvez spécifier `USER`.
   * Définissez la valeur de l’identifiant utilisateur en appelant la méthode `setUserid` de l’objet `UserImpl`. Transmettez une valeur string qui spécifie la valeur de l’identifiant utilisateur. Par exemple, vous pouvez spécifier `wblue`.
   * Définissez le nom canonique en appelant la méthode `setCanonicalName` de l’objet `UserImpl`. Transmettez une valeur string qui spécifie le nom canonique de l’utilisateur. Par exemple, vous pouvez spécifier `wblue`.
   * Définissez le nom donné en appelant la méthode `UserImpl` de l’objet `setGivenName`. Transmettez une valeur string qui spécifie le prénom de l’utilisateur. Par exemple, vous pouvez spécifier `Wendy`.
   * Définissez le nom de famille en appelant la méthode `UserImpl` de l’objet `setFamilyName`. Transmettez une valeur string qui spécifie le nom de famille de l’utilisateur. Par exemple, vous pouvez spécifier `Blue`.

   >[!NOTE]
   >
   >Appelez une méthode appartenant à l’objet `UserImpl` pour définir d’autres valeurs. Par exemple, vous pouvez définir la valeur du paramètre régional en appelant la méthode `setLocale` de l’objet `UserImpl`.

1. Ajoutez l’utilisateur à AEM Forms.

   Appelez la méthode `createLocalUser` de l’objet `DirectoryManagerServiceClient` et transmettez les valeurs suivantes :

   * Objet `UserImpl` représentant le nouvel utilisateur
   * Une valeur string qui représente le mot de passe de l’utilisateur.

   La méthode `createLocalUser` renvoie une valeur string qui spécifie la valeur de l’identifiant utilisateur local.

1. Vérifiez que l’utilisateur a été ajouté.

   * Créez un objet `PrincipalSearchFilter` en utilisant son constructeur.
   * Définissez la valeur de l’identifiant utilisateur en appelant la méthode `setUserId` de l’objet `PrincipalSearchFilter`. Transmettez une valeur string qui représente la valeur de l’identifiant de l’utilisateur.
   * Appelez la méthode `findPrincipals` de l’objet `DirectoryManagerServiceClient` et transmettez l’objet `PrincipalSearchFilter` . Cette méthode renvoie une instance `java.util.List`, où chaque élément est un objet `User`. Parcourez l’instance `java.util.List` pour localiser l’utilisateur.

**Voir également**

[Résumé des étapes](users.md#summary-of-steps)

[Démarrage rapide (mode SOAP) : Ajout d’utilisateurs à l’aide de l’API Java](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-adding-users-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Ajout d’utilisateurs à l’aide de l’API de service Web {#add-users-using-the-web-service-api}

Ajoutez des utilisateurs à l’aide de l’API Directory Manager Service (service Web) :

1. Inclure les fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Assurez-vous d’utiliser la définition WSDL suivante pour la référence de service : `http://localhost:8080/soap/services/DirectoryManagerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un client DirectoryManagerService .

   * Créez un objet `DirectoryManagerServiceClient` à l’aide de son constructeur par défaut.
   * Créez un objet `DirectoryManagerServiceClient.Endpoint.Address` à l’aide du constructeur `System.ServiceModel.EndpointAddress`. Transmettez une valeur string qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/DirectoryManagerService?blob=mtom`). Vous n’avez pas besoin d’utiliser l’attribut `lc_version`. Cet attribut est utilisé lorsque vous créez une référence de service. Veillez à spécifier `?blob=mtom`.
   * Créez un objet `System.ServiceModel.BasicHttpBinding` en obtenant la valeur du champ `DirectoryManagerServiceClient.Endpoint.Binding`. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le champ `MessageEncoding` de l’objet `System.ServiceModel.BasicHttpBinding` sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `DirectoryManagerServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `DirectoryManagerServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Définissez les informations sur l’utilisateur.

   * Créez un objet `UserImpl` en utilisant son constructeur.
   * Définissez le nom demain en attribuant une valeur string au champ `domainName` de l’objet `UserImpl`.
   * Définissez le type principal en attribuant une valeur string au champ `principalType` de l’objet `UserImpl`. Par exemple, vous pouvez spécifier `USER`.
   * Définissez la valeur de l’identifiant de l’utilisateur en attribuant une valeur string au champ `userid` de l’objet `UserImpl`.
   * Définissez la valeur de nom canonique en attribuant une valeur string au champ `UserImpl` de l’objet `canonicalName`.
   * Définissez la valeur du nom donné en attribuant une valeur de chaîne au champ `givenName` de l’objet `UserImpl`.
   * Définissez la valeur du nom de famille en attribuant une valeur de chaîne au champ `familyName` de l’objet `UserImpl`.

1. Ajoutez l’utilisateur à AEM Forms.

   Appelez la méthode `createLocalUser` de l’objet `DirectoryManagerServiceClient` et transmettez les valeurs suivantes :

   * Objet `UserImpl` représentant le nouvel utilisateur
   * Une valeur string qui représente le mot de passe de l’utilisateur.

   La méthode `createLocalUser` renvoie une valeur string qui spécifie la valeur de l’identifiant utilisateur local.

1. Vérifiez que l’utilisateur a été ajouté.

   * Créez un objet `PrincipalSearchFilter` en utilisant son constructeur.
   * Définissez la valeur de l’identifiant de l’utilisateur en attribuant une valeur string qui représente la valeur de l’identifiant de l’utilisateur dans le champ `PrincipalSearchFilter` de l’objet `userId`.
   * Appelez la méthode `findPrincipals` de l’objet `DirectoryManagerServiceClient` et transmettez l’objet `PrincipalSearchFilter` . Cette méthode renvoie un objet de collection `MyArrayOfUser`, où chaque élément est un objet `User`. Parcourez la collection `MyArrayOfUser` pour localiser l’utilisateur.

**Voir également**

[Résumé des étapes](users.md#summary-of-steps)

[Appel d’AEM Forms à l’aide de MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Appel d’AEM Forms à l’aide de SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Suppression d’utilisateurs {#deleting-users}

Vous pouvez utiliser l’API Directory Manager Service (Java et service Web) pour supprimer par programmation les utilisateurs d’AEM Forms. Après la suppression d’un utilisateur, celui-ci ne peut plus être utilisé pour effectuer une opération de service nécessitant un utilisateur. Par exemple, vous ne pouvez pas affecter une tâche à un utilisateur supprimé.

### Résumé des étapes {#summary_of_steps-1}

Pour supprimer un utilisateur, procédez comme suit :

1. Inclure les fichiers de projet.
1. Créez un client DirectoryManagerService .
1. Indiquez l’utilisateur à supprimer.
1. Supprimez l’utilisateur d’AEM Forms.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, incluez les fichiers proxy.

**Création d’un client DirectoryManagerService**

Avant d’effectuer par programmation une opération d’API du service Directory Manager, créez un client de service Directory Manager.

**Spécification de l’utilisateur à supprimer**

Vous pouvez spécifier un utilisateur à supprimer à l’aide de la valeur d’identifiant de l’utilisateur.

**Suppression de l’utilisateur d’AEM Forms**

Pour supprimer un utilisateur, appelez la méthode `DirectoryManagerServiceClient` de l’objet `deleteLocalUser`.

**Voir également**

[Suppression des utilisateurs à l’aide de l’API Java](users.md#delete-users-using-the-java-api)

[Suppression des utilisateurs à l’aide de l’API de service Web](users.md#delete-users-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Ajout d’utilisateurs](users.md#adding-users)

### Suppression des utilisateurs à l’aide de l’API Java {#delete-users-using-the-java-api}

Supprimez les utilisateurs à l’aide de l’API du service Directory Manager (Java) :

1. Inclure les fichiers de projet.

   Incluez les fichiers JAR client, tels que adobe-usermanager-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un client DirectoryManagerService .

   Créez un objet `DirectoryManagerServiceClient` en utilisant son constructeur et en transmettant un objet `ServiceClientFactory` contenant des propriétés de connexion.

1. Indiquez l’utilisateur à supprimer.

   * Créez un objet `PrincipalSearchFilter` en utilisant son constructeur.
   * Définissez la valeur de l’identifiant utilisateur en appelant la méthode `setUserId` de l’objet `PrincipalSearchFilter`. Transmettez une valeur string qui représente la valeur de l’identifiant de l’utilisateur.
   * Appelez la méthode `findPrincipals` de l’objet `DirectoryManagerServiceClient` et transmettez l’objet `PrincipalSearchFilter` . Cette méthode renvoie une instance `java.util.List`, où chaque élément est un objet `User`. Parcourez l’instance `java.util.List` pour localiser l’utilisateur à supprimer.

1. Supprimez l’utilisateur d’AEM Forms.

   Appelez la méthode `deleteLocalUser` de l’objet `DirectoryManagerServiceClient` et transmettez la valeur du champ `oid` de l’objet `User` . Appelez la méthode `getOid` de l’objet `User`. Utilisez l’objet `User` récupéré à partir de l’instance `java.util.List`.

**Voir également**

[Résumé des étapes](users.md#summary-of-steps)

[Démarrage rapide (mode EJB) : Suppression d’utilisateurs à l’aide de l’API Java](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-deleting-users-using-the-java-api)

[Démarrage rapide (mode SOAP) : Suppression d’utilisateurs à l’aide de l’API Java](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-deleting-users-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Suppression des utilisateurs à l’aide de l’API de service Web {#delete-users-using-the-web-service-api}

Supprimez les utilisateurs à l’aide de l’API Directory Manager Service (service Web) :

1. Inclure les fichiers de projet.

   Incluez les fichiers JAR client, tels que adobe-usermanager-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un client DirectoryManagerService .

   * Créez un objet `DirectoryManagerServiceClient` à l’aide de son constructeur par défaut.
   * Créez un objet `DirectoryManagerServiceClient.Endpoint.Address` à l’aide du constructeur `System.ServiceModel.EndpointAddress`. Transmettez une valeur string qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/DirectoryManagerService?blob=mtom`). Vous n’avez pas besoin d’utiliser l’attribut `lc_version`. Cet attribut est utilisé lorsque vous créez une référence de service. Veillez à spécifier `blob=mtom.`
   * Créez un objet `System.ServiceModel.BasicHttpBinding` en obtenant la valeur du champ `DirectoryManagerServiceClient.Endpoint.Binding`. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le champ `MessageEncoding` de l’objet `System.ServiceModel.BasicHttpBinding` sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `DirectoryManagerServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `DirectoryManagerServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Indiquez l’utilisateur à supprimer.

   * Créez un objet `PrincipalSearchFilter` en utilisant son constructeur.
   * Définissez la valeur de l’identifiant de l’utilisateur en attribuant une valeur string au champ `userId` de l’objet `PrincipalSearchFilter`.
   * Appelez la méthode `findPrincipals` de l’objet `DirectoryManagerServiceClient` et transmettez l’objet `PrincipalSearchFilter` . Cette méthode renvoie un objet de collection `MyArrayOfUser`, où chaque élément est un objet `User`. Parcourez la collection `MyArrayOfUser` pour localiser l’utilisateur. L’objet `User` récupéré de l’objet de collection `MyArrayOfUser` est utilisé pour supprimer l’utilisateur.

1. Supprimez l’utilisateur d’AEM Forms.

   Supprimez l’utilisateur en transmettant la valeur du champ `oid` de l’objet `User` à la méthode `deleteLocalUser` de l’objet `DirectoryManagerServiceClient`.

**Voir également**

[Résumé des étapes](users.md#summary-of-steps)

[Appel d’AEM Forms à l’aide de MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Appel d’AEM Forms à l’aide de SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Création de groupes {#creating-groups}

Vous pouvez utiliser l’API Directory Manager Service (Java et service Web) pour créer des groupes AEM Forms par programmation. Après avoir créé un groupe, vous pouvez utiliser ce groupe pour effectuer une opération de service nécessitant un groupe. Par exemple, vous pouvez affecter un utilisateur au nouveau groupe. (Voir [Gestion des utilisateurs et des groupes](users.md#managing-users-and-groups).)

### Résumé des étapes {#summary_of_steps-2}

Pour créer un groupe, procédez comme suit :

1. Inclure les fichiers de projet.
1. Créez un client DirectoryManagerService .
1. Déterminez que le groupe n’existe pas.
1. Créez le groupe.
1. Exécutez une action avec le groupe.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires.

Les fichiers JAR suivants doivent être ajoutés au chemin d’accès aux classes de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utility.jar (Obligatoire si AEM Forms est déployé sur JBoss)
* jbossall-client.jar (requis si AEM Forms est déployé sur JBoss)

Pour plus d’informations sur l’emplacement de ces fichiers JAR, voir [Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Création d’un client DirectoryManagerService**

Avant d’effectuer une opération de service Directory Manager par programmation, créez un client API Directory Manager Service.

**Déterminer si le groupe existe**

Lorsque vous créez un groupe, assurez-vous qu’il n’existe pas dans le même domaine. En d’autres termes, deux groupes ne peuvent pas porter le même nom dans le même domaine. Pour effectuer cette tâche, effectuez une recherche et filtrez les résultats de la recherche selon deux valeurs. Définissez le type principal sur `com.adobe.idp.um.api.infomodel.Principal.PRINCIPALTYPE_GROUP` pour vous assurer que seuls les groupes sont renvoyés. Veillez également à spécifier le nom de domaine.

**Création du groupe**

Une fois que vous avez déterminé que le groupe n’existe pas dans le domaine, créez le groupe et spécifiez les attributs suivants :

* **CommonName** : Nom du groupe.
* **Domaine** : Domaine dans lequel le groupe est ajouté.
* **Description** : Description du groupe.

**Exécution d’une action avec le groupe**

Après avoir créé un groupe, vous pouvez effectuer une action à l’aide de ce groupe. Vous pouvez par exemple ajouter un utilisateur au groupe. Pour ajouter un utilisateur à un groupe, récupérez la valeur d’identifiant unique de l’utilisateur et du groupe. Transmettez ces valeurs à la méthode `addPrincipalToLocalGroup` .

**Voir également**

[Création de groupes à l’aide de l’API Java](users.md#create-groups-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Ajout d’utilisateurs](users.md#adding-users)

[Suppression d’utilisateurs](users.md#deleting-users)

### Créer des groupes à l’aide de l’API Java {#create-groups-using-the-java-api}

Créez un groupe à l’aide de l’API du service Directory Manager (Java) :

1. Inclure les fichiers de projet.

   Incluez les fichiers JAR client, tels que adobe-usermanager-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un client DirectoryManagerService .

   Créez un objet `DirectoryManagerServiceClient` en utilisant son constructeur et en transmettant un objet `ServiceClientFactory` contenant des propriétés de connexion.

1. Déterminez si le groupe existe.

   * Créez un objet `PrincipalSearchFilter` en utilisant son constructeur.
   * Définissez le type principal en appelant l’objet `PrincipalSearchFilter` de l’objet `setPrincipalType`. Transmettez la valeur `com.adobe.idp.um.api.infomodel.Principal.PRINCIPALTYPE_GROUP`.
   * Définissez le domaine en appelant l’objet `PrincipalSearchFilter` de l’objet `setSpecificDomainName`. Transmettez une valeur string qui spécifie le nom de domaine.
   * Pour trouver un groupe, appelez la méthode `DirectoryManagerServiceClient` de l’objet `findPrincipals` (une entité peut être un groupe). Transmettez l’objet `PrincipalSearchFilter` qui spécifie le type principal et le nom de domaine. Cette méthode renvoie une instance `java.util.List` où chaque élément est une instance `Group`. Chaque instance de groupe est conforme au filtre spécifié à l’aide de l’objet `PrincipalSearchFilter` .
   * Effectuez une itération sur l’instance `java.util.List`. Pour chaque élément, récupérez le nom du groupe. Assurez-vous que le nom du groupe n’est pas égal au nouveau nom du groupe.

1. Créez le groupe.

   * Si le groupe n’existe pas, appelez la méthode `setCommonName` de l’objet `Group` et transmettez une valeur string qui spécifie le nom du groupe.
   * Appelez la méthode `setDescription` de l’objet `Group` et transmettez une valeur string qui spécifie la description du groupe.
   * Appelez la méthode `setDomainName` de l’objet `Group` et transmettez une valeur string qui spécifie le nom de domaine.
   * Appelez la méthode `createLocalGroup` de l’objet `DirectoryManagerServiceClient` et transmettez l’instance `Group`.

   La méthode `createLocalUser` renvoie une valeur string qui spécifie la valeur de l’identifiant utilisateur local.

1. Exécutez une action avec le groupe.

   * Créez un objet `PrincipalSearchFilter` en utilisant son constructeur.
   * Définissez la valeur de l’identifiant utilisateur en appelant la méthode `setUserId` de l’objet `PrincipalSearchFilter`. Transmettez une valeur string qui représente la valeur de l’identifiant de l’utilisateur.
   * Appelez la méthode `findPrincipals` de l’objet `DirectoryManagerServiceClient` et transmettez l’objet `PrincipalSearchFilter` . Cette méthode renvoie une instance `java.util.List`, où chaque élément est un objet `User`. Parcourez l’instance `java.util.List` pour localiser l’utilisateur.
   * Ajoutez un utilisateur au groupe en appelant la méthode `addPrincipalToLocalGroup` de l’objet `DirectoryManagerServiceClient`. Transmettez la valeur renvoyée par la méthode `getOid` de l’objet `User`. Transmettez la valeur renvoyée par la méthode `getOid` des objets `Group` (utilisez l’instance `Group` qui représente le nouveau groupe).

**Voir également**

[Résumé des étapes](users.md#summary-of-steps)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Gestion des utilisateurs et des groupes {#managing-users-and-groups}

Cette rubrique décrit comment utiliser (Java) pour affecter, supprimer et interroger par programmation des domaines, des utilisateurs et des groupes.

>[!NOTE]
>
>Lors de la configuration d’un domaine, vous devez définir l’identifiant unique des groupes et des utilisateurs. L’attribut choisi doit non seulement être unique dans l’environnement LDAP, mais il doit également être immuable et ne changera pas dans l’annuaire. Cet attribut doit également être d’un type de données de chaîne simple (la seule exception actuellement autorisée pour la 2000/2003 Principale Directory est `"objectsid"`, qui est une valeur binaire). L’attribut Novell eDirectory `"GUID"`, par exemple, n’est pas un type de données de chaîne simple et ne fonctionnera donc pas.

* Pour Principale Directory, utilisez `"objectsid"`.
* Pour SunOne, utilisez `"nsuniqueid"`.

>[!NOTE]
>
>La création de plusieurs utilisateurs et groupes locaux lorsqu’une synchronisation d’annuaire LDAP est en cours n’est pas prise en charge. Toute tentative est susceptible d’entraîner des erreurs.

### Résumé des étapes {#summary_of_steps-3}

Pour gérer les utilisateurs et les groupes, procédez comme suit :

1. Inclure les fichiers de projet.
1. Créez un client DirectoryManagerService .
1. Appelez les opérations d’utilisateur ou de groupe appropriées.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services web, veillez à inclure les fichiers proxy.

**Création d’un client DirectoryManagerService**

Avant d’effectuer par programmation une opération de service Directory Manager, vous devez créer un client de service Directory Manager. Avec l’API Java, cela est possible en créant un objet `DirectoryManagerServiceClient`. Avec l’API de service Web, cela se fait en créant un objet `DirectoryManagerServiceService`.

**Appeler les opérations d’utilisateur ou de groupe appropriées**

Une fois le client de service créé, vous pouvez appeler les opérations de gestion des utilisateurs ou des groupes. Le client de service vous permet d’affecter, de supprimer et de demander des domaines, des utilisateurs et des groupes. Notez qu’il est possible d’ajouter une entité de répertoire ou une entité locale à un groupe local, mais qu’il n’est pas possible d’ajouter une entité locale à un groupe de répertoires.

**Voir également**

[Gestion des utilisateurs et des groupes à l’aide de l’API Java](users.md#managing-users-and-groups-using-the-java-api)

[Gestion des utilisateurs et des groupes à l’aide de l’API de service Web](users.md#managing-users-and-groups-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Démarrages rapides de l’API User Manager](/help/forms/developing/user-manager-java-api-quick.md#user-manager-java-api-quick-start-soap)

### Gestion des utilisateurs et des groupes à l’aide de l’API Java {#managing-users-and-groups-using-the-java-api}

Pour gérer par programmation les utilisateurs, les groupes et les domaines à l’aide de (Java), effectuez les tâches suivantes :

1. Inclure les fichiers de projet.

   Incluez les fichiers JAR client, tels que adobe-usermanager-client.jar, dans le chemin de classe de votre projet Java. Pour plus d’informations sur l’emplacement de ces fichiers, voir [Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

1. Créez un client DirectoryManagerService .

   Créez un objet `DirectoryManagerServiceClient` en utilisant son constructeur et en transmettant un objet `ServiceClientFactory` contenant des propriétés de connexion. Pour plus d’informations, voir [Définition des propriétés de connexion ](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)*.*

1. Appelez les opérations d’utilisateur ou de groupe appropriées.

   Pour trouver un utilisateur ou un groupe, appelez l’une des méthodes de l’objet `DirectoryManagerServiceClient` pour rechercher des entités (une entité pouvant être un utilisateur ou un groupe). Dans l’exemple ci-dessous, la méthode `findPrincipals` est appelée à l’aide d’un filtre de recherche (un objet `PrincipalSearchFilter` ).

   Dans ce cas, la valeur renvoyée étant une valeur `java.util.List` contenant des objets `Principal`, effectuez une itération sur le résultat et convertissez les objets `Principal` en objets `User` ou `Group`.

   À l’aide de l’objet `User` ou `Group` qui en résulte (qui héritent tous deux de l’interface `Principal`), récupérez les informations dont vous avez besoin dans vos workflows. Par exemple, les valeurs de nom de domaine et de nom canonique, en combinaison, identifient de manière unique une entité. Ils sont récupérés en appelant les méthodes `Principal` de l’objet `getDomainName` et `getCanonicalName` , respectivement.

   Pour supprimer un utilisateur local, appelez la méthode `DirectoryManagerServiceClient` de l’objet `deleteLocalUser` et transmettez l’identifiant de l’utilisateur.

   Pour supprimer un groupe local, appelez la méthode `DirectoryManagerServiceClient` de l’objet `deleteLocalGroup` et transmettez l’identifiant du groupe.

**Voir également**

[Résumé des étapes](users.md#summary-of-steps)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Gestion des utilisateurs et des groupes à l’aide de l’API de service Web {#managing-users-and-groups-using-the-web-service-api}

Pour gérer par programmation les utilisateurs, les groupes et les domaines à l’aide de l’API Directory Manager Service (service Web), effectuez les tâches suivantes :

1. Inclure les fichiers de projet.

   * Créez un assemblage client Microsoft .NET qui utilise le fichier WSDL de Directory Manager. (Voir [Appel d’AEM Forms à l’aide de l’encodage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding).)
   * Référencez l’assemblage client Microsoft .NET. (Voir [Création d’un assemblage client .NET qui utilise l’encodage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding).)

1. Créez un client DirectoryManagerService .

   Créez un objet `DirectoryManagerServiceService` à l’aide du constructeur de votre classe proxy.

1. Appelez les opérations d’utilisateur ou de groupe appropriées.

   Pour trouver un utilisateur ou un groupe, appelez l’une des méthodes de l’objet `DirectoryManagerServiceService` pour rechercher des entités (une entité pouvant être un utilisateur ou un groupe). Dans l’exemple ci-dessous, la méthode `findPrincipalsWithFilter` est appelée à l’aide d’un filtre de recherche (un objet `PrincipalSearchFilter` ). Lors de l’utilisation d’un objet `PrincipalSearchFilter`, les entités locales ne sont renvoyées que si la propriété `isLocal` est définie sur `true`. Ce comportement est différent de ce qui se produirait avec l’API Java.

   >[!NOTE]
   >
   >Si le nombre maximal de résultats n’est pas spécifié dans le filtre de recherche (par le biais du champ `PrincipalSearchFilter.resultsMax` ), un maximum de 1 000 résultats sera renvoyé. Il s’agit d’un comportement différent de celui de l’API Java, dans laquelle 10 résultats sont le maximum par défaut. En outre, les méthodes de recherche telles que `findGroupMembers` ne donneront aucun résultat, sauf si le nombre maximal de résultats est spécifié dans le filtre de recherche (par exemple, via le champ `GroupMembershipSearchFilter.resultsMax` ). Cela s’applique à tous les filtres de recherche qui héritent de la classe `GenericSearchFilter`. Pour plus d’informations, voir [Référence de l’API AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

   Dans ce cas, la valeur renvoyée étant une valeur `object[]` contenant des objets `Principal`, effectuez une itération sur le résultat et convertissez les objets `Principal` en objets `User` ou `Group`.

   À l’aide de l’objet `User` ou `Group` qui en résulte (qui héritent tous deux de l’interface `Principal`), récupérez les informations dont vous avez besoin dans vos workflows. Par exemple, les valeurs de nom de domaine et de nom canonique, en combinaison, identifient de manière unique une entité. Ils sont récupérés en appelant respectivement les champs `domainName` et `canonicalName` de l’objet `Principal` .

   Pour supprimer un utilisateur local, appelez la méthode `DirectoryManagerServiceService` de l’objet `deleteLocalUser` et transmettez l’identifiant de l’utilisateur.

   Pour supprimer un groupe local, appelez la méthode `DirectoryManagerServiceService` de l’objet `deleteLocalGroup` et transmettez l’identifiant du groupe.

**Voir également**

[Résumé des étapes](users.md#summary-of-steps)

[Appel d’AEM Forms à l’aide de MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## Gestion des rôles et des autorisations {#managing-roles-and-permissions}

Cette rubrique décrit comment utiliser l’API du service Authorization Manager (Java) pour attribuer, supprimer et déterminer par programmation des rôles et des autorisations.

Dans AEM Forms, un *rôle* est un groupe d’autorisations d’accès à une ou plusieurs ressources au niveau du système. Ces autorisations sont créées via User Management et sont appliquées par les composants de service. Par exemple, un administrateur peut affecter le rôle &quot;Auteur du jeu de stratégies&quot; à un groupe d’utilisateurs. Rights Management autoriserait alors les utilisateurs de ce groupe avec ce rôle à créer des jeux de stratégies via la console d’administration.

Il existe deux types de rôles : *rôles par défaut* et *rôles personnalisés*. Les rôles par défaut (*rôles système)* résident déjà dans AEM Forms. Il est supposé que les rôles par défaut ne peuvent pas être supprimés ni modifiés par l’administrateur et sont donc immuables. Les rôles personnalisés créés par l’administrateur, qui peuvent ensuite les modifier ou les supprimer, sont donc modifiables.

Les rôles facilitent la gestion des autorisations. Lorsqu’un rôle est attribué à une entité, un ensemble d’autorisations est automatiquement attribué à cette entité, et toutes les décisions spécifiques liées à l’accès pour l’entité sont basées sur cet ensemble global d’autorisations attribuées.

### Résumé des étapes {#summary_of_steps-4}

Pour gérer les rôles et les autorisations, procédez comme suit :

1. Inclure les fichiers de projet.
1. Créez un client AuthorizationManagerService .
1. Appelez les opérations de rôle ou d’autorisation appropriées.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services web, veillez à inclure les fichiers proxy.

**Création d’un client AuthorizationManagerService**

Avant d’effectuer par programmation une opération User Management AuthorizationManagerService, vous devez créer un client AuthorizationManagerService . Avec l’API Java, cela est possible en créant un objet `AuthorizationManagerServiceClient`.

**Appeler les opérations de rôle ou d’autorisation appropriées**

Une fois que vous avez créé le client de service, vous pouvez appeler les opérations de rôle ou d’autorisation. Le client de service vous permet d’affecter, de supprimer et de déterminer des rôles et des autorisations.

**Voir également**

[Gestion des rôles et des autorisations à l’aide de l’API Java](users.md#managing-roles-and-permissions-using-the-java-api)

[Gestion des rôles et des autorisations à l’aide de l’API de service Web](users.md#managing-roles-and-permissions-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Démarrages rapides de l’API User Manager](/help/forms/developing/user-manager-java-api-quick.md#user-manager-java-api-quick-start-soap)

### Gestion des rôles et des autorisations à l’aide de l’API Java {#managing-roles-and-permissions-using-the-java-api}

Pour gérer les rôles et les autorisations à l’aide de l’API du service Authorization Manager (Java), effectuez les tâches suivantes :

1. Inclure les fichiers de projet.

   Incluez les fichiers JAR client, tels que adobe-usermanager-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un client AuthorizationManagerService .

   Créez un objet `AuthorizationManagerServiceClient` en utilisant son constructeur et en transmettant un objet `ServiceClientFactory` contenant des propriétés de connexion.

1. Appelez les opérations de rôle ou d’autorisation appropriées.

   Pour attribuer un rôle à une entité, appelez la méthode `assignRole` de l’objet `AuthorizationManagerServiceClient` et transmettez les valeurs suivantes :

   * Objet `java.lang.String` contenant l’identifiant du rôle
   * Tableau d’objets `java.lang.String` contenant les identifiants principaux.

   Pour supprimer un rôle d’une entité, appelez la méthode `unassignRole` de l’objet `AuthorizationManagerServiceClient` et transmettez les valeurs suivantes :

   * Objet `java.lang.String` contenant l’identifiant du rôle.
   * Tableau d’objets `java.lang.String` contenant les identifiants principaux.


**Voir également**

[Résumé des étapes](users.md#summary-of-steps)

[Démarrage rapide (mode SOAP) : Gestion des rôles et des autorisations à l’aide de l’API Java](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-managing-roles-and-permissions-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Gestion des rôles et des autorisations à l’aide de l’API de service Web {#managing-roles-and-permissions-using-the-web-service-api}

Gérez les rôles et les autorisations à l’aide de l’API Authorization Manager Service (service web) :

1. Inclure les fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Assurez-vous d’utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/AuthorizationManagerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un client AuthorizationManagerService .

   * Créez un objet `AuthorizationManagerServiceClient` à l’aide de son constructeur par défaut.
   * Créez un objet `AuthorizationManagerServiceClient.Endpoint.Address` à l’aide du constructeur `System.ServiceModel.EndpointAddress`. Transmettez une valeur string qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/AuthorizationManagerService?blob=mtom`). Vous n’avez pas besoin d’utiliser l’attribut `lc_version`. Cet attribut est utilisé lorsque vous créez une référence de service.
   * Créez un objet `System.ServiceModel.BasicHttpBinding` en obtenant la valeur du champ `AuthorizationManagerServiceClient.Endpoint.Binding`. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le champ `MessageEncoding` de l’objet `System.ServiceModel.BasicHttpBinding` sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `AuthorizationManagerServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `AuthorizationManagerServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Appelez les opérations de rôle ou d’autorisation appropriées.

   Pour attribuer un rôle à une entité, appelez la méthode `assignRole` de l’objet `AuthorizationManagerServiceClient` et transmettez les valeurs suivantes :

   * Objet `string` contenant l’identifiant du rôle
   * Objet `MyArrayOf_xsd_string` contenant les identifiants principaux.

   Pour supprimer un rôle d’une entité, appelez la méthode `unassignRole` de l’objet `AuthorizationManagerServiceService` et transmettez les valeurs suivantes :

   * Objet `string` contenant l’identifiant du rôle.
   * Tableau d’objets `string` contenant les identifiants principaux.


**Voir également**

[Résumé des étapes](users.md#summary-of-steps)

[Appel d’AEM Forms à l’aide de MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## Authentification des utilisateurs {#authenticating-users}

Cette rubrique décrit comment vous pouvez utiliser l’API du service Authentication Manager (Java) pour permettre à vos applications clientes d’authentifier par programmation les utilisateurs.

L’authentification des utilisateurs peut être nécessaire pour interagir avec une base de données d’entreprise ou d’autres référentiels d’entreprise qui stockent des données sécurisées.

Supposons, par exemple, qu’un utilisateur saisisse un nom d’utilisateur et un mot de passe dans une page web et envoie les valeurs à un serveur d’applications J2EE hébergeant Forms. Une application personnalisée Forms peut authentifier l’utilisateur à l’aide du service Authentication Manager.

Si l’authentification est réussie, l’application accède à une base de données d’entreprise sécurisée. Dans le cas contraire, un message est envoyé à l’utilisateur pour l’informer qu’il n’est pas un utilisateur autorisé.

Le diagramme suivant illustre le flux logique de l’application.

![au_au_umauth_process](assets/au_au_umauth_process.png)

Le tableau suivant décrit les étapes de ce diagramme

<table>
 <thead>
  <tr>
   <th><p>Étape</p></th>
   <th><p>Description</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>3</p></td>
   <td><p>L’utilisateur accède à un site web et spécifie un nom d’utilisateur et un mot de passe. Ces informations sont envoyées à un serveur d’applications J2EE hébergeant AEM Forms.</p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>Les informations d’identification de l’utilisateur sont authentifiées avec le service Authentication Manager. Si les informations d’identification de l’utilisateur sont valides, le workflow passe à l’étape 3. Dans le cas contraire, un message est envoyé à l’utilisateur pour l’informer qu’il n’est pas un utilisateur autorisé.</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>Les informations utilisateur et la conception de formulaire sont récupérées dans une base de données d’entreprise sécurisée. </p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>Les informations utilisateur sont fusionnées avec une conception de formulaire et le formulaire est rendu à l’utilisateur. </p></td>
  </tr>
 </tbody>
</table>

### Résumé des étapes {#summary_of_steps-5}

Pour authentifier un utilisateur par programmation, procédez comme suit :

1. Inclure les fichiers de projet.
1. Créez un client AuthenticationManagerService.
1. Appelez l’opération d’authentification.
1. Si nécessaire, récupérez le contexte afin que l’application cliente puisse le transférer vers un autre service AEM Forms pour authentification.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services web, veillez à inclure les fichiers proxy.

**Création d’un client AuthenticationManagerService**

Avant de pouvoir authentifier un utilisateur par programmation, vous devez créer un client AuthenticationManagerService. Lors de l’utilisation de l’API Java, créez un objet `AuthenticationManagerServiceClient` .

**Appeler l’opération d’authentification**

Une fois le client de service créé, vous pouvez appeler l’opération d’authentification. Cette opération nécessite des informations sur l’utilisateur, telles que son nom et son mot de passe. Si l’utilisateur ne s’authentifie pas, une exception est générée.

**Récupération du contexte d’authentification**

Une fois que vous avez authentifié l’utilisateur, vous pouvez créer un contexte basé sur l’utilisateur authentifié. Vous pouvez ensuite utiliser le contenu pour appeler un autre service AEM Forms. Par exemple, vous pouvez utiliser le contexte pour créer un `EncryptionServiceClient` et chiffrer un document PDF avec un mot de passe. Assurez-vous que l’utilisateur authentifié dispose du rôle `Services User` requis pour appeler un service AEM Forms.

**Voir également**

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Démarrages rapides de l’API User Manager](/help/forms/developing/user-manager-java-api-quick.md#user-manager-java-api-quick-start-soap)

[Chiffrement de documents PDF avec un mot de passe](/help/forms/developing/encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### Authentification d’un utilisateur à l’aide de l’API Java {#authenticate-a-user-using-the-java-api}

Authentifiez un utilisateur à l’aide de l’API du service Authentication Manager (Java) :

1. Inclure les fichiers de projet.

   Incluez les fichiers JAR client, tels que adobe-usermanager-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un client AuthenticationManagerServices .

   Créez un objet `AuthenticationManagerServiceClient` en utilisant son constructeur et en transmettant un objet `ServiceClientFactory` contenant des propriétés de connexion.

1. Appelez l’opération d’authentification.

   Appelez la méthode `authenticate` de l’objet `AuthenticationManagerServiceClient` et transmettez les valeurs suivantes :

   * Objet `java.lang.String` contenant le nom de l’utilisateur.
   * Tableau d’octets (objet `byte[]`) contenant le mot de passe de l’utilisateur. Vous pouvez obtenir l’objet `byte[]` en appelant la méthode `getBytes` de l’objet `java.lang.String`.

   La méthode d’authentification renvoie un objet `AuthResult` contenant des informations sur l’utilisateur authentifié.

1. Récupérez le contexte d’authentification.

   Appelez la méthode `getContext` de l’objet `ServiceClientFactory`, qui renverra un objet `Context`.

   Ensuite, appelez la méthode `initPrincipal` de l’objet `Context` et transmettez la méthode `AuthResult`.

### Authentification d’un utilisateur à l’aide de l’API de service Web {#authenticate-a-user-using-the-web-service-api}

Authentifiez un utilisateur à l’aide de l’API Authentication Manager Service (service Web) :

1. Inclure les fichiers de projet.

   * Créez un assemblage client Microsoft .NET qui utilise le fichier WSDL Authentication Manager. (Voir [Appel d’AEM Forms à l’aide de l’encodage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding).)
   * Référencez l’assemblage client Microsoft .NET. (Voir &quot;Référence à l’assemblage client .NET&quot; dans [Appel d’AEM Forms à l’aide de l’encodage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding).)

1. Créez un client AuthenticationManagerService.

   Créez un objet `AuthenticationManagerServiceService` à l’aide du constructeur de votre classe proxy.

1. Appelez l’opération d’authentification.

   Appelez la méthode `authenticate` de l’objet `AuthenticationManagerServiceClient` et transmettez les valeurs suivantes :

   * Objet `string` contenant le nom de l’utilisateur
   * Tableau d’octets (objet `byte[]`) contenant le mot de passe de l’utilisateur. Vous pouvez obtenir l’objet `byte[]` en convertissant un objet `string` contenant le mot de passe en tableau `byte[]` à l’aide de la logique illustrée dans l’exemple ci-dessous.
   * La valeur renvoyée est un objet `AuthResult` qui peut être utilisé pour récupérer des informations sur l’utilisateur. Dans l’exemple ci-dessous, les informations de l’utilisateur sont récupérées en obtenant d’abord le champ `authenticatedUser` de l’objet `AuthResult` et ensuite les champs `User` de l’objet `canonicalName` ainsi que les champs `domainName` qui en résultent.

**Voir également**

[Appel d’AEM Forms à l’aide de MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Appel d’AEM Forms à l’aide de SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Synchronisation par programmation des utilisateurs {#programmatically-synchronizing-users}

Vous pouvez synchroniser les utilisateurs par programmation à l’aide de l’API User Management. Lorsque vous synchronisez des utilisateurs, vous mettez à jour AEM Forms avec les données utilisateur qui se trouvent dans votre référentiel utilisateur. Supposons, par exemple, que vous ajoutiez de nouveaux utilisateurs à votre référentiel d’utilisateurs. Une fois que vous avez effectué une opération de synchronisation, les nouveaux utilisateurs deviennent AEM utilisateurs forms. En outre, les utilisateurs qui ne se trouvent plus dans votre référentiel d’utilisateurs sont supprimés d’AEM Forms.

Le diagramme suivant montre la synchronisation d’AEM Forms avec un référentiel utilisateur.

![ps_ps_umauth_sync](assets/ps_ps_umauth_sync.png)

Le tableau suivant décrit les étapes de ce diagramme

<table>
 <thead>
  <tr>
   <th><p>Étape</p></th>
   <th><p>Description</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>3</p></td>
   <td><p>Une application cliente demande à AEM Forms d’effectuer une opération de synchronisation.</p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>AEM Forms effectue une opération de synchronisation.</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>Les informations utilisateur sont mises à jour.</p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>Un utilisateur peut afficher les informations utilisateur mises à jour. </p></td>
  </tr>
 </tbody>
</table>

### Résumé des étapes {#summary_of_steps-6}

Pour synchroniser les utilisateurs par programmation, procédez comme suit :

1. Inclure les fichiers de projet.
1. Créez un client UserManagerUtilServiceClient .
1. Indiquez le domaine d’entreprise.
1. Appelez l’opération d’authentification.
1. Déterminer si l’opération de synchronisation est terminée

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services web, veillez à inclure les fichiers proxy.

**Création d’un client UserManagerUtilServiceClient**

Avant de pouvoir synchroniser les utilisateurs par programmation, vous devez créer un objet `UserManagerUtilServiceClient`.

**Définition du domaine d’entreprise**

Avant d’effectuer une opération de synchronisation à l’aide de l’API User Management, vous spécifiez le domaine d’entreprise auquel appartiennent les utilisateurs. Vous pouvez spécifier un ou plusieurs domaines d’entreprise. Avant d’effectuer par programmation une opération de synchronisation, vous devez configurer un domaine d’entreprise à l’aide d’Administration Console. (Voir [Aide à l’administration](https://www.adobe.com/go/learn_aemforms_admin_63).)

**Appeler l&#39;opération de synchronisation**

Après avoir défini un ou plusieurs domaines d’entreprise, vous pouvez effectuer l’opération de synchronisation. Le temps nécessaire à l’exécution de cette opération dépend du nombre d’enregistrements d’utilisateurs situés dans le référentiel d’utilisateurs.

**Déterminer si l’opération de synchronisation est terminée**

Après avoir effectué une opération de synchronisation par programmation, vous pouvez déterminer si l’opération est terminée.

**Voir également**

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Démarrages rapides de l’API User Manager](/help/forms/developing/user-manager-java-api-quick.md#user-manager-java-api-quick-start-soap)

[Chiffrement de documents PDF avec un mot de passe](/help/forms/developing/encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### Synchronisation par programmation des utilisateurs à l’aide de l’API Java {#programmatically-synchronizing-users-using-the-java-api}

Synchroniser les utilisateurs à l’aide de l’API User Management (Java) :

1. Inclure les fichiers de projet.

   Incluez les fichiers JAR client, tels que adobe-usermanager-client.jar et adobe-usermanager-util-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un client UserManagerUtilServiceClient .

   Créez un objet `UserManagerUtilServiceClient` en utilisant son constructeur et en transmettant un objet `ServiceClientFactory` contenant des propriétés de connexion.

1. Indiquez le domaine d’entreprise.

   * Appelez la méthode `scheduleSynchronization` de l’objet `UserManagerUtilServiceClient` pour lancer l’opération de synchronisation des utilisateurs.
   * Créez une instance `java.util.Set` à l’aide d’un constructeur `HashSet`. Veillez à spécifier `String` comme type de données. Cette instance `Java.util.Set` stocke les noms de domaine auxquels s’applique l’opération de synchronisation.
   * Pour chaque nom de domaine à ajouter, appelez la méthode add de l’objet `java.util.Set` et transmettez le nom de domaine.

1. Appelez l’opération de synchronisation.

   Appelez la méthode `getContext` de l’objet `ServiceClientFactory`, qui renverra un objet `Context`.

   Ensuite, appelez la méthode `initPrincipal` de l’objet `Context` et transmettez la méthode `AuthResult`.

**Voir également**

[Synchronisation par programmation des utilisateurs](users.md#programmatically-synchronizing-users)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
