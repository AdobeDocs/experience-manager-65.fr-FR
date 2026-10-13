---
title: Créer des nœuds
description: Découvrez comment remplacer le système de commentaires par une version personnalisée en copiant le nombre minimal de fichiers nécessaires depuis /libs et en les modifiant dans /apps.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 3d72cbdf-5eb4-477d-aa61-035a846f7dcb
solution: Experience Manager
feature: Communities
role: Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: b013f126-a97e-52d1-9f79-cb5bbb12114e
    internal-label: Communities
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 5%
---
# Créer des nœuds {#create-nodes}

Recouvrez le système de commentaires avec une version personnalisée en copiant le nombre minimal de fichiers nécessaires depuis `/libs` dans `/apps` et en les modifiant dans `/apps`.

>[!CAUTION]
>
>Le contenu du dossier /libs n’est jamais modifié, car toute réinstallation ou mise à niveau peut supprimer ou remplacer le dossier /libs sans toucher au contenu du dossier /apps.

À l’aide de [&#128279;](../../help/sites-developing/developing-with-crxde-lite.md) sur une instance de création, commencez par créer un chemin d’accès dans le dossier /apps identique au chemin d’accès aux composants superposés dans le dossier /libs.

Le chemin d’accès en cours de duplication est :

* `/libs/social/commons/components/hbs/comments/comment`

Certains nœuds du chemin d’accès sont des dossiers et d’autres des composants.

1. Accédez à [&#128279;](http://localhost:4502/crx/de/index.jsp)
1. Créer un `/apps/social` (s’il n’existe pas déjà)
   * Sélectionner `/apps` nœud
   * **[!UICONTROL Créer > Dossier]**
     * Enter Name: `social`
1. Sélectionner `social` nœud
   * **[!UICONTROL Créer]** > **[!UICONTROL Dossier]**
     * Enter Name: `commons`
1. Sélectionner `commons` nœud
   * **[!UICONTROL Créer > Dossier]**
     * Enter Name: `components`
1. Sélectionner `components` nœud
   * **[!UICONTROL Créer > Dossier]**.
     * Enter Name: `hbs`
1. Sélectionner `hbs` nœud
   * **[!UICONTROL Créer]** > **[!UICONTROL Créer un composant]**
     * Saisir le libellé : `comments`
     * Saisir le titre : `Comments`
     * Saisir la description : `List of comments without showing avatars`
     * Super Type : `social/commons/components/comments`
     * Saisir un groupe : `Communities`
     * Cliquez sur **[!UICONTROL Suivant]** jusqu’à **[!UICONTROL OK]**
1. Sélectionner `comments` nœud

   * **[!UICONTROL Créer]** > **[!UICONTROL Créer un composant]**

     * Saisir le libellé : `comment`
     * Saisir le titre : `Comment`
     * Saisir la description : `A comment instance without avatars`
     * Super Type : `social/commons/components/comments/comment`
     * Saisir un groupe : `.hidden`
     * Cliquez sur **[!UICONTROL Suivant]** jusqu’à **[!UICONTROL OK]**
   * Sélectionnez **[!UICONTROL Enregistrer tout]**
1. Supprimer le `comments.jsp` par défaut
   * Sélectionner le `/apps/social/commons/components/hbs/comments/comments.jsp` de nœud
   * Sélectionnez **[!UICONTROL Supprimer]**
1. Supprimez le fichier comment.jsp par défaut
   * sélectionner le nœud `/apps/social/commons/components/hbs/comments/comment/comment.jsp`
   * Sélectionnez **[!UICONTROL Supprimer]**
   * Sélectionnez **[!UICONTROL Enregistrer tout]**

>[!NOTE]
>
>Pour préserver la chaîne d’héritage, les `Super Type` (`sling:resourceSuperType` de propriété) des composants de recouvrement sont définis sur la même valeur que la `Super Type` des composants en cours de recouvrement, dans ce cas :
>
>* `social/commons/components/comments`
>* `social/commons/components/comments/comment`

La propre `Type` du recouvrement (propriété `sling:resourceType`) doit être une auto-référence relative afin que tout contenu non trouvé dans /apps soit recherché dans /libs.
* Nom : `sling:resourceType`
* Type : `String`
* Valeur : `social/commons/components/hbs/comments`

1. Sélectionner la `[+] Add` verte
   * Nom : `sling:resourceType`
   * Type : `String`
   * Valeur : `social/commons/components/hbs/comments/comment`
1. Sélectionner la `[+] Add` verte
   * Sélectionnez **[!UICONTROL Enregistrer tout]**

![create-nodes](assets/create-nodes.png)
