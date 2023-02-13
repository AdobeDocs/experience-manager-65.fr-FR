---
title: Créer et configurer des rôles
seo-title: Creating and configuring roles
description: Découvrez comment associer des utilisateurs et des groupes à des rôles faisant partie de la base de données User Management. Vous pouvez également créer, modifier et supprimer des rôles.
seo-description: Learn how to associate users and groups with roles that are already part of the User Management database. You can also create, edit, and delete roles.
uuid: e8e4331d-48e1-4fa9-8f44-f885f4ab1a54
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_organizing_users
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 737fb4d1-adef-47e1-9a0d-8cddd13132cb
exl-id: b447e545-f73e-4fde-a001-86e0e1cf4a12
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '2526'
ht-degree: 100%

---

# Créer et configurer des rôles{#creating-and-configuring-roles}

Les pages Web de User Management vous permettent d’associer des utilisateurs et des groupes à des rôles faisant partie de la base de données User Management. Vous pouvez également créer, modifier et supprimer des rôles.

User Management comporte deux types de rôles :

**Rôles modifiables :** ce type de rôle peut être modifié et supprimé et vous pouvez y ajouter des droits et en supprimer. Les rôles que vous créez sont des rôles mutables. Vous pouvez ajouter et supprimer des utilisateurs et groupes affectés à des rôles mutables.

**Rôles non-modifiables :** les rôles par défaut inclus dans User Management sont des rôles non modifiables. Ils ne peuvent être ni modifiés ni supprimés. Toutefois, vous pouvez ajouter ou supprimer des utilisateurs et des groupes affectés à des rôles non modifiables.

Les API d’AEM forms permettent également de créer des rôles modifiables et non modifiables.

## Rôles par défaut {#default-roles}

Les rôles par défaut suivants sont inclus dans la base de données Gestion des utilisateurs.

**Utilisateur de la console d’administration :** peut accéder à la console d’administration.

**Administrateur de l’application :** peut utiliser toutes les fonctionnalités de Workbench. Peut utiliser les pages Applications et services d’Administration Console pour configurer des propriétés d’exécution de services, des points de fin et la sécurité.

**Administrateur d’AEM Forms :** peut effectuer toutes les tâches pour tous les services installés.

**Administrateur de la sécurité :** contrôle les paramètres User Management et gère les utilisateurs et les groupes associés aux domaines User Manager.

**Utilisateur des services :** peut afficher et appeler n’importe quel service.

**Super administrateur :** a accès à toutes les fonctionnalités administratives du système, notamment aux services.

**Administrateur de confiance :** peut gérer les paramètres d’approbation PKI et les informations d’identification PKI gérés à partir de la page de Trust Store Management dans la console d’administration.

### Rôles par défaut supplémentaires {#additional-default-roles}

Les rôles par défaut supplémentaires suivants peuvent également être inclus, selon les composants d’AEM Forms installés.

**Utilisateur de l’application de téléchargement de document :** peut télécharger des documents à l’aide de Flex Remoting.

**Administrateur Forms :** peut afficher et modifier des paramètres de la page Forms dans la console d’administration.

**Administrateur AEM Forms Contentspace :** peut afficher et modifier des paramètres de la page Content Services (obsolète) dans la console d’administration.

**Utilisateur AEM Forms Contentspace :** peut se connecter aux pages web de Contentspace (obsolète).

**Administrateur Documentum Connector :** peut afficher et modifier des paramètres de la page Connector for EMC Documentum dans la console d’administration.

**Administrateur FileNet Connector d’AEM forms :** peut afficher et modifier les paramètres de la page Connector for IBM FileNet dans la console d’administration.

**Administrateur AEM Forms IBM CM Connector :** peut afficher et modifier les paramètres de la page Connector for IBM Content Manager dans la console d’administration.

**Administrateur Rights Management :** exécute toutes les tâches requises pour l’ensemble des configurations de serveur dans les pages Rights Management appropriées.

**Utilisateur final Rights Management :** peut accéder aux pages web des utilisateurs finaux Rights Management.

**Utilisateur Rights Management Invite :** peut inviter des utilisateurs.

**Gérer les utilisateurs invités et locaux sur Rights Management :** peut effectuer les tâches requises pour gérer tous les utilisateurs invités et locaux sur les pages de Rights Management appropriées.

**Administrateur des jeux de stratégie sur Rights Management :** exécute toutes les tâches requises pour l’ensemble des jeux de stratégies dans les pages Rights Management appropriées.

**Super administrateur Rights Management :** exécute toutes les tâches requises à partir de la page Rights Management.

**Administrateur d’espace de travail AEM Forms :** peut afficher et modifier les paramètres de la page Espace de travail dans la console d’administration.

***Remarque ** : Flex Workspace est obsolète pour la version d’AEM Forms.*

**Utilisateur Workspace :** peut se connecter à l’application Workspace destinée aux utilisateurs finaux.

**Administrateur Output :** peut afficher et modifier des paramètres de la page Output dans la console d’administration.

**Administrateur PDFG :** peut afficher et modifier des paramètres de la page PDF Generator dans la console d’administration.

**Utilisateur PDFG :** peut accéder à toutes les fonctionnalités non administratives de PDF Generator.

**Application web des extensions Acrobat Reader DC :** peut utiliser l’application web des extensions Acrobat Reader DC.

>[!NOTE]
>
>pour des raisons de sécurité, les utilisateurs disposant de certains types de privilèges d’administrateur n’ont pas accès aux pages Web des utilisateurs finaux de Workspace. Comme ces pages peuvent se trouver en dehors d’un pare-feu, autoriser des tâches d’administration pourrait présenter un risque de sécurité. Seuls les utilisateurs disposant du privilège d’administrateur ou d’utilisateur d’AEM Forms Workspace peuvent accéder aux pages Web des utilisateurs finaux de Workspace.

>[!NOTE]
>
>L’espace de travail Flex est obsolète pour la version d’AEM Forms.

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

**ADD_REMOVE_ENDPOINTS_PERM :** ajouter, supprimer et modifier des points de fin d’un service.

**Connexion à Admin Console :** affichage de la console d’administration.

**Modifier un certificat :** permet de modifier les paramètres d’approbation de tout certificat de Trust Store.

**Lire un certificat :** permet de lire tout certificat de Trust Store.

**Écrire un certificat :** permet d’ajouter un certificat à Trust Store.

**Ajouter des composants :** permet d’installer un nouveau composant dans le système.

**Supprimer des composants :** permet de supprimer tout composant du système.

**Lire des composants :** permet de lire tout composant du système.

**Administrateur Contentspace :** permet d’autoriser l’administrateur Contentspace (obsolète).

**Connexion à la console Contentspace :** permet d’autoriser la connexion à la console Contentspace (obsolète).

**Contrôle des paramètres principaux :** permet de gérer les paramètres de la page Paramètres principaux du système dans la console d’administration.

**CREATE_VERSION_PERM :** permet de créer une nouvelle version du service.

**Modifier les informations d’identification :** permet de modifier toute information d’identification de signature dans Trust Store.

**Lire les informations d’identification :** permet de lire toute information d’identification de signature dans Trust Store.

**Écrire des informations d’identification :** permet d’ajouter une information d’identification de signature dans Trust Store.

**Modifier des listes de révocation des certificats :** permet de modifier toute liste de révocation des certificats (CRL, Certificate Revocation List) dans Trust Store.

**Lire des listes de révocation des certificats :** permet de lire toute liste de révocation des certificats de Trust Store.

**Écrire des listes de révocation des certificats :** permet d’ajouter une liste de révocation des certificats à Trust Store.

**Déléguer :** permet de définir une liste de contrôle d’accès (ACL) pour une ressource.

**DELETE_VERSION_PERM :** permet de supprimer une version du service.

**Charger des documents :** permet de charger des documents dans AEM Forms.

**Contrôler les domaines :** permet de créer, supprimer ou modifier des paramètres pour tout domaine User Management, y compris ses fournisseurs d’authentification et d’annuaire.

**Event Type Edit :** permet de modifier des types d’événements.

**Identity Impersonation Control :** permet d’emprunter une identité dans User Manager.

**INVOKE_PERM :** permet d’appeler toutes les opérations d’un service.

**LCDS Data Model Control :** permet de lire et déployer des modèles de données dans Data Services.

**License Manager Update :** permet de mettre à jour les informations de licence.

**MODIFY_CONFIG_PERM :** permet de modifier la configuration d’un service.

**TERM :** permet de modifier la version d’un service.

**PDFGAdminPermission :** administrateur PDFG

**PDFGUserPermission :** utilisateur PDFG

**PERM_DCTM_ADMIN :** administrateur Documentum Connector

**PERM_FILENET_ADMIN :** administrateur FileNet Connector

**PERM_FORMS_ADMIN :** administrateur Forms

**PERM_IBMCM_ADMIN :** administrateur d’IBM CM Connector

**PERM_OUTPUT_ADMIN :** administrateur Output

**PERM_READER_EXTENSIONS_WEB_APPLICATION :** permet d’utiliser l’application web Extensions Acrobat Reader DC.

**PERM_SP_ADMIN :** permet de gérer les paramètres de SharePoint Connector.

**PERM_WORKSPACE_ADMIN :** permet de gérer les paramètres de Workspace.

**PERM_WORKSPACE_USER :** permet de se connecter à l’application Workspace destinée aux utilisateurs finaux.

**Principal Control :** permet de gérer les utilisateurs et groupes de n’importe quel domaine, et de gérer les affectations de rôles pour tous les utilisateurs et groupes de n’importe quel domaine.

**Process Recording Read/Delete :** permet de répertorier et de récupérer les instances de contrôle des workflows.

**PROCESS_OWNER_PERM :** permet de visualiser les données sur les tendances et d’effectuer des tâches administratives sur un service créé à partir d’un processus.

**Read :** permet de lire le contenu d’une ressource.

**READ_PERM :** permet de lire ou d’afficher un service.

**Renouveler l’assertion :** permet de renouveler les assertions dans User Management.

**Repository Delegate :** permet de définir une liste de contrôle d’accès (ACL) pour une ressource.

**Repository Read :** permet de lire le contenu d’une ressource.

**Repository Traverse :** permet d’inclure une ressource dans une demande de ressources de liste ou de lire les métadonnées d’une ressource.

**Repository Write :** permet d’enregistrer des métadonnées et du contenu de référentiel.

**Rights Management Change Policy Owner :** permet de modifier le propriétaire de la stratégie.

**Rights Management End User Console Login :** permet de se connecter à l’interface des utilisateurs finaux de Rights Management.

**Rights Management Manage Configuration :** permet de gérer la configuration du serveur.

**Rights Management Manage Invited and Local Users :** permet de gérer les utilisateurs invités et locaux.

**Rights Management Manage Policy Sets :** permet de gérer toutes les stratégies et tous les documents au sein d’un jeu de stratégies.

**Rights Management Policy Set Add Coordinator :** permet d’ajouter, de supprimer et de modifier des autorisations pour les coordinateurs de jeux de stratégies.

**Rights Management Policy Set Create Policy :** permet de créer une nouvelle stratégie pour un jeu de stratégies.

**Rights Management Policy Set Delete Policy :** permet de supprimer une stratégie à partir d’un jeu de stratégies.

**Rights Management Policy Set Edit Policy :** permet de modifier une stratégie dans un jeu de stratégies.

**Rights Management Policy Set Manage Document Publisher :** lorsque vous créez des jeux de stratégies, vous affectez à des utilisateurs le rôle d’éditeur de document. L’éditeur est l’utilisateur qui protège le document avec une stratégie.

**Rights Management Policy Set Remove Coordinator :** permet de supprimer un coordinateur de jeux de stratégies.

**Rights Management Policy Set Revoke Document :** permet d’appeler l’accès aux documents d’un jeu de stratégies.

**Rights Management Policy Set Switch Policy :** permet de changer de stratégie pour un document.

**Rights Management Policy Set Unrevoke Document :** permet d’annuler la révocation d’un document.

**Rights Management Policy Set View Event :** permet d’afficher des événements de stratégie et de document pour n’importe quel document ou stratégie du jeu de stratégies.

**Rights Management View Server Events :** permet de rechercher et d’afficher tous les événements de contrôle.

**Role Control :** permet de créer, supprimer et modifier des rôles dans User Management.

**Service Activate :** permet de démarrer un service, en le rendant disponible pour des appels.

**Service Add :** permet de déployer un nouveau service dans le registre des services. Cela inclut l’ajout de nouveaux processus et de variantes de processus.

**Service Deactivate :** permet d’arrêter tout service du système.

**Service Delete :** permet de supprimer tout service du système, y compris les processus et variantes de processus.

**Service Invoke :** permet d’appeler tout service dans le registre de services disponible au moment de l’exécution.

**Service Modify :** permet de modifier les propriétés de configuration de tout service du système. Cela inclut le verrouillage et le déverrouillage d’un service dans l’IDE, et l’ajout ou la suppression de points de fin au niveau d’un service.

**Service Read :** permet de lire tout service du système. Cela inclut tous les processus et variantes de processus.

**SERVICE_AGENT_PERM :** permet d’afficher des données et d’interagir avec des instances de processus pour un service créé à partir d’un processus.

**SERVICE_MANAGER_PERM :** permet d’effectuer des actions d’équilibrage de charge et d’autres actions administratives sur un service créé à partir d’un processus.

**START_STOP_PERM :** permet de démarrer ou d’arrêter un service.

**SUPERVISOR_PERM :** permet d’afficher les données d’instance de processus d’un service créé à partir d’un processus.

**Traverse :** permet d’inclure une ressource dans une demande de ressources de liste ou de lire les métadonnées d’une ressource.

**Write :** permet d’enregistrer des métadonnées et du contenu de référentiel.

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
