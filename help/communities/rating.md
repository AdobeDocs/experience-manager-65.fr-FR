---
title: Utilisation des évaluations
seo-title: Using Ratings
description: Ajout d’un composant Évaluation à une page
seo-description: Adding a Rating component to a page
uuid: a986970b-1221-4648-9a69-410f4480e0ae
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: a0e5491e-66bc-47b0-94a5-45a02bc558da
exl-id: 7534ad5d-b408-4b09-bd3d-da7ab009d55b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 32%

---

# Utilisation des évaluations {#using-ratings}

Le `Rating` est utilisé de manière autonome ou conjointement avec d’autres fonctionnalités de Communities. Ce composant permet aux membres de la communauté connectés d’exprimer leurs opinions en évaluant le contenu.

## Ajout d’une évaluation à une page {#adding-a-rating-to-a-page}

Pour ajouter une `Rating` à une page en mode création, recherchez le composant. `Communities / Rating` et faites-le glisser sur la page, par exemple à une position relative à la fonction que les membres peuvent évaluer.

Pour obtenir les informations nécessaires, consultez la section [Principes de base des composants des communautés](basics.md).

Lorsque la variable [bibliothèques côté client requises](rating-basics.md#essentials-for-client-side) sont incluses, c’est ainsi que la variable `Rating` s’affiche.

![Évaluation](assets/rating.png)

## Configuration du composant Évaluation {#configuring-rating}

Sélectionnez le `Rating` pour accéder au composant et le sélectionner. `Configure` qui ouvre la boîte de dialogue de modification.

![configure-new](assets/configure-new.png)

Dans l’onglet **[!UICONTROL Textes et libellés]**, indiquez l’identifiant interne du composant Évaluation.

![tallyname](assets/tallyname.png)

**[!UICONTROL Nom Tally]**
(*Obligatoire*) Un nom simple pour la variable `Rating` qui identifie de manière unique cette instance. Il doit s’agir d’un nom de nœud valide pour le référentiel.

## Expérience des visiteurs {#site-visitor-experience}

### Membres {#members}

Une seule évaluation est autorisée par membre.  Le membre peut modifier son évaluation à tout moment.

### Anonyme {#anonymous}

La publication anonyme d’une évaluation n’est pas possible. Les visiteurs du site doivent s’inscrire (devenir membres) et se connecter pour participer.

## Informations supplémentaires {#additional-information}

Vous trouverez plus d’informations sur la [Notions fondamentales sur la notation](rating-basics.md) pour les développeurs.
