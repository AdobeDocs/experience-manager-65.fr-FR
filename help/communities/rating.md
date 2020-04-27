---
title: Utilisation des évaluations
seo-title: Utilisation des évaluations
description: Ajout d’un composant Évaluation à une page
seo-description: Ajout d’un composant Évaluation à une page
uuid: a986970b-1221-4648-9a69-410f4480e0ae
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: a0e5491e-66bc-47b0-94a5-45a02bc558da
translation-type: tm+mt
source-git-commit: 62f2a11491e427a13cecae75c225ed41a44783cd

---


# Utilisation des évaluations {#using-ratings}

The `Rating` component is used standalone or in conjunction with other Communities features. Ce composant permet aux membres de la communauté connectés d’exprimer leurs opinions en évaluant le contenu.

## Ajout d’une évaluation à une page {#adding-a-rating-to-a-page}

Pour ajouter un `Rating` composant à une page en mode création, localisez le composant `Communities / Rating` et faites-le glisser vers son emplacement sur une page, par exemple une position relative à la fonction à évaluer par les membres.

For necessary information, visit [Communities Components Basics](basics.md).

When the [required client-side libraries](rating-basics.md#essentials-for-client-side) are included, this is how the `Rating` component will appear.

![chlimage_1-493](assets/chlimage_1-493.png)

## Configuration du composant Évaluation {#configuring-rating}

Select the placed `Rating` component to access and select the `Configure` icon which opens the edit dialog.

![chlimage_1-494](assets/chlimage_1-494.png)

Dans l’onglet **[!UICONTROL Textes et libellés]**, indiquez l’identifiant interne du composant Évaluation.

![chlimage_1-495](assets/chlimage_1-495.png)

**[!UICONTROL Nom]** du compte (*Obligatoire*) Nom simple du compte `Rating`qui identifie de manière unique cette instance. Il doit s’agir d’un nom de nœud valide pour le référentiel.

## Expérience des visiteurs {#site-visitor-experience}

### Membres {#members}

Une seule évaluation est autorisée par membre.  Le membre peut modifier son évaluation à tout moment.

### Anonyme {#anonymous}

La publication anonyme d’une évaluation n’est pas possible. Les du site doivent s&#39;inscrire (devenir membre) et se connecter pour participer.

## Informations supplémentaires {#additional-information}

More information may be found on the [Rating Essentials](rating-basics.md) page for developers.
