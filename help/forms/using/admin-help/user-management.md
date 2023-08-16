---
title: User Management
seo-title: User Management
description: User Management vous permet d’activer l’authentification unique entre les modules d’AEM forms et les applications protégées par Netegrity SiteMinder à l’aide de SAML. Ce document fournit des informations supplémentaires sur User Management.
seo-description: User Management lets you enable SSO between AEM forms modules and Netegrity SiteMinder-protected applications by using SAML. This document provides more information about User Management.
uuid: f0c8331a-d995-483d-97b7-259df53b1a1a
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 10e6177a-8228-4515-aba9-bbe59bede449
exl-id: 1da1f6de-ac0d-4e0d-b8bb-956420e42699
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 8%

---

# Gestion des utilisateurs {#user-management}

User Management vous permet d’activer l’authentification unique (SSO) entre les modules d’AEM forms et les applications protégées par Netegrity SiteMinder à l’aide du langage SAML (Security Assertion Markup Language). Lorsque la fonction SSO est implémentée, les pages d’ouverture de session utilisateur d’AEM forms ne sont plus obligatoires et ne s’affichent pas si l’utilisateur est déjà authentifié via le portail d’entreprise.

Pour plus d’informations sur l’amélioration des performances de synchronisation de base de données et d’annuaire pour DB2, voir [Base de données IBM DB2 : exécution de commandes pour une maintenance régulière](/help/forms/using/admin-help/ibm-db2-database-running-commands.md#ibm-db2-database-running-commands-for-regular-maintenance).

## Configuration de User Management pour un serveur LDAP compatible SSL {#configuring-user-management-for-an-ssl-enabled-ldap-server}

Si vous disposez d’un serveur LDAP compatible SSL, configurez User Management pour l’utiliser. (Voir [Configuration de User Management pour un serveur LDAP compatible SSL](/help/forms/using/admin-help/configure-user-management-ssl-enabled.md#configure-user-management-for-an-ssl-enabled-ldap-server).)

## Définition des privilèges d’utilisateur à utiliser avec Document Security {#setting-user-privileges-for-use-with-document-security}

Créez un utilisateur administrateur disposant des privilèges appropriés pour créer des utilisateurs et des groupes. Si votre environnement d’AEM forms comprend Document Security, accordez le droit de gérer les utilisateurs invités et locaux à un utilisateur qui sera l’administrateur de ces utilisateurs. Attribuez également le rôle Utilisateur d’Administration Console pour permettre à l’utilisateur d’accéder à Administration Console. (Voir [Création et configuration des rôles](/help/forms/using/admin-help/creating-configuring-roles.md#creating-and-configuring-roles).)

Pour afficher les utilisateurs et les groupes dans les domaines sélectionnés lors des recherches d’utilisateurs de stratégies, un super-administrateur ou un administrateur de jeux de stratégies doit sélectionner et ajouter des domaines (créés dans User Management) à la liste des utilisateurs et des groupes visibles pour chaque jeu de stratégies créé.

La liste des utilisateurs et des groupes visibles est visible par le coordinateur de jeux de stratégies. Elle permet de restreindre les domaines que l’utilisateur final peut parcourir lorsqu’il choisit des utilisateurs ou des groupes à ajouter aux stratégies. Si cette tâche n’est pas effectuée, le coordinateur de jeux de stratégies ne trouvera aucun utilisateur ou groupe à ajouter à la stratégie. Il peut y avoir plusieurs coordinateurs de jeux de stratégies pour un jeu donné.

>[!NOTE]
>
>La création de domaines doit être effectuée avant la création de stratégies.

### Définition des utilisateurs et groupes visibles {#set-visible-users-and-groups}

Après avoir installé et configuré votre environnement d’AEM forms avec Document Security, configurez tous les domaines appropriés dans User Management.

1. Dans Administration Console, cliquez sur Services > Document Security > Stratégies, puis sur l’onglet Jeux de stratégies.
1. Sélectionnez Jeu de stratégies global, puis cliquez sur l’onglet Utilisateurs et groupes visibles.
1. Cliquez sur Ajouter un(s) domaine(s) et ajoutez des domaines existants selon les besoins.
1. Accédez à Services > Document Security > Configuration > Mes stratégies, puis cliquez sur l’onglet Utilisateurs et groupes visibles .
1. Cliquez sur Ajouter un(s) domaine(s) et ajoutez des domaines existants selon les besoins.

## Restrictions utilisateur de l’administrateur {#administrator-user-restrictions}

Pour des raisons de sécurité, les utilisateurs disposant de certains types de privilèges d’administrateur ne peuvent pas accéder aux pages Web des utilisateurs finaux de Workspace. Étant donné que ces pages web peuvent se trouver en dehors d’un pare-feu, autoriser des tâches au niveau de l’administration peut présenter un risque de sécurité. Seuls les utilisateurs disposant des privilèges d’administrateur ou d’utilisateur de Workspace peuvent accéder aux pages Web des utilisateurs finaux.

>[!NOTE]
>
>L’espace de travail Flex est obsolète pour la version d’AEM Forms.
