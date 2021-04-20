---
title: Authentification IMS Adobe et  [!DNL Admin Console] Prise en charge de Managed Services
seo-title: Authentification IMS Adobe et  [!DNL Admin Console] Prise en charge de Managed Services
description: Découvrez comment utiliser le  [!DNL Admin Console] dans AEM.
seo-description: Découvrez comment utiliser le  [!DNL Admin Console] dans AEM.
uuid: 3f5b32c7-cf62-41a4-be34-3f71bbf224eb
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: f6112dea-a1eb-4fd6-84fb-f098476deab7
exl-id: 95eae97c-01c2-4f5c-8068-f504eab7c49e
feature: Security
translation-type: tm+mt
source-git-commit: 9134130f349c6c7a06ad9658a87f78a86b7dbf9c
workflow-type: tm+mt
source-wordcount: '1692'
ht-degree: 62%

---

# Adobe de l&#39;authentification IMS et [!DNL Admin Console] prise en charge de l&#39;AEM Managed Services {#adobe-ims-authentication-and-admin-console-support-for-aem-managed-services}

>[!NOTE]
>
>Notez que cette fonctionnalité n’est disponible que pour les clients Adobe Managed Services.

## Présentation {#introduction}

AEM 6.4.3.0 introduit la prise en charge [!DNL Admin Console] des instances AEM et de l’Adobe d’authentification basée sur le système IMS(Identity Management System) pour les **clients AEM Managed Services**.

L&#39;intégration AEM à [!DNL Admin Console] permet aux clients d&#39;AEM Managed Services de gérer tous les utilisateurs Experience Cloud dans une seule console. Les utilisateurs et les groupes peuvent être affectés à des profils de produits associés à des instances AEM, ce qui leur permet de se connecter à une instance spécifique.

## Principales caractéristiques {#key-highlights}

* La prise en charge de l’authentification IMS d’AEM est réservée aux auteurs, administrateurs ou développeurs AEM et non aux utilisateurs finaux externes de sites clients comme les visiteurs de site
* [!DNL Admin Console] représentera AEM clients Managed Services en tant qu’organisations IMS et leurs instances en tant que Contextes de produits. Le système client et les administrateurs de produits pourront gérer l’accès aux instances
* AEM Managed Services synchronisera les topologies du client avec le [!DNL Admin Console]. Il y aura une instance du contexte de produit Managed Services AEM par instance dans le [!DNL Admin Console].
* Les Profils de produits dans [!DNL Admin Console] déterminent les instances auxquelles un utilisateur peut accéder.
* L’authentification fédérée à l’aide des propres fournisseurs d’identité des clients conformes SAML 2 est prise en charge
* Seuls les ID d’entreprise ou fédérés (pour l’authentification unique du client) sont pris en charge, et non les Adobe ID personnels.
* [!DNL User Management] (dans l’Adobe  [!DNL Admin Console]) continuera d’appartenir aux administrateurs du client.

## Architecture {#architecture}

L’authentification IMS fonctionne en utilisant le protocole OAuth entre AEM et le point de terminaison Adobe IMS. Une fois qu’un utilisateur a été ajouté à IMS et possède une identité Adobe, il peut se connecter aux instances AEM Managed Services à l’aide des informations d’identification IMS.

Le flux d’identifiant de connexion utilisateur est indiqué ci-dessous, l’utilisateur sera redirigé vers IMS et éventuellement vers le fournisseur d’identité client pour la validation SSO, puis redirigé vers AEM.

![image2018-9-23_23-55-8](assets/image2018-9-23_23-55-8.png)

## Méthode de configuration {#how-to-set-up}

### Organisation d&#39;intégration à [!DNL Admin Console] {#onboarding-organizations-to-admin-console}

L&#39;intégration du client à [!DNL Admin Console] est une condition préalable à l&#39;utilisation de l&#39;Adobe IMS pour l&#39;authentification AEM.

Pour commencer, une organisation doit être configurée pour les clients dans Adobe IMS. Les clients Adobe Enterprise sont représentés en tant qu’organisations IMS dans [Adobe [!DNL Admin Console]](https://helpx.adobe.com/fr/enterprise/using/admin-console.html).

AEM clients Managed Services doivent déjà disposer d&#39;une organisation configurée et, dans le cadre de l&#39;approvisionnement IMS, les instances de client seront mises à disposition dans le [!DNL Admin Console] pour la gestion des droits d&#39;utilisateur et de l&#39;accès.

L’authentification des utilisateurs par IMS sera un travail commun à AMS et les clients, chacun devant mener à bien ses workflows.

Une fois qu’un client est défini en tant qu’organisation IMS et qu’AMS a attribué ce client pour l’IMS, voici, en résumé, les workflows de la configuration nécessaires :

![image2018-9-23_23-33-25](assets/image2018-9-23_23-33-25.png)

1. L&#39;administrateur système désigné reçoit une invitation à se connecter au [!DNL Admin Console]
1. L’administrateur système désigne le domaine pour confirmer la propriété du nom de domaine (dans cet exemple acme.com)
1. L’administrateur système configure les répertoires utilisateur
1. L’administrateur système configure le fournisseur d’identité (IDP) dans [!DNL Admin Console] pour la configuration de l’authentification unique.
1. L’administrateur AEM gère les groupes locaux, les autorisations et les droits comme d’habitude. Voir Synchronisation des utilisateurs et des groupes

>[!NOTE]
>
>Pour plus d’informations sur les bases de la gestion des identités dans Adobe, y compris sur la configuration de fournisseur d’identité, voir l’article présenté [sur cette page.](https://helpx.adobe.com/fr/enterprise/using/set-up-identity.html)
>
>Pour plus d&#39;informations sur l&#39;administration d&#39;entreprise et [!DNL Admin Console] consultez l&#39;article [cette page](https://helpx.adobe.com/fr/enterprise/managing/user-guide.html).

### Intégration d’utilisateurs à [!DNL Admin Console] {#onboarding-users-to-the-admin-console}

Il existe trois méthodes d’intégration des utilisateurs en fonction de la taille du client et de ses préférences :

1. Créer manuellement des utilisateurs et des groupes dans [!DNL Admin Console]
1. Téléchargement d’un fichier CSV avec des utilisateurs
1. Synchronisation des utilisateurs et des groupes depuis le répertoire Active Directory d’entreprise du client.

#### Ajout manuel via [!DNL Admin Console] interface utilisateur {#manual-addition-through-admin-console-ui}

Les utilisateurs et les groupes peuvent être créés manuellement dans l&#39;interface utilisateur [!DNL Admin Console]. Cette méthode peut être utilisée s’il y a un nombre réduit d’utilisateurs à gérer. Par exemple, moins de 50 utilisateurs d’AEM.

Les utilisateurs peuvent aussi être créés manuellement si le client utilise déjà cette méthode pour administrer d’autres produits Adobe comme Analytics, Target ou des applications Creative Cloud.

![image2018-9-23_20-39-9](assets/image2018-9-23_20-39-9.png)

#### Téléchargement de fichier dans l&#39;interface utilisateur [!DNL Admin Console] {#file-upload-in-the-admin-console-ui}

Pour gérer facilement la création d’utilisateurs, un fichier CSV peut être téléchargé pour permettre l’ajout groupé des utilisateurs :

![image2018-9-23_18-59-57](assets/image2018-9-23_18-59-57.png)

#### Outil de synchronisation des utilisateurs {#user-sync-tool}

L’outil de synchronisation des utilisateurs permet aux clients d’entreprise de créer ou de gérer des utilisateurs Adobe utilisant Active Directory ou d’autres services testés de répertoires OpenLDAP. Les utilisateurs cibles sont les administrateurs d’identité informatique (Enterprise Directory et administrateurs système) qui pourront installer et configurer l’outil. Cet outil en open source est personnalisable, de telle sorte que les clients peuvent le faire modifier par un développeur en fonction de leurs besoins spécifiques.

Lorsque User Sync s’exécute, il récupère une liste d’utilisateurs du Principal Directory de l’entreprise (ou de toute autre source de données compatible) et la compare à la liste d’utilisateurs dans [!DNL Admin Console]. Il appelle ensuite l’API d’Adobe [!DNL User Management] afin que [!DNL Admin Console] soit synchronisé avec l’annuaire de l’organisation. Le flux de changement est entièrement à sens unique ; les modifications effectuées dans [!DNL Admin Console] ne sont pas répercutées dans le répertoire.

L’outil permet à l’administrateur système de mapper les groupes d’utilisateurs du répertoire du client avec la configuration du produit et les groupes d’utilisateurs dans [!DNL Admin Console]. La nouvelle version UST permet également la création dynamique de groupes d’utilisateurs dans le [!DNL Admin Console].

Pour configurer la synchronisation des utilisateurs, l’organisation doit créer un ensemble d’informations d’identification de la même manière qu’avec l’[[!DNL User Management] API ](https://www.adobe.io/apis/cloudplatform/usermanagement/docs/setup.html).

![image2018-9-23_13-36-56](assets/image2018-9-23_13-36-56.png)

La synchronisation des utilisateurs est distribuée via le référentiel Adobe Github à cet emplacement :

[https://github.com/adobe-apiplatform/user-sync.py/releases/latest](https://github.com/adobe-apiplatform/user-sync.py/releases/latest)

Notez qu’une version préliminaire 2.4RC1 est disponible avec la prise en charge de la création de groupe dynamique et se trouve ici : [https://github.com/adobe-apiplatform/user-sync.py/releases/tag/v2.4rc1](https://github.com/adobe-apiplatform/user-sync.py/releases/tag/v2.4rc1)

Les principales fonctionnalités de cette version sont la possibilité de mapper dynamiquement de nouveaux groupes LDAP pour l’adhésion des utilisateurs dans [!DNL Admin Console], ainsi que la création de groupes d’utilisateurs dynamiques.

Vous trouverez plus d’informations sur les nouvelles fonctionnalités du groupe ici :

[https://github.com/adobe-apiplatform/user-sync.py/blob/v2/docs/en/user-manual/advanced_configuration](https://github.com/adobe-apiplatform/user-sync.py/blob/v2/docs/en/user-manual/advanced_configuration.md#additional-group-options)

>[!NOTE]
>
>Pour plus d’informations sur l’outil de synchronisation des utilisateurs, consultez la [page de documentation](https://adobe-apiplatform.github.io/user-sync.py/en/).
>
>
>L’outil de synchronisation des utilisateurs doit s’enregistrer en tant qu’UMAPI client d’Adobe I/O en suivant la procédure décrite [ici](https://adobe-apiplatform.github.io/umapi-documentation/en/UM_Authentication.html).
>
>La documentation relative à la console Adobe I/O est disponible [ici](https://www.adobe.io/apis/cloudplatform/console.html).
>
>
>L&#39;API [!DNL User Management] utilisée par l&#39;outil de synchronisation des utilisateurs est traitée à cet [emplacement](https://www.adobe.io/apis/cloudplatform/umapi-new.html).

>[!NOTE]
>
>La configuration IMS d’AEM sera gérée par l’équipe Adobe Managed Services. Cependant, l’administrateur du client peut la modifier en fonction de ses besoins (par exemple, pour gérer l’appartenance automatique des groupes ou le mappage de groupes). Le client IMS sera également enregistré par votre équipe Managed Services.

## Utilisation {#how-to-use}

### Gestion des produits et accès utilisateur dans [!DNL Admin Console] {#managing-products-and-user-access-in-admin-console}

Lorsque l’administrateur de produit du client se connecte à [!DNL Admin Console], plusieurs instances du contexte de produit Managed Services AEM s’affichent, comme illustré ci-dessous :

![screen_shot_2018-09-17at105804pm](assets/screen_shot_2018-09-17at105804pm.png)

Dans cet exemple, l’organisation *AEM-MS-Onboard* comporte 32 instances couvrant différents environnements et topologies tels que Intermédiaire, Production, etc.

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

Pour les autres utilisateurs, la connexion via IMS peut être utilisée une fois qu’IMS est configuré sur l’instance. L’utilisateur doit d’abord cliquer sur le bouton **Se connecter avec Adobe** comme illustré ci-dessous :

![image2018-9-18_0-10-32](assets/image2018-9-18_0-10-32.png)

Il est alors redirigé vers l’écran de connexion IMS et saisit ses informations d’identification :

![screen_shot_2018-09-17at115629pm](assets/screen_shot_2018-09-17at115629pm.png)

Si un fournisseur d’identité fédérée est configuré lors de la configuration initiale de [!DNL Admin Console], l’utilisateur sera redirigé vers le fournisseur d’identité du client pour l’authentification unique.

Le fournisseur d’identité est Okta dans l’exemple ci-dessous :

![screen_shot_2018-09-17at115734pm](assets/screen_shot_2018-09-17at115734pm.png)

Une fois l’authentification terminée, l’utilisateur est redirigé vers AEM et connecté :

![screen_shot_2018-09-18at120124am](assets/screen_shot_2018-09-18at120124am.png)

### Migration d’utilisateurs existants {#migrating-existing-users}

Pour les instances AEM existantes qui utilisent une autre méthode d’authentification et qui sont désormais migrées vers IMS, une étape de migration est nécessaire.

Les utilisateurs existants dans le référentiel AEM (provenant localement, via LDAP ou SAML) peuvent être migrés pour pointer vers IMS en tant que IDP à l’aide de l’utilitaire de migration d’utilisateur.

Cet utilitaire sera exécuté par votre équipe AMS dans le cadre de la mise en service de l’IMS.

### Gestion des autorisations et des listes de contrôle d’accès dans AEM {#managing-permissions-and-acls-in-aem}

Le contrôle d&#39;accès et les autorisations continueront d’être gérés en AEM, ce qui peut se faire en séparant les groupes d’utilisateurs des IMS (par exemple AEM-GRP-008 dans l’exemple ci-dessous) et des groupes locaux où les autorisations et le contrôle d&#39;accès sont définis. Les groupes d’utilisateurs synchronisés à partir de l’IMS peuvent être attribués aux groupes locaux et hériter des autorisations.

Dans l’exemple ci-dessous, nous ajoutons des groupes synchronisés au groupe local *Dam_Users* comme exemple.

Ici, un utilisateur a également été affecté à quelques groupes dans le [!DNL Admin Console]. ( Notez que les utilisateurs et les groupes peuvent être synchronisés à partir du protocole LDAP à l&#39;aide de l&#39;outil de synchronisation des utilisateurs ou créés localement, consultez la section **Intégration d&#39;utilisateurs à[!DNL Admin Console]** ci-dessus).

>[!NOTE]
>
>Les groupes d’utilisateurs ne sont synchronisés que lorsque les utilisateurs se connectent à l’instance.

![screen_shot_2018-09-17at94207pm](assets/screen_shot_2018-09-17at94207pm.png)

L’utilisateur fait partie des groupes suivants dans IMS :

![screen_shot_2018-09-17at94237pm](assets/screen_shot_2018-09-17at94237pm.png)

Lorsque l’utilisateur se connecte, ses adhésions de groupes sont synchronisées, comme illustré ci-dessous :

![screen_shot_2018-09-17at94033pm](assets/screen_shot_2018-09-17at94033pm.png)

Dans AEM, les groupes d’utilisateurs synchronisés à partir de l’IMS peuvent être ajoutés en tant que membres aux groupes locaux existants, par exemple aux utilisateurs DAM.

![screen_shot_2018-09-17at95804pm](assets/screen_shot_2018-09-17at95804pm.png)

Comme illustré ci-dessous, le groupe *AEM-GRP_008* hérite des autorisations et droits des utilisateurs DAM. C’est un moyen efficace de gérer des autorisations pour les groupes synchronisés. Il est généralement utilisé dans les méthodes d’authentification par LDAP.

![screen_shot_2018-09-17at110505pm](assets/screen_shot_2018-09-17at110505pm.png)
