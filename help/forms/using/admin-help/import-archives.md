---
title: Importation et gestion des archives de
seo-title: Importation et gestion des archives
description: Découvrez comment importer et gérer des archives.
seo-description: Découvrez comment importer et gérer des archives.
uuid: aa1613dd-6350-49a7-9643-44365e2acdcc
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/importing_and_managing_applications_and_archives
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: b6f6463a-2ae4-43d2-8d16-cc20a954e50e
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1465'
ht-degree: 100%

---


# Importation et gestion des archives {#import-and-manage-archives}

Importez et gérez les fichiers LCA créés avec Workbench via l’onglet Archives.

## Importation d’une archive {#import-an-archive}

1. Dans Administration Console, cliquez sur Services > Applications et services > Gestion des applications, puis sur l’onglet Archives.
1. Cliquez sur Importer.
1. Cliquez sur Parcourir pour localiser l’archive à importer puis sur Aperçu.
1. Passez en revue la liste des ressources et des objets qui seront installés avec l’archive. Assurez-vous de l’absence de conflits avec des ressources, objets ou configurations de services existants, car il n’existe pas de fonctionnalité d’annulation.

   Si vous choisissez d’importer les configurations de services, AEM forms importe tous les fichiers de configuration de processus (points de fin, profils de sécurité et paramètres de configuration des services) utilisés par les processus dans l’archive LCA.

1. Cliquez sur Importer.
1. Vérifiez les résultats de l’importation, puis cliquez sur Ignorer la configuration pour terminer le processus d’importation ou sur Configurer pour configurer l’archive.

   >[!NOTE]
   >
   >Si vous cliquez sur Ignorer la configuration, vous pourrez configurer l’archive ultérieurement.

1. Si vous cliquez sur Configurer, vous pouvez apporter les modifications voulues dans la page de configuration des points de fin qui s’affiche :

   * Pour renommer un point de fin ou modifier sa description, cliquez dessus.
   * Pour ajouter un point de fin TaskManager, cliquez sur Ajouter un point de fin TaskManager. Pour plus d’informations sur les paramètres de Task Manager, voir [Paramètres des points de fin Task Manager](/help/forms/using/admin-help/configuring-task-manager-endpoints.md#configuring-task-manager-endpoints).
   * Pour ajouter un point de fin WatchedFolder, cliquez sur Ajouter un point de fin WatchedFolder. Pour plus d’informations sur les paramètres de Watched Folder, voir [Paramètres des points de fin Watched Folder](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#watched-folder-endpoint-settings).
   * Pour ajouter un point de fin courrier électronique, cliquez sur Ajouter une adresse électronique. Pour plus de précisions sur les paramètres de courrier électronique, voir [Paramètres des points de fin de courrier électronique](/help/forms/using/admin-help/configuring-email-endpoints.md#email-endpoint-settings).
   * Pour ajouter un point de fin EJB, cliquez sur Ajouter un point de fin EJB et spécifiez un nom et une description pour le point de fin.
   * Pour ajouter un point de fin SOAP, cliquez sur Ajouter un point de fin SOAP et spécifiez un nom et une description pour le point de fin.
   * Pour ajouter un point de fin Remoting, cliquez sur Ajouter un point de fin Remoting. Pour plus de précisions sur les paramètres de points de fin Remoting, voir [Paramètres des points de fin Remoting](/help/forms/using/admin-help/configuring-remoting-endpoints.md#remoting-endpoint-settings).
   * Pour ajouter un point de fin REST, cliquez sur Ajouter un point de fin REST et spécifiez un nom et une description pour ce dernier. Conservez l’URL d’invocation REST qui s’affiche sur la page Ajouter un point de fin REST.
   * Pour supprimer un point de fin, sélectionnez la case à cocher en regard du point de fin et cliquez sur Supprimer.

1. Cliquez sur Next (Suivant).
1. Si un processus ou un service de l’archive LCA possède des paramètres de configuration, une page de configuration des paramètres apparaît. Configurez les paramètres du service et cliquez sur Suivant.
1. Vous pouvez apporter toutes les modifications voulues dans la page de configuration du profil de sécurité :

   * **Demander aux appelants de s’authentifier :** ce paramètre indique si le service peut être appelé sans informations d’identification.

      Si le message *Les appelants sont actuellement tenus de s’authentifier* s’affiche, l’appelant du service doit être authentifié et l’entité de sécurité utilisateur de cet appelant doit être autorisée à appeler le service; si ce n’est pas le cas, la tentative d’appel est refusée. Pour supprimer l’obligation d’authentification, cliquez sur Autoriser des appelants non authentifiés.

      Si le message *Les appelants ne sont pas tenus de s’authentifier* s’affiche, l’appelant du service peut être ou ne pas être authentifié. L’appel du service réussit toujours puisqu’aucune vérification des autorisations n’est effectuée. Pour exiger une authentification, cliquez sur Demander aux appelants de s’authentifier.

   * **Exécuter en tant que :** indique l’identité d’exécution utilisée par un service après son appel. Pour modifier cette option, cliquez sur Changer. Faites votre choix parmi les options suivantes :

      **Non spécifié :** le comportement par défaut est utilisé.

      **Invocateur :** utilise l’identité de l’utilisateur qui a appelé le service.

      **Système :** exécute le service avec des droits illimités. Il s’agit du paramètre par défaut pour les processus de longue durée.

      **Utilisateur nommé :** vous permet d’exécuter le service en tant qu’utilisateur spécifique. Il s’agit du paramètre par défaut pour les processus de courte durée. Lors de la sélection de cette option, cliquez sur Sélectionner un utilisateur pour afficher la page Sélectionner une entité de sécurité, qui vous permet de rechercher et sélectionner l’utilisateur.

   * Pour ajouter une entité de sécurité au profil de sécurité, cliquez sur Ajouter une entité de sécurité et sélectionnez ensuite l’utilisateur ou le groupe à ajouter en tant qu’entité de sécurité. Cliquez sur Suivant et sélectionnez ensuite les autorisations à affecter à cette entité de sécurité :

      **INVOKE_PERM :** invocation de toutes les opérations sur le service.

      **MODIFY_CONFIG_PERM :** modification de la configuration d’un service.

      **SUPERVISOR_PERM :** affichage des données d’instance de processus d’un service créé à partir d’un processus.

      **START_STOP_PERM :** démarrage et arrêt d’un service.

      **ADD_REMOVE_ENDPOINTS_PERM :** ajout, suppression et modification des points de fin d’un service.

      **CREATE_VERSION_PERM :** création d’une nouvelle version du service.

      **DELETE_VERSION_PERM :** suppression d’une version du service.

      **MODIFY_VERSION_PERM :** modification d’une version du service.

      **READ_PERM :** affichage du service.

      Cliquez sur Terminé pour ajouter l’entité de sécurité au profil de sécurité.

1. Cliquez sur Terminé pour achever la configuration.

## Configuration des services AEM forms faisant partie d’un fichier d’archive  {#configure-the-aem-forms-that-are-part-of-an-archive-file}

1. Dans Administration Console, cliquez sur Services > Applications et services > Gestion des applications, puis sur l’onglet Archives.
1. Dans la page Gestion des archives, sélectionnez le fichier d’archives à configurer.
1. Dans la page Afficher l’archive, sélectionnez la ressource de l’archive mise en surbrillance.
1. Configurez le fichier d’archives de processus importé.

## Configuration des services AEM forms faisant partie d’un fichier d’archive à l’aide de l’assistant de configuration  {#use-the-configuration-wizard-to-configure-the-aem-forms-that-are-part-of-an-archive-file}

1. Dans Administration Console, cliquez sur Services > Applications et services > Gestion des applications, puis sur l’onglet Archives.
1. Cliquez sur Configurer en regard du fichier d’archives à configurer.
1. Vous pouvez apporter les modifications voulues dans la page de configuration des points de fin qui s’affiche :

   * Pour renommer un point de fin ou modifier sa description, cliquez dessus.
   * Pour ajouter un point de fin TaskManager, cliquez sur Ajouter un point de fin TaskManager. Pour plus d’informations sur les paramètres de Task Manager, voir [Paramètres des points de fin Task Manager](/help/forms/using/admin-help/configuring-task-manager-endpoints.md#configuring-task-manager-endpoints).
   * Pour ajouter un point de fin WatchedFolder, cliquez sur Ajouter un point de fin WatchedFolder. Pour plus d’informations sur les paramètres de Watched Folder, voir [Paramètres des points de fin Watched Folder](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#watched-folder-endpoint-settings).
   * Pour ajouter un point de fin courrier électronique, cliquez sur Ajouter une adresse électronique. Pour plus de précisions sur les paramètres de courrier électronique, voir [Paramètres des points de fin de courrier électronique](/help/forms/using/admin-help/configuring-email-endpoints.md#email-endpoint-settings).
   * Pour ajouter un point de fin EJB, cliquez sur Ajouter un point de fin EJB et spécifiez un nom et une description pour le point de fin.
   * Pour ajouter un point de fin SOAP, cliquez sur Ajouter un point de fin SOAP et spécifiez un nom et une description pour le point de fin.
   * Pour ajouter un point de fin Remoting, cliquez sur Ajouter un point de fin Remoting. Pour plus de précisions sur les paramètres de points de fin Remoting, voir [Paramètres des points de fin Remoting](/help/forms/using/admin-help/configuring-remoting-endpoints.md#remoting-endpoint-settings).
   * Pour ajouter un point de fin REST, cliquez sur Ajouter un point de fin REST et spécifiez un nom et une description pour ce dernier. Conservez l’URL d’invocation REST qui s’affiche sur la page Ajouter un point de fin REST.
   * Pour supprimer un point de fin, sélectionnez la case à cocher en regard du point de fin et cliquez sur Supprimer.

1. Cliquez sur Next (Suivant).
1. Si un processus ou un service de l’archive LCA possède des paramètres de configuration, une page de configuration des paramètres apparaît. Configurez les paramètres du service et cliquez sur Suivant.
1. Vous pouvez apporter toutes les modifications voulues dans la page de configuration du profil de sécurité :

   * **Demander aux appelants de s’authentifier :** ce paramètre indique si le service peut être appelé sans informations d’identification.

      Si le message *Les appelants sont actuellement tenus de s’authentifier* s’affiche, l’appelant du service doit être authentifié et l’entité de sécurité utilisateur de cet appelant doit être autorisée à appeler le service; si ce n’est pas le cas, la tentative d’appel est refusée. Pour supprimer l’obligation d’authentification, cliquez sur Autoriser des appelants non authentifiés.

      Si le message *Les appelants ne sont pas tenus de s’authentifier* s’affiche, l’appelant du service peut être ou non authentifié. L’appel du service réussit toujours puisqu’aucune vérification des autorisations n’est effectuée. Pour exiger une authentification, cliquez sur Demander aux appelants de s’authentifier.

   * **Exécuter en tant que :** indique l’identité d’exécution utilisée par un service après son appel. Pour modifier cette option, cliquez sur Changer. Faites votre choix parmi les options suivantes :

      **Non spécifié :** le comportement par défaut est utilisé.

      **Invocateur :** utilise l’identité de l’utilisateur qui a appelé le service.

      **Système :** exécute le service avec des droits illimités. Il s’agit du paramètre par défaut pour les processus de longue durée.

      **Utilisateur nommé :** vous permet d’exécuter le service en tant qu’utilisateur spécifique. Il s’agit du paramètre par défaut pour les processus de courte durée. Lors de la sélection de cette option, cliquez sur Sélectionner un utilisateur pour afficher la page Sélectionner une entité de sécurité, qui vous permet de rechercher et sélectionner l’utilisateur.

   * Pour ajouter une entité de sécurité au profil de sécurité, cliquez sur Ajouter une entité de sécurité et sélectionnez ensuite l’utilisateur ou le groupe à ajouter en tant qu’entité de sécurité. Cliquez sur Suivant et sélectionnez ensuite les autorisations à affecter à cette entité de sécurité :

      **INVOKE_PERM :** invocation de toutes les opérations sur le service.

      **MODIFY_CONFIG_PERM :** modification de la configuration d’un service.

      **SUPERVISOR_PERM :** affichage des données d’instance de processus d’un service créé à partir d’un processus.

      **START_STOP_PERM :** démarrage et arrêt d’un service.

      **ADD_REMOVE_ENDPOINTS_PERM :** ajout, suppression et modification des points de fin d’un service.

      **CREATE_VERSION_PERM :** création d’une nouvelle version du service.

      **DELETE_VERSION_PERM :** suppression d’une version du service.

      **MODIFY_VERSION_PERM :** modification d’une version du service.

      **READ_PERM :** affichage du service.

      Cliquez sur Terminé pour ajouter l’entité de sécurité au profil de sécurité.

## Suppression d’une archive  {#remove-an-archive}

>[!NOTE]
>
>pour supprimer une archive contenant des actifs stockés dans un référentiel tiers (EMC Documentum Content Server, IBM FileNet Content Manager ou IBM Content Manager), vous devez également supprimer les fichiers d’actifs du référentiel à l’aide de Workbench.

1. Dans Administration Console, cliquez sur Services > Applications et services > Gestion des archives.
1. Dans la page Gestion des archives, cochez la case correspondant à l’archive à supprimer, puis cliquez sur Supprimer.

