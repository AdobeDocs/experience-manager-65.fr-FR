---
title: Migration vers le framework CIF (Commerce Integration Framework) AEM
description: Migrer vers le framework CIF (Commerce Integration Framework) d’AEM à partir d’une ancienne version.
exl-id: c6c0c2fc-6cfa-4c64-b3d8-7e428b2a4b2e
solution: Experience Manager,Commerce
feature: Commerce Integration Framework
role: Admin, Developer
source-git-commit: b4056a4c1483dc8dcedc3c0f8f6b42f8dead0847
workflow-type: ht
source-wordcount: '262'
ht-degree: 100%

---

# Guide de migration pour le module complémentaire Experience Manager {#cif-migration}

Ce guide permet d’identifier les zones à mettre à jour pour la migration du module complémentaire Experience Manager.

## Module complémentaire CIF

Le module complémentaire CIF est également disponible pour AEM 6.5 dans le [portail de distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/fr/aem.html?fulltext=commerce*&amp;2_group.propertyvalues.property=.%2Fjcr%3Acontent%2Fmetadata%2Fdc%3Aversion&amp;2_group.propertyvalues.operation=equals&amp;2_group.propertyvalues.0_values=target-version%3Aaem%2F6-5&amp;orderby=%40jcr%3Acontent%2Fjcr%3AlastModified&amp;orderby.sort=desc&amp;layout=list&amp;p.offset=0&amp;p.limit=16). Il est compatible et fournit les mêmes fonctionnalités que le module complémentaire CIF pour Experience Manager as a Cloud Service.

Consultez la section [Prise en main d’AEM Content and Commerce](getting-started.md).

Pour prendre en charge les projets qui déploient CIF, Adobe fournit [les composants principaux CIF AEM](https://github.com/adobe/aem-core-cif-components).

## Catalogue de produits

L’importation de données de catalogue de produits n’est pas prise en charge par le module complémentaire CIF. L’utilisation du module complémentaire CIF permet aux requêtes produits et de catalogues de se faire sur demande par le biais d’appels en temps réel vers une solution de commerce externe. Accédez au chapitre Intégration pour en savoir plus sur l’intégration d’une solution de commerce.

>[!TIP]
>
>Si aucune API en temps réel n’est disponible, un cache de produit externe doté d’API doit être utilisé pour l’intégration. Exemple de [Magento open-source](https://business.adobe.com/fr/products/magento/open-source.html).

## Expériences de catalogue de produits avec rendu dans AEM

Si vous utilisez le plan directeur de catalogue avec CIF classique, vous devez mettre à jour le workflow du catalogue de produits. Le module complémentaire CIF effectue désormais le rendu à la volée des expériences de catalogue de produits à l’aide de modèles de catalogue AEM. Aucune réplication des données de produit ou des pages de produit n’est désormais nécessaire.

## Données et interaction d’achat non mises en cache

Les requêtes côté client pour les données et interactions non mises en cache (par exemple, l’ajout au panier, la recherche) doivent accéder directement au point d’entrée de commerce (solution de commerce ou couche d’intégration) via le réseau CDN ou le Dispatcher. Supprimez tous les appels pour lesquels AEM servait uniquement de proxy.
