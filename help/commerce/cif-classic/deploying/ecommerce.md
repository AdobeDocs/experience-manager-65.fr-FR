---
title: Présentation du commerce électronique
description: L’e-commerce générique AEM est disponible dans le cadre de l’installation standard et vous offre toutes les fonctionnalités de la structure d’e-commerce.
feature: Commerce Integration Framework
exl-id: 3567bd28-73aa-401a-8aa9-a62a99d2a613
source-git-commit: f349c8fd9c370ba589d217cd3b1d0521ae5c5597
workflow-type: tm+mt
source-wordcount: '268'
ht-degree: 86%

---

# Présentation du commerce électronique{#ecommerce-overview}

Le commerce électronique générique AEM est disponible dans le cadre de l’installation standard et vous offre toutes les fonctionnalités de la structure de commerce électronique.

Adobe propose deux versions de framework d’intégration de Commerce :

|                         | CIF on-Prem | CIF Cloud |
|-------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------|
| Versions d’AEM prises en charge | AEM On-Prem ou AMS 6.x | AEM AMS 6.4 et 6.5 |
| Back-end | - AEM, Java™ <br> - Intégration monolithique, mappage de prégénération (modèle)<br> - référentiel JCR | - Adobe Commerce <br>- Java et JavaScript <br>- Aucune donnée Commerce stockée dans le référentiel JCR |
| Front-end | Pages générées côté serveur AEM | Application de page mixte (rendu hybride) |
| Catalogue de produits | - Importateur de produits, éditeur, mise en cache dans AEM <br>- Catalogues réguliers avec des pages AEM ou proxy | - Pas d’importation de produit <br>- Modèles génériques <br>- Données à la demande via le connecteur |
| Évolutivité | - Peut prendre en charge jusqu’à quelques millions de produits (selon le cas d’utilisation) <br> - Mise en cache sur Dispatcher | - Aucune limitation de volume <br>- Mise en cache sur Dispatcher ou CDN |
| Modèle de données normalisé | Non | Oui, schéma Adobe Commerce GraphQL |
| Disponibilité | Oui :<br> - Commerce Cloud SAP (extension mise à jour pour prendre en charge AEM 6.4 et Hybris 5 (par défaut) et maintenir la compatibilité avec Hybris 4) <br>- Commerce Cloud Salesforce (connecteur open-source pour prendre en charge AEM 6.4) | Oui, en open source via GitHub. <br> Adobe Commerce (prend en charge la version 2.3.2 (par défaut) et compatible avec la version 2.3.1) |
| Quand l’utiliser | Cas d’utilisation limités : dans les cas où de petits catalogues statiques sont importés si nécessaire | Solution préférée dans la plupart des cas d’utilisation |


## Déploiement d’autres mises en œuvre {#deploying-other-implementations}

Pour AEM et Adobe Commerce, voir [Intégration AEM et Adobe Commerce](/help/commerce/cif/integrating/magento.md) en utilisant la variable [Commerce integration framework](/help/commerce/cif/introduction.md).

>[!NOTE]
>
>Pour plus d’informations sur les concepts et l’administration des implémentations eCommerce, consultez [Administration d’eCommerce](/help/commerce/cif-classic/administering/ecommerce.md).
>
>Pour plus d’informations sur les possibilités d’extension d’eCommerce, consultez [Développement du e-commerce](/help/commerce/cif-classic/developing/ecommerce.md).
