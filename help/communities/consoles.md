---
title: Consoles Communities
description: Découvrez les consoles de la communauté Adobe Experience Manager disponibles dans l’environnement de création à partir du panneau de navigation global.
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: 36f2e3d2-46c7-48a8-a1e9-213f581bd9f3
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
source-wordcount: '326'
ht-degree: 0%
---
# Consoles Communities {#communities-consoles}

Les consoles d’AEM Communities, disponibles dans l’environnement de création à partir du panneau de navigation global, permettent d’accéder aux tâches administratives telles que :

* [Création d’un site communautaire](sites-console.md)
* Ajout de [groupes](groups.md) imbriqués dans le site
* Gestion des [modèles de site de la communauté](sites.md)
* Gestion des [membres de la communauté](members.md)
* [Modération](moderate-ugc.md) contenu créé par l’utilisateur ou l’utilisatrice
* Créer [badges personnalisés](badges.md)
* Configuration du [stockage par défaut pour le contenu créé par l’utilisateur](srp-config.md)

Lorsque le [stockage du contenu créé par l’utilisateur](working-with-srp.md) est configuré pour être un magasin commun partagé par les environnements de création et de publication, la [console de modération](moderation.md), disponible à la fois dans les environnements de création et de publication, fonctionne sur une instance unique du contenu créé par l’utilisateur.

Dans l’environnement de création, une fois connectés avec des droits d’administrateur, les consoles `Communities` sont disponibles à partir des consoles de navigation et des outils.

>[!NOTE]
>
>Dans l’environnement de publication, un [site communautaire](sites-console.md) affiche un élément de menu `Administration` lorsque le membre connecté dispose des privilèges appropriés.

## Panneau de navigation globale {#global-navigation-panel}

Sélectionnez l’icône `Adobe Experience Manager` dans le coin supérieur gauche pour ouvrir le panneau de navigation globale et accéder à deux icônes :

* [Console de navigation](#navigation-console)
* [Console Outils](tools.md)

## Console de navigation {#navigation-console}

Pour accéder aux différentes consoles de Communities, dans la navigation globale, sélectionnez **navigation, Communities**.

![communautés](assets/communities.png)

* [Sites](sites-console.md)

  La console Sites est accessible dans l’environnement de création pour créer et gérer des sites communautaires et leurs [groupes](groups.md).

* [Modération](moderation.md)

  La console Modération permet la modération en bloc du contenu créé par l’utilisateur et dans l’environnement de création. Une console de modération en bloc similaire est accessible dans l’environnement de publication aux membres de la communauté auxquels le rôle de [modérateur de la communauté](users.md#publishenvironmentusersandgroups) est affecté pour un ou plusieurs sites de la communauté.

* [Membres, groupes](members.md)

  Les consoles Membres et groupes permettent de gérer les membres de la communauté et les groupes de membres qui existent dans l’environnement de publication à partir de l’environnement de création.

* [Rapports](reports.md)

  La console Rapports permet de générer des rapports sur les affectations, les pages vues et le contenu publié (UGC) lorsqu’un site communautaire a [activé Adobe Analytics](sites-console.md#analytics). La console n’est disponible que dans l’environnement de création.

## Console Outils {#tools-console}

Pour accéder à [Outils Communities](tools.md) (anciennement la console d’administration), à partir de la navigation globale : **[!UICONTROL Outils]** > **[!UICONTROL Communautés]**
