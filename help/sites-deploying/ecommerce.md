---
title: Aperçu du commerce électronique
seo-title: Aperçu du commerce électronique
description: Le commerce électronique générique AEM est disponible dans le cadre de l’installation standard et vous offre toutes les fonctionnalités de la structure de commerce électronique.
seo-description: Le commerce électronique générique AEM est disponible dans le cadre de l’installation standard et vous offre toutes les fonctionnalités de la structure de commerce électronique.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: e-commerce
content-type: reference
docset: aem65
feature: Commerce Integration Framework
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 56%

---


# Aperçu du commerce électronique{#ecommerce-overview}

Le commerce électronique générique AEM est disponible dans le cadre de l’installation standard et vous offre toutes les fonctionnalités de la structure de commerce électronique.

Adobe propose deux versions de la structure d’intégration de commerce :

|  | CIF sur site | CIF Cloud |
|-------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------|
| Versions d’AEM prises en charge | AEM sur site ou AMS 6.x | AEM AMS 6.4 et 6.5 |
| Back-end | - AEM, Java <br> - Intégration monolithique, mappage de pré-génération (modèle)<br> - référentiel JCR | - Magento <br>- Java et JavaScript <br>- Aucune donnée Commerce stockée dans le référentiel JCR |
| Frontal | Pages rendues côté serveur AEM | Application de page mixte (rendu hybride) |
| Catalogue de produits | - Importateur de produits, éditeur, mise en cache dans AEM <br> - Catalogues réguliers avec des pages AEM ou proxy | - Aucune importation de produit <br>- Modèles génériques <br>- Données à la demande via un connecteur |
| Évolutivité | - Peut prendre en charge jusqu&#39;à quelques millions de produits (selon le cas d&#39;utilisation) <br> - Mise en cache du répartiteur | - Aucune limitation de volume <br> - Mise en cache sur le répartiteur ou le CDN |
| Modèle de données normalisé | Non | Oui, schéma Magento GraphQL |
| Disponibilité | Oui : <br> - Commerce Cloud SAP (Extension mise à jour pour prendre en charge AEM 6.4 et Hybris 5 (par défaut) et conserve la compatibilité avec Hybris 4 <br> - Commerce Cloud Salesforce (Connector open-source pour prendre en charge AEM 6.4) | Oui via open source via GitHub. <br> Magento Commerce (prend en charge Magento 2.3.2 (par défaut) et compatible avec Magento 2.3.1). |
| Quand utiliser la personnalisation | Cas d&#39;utilisation limités : Dans les cas où de petits catalogues statiques peuvent avoir besoin d’être importés | Solution conseillée dans la plupart des cas d’utilisation |


## Déploiement d’autres applications {#deploying-other-implementations}

Pour l&#39;AEM et le Magento, voir [Intégration AEM et Magento](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/integrations.html#!AdobeDocs/commerce-cif-documentation/master/integrations/02-AEM-Magento.md) en utilisant [Commerce Integration Framework](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/integrations.html).

>[!NOTE]
>
>Pour plus d’informations sur les concepts et l’administration des implémentations eCommerce, consultez [Administration d’eCommerce](/help/sites-administering/ecommerce.md).
>
>Pour plus d&#39;informations sur l&#39;extension des capacités de commerce électronique, voir [Développement de l&#39;eCommerce](/help/sites-developing/ecommerce.md).

