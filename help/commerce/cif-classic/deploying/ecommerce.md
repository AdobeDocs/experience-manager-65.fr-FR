---
title: Présentation du commerce électronique
description: AEM eCommerce générique est disponible dans le cadre de l’installation standard et vous fournit toutes les fonctionnalités de la structure eCommerce.
feature: Commerce Integration Framework
exl-id: 3567bd28-73aa-401a-8aa9-a62a99d2a613
source-git-commit: eaffc71c23c18d26ec5cbb2bbb7524790c4826fe
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 85%

---

# Présentation du commerce électronique{#ecommerce-overview}

Le commerce électronique générique AEM est disponible dans le cadre de l’installation standard et vous offre toutes les fonctionnalités de la structure de commerce électronique.

Adobe propose deux versions de framework d’intégration de Commerce :

|                         | CIF on-Prem | CIF Cloud |
|-------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------|
| Versions d’AEM prises en charge | AEM On-Prem ou AMS 6.x | AEM AMS 6.4 et 6.5 |
| Back-end | - AEM, Java <br> - Intégration monolithique, mappage de prégénération (modèle)<br> - Référentiel JCR | - ADOBE COMMERCE <br>- Java et JavaScript <br>- Aucune donnée Commerce stockée dans le référentiel JCR |
| Front-end | Pages générées côté serveur AEM | Application de page mixte (rendu hybride) |
| Catalogue de produits | - Importateur de produits, éditeur, mise en cache dans AEM <br>- Catalogues réguliers avec des pages AEM ou proxy | - Pas d’importation de produit <br>- Modèles génériques <br>- Données à la demande via le connecteur |
| Évolutivité | - Peut prendre en charge jusqu’à quelques millions de produits (selon le cas d’utilisation) <br> - Mise en cache sur Dispatcher | - Aucune limitation de volume <br>- Mise en cache sur Dispatcher ou CDN |
| Modèle de données normalisé | Non | Oui, schéma Adobe Commerce GraphQL |
| Disponibilité | Oui :<br> - Commerce Cloud SAP (extension mise à jour pour prendre en charge AEM 6.4 et Hybris 5 (par défaut) et maintenir la compatibilité avec Hybris 4) <br>- Commerce Cloud Salesforce (connecteur open-source pour prendre en charge AEM 6.4) | Oui, en open source via GitHub. <br> Adobe Commerce (prend en charge la version 2.3.2 (par défaut) et compatible avec la version 2.3.1) |
| Quand l’utiliser | Cas d’utilisation limités : dans le cas de scénarios dans lesquels de petits catalogues statiques doivent être importés | Solution préférée dans la plupart des cas d’utilisation |


## Déploiement d’autres mises en oeuvre {#deploying-other-implementations}

Pour AEM et Adobe Commerce, consultez [Intégration d’AEM et d’Adobe Commerce](/help/commerce/cif/integrating/magento.md) à l’aide du [framework d’intégration de Commerce (CIF)](/help/commerce/cif/introduction.md).

>[!NOTE]
>
>Pour plus d’informations sur les concepts et l’administration des implémentations eCommerce, consultez [Administration d’eCommerce](/help/commerce/cif-classic/administering/ecommerce.md).
>
>Pour plus d’informations sur les possibilités d’extension d’eCommerce, consultez [Développement du e-commerce](/help/commerce/cif-classic/developing/ecommerce.md).
