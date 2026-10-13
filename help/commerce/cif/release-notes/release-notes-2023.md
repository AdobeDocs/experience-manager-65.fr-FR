---
title: Notes de mise à jour d’AEM Content and Commerce 2023
description: Notes de mise à jour d’Adobe Experience Manager Content and Commerce 2023.
exl-id: 00349400-6860-4e3c-ba56-fa12afc5db1d
solution: Experience Manager,Commerce
feature: Commerce Integration Framework
role: Admin, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 100%
---
# Vue d’ensemble de la version GitHub de Commerce Integration Framework

## Présentation de la configuration système requise

Passez en revue la configuration système minimale requise dans le tableau ci-dessous pour la version CIF que vous utilisez actuellement ou que vous prévoyez d’utiliser à l’avenir.

| Composant | Configuration requise |
|:-------|:-----------------------------------------------------------------------------------------------:|
| Module complémentaire CIF | Minimum : AEM 6.5.8, schémas GraphQL Adobe Commerce 2.3.5 |
| Composants principaux CIF | [Configuration requise](https://github.com/adobe/aem-core-cif-components/blob/master/VERSIONS.md) |
| Archétype de projet AEM | [Configuration requise](https://github.com/adobe/aem-project-archetype/blob/master/VERSIONS.md) |

## Date de publication : décembre 2023

| Composant | Version | Détails |
|:-------|:-------:|-----------------------------------------------------------------------------------------------------------:|
| Composants principaux CIF | 2.12.4 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.12.4) |

### Correctifs {#bug-fixes-december}

* Servlets de redirection de produit et de catégorie enregistrés pour le type de ressource Page v3
* Correction des événements de recherche en direct de l’extension AEP CIF

## Date de publication : novembre 2023

| Composant | Version | Détails |
|:-------|:-------------:|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|
| Module complémentaire CIF | 2023.11.23.00 | [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2023.11.23.00.zip) |
| Site de référence CIF Venia | 2023.11.08 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2023.11.08) |

### Correctifs {#bug-fixes-november}

* Affichage de plus de 40 configurations dans la console de configurations CIF

## Date de publication : juillet 2023

| Composant | Version | Détails |
|:-------|:-------:|--------------------------------------------------------------------------------------------------------------:|
| Composants principaux CIF | 2.12.2 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.12.2) |

### Nouveautés {#what-is-new-july}

* Hooks de filtre de produit dans le composant `ProductList`
