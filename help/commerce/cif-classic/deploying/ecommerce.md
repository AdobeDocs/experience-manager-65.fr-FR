---
title: Aperçu du commerce électronique
seo-title: eCommerce Overview
description: Le commerce électronique générique AEM est disponible dans le cadre de l’installation standard et vous offre toutes les fonctionnalités de la structure de commerce électronique.
seo-description: AEM generic eCommerce is available as part of the standard installation and provides you with the full functionality of the eCommerce framework.
contentOwner: Guillaume Carlino
topic-tags: e-commerce
content-type: reference
docset: aem65
feature: Commerce Integration Framework
exl-id: 3567bd28-73aa-401a-8aa9-a62a99d2a613
source-git-commit: a467009851937c4a10b165a3d253c47bf990bbc5
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 45%

---

# Aperçu  Présentation{#ecommerce-overview}

Le commerce électronique générique AEM est disponible dans le cadre de l’installation standard et vous offre toutes les fonctionnalités de la structure de commerce électronique.

Adobe propose deux versions de la structure d’intégration de commerce :

|  | CIF sur site | CIF Cloud |
|-------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------|
| Versions d’AEM prises en charge | AEM sur site ou AMS 6.x | AEM AMS 6.4 et 6.5 |
| Back-end | - AEM, Java <br> - Intégration monolithique, mappage de prégénération (modèle)<br> - Référentiel JCR | - Adobe Commerce <br>- Java et JavaScript <br>- Aucune donnée Commerce stockée dans le référentiel JCR |
| Frontal | Pages rendues côté serveur AEM | Application de page mixte (rendu hybride) |
| Catalogue de produits | - Importateur de produits, éditeur, mise en cache dans AEM <br>- Catalogues réguliers avec des pages AEM ou proxy | - Pas d’importation de produit <br>- Modèles génériques <br>- Données à la demande via le connecteur |
| Évolutivité | - Peut prendre en charge jusqu’à quelques millions de produits (selon le cas d’utilisation) <br> - Mise en cache sur Dispatcher | - Aucune limitation de volume <br>- Mise en cache sur Dispatcher ou CDN |
| Modèle de données normalisé | Non | Oui, schéma Adobe Commerce GraphQL |
| Disponibilité | Oui :<br> - Commerce Cloud SAP (extension mise à jour pour prendre en charge AEM 6.4 et Hybris 5 (par défaut) et maintenir la compatibilité avec Hybris 4) <br>- Commerce Cloud Salesforce (Connecteur Open Source pour prendre en charge AEM 6.4) | Oui via open source via GitHub. <br> Adobe Commerce (prend en charge la version 2.3.2 (par défaut) et est compatible avec la version 2.3.1). |
| Quand utiliser la personnalisation | Cas d’utilisation limités : Dans les cas où de petits catalogues statiques peuvent avoir besoin d’être importés | Solution conseillée dans la plupart des cas d’utilisation |


## Déploiement d’autres applications {#deploying-other-implementations}

Pour AEM et Adobe Commerce, reportez-vous à la section [Intégration d’AEM et d’Adobe Commerce](/help/commerce/cif/integrating/magento.md) en utilisant la variable [Commerce Integration Framework](/help/commerce/cif/introduction.md).

>[!NOTE]
>
>Pour plus d’informations sur les concepts et l’administration des implémentations eCommerce, consultez [Administration d’eCommerce](/help/commerce/cif-classic/administering/ecommerce.md).
>
>Pour plus d’informations sur l’extension des fonctionnalités d’eCommerce, voir [Développement du commerce électronique](/help/commerce/cif-classic/developing/ecommerce.md).
