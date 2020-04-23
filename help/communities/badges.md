---
title: Console Badges
seo-title: Console Badges
description: La console Badges de communautés vous permet d’ajouter des badges personnalisés qui peuvent être affichés pour les membres lorsqu’ils sont gagnés (attribués) ou lorsqu’ils assument un rôle spécifique dans la communauté (affectés).
seo-description: La console Badges de communautés vous permet d’ajouter des badges personnalisés qui peuvent être affichés pour les membres lorsqu’ils sont gagnés (attribués) ou lorsqu’ils assument un rôle spécifique dans la communauté (affectés).
uuid: 7103b133-ef3f-47d6-a2dc-4e6ff92e8fed
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 135b3077-5343-4888-858d-de5e9b1d4b04
docset: aem65
translation-type: tm+mt
source-git-commit: 85f3b8f2a5f079954f4907037c1c722a6b25fd91

---


# Console Badges {#badges-console}

## A propos des badges {#about-badges}

La console Badges communautaires permet d&#39;ajouter des badges personnalisés qui peuvent être affichés pour un membre lorsqu&#39;il est gagné (attribué) ou lorsqu&#39;il assume un rôle spécifique dans la communauté (attribué).

### Visibilité du badge {#badge-visibility}

Actuellement, les badges gagnent ou sont attribués à un membre de la communauté apparaissent avec son nom et son avatar aux emplacements suivants :

* Profils
* [Forums](/help/communities/forum.md)
* [Q&amp;R](/help/communities/working-with-qna.md)
* [Tableaux de bord](/help/communities/enabling-leaderboard.md)
* [Conceptualisation](/help/communities/ideation-feature.md)

Dans l&#39;auteur  , pour accéder à la console Badges

* Dans la navigation globale, accédez à **[!UICONTROL Outils > Communautés > Badges.]**

Cette console affiche les badges actuellement disponibles et à partir desquels de nouveaux badges peuvent être ajoutés.

![chlimage_1-123](assets/chlimage_1-123.png)

## Créer le badge {#create-badge}

Un badge est créé en téléchargeant une image appropriée (72 dpi avec une hauteur comprise entre 26 et 32 pixels) et en fournissant un nom. L’image de badge est stockée dans le référentiel à l’emplacement `/etc/community/badging/images` et automatiquement répliquée dans le  de publication .

Si le de publication  est une batterie d’éditeurs, il est nécessaire de configurer la synchronisation [utilisateur](/help/communities/sync.md).

![chlimage_1-124](assets/chlimage_1-124.png)

* **Télécharger l’image**

   (*Obligatoire*) Image de badge d’une taille recommandée de 32 x 32 pixels à 72 ppp au format JPEG ou PNG.

* **Nom**

   (*Obligatoire*) Nom du badge. Il s’agit du nom par défaut `Display Name` ainsi que du nom du noeud du référentiel. Si le nom `Name` n&#39;est pas un nom de noeud de référentiel valide, il sera modifié.

* **Nom d’affichage**

   (*Facultatif*) Nom à afficher pour le badge dans l’interface utilisateur. La valeur par défaut est le texte non modifié saisi pour le `Name`.

* **Description**

   (*Optional*) A description for the badge.

## Informations supplémentaires {#additional-information}

Pour plus d’informations sur la configuration des règles de notation et de mise en badge, voir [Scoring and Badges](/help/communities/implementing-scoring.md)(Scores et badges).

Pour la gestion des badges pour les membres, voir Console [Membres](/help/communities/members.md).
