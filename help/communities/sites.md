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
translation-type: tm+mt
source-git-commit: 89156f94f2d0494d44d4f0b99abfba4fafbc66d3

---


# Modèles de site {#site-templates}

La console Modèles de site est très similaire à la console Modèles [de](tools-groups.md) groupe, qui se concentre sur des fonctions présentant un intérêt pour les groupes communautaires.

>[!NOTE]
>
>Les consoles pour la création de sites [](sites-console.md)communautaires, de modèles [de sites](sites.md)communautaires, de modèles [de groupes](tools-groups.md) communautaires et de fonctions de [communauté ne sont utilisées que dans le  de l&#39;auteur.](functions.md)


## Console Modèles de site {#site-templates-console}

Dans l&#39;auteur  , pour accéder à la console des sites de la communauté :

* A partir de la navigation globale : **[!UICONTROL Outils > Communautés > Modèles de site]**

Cette console affiche les modèles à partir desquels un site [](sites-console.md) communautaire peut être créé et permet de créer de nouveaux modèles de site.

![chlimage_1-18](assets/chlimage_1-18.png)

## Créer un modèle de site {#create-site-template}

Pour commencer à créer un modèle de site, sélectionnez `Create`.

Le panneau Editeur de site qui contient 3 sous-panneaux s’affiche alors :

### Basic info {#basic-info}

![chlimage_1-19](assets/chlimage_1-19.png)

Dans le panneau Informations de base, un nom, une description et si le modèle est activé ou désactivé sont configurés :

* **[!UICONTROL Nom du modèle de site de la communauté]**

   ID du nom du modèle.

* **[!UICONTROL Description du modèle de site de communauté]**

   Description du modèle.

* **[!UICONTROL Désactivé/Activé]**

   Bascule contrôlant si le modèle peut être référencé.

### Miniature   {#thumbnail}

![chlimage_1-20](assets/chlimage_1-20.png)

(Facultatif) Sélectionnez l’icône Télécharger l’image pour afficher une miniature avec le nom et la description des créateurs de sites de la communauté.

### Structure {#structure}

![chlimage_1-21](assets/chlimage_1-21.png)

Pour ajouter des fonctions de communauté, faites glisser le curseur de droite vers la gauche dans l&#39;ordre d&#39;affichage des liens du menu du site. Les styles seront appliqués au modèle lors de la création du site.

Par exemple, si vous souhaitez un , faites glisser la fonction Page de la bibliothèque et déposez-la sous le créateur de modèles. La boîte de dialogue de configuration de la page s’ouvre alors. Pour plus d&#39;informations sur les boîtes de dialogue de configuration, consultez la console [des fonctions](functions.md) .

Continuez à faire glisser et à déposer toutes les autres fonctions de la communauté souhaitées pour un site communautaire en fonction de ce modèle.

La fonction de page fournit une page vide. La fonction de groupes permet de créer un site de groupe (sous-communauté) au sein du site communautaire.

>[!CAUTION]
>
>La fonction de groupes *ne doit pas* être la *première ou la seule* fonction de la structure du site.
>
>Toute autre fonction, telle que la fonction [de](functions.md#page-function)page, doit être incluse et répertoriée en premier.


![chlimage_1-22](assets/chlimage_1-22.png)

### Modèles de groupe pour la fonction Groupes {#group-templates-for-groups-function}

Lors de l’inclusion d’une fonction de groupes dans le modèle de site, la configuration requiert la spécification des choix de modèle de groupe autorisés lorsqu’un nouveau groupe est créé dans le  de publication .

>[!CAUTION]
>
>La fonction Groupes *ne doit pas* être la *première ou la seule* fonction de la structure du site.


![chlimage_1-23](assets/chlimage_1-23.png)

En sélectionnant plusieurs modèles de groupe de la communauté, l’administrateur du groupe peut choisir de créer un nouveau groupe dans la communauté.

![chlimage_1-24](assets/chlimage_1-24.png)

## Modifier le modèle de site{#edit-site-template}

Lorsque vous consultez des modèles de site dans la console [principale Modèles de](#site-templates-console)site, il est possible de sélectionner un modèle de site existant à modifier.

Ce processus fournit les mêmes panneaux que la [création d’un modèle](#create-site-template)de site.
