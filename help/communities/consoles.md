---
title: Consoles Communities
seo-title: Communities Consoles
description: Consoles de la communauté expliquées
seo-description: Community Consoles explained
uuid: 1c5b2600-9059-4b44-9741-f1b627423d3c
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 5fa9ee8b-5893-4ae9-a986-bfdbb00f355f
role: Admin
exl-id: 36f2e3d2-46c7-48a8-a1e9-213f581bd9f3
source-git-commit: 4dbbcc41757843d3b2d5a3bbb2656ef587e83d2c
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 1%

---

# Consoles Communities {#communities-consoles}

Les consoles AEM Communities, disponibles dans l’environnement de création à partir du panneau de navigation globale, permettent d’accéder aux tâches administratives telles que :

* [Créer un site communautaire](sites-console.md)
* Ajouter [groups](groups.md) imbriqué dans le site
* Gestion [modèles de site de communauté](sites.md)
* Gestion [membres de la communauté](members.md)
* [Modération](moderate-ugc.md) contenu généré par l’utilisateur (UGC)
* Créer [badges personnalisés](badges.md)
* Configuration de la variable [stockage par défaut pour le contenu généré par l’utilisateur](srp-config.md)

When [Stockage UGC](working-with-srp.md) est configuré pour être un magasin commun partagé par les environnements de création et de publication, la variable [console de modération](moderation.md), disponible à partir des environnements de création et de publication, fonctionne sur une instance unique du contenu créé par l’utilisateur.

Dans l’environnement de création, après la connexion avec des privilèges d’administrateur, la variable `Communities` les consoles sont disponibles à partir des consoles de navigation et d’outils.

>[!NOTE]
>
>Dans l’environnement de publication, une [site communautaire](sites-console.md) affiche une `Administration` lorsque le membre connecté dispose des privilèges appropriés.

## Panneau de navigation global {#global-navigation-panel}

Sélectionnez la `Adobe Experience Manager` dans le coin supérieur gauche pour ouvrir le panneau de navigation globale et accéder à deux icônes :

* [Console de navigation](#navigation-console)
* [Console Outils](tools.md)

## Console de navigation {#navigation-console}

Pour accéder aux différentes consoles Communities, dans la navigation globale, sélectionnez **navigation, communautés**.

![communautés](assets/communities.png)

* [Sites](sites-console.md)

   La console Sites est accessible dans l’environnement de création dans le but de créer et de gérer des sites de communauté et ses [groups](groups.md).

* [Modération](moderation.md)

   La console Modération sert à la modération en masse du contenu généré par l’utilisateur et dans l’environnement de création. Une console de modération en bloc similaire est accessible dans l’environnement de publication aux membres de la communauté auxquels est affecté le rôle de [modérateur de communauté](users.md#publishenvironmentusersandgroups) pour un ou plusieurs sites communautaires.

* [Membres, groupes](members.md)

   Les consoles Membres et Groupes permettent de gérer les membres de la communauté et les groupes de membres qui existent dans l’environnement de publication à partir de l’environnement de création.

* [Rapports](reports.md)

   La console Rapports permet de générer des rapports sur les affectations, les pages vues et le contenu publié (contenu généré) lorsqu’un site de communauté possède [activé Adobe Analytics](sites-console.md#analytics). La console n’est disponible que dans l’environnement de création.

## Console Outils {#tools-console}

Pour accéder à [Outils Communities](tools.md) (anciennement Administration Console), à partir de la navigation globale : **[!UICONTROL Outils]** > **[!UICONTROL Communautés]**
