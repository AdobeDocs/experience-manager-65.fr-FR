---
title: Authentification Adobe IMS et [!DNL Admin Console] Prise en charge d’Adobe Experience Manager Managed Services
description: Découvrez comment utiliser le [!DNL Admin Console] dans Adobe Experience Manager.
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
exl-id: 95eae97c-01c2-4f5c-8068-f504eab7c49e
feature: Security
source-git-commit: 260f71acd330167572d817fdf145a018b09cbc65
workflow-type: tm+mt
source-wordcount: '1669'
ht-degree: 62%

---

# Authentification Adobe IMS et prise en charge par l’[!DNL Admin Console] d’AEM Managed Services {#adobe-ims-authentication-and-admin-console-support-for-aem-managed-services}

>[!NOTE]
>
>Cette fonctionnalité est disponible uniquement pour les clients Adobe Managed Services.

>[!NOTE]
>
>Adobe Experience Manager (AEM) ne prend actuellement pas en charge l’affectation de groupes à des profils. Les utilisateurs doivent être ajoutés individuellement.

## Présentation {#introduction}

AEM 6.4.3.0 introduit la prise en charge par l’[!DNL Admin Console] de l’authentification aux instances AEM et basées sur Adobe IMS (système de gestion d’identité) pour les clients **AEM Managed Services**.

L’intégration d’AEM à l’[!DNL Admin Console] permettra aux clients AEM Managed Services de gérer tous les utilisateurs d’Experience Cloud dans une seule console. Les utilisateurs peuvent être affectés à des profils de produit associés à des instances AEM, ce qui leur permet de se connecter à une instance spécifique.

## Principales caractéristiques {#key-highlights}

* AEM prise en charge de l’authentification IMS est réservée aux auteurs, administrateurs ou développeurs AEM, et non aux utilisateurs finaux externes du site client, tels que les visiteurs du site
* L’[!DNL Admin Console] représentera les clients AEM Managed Services comme des organisations IMS, et leurs instances comme des contextes de produit. Le système client et les responsables de l’administration des produits pourront gérer l’accès aux instances
* AEM Managed Services synchronisera les topologies client à l’aide de l’[!DNL Admin Console]. Chaque instance disposera d’une instance de contexte de produit AEM Managed Services dans l’[!DNL Admin Console].
* Les profils de produit dans l’[!DNL Admin Console] détermineront à quelles instances un utilisateur peut accéder.
* L’authentification fédérée à l’aide des propres fournisseurs d’identités compatibles SAML 2 des clients est prise en charge.
* Seuls les Enterprise ID ou les Federated ID (pour l’authentification unique du client) sont pris en charge, et non les ID d’Adobe personnels.
* [!DNL User Management] (dans l’[!DNL Admin Console] Adobe) sera toujours contrôlée par les responsables de l’administration du client.

## Architecture {#architecture}

L’authentification IMS fonctionne en utilisant le protocole OAuth entre AEM et le point d’entrée Adobe IMS. Une fois qu’un utilisateur a été ajouté à IMS et possède une identité Adobe, il peut se connecter aux instances AEM Managed Services à l’aide des informations d’identification IMS.

Le flux de connexion de l’utilisateur est illustré ci-dessous. L’utilisateur sera redirigé vers IMS et éventuellement vers le fournisseur d’identité du client pour la validation SSO, puis redirigé vers AEM.

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
1. L’administrateur système revendique le domaine pour confirmer la propriété du domaine (dans cet exemple acme.com)
1. L’administrateur système configure les répertoires utilisateur
1. Le responsable d’administration système configure le fournisseur d’identité (IDP) dans l’[!DNL Admin Console] pour la configuration SSO.
1. L’administrateur AEM gère les groupes locaux, les autorisations et les privilèges, comme d’habitude. Consultez la section Synchronisation des utilisateurs et des groupes

>[!NOTE]
>
>Pour plus d’informations sur les bases de la gestion des identités dans Adobe, y compris sur la configuration du fournisseur d’identité, consultez l’article présenté [sur cette page.](https://helpx.adobe.com/fr/enterprise/using/set-up-identity.html)
>
>Pour plus d’informations sur l’administration des Grands comptes et sur l’[!DNL Admin Console], consultez l’article présenté [sur cette page](https://helpx.adobe.com/fr/enterprise/managing/user-guide.html).

### Intégration d’utilisateurs à l’[!DNL Admin Console] {#onboarding-users-to-the-admin-console}

Il existe trois méthodes d’intégration en fonction de la taille de l’organisation et de ses préférences :

1. Création manuelle d’utilisateurs et de groupes dans [!DNL Admin Console]
1. Chargement d’un fichier CSV avec des utilisateurs
1. Synchroniser les utilisateurs et les groupes à partir de l’annuaire Principal d’entreprise du client.

#### Ajout manuel à l’aide de l’interface utilisateur de l’[!DNL Admin Console] {#manual-addition-through-admin-console-ui}

Les utilisateurs et les groupes peuvent être créés manuellement dans l’interface utilisateur de l’[!DNL Admin Console]. Cette méthode peut être utilisée s’il n’y a pas beaucoup d’utilisateurs à gérer. Par exemple, moins de 50 utilisateurs AEM.

Les utilisateurs peuvent également être créés manuellement si le client utilise déjà cette méthode pour administrer d’autres produits Adobe tels que des applications Adobe Analytics, Adobe Target ou Adobe Creative Cloud.

![image2018-9-23_20-39-9](assets/image2018-9-23_20-39-9.png)

#### Chargement du fichier dans l’interface utilisateur [!DNL Admin Console] {#file-upload-in-the-admin-console-ui}

Pour gérer facilement la création d’utilisateurs, un fichier CSV peut être chargé pour permettre l’ajout en bloc des utilisateurs :

![image2018-9-23_18-59-57](assets/image2018-9-23_18-59-57.png)

#### Outil de synchronisation des utilisateurs {#user-sync-tool}

L’outil de synchronisation des utilisateurs (UST, User Sync Tool) permet aux clients d’entreprise de créer ou de gérer des utilisateurs d’Adobe qui utilisent Principale Directory ou d’autres services d’annuaire OpenLDAP testés. Les utilisateurs cibles sont les administrateurs d’identité informatique (Enterprise Directory et administrateurs système) qui pourront installer et configurer l’outil. L’outil open source est personnalisable de sorte que les clients puissent demander à un développeur de le modifier en fonction de leurs besoins spécifiques.

Lorsque la synchronisation des utilisateurs s’exécute, elle récupère une liste d’utilisateurs du Principal Directory de l’entreprise (ou de toute autre source de données compatible) et la compare à la liste des utilisateurs dans la variable [!DNL Admin Console]. Il appelle ensuite l’Adobe [!DNL User Management] pour que la variable [!DNL Admin Console] est synchronisé avec le répertoire de l’organisation. Le flux des modifications est entièrement unidirectionnel; les modifications apportées dans la variable [!DNL Admin Console] ne sont pas poussés vers le répertoire .

L’outil permet à l’administrateur système de mapper les groupes d’utilisateurs dans l’annuaire du client avec la configuration de produit et les groupes d’utilisateurs dans le [!DNL Admin Console], la nouvelle version de l’outil de contrôle permet également la création dynamique de groupes d’utilisateurs dans le [!DNL Admin Console].

Pour configurer la synchronisation des utilisateurs, l’organisation doit créer un ensemble d’informations d’identification de la même manière qu’avec l’[[!DNL User Management] API](https://www.adobe.io/apis/cloudplatform/usermanagement/docs/setup.html).

![image2018-9-23_13-36-56](assets/image2018-9-23_13-36-56.png)

La synchronisation des utilisateurs est distribuée via le référentiel Adobe Github à cet emplacement :

[https://github.com/adobe-apiplatform/user-sync.py/releases/latest](https://github.com/adobe-apiplatform/user-sync.py/releases/latest)

Notez qu’une version préliminaire 2.4RC1 avec prise en charge de création de groupe dynamique est disponible à l’adresse suivante : [https://github.com/adobe-apiplatform/user-sync.py/releases/tag/v2.4rc1](https://github.com/adobe-apiplatform/user-sync.py/releases/tag/v2.4rc1).

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
>La documentation relative à la console Adobe I/O est disponible [ici](https://developer.adobe.com/developer-console/docs/guides/).
>
>
>Le fonctionnement de l’API [!DNL User Management] utilisée par l’outil de synchronisation des utilisateurs est abordé en détail [ici](https://adobe-apiplatform.github.io/umapi-documentation/en/).

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

Un profil de produit est associé à chaque instance de contexte du produit. Ce profil de produit est utilisé pour affecter l’accès aux utilisateurs.

![image2018-9-18_7-48-50](assets/image2018-9-18_7-48-50.png)

Tous les utilisateurs ajoutés sous ce profil de produit pourront se connecter à cette instance, comme illustré dans l’exemple ci-dessous :

![screen_shot_2018-09-17at105623pm](assets/screen_shot_2018-09-17at105623pm.png)

### Connexion à AEM {#logging-into-aem}

#### Connexion de l’administrateur local {#local-admin-login}

AEM peut continuer à prendre en charge les connexions locales pour les utilisateurs administrateurs, car l’écran de connexion dispose d’une option de connexion locale :

![screen_shot_2018-09-18at121056am](assets/screen_shot_2018-09-18at121056am.png)

#### Connexion via IMS {#ims-based-login}

Pour les autres cas, la connexion via IMS peut être utilisée une fois qu’IMS est configuré sur l’instance. L’utilisateur clique d’abord sur **Connexion avec Adobe** comme illustré ci-dessous :

![image2018-9-18_0-10-32](assets/image2018-9-18_0-10-32.png)

Il est alors redirigé vers l’écran de connexion IMS et saisit ses informations d’identification :

![screen_shot_2018-09-17at115629pm](assets/screen_shot_2018-09-17at115629pm.png)

Si un fournisseur d’identité fédéré est configuré lors de la configuration initiale d’[!DNL Admin Console], l’utilisateur est redirigé vers le fournisseur d’identité client pour SSO. 

Le fournisseur d’identité est Okta dans l’exemple ci-dessous :

![screen_shot_2018-09-17at115734pm](assets/screen_shot_2018-09-17at115734pm.png)

Une fois l’authentification terminée, l’utilisateur est redirigé vers AEM et connecté :

![screen_shot_2018-09-18at120124am](assets/screen_shot_2018-09-18at120124am.png)

### Migration d’utilisateurs existants {#migrating-existing-users}

Pour les instances d’AEM existantes qui utilisent une autre méthode d’authentification et qui sont maintenant migrées vers IMS, une étape de migration doit être effectuée.

Les utilisateurs existants dans le référentiel AEM (origine locale via LDAP ou SAML) peuvent être migrés pour pointer vers l’IMS en tant que fournisseur d’identité à l’aide de l’utilitaire de migration d’utilisateur.

Cet utilitaire sera exécuté par votre équipe AMS dans le cadre de la mise en service IMS.

### Gestion des autorisations et des listes de contrôle d’accès dans AEM {#managing-permissions-and-acls-in-aem}

Le contrôle d’accès et les autorisations continueront à être gérés dans AEM. Pour ce faire, vous pouvez séparer les groupes d’utilisateurs issus d’IMS (par exemple, AEM-GRP-008 dans l’exemple ci-dessous) et les groupes locaux dans lesquels les autorisations et le contrôle d’accès sont définis. Les groupes d’utilisateurs synchronisés à partir de l’IMS peuvent être attribués aux groupes locaux et hériter des autorisations.

Dans l’exemple ci-dessous, nous ajoutons des groupes synchronisés au groupe local *Dam_Users*.

Dans ce cas, un utilisateur a également été attribué à plusieurs groupes dans l’[!DNL Admin Console]. (Les utilisateurs et les groupes peuvent être synchronisés via LDAP à l’aide de l’outil de synchronisation des utilisateurs ou créés localement. Voir **Intégration d’utilisateurs à[!DNL Admin Console]** précédemment).

>[!NOTE]
>
>Les groupes d’utilisateurs ne sont synchronisés que lorsque les utilisateurs se connectent à l’instance.

![screen_shot_2018-09-17at94207pm](assets/screen_shot_2018-09-17at94207pm.png)

L’utilisateur fait partie des groupes suivants dans IMS :

![screen_shot_2018-09-17at94237pm](assets/screen_shot_2018-09-17at94237pm.png)

Lorsque l’utilisateur se connecte, ses adhésions de groupes sont synchronisées, comme illustré ci-dessous :

![screen_shot_2018-09-17at94033pm](assets/screen_shot_2018-09-17at94033pm.png)

Dans AEM, les groupes d’utilisateurs synchronisés à partir d’IMS peuvent être ajoutés en tant que membres aux groupes locaux existants, par exemple les utilisateurs DAM.

![screen_shot_2018-09-17at95804pm](assets/screen_shot_2018-09-17at95804pm.png)

Comme illustré ci-dessous, le groupe *AEM-GRP_008* hérite des autorisations et droits des utilisateurs DAM. Il s’agit d’un moyen efficace de gérer les autorisations pour les groupes synchronisés. Il est généralement utilisé dans les méthodes d’authentification LDAP.

![screen_shot_2018-09-17at110505pm](assets/screen_shot_2018-09-17at110505pm.png)
