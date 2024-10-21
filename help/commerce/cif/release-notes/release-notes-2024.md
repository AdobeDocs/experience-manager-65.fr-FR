---
title: Notes de mise à jour d’AEM Content and Commerce 2024
description: Notes de mise à jour d’Adobe Experience Manager Content and Commerce 2024.
exl-id: 372e6a46-72bb-4db4-ad01-534ca723ae58
solution: Experience Manager,Commerce
feature: Commerce Integration Framework
role: Admin, Developer
source-git-commit: 1788e5f77d4c46a548710361e9e5dae3c6daab28
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 88%

---

# Vue d’ensemble de la version GitHub de Commerce Integration Framework

## Présentation de la configuration système requise

Passez en revue la configuration système minimale requise dans le tableau ci-dessous pour la version CIF que vous utilisez actuellement ou que vous prévoyez d’utiliser à l’avenir.

| Composant | Configuration requise |
|:-------|:-----------------------------------------------------------------------------------------------:|
| Module complémentaire CIF | Minimum : AEM 6.5.18, schémas GraphQL Adobe Commerce 2.3.5 |
| Composants principaux CIF | [Configuration requise](https://github.com/adobe/aem-core-cif-components/blob/master/VERSIONS.md) |
| Archétype de projet AEM | [Configuration requise](https://github.com/adobe/aem-project-archetype/blob/master/VERSIONS.md) |

## Date de publication : octobre 2024

| Composant | Version | Détails |
|:-------|:-------:|-----------------------------------------------------------------------------------------------------------:|
| Composants principaux CIF | 2.15.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.15.0) |

### Correctifs {#bug-fixes-October}

* Correction des tests de l’interface d’utilisation pour qu’ils fonctionnent correctement avec les composants principaux CIF.
* Correction d’un problème en raison duquel le format des URL de catégorie ne fonctionnait pas comme prévu dans l’instance cloud.

## Date de publication : septembre 2024

| Composant | Version | Détails |
|:-------|:-------:|-----------------------------------------------------------------------------------------------------------:|
| Composants principaux CIF | 2.14.2 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.14.2) |

### Améliorations {#improvements-September}

* Rendre la limite de catégorie personnalisable.

### Correctifs {#bug-fixes-September}

* Les champs Commerce ne sont pas correctement intégrés à l’éditeur de schéma de métadonnées Assets.
* Problème de glisser-déposer pour le multichamp Produits du carrousel.
* Problème avec le champ Multichamp de catégorie de carrousel pour le glisser-déposer
* Le fait de cliquer ne fonctionne pas pour les menus dans la page Informations sur la page de l’éditeur de catégories et de produits.
* Le numéro de commande n’est pas visible sur la page de confirmation de commande.

## Date de publication : janvier 2024

| Composant | Version | Détails |
|:-------|:-------:|-----------------------------------------------------------------------------------------------------------:|
| Composants principaux CIF | 2.12.6 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.12.6) |

### Correctifs {#bug-fixes-january}

* Correction du bouton d’ajout au panier et de l’ajout à la liste de souhaits dans le composant de collecte de produits.
