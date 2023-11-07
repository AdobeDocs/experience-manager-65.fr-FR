---
title: Créer et configurer des rôles
seo-title: Creating and configuring roles
description: Découvrez comment associer des utilisateurs et des groupes à des rôles déjà intégrés à la base de données User Management. Vous pouvez également créer, modifier et supprimer des rôles.
seo-description: Learn how to associate users and groups with roles that are already part of the User Management database. You can also create, edit, and delete roles.
uuid: e8e4331d-48e1-4fa9-8f44-f885f4ab1a54
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_organizing_users
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 737fb4d1-adef-47e1-9a0d-8cddd13132cb
exl-id: b447e545-f73e-4fde-a001-86e0e1cf4a12
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '2523'
ht-degree: 54%

---

# Créer et configurer des rôles{#creating-and-configuring-roles}

Les pages Web de User Management vous permettent d’associer des utilisateurs et des groupes à des rôles qui font déjà partie de la base de données User Management. Vous pouvez également créer, modifier et supprimer des rôles.

User Management dispose de deux types de rôles :

**Rôles modifiables :** ce type de rôle peut être modifié et supprimé et vous pouvez y ajouter des droits et en supprimer. Tout rôle que vous créez est considéré comme un rôle modifiable. Vous pouvez ajouter ou supprimer des utilisateurs et des groupes affectés à des rôles modifiables.

**Rôles non-modifiables :** les rôles par défaut inclus dans User Management sont des rôles non modifiables. Ces rôles ne peuvent pas être modifiés ni supprimés. Vous pouvez toutefois ajouter ou supprimer des utilisateurs et des groupes affectés à des rôles non modifiables.

Les API d’AEM forms permettent également de créer des rôles modifiables et non modifiables.

## Rôles par défaut {#default-roles}

Les rôles par défaut suivants sont inclus dans la base de données User Management.

**Utilisateur de la console d’administration :** peut accéder à la console d’administration.

**Administrateur de l’application :** peut utiliser toutes les fonctionnalités de Workbench. Peut utiliser les pages Applications et services d’Administration Console pour configurer des propriétés d’exécution de services, des points d’entrée et la sécurité.

**Administrateur d’AEM Forms :** peut effectuer toutes les tâches pour tous les services installés.

**Administrateur de la sécurité :** contrôle les paramètres User Management et gère les utilisateurs et les groupes associés aux domaines User Manager.

**Utilisateur des services :** peut afficher et appeler n’importe quel service.

**Super administrateur :** a accès à toutes les fonctionnalités administratives du système, notamment aux services.

**Administrateur de confiance :** peut gérer les paramètres d’approbation PKI et les informations d’identification PKI gérés à partir de la page de Trust Store Management dans la console d’administration.

### Rôles par défaut supplémentaires {#additional-default-roles}

Les rôles par défaut supplémentaires suivants peuvent être inclus, en fonction des composants d’AEM que vous avez installés.

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

**Administrateur des jeux de politique sur Rights Management :** exécute toutes les tâches requises pour l’ensemble des jeux de politiques dans les pages Rights Management appropriées.

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
>Pour des raisons de sécurité, les utilisateurs disposant de certains types de privilèges d’administrateur ne peuvent pas accéder aux pages Web des utilisateurs finaux de Workspace. Étant donné que ces pages peuvent se trouver en dehors d’un pare-feu, autoriser des tâches au niveau de l’administration peut présenter un risque de sécurité. Seuls les utilisateurs disposant des privilèges d’administrateur de l’espace de travail d’AEM forms ou d’utilisateur de l’espace de travail d’AEM forms peuvent accéder aux pages Web des utilisateurs finaux de l’espace de travail.

>[!NOTE]
>
>L’espace de travail Flex est obsolète pour la version d’AEM Forms.

## Création d’un rôle {#create-a-role}

1. Dans Administration Console, cliquez sur Paramètres > Gestion des utilisateurs > Gestion des rôles, puis sur Nouveau rôle.
1. Dans la zone Nom du rôle, saisissez le nom du rôle, saisissez éventuellement une description du rôle, puis cliquez sur Suivant.

   >[!NOTE]
   >
   >Lorsque vous utilisez MySQL, vous ne pouvez pas créer deux rôles portant le même nom, mais dont l’utilisation de caractères étendus diffère. Par exemple, si vous tentez de créer un rôle nommé abcde alors qu’un autre nommé âbcdè existe déjà, une erreur se produit.

1. Cliquez sur Rechercher des autorisations, sélectionnez les autorisations à ajouter au rôle.
1. Cliquez sur OK, puis sur Suivant.
1. Attribuez ce rôle aux utilisateurs et aux groupes :

   * Cliquez sur Rechercher des utilisateurs/groupes.
   * Dans la zone Rechercher, saisissez vos critères de recherche.
   * Sélectionnez Nom, Adresse électronique ou ID utilisateur, puis Utilisateurs, Groupes ou Utilisateurs et groupes.
   * Sélectionnez le domaine, le nombre de résultats à afficher, puis cliquez sur Rechercher.
   * Cochez les cases correspondant aux utilisateurs et aux groupes auxquels affecter ce rôle, puis cliquez sur OK.

1. Pour afficher les détails des utilisateurs et des groupes, sélectionnez l’entité.
1. Cliquez sur OK, puis sur Terminer.

## Modification d’un rôle {#edit-a-role}

1. Dans Administration Console, cliquez sur Paramètres > User Management > Gestion des rôles, puis sur Nom du rôle.

   Par défaut, la page Gestion des rôles affiche tous les rôles de la base de données User Management. Si la liste des rôles est volumineuse, utilisez la zone Rechercher située en haut de la page pour rechercher un nom de rôle spécifique.

1. Cliquez sur le rôle à modifier, modifiez les paramètres généraux, puis cliquez sur Enregistrer.
1. Pour modifier les autorisations de rôle, cliquez sur l’onglet Autorisations et procédez comme suit :

   * Pour ajouter de nouvelles autorisations, cliquez sur Rechercher des autorisations, cochez les cases correspondant aux autorisations à ajouter, cliquez sur OK, puis sur Enregistrer.
   * Pour supprimer une autorisation du rôle, cochez la case correspondant à l’autorisation, cliquez sur Supprimer, puis sur Enregistrer.

1. Pour gérer à qui le rôle est affecté, cliquez sur l’onglet Utilisateurs de rôle et procédez comme suit :

   * Pour attribuer le rôle aux nouveaux utilisateurs et groupes, cliquez sur Rechercher des utilisateurs/groupes, puis complétez les informations de recherche. Cochez la case correspondant à chaque utilisateur et groupe auquel affecter ce rôle, cliquez sur OK, puis sur Enregistrer.
   * Pour supprimer le rôle, cochez la case correspondant aux utilisateurs ou au groupe, cliquez sur Annuler l’affectation, puis sur Enregistrer.

## Suppression d’un rôle {#delete-a-role}

Vous pouvez supprimer les rôles que vous avez créés, mais pas les rôles d’AEM par défaut inclus dans le produit.

1. Dans Administration Console, cliquez sur Paramètres > User Management > Gestion des rôles, puis sur Nom du rôle.

   Par défaut, la page Gestion des rôles affiche tous les rôles de la base de données User Management. Si la liste des rôles est volumineuse, utilisez la zone Rechercher située en haut de la page pour rechercher un nom de rôle spécifique.

1. Cochez la case correspondant au rôle à supprimer, cliquez sur Supprimer, puis sur OK.

## Attribution d’un rôle aux utilisateurs et aux groupes {#assign-a-role-to-users-and-groups}

1. Dans Administration Console, cliquez sur Paramètres > Gestion des utilisateurs > Utilisateurs et groupes.
1. Indiquez les informations permettant d’affiner la recherche, puis cliquez sur Rechercher. Les résultats de la recherche apparaissent au bas de la page. Vous pouvez trier la liste en cliquant sur l’un des en-têtes de colonne.
1. Cochez les cases en regard des utilisateurs et des groupes à associer à un rôle, puis cliquez sur Attribuer un rôle.
1. Sélectionnez le rôle à affecter à l’utilisateur ou au groupe, puis cliquez sur OK.

Vous pouvez également affecter des rôles à l’aide de la page Gestion des rôles .

## Déterminer qui est affecté à un rôle {#determine-who-is-assigned-to-a-role}

1. Dans Administration Console, cliquez sur Paramètres > User Management > Gestion des rôles, puis sur Nom du rôle.

   Par défaut, la page Gestion des rôles affiche tous les rôles de la base de données User Management. Si la liste des rôles est volumineuse, utilisez la zone Rechercher située en haut de la page pour rechercher un nom de rôle spécifique.

1. Sur la page Détails du rôle , cliquez sur l’onglet Utilisateurs de rôle . Une liste des utilisateurs et des groupes directement associés au rôle s’affiche.

## Modification des autorisations de rôle {#change-role-permissions}

Vous pouvez modifier les autorisations de l’un des rôles que vous avez créés. Vous ne pouvez pas modifier les autorisations des rôles d’AEM par défaut inclus dans le produit.

1. Dans Administration Console, cliquez sur Paramètres > User Management > Gestion des rôles, puis sur Nom du rôle.

   Par défaut, la page Gestion des rôles affiche tous les rôles de la base de données User Management. Si la liste des rôles est volumineuse, utilisez la zone Rechercher située en haut de la page pour rechercher un nom de rôle spécifique.

1. Sélectionnez le rôle pour lequel afficher les autorisations, puis cliquez sur l’onglet Autorisations .
1. Pour modifier ces autorisations, cliquez sur Rechercher des autorisations, cochez les cases correspondant aux autorisations à ajouter au rôle, cliquez sur OK, puis sur Enregistrer.
1. Pour supprimer une autorisation, sélectionnez-la, cliquez sur Supprimer, puis sur Enregistrer.

### Autorisations des formulaires AEM {#aem-forms-permissions}

**ADD_REMOVE_ENDPOINTS_PERM :** ajouter, supprimer et modifier des points d’entrée d’un service.

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

**CREATE_VERSION_PERM :** Création d’une version d’un service

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

**Rights Management Change Policy Owner :** permet de modifier le propriétaire de la politique.

**Rights Management End User Console Login :** permet de se connecter à l’interface des utilisateurs finaux de Rights Management.

**Rights Management Manage Configuration :** permet de gérer la configuration du serveur.

**Rights Management Manage Invited and Local Users :** permet de gérer les utilisateurs invités et locaux.

**Rights Management Manage Policy Sets :** permet de gérer toutes les politiques et tous les documents au sein d’un jeu de politiques.

**Rights Management Policy Set Add Coordinator :** permet d’ajouter, de supprimer et de modifier des autorisations pour les coordinateurs de jeux de politiques.

**Création d’un jeu de stratégies de Rights Management :** Création d’une stratégie pour un jeu de stratégies

**Rights Management Policy Set Delete Policy :** permet de supprimer une politique à partir d’un jeu de politiques.

**Rights Management Policy Set Edit Policy :** permet de modifier une politique dans un jeu de politiques.

**Rights Management Policy Set Manage Document Publisher :** lorsque vous créez des jeux de politiques, vous affectez à des utilisateurs le rôle d’éditeur de document. L’éditeur est l’utilisateur qui protège le document avec une politique.

**Rights Management Policy Set Remove Coordinator :** permet de supprimer un coordinateur de jeux de politiques.

**Rights Management Policy Set Revoke Document :** permet d’appeler l’accès aux documents d’un jeu de politiques.

**Rights Management Policy Set Switch Policy :** permet de changer de politique pour un document.

**Rights Management Policy Set Unrevoke Document :** permet d’annuler la révocation d’un document.

**Rights Management Policy Set View Event :** permet d’afficher des événements de politique et de document pour n’importe quel document ou politique du jeu de politiques.

**Rights Management View Server Events :** permet de rechercher et d’afficher tous les événements de contrôle.

**Role Control :** permet de créer, supprimer et modifier des rôles dans User Management.

**Service Activate :** permet de démarrer un service, en le rendant disponible pour des appels.

**Service Add :** permet de déployer un nouveau service dans le registre des services. Cela inclut l’ajout de nouveaux processus et de variantes de processus.

**Service Deactivate :** permet d’arrêter tout service du système.

**Service Delete :** permet de supprimer tout service du système, y compris les processus et variantes de processus.

**Service Invoke :** permet d’appeler tout service dans le registre de services disponible au moment de l’exécution.

**Service Modify :** permet de modifier les propriétés de configuration de tout service du système. Cela inclut le verrouillage et le déverrouillage d’un service dans l’IDE, et l’ajout ou la suppression de points d’entrée au niveau d’un service.

**Service Read :** permet de lire tout service du système. Cela inclut tous les processus et variantes de processus.

**SERVICE_AGENT_PERM :** permet d’afficher des données et d’interagir avec des instances de processus pour un service créé à partir d’un processus.

**SERVICE_MANAGER_PERM :** permet d’effectuer des actions d’équilibrage de charge et d’autres actions administratives sur un service créé à partir d’un processus.

**START_STOP_PERM :** permet de démarrer ou d’arrêter un service.

**SUPERVISOR_PERM :** permet d’afficher les données d’instance de processus d’un service créé à partir d’un processus.

**Traverse :** permet d’inclure une ressource dans une demande de ressources de liste ou de lire les métadonnées d’une ressource.

**Write :** permet d’enregistrer des métadonnées et du contenu de référentiel.

**Ouverture de fichiers dans Workbench**

Pour afficher le contenu de l’affichage Ressources dans Workbench et ouvrir les fichiers à des fins d’affichage, un utilisateur a besoin des autorisations suivantes :

* Repository Read
* Repository Traverse
* Service Invoke
* Service Read

## Supprimer un utilisateur ou un groupe d’un rôle {#remove-a-user-or-group-from-a-role}

Utilisez la page Gestion des rôles pour supprimer des utilisateurs et des groupes d’un rôle particulier. Si l’utilisateur ou le groupe a hérité de l’affectation du rôle, vous ne pouvez pas le supprimer au niveau de l’utilisateur ou du groupe. Supprimez l’utilisateur ou le groupe de l’arborescence d’héritage ou supprimez le rôle du parent.

1. Dans Administration Console, cliquez sur Paramètres > User Management > Gestion des rôles, puis sur Nom du rôle.

   Par défaut, la page Gestion des rôles affiche tous les rôles de la base de données User Management. Si la liste des rôles est volumineuse, utilisez la zone Rechercher située en haut de la page pour rechercher un nom de rôle spécifique.

1. Dans la liste des rôles, cliquez sur le nom du rôle à mettre à jour, puis sur l’onglet Utilisateurs de rôle . Une liste d’utilisateurs et de groupes associés au rôle s’affiche.
1. Cochez les cases correspondant aux utilisateurs et aux groupes à supprimer du rôle, puis cliquez sur Annuler l’affectation.
1. Cliquez sur Enregistrer, puis sur OK.
