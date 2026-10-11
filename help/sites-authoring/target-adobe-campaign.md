---
title: Cibler votre campagne Adobe Campaign
description: Vous pouvez créer des expériences ciblées pour Adobe Campaign après avoir configuré la segmentation.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
exl-id: fc6fccba-41c5-4c13-aac0-b4ef67767abe
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Personalization,Integration
role: User,Admin,Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: e2c1b6d3-bb7e-4fe8-8c72-f7b403298e91
    internal-label: Authoring
  - id: eb3ad9f8-54a2-45f3-abb1-d3976415a718
    internal-label: Personalization
  - id: 243139ec-8e41-5296-a287-31343ab1bc0f
    internal-label: Integration
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 751e1826ed53df7522418e50a206f0fe622256a4
workflow-type: tm+mt
source-wordcount: '429'
ht-degree: 100%
---
# Cibler votre campagne Adobe Campaign{#targeting-your-adobe-campaign}

Pour cibler votre newsletter Adobe Campaign, vous devez d’abord configurer la segmentation, qui n’est disponible que dans l’UI classique (pour le contexte client). Ensuite, vous pouvez créer des expériences ciblées pour Adobe Campaign. Ces deux opérations sont décrites dans cette section.

## Configurer la segmentation dans AEM {#setting-up-segmentation-in-aem}

Pour configurer la segmentation, vous devez utiliser l’UI classique pour configurer les segments. Les étapes restantes peuvent être effectuées dans l’UI standard.

La configuration de la segmentation comprend la création de segments, d’une marque, d’une campagne et d’expériences.

>[!NOTE]
>
>L’ID de segment doit être mappé sur celui du côté Adobe Campaign.

### Créer des segments {#creating-segments}

Pour créer des segments :

1. Ouvrez la [console de segmentation](http://localhost:4502/miscadmin#/etc/segmentation) à l’adresse **&lt;host>:&lt;port>/miscadmin#/etc/segmentation**.
1. Créez une page et saisissez un titre, par exemple, **Segments AC**, puis sélectionnez le modèle **Segment (Adobe Campaign)**.
1. Sélectionnez la page créée dans l’arborescence située à gauche.
1. Créez un segment, par exemple ciblant les utilisateurs masculins, en créant une page sous le segment que vous avez créé, appelé Masculin, puis sélectionnez le modèle **Segment (Adobe Campaign)**.
1. Ouvrez la page de segment créée et effectuez un glisser-déposer d’un **identifiant de segment** du sidekick sur la page.
1. Double-cliquez sur la caractéristique, entrez l’ID représentant le segment Masculin défini dans Adobe Campaign, par exemple, **MASCULIN**, puis cliquez sur **OK**. Le message suivant doit apparaître : *`targetData.segmentCode == "MALE"`*
1. Répétez les étapes pour un autre segment, par exemple un segment ciblant les utilisatrices.

### Créer une marque {#creating-a-brand}

Pour créer une marque :

1. Dans **Sites**, accédez au dossier **Campagnes** (par exemple dans We.Retail).
1. Cliquez sur **Créer une page** et entrez le titre de la page, par exemple Marque We.Retail, puis sélectionnez le modèle **Marque**.

### Créer une campagne {#creating-a-campaign}

Pour créer une campagne :

1. Ouvrez la page **Marque** que vous venez de créer.
1. Cliquez sur **Créer une page** et saisissez un titre pour votre page, par exemple, Campagne We.Retail, puis sélectionnez le modèle **Campagne** et cliquez sur **Créer**.

### Créer des expériences {#creating-experiences}

Pour créer des expériences pour les segments :

1. Ouvrez la page **Campagne** que vous venez de créer.
1. Créez des expériences pour vos segments en cliquant sur **Créer une page** et entrez le titre de la page, par exemple, Masculin puisque vous créez une expérience pour le segment Masculin, puis sélectionnez le modèle **Expérience**.
1. Ouvrez la page Expérience créée.
1. Cliquez sur **Modifier**, puis sous Segments, cliquez sur **Ajouter un élément**.
1. Entrez le chemin du segment Masculin, par exemple **/etc/segmentation/ac-segments/masculin** et cliquez sur **OK**. Le message suivant apparaît : *Expérience ciblée sur : Masculin*.
1. Répétez les étapes précédentes pour créer une expérience pour tous les segments, par exemple la cible féminine.
