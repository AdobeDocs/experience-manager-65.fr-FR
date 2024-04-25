---
title: Création des composants
description: Découvrez comment étendre les composants à l’aide du système de commentaires composé des composants Commentaires et Commentaires .
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 2e02db9f-294d-4d4a-92da-3ab1d38416ab
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '591'
ht-degree: 3%

---

# Création des composants  {#create-the-components}

L’exemple d’extension de composants utilise le système de commentaires, composé de deux composants.

* Commentaires : système de commentaires englobant qui est le composant placé sur une page.
* Commentaire : composant qui capture une instance d’un commentaire publié.

Les deux composants doivent être mis en place, en particulier si vous personnalisez l’apparence d’un commentaire publié.

>[!NOTE]
>
>Un seul système de commentaires par page de site est autorisé.
>
>De nombreuses fonctionnalités de Communities incluent déjà un système de commentaires dont resourceType peut être modifié pour référencer le système de commentaires étendu.

## Création du composant Commentaires {#create-the-comments-component}

Ces instructions spécifient une **Groupe** valeur autre que `.hidden` le composant peut donc être rendu disponible à partir de l’explorateur de composants (sidekick).

La suppression du fichier JSP créé automatiquement est due à l’utilisation du fichier HBS par défaut.

1. Accédez à **CRXDE|Lite** ([http://localhost:4502/crx/de/index.jsp](http://localhost:4502/crx/de/index.jsp))

1. Créez un emplacement pour les applications personnalisées :

   * Sélectionnez la variable `/apps` node

      * **Créer un dossier** named **[!UICONTROL custom]**

   * Sélectionnez la variable `/apps/custom` node

      * **Créer un dossier** named **[!UICONTROL components]**

1. Sélectionnez la variable `/apps/custom/components` node

   * **[!UICONTROL Créer > Composant..]**

      * **Libellé**: *commentaires*
      * **Titre**: *Commentaires Alt*
      * **Description**: *Style de commentaire alternatif*
      * **Super Type**: *social/commons/components/hbs/comments*
      * **Groupe**: *Personnalisé*

   * Sélectionner **[!UICONTROL Suivant]**
   * Sélectionner **[!UICONTROL Suivant]**
   * Sélectionner **[!UICONTROL Suivant]**
   * Sélectionnez **[!UICONTROL OK]**.

1. Développez le noeud qui a été créé : `/apps/custom/components/comments`
1. Sélectionner **[!UICONTROL Enregistrer tout]**
1. Clic droit `comments.jsp`
1. Sélectionner **[!UICONTROL Supprimer]**
1. Sélectionner **[!UICONTROL Enregistrer tout]**

![create-component](assets/create-component.png)

### Création du composant Commentaire enfant {#create-the-child-comment-component}

Ces instructions sont définies **Groupe** to `.hidden` car seul le composant parent doit être inclus dans une page.

La suppression du fichier JSP créé automatiquement est due à l’utilisation du fichier HBS par défaut.

1. Accédez au `/apps/custom/components/comments` node
1. Cliquez avec le bouton droit sur le noeud.

   * Sélectionner **[!UICONTROL Créer]** > **[!UICONTROL Composant..]**

      * **Libellé**: *comment*
      * **Titre**: *Commentaire Alt*
      * **Description**: *Autre style de commentaire*
      * **Super Type**: *social/commons/components/hbs/comments/comment*
      * **Groupe** : `*.hidden*`

   * Sélectionner **[!UICONTROL Suivant]**
   * Sélectionner **[!UICONTROL Suivant]**
   * Sélectionner **[!UICONTROL Suivant]**
   * Sélectionnez **[!UICONTROL OK]**.

1. Développez le noeud qui a été créé : `/apps/custom/components/comments/comment`
1. Sélectionner **[!UICONTROL Enregistrer tout]**
1. Clic droit `comment.jsp`
1. Sélectionner **[!UICONTROL Supprimer]**
1. Sélectionner **[!UICONTROL Enregistrer tout]**

![create-child-component](assets/create-child-component.png)

![create-component-crxde](assets/create-component-crxde.png)

### Copie et modification des scripts HBS par défaut {#copy-and-modify-the-default-hbs-scripts}

Utilisation [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md):

* Copier `comments.hbs`

   * De [/libs/social/commons/components/hbs/comments](http://localhost:4502/crx/de/index.jsp#/libs/social/commons/components/hbs/comments)
   * À [/apps/custom/components/comments](http://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments)

* Modifier `comments.hbs` à :

   * Modifiez la valeur de la variable `data-scf-component` attribute (~line 20) :

      * De `social/commons/components/hbs/comments`
      * À `/apps/custom/components/comments`

   * Modifiez pour inclure le composant de commentaire personnalisé (~line 75) :

      * Remplacer `{{include this resourceType='social/commons/components/hbs/comments/comment'}}`
      * Avec `{{include this resourceType='/apps/custom/components/comments/comment'}}`

* Copier `comment.hbs`

   * De [/libs/social/commons/components/hbs/comments/comment](http://localhost:4502/crx/de/index.jsp#/libs/social/commons/components/hbs/comments/comment)
   * À [/apps/custom/components/comments/comment](http://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments/comment)

* Modifier `comment.hbs` à :

   * Modifier la valeur de l’attribut data-scf-component (~ ligne 19)

      * De `social/commons/components/hbs/comments/comment`
      * À `/apps/custom/components/comments/comment`

* Sélectionner `/apps/custom` node
* Sélectionner **[!UICONTROL Enregistrer tout]**

## Création d’un dossier de bibliothèques clientes {#create-a-client-library-folder}

Pour éviter d’avoir à inclure cette bibliothèque cliente, la valeur de catégories de la bibliothèque cliente du système de commentaires par défaut peut être utilisée ( `cq.social.author.hbs.comments`). Cependant, cette bibliothèque cliente doit également être incluse pour toutes les instances du composant par défaut.

Utilisation [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md):

* Sélectionner `/apps/custom/components/comments` node
* Sélectionner **[!UICONTROL Créer un noeud]**

   * **Nom** : `clientlibs`
   * **Type** : `cq:ClientLibraryFolder`
   * Ajouter à **[!UICONTROL Propriétés]** tab :

      * **Nom** `categories` **Type** `String` **Valeur** `cq.social.author.hbs.comments` `Multi`
      * **Nom** `dependencies` **Type** `String` **Valeur** `cq.social.scf` `Multi`

* Sélectionner **[!UICONTROL Enregistrer tout]**
* Avec `/apps/custom/components/comments/clientlib`Si le noeud est sélectionné, créez trois fichiers :

   * **Nom** : `css.txt`
   * **Nom** : `js.txt`
   * **Nom**: customcommentsystem.js

* Saisissez &quot;customcommentsystem.js&quot; comme contenu de `js.txt`
* Sélectionner **[!UICONTROL Enregistrer tout]**

![comments-clientlibs](assets/comments-clientlibs.png)

## Enregistrement du modèle et de la vue SCF {#register-the-scf-model-view}

Lors de l’extension (remplacement) d’un composant SCF, resourceType est différent (le recouvrement utilise le mécanisme de recherche relatif qui effectue la recherche dans `/apps` before `/libs` afin que resourceType reste identique). C’est pourquoi il est nécessaire d’écrire du code JavaScript (dans la bibliothèque cliente) pour enregistrer le modèle SCF JS et l’afficher pour la ressource personnalisée resourceType.

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

* Sélectionner **[!UICONTROL Enregistrer tout]**

## Publication de l’application {#publish-the-app}

Pour tester le composant étendu dans l’environnement de publication, il est nécessaire de répliquer le composant personnalisé.

Pour ce faire, procédez comme suit :

* À partir de la navigation globale,

   * Sélectionner **[!UICONTROL Outils]** > **[!UICONTROL Déploiement]** > **[!UICONTROL Réplication]**
   * Sélectionner **[!UICONTROL Activer l’arborescence]**
   * Définissez `Start Path` sur `/apps/custom`.
   * Décocher **[!UICONTROL Modifié uniquement]**
   * Sélectionner **[!UICONTROL Activer]** button
