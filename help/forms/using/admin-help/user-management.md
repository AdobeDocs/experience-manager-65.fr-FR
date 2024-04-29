---
title: Gestion des utilisateurs et utilisatrices
description: La gestion des utilisateurs et utilisatrices vous permet d’activer l’authentification unique (SSO) entre les modules d’AEM Forms et les applications protégées par Netegrity SiteMinder à l’aide du langage SAML. Ce document fournit des informations supplémentaires à propos de la gestion des utilisateurs et utilisatrices.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 1da1f6de-ac0d-4e0d-b8bb-956420e42699
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: ht
source-wordcount: '472'
ht-degree: 100%

---

# Gestion des utilisateurs {#user-management}

La gestion des utilisateurs et utilisatrices vous permet d’activer l’authentification unique (SSO) entre les modules d’AEM Forms et les applications protégées par Netegrity SiteMinder à l’aide du langage SAML. Lorsque la fonction SSO est implémentée, les pages d’ouverture de session utilisateur d’AEM forms ne sont plus obligatoires et ne s’affichent pas si l’utilisateur est déjà authentifié via le portail d’entreprise.

Pour plus d’informations sur l’amélioration des performances de synchronisation de base de données et d’annuaire pour DB2, voir [Base de données IBM DB2 : exécution de commandes pour une maintenance régulière](/help/forms/using/admin-help/ibm-db2-database-running-commands.md#ibm-db2-database-running-commands-for-regular-maintenance).

## Configuration de la gestion des utilisateurs et utilisatrices pour un serveur LDAP compatible SSL {#configuring-user-management-for-an-ssl-enabled-ldap-server}

Si vous disposez d’un serveur LDAP compatible SSL, configurez la gestion des utilisateurs et utilisatrices pour l’utiliser. (Voir [Configuration de la gestion des utilisateurs et utilisatrices pour un serveur LDAP compatible SSL](/help/forms/using/admin-help/configure-user-management-ssl-enabled.md#configure-user-management-for-an-ssl-enabled-ldap-server).)

## Définition des privilèges utilisateur à utiliser avec Document Security {#setting-user-privileges-for-use-with-document-security}

Créez une personne administratrice disposant des privilèges appropriés pour la création d’utilisateurs, d’utilisatrices et de groupes. Si votre environnement d’AEM Forms comprend Document Security, accordez le droit de gérer les personnes invitées et locales à une personne qui sera l’administratrice de ces utilisateurs et utilisatrices. Attribuez également le rôle Utilisateur ou utilisatrice de la console d’administration pour permettre à la personne d’accéder à la console d’administration. (Voir [Création et configuration de rôles](/help/forms/using/admin-help/creating-configuring-roles.md#creating-and-configuring-roles).)

Pour afficher les utilisateurs, les utilisatrices et les groupes dans les domaines sélectionnés lors des recherches d’utilisateurs ou utilisatrices de politiques, une personne super-administratrice ou un administrateur ou administratrice de jeux de politiques doit sélectionner et ajouter des domaines (créés dans la gestion des utilisateurs et utilisatrices) à la liste des utilisateurs, des utilisatrices et des groupes visibles pour chaque jeu de politiques créé.

La liste des utilisateurs, des utilisatrices et des groupes est visible par la personne coordinatrice de jeux de politiques. Elle permet de restreindre les domaines que l’utilisateur ou l’utilisatrice peut parcourir lorsqu’il ou elle choisit des utilisateurs, des utilisatrices ou des groupes à ajouter aux politiques. Si cette tâche n’est pas effectuée, la personne coordinatrice de jeux de politiques ne trouvera aucun utilisateur, utilisatrice ou groupe à ajouter à la politique. Un jeu de politiques peut avoir plusieurs personnes coordinatrices.

>[!NOTE]
>
>Vous devez créer les domaines avant de pouvoir créer des politiques.

### Définition des utilisateurs, utilisatrices et groupes visibles {#set-visible-users-and-groups}

Après avoir installé et configuré votre environnement d’AEM Forms avec Document Security, configurez tous les domaines appropriés dans la gestion des utilisateurs et utilisatrices.

1. Dans la console d’administration, cliquez sur Services > Document Security > Politiques, puis sur l’onglet Jeux de politiques.
1. Sélectionnez Jeu de politiques global, puis cliquez sur l’onglet Utilisateurs, utilisatrices et groupes visibles.
1. Cliquez sur Ajouter un ou des domaine(s) et ajoutez des domaines existants selon les besoins.
1. Accédez à Services > Document Security > Configuration > Mes politiques, puis cliquez sur l’onglet Utilisateurs, utilisatrices et groupes visibles.
1. Cliquez sur Ajouter un ou des domaine(s) et ajoutez des domaines existants selon les besoins.

## Restrictions de la personne administratrice {#administrator-user-restrictions}

Pour des raisons de sécurité, les personnes disposant de certains types de privilèges administrateur ne peuvent pas accéder aux pages web des utilisateurs et utilisatrices finaux de Workspace. Étant donné que ces pages web peuvent exister en dehors d’un pare-feu, autoriser des tâches au niveau de l’administration peut présenter un risque de sécurité. Seules les personnes disposant des privilèges administrateur ou utilisateur de Workspace peuvent accéder aux pages web des utilisateurs et utilisatrices finaux.

>[!NOTE]
>
>L’espace de travail Flex est obsolète pour la version d’AEM Forms.
