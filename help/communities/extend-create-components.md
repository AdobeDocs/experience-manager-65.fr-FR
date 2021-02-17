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
source-git-commit: 418e7fad2d990f1a7cb3b69ab4c290ca1b7075ba
workflow-type: tm+mt
source-wordcount: '633'
ht-degree: 7%

---


# Créer les composants {#create-the-components}

L&#39;exemple d&#39;extension de composants utilise le système de commentaires, qui est en fait composé de deux composants

* Commentaires - Système de commentaires englobant qui est le composant placé sur une page.
* Commentaire - Composant qui capture une instance d’un commentaire publié.

Les deux composants doivent être mis en place, en particulier si vous personnalisez l’aspect d’un commentaire publié.

>[!NOTE]
>
>Un seul système de commentaires par page de site est autorisé.
>
>De nombreuses fonctions de communautés incluent déjà un système de commentaires dont resourceType peut être modifié pour référencer le système de commentaires étendu.

## Créer le composant Commentaires {#create-the-comments-component}

Ces instructions spécifient une valeur **Groupe** autre que `.hidden` afin que le composant puisse être disponible à partir du navigateur du composant (sidekick).

La suppression du fichier JSP créé automatiquement est due au fait que le fichier HBS par défaut sera utilisé à la place.

1. Accédez à **CRXDE|Lite** ([http://localhost:4502/crx/de/index.jsp](http://localhost:4502/crx/de/index.jsp)).

1. Créez un emplacement pour les applications personnalisées :

   * Sélectionnez le noeud `/apps`

      * **Créer un** dossier nommé  **[!UICONTROL personnalisé]**
   * Sélectionnez le noeud `/apps/custom`

      * **Création de** composants  **[!UICONTROL nommés dossiers]**


1. Sélectionnez le noeud `/apps/custom/components`

   * **[!UICONTROL Créer > Composant..]**

      * **Libellé** :  *commentaires*
      * **Titre** :  *Commentaires Alt*
      * **Description** :  *Autre style de commentaires*
      * **Super Type** :  *social/biens communs/composants/hbs/commentaires*
      * **Groupe** :  *Personnalisé*
   * Sélectionnez **[!UICONTROL Suivant]**
   * Sélectionnez **[!UICONTROL Suivant]**
   * Sélectionnez **[!UICONTROL Suivant]**
   * **[!UICONTROL Cliquez sur OK]**


1. Développez le noeud qui vient d’être créé : `/apps/custom/components/comments`
1. Sélectionner **[!UICONTROL Enregistrer tout]**
1. Faites un clic-droit `comments.jsp`
1. Sélectionnez **[!UICONTROL Supprimer]**
1. Sélectionner **[!UICONTROL Enregistrer tout]**

![create-component](assets/create-component.png)

### Créer le composant Commentaires enfant {#create-the-child-comment-component}

Ces instructions définissent **Groupe** sur `.hidden` car seul le composant parent doit être inclus dans une page.

La suppression du fichier JSP créé automatiquement est due au fait que le fichier HBS par défaut sera utilisé à la place.

1. Accédez au noeud `/apps/custom/components/comments`
1. Cliquez avec le bouton droit sur le noeud.

   * Sélectionnez **[!UICONTROL Créer]** > **[!UICONTROL Composant...]**

      * **Libellé** :  *commentaire*
      * **Titre** :  *Commentaire Alt*
      * **Description** :  *Autre style de commentaire*
      * **Super Type** :  *social/commons/composants/hbs/commentaires/commentaire*
      * **Groupe**: `*.hidden*`
   * Sélectionnez **[!UICONTROL Suivant]**
   * Sélectionnez **[!UICONTROL Suivant]**
   * Sélectionnez **[!UICONTROL Suivant]**
   * **[!UICONTROL Cliquez sur OK]**


1. Développez le noeud qui vient d’être créé : `/apps/custom/components/comments/comment`
1. Sélectionner **[!UICONTROL Enregistrer tout]**
1. Faites un clic-droit `comment.jsp`
1. Sélectionnez **[!UICONTROL Supprimer]**
1. Sélectionner **[!UICONTROL Enregistrer tout]**

![create-child-component](assets/create-child-component.png)

![create-component-crxde](assets/create-component-crxde.png)

### Copier et modifier les scripts HBS par défaut {#copy-and-modify-the-default-hbs-scripts}

Utilisation de [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md) :

* Copier `comments.hbs`

   * De [/libs/social/commons/components/hbs/commentaires](http://localhost:4502/crx/de/index.jsp#/libs/social/commons/components/hbs/comments)
   * Pour [/apps/custom/components/commentaires](http://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments)

* Modifiez `comments.hbs` en :

   * Modifiez la valeur de l’attribut `data-scf-component` (~ligne 20) :

      * Origine `social/commons/components/hbs/comments`
      * To `/apps/custom/components/comments`
   * Modifier pour inclure le composant de commentaire personnalisé (~ligne 75) :

      * Remplacer `{{include this resourceType='social/commons/components/hbs/comments/comment'}}`
      * Par `{{include this resourceType='/apps/custom/components/comments/comment'}}`


* Copier `comment.hbs`

   * De [/libs/social/commons/components/hbs/commentaires/comment](http://localhost:4502/crx/de/index.jsp#/libs/social/commons/components/hbs/comments/comment)
   * Pour [/apps/custom/components/commentaires/comment](http://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments/comment)

* Modifiez `comment.hbs` en :

   * Modifier la valeur de l’attribut data-scf-component (~ ligne 19)

      * Origine `social/commons/components/hbs/comments/comment`
      * À `/apps/custom/components/comments/comment`

* Sélectionner le noeud `/apps/custom`
* Sélectionner **[!UICONTROL Enregistrer tout]**

## Création d’un dossier de bibliothèques clientes {#create-a-client-library-folder}

Pour éviter d&#39;avoir à inclure explicitement cette bibliothèque cliente, la valeur de catégorie de la bibliothèque clientlib du système de commentaires par défaut peut être utilisée ( `cq.social.author.hbs.comments`), mais cette bibliothèque cliente sera également incluse pour toutes les instances du composant par défaut.

Utilisation de [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md) :

* Sélectionner le noeud `/apps/custom/components/comments`
* Sélectionnez **[!UICONTROL Créer un noeud]**

   * **Nom** : `clientlibs`
   * **Type** : `cq:ClientLibraryFolder`
   * Ajoutez à l&#39;onglet **[!UICONTROL Propriétés]** :

      * **** `categories` **** `String` **NomTypeValeur** `cq.social.author.hbs.comments` `Multi`
      * **** `dependencies` **** `String` **NomTypeValeur** `cq.social.scf` `Multi`

* Sélectionner **[!UICONTROL Enregistrer tout]**
* Avec le noeud `/apps/custom/components/comments/clientlib`s sélectionné, créez 3 fichiers :

   * **Nom** : `css.txt`
   * **Nom** : `js.txt`
   * **Nom** : customcommentsystem.js

* Saisissez &quot;customcommentsystem.js&quot; comme contenu de `js.txt`
* Sélectionner **[!UICONTROL Enregistrer tout]**

![commentaires-clientlibs](assets/comments-clientlibs.png)

## Enregistrer le modèle et la Vue SCF {#register-the-scf-model-view}

Lors de l&#39;extension (remplacement) d&#39;un composant SCF, resourceType est différent (l&#39;incrustation utilise le mécanisme de recherche relatif qui recherche `/apps` avant `/libs` pour que resourceType reste identique). C&#39;est pourquoi il est nécessaire d&#39;écrire du code JavaScript (dans la bibliothèque cliente) pour enregistrer le modèle et la vue SCF JS pour le type de ressource personnalisé.

Saisissez le texte suivant comme contenu de `customcommentsystem.js` :

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

* Sélectionner **[!UICONTROL Enregistrer tout]**

## Publier l’application {#publish-the-app}

Pour expérimenter le composant étendu dans l’environnement de publication, il est nécessaire de répliquer le composant personnalisé.

L&#39;une des façons de le faire est :

* De la navigation globale,

   * Sélectionnez **[!UICONTROL Outils]** > **[!UICONTROL Déploiement]** > **[!UICONTROL Réplication]**
   * Sélectionnez **[!UICONTROL Activer l&#39;arborescence]**
   * Définissez `Start Path` sur `/apps/custom`
   * Décochez **[!UICONTROL Modifié uniquement]**.
   * Bouton Sélectionner **[!UICONTROL Activer]**

