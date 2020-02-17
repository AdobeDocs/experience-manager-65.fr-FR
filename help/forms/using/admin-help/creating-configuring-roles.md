---
title: Création et configuration des rôles
seo-title: Création et configuration des rôles
description: Découvrez comment associer des utilisateurs et des groupes à des rôles faisant partie de la base de données User Management. Vous pouvez également créer, modifier et supprimer des rôles.
seo-description: Découvrez comment associer des utilisateurs et des groupes à des rôles faisant partie de la base de données User Management. Vous pouvez également créer, modifier et supprimer des rôles.
uuid: e8e4331d-48e1-4fa9-8f44-f885f4ab1a54
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_organizing_users
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 737fb4d1-adef-47e1-9a0d-8cddd13132cb
translation-type: tm+mt
source-git-commit: 413af4ef9bc3652e05da78d622183bcf20a8bee7

---


# Création et configuration des rôles{#creating-and-configuring-roles}

Les pages Web de User Management vous permettent d’associer des utilisateurs et des groupes à des rôles faisant partie de la base de données User Management. Vous pouvez également créer, modifier et supprimer des rôles.

User Management comporte deux types de rôles :

**** Rôles mutables : Ce type de rôle peut être modifié et supprimé, et les autorisations de rôle peuvent être ajoutées et supprimées de ces types de rôle. Les rôles que vous créez sont des rôles mutables. Vous pouvez ajouter et supprimer des utilisateurs et groupes affectés à des rôles mutables.

**** Rôles immuables : Les rôles par défaut inclus dans User Management sont des rôles immuables. Ils ne peuvent être ni modifiés ni supprimés. Toutefois, vous pouvez ajouter ou supprimer des utilisateurs et des groupes affectés à des rôles non modifiables.

Les API d&#39;AEM forms permettent également de créer des rôles modifiables et non modifiables.

## Rôles par défaut {#default-roles}

Les rôles par défaut suivants sont inclus dans la base de données Gestion des utilisateurs.

**** Utilisateur d&#39;Administration Console : peut accéder à Administration Console.

**** Administrateur d’applications : Peut utiliser toutes les fonctionnalités de Workbench. Peut utiliser les pages Applications et services de Administration Console pour configurer des propriétés d’exécution de services, des points de fin et la sécurité.

**** Administrateur AEM Forms : peut effectuer toutes les tâches pour tous les services installés.

**** Administrateur de sécurité : Contrôle les paramètres de User Management et gère les utilisateurs et les groupes associés à tout domaine User Manager.

**** Utilisateur des services : Peut afficher et appeler n’importe quel service

**** Super administrateur : A accès à toutes les fonctionnalités administratives du système, y compris les services

**** Administrateur Trust : peut gérer les paramètres d’approbation PKI et les informations d’identification PKI qui sont gérés à partir de la page Trust Store Management dans Administration Console.

### Rôles par défaut supplémentaires {#additional-default-roles}

Les rôles par défaut supplémentaires suivants peuvent également être inclus, selon les composants d’AEM Forms installés.

**** Utilisateur de l’application de téléchargement de document : Peut télécharger des documents à l’aide de Flex Remoting.

**** Administrateur Forms : peut afficher et modifier des paramètres de la page Forms dans Administration Console.

**** Administrateur AEM forms Contentspace : peut afficher et modifier des paramètres de la page Content Services (obsolète) dans Administration Console.

**** Utilisateur d’AEM forms Contentspace : Peut se connecter aux pages Web Contentspace (obsolète)

**** Documentum Connector Administrator : peut afficher et modifier des paramètres de la page Connector for EMC Documentum dans Administration Console.

**** Administrateur AEM forms FileNet Connector : peut afficher et modifier des paramètres de la page Connector for IBM FileNet dans Administration Console.

**** Administrateur AEM forms IBM CM Connector : peut afficher et modifier des paramètres de la page Connector for IBM Content Manager dans Administration Console.

**** Administrateur Rights Management : exécute toutes les tâches requises pour toutes les configurations de serveur sur les pages Rights Management appropriées.

**** Utilisateur final de Rights Management : peut accéder aux pages Web d’utilisateur final de Rights Management.

**** Utilisateur invité Rights Management : Peut inviter des utilisateurs

**** Rights Management Gérer les utilisateurs invités et locaux : peut effectuer les tâches requises pour gérer tous les utilisateurs invités et locaux sur les pages Rights Management appropriées.

**** Administrateur du jeu de stratégies Rights Management : exécute toutes les tâches requises pour tous les jeux de stratégies sur les pages Rights Management appropriées.

**** Super administrateur Rights Management : exécute toutes les tâches requises à partir de la page Rights Management.

**** Administrateur AEM forms Workspace : peut afficher et modifier des paramètres de la page Workspace dans Administration Console.

***Remarque ** : Flex Workspace est obsolète pour la version d’AEM Forms.*

**** Utilisateur de Workspace : Peut se connecter à l’application Workspace destinée aux utilisateurs finaux

**** Administrateur Output : peut afficher et modifier des paramètres de la page Output dans Administration Console.

**** Administrateur PDFG : peut afficher et modifier des paramètres de la page PDF Generator dans Administration Console.

**** Utilisateur PDFG : Peut accéder à toutes les fonctionnalités non administratives de PDF Generator

**** Application Web des extensions d&#39;Acrobat Reader DC : Peut utiliser l’application Web des extensions d’Acrobat Reader DC

>[!NOTE]
>
>pour des raisons de sécurité, les utilisateurs disposant de certains types de privilèges d’administrateur n’ont pas accès aux pages Web des utilisateurs finaux de Workspace. Comme ces pages peuvent se trouver en dehors d’un pare-feu, autoriser des tâches d’administration pourrait présenter un risque de sécurité. Seuls les utilisateurs disposant du privilège d’administrateur ou d’utilisateur d’AEM Forms Workspace peuvent accéder aux pages Web des utilisateurs finaux de Workspace.

>[!NOTE]
>
>Flex Workspace est obsolète pour la version d’AEM Forms.

## Création d’un rôle {#create-a-role}

1. Dans Administration Console, cliquez sur Paramètres > Gestion des utilisateurs > Gestion des rôles, puis sur Nouveau rôle.
1. Dans la zone Nom du rôle, saisissez le nom du rôle, indiquez-en éventuellement une description, puis cliquez sur Suivant.

   >[!NOTE]
   >
   >si vous utilisez MySQL, vous ne pouvez pas créer deux rôles portant le même nom, même s’ils diffèrent par l’utilisation de caractères étendus. Par exemple, si vous essayez de créer un rôle nommé abcde alors qu’un autre nommé âbcdè existe déjà, une erreur se produit.

1. Cliquez sur Rechercher des droits et sélectionnez les droits à ajouter au rôle.
1. Cliquez sur OK puis sur Suivant.
1. Affectez ce rôle à des utilisateurs et à des groupes :

   * Cliquez sur Rechercher des utilisateurs/groupes.
   * Dans la zone Rechercher, saisissez vos critères de recherche.
   * Sélectionnez Nom, Adresse électronique ou ID utilisateur, puis Utilisateurs, Groupes ou Utilisateurs et groupes.
   * Sélectionnez le domaine, le nombre de résultats à afficher, puis cliquez sur Rechercher.
   * Cochez les cases correspondant aux utilisateurs et aux groupes auxquels affecter ce rôle, puis cliquez sur OK.

1. Pour afficher les détails relatifs aux utilisateurs et aux groupes, sélectionnez l’entité.
1. Cliquez sur OK, puis sur Terminer.

## Modification d’un rôle {#edit-a-role}

1. Dans Administration Console, cliquez sur Paramètres > Gestion des utilisateurs > Gestion des rôles, puis sur Nom du rôle.

   Par défaut, tous les rôles trouvés dans la base de données User Management s’affichent dans la page Gestion des rôles. Si la liste est trop importante, utilisez la zone Rechercher située en haut de la page pour rechercher un nom de rôle particulier.

1. Cliquez sur le rôle à modifier, modifiez les paramètres généraux, puis cliquez sur Enregistrer.
1. Pour modifier les droits du rôle, cliquez sur l’onglet Droits et procédez comme suit :

   * Pour ajouter de nouveaux droits, cliquez sur Rechercher des droits, activez les cases à cocher correspondant aux droits à ajouter, cliquez sur OK, puis sur Enregistrer.
   * Pour supprimer un droit d’un rôle, activez la case à cocher correspondant au droit, cliquez sur Supprimer, puis sur Enregistrer.

1. Pour gérer l’affectation d’un rôle, cliquez sur l’onglet Utilisateurs de rôle et procédez comme suit :

   * Pour affecter le rôle à de nouveaux utilisateurs et à de nouveaux groupes, cliquez sur Rechercher des utilisateurs/groupes et saisissez les informations de recherche. Activez la case à cocher correspondant aux utilisateurs et aux groupes auxquels affecter ce rôle, cliquez sur OK, puis sur Enregistrer.
   * Pour supprimer le rôle, activez la case à cocher correspondant aux utilisateurs ou aux groupes, cliquez sur Retirer, puis sur Enregistrer.

## Suppression d’un rôle {#delete-a-role}

Vous pouvez supprimer tous les rôles créés, mais pas les rôles AEM Forms par défaut intégrés au produit.

1. Dans Administration Console, cliquez sur Paramètres > Gestion des utilisateurs > Gestion des rôles, puis sur Nom du rôle.

   Par défaut, tous les rôles trouvés dans la base de données User Management s’affichent dans la page Gestion des rôles. Si la liste est trop importante, utilisez la zone Rechercher située en haut de la page pour rechercher un nom de rôle particulier.

1. Cochez la case correspondant au rôle à supprimer, cliquez sur Supprimer, puis sur OK.

## Affectation d’un rôle aux utilisateurs et aux groupes {#assign-a-role-to-users-and-groups}

1. Dans Administration Console, cliquez sur Paramètres > Gestion des utilisateurs > Utilisateurs et groupes.
1. Indiquez les informations permettant d’affiner la recherche et cliquez sur Rechercher. Les résultats de recherche apparaissent au bas de la page. Vous pouvez trier la liste en cliquant sur les en-têtes de colonne.
1. Cochez les cases situées en regard des utilisateurs et des groupes à associer au rôle, puis cliquez sur Affecter le rôle.
1. Sélectionnez le rôle à affecter à l’utilisateur ou au groupe, puis cliquez sur OK.

Cette opération peut également s’effectuer via la page Gestion des rôles.

## Identification de la personne à laquelle est affecté un rôle {#determine-who-is-assigned-to-a-role}

1. Dans Administration Console, cliquez sur Paramètres > Gestion des utilisateurs > Gestion des rôles, puis sur Nom du rôle.

   Par défaut, tous les rôles trouvés dans la base de données User Management s’affichent dans la page Gestion des rôles. Si la liste est trop importante, utilisez la zone Rechercher située en haut de la page pour rechercher un nom de rôle particulier.

1. Dans la page Détails du rôle, cliquez sur l’onglet Utilisateurs de rôle. La liste des utilisateurs et des groupes directement associés au rôle s’affiche.

## Modification des droits d’un rôle {#change-role-permissions}

Vous pouvez modifier les droits des rôles que vous avez créés, mais pas ceux qui sont attribués aux rôles AEM Forms par défaut inclus au produit.

1. Dans Administration Console, cliquez sur Paramètres > Gestion des utilisateurs > Gestion des rôles, puis sur Nom du rôle.

   Par défaut, tous les rôles trouvés dans la base de données User Management s’affichent dans la page Gestion des rôles. Si la liste est trop importante, utilisez la zone Rechercher située en haut de la page pour rechercher un nom de rôle particulier.

1. Sélectionnez le rôle dont vous souhaitez afficher les droits, puis cliquez sur l’onglet Droits.
1. Pour modifier ces droits, cliquez sur Rechercher des droits, activez les cases à cocher correspondant aux droits à ajouter au rôle, cliquez sur OK, puis sur Enregistrer.
1. Pour supprimer un droit, sélectionnez-le, cliquez sur Supprimer, puis sur Enregistrer.

### Autorisations d’AEM Forms {#aem-forms-permissions}

**** ADD_REMOVE_ENDPOINT_PERM : Ajouter, supprimer et modifier des points de fin pour un service

**** Admin Console Login : Affichage d’Administration Console

**** Certificate Modify : Modification des paramètres d’approbation de tout certificat dans Trust Store

**** Certificate Read : permet de lire tout certificat dans Trust Store.

**** Certificate Write : Ajout d’un certificat au Trust Store

**** Component Add : Installer un nouveau composant dans le système

**** Component Delete : Supprimer tout composant du système

**** Component Read : permet de lire n’importe quel composant du système.

**** Administrateur Contentspace : Autorisation de l’administrateur Contentspace (obsolète)

**** Contentspace Console Login : Autorisation pour Contentspace (obsolète) Console Login

**** Contrôle des paramètres principaux : Gestion des paramètres de la page Paramètres de Core System dans Administration Console

**** CREATE_VERSION_PERM : Création d’une version d’un service

**** Credential Modify : Modification des informations d’identification de signature dans Trust Store

**** Informations d’identification Lues : permet de lire les informations d’identification de signature dans Trust Store.

**** Credential Write : Ajout d’informations d’identification de signature à Trust Store

**** CRL Modify : permet de modifier toute liste de révocation des certificats dans Trust Store.

**** CRL Read : permet de lire toute liste de révocation des certificats dans Trust Store.

**** CRL Write : Ajout d’une liste CRL à Trust Store

**** Déléguer : Définition d’une liste de contrôle d’accès sur une ressource

**** DELETE_VERSION_PERM : Suppression d’une version d’un service

**** Téléchargement du document : Téléchargement de documents dans AEM Forms

**** Domain Control : Créer, supprimer ou modifier des paramètres pour tout domaine User Management, y compris ses fournisseurs d’authentification et d’annuaire

**** Event Type Edit : Modifier en types d’événements

**** Identity Impersonation Control : Personnalisation de l’identité dans User Manager

**** INVOKE_PERM : Appeler toutes les opérations sur un service

**** LCDS Data Model Control : Lecture et déploiement de modèles de données dans Data Services

**** Mise à jour du Gestionnaire de licences : Mettre à jour les informations de licence

**** MODIFY_CONFIG_PERM : Modification de la configuration d’un service

**TERM** Modifier la version d’un service

**** PDFGAdminPermission : Administrateur PDFG

**** PDFGUserPermission : Utilisateur PDFG

**** PERM_DCTM_ADMIN : Administrateur Documentum Connector

**** PERM_FILENET_ADMIN : Administrateur FileNet Connector

**** PERM_FORMS_ADMIN : Administrateur Forms

**** PERM_IBMCM_ADMIN : Administrateur IBM CM Connector

**** PERM_OUTPUT_ADMIN : Administrateur Output

**** PERM_READER_EXTENSIONS_WEB_APPLICATION : Utilisation de l’application Web des extensions d’Acrobat Reader DC

**** PERM_SP_ADMIN : Gestion des paramètres de SharePoint Connector

**** PERM_WORKSPACE_ADMIN : Gestion des paramètres de Workspace

**** PERM_WORKSPACE_USER : Connexion à l’application Workspace destinée aux utilisateurs finaux

**** Principal Control : Gérez les utilisateurs et les groupes de n’importe quel domaine et gérez les affectations de rôles pour tous les utilisateurs et groupes de n’importe quel domaine.

**** Lecture/Suppression de l’enregistrement de processus : Répertorier et récupérer les instances d’audit de processus

**** PROCESS_OWNER_PERM : Afficher les données de tendance et exécuter des actions administratives sur un service créé à partir d’un processus

**** Lecture : Lire le contenu d’une ressource

**** READ_PERM : Lecture ou affichage d’un service

**** Renouveler l’affirmation : Renouveler les assertions dans User Management

**** Repository Delegate : Définition d’une liste de contrôle d’accès sur une ressource

**** Repository Read : Lire le contenu d’une ressource

**** Repository Traverse : Inclure une ressource dans une requête de ressources de liste ou lire les métadonnées d’une ressource

**** Repository Write : Ecrire les métadonnées et le contenu du référentiel

**** Rights Management Change Policy Owner : Modifier le propriétaire de la stratégie

**** Rights Management End User Console Login : Connectez-vous à l’interface utilisateur de Rights Management End User.

**** Rights Management Manage Configuration : Gestion de la configuration du serveur

**** Rights Management Gérer les utilisateurs invités et locaux : Gestion des utilisateurs invités et locaux

**** Rights Management Gérer les jeux de stratégies : Gérer toutes les stratégies et tous les documents d’un jeu de stratégies

**** Rights Management Policy Set Add Coordinator : Ajouter, supprimer et modifier des autorisations pour les coordinateurs de jeux de stratégies

**** Rights Management Policy Set Create Policy : Création d’une stratégie pour un jeu de stratégies

**** Rights Management Policy Set Delete Policy : Suppression d’une stratégie d’un jeu de stratégies

**** Rights Management Policy Set Edit Policy : Modification d’une stratégie dans un jeu de stratégies

**** Rights Management Policy Set Manage Document Publisher : Lorsque vous créez des jeux de stratégies, vous attribuez aux utilisateurs le rôle d’éditeur de documents. L’éditeur est l’utilisateur qui protège le document avec une stratégie.

**** Rights Management Policy Set Remove Coordinator : Suppression d’un coordinateur de jeux de stratégies d’un jeu de stratégies

**** Document de révocation du jeu de stratégies Rights Management : Révocation de l’accès aux documents d’un jeu de stratégies

**** Rights Management Policy Set Switch Policy Policy Policy Policy : Changer de stratégie pour un document

**** Document Annuler la révocation du jeu de stratégies Rights Management : Annulation de la révocation d’un document

**** Rights Management Policy Set View Event : Afficher les événements de stratégie et de document pour toute stratégie ou document au sein d’un jeu de stratégies

**** Rights Management View Server Events : Recherche et affichage de tous les événements de contrôle

**** Role Control : Création, suppression et modification de rôles dans User Management

**** Service Activate : Démarrez un service, le rendant disponible pour l’appel

**** Service Add : Déployez un nouveau service dans le registre des services. Cela inclut l’ajout de nouveaux processus et de variantes de processus.

**** Service Deactivate : Arrêt d’un service du système

**** Service Delete : Supprimer tout service du système, y compris les processus et les variantes de processus

**** Service Invoke : Appeler un service du registre de services disponible au moment de l’exécution

**** Service Modify : Modifiez les propriétés de configuration de tout service du système. Cela inclut le verrouillage et le déverrouillage d’un service dans l’IDE, et l’ajout ou la suppression de points de fin au niveau d’un service.

**** Service Read : Lisez tous les services du système. Cela inclut tous les processus et variantes de processus.

**** SERVICE_AGENT_PERM : Afficher les données et interagir avec les instances de processus pour un service créé à partir d’un processus

**** SERVICE_MANAGER_PERM : Exécution d’un équilibrage de charge et d’autres actions administratives sur un service créé à partir d’un processus

**** START_STOP_PERM : Démarrage ou arrêt d’un service

**** SUPERVISOR_PERM : Afficher les données d’instance de processus pour un service créé à partir d’un processus

**** Parcourir : Inclure une ressource dans une requête de ressources de liste ou lire les métadonnées d’une ressource

**** Écriture : Ecrire les métadonnées et le contenu du référentiel

**Ouverture de fichiers dans Workbench**

Pour consulter le contenu de l’affichage Ressources de Workbench et ouvrir des fichiers, un utilisateur a besoin des autorisations suivantes :

* Repository Read
* Repository Traverse
* Service Invoke
* Service Read

## Suppression d’un utilisateur ou d’un groupe d’un rôle {#remove-a-user-or-group-from-a-role}

La page Gestion des rôles permet de supprimer des utilisateurs et des groupes d’un rôle particulier. Si l’utilisateur ou le groupe a hérité de l’affectation du rôle, il est impossible de supprimer ce rôle au niveau de l’utilisateur ou du groupe. Supprimez l’utilisateur ou le groupe dans l’arborescence d’héritage ou supprimez le rôle depuis le parent.

1. Dans Administration Console, cliquez sur Paramètres > Gestion des utilisateurs > Gestion des rôles, puis sur Nom du rôle.

   Par défaut, tous les rôles trouvés dans la base de données User Management s’affichent dans la page Gestion des rôles. Si la liste est trop importante, utilisez la zone Rechercher située en haut de la page pour rechercher un nom de rôle particulier.

1. Dans la liste des rôles, cliquez sur le nom du rôle à mettre à jour, puis cliquez sur l’onglet Utilisateurs de rôle. La liste des utilisateurs et des groupes associés au rôle s’affiche.
1. Cochez les cases situées en regard des utilisateurs et des groupes à supprimer du rôle, puis cliquez sur Retirer.
1. Cliquez sur Enregistrer, puis sur OK.

