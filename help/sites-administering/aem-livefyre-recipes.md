---
title: Recettes AEM Livefyre
seo-title: Recettes AEM Livefyre
description: Cette section contient des instructions détaillées sur les cas d’utilisation courants d’Adobe Experience Manager Livefyre.
seo-description: Cette section contient des instructions détaillées sur les cas d’utilisation courants d’Adobe Experience Manager Livefyre.
uuid: 78695a63-fca6-4990-9755-0aeaae4a7f64
contentOwner: alba
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: fdea5ede-d44f-463e-af8a-111ee7469ede
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379

---


# Recettes AEM Livefyre{#aem-livefyre-recipes}

Cette section contient des instructions détaillées sur les cas d’utilisation courants d’Adobe Experience Manager Livefyre.

## Traitement et affichage du contenu créé par l’utilisateur à l’aide des composants AEM Livefyre prêts à l’emploi et du Mur multimédia Livefyre {#curate-ugc-using-the-out-of-the-box-livefyre-aem-components-and-display-using-livefyre-media-wall}

Mur multimédia diffuse du contenu Livefyre natif et provenant des réseaux sociaux sur un mur en temps réel. Il existe plusieurs façons d’implémenter le composant Mur multimédia dans AEM, selon les cas d’utilisation et les exigences.

Le module AEM Livefyre fournit une implémentation prête à l’emploi, tandis que l’intégration classique permet de créer des composants AEM Livefyre personnalisés.

### Intégration d’AEM {#aem-integration}

Le package Adobe Experience Manager Livefyre est disponible pour AEM 6.1, 6.2 SP1, 6.3, 6.4 et 6.4 SP1. AEM 5.x et 6.0 ne sont pas pris en charge. Pour obtenir des instructions détaillées, voir [Intégration à Livefyre](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/livefyre.html).

To see which Livefyre Apps are supported, see the [AEM Support Matrix for Livefyre Apps](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#AEMSupportMatrixforLivefyreApps).

### Implémentation classique (pour les composants AEM personnalisés) {#traditional-implementation-for-customized-aem-components}

Il existe trois manières d’implémenter Livefyre dans un composant AEM personnalisé ou d’autres systèmes de gestion de contenu tels que WordPress, Sitecore ou DemandWare. L’intégration Livefyre classique est compatible avec tous types de systèmes de gestion de contenu.

**Méthode 1 : implémentation de l’application Designer**

* **Description :** méthode la plus simple et la plus rapide d’intégrer une application Livefyre. Vous pouvez concevoir, configurer et générer un code intégré JavaScript personnalisé pour intégrer une application Mur multimédia à une page en quelques minutes.
* **** Comment :  [Créer, prévisualiser, publier et incorporer une application de mur multimédia](https://marketing.adobe.com/resources/help/en_US/livefyre/c_create_an_app.html)

* **Exemple :**[https://codepen.io/dharafyre/pen/bvGrLo](https://codepen.io/dharafyre/pen/bvGrLo)

**Méthode 2 : implémentation du SDK**

* **Description :** [Livefyre.js](https://marketing.adobe.com/resources/help/en_US/livefyre/c_livefyre.js.html) est la bibliothèque principale qui alimente les applications et les authentifications sur un site. Celle-ci définit l’objet global *window.Livefyre* et une méthode publique unique, *Livefyre.require*, qui peuvent être utilisés pour charger d’autres bibliothèques JavaScript Livefyre. Ces bibliothèques permettent l’intégration des applications Livefyre et l’intégration aux plateformes tierces d’authentification de l’utilisateur.

* **Comment** : [utilisation du module streamcenter-wall du SDK Livefyre JavaScript](https://marketing.adobe.com/resources/help/en_US/livefyre/?f=c_media_wall_app&s=c_media_wall_integration) (en anglais)

* **Exemple** : [https://codepen.io/dharafyre/pen/KZKBNv?editors=1010](https://codepen.io/dharafyre/pen/KZKBNv?editors=1010)

Pour des personnalisations avancées à l’aide du SDK, consultez la page [SDK streamhub](https://github.com/Livefyre/streamhub-sdk) (en anglais).

**Méthode 3 : implémentation de l’API**

* Pour des expériences et des visualisations de données personnalisées, vous pouvez créer des applications Livefyre de A à Z en utilisant des données Livefyre et des données des médias sociaux, à l’aide des [API Bootstrap et Stream](https://marketing.adobe.com/resources/help/en_US/livefyre/bootstrap-stream-api.html).

Make sure you follow [Twitter](https://developer.twitter.com/en/developer-terms/display-requirements.html), [Facebook](https://en.facebookbrand.com/guidelines/brand), and [Instagram](https://en.instagram-brand.com/) display guidelines when building the UI for UGC.

### Intégration de l’authentification au mur multimédia {#media-wall-authentication-integration}

Pour les intégrations de murs multimédias nécessitant une authentification, consultez la page :

* [Personnalisation de l’intégration](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/livefyre.html#CustomizeSingleSignonIntegration) de la connexion unique pour la gestion des identités AEM
* [Intégration d’identité](https://marketing.adobe.com/resources/help/en_US/livefyre/t_about_identity_integration.html) pour les plateformes d’authentification tierces (en anglais)

### Cas d’utilisation {#use-case-overview}

En tant qu’utilisateur AEM, je souhaite traiter le contenu créé par l’utilisateur à l’aide des composants AEM Livefyre prêts à l’emploi et afficher ce contenu avec Mur multimédia Livefyre.

Étapes de l’implémentation :

1. [Prise en main](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html)
1. [Configuration d’AEM pour utiliser Livefyre](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html) (lien en anglais)
1. [Effectuez un glisser-déposer du composant Mur multimédia d’AEM sur votre page](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#UseLivefyrewithAEMSites)
1. [Configurez des flux et ajoutez des règles pour traiter le contenu créé par l’utilisateur et l’afficher sur le composant Mur multimédia](https://marketing.adobe.com/resources/help/en_US/livefyre/c_streams.html)

For training videos on streaming UGC, see [Create Automatic Content Streams and Search Social Content in Adobe Experience Manager Livefyre](https://helpx.adobe.com/experience-manager/tutorials.html).

### Exemples de clients {#customer-examples}

* [Mur multimédia de CNN](https://edition.cnn.com/specials/nepal-earthquake-media-wall)
* [Mur multimédia du PGA Tour](https://www.pgatour.com/social-hub.html)

Pour des expériences et des visualisations de données personnalisées, vous pouvez créer des applications Livefyre de A à Z en utilisant des données Livefyre et des données des médias sociaux, à l’aide des [API Bootstrap et Stream](https://marketing.adobe.com/resources/help/en_US/livefyre/bootstrap-stream-api.html).

For Livefyre Apps requiring authentication, please see [Identity Integration](https://marketing.adobe.com/resources/help/en_US/livefyre/t_about_identity_integration.html) for third party authentication platforms.

* [Mur multimédia du PGA Tour](https://www.pgatour.com/social-hub.html)
* [TimeOut](https://www.timeout.com/london/restaurants/forest-bar-kitchen#tab_panel_3)

## Intégration de Livefyre Comments à l’aide des composants AEM ou de l’intégration Livefyre classique {#integrate-livefyre-comments-using-aem-components-or-traditional-livefyre-integration}

### Intégration d’AEM {#aem-integration-1}

Le package Adobe Experience Manager Livefyre est disponible pour AEM 6.1, 6.2 SP1, 6.3, 6.4 et 6.4 SP1. AEM 5.x et 6.0 ne sont pas pris en charge. Pour obtenir des instructions détaillées, voir [Intégration à Livefyre](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/livefyre.html).

### Implémentation classique (pour les composants AEM personnalisés) {#traditional-implementation-for-customized-aem-components-1}

Il existe trois façons d’implémenter l’application Livefyre Comments dans un composant AEM personnalisé ou dans d’autres systèmes de gestion de contenu tels que WordPress, Sitecore ou DemandWare. L’intégration Livefyre classique est compatible avec tous types de systèmes de gestion de contenu.

**Méthode 1 : implémentation de l’application Designer**

* **Description :** méthode la plus simple et la plus rapide d’intégrer une application Livefyre. Vous pouvez concevoir, configurer et générer un code intégré JavaScript personnalisé pour intégrer une application Mur multimédia à une page en quelques minutes.
* **** Comment : [Créer, prévisualiser, publier et incorporer une application de commentaires](https://marketing.adobe.com/resources/help/en_US/livefyre/c_create_an_app.html)

* **Exemple :**[https://codepen.io/dharafyre/pen/oYoJdP](https://codepen.io/dharafyre/pen/oYoJdP)

**Méthode 2 : implémentation du SDK**

* **Description :** [Livefyre.js](https://marketing.adobe.com/resources/help/en_US/livefyre/c_livefyre.js.html) est la bibliothèque principale qui alimente les applications et les authentifications sur un site. Celle-ci définit l’objet global *window.Livefyre* et une méthode publique unique, *Livefyre.require*, qui peuvent être utilisés pour charger d’autres bibliothèques JavaScript Livefyre. Ces bibliothèques permettent l’intégration des applications Livefyre et l’intégration aux plateformes tierces d’authentification de l’utilisateur.

* **Comment :**

   * Créez une collection ou une application à l’aide du [jeton CollectionMeta](https://marketing.adobe.com/resources/help/en_US/livefyre/t_create_a_collectionmeta_token.html).
   * Intégrez l’application [Comments](https://marketing.adobe.com/resources/help/en_US/livefyre/c_comments_integration.html) aux sites à l’aide de la structure du code d’intégration Livefyre.js.

* **Exemple :**[https://codepen.io/dharafyre/pen/oYoJdP](https://codepen.io/dharafyre/pen/oYoJdP)

For advanced customizations using the SDK, please see [StreamHub SDKs](https://github.com/Livefyre/streamhub-sdk).

**Méthode 3 : implémentation de l’API**

* Pour des expériences et des visualisations de données personnalisées, vous pouvez créer des applications Livefyre de A à Z en utilisant des données Livefyre et des données des médias sociaux, à l’aide des [API Bootstrap et Stream](https://marketing.adobe.com/resources/help/en_US/livefyre/bootstrap-stream-api.html).

### Intégration de l’authentification à l’application Comments {#comments-app-authentication-integration}

* [Personnalisation de l’intégration](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/livefyre.html#CustomizeSingleSignonIntegration) de la connexion unique pour la gestion des identités AEM
* [Intégration d’identité](https://marketing.adobe.com/resources/help/en_US/livefyre/t_about_identity_integration.html) pour les plateformes d’authentification tierces

### Exemples de clients {#customer-examples-1}

* [Poise (Kimberly Klark)](https://www.poise.com/en-us/advice-and-support/blog-and-podcast/blog/5-holiday-party-tips-for-managing-lbl)

## Utilisation de Livefyre avec AEM Assets pour importer le contenu créé par l’utilisateur dans AEM Assets {#use-livefyre-aem-assets-integration-to-import-ugc-in-aem-assets}

**Configuration de Livefyre (pour le traitement du contenu créé par l’utilisateur et la gestion des droits) :**

1. [Configurez des flux et ajoutez des règles aux dossiers de la bibliothèque de fichiers Livefyre pour traiter le contenu créé par l’utilisateur](https://marketing.adobe.com/resources/help/en_US/livefyre/c_streams.html).

   1. For training videos on streaming UGC, see [Create Automatic Content Streams and Search Social Content in Adobe Experience Manager Livefyre](https://helpx.adobe.com/experience-manager/tutorials.html).

1. [Rassemblez, organisez et gérez le contenu créé par l’utilisateur dans les dossiers de la bibliothèque de fichiers Livefyre](https://marketing.adobe.com/resources/help/en_US/livefyre/c_assets.html) (lien en anglais).

   1. For training videos on creating and managing folders in the Livefyre Studio Asset Library, see [Work with Assets in Adobe Experience Manager Livefyre](https://helpx.adobe.com/experience-manager/tutorials.html).

1. [Demandez des droits sur le contenu créé par l’utilisateur traité à l’aide de Livefyre Studio](https://marketing.adobe.com/resources/help/en_US/livefyre/c_how_requesting_rights_works.html).

**Configuration d’AEM (pour l’importation du contenu créé par l’utilisateur vers AEM Assets) :**

1. [Prise en main](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#GettingStarted)
1. [Configuration d’AEM pour utiliser Livefyre](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#ConfigureAEMtouseLivefyre) (lien en anglais)
1. [Importation du contenu créé par l’utilisateur traité par Livefyre vers AEM Assets](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#UseLivefyrewithAEMAssets) (lien en anglais)

* [Office du tourisme d’Australie](https://www.australia.com/en-us)

## Intégration de Livefyre Reviews à l’aide des composants AEM ou de l’intégration Livefyre classique {#integrate-livefyre-reviews-using-aem-components-or-traditional-livefyre-integration}

### Intégration d’AEM {#aem-integration-2}

Le package Adobe Experience Manager Livefyre est disponible pour AEM 6.1, 6.2 SP1, 6.3, 6.4 et 6.4 SP1. AEM 5.x et 6.0 ne sont pas pris en charge. Pour obtenir des instructions détaillées, voir [Intégration à Livefyre](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/livefyre.html).

Reviews n’est pas prise en charge par AEM 6.1. Veuillez consulter la [grille de prise en charge d’AEM pour l’ensemble des applications Livefyre](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#AEMSupportMatrixforLivefyreApps).

### Implémentation classique (pour les composants AEM personnalisés) {#traditional-implementation-for-customized-aem-components-2}

Il existe deux façons d’implémenter l’application Livefyre Reviews dans un composant AEM personnalisé ou dans d’autres systèmes de gestion de contenu tels que WordPress, Sitecore ou DemandWare. L’intégration Livefyre classique est compatible avec tous types de systèmes de gestion de contenu.

**Méthode 1 : implémentation du SDK**

* **Description :** [Livefyre.js](https://marketing.adobe.com/resources/help/en_US/livefyre/c_livefyre.js.html) est la bibliothèque principale qui alimente les applications et les authentifications sur un site. Celle-ci définit l’objet global *window.Livefyre* et une méthode publique unique, *Livefyre.require*, qui peuvent être utilisés pour charger d’autres bibliothèques JavaScript Livefyre. Ces bibliothèques permettent l’intégration des applications Livefyre et l’intégration aux plateformes tierces d’authentification de l’utilisateur.

* **Comment :**

   * Créez le [jeton CollectionMeta](https://marketing.adobe.com/resources/help/en_US/livefyre/c_reviews_integration.html) pour spécifier les métadonnées à stocker dans la collection Reviews.
   * Intégrez l’[application Reviews](https://marketing.adobe.com/resources/help/en_US/livefyre/c_reviews_integration.html) à Sites à l’aide de la structure du code d’intégration *Livefyre.js*.

* **Exemple :**[https://codepen.io/dharafyre/pen/GXgvvd](https://codepen.io/dharafyre/pen/GXgvvd)

For advanced customizations using the SDK, please see [StreamHub SDKs](https://github.com/Livefyre/streamhub-sdk).

**Méthode 2 : implémentation de l’API**

* Pour des expériences et des visualisations de données personnalisées, vous pouvez créer des applications Livefyre de A à Z en utilisant des données Livefyre et des données des médias sociaux, à l’aide des API Bootstrap et Stream.

Additional Ratings and Reviews APIs can be found [here](https://api.livefyre.com/docs/apis/by-category/ratings-and-reviews).

### Intégration de l’authentification à l’application Comments {#comments-app-authentication-integration-1}

* [Personnalisation de l’intégration](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/livefyre.html#CustomizeSingleSignonIntegration) de la connexion unique pour la gestion des identités AEM
* [Intégration d’identité](https://marketing.adobe.com/resources/help/en_US/livefyre/t_about_identity_integration.html) pour les plateformes d’authentification tierces

### Exemples de clients {#customer-examples-2}

* [TimeOut](https://www.timeout.com/london/restaurants/forest-bar-kitchen#tab_panel_3)
* [myrecipes](https://www.myrecipes.com/recipe/shrimp-florentine-pasta)

