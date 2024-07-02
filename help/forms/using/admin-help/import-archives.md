---
title: Importation et gestion des archives
description: Découvrez comment importer et gérer des archives. L’option Archives permet d’importer et de gérer les fichiers LCA créés dans Workbench. Vous pouvez importer, configurer, utiliser et supprimer une archive.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/importing_and_managing_applications_and_archives
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 0c15677a-ee17-425e-a261-fb3ae8688eb2
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: ht
source-wordcount: '1438'
ht-degree: 100%

---

# Importer et gérer des archives {#import-and-manage-archives}

Importez et gérez les fichiers LCA créés avec Workbench via l’onglet Archives.

## Import d’une archive {#import-an-archive}

1. Dans la console d’administration, cliquez sur Services > Applications et services > Gestion des applications, puis cliquez sur l’onglet Archives.
1. Cliquez sur Importer.
1. Cliquez sur Parcourir pour localiser l’archive à importer puis sur Aperçu.
1. Passez en revue la liste des ressources et des objets qui seront installés avec l’archive. Assurez-vous de l’absence de conflits avec des ressources, objets ou configurations de services existants, car il n’existe pas de fonctionnalité d’annulation.

   Si vous choisissez d’importer les configurations de services, AEM Forms importe tous les fichiers de configuration de processus (points d’entrée, profils de sécurité et paramètres de configuration des services) utilisés par les processus dans l’archive LCA.

1. Cliquez sur Importer.
1. Vérifiez les résultats de l’import, puis cliquez sur Ignorer la configuration pour terminer le processus d’import ou sur Configurer pour configurer l’archive.

   >[!NOTE]
   >
   >Si vous cliquez sur Ignorer la configuration, vous pouvez configurer l’archive ultérieurement.

1. Si vous cliquez sur Configurer, vous pouvez apporter les modifications voulues dans la page de configuration des points d’entrée qui s’affiche :

   * Pour renommer un point d’entrée ou modifier sa description, cliquez dessus.
   * Pour ajouter un point d’entrée TaskManager, cliquez sur Ajouter un point d’entrée TaskManager. Pour plus d’informations sur les paramètres de TaskManager, voir [Configuration des points d’entrée TaskManager](/help/forms/using/admin-help/configuring-task-manager-endpoints.md#configuring-task-manager-endpoints).
   * Pour ajouter un point d’entrée WatchedFolder, cliquez sur Ajouter un point d’entrée WatchedFolder. Pour plus d’informations sur les paramètres de Watched Folder , voir [Paramètres des points d’entrée de Watched Folder](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#watched-folder-endpoint-settings).
   * Pour ajouter un point d’entrée d’e-mail, cliquez sur Ajouter un point d’entrée d’e-mail. Pour plus d’informations sur les paramètres d’e-mail, voir [Paramètres des points d’entrée d’e-mail](/help/forms/using/admin-help/configuring-email-endpoints.md#email-endpoint-settings).
   * Pour ajouter un point d’entrée EJB, cliquez sur Ajouter un point d’entrée EJB et indiquez un nom et une description pour le point d’entrée.
   * Pour ajouter un point d’entrée SOAP, cliquez sur Ajouter un point d’entrée SOAP et indiquez un nom et une description pour le point d’entrée.
   * Pour ajouter un point d’entrée Remoting, cliquez sur Ajouter un point d’entrée Remoting. Pour plus de précisions sur les paramètres de points d’entrée Remoting, voir [Paramètres des points d’entrée Remoting](/help/forms/using/admin-help/configuring-remoting-endpoints.md#remoting-endpoint-settings).
   * Pour ajouter un point d’entrée REST, cliquez sur Ajouter un point d’entrée REST et indiquez un nom et une description pour le point d’entrée. Notez l’URL d’appel REST affichée sur la page Ajouter un point d’entrée REST.
   * Pour supprimer un point d’entrée, cochez la case en regard de celui-ci et cliquez sur Supprimer.

1. Cliquez sur Suivant.
1. Si un processus ou un service de l’archive LCA possède des paramètres de configuration, une page de configuration des paramètres apparaît. Configurez les paramètres du service et cliquez sur Suivant.
1. Vous pouvez apporter toutes les modifications voulues dans la page de configuration du profil de sécurité :

   * **Demander aux personnes appelantes de s’authentifier :** ce paramètre indique si le service peut être appelé avec ou sans informations d’identification.

     Si le message *Les appelants sont actuellement tenus de s’authentifier* s’affiche, l’appelant du service doit être authentifié et le principal de cet appelant doit être autorisé à appeler le service ; si ce n’est pas le cas, la tentative d’appel est refusée. Pour supprimer l’obligation d’authentification, cliquez sur Autoriser des personnes appelantes non authentifiées.

     Si le message *Les personnes appelantes ne sont pas tenues de s’authentifier* s’affiche, la personne appelante du service n’a pas besoin d’être authentifiée. L’appel du service réussit toujours puisqu’aucune vérification des autorisations n’est effectuée. Pour exiger une authentification, cliquez sur Demander aux personnes appelantes de s’authentifier.

   * **Exécuter comme :** indique l’identité d’exécution utilisée par un service après son appel. Pour modifier cette option, cliquez sur Modifier. Faites votre choix parmi les options suivantes :

     **Non spécifié :** le comportement par défaut est utilisé.

     **Invocateur :** utilise l’identité de l’utilisateur qui a appelé le service.

     **Système :** exécute le service avec des droits illimités. Il s’agit du paramètre par défaut pour les processus de longue durée.

     **Utilisateur nommé :** vous permet d’exécuter le service en tant qu’utilisateur spécifique. Il s’agit du paramètre par défaut pour les processus de courte durée. Lors de la sélection de cette option, cliquez sur Sélectionner un utilisateur pour afficher la page Sélectionner une entité de sécurité, qui vous permet de rechercher et de sélectionner une personne.

   * Pour ajouter un principal au profil de sécurité, cliquez sur Ajouter un principal et sélectionnez l’utilisateur ou l’utilisatrice, ou le groupe à ajouter comme principal. Cliquez sur Suivant , puis sélectionnez les autorisations à attribuer à ce principal :

     **INVOKE_PERM :** invocation de toutes les opérations sur le service.

     **MODIFY_CONFIG_PERM :** modification de la configuration d’un service.

     **SUPERVISOR_PERM :** affichage des données d’instance de processus d’un service créé à partir d’un processus.

     **START_STOP_PERM :** démarrage et arrêt d’un service.

     **ADD_REMOVE_ENDPOINTS_PERM :** ajout, suppression et modification des points d’entrée d’un service.

     **CREATE_VERSION_PERM :** création d’une version du service.

     **DELETE_VERSION_PERM :** suppression d’une version du service.

     **MODIFY_VERSION_PERM :** modification d’une version du service.

     **READ_PERM :** affichage du service.

     Cliquez sur Terminé pour ajouter le principal au profil de sécurité.

1. Cliquez sur Terminé pour terminer la configuration.

## Configuration des services AEM forms faisant partie d’un fichier d’archive {#configure-the-aem-forms-that-are-part-of-an-archive-file}

1. Dans la console d’administration, cliquez sur Services > Applications et services > Gestion des applications, puis cliquez sur l’onglet Archives.
1. Sur la page Gestion des archives, sélectionnez le fichier d’archive à configurer.
1. Sur la page Afficher l’archive, sélectionnez la ressource d’archive mise en surbrillance.
1. Configurez le fichier d’archive de processus importé.

## Configuration des services AEM forms faisant partie d’un fichier d’archive à l’aide de l’assistant de configuration {#use-the-configuration-wizard-to-configure-the-aem-forms-that-are-part-of-an-archive-file}

1. Dans la console d’administration, cliquez sur Services > Applications et services > Gestion des applications, puis cliquez sur l’onglet Archives.
1. Cliquez sur Configurer en regard du fichier d’archive à configurer.
1. La page Configurer les points d’entrée s’affiche, dans laquelle vous pouvez apporter les modifications nécessaires :

   * Pour renommer un point d’entrée ou modifier sa description, cliquez dessus.
   * Pour ajouter un point d’entrée TaskManager, cliquez sur Ajouter un point d’entrée TaskManager. Pour plus d’informations sur les paramètres de TaskManager, voir [Configuration des points d’entrée TaskManager](/help/forms/using/admin-help/configuring-task-manager-endpoints.md#configuring-task-manager-endpoints).
   * Pour ajouter un point d’entrée WatchedFolder, cliquez sur Ajouter un point d’entrée WatchedFolder. Pour plus d’informations sur les paramètres de Watched Folder , voir [Paramètres des points d’entrée de Watched Folder](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#watched-folder-endpoint-settings).
   * Pour ajouter un point d’entrée d’e-mail, cliquez sur Ajouter un point d’entrée d’e-mail. Pour plus d’informations sur les paramètres d’e-mail, voir [Paramètres des points d’entrée d’e-mail](/help/forms/using/admin-help/configuring-email-endpoints.md#email-endpoint-settings).
   * Pour ajouter un point d’entrée EJB, cliquez sur Ajouter un point d’entrée EJB et indiquez un nom et une description pour le point d’entrée.
   * Pour ajouter un point d’entrée SOAP, cliquez sur Ajouter un point d’entrée SOAP et indiquez un nom et une description pour le point d’entrée.
   * Pour ajouter un point d’entrée Remoting, cliquez sur Ajouter un point d’entrée Remoting. Pour plus de précisions sur les paramètres de points d’entrée Remoting, voir [Paramètres des points d’entrée Remoting](/help/forms/using/admin-help/configuring-remoting-endpoints.md#remoting-endpoint-settings).
   * Pour ajouter un point d’entrée REST, cliquez sur Ajouter un point d’entrée REST et indiquez un nom et une description pour le point d’entrée. Notez l’URL d’appel REST affichée sur la page Ajouter un point d’entrée REST.
   * Pour supprimer un point d’entrée, cochez la case en regard de celui-ci et cliquez sur Supprimer.

1. Cliquez sur Suivant.
1. Si un processus ou un service de l’archive LCA possède des paramètres de configuration, une page de configuration des paramètres apparaît. Configurez les paramètres du service et cliquez sur Suivant.
1. Sur la page Configurer le profil de sécurité, vous pouvez apporter les modifications nécessaires :

   * **Demander aux personnes appelantes de s’authentifier :** ce paramètre indique si le service peut être appelé avec ou sans informations d’identification.

     Si le message *Les appelants sont actuellement tenus de s’authentifier* s’affiche, l’appelant du service doit être authentifié et le principal de cet appelant doit être autorisé à appeler le service ; si ce n’est pas le cas, la tentative d’appel est refusée. Pour supprimer l’obligation d’authentification, cliquez sur Autoriser des personnes appelantes non authentifiées.

     Si la mention *Les personnes appelantes ne sont pas tenus de s’authentifier* s’affiche, la personne appelante du service peut être authentifiée ou non. L’appel du service réussit toujours puisqu’aucune vérification des autorisations n’est effectuée. Pour exiger une authentification, cliquez sur Demander aux personnes appelantes de s’authentifier.

   * **Exécuter comme :** indique l’identité d’exécution utilisée par un service après son appel. Pour modifier cette option, cliquez sur Modifier. Faites votre choix parmi les options suivantes :

     **Non spécifié :** le comportement par défaut est utilisé.

     **Invocateur :** utilise l’identité de l’utilisateur qui a appelé le service.

     **Système :** exécute le service avec des droits illimités. Il s’agit du paramètre par défaut pour les processus de longue durée.

     **Utilisateur nommé :** vous permet d’exécuter le service en tant qu’utilisateur spécifique. Il s’agit du paramètre par défaut pour les processus de courte durée. Lors de la sélection de cette option, cliquez sur Sélectionner un utilisateur pour afficher la page Sélectionner une entité de sécurité, qui vous permet de rechercher et de sélectionner une personne.

   * Pour ajouter un principal au profil de sécurité, cliquez sur Ajouter un principal et sélectionnez l’utilisateur ou l’utilisatrice, ou le groupe à ajouter comme principal. Cliquez sur Suivant , puis sélectionnez les autorisations à attribuer à ce principal :

     **INVOKE_PERM :** invocation de toutes les opérations sur le service.

     **MODIFY_CONFIG_PERM :** modification de la configuration d’un service.

     **SUPERVISOR_PERM :** affichage des données d’instance de processus d’un service créé à partir d’un processus.

     **START_STOP_PERM :** démarrage et arrêt d’un service.

     **ADD_REMOVE_ENDPOINTS_PERM :** ajout, suppression et modification des points d’entrée d’un service.

     **CREATE_VERSION_PERM :** création d’une version du service.

     **DELETE_VERSION_PERM :** suppression d’une version du service.

     **MODIFY_VERSION_PERM :** modification d’une version du service.

     **READ_PERM :** affichage du service.

     Cliquez sur Terminé pour ajouter le principal au profil de sécurité.

## Suppression d’une archive {#remove-an-archive}

>[!NOTE]
>
>Pour supprimer une archive contenant des ressources stockées dans un référentiel tiers (EMC Documentum Content Server, IBM FileNet Content Manager ou IBM Content Manager), vous devez également supprimer les fichiers de ressources du référentiel à l’aide de Workbench.

1. Dans la console d’administration, cliquez sur Services > Applications et services > Gestion des archives.
1. Sur la page Gestion des archives, cochez la case correspondant à l’archive à supprimer, puis cliquez sur Supprimer.
