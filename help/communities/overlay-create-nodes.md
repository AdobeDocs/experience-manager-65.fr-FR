---
title: Création de noeuds
seo-title: Create Nodes
description: Recouvrir le système de commentaires
seo-description: Overlay the comments system
uuid: 802ae28b-9989-4c2c-b466-ab76a724efd3
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: cd4f53ee-537b-4f10-a64f-474ba2c44576
exl-id: 3d72cbdf-5eb4-477d-aa61-035a846f7dcb
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 11%

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
   * **[!UICONTROL Créer > Dossier ...]**
      * Entrer un nom: `social`
1. Sélectionner `social` node
   * **[!UICONTROL Créer]** > **[!UICONTROL Dossier...]**
      * Entrer un nom: `commons`
1. Sélectionner `commons` node
   * **[!UICONTROL Créer > Dossier...]**
      * Entrer un nom: `components`
1. Sélectionner `components` node
   * **[!UICONTROL Créer > Dossier..]**.
      * Entrer un nom: `hbs`
1. Sélectionner `hbs` node
   * **[!UICONTROL Créer]** > **[!UICONTROL Créer un composant...]**
      * Saisissez le libellé : `comments`
      * Saisissez le titre : `Comments`
      * Saisissez la description : `List of comments without showing avatars`
      * Super Type : `social/commons/components/comments`
      * Entrez Groupe : `Communities`
      * Cliquez sur **[!UICONTROL Suivant]** Jusqu’à **[!UICONTROL OK]**
1. Sélectionner `comments` node

   * **[!UICONTROL Créer]** > **[!UICONTROL Créer un composant...]**

      * Saisissez le libellé : `comment`
      * Saisissez le titre : `Comment`
      * Saisissez la description : `A comment instance without avatars`
      * Super Type : `social/commons/components/comments/comment`
      * Entrez Groupe : `.hidden`
      * Cliquez sur **[!UICONTROL Suivant]** Jusqu’à **[!UICONTROL OK]**
   * Sélectionnez **[!UICONTROL Enregistrer tout]**
1. Suppression de la valeur par défaut `comments.jsp`
   * Sélectionner un noeud `/apps/social/commons/components/hbs/comments/comments.jsp`
   * Sélectionnez **[!UICONTROL Supprimer]**
1. Supprimez le fichier comment.jsp par défaut.
   * select node `/apps/social/commons/components/hbs/comments/comment/comment.jsp`
   * Sélectionnez **[!UICONTROL Supprimer]**
   * Sélectionnez **[!UICONTROL Enregistrer tout]**

>[!NOTE]
>
>Pour préserver la chaîne d’héritage, la variable `Super Type` (propriété `sling:resourceSuperType`) des composants de superposition sont définis sur la même valeur que la variable `Super Type` des composants superposés, dans ce cas :
>
>* `social/commons/components/comments`
>* `social/commons/components/comments/comment`


Le recouvrement `Type`(propriété `sling:resourceType`) doit être une auto-référence relative afin que tout contenu introuvable dans /apps soit ensuite recherché dans /libs.
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
