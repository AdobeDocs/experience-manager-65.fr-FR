---
title: Configurer les paramètres d’administration sécurisée d’AEM Forms sur JEE
description: Découvrez comment administrer des comptes d’utilisateurs et services qui, contrairement à un environnement de développement privé, ne sont pas nécessaires dans un environnement de production AEM Forms sur JEE.
content-type: reference
topic-tags: Security
products: SG_EXPERIENCEMANAGER/6.4
role: Admin
exl-id: 40bc01b4-a59e-4420-81d6-2887857bddce
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '847'
ht-degree: 24%

---

# Configurer les paramètres d’administration sécurisée d’AEM Forms sur JEE {#configuring-secure-administration-settings-for-aem-forms-on-jee}

Découvrez comment administrer des comptes d’utilisateurs et services qui, contrairement à un environnement de développement privé, ne sont pas nécessaires dans un environnement de production AEM Forms sur JEE.

En règle générale, les développeurs n’utilisent pas l’environnement de production pour créer et tester leurs applications. Par conséquent, vous devez administrer des comptes d’utilisateurs et des services qui, bien que nécessaires dans un environnement de développement privé, ne sont pas requis dans un environnement de production.

Cet article décrit les méthodes permettant de réduire la surface d’attaque globale par le biais d’options d’administration fournies par AEM Forms on JEE.

## Désactivation de l’accès distant non essentiel aux services {#disabling-non-essential-remote-access-to-services}

Une fois AEM Forms on JEE installé et configuré, de nombreux services sont disponibles pour un appel distant sur SOAP et Enterprise JavaBeans™ (EJB). Le terme distant, dans ce cas, fait référence à tout appelant disposant d’un accès réseau aux ports SOAP, EJB ou Action Message Format (AMF) pour le serveur d’applications.

Bien que l’utilisation des services d’AEM Forms sur JEE implique la transmission d’informations d’identification valides pour un appelant autorisé, vous devriez limiter la possibilité d’accès distant aux seuls services dont vous souhaitez effectivement qu’ils soient accessibles à distance. Pour obtenir une accessibilité limitée, vous devez réduire au minimum l’ensemble des services accessibles à distance pour un système fonctionnel, puis activer l’appel distant pour les services supplémentaires dont vous avez besoin.

Les services AEM Forms on JEE ont toujours besoin d’au moins un accès SOAP. Ces services sont généralement requis par Workbench, mais comprennent également des services appelés par l’application Web Workspace.

Suivez cette procédure à l’aide de la page web Applications et services dans la console d’administration :

1. Connectez-vous à la console d’administration en saisissant l’URL suivante dans un navigateur web :

   ```java
            https://[host name]:'port'/adminui
   ```

1. Cliquez sur **Services > Applications et services > Préférences**.
1. Définissez les Préférences pour afficher jusqu’à 200 services et points de fin sur la même page.
1. Cliquez sur **Services** > **Applications et services** > **Gestion des points de fin**.
1. Sélectionner **EJB** de la **Fournisseur** répertorier, puis cliquez sur **Filtrer**.
1. Pour désactiver tous les points de fin EJB, cochez la case située en regard de chacun d’eux dans la liste et cliquez sur **Désactiver**.
1. Cliquez sur **Suivant** et répétez l’étape précédente pour tous les points de fin EJB. Assurez-vous qu’EJB est répertorié dans la colonne Fournisseur avant de désactiver les points de fin.
1. Sélectionner **SOAP** de la **Fournisseur** répertorier, puis cliquez sur **Filtrer**.
1. Pour supprimer les points de fin SOAP, cochez la case en regard de chacun d’eux dans la liste et cliquez sur **Supprimer**. Ne supprimez pas les points de fin suivants :

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
   * ApplicationManager

1. Cliquez sur **Suivant** et répétez l’étape précédente pour les points de fin SOAP qui ne figurent pas dans la liste ci-dessus. Assurez-vous que SOAP est répertorié dans la colonne Fournisseur avant de supprimer les points de fin.

## Désactivation des accès anonymes non indispensables à des services {#disabling-non-essential-anonymous-access-to-services}

Certains services de serveur Forms permettent un appel non authentifié (anonyme) pour certaines opérations. Cela signifie qu’une ou plusieurs opérations exposées par le service peuvent être appelées en tant qu’utilisateur authentifié ou en tant qu’aucun utilisateur authentifié.

1. Connectez-vous à Administration Console en saisissant l’URL suivante dans un navigateur Web :

   ```java
            https://[host name]:'port'/adminui
   ```

1. Cliquez sur **Services > Applications et services > Gestion des services**.
1. Cliquez sur le nom du service que vous souhaitez désactiver (par exemple, AuthenticationManagerService).
1. Cliquez sur l’**onglet Sécurité**, désélectionnez **Accès anonyme autorisé** et cliquez sur **Enregistrer**.
1. Effectuez les étapes 3 et 4 pour les services suivants :

   * AuthenticationManagerService
   * EJB
   * E-mail
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

   Si vous avez l’intention d’exposer l’un de ces services pour un appel distant, vous devez également envisager de désactiver l’accès anonyme pour ces services. Dans le cas contraire, tout appelant disposant d’un accès réseau à ce service peut appeler le service sans transmission d’informations d’identification valides.

   L’accès anonyme doit être désactivé pour les services qui ne sont pas nécessaires. De nombreux services internes requièrent l’activation de l’authentification anonyme, car ils doivent être appelés par potentiellement tout utilisateur du système sans préautorisation.

## Modification du délai d’expiration global par défaut {#changing-the-default-global-time-out}

Les utilisateurs finaux peuvent s’authentifier auprès d’AEM Forms via Workbench, les applications web d’AEM Forms ou des applications personnalisées qui appellent des services du serveur AEM Forms. Un paramètre de délai d’expiration permet de spécifier la durée pendant laquelle ces utilisateurs peuvent interagir avec AEM Forms (en utilisant une assertion SAML) avant d’être obligés de s’authentifier de nouveau. Le paramètre par défaut est de deux heures. Dans un environnement de production, la durée doit être réduite au nombre minimum de minutes acceptable.

### Réduction du délai de réauthentification {#minimize-reauthentication-time-limit}

1. Connectez-vous à Administration Console en saisissant l’URL suivante dans un navigateur Web :

   ```java
            https://[host name]:'port'/adminui
   ```

1. Cliquez sur **Paramètres > User Management > Configuration > Importer Et Exporter Des Fichiers De Configuration**.
1. Cliquez sur **Exporter** pour produire un fichier config.xml contenant les paramètres AEM Forms existants.
1. Ouvrez le fichier XML dans un éditeur et recherchez l’entrée suivante :

   `<entry key="assertionValidityInMinutes" value="120"/>`

1. Remplacez la valeur par un nombre supérieur à 5 (en minutes) et enregistrez le fichier.
1. Dans Administration Console, accédez à la page Importer et exporter des fichiers de configuration .
1. Saisissez le chemin d’accès au fichier config.xml modifié ou cliquez sur Parcourir pour y accéder.
1. Cliquez sur **Importer** pour charger le fichier config.xml modifié, puis cliquez sur **OK**.
