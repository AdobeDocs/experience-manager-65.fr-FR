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

Recouvrez le système de commentaires avec une version personnalisée en copiant le nombre minimal de fichiers nécessaires de `/libs` vers `/apps` et en les modifiant dans `/apps`.

>[!CAUTION]
>
>Le contenu du dossier /libs n’est jamais modifié, car toute réinstallation ou mise à niveau peut supprimer ou remplacer le dossier /libs alors que le contenu du dossier /apps est conservé.

En utilisant [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md) sur une instance d’auteur, commencez par créer un chemin d’accès dans le dossier /apps identique au chemin d’accès aux composants superposés dans le dossier /libs.

Le chemin en cours de duplication est le suivant :

* `/libs/social/commons/components/hbs/comments/comment`

Certains noeuds du chemin d’accès sont des dossiers et d’autres sont des composants.

1. Accédez à [http://localhost:4502/crx/de/index.jsp](http://localhost:4502/crx/de/index.jsp)
1. Créer `/apps/social` (s’il n’existe pas déjà)
   * Sélectionner le noeud `/apps`
   * **[!UICONTROL Créer > Dossier]**
      * Saisissez le nom : `social`
1. Sélectionner le noeud `social`
   * **[!UICONTROL Créer]** > **[!UICONTROL Dossier]**
      * Saisissez le nom : `commons`
1. Sélectionner le noeud `commons`
   * **[!UICONTROL Créer > Dossier]**
      * Saisissez le nom : `components`
1. Sélectionner le noeud `components`
   * **[!UICONTROL Créer > Dossier]**.
      * Saisissez le nom : `hbs`
1. Sélectionner le noeud `hbs`
   * **[!UICONTROL Créer]** > **[!UICONTROL Créer un composant]**
      * Saisir le libellé : `comments`
      * Saisissez le titre : `Comments`
      * Saisissez la description : `List of comments without showing avatars`
      * Super Type : `social/commons/components/comments`
      * Entrée dans le groupe : `Communities`
      * Cliquez sur **[!UICONTROL Suivant]** jusqu’à **[!UICONTROL OK]**
1. Sélectionner le noeud `comments`

   * **[!UICONTROL Créer]** > **[!UICONTROL Créer un composant]**

      * Saisir le libellé : `comment`
      * Saisissez le titre : `Comment`
      * Saisissez la description : `A comment instance without avatars`
      * Super Type : `social/commons/components/comments/comment`
      * Entrée dans le groupe : `.hidden`
      * Cliquez sur **[!UICONTROL Suivant]** jusqu’à **[!UICONTROL OK]**
   * Sélectionnez **[!UICONTROL Enregistrer tout]**
1. Supprimer le `comments.jsp` par défaut
   * Sélectionner le noeud `/apps/social/commons/components/hbs/comments/comments.jsp`
   * Sélectionnez **[!UICONTROL Supprimer]**
1. Supprimez le fichier comment.jsp par défaut.
   * select node `/apps/social/commons/components/hbs/comments/comment/comment.jsp`
   * Sélectionnez **[!UICONTROL Supprimer]**
   * Sélectionnez **[!UICONTROL Enregistrer tout]**

>[!NOTE]
>
>Pour préserver la chaîne d’héritage, les `Super Type` (propriété `sling:resourceSuperType`) des composants de recouvrement sont définis sur la même valeur que le `Super Type` des composants superposés, dans ce cas :
>
>* `social/commons/components/comments`
>* `social/commons/components/comments/comment`

Le `Type` de la superposition (propriété `sling:resourceType`) doit être une auto-référence relative afin que tout contenu introuvable dans /apps soit ensuite recherché dans /libs.
* Nom : `sling:resourceType`
* Type : `String`
* Valeur : `social/commons/components/hbs/comments`

1. Sélectionnez le vert `[+] Add`
   * Nom : `sling:resourceType`
   * Type : `String`
   * Valeur : `social/commons/components/hbs/comments/comment`
1. Sélectionnez le vert `[+] Add`
   * Sélectionnez **[!UICONTROL Enregistrer tout]**

![create-nodes](assets/create-nodes.png)
