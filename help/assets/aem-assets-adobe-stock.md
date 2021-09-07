---
title: Gestion des  [!DNL Adobe Stock] ressources
description: Rechercher, récupérer, gérer les licences et gérer les ressources [!DNL Adobe Stock] dans [!DNL Adobe Experience Manager]. Utiliser les ressources sous licence comme toute autre ressource numérique.
contentOwner: Vishabh Gupta
feature: Search, Adobe Stock
role: User, Admin
exl-id: 8ec597df-bb64-4768-bf9c-e8cca4fea25b
source-git-commit: 6d1073003c1b78be848652be0b387889eedbc193
workflow-type: tm+mt
source-wordcount: '2443'
ht-degree: 41%

---

# Utilisation des ressources [!DNL Adobe Stock] dans [!DNL Adobe Experience Manager Assets] {#use-adobe-stock-assets-in-aem-assets}

<!-- old content

[!DNL Experience Manager Assets] provides users the ability to search, preview, save, and license [!DNL Adobe Stock] assets directly from [!DNL Experience Manager]. 

Organizations can integrate their [!DNL Adobe Stock] enterprise plan with [!DNL Experience Manager Assets] to ensure that licensed assets are broadly available for their creative and marketing projects, with the powerful asset management capabilities of [!DNL Experience Manager].

[!DNL Adobe Stock] service provides designers and businesses with access to millions of high-quality, curated, royalty-free photos, vectors, illustrations, videos, templates, and 3D assets for all their creative projects. [!DNL Experience Manager] users are able to quickly find, preview, and license [!DNL Adobe Stock] assets that are saved in [!DNL Experience Manager], without leaving the [!DNL Experience Manager] interface.
-->

<!-- New overview content
-->

Le service [!DNL Adobe Stock] permet aux créateurs et aux entreprises d’accéder à des millions de photos, de vecteurs, d’illustrations, de vidéos, de modèles et de ressources 3D organisés, de haute qualité et libres de droits pour tous leurs projets de création. 

[!DNL Adobe Stock] pour l’offre d’entreprise, inclut par défaut des droits de partage à l’échelle de l’entreprise. Une fois qu’une ressource a reçu une licence d’un utilisateur de votre entreprise, d’autres utilisateurs de votre entreprise peuvent l’identifier, la télécharger et l’utiliser sans avoir à la renouveler. Une fois qu’une ressource a reçu une licence de votre entreprise, le droit de l’utiliser est perpétuel.

Les entreprises peuvent intégrer leur formule d’abonnement pour entreprise [!DNL Adobe Stock] à [!DNL Experience Manager Assets] pour s’assurer que les ressources sous licence sont largement disponibles pour leurs projets de création et de marketing, avec les puissantes fonctionnalités de gestion de ressources de [!DNL Experience Manager]. [!DNL Experience Manager] Les utilisateurs peuvent rapidement rechercher, prévisualiser et acquérir sous licence des ressources Adobe Stock enregistrées dans  [!DNL Experience Manager], sans quitter l’ [!DNL Experience Manager] interface.

<!-- Old content
## Prerequisites {#prerequisites}

The integration requires an [enterprise [!DNL Adobe Stock] plan](https://stockenterprise.adobe.com/).
-->

## Intégration d’[!DNL Experience Manager] et [!DNL Adobe Stock] {#integrate-aem-and-adobe-stock}

[!DNL Experience Manager Assets] permet aux utilisateurs de rechercher, de prévisualiser, d’enregistrer et d’acquérir sous licence  [!DNL Adobe Stock] des ressources directement à partir de  [!DNL Experience Manager].

**Prérequis**

L’intégration nécessite :
* Un [plan  [!DNL Adobe Stock] entreprise](https://stockenterprise.adobe.com/)
* Un utilisateur disposant d’autorisations en Admin Console sur le profil de produit Stock par défaut
* Un utilisateur disposant d’autorisations sur le profil Accès des développeurs pour la création d’une intégration dans Adobe Developer Console

un plan d&#39;entreprise [!DNL Adobe Stock],
* Fournit des droits sur les produits pour [!DNL Adobe Stock] (stocks connectés à Experience Manager)
* Crédits achetés dans le [!DNL Adobe Admin Console] pour les droits sur vos stocks
* Active l’authentification du compte de service (JWT) dans [!DNL Adobe Developer Console] pour les droits de stockage
* Permet la gestion globale des crédits et des licences à partir de [!DNL Adobe Admin Console]

Dans le droit, un profil de produit par défaut pour [!DNL Adobe Stock] existe dans [!DNL Admin Console]. Plusieurs profils peuvent être créés et ils déterminent qui peut acquérir des ressources Stock sous licence. Un utilisateur ayant accès directement au profil de produit peut accéder à [https://stock.adobe.com/](https://stock.adobe.com/) et acquérir sous licence des ressources Stock. En revanche, il existe une autre méthode d’utilisation de l’accès développeur pour créer l’intégration (API) afin d’authentifier la communication entre [!DNL Experience Manager] et [!DNL Adobe Stock].

>[!NOTE]
>
>L’authentification du compte de service Stock (JWT) est fournie avec les droits Enterprise Stock.
>
>L’intégration ne prend pas en charge l’authentification Oauth pour les droits d’entreprise Stock.

<!-- old content
To allow communication between [!DNL Experience Manager] and [!DNL Adobe Stock], create an IMS configuration and an [!DNL Adobe Stock] configuration in [!DNL Experience Manager].

>[!NOTE]
>
>Only [!DNL Experience Manager] administrators and [!DNL Admin Console] administrators for an organization can perform the integration as it requires administrator privileges.
-->

## Étapes d’intégration de [!DNL Experience Manager] et [!DNL Adobe Stock] {#integration-steps}

Pour intégrer [!DNL Experience Manager] et [!DNL Adobe Stock], effectuez les étapes suivantes dans la séquence répertoriée :

1. [Obtention d’un certificat public](#public-certificate)

   Dans [!DNL Experience Manager], créez un compte IMS et générez un certificat public (clé publique).

1. [Création d’une connexion au compte de service (JWT)](#createnewintegration)

   Dans [!DNL Adobe Developer Console], créez un projet pour votre organisation [!DNL Adobe Stock]. Dans le projet, configurez une API à l’aide de la clé publique pour créer une connexion au compte de service (JWT). Obtenez les informations d’identification du compte de service et les informations de charge utile JWT.

1. [Configuration du compte IMS](#create-ims-account-configuration)

   Dans [!DNL Experience Manager], configurez le compte IMS à l’aide des informations d’identification du compte de service et de la charge utile JWT.

1. [Configuration du service cloud](#configure-the-cloud-service)

   Dans [!DNL Experience Manager], configurez un service cloud [!DNL Adobe Stock] à l’aide du compte IMS.


### Création d’une configuration IMS {#create-an-ims-configuration}

La configuration IMS authentifie votre instance d’auteur [!DNL Experience Manager Assets] avec le droit [!DNL Adobe Stock].

La configuration IMS comprend deux étapes :

* [Obtention d’un certificat public](#public-certificate)
* [Configuration du compte IMS](#create-ims-account-configuration)

### Obtention d’un certificat public {#public-certificate}

La clé publique (certificat) authentifie votre profil de produit dans Adobe Developer Console.

1. Connectez-vous à votre instance d’auteur [!DNL Experience Manager Assets]. L’URL par défaut est `http://localhost:4502/aem/start.html`.

1. Dans le panneau **[!UICONTROL Outils]**, accédez à **[!UICONTROL Sécurité]** > **[!UICONTROL Configurations d’Adobe IMS]**.

1. Dans la page Configurations d’Adobe IMS, cliquez sur **[!UICONTROL Créer]**. La page **[!UICONTROL Configuration du compte technique Adobe IMS]** s’affiche.

1. Dans l’onglet **[!UICONTROL Certificat]**, sélectionnez **[!UICONTROL Adobe Stock]** dans la liste déroulante **[!UICONTROL Solution cloud]**.

1. Vous pouvez créer un certificat ou réutiliser un certificat existant pour la configuration.

   Pour créer un certificat, cochez la case **[!UICONTROL Créer un certificat]** et indiquez un **alias** pour la clé publique. L’alias constitue le nom de la clé publique.

1. Cliquez sur **[!UICONTROL Créer un certificat]**. Cliquez sur **[!UICONTROL OK]** pour générer la clé publique.

1. Cliquez sur l’icône **[!UICONTROL Télécharger la clé publique]** et enregistrez le fichier de clé publique (.crt) sur votre ordinateur. La clé publique est utilisée ultérieurement pour configurer l’API de votre client Brand Portal et générer les informations d’identification de compte de service dans la Developer Console Adobe.

   Cliquez sur **[!UICONTROL Suivant]**.

   ![generate-certificate](assets/stock-integration-ims-account.png)

1. Dans l’onglet **Compte**, un compte Adobe IMS est créé, ce qui nécessite les informations d’identification du compte de service.

   Ouvrez un nouvel onglet et [créez une connexion au compte de service (JWT) dans Adobe Developer Console](#createnewintegration).

### Création d’une connexion au compte de service (JWT) {#createnewintegration}

Dans Adobe Developer Console, les projets et les API sont configurés au niveau de l’organisation. La configuration d’une API crée une connexion au compte de service (JWT). Il existe deux méthodes pour configurer l’API : générer une paire de clés (clés privée et publique) ou télécharger une clé publique. Dans cet exemple, les informations d’identification du compte de service sont générées en chargeant la clé publique.

Pour générer les informations d’identification du compte de service et la charge utile JWT :

1. Connectez-vous à Adobe Developer Console avec les privilèges d’administrateur système. L’URL par défaut est [https://www.adobe.com/go/devs_console_ui](https://www.adobe.com/go/devs_console_ui).


   Assurez-vous d’avoir sélectionné l’organisation IMS appropriée (droits Stock) dans la liste déroulante (organisation).

1. Cliquez sur **[!UICONTROL Create new project]** (Créer un projet). Un projet vierge portant un nom généré par le système est créé pour votre organisation.

   Cliquez sur **[!UICONTROL Modifier le projet]**. Mettez à jour le **[!UICONTROL titre du projet]** et la **[!UICONTROL description]**, puis cliquez sur **[!UICONTROL Enregistrer]**.

1. Dans l’onglet **[!UICONTROL Project overview]** (Aperçu du projet), cliquez sur **[!UICONTROL Add API]** (Ajouter une API).

1. Dans la **[!UICONTROL fenêtre Ajouter une API]**, sélectionnez **[!UICONTROL Adobe Stock]**. Cliquez sur **[!UICONTROL Suivant]**.

1. Dans la fenêtre **[!UICONTROL Configurer l’API]**, sélectionnez l’authentification **[!UICONTROL Compte de service (JWT)]**. Cliquez sur **[!UICONTROL Suivant]**.

   ![create-jwt-credentials](assets/aem-stock-jwt.png)

1. Cliquez sur **[!UICONTROL Télécharger votre clé publique]**. Cliquez sur **[!UICONTROL Sélectionner un fichier]** et téléchargez la clé publique (fichier .crt) que vous avez téléchargé dans la section [Obtention d’un certificat public](#public-certificate) . Cliquez sur **[!UICONTROL Suivant]**.

1. Vérifiez la clé publique et cliquez sur **[!UICONTROL Next]** (Suivant).

1. Sélectionnez le profil de produit **[!UICONTROL Adobe Stock]** par défaut et cliquez sur **[!UICONTROL Enregistrer l’API configurée]**.

1. Une fois l’API configurée, vous êtes redirigé vers sa page d’aperçu. Dans le volet de navigation de gauche, sous **[!UICONTROL Credentials]** (Informations d’identification), cliquez sur **[!UICONTROL Service Account (JWT)]** (Compte de service (JWT)). Ici, vous pouvez afficher les informations d’identification et effectuer des actions telles que générer des jetons JWT, copier les informations d’identification et récupérer le secret client.

1. Dans l’onglet **[!UICONTROL Client Credentials]** (Informations d’identification client), copiez l’**[!UICONTROL ID client]**.

   Cliquez sur **[!UICONTROL Retrieve Client Secret]** (Récupérer le secret client) et copiez le **[!UICONTROL secret client]**.

   ![generate-jwt-credentials](assets/aem-stock-jwt-credential.png)

1. Accédez à l’onglet **[!UICONTROL Generate JWT]** (Générer le jeton JWT) et copiez les informations **[!UICONTROL JWT Payload]** (Charge utile JWT).

Vous pouvez maintenant utiliser l’ID client (clé API), le secret client et la charge utile JWT pour [configurer le compte IMS](#create-ims-account-configuration) dans [!DNL Experience Manager Assets].

### Configuration du compte IMS {#create-ims-account-configuration}

Vous devez disposer des informations d’identification [certificate](#public-certificate) et [du compte de service (JWT)](#createnewintegration) pour configurer le compte IMS.

Pour configurer le compte IMS :

1. Ouvrez la configuration IMS et accédez à l’onglet **[!UICONTROL Compte]**. Vous avez maintenu la page ouverte lors de l’[obtention du certificat public](#public-certificate).

1. Spécifiez un **[!UICONTROL titre]** pour le compte IMS.

   Dans le champ **[!UICONTROL Serveur d’autorisation]**, saisissez l’URL : [https://ims-na1.adobelogin.com/](https://ims-na1.adobelogin.com/).

   Saisissez l’ID client dans le champ **[!UICONTROL Clé API]**, **[!UICONTROL Secret client]** et **[!UICONTROL Charge utile]** (charge utile JWT) que vous avez copié lors de la [création de la connexion au compte de service (JWT)](#createnewintegration).

1. Cliquez sur **[!UICONTROL Créer]**. Une configuration de compte IMS est créée.

   ![configure-ims-account](assets/aem-stock-ims-config.png)

1. Sélectionnez la configuration de compte IMS et cliquez sur **[!UICONTROL Contrôle de l’intégrité]**.

   Cliquez sur **[!UICONTROL Vérifier]** dans la boîte de dialogue. Une fois la configuration réussie, un message s’affiche avec la mention *Jeton récupéré avec succès*.

   ![health-check](assets/aem-stock-healthcheck.png)


### Configuration du service cloud {#configure-the-cloud-service}

Pour configurer le service cloud [!DNL Adobe Stock] :

1. Dans l’interface utilisateur [!DNL Experience Manager], accédez à **[!UICONTROL Outils]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Stock]**.

1. Dans la page [!DNL Adobe Stock Configurations], cliquez sur **[!UICONTROL Créer]**.

1. Spécifiez un **[!UICONTROL titre]** pour la configuration cloud.

   Sélectionnez la configuration IMS créée lors de la [configuration du compte IMS](#create-ims-account-configuration).

   Sélectionnez vos paramètres régionaux dans la liste déroulante.

   ![aem-stock-cloud-config](assets/aem-stock-cloud-config.png)

1. Cliquez sur **[!UICONTROL Enregistrer et fermer]**.

   Votre instance [!DNL Experience Manager Assets] d’auteur est désormais intégrée à [!DNL Adobe Stock]. Vous pouvez créer plusieurs configurations [!DNL Adobe Stock] (par exemple, des configurations basées sur des paramètres régionaux). Vous pouvez désormais accéder aux ressources [!DNL Adobe Stock], les rechercher et les obtenir sous licence depuis l’interface utilisateur de [!DNL Experience Manager].

   ![search-stock-assets](assets/aem-stock-searchstocks.png)

   >[!NOTE]
   >
   >À ce stade de l’intégration, seuls les administrateurs peuvent accéder aux ressources [!DNL Adobe Stock], rechercher des ressources Stock (à l’aide de l’omni-recherche) et acquérir sous licence les ressources [!DNL Adobe Stock].
   >
   >Les administrateurs peuvent ajouter d’autres utilisateurs ou groupes au service cloud [!DNL Adobe Stock] et accorder des autorisations à ces utilisateurs non-administrateurs dans [!DNL Experience Manager] pour accéder à la configuration Stock.

1. Pour ajouter des utilisateurs ou des groupes, sélectionnez la configuration de cloud [!DNL Adobe Stock] et cliquez sur **[!UICONTROL Propriétés]**.

1. Recherchez pour ajouter les utilisateurs ou les groupes auxquels vous avez attribué des autorisations d’accès à la configuration Adobe Stock. Voir [attribuer des autorisations au groupe d’utilisateurs](#assign-permissions-to-group).


## Attribution d’autorisations à un groupe d’utilisateurs {#assign-permissions-to-group}

Les administrateurs peuvent créer des groupes d’utilisateurs et accorder des autorisations à certains utilisateurs ou groupes pour accéder au service cloud [!DNL Adobe Stock].

Voici les autorisations requises pour qu’un utilisateur puisse rechercher et acquérir sous licence des ressources Adobe Stock :

* Configurez le chemin d’accès : `/conf/global/settings/stock`
* Autorisations: `jcr:read`
* Type d’autorisation: `Allow`

Vous pouvez créer un groupe d’utilisateurs ou attribuer des autorisations à un groupe d’utilisateurs existant. Les autorisations peuvent être attribuées à partir de l’interface [!DNL Experience Manager Assets] ou de la console [!DNL User Admin].

**Pour permettre l’accès à un groupe d’utilisateurs à partir de  [!DNL Experience Manager]:**

1. Dans l’interface utilisateur [!DNL Experience Manager], accédez à **[!UICONTROL Outils]** > **[!UICONTROL Sécurité]** > **[!UICONTROL Groupes]**. Créez un groupe d’utilisateurs pour [!DNL Adobe Stock].

1. Accédez à **[!UICONTROL Outils]** > **[!UICONTROL Sécurité]** > **[!UICONTROL Autorisations]**.

1. Recherchez le groupe d’utilisateurs dans le panneau de gauche et ajoutez la nouvelle **[!UICONTROL Entrée de contrôle d’accès (ACE)]** pour Adobe Stock.

   * Configurez le chemin d’accès : `/conf/global/settings/stock`
   * Autorisations: `jcr:read`
   * Type d’autorisation: `Allow`

   Cliquez sur **[!UICONTROL Ajouter]**.

   ![permissions utilisateur](assets/aem-stock-user-permissions.png)

1. Accédez à **[!UICONTROL Outils]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Stock]**. Sélectionnez la configuration de cloud [!DNL Adobe Stock] et cliquez sur **[!UICONTROL Propriétés]**.

1. Ajoutez le groupe d’utilisateurs nouvellement créé à la configuration [!DNL Adobe Stock]. Cliquez sur **[!UICONTROL Enregistrer et fermer]**.

   ![assign-user](assets/aem-stock-adduser.png)

**Pour permettre l’accès d’un utilisateur à partir de  [!DNL User Admin Console]:**

1. Ouvrez le [!DNL Experience Manager] Admin Console utilisateur. L’URL par défaut est `http://localhost:4502/userdamin`.

1. Dans le panneau de gauche, recherchez l’utilisateur en saisissant `user_id` ou `name`. Double-cliquez pour ouvrir les propriétés de l’utilisateur.

1. Accédez à l’onglet **[!UICONTROL Autorisations]** et autorisez les `read` autorisations pour la configuration de cloud [!DNL Adobe Stock] : `/conf/global/settings/stock`.

   >[!CAUTION]
   >
   >Si la configuration du cloud n’est pas autorisée, l’utilisateur ne peut accéder qu’aux **[!UICONTROL ressources]** dans l’interface [!DNL Experience Manager].
   >
   >Pour autoriser l’accès aux ressources [!UICONTROL Assets] et [!DNL Adobe Stock], assurez-vous que la configuration cloud est autorisée pour l’utilisateur.

1. Cliquez sur **[!UICONTROL Enregistrer]** pour mettre à jour les autorisations.

   ![assign-user-in-user-admin](assets/aem-stock-user-admin-console.png)

1. Ajoutez l’utilisateur ou le groupe à la configuration cloud [!DNL Adobe Stock].


## Accès aux ressources Adobe Stock {#access-stock-assets}

Un utilisateur non-administrateur disposant d’autorisations pour la configuration cloud [!DNL Adobe Stock] peut rechercher et acquérir sous licence les ressources [!DNL Adobe Stock] à partir de l’interface [!DNL Experience Manager].

L’utilisateur doit effectuer une étape supplémentaire pour activer la configuration cloud [!DNL Adobe Stock] avant d’accéder aux ressources [!DNL Adobe Stock]. Il s’agit d’une activité ponctuelle. Si l’utilisateur se voit attribuer des autorisations sur plusieurs configurations de cloud [!DNL Adobe Stock], il peut sélectionner la configuration souhaitée dans **[!UICONTROL Préférences utilisateur]**.

Pour activer la configuration de cloud [!DNL Adobe Stock] :

1. Connectez-vous à [!DNL Experience Manager].

1. Cliquez sur l’icône de l’utilisateur dans le coin supérieur droit, puis sur **[!UICONTROL Mes préférences]**. La fenêtre **[!UICONTROL Préférences utilisateur]** s’ouvre.

1. Sélectionnez la **[!UICONTROL Configuration du stock]** souhaitée dans la liste déroulante et cliquez sur **[!UICONTROL Accepter]** pour activer la configuration.

   ![préférences utilisateur](assets/aem-stock-preferences.png)

1. Accédez à **[!UICONTROL Ressources]** > **[!UICONTROL Adobe Stock]**. Vous pouvez désormais afficher, rechercher et acquérir sous licence des ressources [!DNL Adobe Stock].

Le tableau suivant explique le fonctionnement des autorisations utilisateur lors de l’accès aux ressources [!DNL Adobe Stock] :

| User | Groupe | Autorisations | Configuration Accept Stock dans les préférences utilisateur | Accès aux ressources | Accès à Adobe Stock |
| --- | --- | --- | --- | --- | --- |
| admin | N/A | Tous | N/A | Oui | Oui |
| test-doc1 | Utilisateur DAM | `/conf/global/settings/stock/cloud-config` | Oui | Oui | Oui |
| test-doc1 | Utilisateur DAM | `/conf/global/settings/stock/cloud-config` | Non | Erreur : Échec du chargement des données | Non |
| test-doc1 | Utilisateur DAM | allow : `/conf/global/settings/stock` deny : `/cloud-config` | La configuration des stocks n’est pas visible | Oui | Non |


## Utilisation et gestion de ressources [!DNL Adobe Stock] dans [!DNL Experience Manager] {#usemanage}

Grâce à cette fonctionnalité, les entreprises peuvent permettre à leurs utilisateurs de travailler avec des ressources [!DNL Adobe Stock] dans [!DNL Experience Manager Assets]. Dans l’interface utilisateur [!DNL Experience Manager], les utilisateurs peuvent rechercher des ressources [!DNL Adobe Stock] et obtenir des licences pour les ressources requises.

Une fois qu’une ressource [!DNL Adobe Stock] est sous licence dans [!DNL Experience Manager], elle peut être utilisée et gérée comme une ressource standard. Dans [!DNL Experience Manager], les utilisateurs peuvent rechercher des ressources, les prévisualiser, les copier, les publier, les partager sur [!DNL Brand Portal] et les utiliser via l’application de bureau [!DNL Experience Manager], etc.

![Recherche de  [!DNL Adobe Stock] ressources et filtrage des résultats de votre  [!DNL Adobe Experience Manager] espace de travail](assets/adobe-stock-search-results-workspace.png)

**A.**[!DNL Adobe Stock] Rechercher les ressources semblables à celles dont l’ID est fourni. **B.** Rechercher les ressources correspondant à la forme ou à l’orientation que vous avez sélectionnée. **C.** Recherchez l’un des types de ressources les plus pris en charge  **D.** Ouvrez ou réduisez le volet des filtres  **E.**  Donnez la licence et enregistrez la ressource sélectionnée dans  [!DNL Experience Manager] **F.** Enregistrez la ressource dans  [!DNL Experience Manager] avec le filigrane  **G.** Explorez les ressources du site web  [!DNL Adobe Stock] semblables à la ressource sélectionnée  **H.** Afficher les ressources sélectionnées sur le site web  [!DNL Adobe Stock]  **.**   **J.** Basculement entre le mode Carte et le mode Liste

### Recherche de ressources {#find-assets}

Vos utilisateurs [!DNL Experience Manager] peuvent rechercher des ressources dans [!DNL Experience Manager] et dans [!DNL Adobe Stock]. Lorsque l’emplacement de recherche n’est pas limité à [!DNL Adobe Stock], les résultats de recherche en provenance d’[!DNL Experience Manager] et d’[!DNL Adobe Stock] sont affichés.

* Pour rechercher des ressources [!DNL Adobe Stock], cliquez sur **[!UICONTROL Navigation]** > **[!UICONTROL Ressources]** > **[!UICONTROL Rechercher sur Adobe Stock]**.

* Pour rechercher des ressources dans [!DNL Adobe Stock] et [!DNL Experience Manager Assets], cliquez sur ![Rechercher](assets/do-not-localize/search_icon.png).

Vous pouvez également commencer à saisir `Location: Adobe Stock` dans la barre de recherche pour sélectionner des ressources [!DNL Adobe Stock] [!DNL Experience Manager] propose des fonctionnalités de filtrage avancé sur les ressources recherchées, ce qui permet aux utilisateurs de cibler rapidement les ressources requises à l’aide de filtres tels que les types de ressources pris en charge, l’orientation d’image et l’état de licence.

>[!NOTE]
>
>Les ressources recherchées à partir de [!DNL Adobe Stock] s’affichent dans [!DNL Experience Manager]. Les ressources [!DNL Adobe Stock] ne sont pas récupérées ni stockées dans le référentiel [!DNL Experience Manager] tant qu’un utilisateur n’a pas [enregistré une ressource](/help/assets/aem-assets-adobe-stock.md#saveassets) ou [acquis sous licence et enregistré une ressource ](/help/assets/aem-assets-adobe-stock.md#licenseassets). Les ressources déjà stockées dans [!DNL Experience Manager] sont affichées et mises en surbrillance pour simplifier leur référencement et leur accès. En outre, les ressources [!DNL Stock] sont enregistrées avec quelques métadonnées supplémentaires pour indiquer la source comme étant [!DNL Stock].

![Filtres de recherche dans  [!DNL Experience Manager] et  [!DNL Adobe Stock] ressources mises en surbrillance dans les résultats de recherche](assets/aem-search-filters2.jpg)

### Enregistrement et affichage des ressources requises {#saveassets}

Sélectionnez une ressource que vous souhaitez enregistrer dans [!DNL Experience Manager]. Cliquez sur [!UICONTROL Enregistrer] dans la barre d’outils supérieure, et indiquez le nom et l’emplacement de la ressource. Les ressources sans licence sont enregistrées en local avec un filigrane.

La prochaine fois que vous rechercherez des ressources, les ressources enregistrées seront mises en évidence avec un badge pour indiquer qu’elles sont disponibles dans [!DNL Experience Manager Assets].

>[!NOTE]
>
>Les ressources ajoutées récemment sont assorties d’un badge Nouvelle au lieu du badge Sous licence.

### Acquisition de ressources sous licence {#licenseassets}

Les utilisateurs peuvent acquérir des ressources [!DNL Adobe Stock] sous licence en utilisant le quota de leur abonnement pour entreprise [!DNL Adobe Stock]. Lorsque vous acquérez une ressource sous licence, elle est enregistrée sans filigrane, et elle peut être recherchée et utilisée dans [!DNL Experience Manager Assets].

![Boîte de dialogue permettant d’acquérir sous licence et d’enregistrer  [!DNL Adobe Stock] des ressources dans  [!DNL Experience Manager Assets]](assets/aem-stock_licenseandsave.jpg)


### Accès aux propriétés de ressources et de métadonnées {#access-metadata-and-asset-properties}

Les utilisateurs peuvent accéder aux métadonnées et les prévisualiser, ce qui inclut les propriétés de métadonnées [!DNL Adobe Stock] des ressources enregistrées dans [!DNL Experience Manager], et ajouter des **[!UICONTROL Références de licence]** pour une ressource. Cependant, les mises à jour apportées à une référence de licence ne sont pas synchronisées entre [!DNL Experience Manager] et le site web d’[!DNL Adobe Stock].

Les utilisateurs peuvent afficher les propriétés de toutes les ressources, avec et sans licence.

![Affichage des métadonnées et des références de licence des ressources enregistrées, et accès à ces éléments](assets/metadata_properties.jpg)


## Limitations connues {#known-limitations}

* **Problèmes d&#39;intégration avec  [!DNL Experience Manager] Service Pack 6.5.7.0 et versions ultérieures** : Un problème inattendu est identifié lors de l’intégration à la version  [!DNL Experience Manager] 6.5.7.0 et ultérieure. Le problème est en cours de test et devrait être disponible dans [!DNL Experience Manager] 6.5.11.0. Contactez [!DNL Customer Support] pour obtenir un correctif immédiat.

* **La fonctionnalité de restriction des licences des utilisateurs ne fonctionne pas correctement** : Tous les utilisateurs disposant  `read` d’autorisations sur la configuration de stock sont autorisés à rechercher et à obtenir des licences pour les  [!DNL Adobe Stock] ressources.

* **Les utilisateurs non-administrateurs doivent activer manuellement la configuration  [!DNL Adobe Stock] cloud** : Dans la fenêtre  **[!UICONTROL Préférences]** utilisateur, la  **[!UICONTROL configuration]** Stock affiche la configuration  [!DNL Adobe Stock] cloud comme activée, mais elle ne fonctionne pas pour un utilisateur non administrateur. L’utilisateur doit cliquer sur le bouton **[!UICONTROL Accepter]** pour activer la configuration Stock. En l’absence de cette étape, le système reflète un message d’erreur lors de l’accès à **[!UICONTROL Assets]**.

* **L’avertissement d’image éditoriale n’est pas affiché** : lors de l’octroi d’une licence pour une image, les utilisateurs ne peuvent pas vérifier si une image est destinée à une utilisation éditoriale uniquement. Pour lutter contre une éventuelle utilisation abusive, les administrateurs peuvent désactiver l’accès aux ressources éditoriales à partir d’Admin Console.

* **Type de licence affiché incorrect** : il est possible qu’un type de licence incorrect apparaisse dans [!DNL Experience Manager] pour une ressource. Les utilisateurs peuvent se connecter au site web d’[!DNL Adobe Stock] pour afficher le type de licence.

* **Les champs de référence et les métadonnées ne sont pas synchronisés** : lorsqu’un utilisateur met à jour un champ de référence de licence, les informations de référence de licence sont mises à jour dans [!DNL Experience Manager], mais pas sur le site web d’[!DNL Adobe Stock]. De même, si l’utilisateur met à jour les champs de référence sur le site web d’[!DNL Adobe Stock], les mises à jour ne sont pas synchronisées dans [!DNL Experience Manager].

>[!MORELIKETHIS]
>
>* [Tutoriel vidéo sur l’ [!DNL Adobe Stock] utilisation de ressources avec [!DNL Experience Manager Assets]](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/creative-workflows/adobe-stock.html?lang=fr)
>* [[!DNL Adobe Stock] aide pour les plans d’entreprise](https://helpx.adobe.com/fr/enterprise/using/adobe-stock-enterprise.html)
>* [[!DNL Adobe Stock] FAQ](https://helpx.adobe.com/fr/stock/faq.html)



<!--old content

### Create an IMS configuration {#create-an-ims-configuration}

1. In the [!DNL Experience Manager] user interface, navigate to **[!UICONTROL Tools]** > **[!UICONTROL Security]** > **[!UICONTROL Adobe IMS Configurations]**. Click **[!UICONTROL Create]** and select **[!UICONTROL Cloud Solution]** > **[!UICONTROL Adobe Stock]**.
1. Either reuse an existing certificate or select **[!UICONTROL Create new certificate]**.
1. Click **[!UICONTROL Create certificate]**. Once created, download the public key. Click **[!UICONTROL Next]**. Leave the [!UICONTROL Adobe IMS Technical Account Configuration] screen open to provide the required values shortly.
1. Access [Adobe Developer Console](https://console.adobe.io). Ensure that your account has administrator permissions for the organization for which the integration is required.
1. Click **[!UICONTROL Create new project]** and click **[!UICONTROL Add API]**. Select **[!UICONTROL Adobe Stock]** from the list of APIs that are available to you. Select [!UICONTROL OAUTH 2.0 Web].
1. Provide **[!UICONTROL Default redirect URI]** and **[!UICONTROL Redirect URI pattern]** values. Click **[!UICONTROL Save configured API]**. Copy the generated ID and secret.
1. In [!UICONTROL Adobe IMS Technical Account Configuration] screen, provide the values in the boxes titled **[!UICONTROL Title]**, **[!UICONTROL Authorization Server]**, **[!UICONTROL API Key]**, **[!UICONTROL Client Secret]**, and **[!UICONTROL Payload]**. For detailed information about these values, see [JWT authentication quick start](https://www.adobe.io/authentication/auth-methods.html#!AdobeDocs/adobeio-auth/master/JWT/JWT.md).

-->

<!-- TBD: Update the URL to update the terminology when AIO team updates their documentation URL. Logged issue github.com/AdobeDocs/adobeio-auth/issues/63.
-->

<!--
### Create [!DNL Adobe Stock] configuration in [!DNL Experience Manager] {#create-adobe-stock-configuration-in-aem}

1. In the [!DNL Experience Manager], navigate to **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Stock]**.
1. Click **[!UICONTROL Create]** to create a configuration and associate it with your existing IMS Configuration. Select `PROD` as the environment parameter.
1. In **[!UICONTROL Licensed Assets Path]** field, leave a location as is. Do not change the location where you want to store the [!DNL Adobe Stock] assets.
1. Complete creation by adding all the required properties. Click **[!UICONTROL Save & Close]**.
1. Add [!DNL Experience Manager] users or groups, who can license the assets.

>[!NOTE]
>
>If there are multiple [!DNL Adobe Stock] configurations, select the desired configuration in [!UICONTROL User Preferences] panel. To access the panel from [!DNL Experience Manager] home page, click the user icon and then click **[!UICONTROL User Preferences]** > **[!UICONTROL Stock Configuration]**.

-->