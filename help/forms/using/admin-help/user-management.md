---
title: Gestion des utilisateurs
seo-title: Gestion des utilisateurs
description: Le gestionnaire des utilisateurs vous permet également d’activer l’authentification unique (SSO) entre les modules d’AEM forms et les applications protégées par Netegrity SiteMinder, à l’aide du langage SAML. Ce document fournit plus d’informations concernant le gestionnaire des utilisateurs.
seo-description: Le gestionnaire des utilisateurs vous permet également d’activer l’authentification unique (SSO) entre les modules d’AEM forms et les applications protégées par Netegrity SiteMinder, à l’aide du langage SAML. Ce document fournit plus d’informations concernant le gestionnaire des utilisateurs.
uuid: f0c8331a-d995-483d-97b7-259df53b1a1a
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 10e6177a-8228-4515-aba9-bbe59bede449
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 100%

---


# Gestion des utilisateurs {#user-management}

Le gestionnaire des utilisateurs vous permet également d’activer l’authentification unique (SSO) entre les modules d’AEM forms et les applications protégées par Netegrity SiteMinder, à l’aide du langage SAML (Security Assertion Markup Language). Lorsque la fonction SSO est implémentée, les pages d’ouverture de session utilisateur d&#39;AEM forms ne sont plus obligatoires et ne s’affichent pas si l’utilisateur est déjà authentifié via le portail d’entreprise.

Pour plus d’informations sur l’amélioration des performances de synchronisation de la base de données et de l’annuaire pour DB2, voir [Base de données IBM DB2 : exécution des commandes pour des opérations de maintenance standard](/help/forms/using/admin-help/ibm-db2-database-running-commands.md#ibm-db2-database-running-commands-for-regular-maintenance).

## Configuration de User Management pour un serveur LDAP compatible SSL {#configuring-user-management-for-an-ssl-enabled-ldap-server}

Si vous disposez d’un serveur LDAP compatible SSL, configurez User Management en conséquence (voir [Configuration de User Management pour un serveur LDAP compatible SSL](/help/forms/using/admin-help/configure-user-management-ssl-enabled.md#configure-user-management-for-an-ssl-enabled-ldap-server)).

## Définition des privilèges d’utilisateur utilisés avec Document Security  {#setting-user-privileges-for-use-with-document-security}

Créez un utilisateur administrateur disposant des privilèges appropriés pour la création d’utilisateurs et de groupes. Si votre environnement AEM forms inclut Document Security, accordez le privilège de gestion des utilisateurs locaux et invités à un utilisateur qui sera l’administrateur de ces utilisateurs. Affectez-lui également le rôle Utilisateur d’Administration Console de manière à permettre à cet utilisateur d’accéder à Administration Console (voir [Création et configuration de rôles](/help/forms/using/admin-help/creating-configuring-roles.md#creating-and-configuring-roles)).

Pour afficher les utilisateurs et les groupes des domaines sélectionnés lors des recherches d’utilisateurs de stratégies, un super-administrateur ou un administrateur de jeux de stratégies doit sélectionner et ajouter des domaines (créés dans User Management) à la liste des utilisateurs et groupes visibles pour chaque jeu de stratégies créé.

La liste des utilisateurs et des groupes visibles est accessible au coordinateur des jeux de stratégies. Elle permet de restreindre les domaines que ce dernier peut consulter lorsqu’il choisit les utilisateurs ou les groupes à ajouter aux stratégies. Si cette tâche n’est pas effectuée, le coordinateur des jeux de stratégies ne trouvera aucun utilisateur ni aucun groupe à ajouter aux stratégies. Un jeu de stratégies peut avoir plusieurs coordinateurs.

>[!NOTE]
>
>vous devez commencer par créer les domaines avant de pouvoir créer des stratégies.

### Définition des utilisateurs et groupes visibles  {#set-visible-users-and-groups}

Après avoir installé et configuré l’environnement AEM forms avec Document Security, définissez tous les domaines appropriés dans Gestion des utilisateurs.

1. Dans Administration Console, cliquez sur Services > Document Security> Stratégies et cliquez sur l’onglet Jeux de stratégies.
1. Sélectionnez Jeu de stratégies global, puis cliquez sur l’onglet Utilisateurs et groupes visibles.
1. Cliquez sur Ajouter des domaines et ajoutez les domaines nécessaires.
1. Accédez à Services > Document Security > Configuration > Mes stratégies et cliquez sur l’onglet Utilisateurs et groupes visibles.
1. Cliquez sur Ajouter des domaines et ajoutez les domaines nécessaires.

## Restrictions de l’utilisateur administrateur  {#administrator-user-restrictions}

Pour des raisons de sécurité, les utilisateurs disposant de certains types de privilèges d’administrateur n’ont pas accès aux pages Web des utilisateurs finaux de Workspace. Comme ces pages Web peuvent se trouver en dehors d’un pare-feu, autoriser des tâches d’administration pourrait présenter un risque de sécurité. Seuls les utilisateurs disposant du privilège d’administrateur de Workspace ou du privilège d’utilisateur de Workspace peuvent accéder aux pages Web des utilisateurs finaux.

>[!NOTE]
>
>Flex Workspace est obsolète pour la version d’AEM forms.

