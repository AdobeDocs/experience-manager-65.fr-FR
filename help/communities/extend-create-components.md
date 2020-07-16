---
title: Création des composants
seo-title: Création des composants
description: Création du composant Commentaires
seo-description: Création du composant Commentaires
uuid: ea6e00d4-1db7-40ef-ae49-9ec55df58adf
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 83c4f18a-d7d6-4090-88c7-41a9075153b5
translation-type: tm+mt
source-git-commit: 230c700d87d82d248b7d0bbc45c69c5c2b0e3ff8
workflow-type: tm+mt
source-wordcount: '633'
ht-degree: 6%

---


# Création des composants  {#create-the-components}

L&#39;exemple d&#39;extension de composants utilise le système de commentaires, qui est en fait composé de deux composants

* Commentaires - Système de commentaires englobant qui est le composant placé sur une page.
* Commentaire - Composant qui capture une instance d’un commentaire publié.

Les deux composants doivent être mis en place, en particulier si vous personnalisez l’aspect d’un commentaire publié.

>[!NOTE]
>
>Un seul système de commentaires par page de site est autorisé.
>
>De nombreuses fonctions de communautés incluent déjà un système de commentaires dont resourceType peut être modifié pour référencer le système de commentaires étendu.


## Create the Comments Component {#create-the-comments-component}

Ces instructions spécifient une valeur de **groupe** autre que `.hidden` afin que le composant puisse être rendu disponible à partir du navigateur de composants (sidekick).

La suppression du fichier JSP créé automatiquement est due au fait que le fichier HBS par défaut sera utilisé à la place.

1. Browse to **CRXDE|Lite** ([http://localhost:4502/crx/de/index.jsp](http://localhost:4502/crx/de/index.jsp))

1. Créez un emplacement pour les applications personnalisées :

   * Sélectionner le `/apps` noeud

      * **Créer un dossier** nommé **[!UICONTROL personnalisé]**
   * Sélectionner le `/apps/custom` noeud

      * **Créer un dossier** nommé **[!UICONTROL composants]**


1. Sélectionner le `/apps/custom/components` noeud

   * **[!UICONTROL Créer > Composant..]**

      * **Libellé**: *commentaires*
      * **Titre**: *Commentaires Alt*
      * **Description**: *Autre style de commentaires*
      * **Super Type**: *social/biens communs/composants/hbs/commentaires*
      * **Groupe**: *Personnalisé*
   * Sélectionnez **[!UICONTROL Suivant]**
   * Sélectionnez **[!UICONTROL Suivant]**
   * Sélectionnez **[!UICONTROL Suivant]**
   * **[!UICONTROL Cliquez sur OK]**


1. Développez le noeud qui vient d’être créé : `/apps/custom/components/comments`
1. Select **[!UICONTROL Save All]**
1. Right-click `comments.jsp`
1. Sélectionner **[!UICONTROL Supprimer]**
1. Select **[!UICONTROL Save All]**

![chlimage_1-70](assets/chlimage_1-70.png)

### Créer un composant de commentaire enfant {#create-the-child-comment-component}

Ces instructions définissent **le groupe** sur `.hidden` car seul le composant parent doit être inclus dans une page.

La suppression du fichier JSP créé automatiquement est due au fait que le fichier HBS par défaut sera utilisé à la place.

1. Navigate to the `/apps/custom/components/comments` node
1. Cliquez avec le bouton droit sur le noeud.

   * Sélectionnez **[!UICONTROL Créer] > **[!UICONTROL Composant...]**

      * **Libellé**: *commentaire*
      * **Titre**: *Commentaire Alt*
      * **Description**: *Autre style de commentaire*
      * **Super Type**: *social/commons/composants/hbs/commentaires/commentaire*
      * **Groupe**: `*.hidden*`
   * Sélectionnez **[!UICONTROL Suivant]**
   * Sélectionnez **[!UICONTROL Suivant]**
   * Sélectionnez **[!UICONTROL Suivant]**
   * **[!UICONTROL Cliquez sur OK]**


1. Développez le noeud qui vient d’être créé : `/apps/custom/components/comments/comment`
1. Select **[!UICONTROL Save All]**
1. Right-click `comment.jsp`
1. Sélectionner **[!UICONTROL Supprimer]**
1. Select **[!UICONTROL Save All]**

![chlimage_1-71](assets/chlimage_1-71.png)

![chlimage_1-72](assets/chlimage_1-72.png)

### Copier et modifier les scripts HBS par défaut {#copy-and-modify-the-default-hbs-scripts}

Using [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md):

* Copier `comments.hbs`

   * De [/libs/social/commons/components/hbs/commentaires](http://localhost:4502/crx/de/index.jsp#/libs/social/commons/components/hbs/comments)
   * Pour [/applications/personnalisation/composants/commentaires](http://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments)

* Modifier `comments.hbs` :

   * Modifiez la valeur de l’ `data-scf-component` attribut (~ligne 20) :

      * Origine `social/commons/components/hbs/comments`
      * To `/apps/custom/components/comments`
   * Modifier pour inclure le composant de commentaire personnalisé (~ligne 75) :

      * Remplacer `{{include this resourceType='social/commons/components/hbs/comments/comment'}}`
      * Par `{{include this resourceType='/apps/custom/components/comments/comment'}}`


* Copier `comment.hbs`

   * De [/libs/social/commons/composants/hbs/commentaires/commentaires](http://localhost:4502/crx/de/index.jsp#/libs/social/commons/components/hbs/comments/comment)
   * Pour [/applications/personnalisation/composants/commentaires/commentaire](http://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments/comment)

* Modifier `comment.hbs` :

   * Modifier la valeur de l’attribut data-scf-component (~ ligne 19)

      * Origine `social/commons/components/hbs/comments/comment`
      * To `/apps/custom/components/comments/comment`

* Sélectionner le `/apps/custom` noeud
* Select **[!UICONTROL Save All]**

## Création d’un dossier de bibliothèques clientes {#create-a-client-library-folder}

Pour éviter d&#39;avoir à inclure explicitement cette bibliothèque cliente, la valeur de catégorie de la bibliothèque clientlib du système de commentaires par défaut peut être utilisée ( `cq.social.author.hbs.comments`), mais cette bibliothèque clientlib sera également incluse pour toutes les instances du composant par défaut.

Using [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md):

* Sélectionner le `/apps/custom/components/comments` noeud
* Sélectionner **[!UICONTROL Créer un noeud]**

   * **Nom** : `clientlibs`
   * **Type** : `cq:ClientLibraryFolder`
   * Ajoutez à l&#39;onglet **[!UICONTROL Propriétés]** :

      * **Nom** `categories`**Type** `String` **Valeur** `cq.social.author.hbs.comments` `Multi`
      * **Nom** `dependencies`**Type** `String` **Valeur** `cq.social.scf` `Multi`

* Select **[!UICONTROL Save All]**
* Le noeud `/apps/custom/components/comments/clientlib`s étant sélectionné, créez 3 fichiers :

   * **Nom** : `css.txt`
   * **Nom** : `js.txt`
   * **Nom**: customcommentsystem.js

* Saisissez &quot;customcommentsystem.js&quot; comme contenu de `js.txt`
* Select **[!UICONTROL Save All]**

![chlimage_1-73](assets/chlimage_1-73.png)

## Enregistrement du modèle et de la Vue SCF {#register-the-scf-model-view}

Lors de l&#39;extension (remplacement) d&#39;un composant SCF, resourceType est différent (l&#39;incrustation utilise le mécanisme de recherche relatif qui effectue les recherches `/apps` avant `/libs` , de sorte que resourceType reste identique). C&#39;est pourquoi il est nécessaire d&#39;écrire du code JavaScript (dans la bibliothèque cliente) pour enregistrer le modèle et la vue SCF JS pour le type de ressource personnalisé.

Saisissez le texte suivant comme contenu de `customcommentsystem.js`:

### customcommentsystem.js {#customcommentsystem-js}

```xml
(function($CQ, _, Backbone, SCF) {
    "use strict";

    var CustomComment = SCF.Components["social/commons/components/hbs/comments/comment"].Model;
    var CustomCommentView = SCF.Components["social/commons/components/hbs/comments/comment"].View;

    var CustomCommentSystem = SCF.Components["social/commons/components/hbs/comments"].Model;
    var CustomCommentSystemView = SCF.Components["social/commons/components/hbs/comments"].View;

    SCF.registerComponent('/apps/custom/components/comments/comment', CustomComment, CustomCommentView);
    SCF.registerComponent('/apps/custom/components/comments', CustomCommentSystem, CustomCommentSystemView);

})($CQ, _, Backbone, SCF);
```

* Select **[!UICONTROL Save All]**

## Publication de l’application {#publish-the-app}

Pour expérimenter le composant étendu dans l’environnement de publication, il est nécessaire de répliquer le composant personnalisé.

Une façon de le faire est

* A partir de la navigation globale

   * Select **[!UICONTROL Tools]** > **[!UICONTROL Deployment]** > **[!UICONTROL Replication]**
   * Sélectionner **[!UICONTROL Activer l&#39;arborescence]**
   * Définir `Start Path` sur `/apps/custom`
   * Désélectionner **[!UICONTROL uniquement modifié]**
   * Sélectionner le bouton **[!UICONTROL Activer]**

