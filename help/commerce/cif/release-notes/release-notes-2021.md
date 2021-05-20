---
title: Notes de mise à jour d’AEM Content and Commerce 2021
description: Notes de mise à jour d’AEM Content and Commerce 2021
source-git-commit: da538dac17b4c6182b44801b4c79d6cdbf35f640
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 14%

---

# Présentation de la version GitHub de Commerce Integration Framework

## Présentation de la configuration système requise

Passez en revue la configuration système minimale requise dans le tableau ci-dessous pour la version CIF que vous utilisez actuellement ou que vous prévoyez d’utiliser à l’avenir.

**Module complémentaire CIF désormais disponible via  [Adobe Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html). L’ancien connecteur CIF AEM passe en mode de maintenance et ne doit plus être utilisé. Effectuez une migration vers le nouveau module complémentaire CIF.**

| Composant | Configuration requise |
|:-------|:-----:|
| Module complémentaire CIF | Minimum : AEM 6.5.7, schémas GraphQL Magento 2.3.5 |
| Composants principaux CIF | [Configuration requise](https://github.com/adobe/aem-core-cif-components/blob/master/VERSIONS.md) |
| Archétype de projet AEM | [Configuration requise](https://github.com/adobe/aem-project-archetype/blob/master/VERSIONS.md) |

## Date de publication : Avril 2021

| Composant | Version | Détails |
|:-------|:-----:|---------------------:|
| Module complémentaire CIF | 2021.04.22 | [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.04.22.zip) |
| Composants principaux CIF | 1.10.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases) |
| Site de référence CIF Venia | 2021.04.22 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases) |

### Nouveautés {#what-is-new-april}

* Prise en charge de l’UID de catégorie : libère les intégrations commerciales tierces pour les systèmes qui utilisent des chaînes pour les ID de catégorie.

* Extension AEM pour PWA Studio, y compris exemple d’intégration

* Nouveau composant principal de navigation CIF qui étend le composant principal de navigation WCM

* Indicateur visuel pour les données de catalogue intermédiaires dans AEM storefront

### Correctifs {#bug-fixes-april}

* Le champ de catégorie racine n’était pas affiché sous l’onglet Commerce dans les propriétés de page des pages de catégorie.

## Date de publication : Mars 2021 {#what-is-new-march}

| GitHub | Version | Notes de mise à jour détaillées |
|:-------|:-----:|---------------------:|
| Connecteur CIF | 1.9.0 | [Notes de mise à jour](https://github.com/adobe/commerce-cif-connector/releases) |
| Composants principaux CIF | 1.9.0 | [Notes de mise à jour](https://github.com/adobe/aem-core-cif-components/releases) |
| Site de référence CIF Venia | 2021.03.25 | [Notes de mise à jour](https://github.com/adobe/aem-cif-guides-venia/releases) |

### Nouveautés

* Prise en charge de Magento 2.4.2

### Nouveautés

* Amélioration de la réutilisation du composant Détails du produit pour les pages pilotées par le contenu

* Amélioration de la mise en cache et diminution des appels d’arrière-plan pour les PDP

* Plusieurs correctifs.

## Date de publication : Février 2021

| GitHub | Version | Notes de mise à jour détaillées |
|:-------|:-----:|---------------------:|
| Connecteur CIF | 1.8.0 | [Notes de mise à jour](https://github.com/adobe/commerce-cif-connector/releases) |
| Composants principaux CIF | 1.8.0 | [Notes de mise à jour](https://github.com/adobe/aem-core-cif-components/releases) |
| Site de référence CIF Venia | 2021.02.24 | [Notes de mise à jour](https://github.com/adobe/aem-cif-guides-venia/releases) |

### Nouveautés {#what-is-new-february}

* Gestion de l’expérience du produit : Enrichissez les pages du catalogue de produits individuellement avec les fragments d’expérience.

* Étendez les propriétés de la console de produit pour afficher les ressources liées et les fragments d’expérience, y compris l’action permettant d’accéder rapidement au contenu associé.

### Nouveautés {#what-is-improved-february}

* Amélioration de la couche de données côté client avec l’URL de l’image du produit et les informations sur les catégories.

* Plusieurs correctifs.

## Date de publication : Janvier 2021

| GitHub | Version | Notes de mise à jour détaillées |
|:-------|:-----:|---------------------:|
| Connecteur CIF | 1.7.0 | [Notes de mise à jour](https://github.com/adobe/commerce-cif-connector/releases) |
| Composants principaux CIF | 1.7.0 | [Notes de mise à jour](https://github.com/adobe/aem-core-cif-components/releases) |
| Site de référence CIF Venia | 2021.02.02 | [Notes de mise à jour](https://github.com/adobe/aem-cif-guides-venia/releases) |

### Nouveautés {#what-is-new-january}

* Gestion de l’expérience du produit : Nouvel onglet de propriété &quot;Commerce&quot; pour les ressources et les fragments d’expérience. Cet onglet vous permet de lier les ressources et les fragments d’expérience aux produits et catégories. L’onglet affiche également des données en temps réel pour les objets de commerce liés et un lien pour afficher les détails dans la console du produit.

### Nouveautés {#what-is-improved-january}

* Envoyez les données utilisateur après l’authentification pour Adobe de la couche de données client.

* Plusieurs correctifs.
