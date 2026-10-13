---
title: Présentation du commerce électronique
description: L’e-commerce générique AEM est disponible dans le cadre de l’installation standard et vous offre toutes les fonctionnalités de la structure d’e-commerce.
feature: Commerce Integration Framework
exl-id: 3567bd28-73aa-401a-8aa9-a62a99d2a613
solution: Experience Manager,Commerce
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
source-wordcount: '278'
ht-degree: 97%
---
# Présentation du commerce électronique{#ecommerce-overview}

Le commerce électronique générique AEM est disponible dans le cadre de l’installation standard et vous offre toutes les fonctionnalités de la structure de commerce électronique.

Adobe propose deux versions de Commerce integration framework :

|                         | CIF on-Prem | CIF Cloud |
|-------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------|
| Versions d’AEM prises en charge | AEM On-Prem ou AMS 6.x | AEM AMS 6.4 et 6.5 |
| Back-end | - AEM, Java™ <br> - Intégration monolithique, mappage de prégénération (modèle)<br> - Référentiel JCR | - Adobe Commerce <br>- Java et JavaScript <br>- Aucune donnée Commerce stockée dans le référentiel JCR |
| Front-end | Pages générées côté serveur AEM | Application de page mixte (rendu hybride) |
| Catalogue de produits | - Importateur de produits, éditeur, mise en cache dans AEM <br>- Catalogues réguliers avec des pages AEM ou proxy | - Pas d’importation de produit <br>- Modèles génériques <br>- Données à la demande via le connecteur |
| Évolutivité | - Peut prendre en charge jusqu’à quelques millions de produits (selon le cas d’utilisation) <br> - Mise en cache sur Dispatcher | - Aucune limitation de volume <br>- Mise en cache sur Dispatcher ou CDN |
| Modèle de données normalisé | Non | Oui, schéma Adobe Commerce GraphQL |
| Disponibilité | Oui :<br> - Commerce Cloud SAP (extension mise à jour pour prendre en charge AEM 6.4 et Hybris 5 (par défaut) et maintenir la compatibilité avec Hybris 4) <br>- Commerce Cloud Salesforce (connecteur open-source pour prendre en charge AEM 6.4) | Oui, en open source via GitHub. <br> Adobe Commerce (prend en charge la version 2.3.2 (par défaut) et compatible avec la version 2.3.1) |
| Quand l’utiliser | Cas d’utilisation limités : dans le cas de scénarios d’importations de petits catalogues statiques | Solution préférée dans la plupart des cas d’utilisation |


## Déploiement d’autres mises en œuvre {#deploying-other-implementations}

Pour AEM et Adobe Commerce, consultez [Intégration d’AEM et d’Adobe Commerce](/help/commerce/cif/integrating/magento.md) à l’aide de [Commerce integration framework (CIF)](/help/commerce/cif/introduction.md).

>[!NOTE]
>
>Pour plus d’informations sur les concepts et l’administration des implémentations eCommerce, consultez [Administration d’eCommerce](/help/commerce/cif-classic/administering/ecommerce.md).
>
>Pour plus d’informations sur les possibilités d’extension d’eCommerce, consultez [Développement du e-commerce](/help/commerce/cif-classic/developing/ecommerce.md).
