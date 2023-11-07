---
title: Intégration des pages de destination à Adobe Analytics
seo-title: Integrating Landing Pages with Adobe Analytics
description: Découvrez comment intégrer des landing pages à Adobe Analytics.
seo-description: Learn how to integrate landing pages with Adobe Analytics.
uuid: 8f6672d1-497f-4ccb-b3cc-f6120fc467ba
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 8ae7ccec-489b-4d20-ac56-6101402fb18a
exl-id: da3f7b7e-87e5-446a-9a77-4b12b850a381
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 63%

---

# Intégration des pages de destination à Adobe Analytics{#integrating-landing-pages-with-adobe-analytics}

AEM a intégré la solution des pages de destination à [Adobe Analytics](https://www.omniture.com/en/products/analytics/sitecatalyst) en utilisant les composants CTA (call-to-action) suivants :

1. Composant Clic publicitaire
1. Composant de lien graphique

Ces composants exposent certains attributs pouvant être mappés via les variables Adobe Analytics (variables de trafic, de conversion) et des événements de réussite pour envoyer des informations à Adobe Analytics.

## Prérequis {#prerequisites}

Adobe vous recommande de passer en revue l’[intégration AEM-Adobe Analytics existante](/help/sites-administering/adobeanalytics.md) pour en comprendre le fonctionnement.

## Composants disponibles pour le mappage {#components-available-for-mapping}

Dans AEM, les composants **Appel à l’action** (**ClickThroughLink** et **GraphicalLink**) affichés ici dans le sidekick peuvent être mappés sur des variables Adobe Analytics.

![chlimage_1-21](assets/chlimage_1-21a.jpeg)

### Mappage des composants de page d’entrée à Adobe Analytics {#mapping-landing-page-components-to-adobe-analytics}

Pour mapper des composants de page d’entrée à Adobe Analytics :

1. Après avoir créé la configuration Adobe Analytics et créé une structure, sélectionnez la suite de rapports appropriée dans le menu déroulant. Les variables Adobe Analytics sont alors récupérées et affichées dans l’outil de recherche de contenu.
1. Faites glisser les composants CTA (Appel à l’action) du sidekick vers la zone de mappage située au milieu de la page, le cas échéant.

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
   <td>Destination à laquelle vous accédez lorsque vous cliquez sur le lien </td>
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
1. Vous pouvez maintenant créer une landing page ou ouvrir une landing page existante avec des composants CTA existants, puis cliquer sur **Cloud Service** dans **Propriétés de la page** dans le sidekick (dans l’IU optimisée pour les écrans tactiles, sélectionnez **Ouvrir les propriétés** et cliquez sur **Cloud Service**) et configurez la structure à utiliser avec la landing page. Sélectionnez le framework dans la liste déroulante.

   ![chlimage_1-25](assets/chlimage_1-25a.png)

1. Après avoir configuré le framework avec la page de destination, vous pouvez utiliser les composants activés. Tout clic effectué sur l’appel à l’action est alors enregistré dans Adobe Analytics.
