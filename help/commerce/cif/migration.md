---
title: Migration vers le module complémentaire AEM Commerce Integration Framework (CIF)
description: Comment migrer vers le module complémentaire AEM Commerce Integration Framework (CIF) à partir d’une ancienne version
translation-type: tm+mt
source-git-commit: da538dac17b4c6182b44801b4c79d6cdbf35f640
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 4%

---

# Guide de migration pour l&#39;Ajoute Experience Manager {#cif-migration}

Ce guide vous aide à identifier les zones à mettre à jour pour la migration des modules complémentaires Experience Manager.

## AJOUTE CIF

Le module complémentaire CIF est disponible pour AEM 6.5 via le [portail de distribution de logiciels](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html). Il est compatible et offre les mêmes fonctionnalités que le module complémentaire CIF pour Experience Manager en tant que Cloud Service.

Voir [Prise en main du contenu et du commerce AEM](getting-started.md).

Pour soutenir des projets de déploiement du FIC, Adobe fournit [AEM CIF Core Components](https://github.com/adobe/aem-core-cif-components).

## Catalogue de produits

L’importation de données de catalogue de produits n’est pas prise en charge par le module complémentaire CIF. En utilisant les identifiants de module complémentaire CIF, les demandes de produits et de catalogues sont à la demande via des appels en temps réel vers une solution de commerce externe. Accédez au chapitre Intégration pour en savoir plus sur l&#39;intégration d&#39;une solution commerciale.

>[!TIP]
>
>Si aucune API en temps réel n’est disponible, un cache de produit externe avec des API doit être utilisé pour l’intégration. Exemple [Magento open-source](https://magento.com/products/magento-open-source).

## Expériences du catalogue de produits avec rendu AEM

Si vous utilisez le modèle de catalogue avec CIF classique, vous devez mettre à jour le processus du catalogue de produits. Le module complémentaire CIF effectue désormais le rendu en temps réel des expériences de catalogue de produits à l’aide de modèles de catalogue AEM. Aucune réplication des données de produit ou des pages de produits n’est plus requise.

## Interaction entre les données non mises en cache et les achats

Les demandes côté client pour des données et interactions non mises en cache (par exemple, ajouts au panier, recherche) doivent être envoyées directement au point de terminaison du commerce (solution commerciale ou couche d’intégration) via CDN / Répartiteur. Supprimez les appels pour lesquels AEM n&#39;était qu&#39;un proxy.
