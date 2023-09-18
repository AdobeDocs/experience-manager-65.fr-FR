---
title: Modèles de site
description: Accès à la console Modèles de site
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: 05a944a3-adb1-47b4-b4a5-15bac91c995e
source-git-commit: ab3d016c7c9c622be361596137b150d8719630bd
workflow-type: tm+mt
source-wordcount: '444'
ht-degree: 4%

---

# Modèles de site {#site-templates}

La console Modèles de site est similaire au [Modèles de groupe](tools-groups.md) console, qui est axée sur des fonctions présentant un intérêt pour les groupes communautaires.

>[!NOTE]
>
>Les consoles pour la création de [sites communautaires](sites-console.md), [modèles de site de communauté](sites.md), [modèles de groupe de communautés](tools-groups.md), et [fonctions de communauté](functions.md) sont utilisables uniquement dans l’environnement de création.

## Console Modèles de site {#site-templates-console}

Dans l’environnement de création, pour accéder à la console des sites de la communauté :

* À partir de la navigation globale : **[!UICONTROL Outils > Communautés > Modèles de site]**

Cette console affiche les modèles à partir desquels une [site communautaire](sites-console.md) peut être créé et permet de créer des modèles de site.

![site-template](assets/site-template.png)

## Créer un modèle de site {#create-site-template}

Pour commencer à créer un modèle de site, sélectionnez `Create`.

Cela ouvre le panneau Éditeur de site qui contient trois sous-panneaux :

### Informations de base {#basic-info}

![site-template-basicinfo](assets/site-template-basicinfo.png)

Dans le panneau Informations de base , un nom, une description et si le modèle est activé ou désactivé sont configurés :

* **[!UICONTROL Nom du modèle de site de la communauté]**

  ID du nom du modèle.

* **[!UICONTROL Description du modèle de site de communauté]**

  Description du modèle.

* **[!UICONTROL Désactivé/activé]**

  Bascule contrôlant si le modèle est référencable.

### Miniature {#thumbnail}

![site-thumbnail](assets/site-thumbnail.png)

(Facultatif) Sélectionnez l’icône Télécharger l’image pour afficher une miniature ainsi que le nom et la description des créateurs de sites de communauté.

### Structure {#structure}

![structure du site](assets/site-structure.png)

Pour ajouter des fonctions de communauté, faites glisser du côté droit vers la gauche dans l’ordre dans lequel doivent apparaître les liens du menu du site. Les styles sont appliqués au modèle lors de la création du site.

Par exemple, si vous souhaitez une page d’accueil, faites glisser la fonction Page de la bibliothèque et déposez-la sous le créateur de modèles. La boîte de dialogue de configuration de la page s’ouvre alors. Voir [console fonctions](functions.md) pour plus d’informations sur les boîtes de dialogue de configuration.

Continuez à faire glisser et déposer toutes les autres fonctions de la communauté souhaitées pour un site de la communauté en fonction de ce modèle.

La fonction page fournit une page vide. La fonction Groupes permet de créer un site de groupe (sous-communauté) au sein du site de la communauté.

>[!CAUTION]
>
>La fonction Groups doit *ne pas être le premier ou le seul* dans la structure du site.
>
>Toute autre fonction, telle que [fonction de page](functions.md#page-function), doit être inclus et répertorié en premier.

![éditeur de site](assets/site-editor.png)

### Modèles de groupe pour la fonction Groupes {#group-templates-for-groups-function}

Lors de l’inclusion d’une fonction Groupes dans le modèle de site, la configuration nécessite la spécification des choix de modèle de groupe autorisés lorsqu’un nouveau groupe est créé dans l’environnement de publication.

>[!CAUTION]
>
>La fonction Groups doit *ne pas être le premier ou le seul* dans la structure du site.

![site-fonctions](assets/site-functions.png)

En sélectionnant plusieurs modèles de groupe de communauté, vous avez le choix entre l’administrateur du groupe qui crée un groupe dans la communauté.

![site-function](assets/site-functions1.png)

## Modifier le modèle de site {#edit-site-template}

Lors de l’affichage des modèles de site dans l’élément principal [Console Modèles de site](#site-templates-console), il est possible de sélectionner un modèle de site existant à modifier.

Ce processus fournit les mêmes panneaux que [création d’un modèle de site](#create-site-template).
