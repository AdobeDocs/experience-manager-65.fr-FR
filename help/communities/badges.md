---
title: Console Badges
description: La console Badges de communautés vous permet d’ajouter des badges personnalisés qui peuvent être affichés pour les membres lorsqu’ils sont gagnés (attribués) ou lorsqu’ils assument un rôle spécifique dans la communauté (attribué)
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
role: Admin
exl-id: 50ed9ec4-ff04-4f9d-aefb-0837542a9455
solution: Experience Manager
feature: Communities
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: b013f126-a97e-52d1-9f79-cb5bbb12114e
    internal-label: Communities
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '291'
ht-degree: 4%
---
# Console Badges {#badges-console}

## À propos des badges {#about-badges}

La console Badges de communautés vous permet d’ajouter des badges personnalisés qui peuvent être affichés pour un membre lorsqu’ils sont gagnés (attribués) ou lorsqu’il assume un rôle spécifique dans la communauté (attribué).

### Badge Visibility {#badge-visibility}

Actuellement, les badges gagnés ou attribués à un membre de la communauté apparaissent avec son nom et son avatar aux emplacements suivants :

* Profils
* [Forums](/help/communities/forum.md)
* [Q&amp;R](/help/communities/working-with-qna.md)
* [Classements](/help/communities/enabling-leaderboard.md)
* [Conceptualisation](/help/communities/ideation-feature.md)

Dans l’environnement de création, accédez à la console Badges :

* Dans la navigation globale : **[!UICONTROL Outils]** > **[!UICONTROL Communautés]** > **[!UICONTROL Badges]**

Cette console affiche les badges actuellement disponibles et à partir desquels de nouveaux badges peuvent être ajoutés.

![badges-homepage](assets/badges-homepage.png)

## Créer le badge {#create-badge}

Un badge est créé en téléchargeant une image suffisamment petite (72 dpi avec une hauteur comprise entre 26 et 32 pixels) et en fournissant un nom. L’image de badge est stockée dans le référentiel à l’adresse `/libs/settings/community/badging/images` et est automatiquement répliquée dans l’environnement de publication.

Si l’environnement de publication est une batterie d’éditeurs, il est nécessaire de configurer [la synchronisation des utilisateurs](/help/communities/sync.md).

![create-badge](assets/create-badge.png)

* **Charger l’image**

  (*Obligatoire*) Image de badge d’une taille recommandée de 32 x 32 pixels à 72 ppp au format JPEG ou PNG.

* **Nom**

  (*Obligatoire*) Nom du badge. Il s’agit de la `Display Name` par défaut et du nom du nœud du référentiel. Si le `Name` n’est pas un nom de nœud de référentiel valide, il est modifié.

* **Nom d’affichage**

  (*Facultatif*) Nom à afficher pour le badge dans l’interface utilisateur. La valeur par défaut est le texte non modifié saisi pour le `Name`.

* **Description**

  (*facultatif*) Description du badge.

## Informations supplémentaires {#additional-information}

Pour plus d’informations sur la configuration des règles de notation et de badge, voir [Notation et badges](/help/communities/implementing-scoring.md).

Pour gérer les badges des membres, voir [Console des membres](/help/communities/members.md).
