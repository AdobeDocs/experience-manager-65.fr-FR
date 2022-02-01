---
title: Notes de mise à jour d’AEM Content and Commerce 2022
description: Notes de mise à jour d’AEM Content and Commerce 2022
exl-id: ec47c5f8-d4dd-469f-94df-5ee28f25d696
source-git-commit: 26df21270e8c586ba21b9bf3e9fc5003facbaade
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 22%

---

# Présentation de la version GitHub de Commerce Integration Framework

## Présentation de la configuration système requise

Passez en revue la configuration système minimale requise dans le tableau ci-dessous pour la version CIF que vous utilisez actuellement ou que vous prévoyez d’utiliser à l’avenir.

| Composant | Configuration requise |
|:-------|:-----:|
| Module complémentaire CIF | Minimum : AEM 6.5.7, schémas GraphQL Magento 2.3.5 |
| Composants principaux CIF | [Configuration requise](https://github.com/adobe/aem-core-cif-components/blob/master/VERSIONS.md) |
| Archétype de projet AEM | [Configuration requise](https://github.com/adobe/aem-project-archetype/blob/master/VERSIONS.md) |

## Date de publication : Janvier 2022

| Composant | Version | Détails |
|:-------|:-----:|---------------------:|
| Module complémentaire CIF | 2022.01.20.00 | [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.01.20.00.zip) |
| Composants principaux CIF | 2.5.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.5.0) |
| Site de référence CIF Venia | 2022.01.27 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2022.01.27) |

### Nouveautés {#what-is-new-january}

* Amélioration des composants myAccount
* Le composant de recommandation de produit prend en charge d’autres types de page (page d’accueil, panier, confirmation de commande).
* **Liste de souhaits**
   * Les visiteurs connectés peuvent ajouter des produits à une liste bloquée.
   * La gestion de la liste des souhaits et de ses produits est possible via myAccount
   * Le bouton &quot;Ajouter à la liste des souhaits&quot; peut être activé/désactivé au niveau des composants via une stratégie (par exemple, teaser de produit, détails de produit).
   * Disponible en tant que composant principal et dans l’AEM Venia Storefront

![Liste de souhaits](/help/assets/CIF/wishlist.png)

