---
title: Authentification Adobe IMS et prise en charge par l’ [!DNL Admin Console]  d’AEM Managed Services
seo-title: Adobe IMS Authentication and [!DNL Admin Console] Support for AEM Managed Services
description: Découvrez comment utiliser l’ [!DNL Admin Console]  dans AEM.
seo-description: Learn how to use the [!DNL Admin Console] in AEM.
uuid: 3f5b32c7-cf62-41a4-be34-3f71bbf224eb
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: f6112dea-a1eb-4fd6-84fb-f098476deab7
exl-id: 95eae97c-01c2-4f5c-8068-f504eab7c49e
feature: Security
source-git-commit: 778987e69a23f81584f7a86db2fe24df64035919
workflow-type: tm+mt
source-wordcount: '1683'
ht-degree: 99%

---

# Authentification Adobe IMS et prise en charge par l’[!DNL Admin Console] d’AEM Managed Services {#adobe-ims-authentication-and-admin-console-support-for-aem-managed-services}

>[!NOTE]
>
>Notez que cette fonctionnalité n’est disponible que pour les clients Adobe Managed Services.

>[!NOTE]
>
>AEM ne prend actuellement pas en charge l’affectation de groupes à des profils. Les utilisateurs doivent être ajoutés individuellement.

## Présentation {#introduction}

AEM 6.4.3.0 introduit la prise en charge par l’[!DNL Admin Console] de l’authentification aux instances AEM et basées sur Adobe IMS (système de gestion d’identité) pour les clients **AEM Managed Services**.

L’intégration d’AEM à l’[!DNL Admin Console] permettra aux clients AEM Managed Services de gérer tous les utilisateurs d’Experience Cloud dans une seule console. Les utilisateurs et les groupes peuvent être affectés aux profils de produit associés aux instances AEM, ce qui leur permet de se connecter à une instance spécifique.

## Principales caractéristiques {#key-highlights}

* La prise en charge de l’authentification IMS d’AEM est réservée aux auteurs, administrateurs ou développeurs AEM et non aux utilisateurs finaux externes de sites clients comme les visiteurs de site
* L’[!DNL Admin Console] représentera les clients AEM Managed Services comme des organisations IMS, et leurs instances comme des contextes de produit. Le système client et les responsables de l’administration des produits pourront gérer l’accès aux instances
* AEM Managed Services synchronisera les topologies client à l’aide de l’[!DNL Admin Console]. Chaque instance disposera d’une instance de contexte de produit AEM Managed Services dans l’[!DNL Admin Console].
* Les profils de produit dans l’[!DNL Admin Console] détermineront à quelles instances un utilisateur peut accéder.
* L’authentification fédérée à l’aide des propres fournisseurs d’identité des clients conformes SAML 2 est prise en charge
* Seuls les ID d’entreprise ou fédérés (pour l’authentification unique du client) sont pris en charge, et non les Adobe ID personnels.
* [!DNL User Management] (dans l’[!DNL Admin Console] Adobe) sera toujours contrôlée par les responsables de l’administration du client.

## Architecture {#architecture}

L’authentification IMS fonctionne en utilisant le protocole OAuth entre AEM et le point de terminaison Adobe IMS. Une fois qu’un utilisateur a été ajouté à IMS et possède une identité Adobe, il peut se connecter aux instances AEM Managed Services à l’aide des informations d’identification IMS.

Le flux d’identifiant de connexion utilisateur est indiqué ci-dessous, l’utilisateur sera redirigé vers IMS et éventuellement vers le fournisseur d’identité client pour la validation SSO, puis redirigé vers AEM.

![image2018-9-23_23-55-8](assets/image2018-9-23_23-55-8.png)

## Méthode de configuration {#how-to-set-up}

### Intégration des organisations à l’[!DNL Admin Console] {#onboarding-organizations-to-admin-console}

L’intégration à l’[!DNL Admin Console] est un prérequis pour utiliser Adobe IMS pour l’authentification à AEM.

Pour commencer, une organisation doit être configurée dans Adobe IMS. Les clients Adobe Grands comptes sont représentés en tant qu’organisations IMS dans [l’ [!DNL Admin Console] Adobe](https://helpx.adobe.com/fr/enterprise/using/admin-console.html).

Une organisation doit déjà être configurée pour les clients AEM Managed Services et, dans le cadre de la mise en service IMS, les instances seront mise à disposition dans l’[!DNL Admin Console] pour gérer les droits et accès d’utilisation.

L’activation de authentification par IMS sera menée conjointement par AMS et par les organisations, chacun devant mener à bien ses propres workflows.

Une fois qu’un client est défini en tant qu’organisation IMS et qu’AMS a provisionné ce client dans l’IMS, voici, en résumé, les workflows de configuration nécessaires :

![image2018-9-23_23-33-25](assets/image2018-9-23_23-33-25.png)

1. Le responsable désigné d’administration système reçoit une invitation à se connecter à l’[!DNL Admin Console].
1. L’administrateur système désigne le domaine pour confirmer la propriété du nom de domaine (dans cet exemple acme.com)
1. L’administrateur système configure les répertoires utilisateur
1. Le responsable d’administration système configure le fournisseur d’identité (IDP) dans l’[!DNL Admin Console] pour la configuration SSO.
1. Le responsable d’administration AEM gère comme d’habitude les groupes locaux, les autorisations et les droits. Consultez la section Synchronisation des utilisateurs et des groupes

>[!NOTE]
>
>Pour plus d’informations sur les bases de la gestion des identités dans Adobe, y compris sur la configuration du fournisseur d’identité, consultez l’article présenté [sur cette page.](https://helpx.adobe.com/fr/enterprise/using/set-up-identity.html)
>
>Pour plus d’informations sur l’administration des Grands comptes et sur l’[!DNL Admin Console], consultez l’article présenté [sur cette page](https://helpx.adobe.com/fr/enterprise/managing/user-guide.html).

### Intégration d’utilisateurs à l’[!DNL Admin Console] {#onboarding-users-to-the-admin-console}

Il existe trois méthodes d’intégration en fonction de la taille de l’organisation et de ses préférences :

1. Création manuelle d’utilisateurs et de groupes dans [!DNL Admin Console]
1. Téléchargement d’un fichier CSV avec des utilisateurs
1. Synchronisation des utilisateurs et des groupes depuis le répertoire Active Directory d’entreprise du client.

#### Ajout manuel à l’aide de l’interface utilisateur de l’[!DNL Admin Console] {#manual-addition-through-admin-console-ui}

Les utilisateurs et les groupes peuvent être créés manuellement dans l’interface utilisateur de l’[!DNL Admin Console]. Cette méthode peut être utilisée s’il y a un nombre réduit d’utilisateurs à gérer. Par exemple, moins de 50 utilisateurs d’AEM.

Les utilisateurs peuvent aussi être créés manuellement si le client utilise déjà cette méthode pour administrer d’autres produits Adobe comme Analytics, Target ou des applications Creative Cloud.

![image2018-9-23_20-39-9](assets/image2018-9-23_20-39-9.png)

#### Chargement du fichier dans l’interface utilisateur [!DNL Admin Console] {#file-upload-in-the-admin-console-ui}

Pour gérer facilement la création d’utilisateurs, un fichier CSV peut être chargé pour permettre l’ajout en bloc des utilisateurs :

![image2018-9-23_18-59-57](assets/image2018-9-23_18-59-57.png)

#### Outil de synchronisation des utilisateurs {#user-sync-tool}

L’outil de synchronisation des utilisateurs permet aux clients d’entreprise de créer ou de gérer des utilisateurs Adobe utilisant Active Directory ou d’autres services testés de répertoires OpenLDAP. Les utilisateurs cibles sont les administrateurs d’identité informatique (Enterprise Directory et administrateurs système) qui pourront installer et configurer l’outil. Cet outil en open source est personnalisable, de telle sorte que les clients peuvent le faire modifier par un développeur en fonction de leurs besoins spécifiques.

Lorsque la synchronisation des utilisateurs s’exécute, elle récupère une liste d’utilisateurs à partir du répertoire Active Directory de l’organisation (ou de toute autre source de données compatible) et la compare à la liste des utilisateurs de l’[!DNL Admin Console]. Elle appelle ensuite l’API [!DNL User Management] d’Adobe pour synchroniser l’[!DNL Admin Console] avec le répertoire de l’organisation. Le flux de modification est complètement unidirectionnel et les modifications apportées dans l’[!DNL Admin Console] ne sont pas transférées vers le répertoire.

Cet outil permet à l’administrateur système de mapper les groupes d’utilisateurs dans le répertoire client avec la configuration de produits et les groupes d’utilisateurs dans l’[!DNL Admin Console]. La nouvelle version de l’outil de synchronisation des utilisateurs permet également la création dynamique de groupes d’utilisateurs dans l’[!DNL Admin Console].

Pour configurer la synchronisation des utilisateurs, l’organisation doit créer un ensemble d’informations d’identification de la même manière qu’avec l’[[!DNL User Management] API](https://www.adobe.io/apis/cloudplatform/usermanagement/docs/setup.html).

![image2018-9-23_13-36-56](assets/image2018-9-23_13-36-56.png)

La synchronisation des utilisateurs est distribuée via le référentiel Adobe Github à cet emplacement :

[https://github.com/adobe-apiplatform/user-sync.py/releases/latest](https://github.com/adobe-apiplatform/user-sync.py/releases/latest)

Notez qu’une version préliminaire 2.4 RC1 avec prise en charge de création de groupe dynamique est disponible à l’adresse suivante : [https://github.com/adobe-apiplatform/user-sync.py/releases/tag/v2.4rc1](https://github.com/adobe-apiplatform/user-sync.py/releases/tag/v2.4rc1).

Cette version a pour principales fonctionnalités la possibilité de mapper de manière dynamique les nouveaux groupes LDAP pour l’appartenance des utilisateurs à [!DNL Admin Console], ainsi que la création dynamique de groupes d’utilisateurs.

Vous trouverez plus d’informations sur les nouvelles fonctionnalités du groupe aux adresses :

[https://adobe-apiplatform.github.io/user-sync.py/en/user-manual/advanced_configuration.html#additional-group-options](https://adobe-apiplatform.github.io/user-sync.py/en/user-manual/advanced_configuration.html#additional-group-options)

>[!NOTE]
>
>Pour plus d’informations sur l’outil de synchronisation des utilisateurs, consultez la [page de documentation](https://adobe-apiplatform.github.io/user-sync.py/en/).
>
>
>L’outil de synchronisation des utilisateurs doit s’enregistrer en tant qu’UMAPI client d’Adobe I/O en suivant la procédure décrite [ici](https://adobe-apiplatform.github.io/umapi-documentation/en/UM_Authentication.html).
>
>La documentation relative à la console Adobe I/O est disponible [ici](https://www.adobe.io/apis/cloudplatform/console.html).
>
>
>Le fonctionnement de l’API [!DNL User Management] utilisée par l’outil de synchronisation des utilisateurs est abordé en détail [ici](https://www.adobe.io/apis/cloudplatform/umapi-new.html).

>[!NOTE]
>
>La configuration IMS d’AEM sera gérée par l’équipe Adobe Managed Services. Cependant, l’administrateur du client peut la modifier en fonction de ses besoins (par exemple, pour gérer l’appartenance automatique des groupes ou le mappage de groupes). Le client IMS sera également enregistré par votre équipe Managed Services.

## Utilisation {#how-to-use}

### Gestion des produits et des accès utilisateur dans [!DNL Admin Console] {#managing-products-and-user-access-in-admin-console}

Lorsque le responsable d’administration du produit se connecte à l’[!DNL Admin Console], il voit plusieurs instances de contexte du produit AEM Managed Services, comme illustré ci-dessous :

![screen_shot_2018-09-17at105804pm](assets/screen_shot_2018-09-17at105804pm.png)

Dans cet exemple, l’organisation *AEM-MS-Onboard* comporte 32 instances couvrant différents environnements et topologies tels que l’évaluation, l’exploitation, etc.

![screen_shot_2018-09-17at105517pm](assets/screen_shot_2018-09-17at105517pm.png)

Les détails de l’instance peuvent être vérifiés pour identifier celle-ci :

![screen_shot_2018-09-17at105601pm](assets/screen_shot_2018-09-17at105601pm.png)

Un profil de produit est associé à chaque instance de contexte du produit. Ce profil de produit est utilisé pour attribuer l’accès aux utilisateurs et aux groupes.

![image2018-9-18_7-48-50](assets/image2018-9-18_7-48-50.png)

Tous les utilisateurs et groupes ajoutés au profil de produit pourront se connecter à cette instance, comme illustré dans l’exemple ci-dessous :

![screen_shot_2018-09-17at105623pm](assets/screen_shot_2018-09-17at105623pm.png)

### Connexion à AEM {#logging-into-aem}

#### Connexion de l’administrateur local {#local-admin-login}

AEM peut continuer à prendre en charge les connexions locales pour les utilisateurs administrateurs, puisque l’écran de connexion dispose d’une option de connexion locale :

![screen_shot_2018-09-18at121056am](assets/screen_shot_2018-09-18at121056am.png)

#### Connexion via IMS {#ims-based-login}

Pour les autres cas, la connexion via IMS peut être utilisée une fois qu’IMS est configuré sur l’instance. L’utilisateur doit d’abord cliquer sur le bouton **Se connecter avec Adobe** comme illustré ci-dessous :

![image2018-9-18_0-10-32](assets/image2018-9-18_0-10-32.png)

Il est alors redirigé vers l’écran de connexion IMS et saisit ses informations d’identification :

![screen_shot_2018-09-17at115629pm](assets/screen_shot_2018-09-17at115629pm.png)

Si un fournisseur d’identité fédéré est configuré lors de la configuration initiale d’[!DNL Admin Console], l’utilisateur est redirigé vers le fournisseur d’identité client pour SSO. 

Le fournisseur d’identité est Okta dans l’exemple ci-dessous :

![screen_shot_2018-09-17at115734pm](assets/screen_shot_2018-09-17at115734pm.png)

Une fois l’authentification terminée, l’utilisateur est redirigé vers AEM et connecté :

![screen_shot_2018-09-18at120124am](assets/screen_shot_2018-09-18at120124am.png)

### Migration d’utilisateurs existants {#migrating-existing-users}

Pour les instances AEM existantes qui utilisent une autre méthode d’authentification et qui sont désormais migrées vers IMS, une étape de migration est nécessaire.

Les utilisateurs existants dans le référentiel AEM (origine locale via LDAP ou SAML) peuvent être migrés pour pointer vers l’IMS en tant que fournisseur d’identité à l’aide de l’utilitaire de migration d’utilisateur.

Cet utilitaire sera exécuté par votre équipe AMS dans le cadre de la mise en service de l’IMS.

### Gestion des autorisations et des listes de contrôle d’accès dans AEM {#managing-permissions-and-acls-in-aem}

Le contrôle et les autorisations d’accès continueront à être gérés dans AEM. Pour cela, il convient de séparer les groupes d’utilisateurs issus de l’IMS (par exemple AEM-GRP-008 dans l’exemple ci-dessous) des groupes locaux où sont définis les autorisations et le contrôle d’accès. Les groupes d’utilisateurs synchronisés à partir de l’IMS peuvent être attribués aux groupes locaux et hériter des autorisations.

Dans l’exemple ci-dessous, nous ajoutons des groupes synchronisés au groupe local *Dam_Users*.

Dans ce cas, un utilisateur a également été attribué à plusieurs groupes dans l’[!DNL Admin Console]. (Notez que les utilisateurs et les groupes peuvent être synchronisés à partir du LDAP à l’aide de l’outil de synchronisation des utilisateurs ou alors créés localement ; consultez la section **Intégration d’utilisateurs à l’[!DNL Admin Console]** ci-dessus).

>[!NOTE]
>
>Les groupes d’utilisateurs ne sont synchronisés que lorsque les utilisateurs se connectent à l’instance.

![screen_shot_2018-09-17at94207pm](assets/screen_shot_2018-09-17at94207pm.png)

L’utilisateur fait partie des groupes suivants dans IMS :

![screen_shot_2018-09-17at94237pm](assets/screen_shot_2018-09-17at94237pm.png)

Lorsque l’utilisateur se connecte, ses adhésions de groupes sont synchronisées, comme illustré ci-dessous :

![screen_shot_2018-09-17at94033pm](assets/screen_shot_2018-09-17at94033pm.png)

Dans AEM, les groupes d’utilisateurs synchronisés à partir de l’IMS peuvent être ajoutés en tant que membres aux groupes locaux existants, par exemple aux utilisateurs de la gestion des ressources numériques.

![screen_shot_2018-09-17at95804pm](assets/screen_shot_2018-09-17at95804pm.png)

Comme illustré ci-dessous, le groupe *AEM-GRP_008* hérite des autorisations et droits des utilisateurs DAM. C’est un moyen efficace de gérer des autorisations pour les groupes synchronisés. Il est généralement utilisé dans les méthodes d’authentification par LDAP.

![screen_shot_2018-09-17at110505pm](assets/screen_shot_2018-09-17at110505pm.png)
