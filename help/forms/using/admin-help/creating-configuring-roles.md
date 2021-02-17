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
workflow-type: tm+mt
source-wordcount: '2556'
ht-degree: 51%

---


# Création et configuration des rôles{#creating-and-configuring-roles}

Les pages Web de User Management vous permettent d’associer des utilisateurs et des groupes à des rôles faisant partie de la base de données User Management. Vous pouvez également créer, modifier et supprimer des rôles.

User Management comporte deux types de rôles :

**Rôles mutables :** Ce type de rôle peut être modifié et supprimé et les autorisations de rôle peuvent être ajoutées et supprimées de ces types de rôle. Les rôles que vous créez sont des rôles mutables. Vous pouvez ajouter et supprimer des utilisateurs et groupes affectés à des rôles mutables.

**Rôles immuables :** les rôles par défaut inclus dans User Management sont des rôles immuables. Ils ne peuvent être ni modifiés ni supprimés. Toutefois, vous pouvez ajouter ou supprimer des utilisateurs et des groupes affectés à des rôles non modifiables.

Les API d&#39;AEM forms permettent également de créer des rôles modifiables et non modifiables.

## Rôles par défaut {#default-roles}

Les rôles par défaut suivants sont inclus dans la base de données Gestion des utilisateurs.

**Utilisateur d’Administration Console :** peut accéder à Administration Console.

**Administrateur d’applications :** peut utiliser toutes les fonctionnalités de Workbench. Peut utiliser les pages Applications et services de Administration Console pour configurer des propriétés d’exécution de services, des points de fin et la sécurité.

**Administrateur AEM forms :** peut exécuter toutes les tâches pour tous les services installés.

**Administrateur de sécurité :** contrôle les paramètres User Management et gère les utilisateurs et les groupes associés à tout domaine User Manager.

**Utilisateur des services :** peut vue et appeler n’importe quel service.

**Super administrateur :** a accès à toutes les fonctionnalités d’administration du système, y compris les services

**Administrateur d’approbation :** peut gérer les paramètres d’approbation PKI et les informations d’identification PKI qui sont gérés à partir de la page Trust Store Management dans Administration Console.

### Rôles par défaut supplémentaires {#additional-default-roles}

Les rôles par défaut supplémentaires suivants peuvent également être inclus, selon les composants d’AEM Forms installés.

**Utilisateur de l’application de téléchargement de document :** peut télécharger des documents à l’aide de Flex Remoting.

**Administrateur Forms :** peut vue et modifier des paramètres de la page Forms dans Administration Console

**AEM forms Contentspace Administrator :** peut vue et modifier des paramètres de la page Content Services (obsolète) dans Administration Console.

**AEM Forms Contentspace User:** peut se connecter aux pages Web Contentspace (obsolète)

**Documentum Connector Administrator :** peut vue et modifier des paramètres de la page Connector for EMC Documentum dans Administration Console.

**AEM forms Administrateur FileNet Connector :** peut vue et modifier des paramètres de la page Connector for IBM FileNet dans Administration Console.

**AEM forms Administrateur IBM CM Connector :** peut vue et modifier des paramètres de la page Connector for IBM Content Manager dans Administration Console.

**Administrateur Rights Management :** exécute toutes les tâches requises pour toutes les configurations de serveur sur les pages de Rights Management appropriées.

**Utilisateur final Rights Management :** peut accéder aux pages Web des utilisateurs finaux Rights Management

**Rights Management Invitation d’un utilisateur :** peut inviter des utilisateurs

**Rights Management Gérer les utilisateurs invités et locaux :** peut exécuter les tâches requises pour gérer tous les utilisateurs invités et locaux sur les pages de Rights Management appropriées.

**Administrateur de jeux de stratégies de Rights Management :** exécute toutes les tâches requises pour tous les jeux de stratégies sur les pages de Rights Management appropriées.

**Super administrateur Rights Management :** exécute toutes les tâches requises à partir de la page Rights Management

**AEM Forms Workspace Administrator :** peut vue et modifier des paramètres de la page Workspace dans Administration Console

***Remarque ** : Flex Workspace est obsolète pour la version d’AEM Forms.*

**Utilisateur de Workspace :** peut se connecter à l’application Workspace destinée aux utilisateurs finaux.

**Administrateur Output :** peut vue et modifier des paramètres de la page Output dans Administration Console.

**Administrateur PDFG :** peut vue et modifier des paramètres de la page PDF Generator dans Administration Console.

**utilisateur de PDFG :** peut accéder à toutes les fonctionnalités non administratives de PDF Generator.

**application web des extensions Acrobat Reader DC :** peut utiliser l’application Web des extensions Acrobat Reader DC

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

## Modification d’un rôle  {#edit-a-role}

1. Dans Administration Console, cliquez sur Paramètres > Gestion des utilisateurs > Gestion des rôles, puis sur Nom du rôle.

   Par défaut, tous les rôles trouvés dans la base de données User Management s’affichent dans la page Gestion des rôles. Si la liste est trop importante, utilisez la zone Rechercher située en haut de la page pour rechercher un nom de rôle particulier.

1. Cliquez sur le rôle à modifier, modifiez les paramètres généraux, puis cliquez sur Enregistrer.
1. Pour modifier les droits du rôle, cliquez sur l’onglet Droits et procédez comme suit :

   * Pour ajouter de nouveaux droits, cliquez sur Rechercher des droits, activez les cases à cocher correspondant aux droits à ajouter, cliquez sur OK, puis sur Enregistrer.
   * Pour supprimer un droit d’un rôle, activez la case à cocher correspondant au droit, cliquez sur Supprimer, puis sur Enregistrer.

1. Pour gérer l’affectation d’un rôle, cliquez sur l’onglet Utilisateurs de rôle et procédez comme suit :

   * Pour affecter le rôle à de nouveaux utilisateurs et à de nouveaux groupes, cliquez sur Rechercher des utilisateurs/groupes et saisissez les informations de recherche. Activez la case à cocher correspondant aux utilisateurs et aux groupes auxquels affecter ce rôle, cliquez sur OK, puis sur Enregistrer.
   * Pour supprimer le rôle, activez la case à cocher correspondant aux utilisateurs ou aux groupes, cliquez sur Retirer, puis sur Enregistrer.

## Suppression d’un rôle  {#delete-a-role}

Vous pouvez supprimer tous les rôles créés, mais pas les rôles AEM Forms par défaut intégrés au produit.

1. Dans Administration Console, cliquez sur Paramètres > Gestion des utilisateurs > Gestion des rôles, puis sur Nom du rôle.

   Par défaut, tous les rôles trouvés dans la base de données User Management s’affichent dans la page Gestion des rôles. Si la liste est trop importante, utilisez la zone Rechercher située en haut de la page pour rechercher un nom de rôle particulier.

1. Cochez la case correspondant au rôle à supprimer, cliquez sur Supprimer, puis sur OK.

## Affectation d’un rôle aux utilisateurs et aux groupes  {#assign-a-role-to-users-and-groups}

1. Dans Administration Console, cliquez sur Paramètres > Gestion des utilisateurs > Utilisateurs et groupes.
1. Indiquez les informations permettant d’affiner la recherche et cliquez sur Rechercher. Les résultats de recherche apparaissent au bas de la page. Vous pouvez trier la liste en cliquant sur les en-têtes de colonne.
1. Cochez les cases situées en regard des utilisateurs et des groupes à associer au rôle, puis cliquez sur Affecter le rôle.
1. Sélectionnez le rôle à affecter à l’utilisateur ou au groupe, puis cliquez sur OK.

Cette opération peut également s’effectuer via la page Gestion des rôles.

## Identification de la personne à laquelle est affecté un rôle  {#determine-who-is-assigned-to-a-role}

1. Dans Administration Console, cliquez sur Paramètres > Gestion des utilisateurs > Gestion des rôles, puis sur Nom du rôle.

   Par défaut, tous les rôles trouvés dans la base de données User Management s’affichent dans la page Gestion des rôles. Si la liste est trop importante, utilisez la zone Rechercher située en haut de la page pour rechercher un nom de rôle particulier.

1. Dans la page Détails du rôle, cliquez sur l’onglet Utilisateurs de rôle. La liste des utilisateurs et des groupes directement associés au rôle s’affiche.

## Modification des droits d’un rôle  {#change-role-permissions}

Vous pouvez modifier les droits des rôles que vous avez créés, mais pas ceux qui sont attribués aux rôles AEM Forms par défaut inclus au produit.

1. Dans Administration Console, cliquez sur Paramètres > Gestion des utilisateurs > Gestion des rôles, puis sur Nom du rôle.

   Par défaut, tous les rôles trouvés dans la base de données User Management s’affichent dans la page Gestion des rôles. Si la liste est trop importante, utilisez la zone Rechercher située en haut de la page pour rechercher un nom de rôle particulier.

1. Sélectionnez le rôle dont vous souhaitez afficher les droits, puis cliquez sur l’onglet Droits.
1. Pour modifier ces droits, cliquez sur Rechercher des droits, activez les cases à cocher correspondant aux droits à ajouter au rôle, cliquez sur OK, puis sur Enregistrer.
1. Pour supprimer un droit, sélectionnez-le, cliquez sur Supprimer, puis sur Enregistrer.

### Autorisations d’AEM Forms  {#aem-forms-permissions}

**AJOUTE_REMOVE_ENDPOINT_PERM:** Ajouter, supprimer et modifier des points de fin pour un service

**Admin Console Login:** Vue de la console d’administration

**Certificate Modify :** modifiez les paramètres d’approbation de tout certificat dans Trust Store.

**Certificat Lu :** permet de lire tout certificat dans Trust Store.

**Écriture de certificat:** Ajouter un certificat à Trust Store

**Ajoute de composant :** installation d’un nouveau composant dans le système

**Component Delete :** supprime tout composant du système

**Composant Lu :** permet de lire tout composant du système.

**Contentspace Administrator:** Permission for Contentspace (obsolète) Administrator

**Contentspace Console Login:** Permission for Contentspace (obsolète) Console Login

**Contrôle des paramètres principaux :** gérez les paramètres de la page Paramètres de Core System dans Administration Console.

**CREATE_VERSION_PERM:** Création d’une version d’un service

**modification des informations d’identification:** modification des informations d’identification de signature dans Trust Store

**Informations d’identification Lues :** permet de lire les informations d’identification de signature dans Trust Store.

**écriture des informations d’identification:** Ajouter des informations d’identification de signature à Trust Store

**CRL Modify:** Modify any CRL (Certificate Revocation Liste) dans Trust Store

**Lecture de la liste CRL :** lecture de toute liste CRL dans Trust Store

**CRL Write:** Ajouter une CRL à Trust Store

**Délégué:** Définition d&#39;une ACL sur une ressource

**DELETE_VERSION_PERM:** Suppression d’une version d’un service

**Document Upload:** Téléchargement de documents dans AEM formulaires

**Contrôle de domaine :** créez, supprimez ou modifiez des paramètres pour tout domaine User Management, y compris les fournisseurs d’authentification et d’annuaire.

**type d&#39;événement de modification:** modification en type d&#39;événement

**Identity Impersonation Control:** Impersonation identity dans User Manager

**INVOKE_PERM:** appel de toutes les opérations sur un service

**LCDS Data Model Control:** Lecture et déploiement des modèles de données dans Data Services

**Mise à jour de License Manager:** Mise à jour des informations de licence

**MODIFY_CONFIG_PERM:** Modification de la configuration d’un service

**** TERMModifier la version d’un service

**PDFGAdminPermission:administrateur de** PDFG

**PDFGUserPermission:utilisateur** PDFG

**PERM_DCTM_ADMIN:administrateur de** Documentum Connector

**PERM_FILENET_ADMIN:administrateur de** FileNet Connector

**PERM_FORMS_ADMIN:administrateur** Forms

**PERM_IBMCM_ADMIN:administrateur d’** IBM CM Connector.

**PERM_OUTPUT_ADMIN:administrateur** Output

**PERM_READER_EXTENSIONS_WEB_APPLICATION:** Utilisation de l’application Web des extensions Acrobat Reader DC

**PERM_SP_ADMIN:** Gestion des paramètres de SharePoint Connector

**PERM_WORKSPACE_ADMIN:** Gestion des paramètres de l’espace de travail

**PERM_WORKSPACE_USER:** Connexion à l’application Workspace destinée aux utilisateurs finaux

**Principal Control :** gérez les utilisateurs et les groupes pour n’importe quel domaine, et gérez les affectations de rôles pour tous les utilisateurs et groupes de n’importe quel domaine.

**Enregistrement du processus Lecture/Suppression:** Liste et récupération des instances d’audit du processus

**PROCESS_OWNER_PERM:** Vue des données de tendance et exécution d’actions administratives sur un service créé à partir d’un processus

**Lecture:** lecture du contenu d’une ressource

**READ_PERM:** lecture ou vue d’un service

**Renouveler l’assertion:** Renouveler les assertions dans User Management

**Repository Delegate:** Définition d’une ACL sur une ressource

**Repository Read:** Lecture du contenu d’une ressource

**Repository Traverse:** Inclure une ressource dans une demande de ressources de liste ou lire les métadonnées d&#39;une ressource

**Repository Write:** Write repository metadata and content

**Rights Management Changer de propriétaire de stratégie:** Changer de propriétaire de stratégie

**Rights Management End User Console Login:** Connexion à l’interface utilisateur Rights Management End User

**Rights Management Gérer la configuration:** Gérer la configuration du serveur

**Rights Management Gérer les utilisateurs invités et locaux:** Gérer les utilisateurs invités et locaux

**Rights Management Gérer les jeux de stratégies:** Gérer toutes les stratégies et tous les documents d’un jeu de stratégies

**coordinateur d’Ajoutes de jeux de stratégies Rights Management:** Ajouter, supprimer et modifier les autorisations des coordinateurs de jeux de stratégies

**jeu de stratégies Rights Management Créer une stratégie:** Créer une stratégie pour un jeu de stratégies

**jeu de stratégies Rights Management Supprimer la stratégie:** supprimer une stratégie d’un jeu de stratégies

**jeu de stratégies Rights Management Modifier la stratégie:** modifier une stratégie dans un jeu de stratégies

**Jeu de stratégies de Rights Management Gérer l’éditeur de Document :** lorsque vous créez des jeux de stratégies, vous attribuez aux utilisateurs le rôle d’éditeur de document. L’éditeur est l’utilisateur qui protège le document avec une stratégie.

**jeu de stratégies Rights Management Supprimer le coordinateur:** Supprimer un coordinateur de jeux de stratégies d’un jeu de stratégies

**document de révocation du jeu de stratégies de Rights Management :** révoquer l’accès aux documents d’un jeu de stratégies

**Jeu de stratégies Rights Management Stratégie de changement :** Changer de stratégie pour un document

**document Annuler la révocation du jeu de stratégies de Rights Management :** Annuler la révocation d&#39;un document

**événement de Vue du jeu de stratégies de Rights Management:stratégie de** Vue et événement de document pour toute stratégie ou document d’un jeu de stratégies

**événements du serveur de Vue Rights Management :** recherche et vue de tous les événements de contrôle

**Contrôle des rôles:** création, suppression et modification de rôles dans User Management

**Service Activate:** Début de tout service, le rendant disponible pour un appel

**Ajoute de service :** déployez un nouveau service dans le registre de services. Cela inclut l’ajout de nouveaux processus et de variantes de processus.

**Service Deactivate:** Arrêt d’un service du système

**Service Delete :** permet de supprimer tout service du système, y compris les processus et variantes de processus.

**Service Invoke:** Invoke tout service du registre de services disponible à l’exécution

**Service Modify :** modifiez les propriétés de configuration de tout service du système. Cela inclut le verrouillage et le déverrouillage d’un service dans l’IDE, et l’ajout ou la suppression de points de fin au niveau d’un service.

**Service Read :** permet de lire tous les services du système. Cela inclut tous les processus et variantes de processus.

**SERVICE_AGENT_PERM:** Vue de données et interaction avec les instances de processus pour un service créé à partir d’un processus

**SERVICE_MANAGER_PERM:** Exécution de l’équilibrage de charge et d’autres actions administratives sur un service créé à partir d’un processus

**DÉBUT_STOP_PERM:** Début ou arrêt d’un service

**SUPERVISOR_PERM:** Vue des données d’instance de processus pour un service créé à partir d’un processus

**Traverse:** Inclure une ressource dans une demande de ressources de liste ou lire les métadonnées d&#39;une ressource

**Écrire:** Écrire les métadonnées et le contenu du référentiel

**Ouverture de fichiers dans Workbench**

Pour consulter le contenu de l’affichage Ressources de Workbench et ouvrir des fichiers, un utilisateur a besoin des autorisations suivantes :

* Repository Read
* Repository Traverse
* Service Invoke
* Service Read

## Suppression d’un utilisateur ou d’un groupe d’un rôle  {#remove-a-user-or-group-from-a-role}

La page Gestion des rôles permet de supprimer des utilisateurs et des groupes d’un rôle particulier. Si l’utilisateur ou le groupe a hérité de l’affectation du rôle, il est impossible de supprimer ce rôle au niveau de l’utilisateur ou du groupe. Supprimez l’utilisateur ou le groupe dans l’arborescence d’héritage ou supprimez le rôle depuis le parent.

1. Dans Administration Console, cliquez sur Paramètres > Gestion des utilisateurs > Gestion des rôles, puis sur Nom du rôle.

   Par défaut, tous les rôles trouvés dans la base de données User Management s’affichent dans la page Gestion des rôles. Si la liste est trop importante, utilisez la zone Rechercher située en haut de la page pour rechercher un nom de rôle particulier.

1. Dans la liste des rôles, cliquez sur le nom du rôle à mettre à jour, puis cliquez sur l’onglet Utilisateurs de rôle. La liste des utilisateurs et des groupes associés au rôle s’affiche.
1. Cochez les cases situées en regard des utilisateurs et des groupes à supprimer du rôle, puis cliquez sur Retirer.
1. Cliquez sur Enregistrer, puis sur OK.

