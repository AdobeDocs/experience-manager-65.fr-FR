---
title: Notes de mise à jour AEM Content and Commerce 2021
description: Notes de mise à jour AEM Content and Commerce 2021
translation-type: tm+mt
source-git-commit: 2d0b52dbf85e1fbe91c09a8366744aa77f25cd73
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 15%

---

# Présentation de la version GitHub de Commerce Integration Framework

## Présentation de la configuration système requise

Consultez le tableau ci-dessous pour connaître la configuration minimale requise pour la version CIF que vous utilisez actuellement ou que vous prévoyez d’utiliser à l’avenir.

**Le module complémentaire CIF est désormais disponible via  [Adobe Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html). L&#39;ancien AEM CIF Connector passe en mode de maintenance et ne doit plus être utilisé. Veuillez migrer vers le nouveau module complémentaire CIF.**

| Composant | Configuration requise |
|:-------|:-----:|
| Module complémentaire CIF | Minimum : AEM 6.5.7, Magento 2.3.5 schémas GraphQL |
| Composants principaux CIF | [Configuration requise](https://github.com/adobe/aem-core-cif-components/blob/master/VERSIONS.md) |
| Archétype de projet AEM | [Configuration requise](https://github.com/adobe/aem-project-archetype/blob/master/VERSIONS.md) |

## Date de publication : Avril 2021

| Composant | Version | Détails |
|:-------|:-----:|---------------------:|
| Module complémentaire CIF | v2021.04.22 | [Distribution de logiciels](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.04.22.zip) |
| Composants principaux CIF | 1,10,0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases) |
| Site de référence de CIF Venia | 2021.04.22 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases) |

### Nouveautés {#what-is-new-april}

* **Le module complémentaire CIF est désormais disponible via  [Adobe Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html). L&#39;ancien AEM CIF Connector passe en mode de maintenance et ne doit plus être utilisé. Veuillez migrer vers le nouveau module complémentaire CIF.**

* Prise en charge de l’identifiant d’utilisateur de catégorie - Déverrouille les intégrations commerciales tierces pour les systèmes qui utilisent des chaînes pour les identifiants de catégorie

* Extension AEM pour PWA Studio incl. exemple d’intégration

* Nouveau composant de base de navigation CIF qui étend le composant de base de navigation WCM

* Indicateur visuel pour les données de catalogue par étapes dans AEM vitrine

### Correctifs {#bug-fixes-april}

* Le champ de catégorie racine n’était pas affiché sous l’onglet Commerce dans les propriétés de page des pages de catégorie.

## Date de publication : Mars 2021 {#what-is-new-march}

| GitHub | Version | Notes de mise à jour détaillées |
|:-------|:-----:|---------------------:|
| Connecteur CIF | 1.9.0 | [Notes de mise à jour](https://github.com/adobe/commerce-cif-connector/releases) |
| Composants principaux CIF | 1.9.0 | [Notes de mise à jour](https://github.com/adobe/aem-core-cif-components/releases) |
| Site de référence de CIF Venia | 2021,03,25 | [Notes de mise à jour](https://github.com/adobe/aem-cif-guides-venia/releases) |

### Nouveautés

* Prise en charge de Magento 2.4.2

### Améliorations

* Amélioration de la réutilisation du composant des détails du produit pour les pages pilotées par le contenu

* Meilleure mise en cache et moins d’appels principaux pour les PDP

* Plusieurs correctifs de bogues.

## Date de publication : Février 2021

| GitHub | Version | Notes de mise à jour détaillées |
|:-------|:-----:|---------------------:|
| Connecteur CIF | 1.8.0 | [Notes de mise à jour](https://github.com/adobe/commerce-cif-connector/releases) |
| Composants principaux CIF | 1.8.0 | [Notes de mise à jour](https://github.com/adobe/aem-core-cif-components/releases) |
| Site de référence de CIF Venia | 2021.02.24 | [Notes de mise à jour](https://github.com/adobe/aem-cif-guides-venia/releases) |

### Nouveautés {#what-is-new-february}

* Gestion de l&#39;expérience des produits : Enrichissez les pages du catalogue de produits individuellement avec les fragments d’expérience.

* Propriétés étendues de la console de produits pour afficher les ressources liées et les fragments d’expérience, y compris les actions permettant d’accéder rapidement au contenu associé.

### Améliorations  {#what-is-improved-february}

* Amélioration de la couche de données côté client avec l’URL d’image du produit et les informations de catégorie

* Plusieurs correctifs de bogues.

## Date de publication : Janvier 2021

| GitHub | Version | Notes de mise à jour détaillées |
|:-------|:-----:|---------------------:|
| Connecteur CIF | 1.7.0 | [Notes de mise à jour](https://github.com/adobe/commerce-cif-connector/releases) |
| Composants principaux CIF | 1.7.0 | [Notes de mise à jour](https://github.com/adobe/aem-core-cif-components/releases) |
| Site de référence de CIF Venia | 2021.02.02 | [Notes de mise à jour](https://github.com/adobe/aem-cif-guides-venia/releases) |

### Nouveautés {#what-is-new-january}

* Gestion de l&#39;expérience des produits : Nouvel onglet de propriété Commerce pour les ressources et les fragments d’expérience. Cet onglet vous permet de lier des ressources et des fragments d’expérience à des produits et catégories. L&#39;onglet affiche également des données en temps réel pour les objets de commerce liés et un lien pour afficher des détails dans la console du produit.

### Améliorations  {#what-is-improved-january}

* Envoyez les données utilisateur après l’authentification à la couche de données du client Adobe.

* Plusieurs correctifs de bogues.
