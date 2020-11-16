---
title: Gestion des utilisateurs
seo-title: Gestion des utilisateurs
description: 'null'
seo-description: 'null'
uuid: 68d8a0bc-6e3d-4286-ba5c-534dcf58cb84
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 95804bff-9e6f-4807-aae4-790bd9e7cb57
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '6191'
ht-degree: 4%

---


# Gestion des utilisateurs {#managing-users}

**À propos de User Management**

Vous pouvez utiliser l’API User Management pour créer des applications clientes capables de gérer des rôles, des autorisations et des entités (qui peuvent être des utilisateurs ou des groupes), ainsi que d’authentifier des utilisateurs. L’API User Management se compose des API AEM Forms suivantes :

* API du service Directory Manager
* API du service Authentication Manager
* API du service Authorization Manager

User Management vous permet d’attribuer, de supprimer et de déterminer des rôles et des autorisations. Il vous permet également d’attribuer, de supprimer et de requête des domaines, des utilisateurs et des groupes. Enfin, vous pouvez utiliser User Management pour authentifier les utilisateurs.

En [Ajoutant les utilisateurs](users.md#adding-users) , vous comprendrez comment ajouter des utilisateurs par programmation. Cette section utilise l’API du service Directory Manager.

En [supprimant des utilisateurs](users.md#deleting-users) , vous comprendrez comment supprimer des utilisateurs par programmation. Cette section utilise l’API du service Directory Manager.

Dans [Gestion des utilisateurs et des groupes](users.md#managing-users-and-groups) , vous comprendrez la différence entre un utilisateur local et un utilisateur d’annuaire, et vous verrez des exemples d’utilisation des API de services Web et Java pour gérer par programmation les utilisateurs et les groupes. Cette section utilise l’API du service Directory Manager.

Dans [Gestion des rôles et des autorisations](users.md#managing-roles-and-permissions) , vous découvrirez les rôles et les autorisations du système et ce que vous pouvez faire par programmation pour les améliorer, et vous verrez des exemples d’utilisation des API Java et des services Web pour gérer par programmation les rôles et les autorisations. Cette section utilise à la fois l’API Service du Gestionnaire d’annuaires et l’API Service du Gestionnaire d’autorisations.

Dans [Authentification des utilisateurs](users.md#authenticating-users) , vous trouverez des exemples d’utilisation des API Java et des API de services Web pour authentifier les utilisateurs par programmation. Cette section utilise l’API Service du Gestionnaire d’autorisations.

**Présentation du processus d&#39;authentification**

User Management offre une fonctionnalité d’authentification intégrée et vous permet également de la connecter à votre propre fournisseur d’authentification. Lorsque User Management reçoit une demande d’authentification (par exemple, un utilisateur tente de se connecter), il transmet les informations utilisateur au fournisseur d’authentification pour authentification. User Management reçoit les résultats du fournisseur d’authentification après l’authentification de l’utilisateur.

Le diagramme suivant montre l&#39;interaction entre un utilisateur final qui tente de se connecter, User Management et le fournisseur d&#39;authentification.

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
   <td><p>User Management envoie le nom d’utilisateur et le mot de passe, ainsi que les informations de configuration, au fournisseur d’authentification.</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>Le fournisseur d’authentification se connecte au magasin d’utilisateurs et authentifie l’utilisateur.</p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>Le fournisseur d’authentification renvoie les résultats à User Management.</p></td>
  </tr>
  <tr>
   <td><p>5</p></td>
   <td><p>User Management permet à l’utilisateur de se connecter ou refuse l’accès au produit.</p></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Si le fuseau horaire du serveur est différent du fuseau horaire du client, lorsque vous utilisez le fichier WSDL pour le service AEM Forms Generate PDF sur une pile SOAP native utilisant un client .NET sur une grappe WebSphere Application Server, l’erreur d’authentification User Management suivante peut se produire :

`[com.adobe.idp.um.webservices.WSSecurityHandler] errorCode:12803 errorCodeHEX:0x3203 message:WSSecurityHandler: UM authenticate returns exception : An error was discovered processing the <wsse:Security> header. (WSSecurityEngine: Invalid timestamp The security semantics of message have expired).`

**Présentation de la gestion des répertoires**

User Management est fourni avec un prestataire d’annuaire (DirectoryManagerService) qui prend en charge les connexions aux annuaires LDAP. Si votre entreprise utilise un référentiel non LDAP pour stocker les enregistrements d’utilisateurs, vous pouvez créer votre propre prestataire d’annuaire qui fonctionne avec votre référentiel.

Les prestataires d’annuaire récupèrent les enregistrements d’un magasin d’utilisateurs à la demande de User Management. User Management met régulièrement en cache les enregistrements d’utilisateurs et de groupes dans la base de données afin d’améliorer les performances.

Le prestataire d’annuaire peut être utilisé pour synchroniser la base de données User Management avec la banque d’utilisateurs. Cette étape permet de s’assurer que toutes les informations d’annuaire des utilisateurs et tous les enregistrements d’utilisateurs et de groupes sont à jour.

En outre, DirectoryManagerService vous permet de créer et de gérer des domaines. Les domaines définissent différentes bases d’utilisateurs. Les limites d’un domaine sont généralement définies en fonction de la manière dont votre organisation est structurée ou dont votre magasin d’utilisateurs est configuré. Les domaines User Management fournissent des paramètres de configuration que les fournisseurs d’authentification et les prestataires d’annuaire utilisent.

Dans le fichier XML de configuration exporté par User Management, le noeud racine dont la valeur d’attribut est `Domains` contient un élément XML pour chaque domaine défini pour User Management. Chacun de ces éléments contient d’autres éléments qui définissent les aspects du domaine associés à des prestataires spécifiques.

**Présentation des valeurs objectSID**

Lors de l’utilisation de Principale Directory, il est important de comprendre qu’une `objectSID` valeur n’est pas un attribut unique sur plusieurs domaines. Cette valeur stocke l’identifiant de sécurité d’un objet. Dans un environnement de plusieurs domaines (par exemple, une arborescence de domaines), la `objectSID` valeur peut être différente.

Une `objectSID` valeur change si un objet est déplacé d&#39;un domaine Principale Directory vers un autre. Certains objets ont la même `objectSID` valeur n’importe où dans le domaine. Par exemple, les groupes tels que BUILTIN\Administrators, BUILTIN\Power Users, etc., auraient la même `objectSID` valeur indépendamment des domaines. Ces `objectSID` valeurs sont bien connues.

## Adding Users {#adding-users}

Vous pouvez utiliser l’API Service Directory Manager (Java et le service Web) pour ajouter des utilisateurs par programmation à AEM Forms. Après avoir ajouté un utilisateur, vous pouvez l’utiliser lors d’une opération de service nécessitant un utilisateur. Par exemple, vous pouvez affecter une tâche au nouvel utilisateur.

### Résumé des étapes {#summary-of-steps}

Pour ajouter un utilisateur, procédez comme suit :

1. Incluez des fichiers de projet.
1. Créez un client DirectoryManagerService.
1. Définissez les informations utilisateur.
1. Ajoutez l’utilisateur à AEM Forms.
1. Vérifiez que l’utilisateur est ajouté.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, incluez les fichiers proxy.

**Création d’un client DirectoryManagerService**

Avant de pouvoir exécuter une opération de service Directory Manager par programmation, créez un client API de service Directory Manager.

**Définition des informations utilisateur**

Lorsque vous ajoutez un nouvel utilisateur à l’aide de l’API Service Directory Manager, définissez les informations de cet utilisateur. En règle générale, lorsque vous ajoutez un nouvel utilisateur, vous définissez les valeurs suivantes :

* **Nom** de domaine : Domaine auquel l’utilisateur appartient (par exemple, `DefaultDom`).
* **Valeur** de l&#39;identifiant utilisateur : Valeur d’identificateur de l’utilisateur (par exemple, `wblue`).
* **Type** principal : Type d’utilisateur (par exemple, vous pouvez spécifier `USER)`.
* **Prénom**: Nom donné à l’utilisateur (par exemple, `Wendy`).
* **Nom** de famille : Nom de famille de l’utilisateur (par exemple, `Blue)`.
* **Paramètres régionaux**: Informations sur les paramètres régionaux de l’utilisateur.

**Ajouter l&#39;utilisateur à AEM Forms**

Après avoir défini les informations utilisateur, vous pouvez ajouter l’utilisateur à AEM Forms. Pour ajouter un utilisateur, appelez la `DirectoryManagerServiceClient` `createLocalUser` méthode de l’objet.

**Vérification de l’ajout de l’utilisateur**

Vous pouvez vérifier que l’utilisateur a été ajouté pour vous assurer qu’aucun problème n’est survenu. Localisez le nouvel utilisateur à l’aide de la valeur d’identificateur d’utilisateur.

**Voir également**

[Ajouter les utilisateurs à l’aide de l’API Java](users.md#add-users-using-the-java-api)

[Ajouter les utilisateurs à l’aide de l’API du service Web](users.md#add-users-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Suppression d’utilisateurs](users.md#deleting-users)

### Ajouter les utilisateurs à l’aide de l’API Java {#add-users-using-the-java-api}

Ajoutez les utilisateurs à l’aide de l’API Service Directory Manager (Java) :

1. Incluez des fichiers de projet.

   Incluez des fichiers JAR client, tels que adobe-usermanager-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un client DirectoryManagerServices.

   Créez un `DirectoryManagerServiceClient` objet en utilisant son constructeur et en transmettant un `ServiceClientFactory` objet contenant des propriétés de connexion.

1. Définissez les informations utilisateur.

   * Créez un objet `UserImpl` en utilisant son constructeur.
   * Définissez le nom demain en appelant la `UserImpl` `setDomainName` méthode de l’objet. Transmettez une valeur de chaîne qui spécifie le nom de domaine.
   * Définissez le type principal en appelant la `UserImpl` méthode de l’ `setPrincipalType` objet. Transmettez une valeur de chaîne qui spécifie le type d’utilisateur. Par exemple, vous pouvez spécifier `USER`.
   * Définissez la valeur de l’identifiant utilisateur en appelant la `UserImpl` méthode de l’ `setUserid` objet. Transmettez une valeur de chaîne qui spécifie la valeur de l’identifiant utilisateur. Par exemple, vous pouvez spécifier `wblue`.
   * Définissez le nom canonique en appelant la `UserImpl` méthode de l’ `setCanonicalName` objet. Transmettez une valeur de chaîne qui spécifie le nom canonique de l’utilisateur. Par exemple, vous pouvez spécifier `wblue`.
   * Définissez le nom donné en appelant la `UserImpl` méthode de l’ `setGivenName` objet. Transmettez une valeur de chaîne qui spécifie le prénom de l’utilisateur. Par exemple, vous pouvez spécifier `Wendy`.
   * Définissez le nom de famille en appelant la `UserImpl` méthode de l’ `setFamilyName` objet. Transmettez une valeur de chaîne qui spécifie le nom de famille de l’utilisateur. Par exemple, vous pouvez spécifier `Blue`.

   >[!NOTE]
   >
   >Appelez une méthode qui appartient à l’ `UserImpl` objet pour définir d’autres valeurs. Par exemple, vous pouvez définir la valeur du paramètre régional en appelant la `UserImpl` méthode de l’ `setLocale` objet.

1. Ajoutez l’utilisateur à AEM Forms.

   Appelez la méthode `DirectoryManagerServiceClient` de l’ `createLocalUser` objet et transmettez les valeurs suivantes :

   * Objet `UserImpl` représentant le nouvel utilisateur
   * Valeur de chaîne représentant le mot de passe de l’utilisateur.

   La `createLocalUser` méthode renvoie une valeur de chaîne qui spécifie la valeur de l’identifiant utilisateur local.

1. Vérifiez que l’utilisateur a été ajouté.

   * Créez un objet `PrincipalSearchFilter` en utilisant son constructeur.
   * Définissez la valeur de l’identifiant utilisateur en appelant la `PrincipalSearchFilter` méthode de l’ `setUserId` objet. Transmettez une valeur de chaîne qui représente la valeur de l’identifiant utilisateur.
   * Invoke the `DirectoryManagerServiceClient` object’s `findPrincipals` method and pass the `PrincipalSearchFilter` object. Cette méthode renvoie une `java.util.List` instance, où chaque élément est un `User` objet. Effectuez une itération sur l’ `java.util.List` instance pour localiser l’utilisateur.

**Voir également**

[Résumé des étapes](users.md#summary-of-steps)

[Début rapide (mode SOAP) : Ajouter les utilisateurs à l’aide de l’API Java](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-adding-users-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Ajouter les utilisateurs à l’aide de l’API du service Web {#add-users-using-the-web-service-api}

Ajoutez les utilisateurs à l’aide de l’API Service Directory Manager (service Web) :

1. Incluez des fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Veillez à utiliser la définition WSDL suivante pour la référence de service : `http://localhost:8080/soap/services/DirectoryManagerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un client DirectoryManagerService.

   * Create a `DirectoryManagerServiceClient` object by using its default constructor.
   * Create a `DirectoryManagerServiceClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/DirectoryManagerService?blob=mtom`). Vous n’avez pas besoin d’utiliser l’ `lc_version` attribut. Cet attribut est utilisé lorsque vous créez une référence de service. Assurez-vous de spécifier `?blob=mtom`.
   * Créez un `System.ServiceModel.BasicHttpBinding` objet en obtenant la valeur du `DirectoryManagerServiceClient.Endpoint.Binding` champ. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le `System.ServiceModel.BasicHttpBinding` champ de l’ `MessageEncoding` objet sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en exécutant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `DirectoryManagerServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `DirectoryManagerServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Définissez les informations utilisateur.

   * Créez un objet `UserImpl` en utilisant son constructeur.
   * Définissez le nom demain en attribuant une valeur de chaîne au `UserImpl` `domainName` champ de l’objet.
   * Définissez le type principal en attribuant une valeur de chaîne au `UserImpl` `principalType` champ de l’objet. Par exemple, vous pouvez spécifier `USER`.
   * Définissez la valeur de l’identifiant utilisateur en attribuant une valeur de chaîne au `UserImpl` `userid` champ de l’objet.
   * Définissez la valeur de nom canonique en attribuant une valeur de chaîne au `UserImpl` champ de l’ `canonicalName` objet.
   * Définissez la valeur de nom donnée en attribuant une valeur de chaîne au `UserImpl` `givenName` champ de l’objet.
   * Définissez la valeur du nom de famille en attribuant une valeur de chaîne au `UserImpl` champ de l’ `familyName` objet.

1. Ajoutez l’utilisateur à AEM Forms.

   Appelez la méthode `DirectoryManagerServiceClient` de l’ `createLocalUser` objet et transmettez les valeurs suivantes :

   * Objet `UserImpl` représentant le nouvel utilisateur
   * Valeur de chaîne représentant le mot de passe de l’utilisateur.

   La `createLocalUser` méthode renvoie une valeur de chaîne qui spécifie la valeur de l’identifiant utilisateur local.

1. Vérifiez que l’utilisateur a été ajouté.

   * Créez un objet `PrincipalSearchFilter` en utilisant son constructeur.
   * Définissez la valeur d’identifiant utilisateur de l’utilisateur en attribuant une valeur de chaîne qui représente la valeur d’identifiant utilisateur au `PrincipalSearchFilter` `userId` champ de l’objet.
   * Invoke the `DirectoryManagerServiceClient` object’s `findPrincipals` method and pass the `PrincipalSearchFilter` object. Cette méthode renvoie un objet `MyArrayOfUser` de collection, où chaque élément est un `User` objet. Effectuez une itération dans la `MyArrayOfUser` collection pour localiser l’utilisateur.

**Voir également**

[Résumé des étapes](users.md#summary-of-steps)

[Appel de AEM Forms à l’aide de MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Appel de AEM Forms à l’aide de SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Suppression d’utilisateurs {#deleting-users}

Vous pouvez utiliser l’API Service Directory Manager (Java et le service Web) pour supprimer par programmation des utilisateurs d’AEM Forms. Après avoir supprimé un utilisateur, il ne peut plus être utilisé pour effectuer une opération de service nécessitant un utilisateur. Par exemple, vous ne pouvez pas affecter une tâche à un utilisateur supprimé.

### Résumé des étapes {#summary_of_steps-1}

Pour supprimer un utilisateur, procédez comme suit :

1. Incluez des fichiers de projet.
1. Créez un client DirectoryManagerService.
1. Indiquez l’utilisateur à supprimer.
1. Supprimez l’utilisateur de AEM Forms.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, incluez les fichiers proxy.

**Création d’un client DirectoryManagerService**

Avant de pouvoir exécuter par programmation une opération d’API de service Directory Manager, créez un client de service Directory Manager.

**Spécifier l&#39;utilisateur à supprimer**

Vous pouvez spécifier un utilisateur à supprimer à l’aide de la valeur d’identificateur de l’utilisateur.

**Supprimer l&#39;utilisateur d&#39;AEM Forms**

Pour supprimer un utilisateur, appelez la `DirectoryManagerServiceClient` `deleteLocalUser` méthode de l’objet.

**Voir également**

[Suppression d’utilisateurs à l’aide de l’API Java](users.md#delete-users-using-the-java-api)

[Suppression d’utilisateurs à l’aide de l’API de service Web](users.md#delete-users-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Ajouter des utilisateurs](users.md#adding-users)

### Suppression d’utilisateurs à l’aide de l’API Java {#delete-users-using-the-java-api}

Supprimez des utilisateurs à l’aide de l’API Service Directory Manager (Java) :

1. Incluez des fichiers de projet.

   Incluez des fichiers JAR client, tels que adobe-usermanager-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un client DirectoryManagerService.

   Créez un `DirectoryManagerServiceClient` objet en utilisant son constructeur et en transmettant un `ServiceClientFactory` objet contenant des propriétés de connexion.

1. Indiquez l’utilisateur à supprimer.

   * Créez un objet `PrincipalSearchFilter` en utilisant son constructeur.
   * Définissez la valeur de l’identifiant utilisateur en appelant la `PrincipalSearchFilter` méthode de l’ `setUserId` objet. Transmettez une valeur de chaîne qui représente la valeur de l’identifiant utilisateur.
   * Invoke the `DirectoryManagerServiceClient` object’s `findPrincipals` method and pass the `PrincipalSearchFilter` object. Cette méthode renvoie une `java.util.List` instance, où chaque élément est un `User` objet. Effectuez une itération sur l’ `java.util.List` instance pour localiser l’utilisateur à supprimer.

1. Supprimez l’utilisateur de AEM Forms.

   Appelez la `DirectoryManagerServiceClient` méthode de l’ `deleteLocalUser` objet et transmettez la valeur du `User` champ de l’ `oid` objet. Appelle la méthode `User` de l’ `getOid` objet. Utilisez l’ `User` objet récupéré de l’ `java.util.List` instance.

**Voir également**

[Résumé des étapes](users.md#summary-of-steps)

[Début rapide (mode EJB) : Suppression d’utilisateurs à l’aide de l’API Java](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-deleting-users-using-the-java-api)

[Début rapide (mode SOAP) : Suppression d’utilisateurs à l’aide de l’API Java](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-deleting-users-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Suppression d’utilisateurs à l’aide de l’API de service Web {#delete-users-using-the-web-service-api}

Supprimez des utilisateurs à l’aide de l’API Service Directory Manager (service Web) :

1. Incluez des fichiers de projet.

   Incluez des fichiers JAR client, tels que adobe-usermanager-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un client DirectoryManagerService.

   * Create a `DirectoryManagerServiceClient` object by using its default constructor.
   * Create a `DirectoryManagerServiceClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/DirectoryManagerService?blob=mtom`). Vous n’avez pas besoin d’utiliser l’ `lc_version` attribut. Cet attribut est utilisé lorsque vous créez une référence de service. Assurez-vous de spécifier `blob=mtom.`
   * Créez un `System.ServiceModel.BasicHttpBinding` objet en obtenant la valeur du `DirectoryManagerServiceClient.Endpoint.Binding` champ. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le `System.ServiceModel.BasicHttpBinding` champ de l’ `MessageEncoding` objet sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en exécutant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `DirectoryManagerServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `DirectoryManagerServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Indiquez l’utilisateur à supprimer.

   * Créez un objet `PrincipalSearchFilter` en utilisant son constructeur.
   * Définissez la valeur de l’identifiant utilisateur en attribuant une valeur de chaîne au `PrincipalSearchFilter` `userId` champ de l’objet.
   * Invoke the `DirectoryManagerServiceClient` object’s `findPrincipals` method and pass the `PrincipalSearchFilter` object. Cette méthode renvoie un objet `MyArrayOfUser` de collection, où chaque élément est un `User` objet. Effectuez une itération dans la `MyArrayOfUser` collection pour localiser l’utilisateur. L’ `User` objet récupéré de l’objet `MyArrayOfUser` de collection est utilisé pour supprimer l’utilisateur.

1. Supprimez l’utilisateur de AEM Forms.

   Supprimez l’utilisateur en transmettant la valeur `User` du champ de l’ `oid` objet à la `DirectoryManagerServiceClient` méthode de l’ `deleteLocalUser` objet.

**Voir également**

[Résumé des étapes](users.md#summary-of-steps)

[Appel de AEM Forms à l’aide de MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Appel de AEM Forms à l’aide de SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Création de groupes  {#creating-groups}

Vous pouvez utiliser l’API Service Directory Manager (Java et le service Web) pour créer par programmation des groupes AEM Forms. Après avoir créé un groupe, vous pouvez l’utiliser pour effectuer une opération de service nécessitant un groupe. Par exemple, vous pouvez affecter un utilisateur au nouveau groupe. (See [Managing Users and Groups](users.md#managing-users-and-groups).)

### Résumé des étapes {#summary_of_steps-2}

Pour créer un groupe, procédez comme suit :

1. Incluez des fichiers de projet.
1. Créez un client DirectoryManagerService.
1. Déterminez que le groupe n’existe pas.
1. Créez le groupe.
1. Exécutez une action avec le groupe.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires.

Les fichiers JAR suivants doivent être ajoutés au chemin de classe de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (requis si AEM Forms est déployé sur JBoss)
* jbossall-client.jar (requis si AEM Forms est déployé sur JBoss)

For information about the location of these JAR files, see [Including AEM Forms Java library files](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Création d’un client DirectoryManagerService**

Avant de pouvoir exécuter une opération de service Directory Manager par programmation, créez un client API de service Directory Manager.

**Déterminer si le groupe existe**

Lorsque vous créez un groupe, assurez-vous qu’il n’existe pas dans le même domaine. Autrement dit, deux groupes ne peuvent pas porter le même nom dans le même domaine. Pour effectuer cette tâche, effectuez une recherche et filtrez les résultats de la recherche en fonction de deux valeurs. Définissez le type principal sur `com.adobe.idp.um.api.infomodel.Principal.PRINCIPALTYPE_GROUP` pour vous assurer que seuls les groupes sont renvoyés. Veillez également à spécifier le nom de domaine.

**Création du groupe**

Après avoir déterminé que le groupe n’existe pas dans le domaine, créez-le et spécifiez les attributs suivants :

* **CommonName**: Nom du groupe.
* **Domaine**: Domaine dans lequel le groupe est ajouté.
* **Description**: Description du groupe.

**Exécution d’une action avec le groupe**

Après avoir créé un groupe, vous pouvez exécuter une action à l’aide de ce groupe. Par exemple, vous pouvez ajouter un utilisateur au groupe. Pour ajouter un utilisateur à un groupe, récupérez la valeur d’identificateur unique de l’utilisateur et du groupe. Transmettez ces valeurs à la `addPrincipalToLocalGroup` méthode.

**Voir également**

[Création de groupes à l’aide de l’API Java](users.md#create-groups-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Ajouter des utilisateurs](users.md#adding-users)

[Suppression d’utilisateurs](users.md#deleting-users)

### Création de groupes à l’aide de l’API Java {#create-groups-using-the-java-api}

Créez un groupe à l’aide de l’API Service Directory Manager (Java) :

1. Incluez des fichiers de projet.

   Incluez des fichiers JAR client, tels que adobe-usermanager-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un client DirectoryManagerService.

   Créez un `DirectoryManagerServiceClient` objet en utilisant son constructeur et en transmettant un `ServiceClientFactory` objet contenant des propriétés de connexion.

1. Déterminez si le groupe existe.

   * Créez un objet `PrincipalSearchFilter` en utilisant son constructeur.
   * Définissez le type principal en appelant l’ `PrincipalSearchFilter` objet de l’ `setPrincipalType` objet. Transmettez la valeur `com.adobe.idp.um.api.infomodel.Principal.PRINCIPALTYPE_GROUP`.
   * Définissez le domaine en appelant l’ `PrincipalSearchFilter` objet de l’ `setSpecificDomainName` objet. Transmettez une valeur de chaîne qui spécifie le nom de domaine.
   * Pour trouver un groupe, appelez la `DirectoryManagerServiceClient` méthode de l’ `findPrincipals` objet (une entité de sécurité peut être un groupe). Transmettez l’ `PrincipalSearchFilter` objet qui spécifie le type principal et le nom de domaine. Cette méthode renvoie une `java.util.List` instance où chaque élément est une `Group` instance. Chaque instance de groupe est conforme au filtre spécifié à l’aide de l’ `PrincipalSearchFilter` objet.
   * Effectuez une itération sur l’ `java.util.List` instance. Pour chaque élément, récupérez le nom du groupe. Assurez-vous que le nom du groupe n’est pas égal au nouveau nom du groupe.

1. Créez le groupe.

   * Si le groupe n’existe pas, appelez la `Group` `setCommonName` méthode de l’objet et transmettez une valeur de chaîne qui spécifie le nom du groupe.
   * Appelez la méthode `Group` de l’objet `setDescription` et transmettez une valeur de chaîne qui spécifie la description du groupe.
   * Appelez la `Group` `setDomainName` méthode de l’objet et transmettez une valeur de chaîne qui spécifie le nom de domaine.
   * Invoke the `DirectoryManagerServiceClient` object’s `createLocalGroup` method and pass the `Group` instance.

   La `createLocalUser` méthode renvoie une valeur de chaîne qui spécifie la valeur de l’identifiant utilisateur local.

1. Exécutez une action avec le groupe.

   * Créez un objet `PrincipalSearchFilter` en utilisant son constructeur.
   * Définissez la valeur de l’identifiant utilisateur en appelant la `PrincipalSearchFilter` méthode de l’ `setUserId` objet. Transmettez une valeur de chaîne qui représente la valeur de l’identifiant utilisateur.
   * Invoke the `DirectoryManagerServiceClient` object’s `findPrincipals` method and pass the `PrincipalSearchFilter` object. Cette méthode renvoie une `java.util.List` instance, où chaque élément est un `User` objet. Effectuez une itération sur l’ `java.util.List` instance pour localiser l’utilisateur.
   * Ajoutez un utilisateur au groupe en appelant la `DirectoryManagerServiceClient` `addPrincipalToLocalGroup` méthode de l’objet. Transmettez la valeur renvoyée par la `User` méthode de l’ `getOid` objet. Transmettez la valeur renvoyée par la `Group` méthode des objets `getOid` (utilisez l’ `Group` instance qui représente le nouveau groupe).

**Voir également**

[Résumé des étapes](users.md#summary-of-steps)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Gestion des utilisateurs et des groupes {#managing-users-and-groups}

Cette rubrique décrit comment vous pouvez utiliser (Java) pour attribuer, supprimer et requête par programmation des domaines, des utilisateurs et des groupes.

>[!NOTE]
>
>Lors de la configuration d’un domaine, vous devez définir l’identifiant unique des groupes et des utilisateurs. L’attribut choisi ne doit pas seulement être unique dans l’environnement LDAP, mais doit également être immuable et ne peut pas être modifié dans l’annuaire. Cet attribut doit également être d&#39;un type de données de chaîne simple (la seule exception actuellement autorisée pour Principale Directory 2000/2003 est `"objectsid"`, ce qui est une valeur binaire). L&#39;attribut Novell eDirectory `"GUID"`, par exemple, n&#39;est pas un type de données de chaîne simple et ne fonctionnera donc pas.

* Pour Principale Directory, utilisez `"objectsid"`.
* Pour SunOne, utilisez `"nsuniqueid"`.

>[!NOTE]
>
>La création de plusieurs utilisateurs et groupes locaux pendant la synchronisation d’un annuaire LDAP n’est pas prise en charge. Toute tentative est susceptible d’entraîner des erreurs.

### Résumé des étapes {#summary_of_steps-3}

Pour gérer les utilisateurs et les groupes, procédez comme suit :

1. Incluez des fichiers de projet.
1. Créez un client DirectoryManagerService.
1. Appelez les opérations d’utilisateur ou de groupe appropriées.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

**Création d’un client DirectoryManagerService**

Avant de pouvoir exécuter une opération de service Directory Manager par programmation, vous devez créer un client de service Directory Manager. Avec l’API Java, cela se fait en créant un `DirectoryManagerServiceClient` objet. Avec l’API du service Web, cela se fait en créant un `DirectoryManagerServiceService` objet.

**Appeler les opérations d’utilisateur ou de groupe appropriées**

Une fois le client de service créé, vous pouvez appeler les opérations de gestion des utilisateurs ou des groupes. Le client de service vous permet d’attribuer, de supprimer et de requête des domaines, des utilisateurs et des groupes. Notez qu&#39;il est possible d&#39;ajouter une entité de sécurité d&#39;annuaire ou une entité de sécurité locale à un groupe local, mais qu&#39;il n&#39;est pas possible d&#39;ajouter une entité de sécurité locale à un groupe d&#39;annuaire.

**Voir également**

[Gestion des utilisateurs et des groupes à l’aide de l’API Java](users.md#managing-users-and-groups-using-the-java-api)

[Gestion des utilisateurs et des groupes à l’aide de l’API du service Web](users.md#managing-users-and-groups-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Débuts rapides de l’API User Manager](/help/forms/developing/user-manager-java-api-quick.md#user-manager-java-api-quick-start-soap)

### Gestion des utilisateurs et des groupes à l’aide de l’API Java {#managing-users-and-groups-using-the-java-api}

Pour gérer par programmation les utilisateurs, les groupes et les domaines à l’aide de Java, effectuez les tâches suivantes :

1. Incluez des fichiers de projet.

   Incluez des fichiers JAR client, tels que adobe-usermanager-client.jar, dans le chemin de classe de votre projet Java. Pour plus d’informations sur l’emplacement de ces fichiers, voir [Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

1. Créez un client DirectoryManagerService.

   Créez un `DirectoryManagerServiceClient` objet en utilisant son constructeur et en transmettant un `ServiceClientFactory` objet contenant des propriétés de connexion. Pour plus d’informations, voir [Définition des propriétés ](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)*de connexion.*

1. Appelez les opérations d’utilisateur ou de groupe appropriées.

   Pour rechercher un utilisateur ou un groupe, appelez l’une des méthodes de recherche des entités de l’ `DirectoryManagerServiceClient` objet (une entité de sécurité pouvant être un utilisateur ou un groupe). Dans l’exemple ci-dessous, la `findPrincipals` méthode est appelée à l’aide d’un filtre de recherche (un `PrincipalSearchFilter` objet).

   Dans ce cas, étant donné que la valeur renvoyée est un `java.util.List` objet contenant `Principal` des objets, effectuez une itération dans le résultat et projetez les `Principal` objets vers des objets `User` ou `Group` .

   A l’aide du résultat `User` ou de l’ `Group` objet (qui héritent tous deux de l’ `Principal` interface), récupérez les informations dont vous avez besoin dans vos workflows. Par exemple, les valeurs de nom de domaine et de nom canonique, combinées, identifient de manière unique une entité de sécurité. Ils sont récupérés en appelant les méthodes `Principal``getDomainName` et `getCanonicalName` de l’objet, respectivement.

   Pour supprimer un utilisateur local, appelez la `DirectoryManagerServiceClient` `deleteLocalUser` méthode de l’objet et transmettez son identifiant.

   Pour supprimer un groupe local, appelez la `DirectoryManagerServiceClient` `deleteLocalGroup` méthode de l’objet et transmettez l’identifiant du groupe.

**Voir également**

[Résumé des étapes](users.md#summary-of-steps)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Gestion des utilisateurs et des groupes à l’aide de l’API du service Web {#managing-users-and-groups-using-the-web-service-api}

Pour gérer par programmation les utilisateurs, les groupes et les domaines à l’aide de l’API Service Directory Manager (service Web), effectuez les tâches suivantes :

1. Incluez des fichiers de projet.

   * Créez un assembly client Microsoft .NET qui consomme le fichier WSDL du gestionnaire de répertoires. (Voir [Appel d’AEM Forms à l’aide du codage](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)Base64.)
   * Référencez l&#39;assembly client Microsoft .NET. (voir [Création d&#39;un assembly client .NET utilisant le codage](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)Base64).

1. Créez un client DirectoryManagerService.

   Créez un `DirectoryManagerServiceService` objet en utilisant le constructeur de votre classe proxy.

1. Appelez les opérations d’utilisateur ou de groupe appropriées.

   Pour rechercher un utilisateur ou un groupe, appelez l’une des méthodes de recherche des entités de l’ `DirectoryManagerServiceService` objet (une entité de sécurité pouvant être un utilisateur ou un groupe). Dans l’exemple ci-dessous, la `findPrincipalsWithFilter` méthode est appelée à l’aide d’un filtre de recherche (un `PrincipalSearchFilter` objet). Lors de l’utilisation d’un `PrincipalSearchFilter` objet, les entités locales ne sont renvoyées que si la `isLocal` propriété est définie sur `true`. Ce comportement est différent de ce qui se produirait avec l’API Java.

   >[!NOTE]
   >
   >Si le nombre maximal de résultats n&#39;est pas spécifié dans le filtre de recherche (par le `PrincipalSearchFilter.resultsMax` champ), un maximum de 1 000 résultats sont renvoyés. Il s’agit d’un comportement différent de ce qui se produit avec l’API Java, où 10 résultats sont la valeur maximale par défaut. En outre, les méthodes de recherche telles que `findGroupMembers` ne retourneront aucun résultat à moins que le nombre maximal de résultats ne soit spécifié dans le filtre de recherche (par exemple, par l’intermédiaire du `GroupMembershipSearchFilter.resultsMax` champ). Cela s&#39;applique à tous les filtres de recherche qui héritent de la `GenericSearchFilter` classe. For more information, see [AEM Forms API Reference](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

   Dans ce cas, étant donné que la valeur renvoyée est un `object[]` objet contenant `Principal` des objets, effectuez une itération dans le résultat et projetez les `Principal` objets vers des objets `User` ou `Group` .

   A l’aide du résultat `User` ou de l’ `Group` objet (qui héritent tous deux de l’ `Principal` interface), récupérez les informations dont vous avez besoin dans vos workflows. Par exemple, les valeurs de nom de domaine et de nom canonique, combinées, identifient de manière unique une entité de sécurité. Ils sont récupérés en appelant respectivement les champs `Principal``domainName` et `canonicalName` de l’objet.

   Pour supprimer un utilisateur local, appelez la `DirectoryManagerServiceService` `deleteLocalUser` méthode de l’objet et transmettez son identifiant.

   Pour supprimer un groupe local, appelez la `DirectoryManagerServiceService` `deleteLocalGroup` méthode de l’objet et transmettez l’identifiant du groupe.

**Voir également**

[Résumé des étapes](users.md#summary-of-steps)

[Appel de AEM Forms à l’aide de MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## Gestion des rôles et des autorisations {#managing-roles-and-permissions}

Cette rubrique décrit comment vous pouvez utiliser l’API du service Authorization Manager (Java) pour attribuer, supprimer et déterminer des rôles et des autorisations par programmation.

En AEM Forms, un *rôle* est un groupe d’autorisations d’accès à une ou plusieurs ressources au niveau du système. Ces autorisations sont créées via User Management et appliquées par les composants de service. Par exemple, un administrateur peut attribuer le rôle &quot;Auteur du jeu de stratégies&quot; à un groupe d’utilisateurs. Le Rights Management autoriserait alors les utilisateurs de ce groupe ayant ce rôle à créer des jeux de stratégies via Administration Console.

Il existe deux types de rôles : *rôles* par défaut et rôles ** personnalisés. Les rôles par défaut (rôles *système)* résident déjà en AEM Forms. Il est supposé que les rôles par défaut ne peuvent pas être supprimés ou modifiés par l’administrateur et sont donc immuables. Les rôles personnalisés créés par l&#39;administrateur, qui peuvent par la suite les modifier ou les supprimer, sont donc modifiables.

Les rôles facilitent la gestion des autorisations. Lorsqu’un rôle est attribué à une entité de sécurité, un ensemble d’autorisations est automatiquement attribué à cette entité de sécurité et toutes les décisions spécifiques liées à l’accès pour l’entité de sécurité sont basées sur cet ensemble global d’autorisations attribuées.

### Résumé des étapes {#summary_of_steps-4}

Pour gérer les rôles et les autorisations, effectuez les étapes suivantes :

1. Incluez des fichiers de projet.
1. Créez un client AuthorizationManagerService.
1. Appelez le rôle approprié ou les opérations d’autorisation.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

**Création d’un client AuthorizationManagerService**

Avant de pouvoir exécuter par programmation une opération User Management AuthorizationManagerService, vous devez créer un client AuthorizationManagerService. Avec l’API Java, cela se fait en créant un `AuthorizationManagerServiceClient` objet.

**Appeler le rôle approprié ou les opérations d’autorisation**

Une fois le client de service créé, vous pouvez appeler les opérations de rôle ou d’autorisation. Le client de service vous permet d’attribuer, de supprimer et de déterminer des rôles et des autorisations.

**Voir également**

[Gestion des rôles et des autorisations à l’aide de l’API Java](users.md#managing-roles-and-permissions-using-the-java-api)

[Gestion des rôles et des autorisations à l’aide de l’API du service Web](users.md#managing-roles-and-permissions-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Débuts rapides de l’API User Manager](/help/forms/developing/user-manager-java-api-quick.md#user-manager-java-api-quick-start-soap)

### Gestion des rôles et des autorisations à l’aide de l’API Java {#managing-roles-and-permissions-using-the-java-api}

Pour gérer les rôles et les autorisations à l’aide de l’API du service Authorization Manager (Java), effectuez les tâches suivantes :

1. Incluez des fichiers de projet.

   Incluez des fichiers JAR client, tels que adobe-usermanager-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un client AuthorizationManagerService.

   Créez un `AuthorizationManagerServiceClient` objet en utilisant son constructeur et en transmettant un `ServiceClientFactory` objet contenant des propriétés de connexion.

1. Appelez le rôle approprié ou les opérations d’autorisation.

   Pour attribuer un rôle à une entité de sécurité, appelez la `AuthorizationManagerServiceClient` `assignRole` méthode de l’objet et transmettez les valeurs suivantes :

   * Objet `java.lang.String` contenant l’identifiant de rôle
   * Tableau d&#39;objets `java.lang.String` contenant les identifiants principaux.

   Pour supprimer un rôle d’une entité de sécurité, appelez la `AuthorizationManagerServiceClient` `unassignRole` méthode de l’objet et transmettez les valeurs suivantes :

   * Objet `java.lang.String` contenant l’identifiant de rôle.
   * Tableau d&#39;objets `java.lang.String` contenant les identifiants principaux.


**Voir également**

[Résumé des étapes](users.md#summary-of-steps)

[Début rapide (mode SOAP) : Gestion des rôles et des autorisations à l’aide de l’API Java](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-managing-roles-and-permissions-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Gestion des rôles et des autorisations à l’aide de l’API du service Web {#managing-roles-and-permissions-using-the-web-service-api}

Gérez les rôles et les autorisations à l’aide de l’API Service Authorization Manager (service Web) :

1. Incluez des fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Assurez-vous d’utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/AuthorizationManagerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un client AuthorizationManagerService.

   * Créez un `AuthorizationManagerServiceClient` objet en utilisant son constructeur par défaut.
   * Créez un `AuthorizationManagerServiceClient.Endpoint.Address` objet en utilisant le `System.ServiceModel.EndpointAddress` constructeur. Transférez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/AuthorizationManagerService?blob=mtom`). Vous n’avez pas besoin d’utiliser l’ `lc_version` attribut. Cet attribut est utilisé lorsque vous créez une référence de service.
   * Créez un `System.ServiceModel.BasicHttpBinding` objet en obtenant la valeur du `AuthorizationManagerServiceClient.Endpoint.Binding` champ. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le `System.ServiceModel.BasicHttpBinding` champ de l’ `MessageEncoding` objet sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en exécutant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `AuthorizationManagerServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `AuthorizationManagerServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Appelez le rôle approprié ou les opérations d’autorisation.

   Pour attribuer un rôle à une entité de sécurité, appelez la `AuthorizationManagerServiceClient` `assignRole` méthode de l’objet et transmettez les valeurs suivantes :

   * Objet `string` contenant l’identifiant de rôle
   * Objet `MyArrayOf_xsd_string` contenant les identifiants principaux.

   Pour supprimer un rôle d’une entité de sécurité, appelez la `AuthorizationManagerServiceService` `unassignRole` méthode de l’objet et transmettez les valeurs suivantes :

   * Objet `string` contenant l’identifiant de rôle.
   * Tableau d&#39;objets `string` contenant les identifiants principaux.


**Voir également**

[Résumé des étapes](users.md#summary-of-steps)

[Appel de AEM Forms à l’aide de MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## Authentification des utilisateurs {#authenticating-users}

Cette rubrique décrit comment vous pouvez utiliser l’API du service Authentication Manager (Java) pour permettre à vos applications clientes d’authentifier les utilisateurs par programmation.

L’authentification de l’utilisateur peut être nécessaire pour interagir avec une base de données d’entreprise ou d’autres référentiels d’entreprise qui stockent des données sécurisées.

Prenons, par exemple, un scénario où un utilisateur saisit un nom d’utilisateur et un mot de passe dans une page Web et envoie les valeurs à un serveur d’applications J2EE hébergeant Forms. Une application personnalisée Forms peut authentifier l’utilisateur avec le service Authentication Manager.

Si l’authentification réussit, l’application accède à une base de données d’entreprise sécurisée. Dans le cas contraire, un message est envoyé à l’utilisateur pour lui indiquer qu’il n’est pas un utilisateur autorisé.

Le diagramme suivant illustre le flux logique de l’application.

![au_au_umauth_process](assets/au_au_umauth_process.png)

Le tableau suivant décrit les étapes de ce diagramme.

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
   <td><p>L’utilisateur accède à un site Web et spécifie un nom d’utilisateur et un mot de passe. Ces informations sont envoyées à un serveur d’applications J2EE hébergeant AEM Forms.</p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>Les informations d’identification de l’utilisateur sont authentifiées avec le service Authentication Manager. Si les informations d’identification de l’utilisateur sont valides, le processus passe à l’étape 3. Dans le cas contraire, un message est envoyé à l’utilisateur pour lui indiquer qu’il n’est pas un utilisateur autorisé.</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>Les informations utilisateur et une conception de formulaire sont récupérées dans une base de données d’entreprise sécurisée. </p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>Les informations utilisateur sont fusionnées avec une conception de formulaire et le formulaire est rendu à l’utilisateur. </p></td>
  </tr>
 </tbody>
</table>

### Résumé des étapes {#summary_of_steps-5}

Pour authentifier par programmation un utilisateur, procédez comme suit :

1. Incluez des fichiers de projet.
1. Créez un client AuthenticationManagerService.
1. Appelez l’opération d’authentification.
1. Si nécessaire, récupérez le contexte afin que l’application cliente puisse le transférer à un autre service AEM Forms pour authentification.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

**Création d’un client AuthenticationManagerService**

Avant de pouvoir authentifier un utilisateur par programmation, vous devez créer un client AuthenticationManagerService. Lors de l’utilisation de l’API Java, créez un `AuthenticationManagerServiceClient` objet.

**Appeler l’opération d’authentification**

Après avoir créé le client de service, vous pouvez appeler l’opération d’authentification. Cette opération nécessite des informations sur l’utilisateur, telles que son nom et son mot de passe. Si l’utilisateur ne s’authentifie pas, une exception est générée.

**Récupérer le contexte d&#39;authentification**

Une fois l’utilisateur authentifié, vous pouvez créer un contexte basé sur l’utilisateur authentifié. Vous pouvez ensuite utiliser le contenu pour appeler un autre service AEM Forms. Par exemple, vous pouvez utiliser le contexte pour créer un document PDF `EncryptionServiceClient` et le chiffrer avec un mot de passe. Assurez-vous que l’utilisateur authentifié dispose du rôle nommé `Services User` nécessaire pour appeler un service AEM Forms.

**Voir également**

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Débuts rapides de l’API User Manager](/help/forms/developing/user-manager-java-api-quick.md#user-manager-java-api-quick-start-soap)

[Chiffrement de Documents PDF avec un mot de passe](/help/forms/developing/encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### Authentification d’un utilisateur à l’aide de l’API Java {#authenticate-a-user-using-the-java-api}

Authentifiez un utilisateur à l’aide de l’API du service Authentication Manager (Java) :

1. Incluez des fichiers de projet.

   Incluez des fichiers JAR client, tels que adobe-usermanager-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un client AuthenticationManagerServices.

   Créez un `AuthenticationManagerServiceClient` objet en utilisant son constructeur et en transmettant un `ServiceClientFactory` objet contenant des propriétés de connexion.

1. Appelez l’opération d’authentification.

   Appelez la méthode `AuthenticationManagerServiceClient` de l’ `authenticate` objet et transmettez les valeurs suivantes :

   * Objet `java.lang.String` contenant le nom de l’utilisateur.
   * Tableau d’octets (objet `byte[]` ) contenant le mot de passe de l’utilisateur. Vous pouvez obtenir l’ `byte[]` objet en appelant la `java.lang.String` méthode de l’ `getBytes` objet.

   La méthode authenticate renvoie un `AuthResult` objet, qui contient des informations sur l’utilisateur authentifié.

1. Récupérez le contexte d’authentification.

   Appelez la `ServiceClientFactory` méthode de l’ `getContext` objet, qui renvoie un `Context` objet.

   Appelez ensuite la `Context` méthode de l’ `initPrincipal` objet, puis transmettez le `AuthResult`.

### Authentification d’un utilisateur à l’aide de l’API du service Web {#authenticate-a-user-using-the-web-service-api}

Authentifiez un utilisateur à l’aide de l’API Service Authentication Manager (service Web) :

1. Incluez des fichiers de projet.

   * Créez un assembly client Microsoft .NET qui consomme le fichier WSDL d&#39;Authentication Manager. (Voir [Appel d’AEM Forms à l’aide du codage](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)Base64.)
   * Référencez l&#39;assembly client Microsoft .NET. (Voir &quot;Référence à l&#39;assembly client .NET&quot; dans [Appel d&#39;AEM Forms à l&#39;aide du codage](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)Base64.)

1. Créez un client AuthenticationManagerService.

   Créez un `AuthenticationManagerServiceService` objet en utilisant le constructeur de votre classe proxy.

1. Appelez l’opération d’authentification.

   Appelez la méthode `AuthenticationManagerServiceClient` de l’ `authenticate` objet et transmettez les valeurs suivantes :

   * Objet `string` contenant le nom de l’utilisateur.
   * Tableau d’octets (objet `byte[]` ) contenant le mot de passe de l’utilisateur. Vous pouvez obtenir l’ `byte[]` objet en convertissant un `string` objet contenant le mot de passe en un `byte[]` tableau à l’aide de la logique illustrée dans l’exemple ci-dessous.
   * La valeur renvoyée sera un `AuthResult` objet, qui peut être utilisé pour récupérer des informations sur l’utilisateur. Dans l’exemple ci-dessous, les informations de l’utilisateur sont récupérées en obtenant d’abord le `AuthResult` champ de l’objet, puis en obtenant ensuite les champs `authenticatedUser` et `User` de l’objet `canonicalName` `domainName` résultant.

**Voir également**

[Appel de AEM Forms à l’aide de MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Appel de AEM Forms à l’aide de SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Synchronisation par programmation des utilisateurs {#programmatically-synchronizing-users}

Vous pouvez synchroniser les utilisateurs par programmation à l’aide de l’API User Management. Lorsque vous synchronisez des utilisateurs, vous mettez à jour AEM Forms avec les données utilisateur qui se trouvent dans votre référentiel d’utilisateurs. Supposons, par exemple, que vous ajoutiez de nouveaux utilisateurs à votre référentiel d’utilisateurs. Une fois que vous avez effectué une synchronisation, les nouveaux utilisateurs deviennent des utilisateurs AEM forms. En outre, les utilisateurs qui ne se trouvent plus dans votre référentiel d’utilisateurs sont supprimés d’AEM Forms.

Le diagramme suivant montre l’AEM Forms synchronisé avec un référentiel utilisateur.

![ps_ps_umauth_sync](assets/ps_ps_umauth_sync.png)

Le tableau suivant décrit les étapes de ce diagramme.

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
   <td><p>Un utilisateur peut vue les informations utilisateur mises à jour. </p></td>
  </tr>
 </tbody>
</table>

### Résumé des étapes {#summary_of_steps-6}

Pour synchroniser les utilisateurs par programmation, procédez comme suit :

1. Incluez des fichiers de projet.
1. Créez un client UserManagerUtilServiceClient.
1. Spécifiez le domaine d’entreprise.
1. Appelez l’opération d’authentification.
1. Déterminer si l&#39;opération de synchronisation est terminée

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

**Création d’un UserManagerUtilServiceClientclient**

Avant de pouvoir synchroniser les utilisateurs par programmation, vous devez créer un `UserManagerUtilServiceClient` objet.

**Spécifier le domaine d’entreprise**

Avant d’effectuer une synchronisation à l’aide de l’API User Management, vous devez spécifier le domaine d’entreprise auquel appartiennent les utilisateurs. Vous pouvez spécifier un ou plusieurs domaines d’entreprise. Avant d’effectuer une synchronisation par programmation, vous devez configurer un domaine d’entreprise à l’aide d’Administration Console. (See [administration help](https://www.adobe.com/go/learn_aemforms_admin_63).)

**Appeler l’opération de synchronisation**

Après avoir spécifié un ou plusieurs domaines d’entreprise, vous pouvez effectuer l’opération de synchronisation. Le temps nécessaire pour effectuer cette opération dépend du nombre d’enregistrements d’utilisateurs situés dans le référentiel d’utilisateurs.

**Déterminer si l&#39;opération de synchronisation est terminée**

Après avoir exécuté une opération de synchronisation par programmation, vous pouvez déterminer si l’opération est terminée.

**Voir également**

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Débuts rapides de l’API User Manager](/help/forms/developing/user-manager-java-api-quick.md#user-manager-java-api-quick-start-soap)

[Chiffrement de Documents PDF avec un mot de passe](/help/forms/developing/encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### Synchronisation par programmation des utilisateurs à l’aide de l’API Java {#programmatically-synchronizing-users-using-the-java-api}

Synchronisez les utilisateurs à l’aide de l’API User Management (Java) :

1. Incluez des fichiers de projet.

   Incluez les fichiers JAR client, tels que adobe-usermanager-client.jar et adobe-usermanager-util-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un client UserManagerUtilServiceClient.

   Créez un `UserManagerUtilServiceClient` objet en utilisant son constructeur et en transmettant un `ServiceClientFactory` objet contenant des propriétés de connexion.

1. Spécifiez le domaine d’entreprise.

   * Appelez la méthode de l’ `UserManagerUtilServiceClient` objet `scheduleSynchronization` pour début de l’opération de synchronisation de l’utilisateur.
   * Créez une `java.util.Set` instance en utilisant un `HashSet` constructeur. Assurez-vous de spécifier `String` le type de données. Cette `Java.util.Set` instance stocke les noms de domaine auxquels s’applique l’opération de synchronisation.
   * Pour chaque nom de domaine à ajouter, appelez la méthode add de l’ `java.util.Set` objet et transmettez le nom de domaine.

1. Appelez l’opération de synchronisation.

   Appelez la `ServiceClientFactory` méthode de l’ `getContext` objet, qui renvoie un `Context` objet.

   Appelez ensuite la `Context` méthode de l’ `initPrincipal` objet, puis transmettez le `AuthResult`.

**Voir également**

[Synchronisation par programmation des utilisateurs](users.md#programmatically-synchronizing-users)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
