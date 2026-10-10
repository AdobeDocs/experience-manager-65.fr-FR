---
title: Intégration des pages de destination à Adobe Analytics
description: Découvrez comment intégrer des pages de destination à Adobe Analytics.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
exl-id: da3f7b7e-87e5-446a-9a77-4b12b850a381
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Admin
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: 243139ec-8e41-5296-a287-31343ab1bc0f
    internal-label: Integration
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 100%
---
# Intégration des pages de destination à Adobe Analytics{#integrating-landing-pages-with-adobe-analytics}

AEM a intégré la solution des pages de destination à [Adobe Analytics](https://www.omniture.com/en/products/analytics/sitecatalyst) en utilisant les composants CTA suivants :

1. Composant Clic publicitaire
1. Composant Lien graphique

Ces composants exposent certains attributs pouvant être mappés via les variables Adobe Analytics (variables de trafic, de conversion) et des événements de réussite pour envoyer des informations à Adobe Analytics.

## Prérequis {#prerequisites}

Adobe vous recommande de passer en revue l’[intégration AEM-Adobe Analytics existante](/help/sites-administering/adobeanalytics.md) pour en comprendre le fonctionnement.

## Composants disponibles pour le mappage {#components-available-for-mapping}

Dans AEM, les composants **Appel à l’action** (**ClickThroughLink** et **GraphicalLink**) affichés ici dans le sidekick peuvent être mappés sur des variables Adobe Analytics.

![chlimage_1-21](assets/chlimage_1-21a.jpeg)

### Mappage des composants Page de destination à Adobe Analytics {#mapping-landing-page-components-to-adobe-analytics}

Pour mapper des composants Page de destination à Adobe Analytics :

1. Après avoir créé la configuration Adobe Analytics ainsi qu’un nouveau framework, sélectionnez la suite de rapports appropriée dans le menu déroulant. Les variables Adobe Analytics sont alors récupérées et affichées dans l’outil de recherche de contenu.
1. Faites glisser les composants CTA (appel à l’action) du sidekick vers la zone de mappage située au milieu de la page, le cas échéant.

<table>
 <tbody>
  <tr>
   <td><strong>Nom du composant</strong></td>
   <td><strong>Attributs présentés</strong></td>
   <td><strong>Signification de l’attribut</strong></td>
  </tr>
  <tr>
   <td><strong>Lien des clics publicitaires CTA</strong></td>
   <td><i>eventdata.clickthroughLinkLabel</i> <br /> </td>
   <td>Libellé ou texte du lien </td>
  </tr>
  <tr>
   <td><br type="_moz" /> </td>
   <td><i>eventdata.clickthroughLinkTarget</i> <br /> </td>
   <td>Destination à laquelle vous accédez lorsque vous cliquez sur le lien. </td>
  </tr>
  <tr>
   <td><br type="_moz" /> </td>
   <td><i>eventdata.events.clickthroughLinkClick</i> <br /> </td>
   <td>Événement de clic </td>
  </tr>
  <tr>
   <td><strong>Lien graphique CTA</strong></td>
   <td><i>eventdata.clicktroughImageLabel</i> <br /> </td>
   <td>Titre de l’image CTA </td>
  </tr>
  <tr>
   <td><br type="_moz" /> </td>
   <td><i>eventdata.clicktroughImageTarget</i> <br /> </td>
   <td>Destination à laquelle vous accédez lorsque vous cliquez sur l’image contenant un lien.</td>
  </tr>
  <tr>
   <td><br type="_moz" /> </td>
   <td><i>eventdata.clicktroughImageAsset</i> <br /> </td>
   <td>Chemin d’accès à la ressource image dans le référentiel </td>
  </tr>
  <tr>
   <td><br type="_moz" /> </td>
   <td><i>eventdata.events.clicktroughImageClick</i> <br /> </td>
   <td>Événement de clic</td>
  </tr>
 </tbody>
</table>

1. Mappez ces attributs exposés avec toute variable Adobe Analytics issue de l’outil de recherche de contenu. Le framework est maintenant prêt à être utilisé.
1. Vous pouvez à présent créer une nouvelle page de destination ou en ouvrir une existante avec des composants CTA existants et cliquer sur l’onglet **Services cloud** dans **Propriétés de page** dans le sidekick (dans l’IU optimisée pour les écrans tactiles, sélectionnez **Ouvrir les propriétés** et cliquez sur **Services cloud**), puis configurer le framework à utiliser avec la page de destination. Sélectionnez le framework dans la liste déroulante.

   ![chlimage_1-25](assets/chlimage_1-25a.png)

1. Après avoir configuré le framework avec la page de destination, vous pouvez utiliser les composants activés. Tout clic effectué sur l’appel à l’action est alors enregistré dans Adobe Analytics.
