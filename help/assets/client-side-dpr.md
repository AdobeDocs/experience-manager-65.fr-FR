---
title: Utilisation de l’imagerie dynamique avec rapport des pixels côté client
description: Découvrez comment utiliser le rapport de pixels d’appareil côté client avec l’imagerie dynamique dans Adobe Experience Manager as a Cloud Service avec Dynamic Media.
role: Admin,User
exl-id: e38f522a-242a-4ea9-a866-d8d129950831
solution: Experience Manager, Experience Manager Assets
feature: Smart Imaging
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: d09181b5-a36a-43de-ba01-36641440bc43
    internal-label: Experience Manager Assets
feature_v2:
  - id: bd0d2470-932c-4269-8eca-6d939b72d9ef
    internal-label: Dynamic Media
subfeature_v2:
  - id: b39a6d56-d787-413f-8024-351803c28d44
    internal-label: Smart Imaging
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '328'
ht-degree: 100%
---
# À propos de l’imagerie dynamique avec rapport des pixels d’appareil côté client (RPD) {#client-side-dpr}

La solution d’imagerie dynamique actuelle utilise des chaînes d’agent utilisateur pour déterminer le type d’appareil utilisé (ordinateur de bureau, tablette, mobile, etc.).

Les fonctionnalités de détection d’appareil (RGPD basées sur des chaînes d’agent utilisateur) sont souvent inexactes, en particulier pour les appareils Apple. En outre, chaque fois qu’un nouvel appareil est lancé, il doit être validé.

Le RGPD côté client vous donne des valeurs et fonctionne entièrement exacts pour n’importe quel appareil, qu’il s’agisse d’Apple ou de tout autre nouvel appareil qui a été lancé.

## Utilisation du code DPR côté client

**Applications rendues côté serveur**

1. Chargement de l’init du service worker (`srvinit.js`) en incluant le script suivant dans la section d’en-tête de votre page de HTML :

   ```javascript
   <script type="text/javascript" src="srvinit.js"></script>
   ```

   Adobe recommande de charger ce script _avant_ tout autre script, de sorte que le service worker commence immédiatement l’initialisation.

1. Insérez le code de balise d’image DPR suivant en haut de la section corps de votre page de HTML :

   ```html
   <img src="aem_dm_dpr_1x.jpg" style="width:1px;height:1px;display:none"
       srcset="aem_dm_dpr_1x.jpg 1x, aem_dm_dpr_1.1x.jpg 1.1x, aem_dm_dpr_1.2x.jpg 1.2x, aem_dm_dpr_1.3x.jpg 1.3x, aem_dm_dpr_1.4x.jpg 1.4x, aem_dm_dpr_1.5x.jpg 1.5x, aem_dm_dpr_1.6x.jpg 1.6x,          aem_dm_dpr_1.7x.jpg 1.7x, aem_dm_dpr_1.8x.jpg 1.8x, aem_dm_dpr_1.9x.jpg 1.9x,
       aem_dm_dpr_2x.jpg 2x, aem_dm_dpr_2.1x.jpg 2.1x, aem_dm_dpr_2.2x.jpg 2.2x, aem_dm_dpr_2.3x.jpg 2.3x, aem_dm_dpr_2.4x.jpg 2.4x, aem_dm_dpr_2.5x.jpg 2.5x, aem_dm_dpr_2.6x.jpg 2.6x, aem_dm_dpr_2.7x.jpg 2.7x, aem_dm_dpr_2.8x.jpg 2.8x, aem_dm_dpr_2.9x.jpg 2.9x,
       aem_dm_dpr_3x.jpg 3x, aem_dm_dpr_3.1x.jpg 3.1x, aem_dm_dpr_3.2x.jpg 3.2x, aem_dm_dpr_3.3x.jpg 3.3x, aem_dm_dpr_3.4x.jpg 3.4x, aem_dm_dpr_3.5x.jpg 3.5x, aem_dm_dpr_3.6x.jpg 3.6x, aem_dm_dpr_3.7x.jpg 3.7x, aem_dm_dpr_3.8x.jpg 3.8x, aem_dm_dpr_3.9x.jpg 3.9x,
       aem_dm_dpr_4x.jpg 4x, aem_dm_dpr_4.1x.jpg 4.1x, aem_dm_dpr_4.2x.jpg 4.2x, aem_dm_dpr_4.3x.jpg 4.3x, aem_dm_dpr_4.4x.jpg 4.4x, aem_dm_dpr_4.5x.jpg 4.5x, aem_dm_dpr_4.6x.jpg 4.6x, aem_dm_dpr_4.7x.jpg 4.7x, aem_dm_dpr_4.8x.jpg 4.8x, aem_dm_dpr_4.9x.jpg 4.9x,
       aem_dm_dpr_5x.jpg 5x">
   ```

   Il est obligatoire d’inclure ce code de balise d’image RGPD _avant_ toutes les images statiques dans votre page de HTML.

**Applications rendues côté client**

1. Insérez les scripts DPR suivants dans la section d’en-tête de votre page de HTML :

   ```javascript
   <script type="text/javascript" src="srvinit.js"></script>
   <script type="text/javascript" src="dprImageInjection.js"></script>
   ```

   Vous pouvez combiner les deux scripts DPR en un seul afin d’éviter plusieurs requêtes réseau.

   Adobe recommande de charger ces scripts _avant_ tout autre script dans la page de HTML.
   Adobe recommande également le Bootstrap de votre application sous la balise de HTML diff plutôt qu’un élément de corps. La raison en est la suivante : `dprImageInjection.js` injecte dynamiquement la balise d’image dans la partie supérieure de la section corps de la page HTML.

## Téléchargement des fichiers JavaScript {#client-side-dpr-script}

Les fichiers JavaScript suivants sont fournis à titre de référence uniquement dans le cadre du téléchargement. Si vous envisagez d’utiliser ces fichiers dans des pages de HTML, veillez à modifier le code de chaque fichier en fonction de vos besoins.

* `dprImageInjection.js`
* `srvinit.js`
* `srvwrk.js`

[Téléchargement des fichiers JavaScript](/help/assets/assets-dm/aem-dynamicmedia-smartimaging-dpr.zip)

>[!MORELIKETHIS]
>
>* [Imagerie dynamique](/help/assets/imaging-faq.md)
