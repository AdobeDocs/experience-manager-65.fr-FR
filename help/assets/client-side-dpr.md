---
title: Utilisation de l’imagerie dynamique avec le rapport pixel d’appareil côté client
description: Découvrez comment utiliser le rapport pixel d’appareil côté client avec l’imagerie dynamique dans Adobe Experience Manager as a Cloud Service avec Dynamic Media.
role: Admin,User
exl-id: e38f522a-242a-4ea9-a866-d8d129950831
source-git-commit: c8682118f15132063073df5cdc2b576b6e62a0c8
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 100%

---

# À propos de l’imagerie dynamique avec le rapport pixel d’appareil côté client (DPR) {#client-side-dpr}

La solution d’imagerie dynamique actuelle utilise des chaînes d’agent utilisateur pour déterminer le type d’appareil utilisé (ordinateur de bureau, tablette, mobile, etc.).

Les fonctionnalités de détection d’appareil (DPR basé sur des chaînes d’agent utilisateur) sont souvent inexactes, en particulier pour les périphériques Apple. En outre, chaque fois qu’un nouvel appareil est lancé, il doit être validé.

Le DPR côté client vous donne des valeurs parfaitement précises et fonctionne pour n’importe quel appareil, qu’il s’agisse d’un appareil Apple ou de tout autre nouvel appareil existant.

## Utilisation du code DPR côté client

**Applications rendues côté serveur**

1. Chargez l’initialisation du service worker (`srvinit.js`) en incluant le script suivant dans la section d’en-tête de votre page HTML :

   ```javascript
   <script type="text/javascript" src="srvinit.js"></script>
   ```

   Adobe recommande de charger ce script _avant_ tout autre script de sorte que le service worker commence immédiatement l’initialisation.

1. Insérez le code de balise d’image DPR suivant en haut de la section du corps de votre page de HTML :

   ```html
   <img src="aem_dm_dpr_1x.jpg" style="width:1px;height:1px;display:none"
       srcset="aem_dm_dpr_1x.jpg 1x, aem_dm_dpr_1.1x.jpg 1.1x, aem_dm_dpr_1.2x.jpg 1.2x, aem_dm_dpr_1.3x.jpg 1.3x, aem_dm_dpr_1.4x.jpg 1.4x, aem_dm_dpr_1.5x.jpg 1.5x, aem_dm_dpr_1.6x.jpg 1.6x,          aem_dm_dpr_1.7x.jpg 1.7x, aem_dm_dpr_1.8x.jpg 1.8x, aem_dm_dpr_1.9x.jpg 1.9x,
       aem_dm_dpr_2x.jpg 2x, aem_dm_dpr_2.1x.jpg 2.1x, aem_dm_dpr_2.2x.jpg 2.2x, aem_dm_dpr_2.3x.jpg 2.3x, aem_dm_dpr_2.4x.jpg 2.4x, aem_dm_dpr_2.5x.jpg 2.5x, aem_dm_dpr_2.6x.jpg 2.6x, aem_dm_dpr_2.7x.jpg 2.7x, aem_dm_dpr_2.8x.jpg 2.8x, aem_dm_dpr_2.9x.jpg 2.9x,
       aem_dm_dpr_3x.jpg 3x, aem_dm_dpr_3.1x.jpg 3.1x, aem_dm_dpr_3.2x.jpg 3.2x, aem_dm_dpr_3.3x.jpg 3.3x, aem_dm_dpr_3.4x.jpg 3.4x, aem_dm_dpr_3.5x.jpg 3.5x, aem_dm_dpr_3.6x.jpg 3.6x, aem_dm_dpr_3.7x.jpg 3.7x, aem_dm_dpr_3.8x.jpg 3.8x, aem_dm_dpr_3.9x.jpg 3.9x,
       aem_dm_dpr_4x.jpg 4x, aem_dm_dpr_4.1x.jpg 4.1x, aem_dm_dpr_4.2x.jpg 4.2x, aem_dm_dpr_4.3x.jpg 4.3x, aem_dm_dpr_4.4x.jpg 4.4x, aem_dm_dpr_4.5x.jpg 4.5x, aem_dm_dpr_4.6x.jpg 4.6x, aem_dm_dpr_4.7x.jpg 4.7x, aem_dm_dpr_4.8x.jpg 4.8x, aem_dm_dpr_4.9x.jpg 4.9x,
       aem_dm_dpr_5x.jpg 5x">
   ```

   Il est obligatoire d’inclure ce code de balise d’image DPR _avant_ toutes les images statiques dans votre page de HTML.

**Applications rendues côté client**

1. Insérez les scripts DPR suivants dans la section d’en-tête de votre page HTML :

   ```javascript
   <script type="text/javascript" src="srvinit.js"></script>
   <script type="text/javascript" src="dprImageInjection.js"></script>
   ```

   Vous pouvez combiner les deux scripts DPR dans un seul script afin d’éviter plusieurs requêtes réseau.

   Adobe recommande de charger ces scripts _avant_ tout autre script dans la page HTML.
Adobe recommande également de passer votre application par Bootstrap avec la balise de diff HTML plutôt qu’en tant qu’élément de corps. En effet, `dprImageInjection.js` injecte dynamiquement la balise d’image en haut de la section du corps de la page HTML.

## Téléchargement des fichiers JavaScript {#client-side-dpr-script}

Les fichiers JavaScript suivants à télécharger sont fournis uniquement à titre d’exemple. Si vous envisagez d’utiliser ces fichiers dans des pages HTML, assurez-vous de modifier le code de chaque fichier en fonction de vos besoins.

* `dprImageInjection.js`
* `srvinit.js`
* `srvwrk.js`

[Téléchargement des fichiers JavaScript](/help/assets/assets-dm/aem-dynamicmedia-smartimaging-dpr.zip)

>[!MORELIKETHIS]
>
>* [Imagerie dynamique](/help/assets/imaging-faq.md)

