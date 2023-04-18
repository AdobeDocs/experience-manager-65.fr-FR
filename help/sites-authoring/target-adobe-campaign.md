---
title: Ciblage de votre Adobe Campaign
description: Vous pouvez créer des expériences ciblées pour Adobe Campaign après avoir configuré la segmentation.
uuid: 8fcc9210-d8c5-44e3-8aa8-6c6db810c98e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
discoiquuid: f1cb5e98-ccd1-4b2c-acca-2b3cc1b7ac5f
exl-id: fc6fccba-41c5-4c13-aac0-b4ef67767abe
source-git-commit: f4b6eb2ded17ec641f23a1fc3b977ce77169c8a1
workflow-type: tm+mt
source-wordcount: '811'
ht-degree: 45%

---

# Cibler votre campagne Adobe Campaign{#targeting-your-adobe-campaign}

Pour cibler votre newsletter Adobe Campaign, vous devez d’abord configurer la segmentation, qui n’est disponible que dans l’interface utilisateur classique (pour le contexte client). Ensuite, vous pouvez créer des expériences ciblées pour Adobe Campaign. Les deux sont décrits dans cette section.

## Configuration de la segmentation dans AEM {#setting-up-segmentation-in-aem}

Pour configurer la segmentation, vous devez utiliser l’interface utilisateur classique pour configurer les segments. Les étapes restantes peuvent être effectuées dans l’interface utilisateur standard.

La configuration de la segmentation comprend la création de segments, d’une marque, d’une campagne et d’expériences.

>[!NOTE]
>
>L’ID de segment doit être mappé sur celui du côté Adobe Campaign.

### Création de segments {#creating-segments}

Pour créer des segments :

1. Ouvrez la [console de segmentation](http://localhost:4502/miscadmin#/etc/segmentation) à l’adresse **&lt;host>:&lt;port>/miscadmin#/etc/segmentation**.
1. Créez une page et saisissez un titre, par exemple, **Segments AC** et sélectionnez le modèle **Segment (Adobe Campaign)**.
1. Sélectionnez la page créée dans l’arborescence située à gauche.
1. Créez un segment, par exemple en ciblant les utilisateurs masculins, en créant une page sous le segment que vous avez créé, appelé Masculin, puis sélectionnez l’option **Segment (Adobe Campaign)** modèle.
1. Ouvrez la page de segment créée et effectuez un glisser-déposer d’un **Identifiant de segment** du sidekick sur la page.
1. Double-cliquez sur la caractéristique, entrez l’ID représentant le segment Masculin défini dans Adobe Campaign, par exemple, **MASCULIN**, puis cliquez sur **OK**. Le message suivant doit apparaître : *`targetData.segmentCode == "MALE"`*
1. Répétez les étapes d’un autre segment, par exemple un segment ciblant les femmes.

### Création d’une marque {#creating-a-brand}

Pour créer une marque :

1. Dans **Sites**, accédez au dossier **Campagnes** (par exemple dans We.Retail).
1. Cliquez sur **Créer une page** et entrez le titre de la page, par exemple Marque We.Retail, puis sélectionnez le modèle **Marque**.

### Créer une campagne {#creating-a-campaign}

Pour créer une campagne :

1. Ouvrez le **Marque** la page que vous venez de créer.
1. Cliquez sur **Créer une page** et saisissez un titre pour votre page, par exemple, Campagne We.Retail, puis sélectionnez l’option **Campagne** modèle et cliquez sur **Créer**.

### Création d’expériences {#creating-experiences}

Pour créer des expériences pour les segments :

1. Ouvrez la page **Campagne** que vous venez de créer.
1. Créez des expériences pour vos segments en cliquant sur **Créer une page** et entrez le titre de la page, par exemple, Masculin puisque vous créez une expérience pour le segment Masculin, puis sélectionnez le modèle **Expérience**.
1. Ouvrez la page Expérience créée.
1. Cliquez sur **Modifier**, puis sous Segments, cliquez sur **Ajouter un élément**.
1. Entrez le chemin du segment Masculin, par exemple **/etc/segmentation/segments-ac/masculin** et cliquez sur **OK**. Le message suivant apparaît : *Expérience ciblée au niveau de : Masculin*.
1. Répétez les étapes précédentes pour créer une expérience pour tous les segments, par exemple la cible femme.

## Création d’une newsletter avec du contenu ciblé {#creating-a-newsletter-with-targeted-content}

Après avoir créé des segments, une marque, une campagne et une expérience, vous pouvez créer une newsletter avec du contenu ciblé. Après avoir créé l’expérience, vous liez les expériences à vos segments.

>[!NOTE]
>
>[Les exemples d’e-mails ne sont disponibles que dans Geometrixx](/help/sites-developing/we-retail.md). Téléchargez un exemple de contenu Geometrixx à partir du partage de packages.

Pour créer une newsletter avec du contenu ciblé :

1. Créez une newsletter avec le contenu ciblé : en dessous des campagnes par e-mail dans Geometrixx Outdoors, cliquez ou appuyez sur **Créer** > **Page** et sélectionnez l’un des modèles d’e-mails Adobe Campaign.

   ![chlimage_1-188](assets/chlimage_1-188.png)

1. Dans la newsletter, ajoutez des composants Texte et Personnalisation.
1. Ajoutez le texte dans les composants Texte et Personnalisation, par exemple « Newsletter par défaut. »
1. Cliquez sur la flèche située à côté de **Modifier** et sélectionnez **Ciblage**.
1. Sélectionnez votre marque dans le menu déroulant Marque et sélectionnez votre campagne. (Il s’agit de la marque et de la campagne que vous avez créées précédemment).
1. Cliquez sur **Commencer le ciblage**. Vous voyez vos segments apparaître dans la zone Audiences. L’expérience par défaut est utilisée si aucun des segments définis ne correspond.

   >[!NOTE]
   >
   >Par défaut, les exemples d&#39;emails inclus avec AEM utilisent Adobe Campaign comme moteur de ciblage. Pour les newsletters personnalisées, vous devrez peut-être sélectionner Adobe Campaign comme moteur de ciblage. Lors du ciblage, appuyez ou cliquez sur + dans la barre d’outils, saisissez le titre de la nouvelle activité, puis sélectionnez **Adobe Campaign** comme moteur de ciblage.

1. Cliquez sur **Par défaut** puis le composant Texte et personnalisation que vous avez ajouté et qui affiche l’oeil à puces avec une flèche dessus. Cliquez sur l’icône pour cibler ce composant.

   ![chlimage_1-189](assets/chlimage_1-189.png)

1. Accédez à un autre segment (Masculin), puis cliquez sur **Ajouter une offre** et sur l’icône +. Puis, modifiez l’offre.
1. Accédez à un autre segment (Féminin) et cliquez sur **Ajouter une offre** et l’icône +. Modifiez ensuite cette offre.
1. Cliquez sur **Suivant** pour afficher la correspondance, puis sur **Suivant** pour afficher les paramètres, ce qui ne s’applique pas à Adobe Campaign, puis cliquez sur **Enregistrer**.

   AEM génère automatiquement le code de ciblage correct pour Adobe Campaign lorsque le contenu est utilisé dans une diffusion dans Adobe Campaign.

1. Dans Adobe Campaign, créez votre diffusion - sélectionnez **Diffusion Email avec contenu AEM** et sélectionnez le compte d’AEM local, le cas échéant, et confirmez vos modifications.

   En mode HTML, les différentes expériences des composants ciblés sont incluses dans le code de ciblage Adobe Campaign.

   ![chlimage_1-190](assets/chlimage_1-190.png)

   >[!NOTE]
   >
   >Si vous configurez également les segments dans Adobe Campaign, cliquez sur **Aperçu** pour voir les expériences de chaque segment.
