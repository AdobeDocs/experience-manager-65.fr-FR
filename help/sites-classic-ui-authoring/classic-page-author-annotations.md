---
title: Annotations lors de la modification d’une page
seo-title: Annotations lors de la modification d’une page
description: L’ajout de contenu aux pages de votre site web est souvent l’objet de discussions avant la publication réelle. Pour faciliter cette procédure, de nombreux composants directement liés au contenu permettent d’ajouter une annotation.
seo-description: L’ajout de contenu aux pages de votre site web est souvent l’objet de discussions avant la publication réelle. Pour faciliter cette procédure, de nombreux composants directement liés au contenu permettent d’ajouter une annotation.
page-status-flag: de-activated
uuid: d8d6ba76-f2aa-4044-98bf-5d506742d90d
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 9bee0197-f275-49cc-922d-62cba826c4e5
translation-type: tm+mt
source-git-commit: c8a02ad9fc33e963d2c760840e70c40ede988054
workflow-type: tm+mt
source-wordcount: '821'
ht-degree: 95%

---


# Annotations lors de la modification d’une page{#annotations-when-editing-a-page}

L’ajout de contenu aux pages de votre site web est souvent l’objet de discussions avant la publication réelle. Pour faciliter cette procédure, de nombreux composants directement liés au contenu (contrairement, par exemple, à la mise en page) permettent d’ajouter une annotation.

Une annotation place une note autocollante colorée sur la page. L’annotation vous permet (ainsi qu’aux autres utilisateurs) de laisser des commentaires ou des questions à l’intention d’autres auteurs ou réviseurs.

>[!NOTE]
>
>La définition d’un type de composant individuel détermine s’il est possible d’ajouter une annotation sur des instances de ce composant.

>[!NOTE]
>
>Les annotations créées dans l’IU classique sont également affichées dans l’IU optimisée pour les écrans tactiles. Toutefois, les esquisses sont spécifiques à l’IU et ne s’affichent donc que dans l’interface dans laquelle elles ont été créées.

>[!CAUTION]
>
>Si vous supprimez une ressource (par ex. un paragraphe), toutes les annotations et tous les schémas associés sont également supprimés, quelle que soit leur position sur la page dans son ensemble.

>[!NOTE]
>
>En fonction de vos besoins, vous pouvez également développer un processus d’envoi de notifications lorsque des annotations sont ajoutées, mises à jour ou supprimées.

## Annotations {#annotations}

Selon la conception du paragraphe, une annotation est soit disponible en tant qu’option dans le menu contextuel (habituellement le bouton droit de la souris lorsqu’il est positionné au-dessus du paragraphe requis), soit en tant que bouton dans la barre d’édition du paragraphe.

Dans tous les cas, sélectionnez **Annoter**. Une annotation sur une étiquette autocollante colorée est appliquée au paragraphe et vous passez immédiatement en mode d’édition, ce qui vous permet d’ajouter directement du texte :

![chlimage_1-137](assets/chlimage_1-137.png)

Vous pouvez déplacer l’annotation dans une nouvelle position sur la page. Cliquez sur le bord supérieur, puis maintenez le bouton de la souris enfoncé et faites glisser simultanément l’annotation sur la nouvelle position. La nouvelle position peut être partout sur la page, mais toutefois il convient généralement de maintenir la connexion avec le paragraphe d’une manière ou d’une autre.

Les annotations (y compris les schémas qui leur sont associés) sont également comprises dans toute action de copie, de découpe ou de suppression affectant le paragraphe auquel elles sont jointes ; pour les actions de copie et de découpe, la position de l’annotation (et des schémas qui lui sont associés) est conservée par rapport au paragraphe d’origine.

La taille de l&#39;annotation peut également être augmentée ou diminuée en faisant glisser le coin inférieur droit.

À des fins de suivi, la ligne de pied de page indique l’utilisateur qui a créé l’annotation et la date. Les auteurs consécutifs peuvent modifier la même annotation (le pied de page est alors mis à jour), ou créer une nouvelle annotation pour le même paragraphe.

Une confirmation est exigée lorsque vous choisissez de supprimer l’annotation (supprimer une annotation supprime également tout schéma qui lui est associé).

Les trois icônes dans la partie supérieure gauche vous permettent de minimiser l’annotation (ainsi que tout schéma qui lui est associé), de changer la couleur et d’ajouter des schémas.

>[!NOTE]
>
>Les annotations ne sont visibles que dans le mode d’édition de l’environnement de l’auteur.
>
>Elles ne sont pas visibles dans un environnement de publication, ni dans les modes Aperçu ou Conception dans un environnement de création.

>[!NOTE]
>
>Les annotations ne peuvent pas être ajoutées à une page verrouillée par un autre utilisateur.

## Schémas d’annotation {#annotation-sketches}

>[!NOTE]
>
>Les schémas ne sont pas disponibles dans Internet Explorer, donc :
>
>* l’icône ne s’affiche pas ;
>* les schémas existants, créés dans un autre navigateur, ne s’affichent pas.

>



Les schémas sont une fonctionnalité des annotations qui vous permet de créer des graphiques en courbes simples, n’importe où dans la fenêtre de navigateur (partie visible) :

![chlimage_1-138](assets/chlimage_1-138.png)

* Le curseur prend la forme d’une croix lorsque vous passez en mode de schéma. Vous pouvez tracer plusieurs lignes distinctes.
* La ligne de schéma reflète la couleur de l’annotation et peut être :

   * à main levée

      le mode par défaut ; terminez en relâchant le bouton de la souris.

   * droite :

      maintenez la touche `ALT` enfoncée et cliquez sur les points de début et de fin ; terminez par un double-clic.

* Une fois que vous avez quitté le mode de schéma, vous pouvez cliquer sur une courbe du schéma pour sélectionner celui-ci.
* Déplacez un schéma en sélectionnant celui-ci, puis en le faisant glisser sur la position de votre choix.
* Un schéma recouvre le contenu. Cela signifie qu’entre les 4 coins du schéma vous ne pouvez pas cliquer sur le paragraphe sous-jacent ; par exemple, pour modifier un lien ou y accéder. Si cela pose problème (par exemple, si un grand schéma couvre une large zone de la page), vous pouvez minimiser l’annotation appropriée, car vous minimisez alors également tous les schémas qui lui sont associés, vous procurant ainsi l’accès à la zone sous-jacente.
* Pour supprimer un schéma individuel : sélectionnez le schéma requis, puis appuyez sur la touche **Supprimer** (**fn**-**Retour Arrière** sur un MAC).

* Si vous déplacez ou copiez un paragraphe, toutes les annotations qui lui sont associées, ainsi que leurs schémas, sont également déplacés ou copiés ; leur position par rapport au paragraphe demeure inchangée.
* Si vous supprimez une annotation, tous les schémas qui lui sont associés sont également supprimés.

