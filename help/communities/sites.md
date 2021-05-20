---
title: Modèles de site
seo-title: Modèles de site
description: Accès à la console Modèles de site
seo-description: Accès à la console Modèles de site
uuid: d2f7556e-7e43-424e-82f1-41790aeb2d98
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 202d7dba-2b34-431d-b10f-87775632807f
role: Administrator
exl-id: 05a944a3-adb1-47b4-b4a5-15bac91c995e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 4%

---

# Modèles de site {#site-templates}

La console Modèles de site est très similaire à la console [Modèles de groupe](tools-groups.md), qui est axée sur des fonctions présentant un intérêt pour les groupes communautaires.

>[!NOTE]
>
>Les consoles pour la création de [sites de communauté](sites-console.md), [modèles de site de communauté](sites.md), [modèles de groupe de communauté](tools-groups.md) et [fonctions de communauté](functions.md) ne peuvent être utilisées que dans l’environnement de création.

## Console Modèles de site {#site-templates-console}

Dans l’environnement de création, pour accéder à la console des sites de la communauté :

* À partir de la navigation globale : **[!UICONTROL Outils > Communautés > Modèles de site]**

Cette console affiche les modèles à partir desquels un [site communautaire](sites-console.md) peut être créé et permet de créer des modèles de site.

![site-template](assets/site-template.png)

## Créer un modèle de site {#create-site-template}

Pour commencer à créer un modèle de site, sélectionnez `Create`.

Le panneau Éditeur de site s’affiche alors et contient trois sous-panneaux :

### Informations de base {#basic-info}

![site-template-basicinfo](assets/site-template-basicinfo.png)

Dans le panneau Informations de base , un nom, une description et si le modèle est activé ou désactivé sont configurés :

* **[!UICONTROL Nom du modèle de site de la communauté]**

   ID du nom du modèle.

* **[!UICONTROL Description du modèle de site de communauté]**

   Description du modèle.

* **[!UICONTROL Désactivé/activé]**

   Bascule contrôlant si le modèle est référencable.

### Miniature  {#thumbnail}

![site-thumbnail](assets/site-thumbnail.png)

(Facultatif) Sélectionnez l’icône Télécharger l’image afin d’afficher une miniature ainsi que le nom et la description des créateurs des sites de la communauté.

### Structure {#structure}

![structure du site](assets/site-structure.png)

Pour ajouter des fonctions de communauté, faites glisser du côté droit vers la gauche dans l’ordre dans lequel doivent apparaître les liens du menu du site. Des styles seront appliqués au modèle lors de la création du site.

Par exemple, si vous souhaitez une page d’accueil, faites glisser la fonction Page de la bibliothèque et déposez-la sous le créateur de modèles. La boîte de dialogue de configuration de la page s’ouvre alors. Voir la [console des fonctions](functions.md) pour plus d’informations sur les boîtes de dialogue de configuration.

Continuez à faire glisser et déposer toutes les autres fonctions de la communauté souhaitées pour un site de la communauté en fonction de ce modèle.

La fonction page fournit une page vide. La fonction de groupes permet de créer un site de groupe (sous-communauté) au sein du site de la communauté.

>[!CAUTION]
>
>La fonction groups doit *ne pas* être la *première ou la seule fonction* dans la structure du site.
>
>Toute autre fonction, telle que la [fonction de page](functions.md#page-function), doit être incluse et répertoriée en premier.

![éditeur de site](assets/site-editor.png)

### Modèles de groupe pour la fonction Groupes {#group-templates-for-groups-function}

Lors de l’inclusion d’une fonction de groupe dans le modèle de site, la configuration nécessite la spécification des choix de modèle de groupe autorisés lorsqu’un nouveau groupe est créé dans l’environnement de publication.

>[!CAUTION]
>
>La fonction Groupes doit *ne pas* être la *première ou la seule fonction* dans la structure du site.

![site-fonctions](assets/site-functions.png)

En sélectionnant plusieurs modèles de groupe de communauté, l’administrateur du groupe a le choix de créer un nouveau groupe dans la communauté.

![site-function](assets/site-functions1.png)

## Modifier le modèle de site{#edit-site-template}

Lors de l’affichage des modèles de site dans la [console Modèles de site](#site-templates-console) principale, il est possible de sélectionner un modèle de site existant à modifier.

Ce processus fournit les mêmes panneaux que la [création d’un modèle de site](#create-site-template).
