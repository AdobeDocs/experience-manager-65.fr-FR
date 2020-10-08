---
title: Modèles de site
seo-title: Modèles de site
description: Comment accéder à la console Modèles de site
seo-description: Comment accéder à la console Modèles de site
uuid: d2f7556e-7e43-424e-82f1-41790aeb2d98
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 202d7dba-2b34-431d-b10f-87775632807f
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 4%

---


# Modèles de site {#site-templates}

La console Modèles de site est très similaire à la console Modèles [de](tools-groups.md) groupe, qui est axée sur des fonctions présentant un intérêt pour les groupes communautaires.

>[!NOTE]
>
>Les consoles pour la création de sites [](sites-console.md)communautaires, de modèles [de sites](sites.md)communautaires, de modèles de groupes de [communautés et de fonctions de](tools-groups.md) [communauté ne sont utilisées que dans l&#39;environnement d&#39;auteur.](functions.md)

## Console Modèles de site {#site-templates-console}

Dans l’environnement de l’auteur, pour accéder à la console des sites communautaires :

* A partir de la navigation globale : **[!UICONTROL Outils > Communautés > Modèles de site]**

Cette console affiche les modèles à partir desquels un site [](sites-console.md) communautaire peut être créé et permet de créer de nouveaux modèles de site.

![site-template](assets/site-template.png)

## Créer un modèle de site {#create-site-template}

Pour commencer à créer un modèle de site, sélectionnez `Create`.

Le panneau Editeur de site qui contient 3 sous-panneaux s’affiche alors :

### Basic info {#basic-info}

![site-template-basicinfo](assets/site-template-basicinfo.png)

Dans le panneau Informations de base, un nom, une description et si le modèle est activé ou désactivé sont configurés :

* **[!UICONTROL Nom du modèle de site de la communauté]**

   ID du nom du modèle.

* **[!UICONTROL Description du modèle de site de communauté]**

   Description du modèle.

* **[!UICONTROL Désactivé/Activé]**

   Bascule permettant de contrôler si le modèle est référencé.

### Miniature  {#thumbnail}

![site-miniature](assets/site-thumbnail.png)

(Facultatif) Sélectionnez l’icône Télécharger l’image pour afficher une miniature ainsi que le nom et la description des créateurs de sites communautaires.

### Structure {#structure}

![structure du site](assets/site-structure.png)

Pour ajouter des fonctions de communauté, faites glisser le curseur de droite vers la gauche dans l&#39;ordre d&#39;affichage des liens du menu du site. Les styles seront appliqués au modèle lors de la création du site.

Par exemple, si vous souhaitez une page d&#39;accueil, faites glisser la fonction Page de la bibliothèque et déposez-la sous le créateur de modèles. La boîte de dialogue de configuration de la page s’ouvre alors. Pour plus d&#39;informations sur les boîtes de dialogue de configuration, consultez la console [](functions.md) fonctions.

Continuez à faire glisser et à déposer toutes les autres fonctions de la communauté souhaitées pour un site communautaire en fonction de ce modèle.

La fonction page fournit une page vide. La fonction de groupes permet de créer un site de groupe (sous-communauté) au sein du site communautaire.

>[!CAUTION]
>
>La fonction de groupes *ne doit pas* être la *première ou la seule* fonction de la structure du site.
>
>Toute autre fonction, telle que la fonction [de](functions.md#page-function)page, doit être incluse et répertoriée en premier.

![éditeur de site](assets/site-editor.png)

### Modèles de groupe pour la fonction Groupes {#group-templates-for-groups-function}

Lorsque vous incluez une fonction de groupes dans le modèle de site, la configuration requiert la spécification des choix de modèle de groupe autorisés lorsqu&#39;un nouveau groupe est créé dans l&#39;environnement de publication.

>[!CAUTION]
>
>La fonction Groupes *ne doit pas* être la *première ou la seule* fonction de la structure du site.

![fonction de site](assets/site-functions.png)

En sélectionnant au moins deux modèles de groupe de communauté, un choix est fourni à l’administrateur du groupe lors de la création d’un nouveau groupe dans la communauté.

![fonction de site](assets/site-functions1.png)

## Modifier le modèle de site{#edit-site-template}

Lorsque vous consultez des modèles de site dans la console [](#site-templates-console)principale Modèles de site, il est possible de sélectionner un modèle de site existant à modifier.

Ce processus fournit les mêmes panneaux que la [création d’un modèle](#create-site-template)de site.
