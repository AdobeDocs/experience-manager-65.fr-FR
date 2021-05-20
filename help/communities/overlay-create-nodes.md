---
title: Création de noeuds
seo-title: Création de noeuds
description: Recouvrir le système de commentaires
seo-description: Recouvrir le système de commentaires
uuid: 802ae28b-9989-4c2c-b466-ab76a724efd3
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: cd4f53ee-537b-4f10-a64f-474ba2c44576
exl-id: 3d72cbdf-5eb4-477d-aa61-035a846f7dcb
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 8%

---

# Créer des noeuds {#create-nodes}

Recouvrez le système de commentaires avec une version personnalisée en copiant le nombre minimal de fichiers nécessaire de `/libs` dans `/apps` et en les modifiant dans `/apps`.

>[!CAUTION]
>
>Le contenu du dossier /libs n’est jamais modifié, car toute réinstallation ou mise à niveau peut supprimer ou remplacer le dossier /libs alors que le contenu du dossier /apps est conservé.

En utilisant [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md) sur une instance d’auteur, commencez par créer un chemin dans le dossier /apps identique au chemin d’accès aux composants superposés du dossier /libs .

Le chemin en cours de duplication est le suivant :

* `/libs/social/commons/components/hbs/comments/comment`

Certains noeuds du chemin d’accès sont des dossiers et d’autres sont des composants.

1. Accédez à [http://localhost:4502/crx/de/index.jsp](http://localhost:4502/crx/de/index.jsp)
1. Créer `/apps/social` (s’il n’existe pas déjà)
   * Noeud `/apps`
   * **[!UICONTROL Créer > Dossier ...]**
      * Entrer un nom: `social`
1. Noeud `social`
   * **[!UICONTROL Créer]**  >  **[!UICONTROL Dossier...]**
      * Entrer un nom: `commons`
1. Noeud `commons`
   * **[!UICONTROL Créer > Dossier...]**
      * Entrer un nom: `components`
1. Noeud `components`
   * **[!UICONTROL Créer > Dossier..]**.
      * Entrer un nom: `hbs`
1. Noeud `hbs`
   * **[!UICONTROL Créer]**  >  **[!UICONTROL Créer un composant...]**
      * Saisissez le libellé : `comments`
      * Saisissez le titre : `Comments`
      * Saisissez la description : `List of comments without showing avatars`
      * Super Type : `social/commons/components/comments`
      * Entrez Groupe : `Communities`
      * Cliquez sur **[!UICONTROL Suivant]** jusqu’à **[!UICONTROL OK]**
1. Noeud `comments`

   * **[!UICONTROL Créer]**  >  **[!UICONTROL Créer un composant...]**

      * Saisissez le libellé : `comment`
      * Saisissez le titre : `Comment`
      * Saisissez la description : `A comment instance without avatars`
      * Super Type : `social/commons/components/comments/comment`
      * Entrez Groupe : `.hidden`
      * Cliquez sur **[!UICONTROL Suivant]** jusqu’à **[!UICONTROL OK]**
   * Sélectionnez **[!UICONTROL Enregistrer tout]**.
1. Supprimer la valeur par défaut `comments.jsp`
   * Sélectionner le noeud `/apps/social/commons/components/hbs/comments/comments.jsp`
   * Sélectionnez **[!UICONTROL Supprimer]**
1. Supprimez le fichier comment.jsp par défaut.
   * sélectionner le noeud `/apps/social/commons/components/hbs/comments/comment/comment.jsp`
   * Sélectionnez **[!UICONTROL Supprimer]**
   * Sélectionnez **[!UICONTROL Enregistrer tout]**.

>[!NOTE]
>
>Pour préserver la chaîne d’héritage, la valeur `Super Type` (propriété `sling:resourceSuperType`) des composants de recouvrement est définie sur la même valeur que la valeur `Super Type` des composants superposés, dans ce cas :
>
>* `social/commons/components/comments`
>* `social/commons/components/comments/comment`


La `Type` (propriété `sling:resourceType`) de la superposition doit être une auto-référence relative afin que tout contenu introuvable dans /apps soit ensuite recherché dans /libs.
* Nom : `sling:resourceType`
* Type : `String`
* Valeur : `social/commons/components/hbs/comments`

1. Sélectionnez le vert `[+] Add`
   * Nom : `sling:resourceType`
   * Type : `String`
   * Valeur : `social/commons/components/hbs/comments/comment`
1. Sélectionnez le vert `[+] Add`
   * Sélectionnez **[!UICONTROL Enregistrer tout]**.

![create-nodes](assets/create-nodes.png)
