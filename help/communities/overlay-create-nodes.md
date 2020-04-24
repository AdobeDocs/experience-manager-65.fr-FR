---
title: Création de noeuds
seo-title: Création de noeuds
description: Recouvrement du système de commentaires
seo-description: Recouvrement du système de commentaires
uuid: 802ae28b-9989-4c2c-b466-ab76a724efd3
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: cd4f53ee-537b-4f10-a64f-474ba2c44576
translation-type: tm+mt
source-git-commit: 48afa2146d0dcbab4beaa1044645c269b49fd7ff

---


# Création de noeuds {#create-nodes}

Incrustez le système de commentaires avec une version personnalisée en copiant le nombre minimal de fichiers nécessaire `/libs` dans `/apps` et en les modifiant dans `/apps`.

>[!CAUTION]
>
>Le contenu du dossier /libs n&#39;est jamais modifié, car toute réinstallation ou mise à niveau peut supprimer ou remplacer le dossier /libs, tandis que le contenu du dossier /apps reste intact.


A l’aide de [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md) sur une instance d’auteur, commencez par créer un chemin dans le dossier /apps identique au chemin d’accès aux composants superposés du dossier /libs.

Le chemin dupliqué est le suivant :

* `/libs/social/commons/components/hbs/comments/comment`

Certains noeuds du chemin d’accès sont des dossiers et d’autres sont des composants.

1. Accédez à [http://localhost:4502/crx/de/index.jsp](http://localhost:4502/crx/de/index.jsp)
1. Créer `/apps/social` (s’il n’existe pas déjà)
   * Sélectionner le `/apps` noeud
   * **[!UICONTROL Créer > Dossier...]**
      * Entrer un nom: `social`
1. Sélectionner le `social` noeud
   * **[!UICONTROL Créer]** > **[!UICONTROL Dossier...]**
      * Entrer un nom: `commons`
1. Sélectionner le `commons` noeud
   * **[!UICONTROL Créer > Dossier...]**
      * Entrer un nom: `components`
1. Sélectionner le `components` noeud
   * **[!UICONTROL Créer > Dossier..]**.
      * Entrer un nom: `hbs`
1. Sélectionner le `hbs` noeud
   * **[!UICONTROL Créer]** > **[!UICONTROL Créer un composant...]**
      * Entrez une étiquette : `comments`
      * Enter Title: `Comments`
      * Enter Description: `List of comments without showing avatars`
      * Super Type : `social/commons/components/comments`
      * Entrez un groupe : `Communities`
      * Cliquez sur **[!UICONTROL Suivant]** jusqu’à **[!UICONTROL OK]**
1. Sélectionner le `comments` noeud

   * **[!UICONTROL Créer > Créer un composant...]**

      * Entrez une étiquette : `comment`
      * Enter Title: `Comment`
      * Enter Description: `A comment instance without avatars`
      * Super Type : `social/commons/components/comments/comment`
      * Entrez un groupe : `.hidden`
      * Cliquez sur **[!UICONTROL Suivant]** jusqu’à **[!UICONTROL OK]**
   * Select **[!UICONTROL Save All]**
1. Supprimer la valeur par défaut `comments.jsp`
   * Sélectionner un noeud `/apps/social/commons/components/hbs/comments/comments.jsp`
   * Sélectionner **[!UICONTROL Supprimer]**
1. Supprimer le fichier comment.jsp par défaut
   * sélectionner un noeud `/apps/social/commons/components/hbs/comments/comment/comment.jsp`
   * Sélectionner **[!UICONTROL Supprimer]**
   * Select **[!UICONTROL Save All]**

>[!NOTE]
>
>Afin de préserver la chaîne d’héritage, la `Super Type` (propriété `sling:resourceSuperType`) des composants d’incrustation est définie sur la même valeur que celle `Super Type` des composants superposés, dans ce cas :
>
>* `social/commons/components/comments`
>* `social/commons/components/comments/comment`
>



La propriété `Type`(property `sling:resourceType`) de l’incrustation doit être une auto-référence relative afin que tout contenu non trouvé dans /apps soit ensuite recherché dans /libs.
* Nom: `sling:resourceType`
* Type: `String`
* Valeur: `social/commons/components/hbs/comments`

1. Sélectionnez le vert `[+] Add`
   * Nom: `sling:resourceType`
   * Type: `String`
   * Valeur: `social/commons/components/hbs/comments/comment`
1. Sélectionnez le vert `[+] Add`
   * Select **[!UICONTROL Save All]**

![chlimage_1-4](assets/chlimage_1-4.png)

