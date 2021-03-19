---
title: Configuration des paramètres d’administration sécurisée pour AEM Forms on JEE
seo-title: Configuration des paramètres d’administration sécurisée pour AEM Forms on JEE
description: Découvrez comment administrer des comptes d’utilisateurs et des services qui, bien que requis dans un environnement de développement privé, ne sont pas requis dans un environnement de production de AEM Forms on JEE.
seo-description: Découvrez comment administrer des comptes d’utilisateurs et des services qui, bien que requis dans un environnement de développement privé, ne sont pas requis dans un environnement de production de AEM Forms on JEE.
uuid: 04e45d06-f57d-406c-8228-15f483199430
content-type: reference
topic-tags: Security
products: SG_EXPERIENCEMANAGER/6.4
discoiquuid: d211d8b0-e75f-49c3-808d-5d0e26ad3a6b
role: Administrator
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '885'
ht-degree: 80%

---


# Configuration des paramètres d’administration sécurisée pour AEM Forms on JEE {#configuring-secure-administration-settings-for-aem-forms-on-jee}

Découvrez comment administrer des comptes d’utilisateurs et des services qui, bien que requis dans un environnement de développement privé, ne sont pas requis dans un environnement de production de AEM Forms on JEE.

En règle générale, les développeurs n’utilisent pas l’environnement de production pour construire et tester leurs applications. Pour cette raison, vous devez administrer des comptes utilisateur et des services qui, bien que nécessaires dans un environnement de développement privé, ne le sont pas dans un environnement de production.

Cet article décrit les méthodes que vous pouvez appliquer pour réduire la surface d’attaque globale en utilisant des options d’administration qu’AEM Forms sur JEE fournit.

## Désactivation des accès distants non indispensables à des services {#disabling-non-essential-remote-access-to-services}

Une fois qu’AEM Forms sur JEE est installé et configuré, de nombreux services sont accessibles par appel distant sur SOAP et Enterprise JavaBeans™ (EJB). Le terme « distant » renvoie ici à tout appelant disposant d’un accès réseau aux ports SOAP, EJB ou Action Message Format (AMF) du serveur d’applications.

Bien que l’utilisation des services d’AEM Forms sur JEE implique la transmission d’informations d’identification valides pour un appelant autorisé, vous devriez limiter la possibilité d’accès distant aux seuls services dont vous souhaitez effectivement qu’ils soient accessibles à distance. Pour limiter efficacement l’accessibilité, réduisez au minimum le nombre de services accessibles à distance sans gêner le fonctionnement du système, puis activez l’appel distant pour les services supplémentaires dont vous avez besoin.

Les services d’AEM Forms sur JEE doivent toujours disposer d’au moins un accès SOAP. Ces services sont généralement nécessaires pour Workbench, mais il peut également s’agir de services appelés par l’application Web Workspace.

Suivez cette procédure en utilisant la page Web Applications et services d’Administration Console :

1. Connectez-vous à Administration Console en saisissant l’URL suivante dans un navigateur Web :

   ```java
            https://[host name]:'port'/adminui
   ```

1. Cliquez sur **Services > Applications et services > Préférences**.
1. Définissez les préférences afin d’afficher jusqu’à 200 services et points de fin par page.
1. Cliquez sur **Services** > **Applications et services** > **Gestion des points de fin**.
1. Sélectionnez **EJB** depuis la liste **Fournisseur**, puis cliquez sur **Filtre**.
1. Pour désactiver tous les points de fin EJB, sélectionnez la case à cocher située en regard de chaque point de fin dans la liste et cliquez sur **Désactiver**.
1. Cliquez sur **Suivant** et répétez les étapes décrites ci-dessus pour chaque point de fin EJB. Assurez-vous qu’EJB figure dans la colonne Fournisseur avant de désactiver les points de fin.
1. Sélectionnez **SOAP** depuis la liste **Fournisseur**, puis cliquez sur **Filtre**.
1. Pour désactiver tous les points de fin SOAP, cochez la case située en regard de chaque point de fin dans la liste et cliquez sur **Supprimer**. Ne supprimez pas les points de fin suivants :

   * AuthenticationManagerService
   * DirectoryManagerService
   * JobManager
   * event_management_service
   * event_configuration_service
   * ProcessManager
   * TemplateManager
   * RepositoryService
   * TaskManagerService
   * TaskQueueManager
   * TaskManagerQueryService
   * WorkspaceSingleSignOn
   * Gestionnaire d’application

1. Cliquez sur **Suivant** et répétez les étapes précédentes pour chaque point de fin SOAP qui ne figure pas dans la liste ci-dessus. Assurez-vous que SOAP figure dans la colonne Fournisseur avant de supprimer les points de fin.

## Désactivation des accès anonymes non indispensables à des services  {#disabling-non-essential-anonymous-access-to-services}

Certains services du serveur de formulaires permettent d’appeler sans authentification (de manière anonyme) certaines opérations. Ceci signifie qu’il est possible d’appeler une ou plusieurs opérations exposées par le service en tant qu’utilisateur authentifié ou non.

1. Connectez-vous à la console d’administration en saisissant l’URL suivante dans un navigateur Web :

   ```java
            https://[host name]:'port'/adminui
   ```

1. Cliquez sur **Services > Applications et services > Gestion des services**.
1. Cliquez sur le nom du service à désactiver (par exemple, AuthenticationManagerService).
1. Cliquez sur l&#39;onglet **Sécurité**, désélectionnez **Accès anonyme autorisé**, puis cliquez sur **Enregistrer**.
1. Effectuez les étapes 3 et 4 pour les services suivants :

   * AuthenticationManagerService
   * EJB
   * Courrier électronique
   * JobManager
   * WatchedFolder
   * UsermanagerUtilService
   * Remoting
   * RepositoryProviderService
   * EMCDocumentumRepositoryProvider
   * IBMFilenetRepositoryProvider
   * FormAugmenter
   * TaskManagerService
   * TaskManagerConnector
   * TaskManagerQueryService
   * TaskQueueManager
   * TaskEndpointManager
   * UserService
   * WorkspaceSearchTemplateService
   * WorkspacePropertyService
   * OutputService
   * FormsService

   Si vous prévoyez d’exposer l’un de ces services pour les appels distants, vous devriez également envisager de désactiver l’accès anonyme pour ces services. Si vous ne le faites pas, tout appelant disposant d’un accès réseau à ce service pourra appeler le service sans spécifier d’informations d’identification valides.

   Nous vous conseillons de désactiver l’accès anonyme pour tous les services dont vous n’avez pas besoin. De nombreux services internes impliquent que l’authentification anonyme soit activée, car ils doivent pouvoir être appelés par potentiellement tout utilisateur du système sans préautorisation.

## Modification du délai d’expiration global par défaut {#changing-the-default-global-time-out}

Les utilisateurs finaux peuvent s’authentifier auprès d’AEM Forms par le biais de Workbench, d’applications Web AEM Forms ou d’applications personnalisées appelant les services de serveur AEM Forms. Un paramètre de délai d’expiration permet de spécifier la durée pendant laquelle ces utilisateurs peuvent interagir avec AEM Forms (en utilisant une assertion SAML) avant d’être obligés de s’authentifier de nouveau. Par défaut, ce paramètre est défini sur deux heures. Dans un environnement de production, cette durée doit être réduite au nombre minimum de minutes acceptable.

### Réduction au minimum de la durée limite avant réauthentification:  {#minimize-reauthentication-time-limit}

1. Connectez-vous à la console d’administration en saisissant l’URL suivante dans un navigateur Web :

   ```java
            https://[host name]:'port'/adminui
   ```

1. Cliquez sur **Paramètres > User Management > Configuration > Importer et exporter des fichiers de configuration**.
1. Cliquez sur **Exporter** pour produire un fichier config.xml contenant les paramètres d’AEM Forms existants.
1. Ouvrez le fichier XML dans un éditeur et recherchez l’entrée suivante :

   `<entry key=”assertionValidityInMinutes” value=”120”/>`

1. Spécifiez une valeur en minutes supérieure ou égale à 5 et enregistrez le fichier.
1. Dans la console d’administration, naviguez jusqu’à la page Importer et exporter des fichiers de configuration.
1. Saisissez le chemin d’accès au fichier config.xml modifié ou cliquez sur Parcourir pour le localiser.
1. Cliquez sur **Importer** pour télécharger le fichier config.xml, puis cliquez sur **OK**.

