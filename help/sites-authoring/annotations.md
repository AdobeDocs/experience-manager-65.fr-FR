---
title: Annotations lors de la modification d’une page
seo-title: Annotations lors de la modification d’une page
description: De nombreux composants directement liés au contenu permettent d’ajouter une annotation.
seo-description: De nombreux composants directement liés au contenu permettent d’ajouter une annotation.
uuid: 157be55c-8ab8-472e-be32-0dcc02bfa41d
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: aa89326a-ad33-4b0b-8d09-c68c5a5c790a
translation-type: tm+mt
source-git-commit: cec6c4f9a1a75eb049dd4b8461c36c8d58d46f79
workflow-type: tm+mt
source-wordcount: '651'
ht-degree: 97%

---


# Annotations lors de la modification d’une page{#annotations-when-editing-a-page}

L’ajout de contenu aux pages de votre site web est souvent l’objet de discussions avant la publication réelle. Pour faciliter cette procédure, de nombreux composants directement liés au contenu (contrairement, par exemple, à la mise en page) permettent d’ajouter une annotation.

Une annotation place une note autocollante colorée sur la page. L’annotation vous permet (ainsi qu’aux autres utilisateurs) de laisser des commentaires ou des questions à l’intention d’autres auteurs ou réviseurs.

>[!NOTE]
>
>La définition d’un type de composant individuel détermine s’il est possible d’ajouter une annotation sur des instances de ce composant.

>[!NOTE]
>
>Les annotations créées dans l’IU classique sont affichées dans l’IU optimisée pour les écrans tactiles. Toutefois, les esquisses sont spécifiques à l’IU et ne s’affichent donc que dans l’interface dans laquelle elles ont été créées.

>[!CAUTION]
>
>Si vous supprimez une ressource (un paragraphe, par exemple), toutes les annotations et tous les schémas associés sont également supprimés, quelle que soit leur position sur la page dans son ensemble.

>[!NOTE]
>
>Selon vos besoins, vous pouvez également développer un workflow pour envoyer des notifications lorsque celles-ci sont ajoutées, mises à jour ou supprimées.

## Annotations {#annotations}

Un [mode](/help/sites-authoring/author-environment-tools.md#page-modes) spécial est utilisé pour la création et l’affichage des annotations.

>[!NOTE]
>
>Pour rappel, des [commentaires](/help/sites-authoring/basic-handling.md#timeline) sont également disponibles pour fournir un retour d’informations sur une page.

>[!NOTE]
>
>Vous pouvez annoter un large éventail de ressources :
>
>* [Annotation de ressources](/help/assets/manage-assets.md#annotating)
>* [Annotation de ressources vidéo](/help/assets/managing-video-assets.md#annotate-video-assets)

>



### Annotation d’un composant {#annotating-a-component}

Le mode Annoter permet de créer, de modifier, de déplacer ou de supprimer des annotations sur votre contenu :

1. Pour activer le mode Annotation, cliquez sur l’icône dans la barre d’outils (en haut à droite) lorsque vous modifiez une page :

   ![](do-not-localize/screen_shot_2018-03-22at110414.png)

   Vous pouvez maintenant afficher les annotations existantes.

   >[!NOTE]
   >
   >Pour quitter le mode Annotation, appuyez ou cliquez sur l’icône Annoter (symbole x) à droite de la barre d’outils supérieure.

1. Cliquez/appuyez sur l’icône Ajouter une annotation (symbole plus à gauche de la barre d’outils) pour commencer à ajouter des annotations.

   >[!NOTE]
   >
   >Pour mettre un terme à l’ajout d’annotations (et revenir à l’affichage), appuyez/cliquez sur l’icône Annuler (symbole x dans un cercle blanc) à gauche de la barre d’outils supérieure.

1. Cliquez/appuyez sur le composant requis (les composants qui peuvent être annotés sont encadrés en bleu) pour ajouter l’annotation et ouvrir la boîte de dialogue :

   ![screen_shot_2018-03-22at110606](assets/screen_shot_2018-03-22at110606.png)

   Utilisez alors le champ et/ou l’icône appropriée pour effectuer ce qui suit :

   * Entrez le texte de l’annotation.
   * Créez une esquisse (traits et formes) pour mettre en surbrillance une zone du composant.

      Le curseur prend la forme d&#39;un fil croisé lorsque vous créez une esquisse. Vous pouvez tracer plusieurs lignes distinctes. La ligne d’esquisse reflète la couleur de l’annotation et peut être une flèche, un cercle ou un ovale.
   ![](do-not-localize/screen_shot_2018-03-22at110640.png)

   * Choisissez/changez la couleur :

   ![](do-not-localize/chlimage_1-19.png)

   * Supprimez l’annotation.

   ![](do-not-localize/screen_shot_2018-03-22at110647.png)

1. Pour fermer la boîte de dialogue de l’annotation, cliquez ou appuyez en dehors de la boîte de dialogue. Une vue tronquée (le premier mot) de l’annotation s’affiche avec les schémas :

   ![screen_shot_2018-03-22at110850](assets/screen_shot_2018-03-22at110850.png)

1. Après avoir modifié une annotation, vous pouvez effectuer ce qui suit :

   * Cliquer/appuyer sur la marque de texte pour ouvrir l’annotation. Vous pouvez alors voir le texte intégral de l’annotation, modifier cette dernière ou encore la supprimer.

      * Il n’est pas possible de supprimer les esquisses indépendamment de l’annotation.
   * Repositionner la marque de texte.
   * Cliquez/appuyez sur un trait du schéma pour le sélectionner et le faire glisser jusqu’à la position voulue.
   * Déplacer ou copier un composant.

      * Toutes les annotations qui lui sont associées, ainsi que leurs esquisses, sont également déplacées ou copiées ; leur position par rapport au paragraphe demeure inchangée.


1. Pour quitter le mode Annotation et revenir au mode précédemment affiché, appuyez ou cliquez sur l’icône Annoter (symbole x) à droite de la barre d’outils supérieure.

>[!NOTE]
>
>Les annotations ne peuvent pas être ajoutées à une page verrouillée par un autre utilisateur.

### Indicateur d’annotations {#annotation-indicator}

Les annotations n’apparaissent pas en mode d’édition, mais le badge en haut à droite de la barre d’outils indique le nombre d’annotations figurant sur la page active. Le badge remplace l’icône Annotations par défaut ; il fonctionne comme un lien rapide pour activer/désactiver le mode Annotation :

![chlimage_1-242](assets/chlimage_1-242.png)

