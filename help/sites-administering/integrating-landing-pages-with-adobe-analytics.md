---
title: Intégration des pages d’entrée à Adobe Analytics
seo-title: Intégration des pages d’entrée à Adobe Analytics
description: Découvrez comment intégrer des pages d’entrée à Adobe Analytics.
seo-description: Découvrez comment intégrer des pages d’entrée à Adobe Analytics.
uuid: 8f6672d1-497f-4ccb-b3cc-f6120fc467ba
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 8ae7ccec-489b-4d20-ac56-6101402fb18a
exl-id: da3f7b7e-87e5-446a-9a77-4b12b850a381
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 48%

---

# Intégration des pages d’entrée à Adobe Analytics{#integrating-landing-pages-with-adobe-analytics}

AEM a intégré la solution des landing pages avec [Adobe Analytics](https://www.omniture.com/en/products/analytics/sitecatalyst) en utilisant les composants CTA (call-to-action) suivants :

1. Composant Lien des clics publicitaires
1. Composant Lien graphique

Ces composants présentent certains attributs qui peuvent être mappés via des variables Adobe Analytics (Trafic, variables de conversion) et des événements de succès pour envoyer des informations à Adobe Analytics.

## Prérequis {#prerequisites}

Adobe vous recommande de passer par l’[intégration existante AEM-Adobe Analytics](/help/sites-administering/adobeanalytics.md) pour comprendre le fonctionnement de cette intégration.

## Composants disponibles pour le mappage {#components-available-for-mapping}

Dans AEM, les composants **Appel à l’action** - **ClickThroughLink** et **GraphicalLink** - affichés ici dans le sidekick, peuvent être mappés à des variables Adobe Analytics.

![chlimage_1-21](assets/chlimage_1-21a.jpeg)

### Mappage de composants de page d’entrée sur Adobe Analytics {#mapping-landing-page-components-to-adobe-analytics}

Pour mapper des composants de page d’entrée sur Adobe Analytics :

1. Après avoir créé la configuration Adobe Analytics et créé une nouvelle structure, sélectionnez la suite de rapports appropriée dans le menu déroulant. Ceci fait, les variables Adobe Analytics sont récupérées et affichées dans l’outil de recherche de contenu.
1. Faites glisser des composants CTA (Appel à l’action) depuis le sidekick vers la zone de mappage située au centre de la page, s’il y a lieu.

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
   <td>Libellé du lien ou texte du lien </td>
  </tr>
  <tr>
   <td><br type="_moz" /> </td>
   <td><i>eventdata.clickthroughLinkTarget</i> <br /> </td>
   <td>Destination à laquelle vous accédez lorsque vous cliquez sur le lien. </td>
  </tr>
  <tr>
   <td><br type="_moz" /> </td>
   <td><i>eventdata.events.clickthroughLinkClick</i> <br /> </td>
   <td>Evénement de clic. </td>
  </tr>
  <tr>
   <td><strong>Lien graphique CTA</strong></td>
   <td><i>eventdata.clickthroughImageLabel</i> <br /> </td>
   <td>Titre de l’image CTA </td>
  </tr>
  <tr>
   <td><br type="_moz" /> </td>
   <td><i>eventdata.clickthroughImageTarget</i> <br /> </td>
   <td>Destination à laquelle vous accédez lorsque vous cliquez sur l’image contenant un lien.</td>
  </tr>
  <tr>
   <td><br type="_moz" /> </td>
   <td><i>eventdata.clickthroughImageAsset</i> <br /> </td>
   <td>Chemin d’accès à la ressource image dans le référentiel </td>
  </tr>
  <tr>
   <td><br type="_moz" /> </td>
   <td><i>eventdata.events.clickthroughImageClick</i> <br /> </td>
   <td>Evénement de clic.</td>
  </tr>
 </tbody>
</table>

1. Mappez ces attributs exposés avec toute variable Adobe Analytics issue du Content Finder. La structure est maintenant prête à être utilisée.
1. Vous pouvez désormais créer une page d’entrée ou ouvrir une page d’entrée existante avec des composants CTA existants, puis cliquer sur l’onglet **Cloud Services** dans **Propriétés de page** dans le sidekick (dans l’IU optimisée pour les écrans tactiles, sélectionnez **Ouvrir les propriétés** et cliquez sur **Cloud Services**) et configurez la structure à utiliser avec la page d’entrée. Sélectionnez la structure dans la liste déroulante.

   ![chlimage_1-25](assets/chlimage_1-25a.png)

1. Après avoir configuré la structure avec la page d’accueil, vous pouvez utiliser les composants instrumentés. Tout clic effectué sur l’appel à l’action est alors enregistré dans Adobe Analytics.
