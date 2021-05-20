---
title: Console Badges
seo-title: Console Badges
description: La console Badges de communauté vous permet d’ajouter des badges personnalisés qui peuvent être affichés pour les membres lorsqu’ils sont gagnés (attribués) ou lorsqu’ils assument un rôle spécifique dans la communauté (affecté).
seo-description: La console Badges de communauté vous permet d’ajouter des badges personnalisés qui peuvent être affichés pour les membres lorsqu’ils sont gagnés (attribués) ou lorsqu’ils assument un rôle spécifique dans la communauté (affecté).
uuid: 7103b133-ef3f-47d6-a2dc-4e6ff92e8fed
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 135b3077-5343-4888-858d-de5e9b1d4b04
docset: aem65
role: Administrator
exl-id: 50ed9ec4-ff04-4f9d-aefb-0837542a9455
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 4%

---

# Console Badges {#badges-console}

## À propos des badges {#about-badges}

La console Badges de communauté permet d’ajouter des badges personnalisés qui peuvent être affichés pour un membre lorsqu’il est gagné (attribué) ou lorsqu’il occupe un rôle spécifique dans la communauté (affecté).

### Visibilité du badge {#badge-visibility}

Actuellement, les badges qu’un membre de la communauté gagne ou se voit attribuer s’affichent avec son nom et son avatar aux emplacements suivants :

* Profils
* [Forums](/help/communities/forum.md)
* [Q&amp;R](/help/communities/working-with-qna.md)
* [Tableaux de bord](/help/communities/enabling-leaderboard.md)
* [Conceptualisation](/help/communities/ideation-feature.md)

Dans l’environnement de création, accédez à la console Badges :

* À partir de la navigation globale : **[!UICONTROL Outils]** > **[!UICONTROL Communautés]** > **[!UICONTROL Badges]**

Cette console affiche les badges actuellement disponibles et à partir desquels de nouveaux badges peuvent être ajoutés.

![badges-homepage](assets/badges-homepage.png)

## Créer le badge {#create-badge}

Un badge est créé en téléchargeant une image de petite taille (72 dpi avec une hauteur comprise entre 26 et 32 pixels) et en fournissant un nom. L’image de badge est stockée dans le référentiel à l’emplacement `/libs/settings/community/badging/images` et est automatiquement répliquée dans l’environnement de publication.

Si l’environnement de publication est une ferme d’éditeurs, il est nécessaire de configurer la [synchronisation des utilisateurs](/help/communities/sync.md).

![create-badge](assets/create-badge.png)

* **Télécharger l’image**

   (*Obligatoire*) Image de badge d’une taille recommandée de 32 x 32 pixels à 72 ppp au format JPEG ou PNG.

* **Name** (Nom)

   (*Obligatoire*) Nom du badge. Il s’agit de la valeur par défaut `Display Name` ainsi que du nom du noeud de référentiel. Si `Name` n’est pas un nom de noeud de référentiel valide, il sera modifié.

* **Nom d’affichage**

   (*Facultatif*) Nom à afficher pour le badge dans l’interface utilisateur. La valeur par défaut est le texte non modifié saisi pour la balise `Name`.

* **Description**

   (*Facultatif*) Description du badge.

## Informations supplémentaires {#additional-information}

Pour plus d’informations sur la configuration des règles de notation et de badge, voir [Notation et badges](/help/communities/implementing-scoring.md).

Pour la gestion des badges pour les membres, voir [Console Membres](/help/communities/members.md).
