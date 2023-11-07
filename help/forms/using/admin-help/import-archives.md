---
title: Importer et gérer des archives
description: Découvrez comment importer et gérer des archives. Archives importe et gère les fichiers LCA créés dans Workbench. Vous pouvez importer, configurer, utiliser et supprimer une archive.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/importing_and_managing_applications_and_archives
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 0c15677a-ee17-425e-a261-fb3ae8688eb2
source-git-commit: fc2f26a69c208947c14e8c6036825bb217901481
workflow-type: tm+mt
source-wordcount: '1470'
ht-degree: 24%

---

# Importer et gérer des archives {#import-and-manage-archives}

Utilisez l’onglet Archives pour importer et gérer les fichiers LCA créés dans Workbench.

## Importation d’une archive {#import-an-archive}

1. Dans Administration Console, cliquez sur Services > Applications et services > Gestion des applications, puis cliquez sur l’onglet Archives.
1. Cliquez sur Importer.
1. Cliquez sur Parcourir pour localiser l’archive à importer, puis sur Aperçu.
1. Consultez la liste des ressources et des objets qui seront installés avec l’archive. Assurez-vous qu’il n’existe aucun conflit avec les ressources, objets et configurations de service existants, car aucune fonctionnalité d’annulation n’est disponible.

   Si vous choisissez d’importer les configurations de service, AEM forms importe tous les fichiers de configuration de processus (points de terminaison, profils de sécurité et paramètres de configuration de service) utilisés par les processus dans l’archive LCA.

1. Cliquez sur Importer.
1. Vérifiez les résultats de l’importation, puis cliquez sur Ignorer la configuration pour terminer le processus d’importation ou sur Configurer pour configurer l’archive.

   >[!NOTE]
   >
   >Si vous cliquez sur Ignorer la configuration, vous pouvez configurer l’archive ultérieurement.

1. Si vous cliquez sur Configurer, la page Configurer les points de fin s’affiche. Vous pouvez y apporter les modifications nécessaires :

   * Pour renommer un point de fin ou modifier sa description, cliquez dessus.
   * Pour ajouter un point de fin TaskManager, cliquez sur Ajouter un point de fin TaskManager. Pour plus d’informations sur les paramètres de Task Manager, voir [Configuration des points de fin TaskManager](/help/forms/using/admin-help/configuring-task-manager-endpoints.md#configuring-task-manager-endpoints).
   * Pour ajouter un point de fin Watched Folder, cliquez sur Ajouter un point de fin Watched Folder. Pour plus d’informations sur les paramètres du dossier de contrôle, voir [Paramètres des points de fin Watched Folder](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#watched-folder-endpoint-settings).
   * Pour ajouter un point de fin Email, cliquez sur Ajouter un message électronique. Pour plus d’informations sur les paramètres de courrier électronique, voir [Paramètres des points de fin de courrier électronique](/help/forms/using/admin-help/configuring-email-endpoints.md#email-endpoint-settings).
   * Pour ajouter un point de fin EJB, cliquez sur Ajouter un point de fin EJB et indiquez un nom et une description pour le point de fin.
   * Pour ajouter un point de fin SOAP, cliquez sur Ajouter un point de fin SOAP et indiquez un nom et une description pour le point de fin.
   * Pour ajouter un point de fin Remoting, cliquez sur Ajouter un point de fin Remoting. Pour plus d’informations sur les paramètres d’installation à distance, voir [Paramètres des points de fin Remoting](/help/forms/using/admin-help/configuring-remoting-endpoints.md#remoting-endpoint-settings).
   * Pour ajouter un point de fin REST, cliquez sur Ajouter un point de fin REST et indiquez un nom et une description pour le point de fin. Notez l’URL d’appel REST affichée sur la page Ajouter un point de fin REST .
   * Pour supprimer un point de fin, cochez la case en regard de celui-ci et cliquez sur Supprimer.

1. Cliquez sur Suivant.
1. Si un processus ou un service de l’archive LCA comporte des paramètres de configuration, une page Configurer les paramètres s’affiche, dans laquelle vous configurez les paramètres de service et cliquez sur Suivant.
1. Sur la page Configurer le profil de sécurité , apportez les modifications nécessaires :

   * **Exiger que les appelants s’authentifient :** Ce paramètre indique si le service peut être appelé avec ou sans informations d’identification.

     Si le message *Les appelants sont actuellement tenus de s’authentifier* s’affiche, l’appelant du service doit être authentifié et le principal de cet appelant doit être autorisé à appeler le service ; si ce n’est pas le cas, la tentative d’appel est refusée. Pour supprimer la nécessité de s’authentifier, cliquez sur Autoriser les appelants non authentifiés.

     If *Les appelants ne sont pas tenus de s’authentifier* s’affiche, l’appelant du service ne doit pas être authentifié. L’appel du service réussit toujours car il n’y a pas de vérification d’autorisation. Pour exiger une authentification, cliquez sur Demander aux appelants de s’authentifier.

   * **Exécutez comme :** Indique l’identité d’exécution utilisée par un service après son appel. Pour modifier cette option, cliquez sur Modifier. Faites votre choix parmi les options suivantes :

     **Non spécifié :** le comportement par défaut est utilisé.

     **Invocateur :** utilise l’identité de l’utilisateur qui a appelé le service.

     **Système :** exécute le service avec des droits illimités. Il s’agit du paramètre par défaut pour les processus de longue durée.

     **Utilisateur nommé :** vous permet d’exécuter le service en tant qu’utilisateur spécifique. Il s’agit du paramètre par défaut pour les processus de courte durée. Lorsque vous sélectionnez cette option, cliquez sur Sélectionner un utilisateur pour afficher la page Sélectionner une entité de sécurité, dans laquelle vous pouvez rechercher et sélectionner l’utilisateur.

   * Pour ajouter une entité de sécurité au profil de sécurité, cliquez sur Ajouter une entité de sécurité et sélectionnez l’utilisateur ou le groupe à ajouter comme entité de sécurité. Cliquez sur Suivant , puis sélectionnez les autorisations à attribuer à cette entité :

     **INVOKE_PERM :** invocation de toutes les opérations sur le service.

     **MODIFY_CONFIG_PERM :** modification de la configuration d’un service.

     **SUPERVISOR_PERM :** affichage des données d’instance de processus d’un service créé à partir d’un processus.

     **START_STOP_PERM :** démarrage et arrêt d’un service.

     **ADD_REMOVE_ENDPOINTS_PERM :** ajout, suppression et modification des points d’entrée d’un service.

     **CREATE_VERSION_PERM :** Pour créer une version du service

     **DELETE_VERSION_PERM :** suppression d’une version du service.

     **MODIFY_VERSION_PERM :** modification d’une version du service.

     **READ_PERM :** affichage du service.

     Cliquez sur Terminé pour ajouter l&#39;entité de sécurité au profil de sécurité.

1. Cliquez sur Terminé pour terminer la configuration.

## Configuration des AEM forms faisant partie d’un fichier d’archive {#configure-the-aem-forms-that-are-part-of-an-archive-file}

1. Dans Administration Console, cliquez sur Services > Applications et services > Gestion des applications, puis cliquez sur l’onglet Archives.
1. Sur la page Gestion des archives, sélectionnez le fichier d’archive à configurer.
1. Sur la page Afficher l’archive , sélectionnez la ressource d’archive mise en surbrillance.
1. Configurez le fichier d’archive de processus importé.

## Utilisation de l’assistant de configuration pour configurer les formulaires AEM qui font partie d’un fichier d’archive {#use-the-configuration-wizard-to-configure-the-aem-forms-that-are-part-of-an-archive-file}

1. Dans Administration Console, cliquez sur Services > Applications et services > Gestion des applications, puis cliquez sur l’onglet Archives.
1. Cliquez sur Configurer en regard du fichier d’archive à configurer.
1. La page Configurer les points de fin s’affiche, dans laquelle vous pouvez apporter les modifications nécessaires :

   * Pour renommer un point de fin ou modifier sa description, cliquez dessus.
   * Pour ajouter un point de fin TaskManager, cliquez sur Ajouter un point de fin TaskManager. Pour plus d’informations sur les paramètres de Task Manager, voir [Configuration des points de fin TaskManager](/help/forms/using/admin-help/configuring-task-manager-endpoints.md#configuring-task-manager-endpoints).
   * Pour ajouter un point de fin Watched Folder, cliquez sur Ajouter un point de fin Watched Folder. Pour plus d’informations sur les paramètres du dossier de contrôle, voir [Paramètres des points de fin Watched Folder](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#watched-folder-endpoint-settings).
   * Pour ajouter un point de fin Email, cliquez sur Ajouter un message électronique. Pour plus d’informations sur les paramètres de courrier électronique, voir [Paramètres des points de fin de courrier électronique](/help/forms/using/admin-help/configuring-email-endpoints.md#email-endpoint-settings).
   * Pour ajouter un point de fin EJB, cliquez sur Ajouter un point de fin EJB et indiquez un nom et une description pour le point de fin.
   * Pour ajouter un point de fin SOAP, cliquez sur Ajouter un point de fin SOAP et indiquez un nom et une description pour le point de fin.
   * Pour ajouter un point de fin Remoting, cliquez sur Ajouter un point de fin Remoting. Pour plus d’informations sur les paramètres d’installation à distance, voir [Paramètres des points de fin Remoting](/help/forms/using/admin-help/configuring-remoting-endpoints.md#remoting-endpoint-settings).
   * Pour ajouter un point de fin REST, cliquez sur Ajouter un point de fin REST et indiquez un nom et une description pour le point de fin. Notez l’URL d’appel REST affichée sur la page Ajouter un point de fin REST .
   * Pour supprimer un point de fin, cochez la case en regard de celui-ci et cliquez sur Supprimer.

1. Cliquez sur Suivant.
1. Si un processus ou un service de l’archive LCA comporte des paramètres de configuration, une page Configurer les paramètres s’affiche, dans laquelle vous configurez les paramètres de service et cliquez sur Suivant.
1. Sur la page Configurer le profil de sécurité , vous pouvez apporter les modifications nécessaires :

   * **Exiger que les appelants s’authentifient :** Ce paramètre indique si le service peut être appelé avec ou sans informations d’identification.

     Si le message *Les appelants sont actuellement tenus de s’authentifier* s’affiche, l’appelant du service doit être authentifié et le principal de cet appelant doit être autorisé à appeler le service ; si ce n’est pas le cas, la tentative d’appel est refusée. Pour supprimer la nécessité de s’authentifier, cliquez sur Autoriser les appelants non authentifiés.

     If *Les appelants ne sont pas tenus de s’authentifier* s’affiche, l’appelant du service peut être authentifié ou non. L’appel du service réussit toujours car il n’y a pas de vérification d’autorisation. Pour exiger une authentification, cliquez sur Demander aux appelants de s’authentifier.

   * **Exécutez comme :** Indique l’identité d’exécution utilisée par un service après son appel. Pour modifier cette option, cliquez sur Modifier. Faites votre choix parmi les options suivantes :

     **Non spécifié :** le comportement par défaut est utilisé.

     **Invocateur :** utilise l’identité de l’utilisateur qui a appelé le service.

     **Système :** exécute le service avec des droits illimités. Il s’agit du paramètre par défaut pour les processus de longue durée.

     **Utilisateur nommé :** vous permet d’exécuter le service en tant qu’utilisateur spécifique. Il s’agit du paramètre par défaut pour les processus de courte durée. Lorsque vous sélectionnez cette option, cliquez sur Sélectionner un utilisateur pour afficher la page Sélectionner une entité de sécurité, dans laquelle vous pouvez rechercher et sélectionner l’utilisateur.

   * Pour ajouter une entité de sécurité au profil de sécurité, cliquez sur Ajouter une entité de sécurité et sélectionnez l’utilisateur ou le groupe à ajouter comme entité de sécurité. Cliquez sur Suivant , puis sélectionnez les autorisations à attribuer à cette entité :

     **INVOKE_PERM :** invocation de toutes les opérations sur le service.

     **MODIFY_CONFIG_PERM :** modification de la configuration d’un service.

     **SUPERVISOR_PERM :** affichage des données d’instance de processus d’un service créé à partir d’un processus.

     **START_STOP_PERM :** démarrage et arrêt d’un service.

     **ADD_REMOVE_ENDPOINTS_PERM :** ajout, suppression et modification des points d’entrée d’un service.

     **CREATE_VERSION_PERM :** Pour créer une version du service

     **DELETE_VERSION_PERM :** suppression d’une version du service.

     **MODIFY_VERSION_PERM :** modification d’une version du service.

     **READ_PERM :** affichage du service.

     Cliquez sur Terminé pour ajouter l&#39;entité de sécurité au profil de sécurité.

## Suppression d’une archive {#remove-an-archive}

>[!NOTE]
>
>Pour supprimer une archive contenant des ressources stockées dans un référentiel tiers (EMC Documentum Content Server, IBM FileNet Content Manager ou IBM Content Manager), vous devez également supprimer les fichiers de ressources du référentiel à l’aide de Workbench.

1. Dans Administration Console, cliquez sur Services > Applications et services > Gestion des archives.
1. Sur la page Gestion des archives, cochez la case correspondant à l’archive à supprimer, puis cliquez sur Supprimer.
