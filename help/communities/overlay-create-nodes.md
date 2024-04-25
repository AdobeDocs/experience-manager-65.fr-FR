---
title: Création de noeuds
description: Découvrez comment superposer le système de commentaires avec une version personnalisée en copiant le nombre minimal de fichiers nécessaires à partir de /libs et en les modifiant dans /apps.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 3d72cbdf-5eb4-477d-aa61-035a846f7dcb
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 3%

---

# Création de noeuds {#create-nodes}

Recouvrez le système de commentaires avec une version personnalisée en copiant le nombre minimal de fichiers nécessaire à partir de `/libs` into `/apps` et les modifier dans `/apps`.

>[!CAUTION]
>
>Le contenu du dossier /libs n’est jamais modifié, car toute réinstallation ou mise à niveau peut supprimer ou remplacer le dossier /libs alors que le contenu du dossier /apps est conservé.

Utilisation [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md) sur une instance d’auteur, commencez par créer un chemin d’accès dans le dossier /apps identique au chemin d’accès aux composants superposés du dossier /libs .

Le chemin en cours de duplication est le suivant :

* `/libs/social/commons/components/hbs/comments/comment`

Certains noeuds du chemin d’accès sont des dossiers et d’autres sont des composants.

1. Accédez à [http://localhost:4502/crx/de/index.jsp](http://localhost:4502/crx/de/index.jsp)
1. Créer `/apps/social` (s’il n’existe pas déjà)
   * Sélectionner `/apps` node
   * **[!UICONTROL Créer > Dossier]**
      * Saisissez le nom : `social`
1. Sélectionner `social` node
   * **[!UICONTROL Créer]** > **[!UICONTROL Dossier]**
      * Saisissez le nom : `commons`
1. Sélectionner `commons` node
   * **[!UICONTROL Créer > Dossier]**
      * Saisissez le nom : `components`
1. Sélectionner `components` node
   * **[!UICONTROL Créer > Dossier]**.
      * Saisissez le nom : `hbs`
1. Sélectionner `hbs` node
   * **[!UICONTROL Créer]** > **[!UICONTROL Créer un composant]**
      * Saisissez le libellé : `comments`
      * Saisissez le titre : `Comments`
      * Saisissez la description : `List of comments without showing avatars`
      * Super Type : `social/commons/components/comments`
      * Entrez Groupe : `Communities`
      * Cliquez sur **[!UICONTROL Suivant]** Jusqu’à **[!UICONTROL OK]**
1. Sélectionner `comments` node

   * **[!UICONTROL Créer]** > **[!UICONTROL Créer un composant]**

      * Saisissez le libellé : `comment`
      * Saisissez le titre : `Comment`
      * Saisissez la description : `A comment instance without avatars`
      * Super Type : `social/commons/components/comments/comment`
      * Entrez Groupe : `.hidden`
      * Cliquez sur **[!UICONTROL Suivant]** Jusqu’à **[!UICONTROL OK]**
   * Sélectionner **[!UICONTROL Enregistrer tout]**
1. Suppression de la valeur par défaut `comments.jsp`
   * Sélectionner un noeud `/apps/social/commons/components/hbs/comments/comments.jsp`
   * Sélectionner **[!UICONTROL Supprimer]**
1. Supprimez le fichier comment.jsp par défaut.
   * select node `/apps/social/commons/components/hbs/comments/comment/comment.jsp`
   * Sélectionner **[!UICONTROL Supprimer]**
   * Sélectionner **[!UICONTROL Enregistrer tout]**

>[!NOTE]
>
>Pour préserver la chaîne d’héritage, la variable `Super Type` (propriété `sling:resourceSuperType`) des composants de superposition sont définis sur la même valeur que la variable `Super Type` des composants superposés, dans ce cas :
>
>* `social/commons/components/comments`
>* `social/commons/components/comments/comment`

Le recouvrement propre `Type`(propriété `sling:resourceType`) doit être une auto-référence relative afin que tout contenu introuvable dans /apps soit ensuite recherché dans /libs.
* Nom : `sling:resourceType`
* Type : `String`
* Valeur : `social/commons/components/hbs/comments`

1. Sélectionnez le vert `[+] Add`
   * Nom : `sling:resourceType`
   * Type : `String`
   * Valeur : `social/commons/components/hbs/comments/comment`
1. Sélectionnez le vert `[+] Add`
   * Sélectionner **[!UICONTROL Enregistrer tout]**

![create-nodes](assets/create-nodes.png)
