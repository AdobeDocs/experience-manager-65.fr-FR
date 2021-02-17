---
title: Ciblage d’un élément de campagne Adobe Campaign
seo-title: Ciblage d’un élément de campagne Adobe Campaign
description: Vous pouvez créer des expériences ciblées pour Adobe Campaign après la configuration de la segmentation
seo-description: Vous pouvez créer des expériences ciblées pour Adobe Campaign après la configuration de la segmentation
uuid: 8fcc9210-d8c5-44e3-8aa8-6c6db810c98e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
discoiquuid: f1cb5e98-ccd1-4b2c-acca-2b3cc1b7ac5f
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '827'
ht-degree: 78%

---


# Ciblage d’un élément de campagne Adobe Campaign{#targeting-your-adobe-campaign}

Pour cibler votre newsletter Adobe Campaign, vous devez d’abord configurer la segmentation, ce qui n’est possible que dans l’IU classique (pour ClientContext). Ensuite, vous pouvez créer des expériences ciblées pour Adobe Campaign. Les deux procédures sont décrites dans cette section.

## Configuration de la segmentation dans AEM {#setting-up-segmentation-in-aem}

Pour configurer la segmentation, vous devez utiliser l’IU classique afin de configurer les segments. Les étapes restantes peuvent être exécutées dans l’IU standard.

La configuration de la segmentation comprend la création de segments, d’une marque, d’une campagne et d’expériences.

>[!NOTE]
>
>L’ID de segment doit être mappé sur celui du côté Adobe Campaign.

### Création de segments {#creating-segments}

Pour créer des segments :

1. Ouvrez la [console de segmentation](http://localhost:4502/miscadmin#/etc/segmentation) à **&lt;hôte>:&lt;port>/miscadmin#/etc/segmentation**.
1. Créez une page et entrez un titre, par exemple **Segments AC**, puis sélectionnez le modèle **Segment (Adobe Campaign)**.
1. Sélectionnez la page créée dans l’arborescence située sur le côté gauche.
1. Créez un segment, par exemple en ciblant les utilisateurs hommes, en créant une nouvelle page sous le segment créé et intitulé Masculin, puis sélectionnez le modèle **Segment (Adobe Campaign)**.
1. Ouvrez la page du segment créé et faites glisser **ID de segment** à partir du sidekick jusque sur la page.
1. Doublon-clic sur la caractéristique, saisissez l’identifiant représentant dans ce cas, le segment mâle défini dans Adobe Campaign - par exemple, **MALE** - et cliquez sur **OK**. Le message suivant doit apparaître : *`targetData.segmentCode == "MALE"`*
1. Recommencez ces étapes pour un autre segment, par exemple, un segment ciblant les utilisateurs femmes.

### Création d’une marque  {#creating-a-brand}

Pour créer une marque, procédez comme suit :

1. Dans **Sites**, accédez au dossier **Campagnes** (par exemple dans We.Retail).
1. Cliquez sur **Créer une page** et entrez le titre de la page, par exemple Marque We.Retail, puis sélectionnez le modèle **Marque**.

### Création d’une campagne {#creating-a-campaign}

Pour créer une campagne, procédez comme suit :

1. Ouvrez la page **Marque** que vous venez de créer. 
1. Cliquez sur **Créer une page** et saisissez le titre de la page, par exemple, Campagne We.Retail, puis sélectionnez le modèle **Campagne** et cliquez sur **Créer**.

### Création d’expériences {#creating-experiences}

Pour créer des expériences liées à des segments :

1. Ouvrez la page **Campaign** que vous venez de créer.
1. Créez des expériences pour vos segments en cliquant sur **Créer une page** et en saisissant un titre pour votre page, par exemple Homme lorsque vous créez une expérience pour le segment Homme, et en sélectionnant le modèle **Expérience**.
1. Ouvrez la page Expérience créée.
1. Cliquez sur **Modifier**, puis sous Segments, cliquez sur **Ajouter un élément**.
1. Entrez le chemin d’accès au segment mâle, par exemple **/etc/segmentation/ac-segments/male** et cliquez sur **OK**. Le message suivant doit apparaître : *L&#39;expérience est ciblée sur : Homme*
1. Recommencez les étapes précédentes afin de créer une expérience pour tous les segments, par exemple la cible Féminin.

## Création d’une newsletter avec du contenu ciblé  {#creating-a-newsletter-with-targeted-content}

Une fois que vous avez créé des segments, une marque, une campagne et une expérience, vous pouvez créer une newsletter avec du contenu ciblé. Après avoir créé l’expérience, vous l’associez à vos segments.

>[!NOTE]
>
>[Les exemples de messages électroniques ne sont disponibles que dans Geometrixx](/help/sites-developing/we-retail.md). Téléchargez un exemple de contenu Geometrixx à partir de Package Share.

Pour créer une newsletter avec du contenu ciblé :

1. Créez un bulletin d’information avec du contenu ciblé : Sous Campagnes par courriel en Geometrixx Outdoors, cliquez ou appuyez sur **Créer** > **Page**, puis sélectionnez l’un des modèles Adobe Campaign Mail.

   ![chlimage_1-188](assets/chlimage_1-188.png)

1. Dans la newsletter, ajoutez un composant Texte et personnalisation.
1. Ajoutez le texte dans le composant Texte et personnalisation, par exemple « Newsletter par défaut. »
1. Cliquez sur la flèche en regard de **Modifier** et sélectionnez **Ciblage**.
1. Sélectionnez votre marque dans le menu déroulant Marque, puis sélectionnez votre campagne. (Il s’agit de la marque et de la campagne que vous avez créées précédemment.)
1. Cliquez sur **Commencer le ciblage**. Vous voyez vos segments apparaître dans la zone Audiences. L’expérience par défaut est utilisée si aucun des segments définis ne correspond.

   >[!NOTE]
   >
   >Par défaut, les exemples de message électronique fournis dans AEM utilisent Adobe Campaign comme moteur de ciblage. Pour les newsletters personnalisées, il se peut que vous deviez sélectionner Adobe Campaign comme moteur de ciblage. Lors du ciblage, cliquez ou appuyez sur + dans la barre d’outils, entrez le titre de la nouvelle activité, puis sélectionnez **Adobe Campaign** comme moteur de ciblage.

1. Cliquez sur **Par défaut**, puis sur le composant Texte et personnalisation que vous avez ajouté. La cible s’affiche avec une flèche dessus. Cliquez sur l’icône pour cibler ce composant.

   ![chlimage_1-189](assets/chlimage_1-189.png)

1. Accédez à un autre segment (Masculin), puis cliquez sur **Ajouter une offre** et sur l’icône +. Puis, modifiez l’offre.
1. Accédez à un autre segment (Féminin), puis cliquez sur **Ajouter une offre** et sur l’icône +. Modifiez ensuite cette offre. 
1. Cliquez sur **Suivant** pour afficher le mappage, puis sur **Suivant** pour afficher les paramètres qui ne s’appliquent pas à Adobe Campaign, puis cliquez sur **Enregistrer**.

   AEM génère automatiquement le code de ciblage correct pour Adobe Campaign lorsque le contenu est utilisé dans une diffusion au sein d’Adobe Campaign.

1. Dans Adobe Campaign, créez la diffusion. Sélectionnez **Envoi de courriers électroniques avec le contenu AEM** et sélectionnez le compte AEM local selon les besoins. Confirmez vos modifications.

   En mode d’affichage HTML, les différentes expériences des composants ciblés sont incluses dans le code de ciblage d’Adobe Campaign.

   ![chlimage_1-190](assets/chlimage_1-190.png)

   >[!NOTE]
   >
   >Si vous configurez également les segments dans Adobe Campaign, cliquez sur **Aperçu** pour voir les expériences de chaque segment.

