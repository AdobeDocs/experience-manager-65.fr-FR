---
title: Annotations lors de l’édition d’une page
description: L’ajout de contenu aux pages de votre site web est souvent l’objet de discussions avant la publication réelle. En effet, vous pouvez utiliser plusieurs composants directement liés au contenu pour ajouter une annotation.
page-status-flag: de-activated
uuid: d8d6ba76-f2aa-4044-98bf-5d506742d90d
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 9bee0197-f275-49cc-922d-62cba826c4e5
exl-id: d60e9601-d15b-4378-a33e-e90961f63195
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: ht
source-wordcount: '782'
ht-degree: 100%

---

# Annotations lors de la modification d’une page{#annotations-when-editing-a-page}

L’ajout de contenu aux pages de votre site web est souvent l’objet de discussions avant la publication réelle. Pour faciliter cette tâche, de nombreux composants directement liés au contenu (par opposition à la disposition par exemple) vous permettent d’ajouter une annotation.

Une annotation place une note autocollante colorée sur la page. L’annotation vous permet (ainsi qu’aux autres utilisateurs) de laisser des commentaires ou des questions à l’intention d’autres auteurs ou réviseurs.

>[!NOTE]
>
>La définition d’un type de composant individuel détermine s’il est possible d’ajouter une annotation sur des instances de ce composant.

>[!NOTE]
>
>Les annotations créées dans l’IU classique s’affichent également dans l’UI optimisée pour les écrans tactiles. Toutefois, les esquisses sont spécifiques à l’interface utilisateur et ne s’affichent que dans l’interface dans laquelle elles ont été créées.

>[!CAUTION]
>
>Si vous supprimez une ressource (par ex. un paragraphe), toutes les annotations et tous les schémas associés sont également supprimés, quelle que soit leur position sur la page dans son ensemble.

>[!NOTE]
>
>Selon vos besoins, vous pouvez également développer un workflow pour envoyer des notifications lorsque celles-ci sont ajoutées, mises à jour ou supprimées.

## Annotations {#annotations}

Selon la conception du paragraphe, l’annotation est disponible soit sous la forme d’une option dans le menu contextuel (généralement le bouton droit de la souris lorsqu’il est placé sur le paragraphe requis) soit d’un bouton dans la barre d’édition du paragraphe.

Dans un cas comme dans l’autre, sélectionnez **Annoter**. Une annotation autocollante colorée est appliquée au paragraphe. Vous passez immédiatement en mode d’édition, ce qui vous permet d’ajouter directement du texte :

![chlimage_1-137](assets/chlimage_1-137.png)

Vous pouvez déplacer l’annotation vers un nouvel emplacement sur la page. Cliquez sur la zone de la bordure supérieure, puis maintenez la touche enfoncée et faites glisser simultanément l’annotation au nouvel emplacement. Cette opération peut se faire à n’importe endroit de la page, bien qu’il soit généralement utile de la garder connectée au paragraphe d’une manière ou d’une autre.

Les annotations (y compris les esquisses associées) sont également incluses dans toute action copier, couper ou supprimer effectuée sur le paragraphe auquel elles sont jointes ; pour les actions copier ou couper, la position de l’annotation (et des esquisses associées) reste la même que celle du paragraphe d’origine.

La taille de l’annotation peut également être augmentée ou réduite, en faisant glisser le coin droit inférieur.

À des fins de suivi, la ligne de pied de page indique l’utilisateur ou l’utilisatrice qui a créé l’annotation ainsi que la date. Les auteurs et autrices suivants peuvent modifier la même annotation (le pied de page sera mis à jour) ou créer une annotation pour le même paragraphe.

Une confirmation est demandée lorsque vous choisissez de supprimer l’annotation (la suppression d’une annotation supprime également les esquisses qui y sont associées).

Les trois icônes dans la partie supérieure gauche vous permettent de minimiser l’annotation (ainsi que tout schéma qui lui est associé), de changer la couleur et d’ajouter des schémas.

>[!NOTE]
>
>Les annotations ne sont visibles que dans le mode d’édition de l’environnement de l’auteur.
>
>Elles ne sont pas visibles dans un environnement de publication, ni dans les modes Aperçu ou Conception dans un environnement de création.

>[!NOTE]
>
>Les annotations ne peuvent pas être ajoutées à une page verrouillée par un autre utilisateur.

## Esquisses d’annotation {#annotation-sketches}

>[!NOTE]
>
>Les esquisses ne sont pas disponibles dans Internet Explorer, donc :
>
>* l’icône ne s’affiche pas ;
>* les esquisses existantes, créées dans un autre navigateur, ne s’affichent pas.
>


Les esquisses constituent une fonction des annotations qui vous permet de créer des graphiques en courbes simples n’importe où dans la fenêtre du navigateur (partie visible) :

![chlimage_1-138](assets/chlimage_1-138.png)

* Le curseur prend la forme d’une croix lorsque vous êtes en mode esquisse. Vous pouvez tracer plusieurs lignes distinctes.
* La ligne d’esquisse reflète la couleur de l’annotation et peut être :

   * à main levée :

      le mode par défaut ; terminez en relâchant le bouton de la souris ;

   * droite :

      maintenez la touche `ALT` enfoncée et cliquez sur les points de début et de fin ; terminez par un double-clic.

* Après avoir quitté le mode d’esquisse, vous pouvez cliquer sur une ligne d’esquisse pour sélectionner cette dernière.
* Déplacez une esquisse en la sélectionnant, puis en la faisant glisser à l’emplacement souhaité.
* Une esquisse recouvre le contenu. En effet, entre les 4 coins de l’esquisse, vous ne pouvez pas cliquer sur le paragraphe sous-jacent ; par exemple, si vous devez modifier un lien ou y accéder. Si cela pose problème (par exemple, si vous disposez d’une esquisse couvrant une grande partie de la page), réduisez l’annotation appropriée, car cela réduit également toutes les esquisses associées, vous donnant ainsi accès à la zone sous-jacente.
* Pour supprimer une esquisse spécifique, sélectionnez-la, puis appuyez sur la touche **Supprimer** (**fn**-**touche Retour arrière** sur Mac).

* Si vous déplacez ou copiez un paragraphe, toutes les annotations associées et leurs esquisses sont également déplacées ou copiées ; leur position par rapport au paragraphe reste la même.
* Lorsque vous supprimez une annotation, toutes les esquisses qui y sont associées seront également supprimées.
