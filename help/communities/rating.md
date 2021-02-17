---
title: Utilisation des évaluations
seo-title: Utilisation des évaluations
description: Ajouter un composant Note à une page
seo-description: Ajouter un composant Note à une page
uuid: a986970b-1221-4648-9a69-410f4480e0ae
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: a0e5491e-66bc-47b0-94a5-45a02bc558da
translation-type: tm+mt
source-git-commit: 0051791da06d15a48b82cf93164a89b4ea42ce98
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 31%

---


# Utilisation des évaluations {#using-ratings}

Le composant `Rating` est utilisé de manière autonome ou conjointement avec d&#39;autres fonctionnalités de communautés. Ce composant permet aux membres de la communauté connectés d&#39;exprimer leurs opinions en évaluant le contenu.

## Ajout d’une évaluation à une page {#adding-a-rating-to-a-page}

Pour ajouter un composant `Rating` à une page en mode création, recherchez le composant `Communities / Rating` et faites-le glisser sur sa place sur une page, par exemple une position relative à la fonction à évaluer par les membres.

Pour obtenir les informations nécessaires, consultez [Community Components Basics](basics.md).

Lorsque les [bibliothèques client requises](rating-basics.md#essentials-for-client-side) sont incluses, c&#39;est ainsi que le composant `Rating` s&#39;affiche.

![Évaluation](assets/rating.png)

## Configuration du composant Évaluation {#configuring-rating}

Sélectionnez le composant `Rating` placé auquel accéder et sélectionnez l&#39;icône `Configure` qui ouvre la boîte de dialogue de modification.

![configure-new](assets/configure-new.png)

Dans l’onglet **[!UICONTROL Textes et libellés]**, indiquez l’identifiant interne du composant Évaluation.

![tallyname](assets/tallyname.png)

**[!UICONTROL Nom]**
 du compte (*Obligatoire*) Nom simple du compte  `Rating` qui identifie de manière unique cette instance. Il doit s’agir d’un nom de nœud valide pour le référentiel.

## Expérience des visiteurs {#site-visitor-experience}

### Membres {#members}

Une seule évaluation est autorisée par membre.  Le membre peut modifier son évaluation à tout moment.

### Anonyme  {#anonymous}

La publication anonyme d’une évaluation n’est pas possible. Les visiteurs du site doivent s&#39;inscrire (devenir membre) et se connecter pour participer.

## Informations supplémentaires {#additional-information}

Pour plus d&#39;informations, consultez la page [Notation des fondamentaux](rating-basics.md) pour les développeurs.
