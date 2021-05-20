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
exl-id: 2e02db9f-294d-4d4a-92da-3ab1d38416ab
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '633'
ht-degree: 7%

---

# Création des composants {#create-the-components}

L’exemple d’extension de composants utilise le système de commentaires, qui est en fait composé de deux composants.

* Commentaires : système de commentaires englobant qui est le composant placé sur une page.
* Commentaire : composant qui capture une instance d’un commentaire publié.

Les deux composants doivent être mis en place, en particulier si vous personnalisez l’apparence d’un commentaire publié.

>[!NOTE]
>
>Un seul système de commentaires par page de site est autorisé.
>
>De nombreuses fonctionnalités de Communities incluent déjà un système de commentaires dont resourceType peut être modifié pour référencer le système de commentaires étendu.

## Créer le composant Commentaires {#create-the-comments-component}

Ces instructions spécifient une valeur **Groupe** autre que `.hidden` afin que le composant puisse être rendu disponible à partir de l’explorateur de composants (sidekick).

La suppression du fichier JSP créé automatiquement est due au fait que le fichier HBS par défaut sera utilisé à la place.

1. Accédez à **CRXDE|Lite** ([http://localhost:4502/crx/de/index.jsp](http://localhost:4502/crx/de/index.jsp))

1. Créez un emplacement pour les applications personnalisées :

   * Sélectionnez le noeud `/apps`

      * **Créer un** dossier nommé  **[!UICONTROL personnalisé]**
   * Sélectionnez le noeud `/apps/custom`

      * **Création de** composants nommés  **[!UICONTROL dossiers]**


1. Sélectionnez le noeud `/apps/custom/components`

   * **[!UICONTROL Créer > Composant..]**

      * **Libellé** :  *commentaires*
      * **Titre** :  *Commentaires Alt*
      * **Description** :  *Style de commentaire alternatif*
      * **Super Type** :  *social/commons/components/hbs/comments*
      * **Groupe** :  *Personnalisé*
   * Sélectionnez **[!UICONTROL Suivant]**
   * Sélectionnez **[!UICONTROL Suivant]**
   * Sélectionnez **[!UICONTROL Suivant]**
   * **[!UICONTROL Cliquez sur OK]**


1. Développez le noeud que vous venez de créer : `/apps/custom/components/comments`
1. Sélectionnez **[!UICONTROL Enregistrer tout]**.
1. Faites un clic-droit `comments.jsp`
1. Sélectionnez **[!UICONTROL Supprimer]**
1. Sélectionnez **[!UICONTROL Enregistrer tout]**.

![create-component](assets/create-component.png)

### Créer le composant Commentaire enfant {#create-the-child-comment-component}

Ces instructions définissent **Groupe** sur `.hidden`, car seul le composant parent doit être inclus dans une page.

La suppression du fichier JSP créé automatiquement est due au fait que le fichier HBS par défaut sera utilisé à la place.

1. Accédez au noeud `/apps/custom/components/comments`
1. Cliquez avec le bouton droit sur le noeud

   * Sélectionnez **[!UICONTROL Créer]** > **[!UICONTROL Composant...]**

      * **Libellé** :  *comment*
      * **Titre** :  *Commentaire Alt*
      * **Description** :  *Autre style de commentaire*
      * **Super Type** :  *social/commons/components/hbs/comments/comment*
      * **Groupe**: `*.hidden*`
   * Sélectionnez **[!UICONTROL Suivant]**
   * Sélectionnez **[!UICONTROL Suivant]**
   * Sélectionnez **[!UICONTROL Suivant]**
   * **[!UICONTROL Cliquez sur OK]**


1. Développez le noeud que vous venez de créer : `/apps/custom/components/comments/comment`
1. Sélectionnez **[!UICONTROL Enregistrer tout]**.
1. Faites un clic-droit `comment.jsp`
1. Sélectionnez **[!UICONTROL Supprimer]**
1. Sélectionnez **[!UICONTROL Enregistrer tout]**.

![create-child-component](assets/create-child-component.png)

![create-component-crxde](assets/create-component-crxde.png)

### Copiez et modifiez les scripts HBS par défaut {#copy-and-modify-the-default-hbs-scripts}

Utilisation de [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md) :

* Copier `comments.hbs`

   * De [/libs/social/commons/components/hbs/comments](http://localhost:4502/crx/de/index.jsp#/libs/social/commons/components/hbs/comments)
   * À [/apps/custom/components/comments](http://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments)

* Modifiez `comments.hbs` en :

   * Modifiez la valeur de l’attribut `data-scf-component` (~line 20) :

      * Origine `social/commons/components/hbs/comments`
      * To `/apps/custom/components/comments`
   * Modifiez pour inclure le composant de commentaire personnalisé (~line 75) :

      * Remplacer `{{include this resourceType='social/commons/components/hbs/comments/comment'}}`
      * Par `{{include this resourceType='/apps/custom/components/comments/comment'}}`


* Copier `comment.hbs`

   * De [/libs/social/commons/components/hbs/comments/comment](http://localhost:4502/crx/de/index.jsp#/libs/social/commons/components/hbs/comments/comment)
   * À [/apps/custom/components/comments/comment](http://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments/comment)

* Modifiez `comment.hbs` en :

   * Modifier la valeur de l’attribut data-scf-component (~ ligne 19)

      * Origine `social/commons/components/hbs/comments/comment`
      * À `/apps/custom/components/comments/comment`

* Noeud `/apps/custom`
* Sélectionnez **[!UICONTROL Enregistrer tout]**.

## Création d’un dossier de bibliothèques clientes {#create-a-client-library-folder}

Pour éviter d’avoir à inclure explicitement cette bibliothèque cliente, la valeur de catégories de la bibliothèque cliente du système de commentaires par défaut peut être utilisée ( `cq.social.author.hbs.comments`), mais cette bibliothèque cliente sera également incluse pour toutes les instances du composant par défaut.

Utilisation de [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md) :

* Noeud `/apps/custom/components/comments`
* Sélectionnez **[!UICONTROL Créer un noeud]**

   * **Nom** : `clientlibs`
   * **Type** : `cq:ClientLibraryFolder`
   * Ajoutez à l’onglet **[!UICONTROL Propriétés]** :

      * **** `categories` **** `String` **NameTypeValue** `cq.social.author.hbs.comments` `Multi`
      * **** `dependencies` **** `String` **NameTypeValue** `cq.social.scf` `Multi`

* Sélectionnez **[!UICONTROL Enregistrer tout]**.
* Avec le noeud `/apps/custom/components/comments/clientlib`s sélectionné, créez 3 fichiers :

   * **Nom** : `css.txt`
   * **Nom** : `js.txt`
   * **Nom** : customcommentsystem.js

* Saisissez &#39;customcommentsystem.js&#39; comme contenu de `js.txt`
* Sélectionnez **[!UICONTROL Enregistrer tout]**.

![comments-clientlibs](assets/comments-clientlibs.png)

## Enregistrement du modèle et de la vue SCF {#register-the-scf-model-view}

Lors de l’extension (remplacement) d’un composant SCF, le paramètre resourceType est différent (le recouvrement utilise le mécanisme de recherche relatif qui recherche `/apps` avant `/libs` afin que le paramètre resourceType reste identique). C’est pourquoi il est nécessaire d’écrire du code JavaScript (dans la bibliothèque cliente) pour enregistrer le modèle SCF JS et l’afficher pour la ressource personnalisée resourceType.

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

* Sélectionnez **[!UICONTROL Enregistrer tout]**.

## Publier l’application {#publish-the-app}

Pour tester le composant étendu dans l’environnement de publication, il est nécessaire de répliquer le composant personnalisé.

Pour ce faire, procédez comme suit :

* À partir de la navigation globale,

   * Sélectionnez **[!UICONTROL Outils]** **[!UICONTROL Déploiement]** > **[!UICONTROL Réplication]**
   * Sélectionnez **[!UICONTROL Activer l’arborescence]**
   * Définissez `Start Path` sur `/apps/custom`
   * Décochez **[!UICONTROL Uniquement Modifié]**
   * Bouton Sélectionner **[!UICONTROL Activer]**
