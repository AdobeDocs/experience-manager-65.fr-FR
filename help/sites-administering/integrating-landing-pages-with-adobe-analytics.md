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
translation-type: tm+mt
source-git-commit: 1c1ade947f2cbd26b35920cfd10b1666b132bcbd
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 48%

---


# Intégration des pages d’entrée à Adobe Analytics{#integrating-landing-pages-with-adobe-analytics}

AEM a intégré la solution landings page avec [Adobe Analytics](https://www.omniture.com/en/products/analytics/sitecatalyst) en utilisant les composants d&#39;appel à l&#39;action suivants :

1. Composant Lien des clics publicitaires
1. Composant Lien graphique

Ces composants exposent certains attributs qui peuvent être mappés via des variables Adobe Analytics (Trafic, variables de conversion) et des événements de réussite pour envoyer des informations à Adobe Analytics.

## Conditions préalables {#prerequisites}

L’Adobe vous recommande de passer par l’[intégration existante AEM-Adobe Analytics](/help/sites-administering/adobeanalytics.md) pour comprendre comment cette intégration fonctionne.

## Composants disponibles pour le mappage {#components-available-for-mapping}

En AEM, les composants **Appel à l&#39;action** - **ClickThroughLink** et **GraphicalLink** - affichés ici dans le sidekick, peuvent être associés à des variables Adobe Analytics.

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
   <td>La destination à laquelle vous accédez lorsque vous cliquez sur le lien </td>
  </tr>
  <tr>
   <td><br type="_moz" /> </td>
   <td><i>eventdata.événements.clickthroughLinkClick</i> <br /> </td>
   <td>Evénement de clic. </td>
  </tr>
  <tr>
   <td><strong>Lien graphique CTA</strong></td>
   <td><i>eventdata.clicktroughImageLabel</i> <br /> </td>
   <td>Titre de l'image CTA </td>
  </tr>
  <tr>
   <td><br type="_moz" /> </td>
   <td><i>eventdata.clicktroughImageTarget</i> <br /> </td>
   <td>Destination à laquelle vous accédez lorsque vous cliquez sur l’image contenant un lien.</td>
  </tr>
  <tr>
   <td><br type="_moz" /> </td>
   <td><i>eventdata.clicktroughImageAsset</i> <br /> </td>
   <td>Chemin d’accès au fichier d’image dans le référentiel </td>
  </tr>
  <tr>
   <td><br type="_moz" /> </td>
   <td><i>eventdata.événements.clicktroughImageClick</i> <br /> </td>
   <td>Evénement de clic.</td>
  </tr>
 </tbody>
</table>

1. Mappez ces attributs exposés avec toute variable Adobe Analytics issue du Content Finder. La structure est maintenant prête à être utilisée.
1. Vous pouvez maintenant créer un landing page ou ouvrir un landing page existant avec des composants CTA existants et cliquer sur **Cloud Services** dans **Propriétés de la page** dans le panneau latéral (dans l&#39;IU optimisée pour les écrans tactiles, sélectionnez **Ouvrir les propriétés**, puis cliquez sur **Cloud Services**) et configurer la structure à utiliser avec le landing page. Sélectionnez la structure dans la liste déroulante.

   ![chlimage_1-25](assets/chlimage_1-25a.png)

1. Après avoir configuré la structure avec la page d’accueil, vous pouvez utiliser les composants instrumentés. Tout clic effectué sur l’appel à l’action est alors enregistré dans Adobe Analytics.

