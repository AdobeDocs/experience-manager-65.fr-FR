---
title: Implémentation de référence We.Retail
seo-title: Implémentation de référence We.Retail
description: We.Retail est un aperçu technologique d’une implémentation de référence qui illustre la méthode recommandée pour mettre en place une présence en ligne avec AEM.
seo-description: We.Retail est un aperçu technologique d’une implémentation de référence qui illustre la méthode recommandée pour mettre en place une présence en ligne avec AEM.
uuid: d8833192-b592-4812-bf9b-bd882e8ee7f0
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: f50150af-deff-4c29-bfe0-1cfc67b29d51
translation-type: tm+mt
source-git-commit: 307a1db2e5bbb72d730c89ba14f5ce02b96c108d
workflow-type: tm+mt
source-wordcount: '779'
ht-degree: 89%

---


# Implémentation de référence We.Retail{#we-retail-reference-implementation}

## Présentation {#introduction}

We.Retail est à la fois une implémentation de référence et un exemple de contenu illustrant la méthode recommandée pour mettre en place une présence en ligne avec Adobe Experience Manager.

We.Retail utilise les technologies AEM les plus récentes, telles que HTL, les mises en page réactives, les modèles modifiables, les composants principaux, et bien plus encore.

Bien que le site représente le secteur du commerce de détail, la façon dont il est configuré le rend applicable à tous les secteurs. Seuls le catalogue de produits et les fonctionnalités du panier d’achat sont propres au secteur du commerce de détail.

## Fonctions {#features}

En tant qu’implémentation de référence standard d’AEM, We.Retail présente certaines des fonctions les plus puissantes d’AEM.

| **Fonctionnalité** | **Description** | **Intéressé ?** |
|---|---|---|
| [Structure de site globalisée](/help/sites-administering/tc-bp.md) | We.Retail comprend des gabarits de langue qui sont copiés de manière dynamique dans des sites localisés. | [Faites un essai !](/help/sites-developing/we-retail-globalized-site-structure.md) |
| [Mise en page réactive](/help/sites-authoring/responsive-layout.md) | Toutes les pages disposent d’une mise en page réactive pour s’adapter de manière dynamique à la taille de l’écran et du terminal. | [Faites un essai !](/help/sites-developing/we-retail-responsive-layout.md) |
| [Modèles modifiables](/help/sites-developing/page-templates-editable.md) | Toutes les pages reposent sur des modèles modifiables, ce qui permet aux non-développeurs d’adapter et de personnaliser les modèles. | [Faites un essai !](/help/sites-developing/we-retail-editable-templates.md) |
| [HTML Template Language](https://docs.adobe.com/content/help/fr-FR/experience-manager-htl/using/overview.html) | Tous les composants sont basés sur HTL. |  |
| [Fonctionnalités de commerce électronique](/help/sites-developing/ecommerce.md) | Catalogue de produits intégré. |  |
| [Sites Communities](/help/communities/overview.md) | Les visiteurs sont autorisés à participer à des discussions communautaires, à lire des blogs et bien plus encore. |  |
| [Composants principaux](https://docs.adobe.com/content/help/fr-FR/experience-manager-core-components/using/introduction.html) | Tous les composants sont basés sur les nouveaux composants principaux. Ils s’avèrent également plus faciles à utiliser et à configurer en standard. | [Faites un essai !](/help/sites-developing/we-retail-core-components.md) |
| [Fragments de contenu](/help/assets/content-fragments/content-fragments.md) | La section Expériences We.Retail permet de réutiliser du contenu au moyen de fragments de contenu. | [Faites un essai !](/help/sites-developing/we-retail-content-fragments.md) |
| [Fragments d’expérience](/help/sites-authoring/experience-fragments.md) | Un fragment d’expérience est un groupe d’un ou plusieurs composants comprenant un contenu et une disposition pouvant être référencés dans les pages. | [Faites un essai !](/help/sites-developing/we-retail-experience-fragments.md) |

## Prise en main {#getting-started}

We.Retail est fourni sous la forme d’un échantillon de contenu d’AEM. Pour l’utiliser, [démarrez AEM comme vous le feriez normalement](/help/sites-deploying/deploy.md#getting-started), en veillant à ce que l’échantillon de contenu ne soit pas désactivé.

>[!CAUTION]
>
>We.Retail ne doit pas être installé sur les instances de production. Les instances de production doivent être démarrées dans `nosamplecontent` [runmode](/help/sites-deploying/configure-runmodes.md).

>[!CAUTION]
>
>We.Retail repose sur la technologie AEM la plus récente et ne prend donc pas en charge la [création dans l’IU classique](/help/sites-classic-ui-authoring/home.md).

### Dernière version {#latest-version}

Bien que We.Retail soit distribué avec la version AEM, il se peut que des mises à jour soient apportées au contenu et à ses fonctionnalités après la publication du produit. Il est donc possible de [télécharger la dernière version de GitHub](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/releases), puis de [télécharger](/help/sites-administering/package-manager.md#uploading-packages-from-your-file-system) et [installer](/help/sites-administering/package-manager.md#installing-packages) sous forme de package sur votre instance AEM.

### Premiers pas {#first-steps}

1. Une fois AEM démarré (et/ou We.Retail installé), le site **We.Retail** est disponible dans la [console sites](/help/sites-authoring/basic-handling.md#global-navigation).
1. Par exemple, la page suivante peut être ouverte et elle doit ressembler à ce qui est affiché dans l’[annexe](#appendix) ci-dessous :

   `https://<server name>:<port number>/editor.html/content/we-retail/language-masters/en.html`

## We.Retail et Geometrixx {#we-retail-geometrixx}

Geometrixx et ses nombreuses incarnations ont servi d’exemple de contenu dans les versions antérieures d’AEM. Depuis la version 6.3, We.Retail est l’échantillon de contenu fourni avec AEM et sert de nouvelle implémentation de référence standard.

D’un point de vue technique, We.Retail est plus robuste et exploite la technologie AEM dernier cri pour garantir une souplesse et une évolutivité accrues, tout en offrant les fonctionnalités les plus récentes du produit.

### Comparaison des fonctions {#feature-comparison}

Le tableau suivant vous donne un aperçu des principales fonctionnalités qui sont disponibles dans We.Retail par rapport à Geometrixx.

* **Disponible** signifie que l’échantillon de contenu contient des exemples de la fonctionnalité.
* **Non disponible** signifie qu’aucun exemple de la fonctionnalité n’est disponible dans l’échantillon de contenu. Cependant, cela ne signifie pas que la fonctionnalité proprement dite n’est pas disponible.

| **Fonctionnalité** | **We.Retail** | **Geometrixx** |
|---|---|---|
| Structure de site globalisée | Les maîtres de langues sont copiés en direct sur des sites spécifiques à chaque pays. | Non disponible |
| Fragments de contenu | Disponible | Non disponible |
| Fragments d’expérience | Disponible | Non disponible |
| Mise en page réactive   | Pour toutes les pages | Uniquement Geometrixx Media |
| Modèles modifiables | Pour toutes les pages | Non disponible |
| HTL | Tous les composants | Limited |
| Ciblage | Pour toutes les pages | Uniquement Geometrixx Outdoors |
| Screens | Disponible | Non disponible |
| Mobile | Non disponible | Disponible |
| Manuscrits | Non disponible | Disponible |
| Carrousel, téléchargement, composants de graphique | Non disponible | Disponible |
| Contrôle de colonne | Remplacé par le conteneur de mise en page | Disponible |
| Formulaires | Non disponible | Disponible |
| Campagne | Aucun exemple de courrier électronique | Disponible |

>[!NOTE]
>
>Cette liste est la plus complète possible, mais ne doit pas être considérée comme exhaustive.

## Contribution {#contribute}

We.Retail a été publié en tant que projet Open Source et la dernière version du code source peut également être téléchargée depuis GitHub.

CODE SUR GITHUB

Vous pouvez trouver le code de cette page sur GitHub.

* [Ouvrez le projet aem-sample-we-commerce sur GitHub.](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail)
* Téléchargez le projet sous la forme d’[un fichier ZIP](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/archive/master.zip).

La dernière version peut également être [téléchargée directement](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/releases/latest) en tant que module à +installer.

Si vous rencontrez des problèmes, envoyez [Problèmes GitHub](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/issues).

N’hésitez pas à répliquer ou à contribuer avec des [requêtes d’extraction](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/pulls).

## Aperçu {#preview}

Aperçu de page d’accueil de We.Retail :

![screencapture-localhost-4502-editor-html-content-we-commerce-us-fr-html-2018-08-17-14_33_32](assets/screencapture-localhost-4502-editor-html-content-we-retail-us-en-html-2018-08-17-14_33_32.png)

