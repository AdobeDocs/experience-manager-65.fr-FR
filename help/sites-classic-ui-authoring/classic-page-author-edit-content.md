---
title: Modifier le contenu de la page
description: Vous ajoutez du contenu en faisant glisser des composants sur la page. Ils peuvent ensuite être modifiés sur place, déplacés ou supprimés.
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
docset: aem65
exl-id: e1b5aea0-983c-4e7b-9d35-d7beeee45dc7
source-git-commit: 10b370fd8f855f71c6d7d791c272137bb5e04d97
workflow-type: tm+mt
source-wordcount: '1829'
ht-degree: 91%

---

# Modification du contenu de la page{#editing-page-content}

Une fois la page créée (une nouvelle page ou dans le cadre d’un lancement ou d’une Live Copy), vous pouvez modifier le contenu pour effectuer toute mise à jour dont vous avez besoin.

Le contenu est ajouté à l’aide des [composants](/help/sites-classic-ui-authoring/classic-page-author-default-components.md) (appropriés au type de contenu) qui peuvent être glissés sur la page. Ils peuvent ensuite être modifiés sur place, déplacés ou supprimés.

>[!NOTE]
>
>Votre compte a besoin des [droits d’accès appropriés](/help/sites-administering/security.md) et des [autorisations](/help/sites-administering/security.md#permissions) pour modifier des pages ; par exemple, ajouter, modifier ou supprimer des composants, annoter, déverrouiller.
>
>En cas de problème, contactez votre administrateur système.

## Sidekick {#sidekick}

Le sidekick est un outil clé lors de la création de pages. Il flotte lors de la création d’une page et il est donc toujours visible.

Plusieurs onglets et icônes sont disponibles, notamment :

* Composants
* Page
* Informations
* Contrôle de version
* Workflow
* Modes
* Génération de modèles automatique
* ClientContext
* Sites Web

![chlimage_1-71](assets/chlimage_1-71.png)

Donne accès à diverses fonctionnalités, par exemple :

* [la sélection de composants ;](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#sidekick)
* [l’affichage des références ;](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#showing-references)
* [l’accès au journal d’audit ;](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#audit-log)
* [le changement de mode ;](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#page-modes)
* la [création](/help/sites-classic-ui-authoring/classic-page-author-work-with-versions.md#creating-a-new-version), la [restauration](/help/sites-classic-ui-authoring/classic-page-author-work-with-versions.md#restoring-a-page-version-from-sidekick) et la [comparaison](/help/sites-classic-ui-authoring/classic-page-author-work-with-versions.md#comparing-with-a-previous-version) des versions ;

* la [publication](/help/sites-classic-ui-authoring/classic-page-author-publish-pages.md#publishing-a-page) et la [dépublication](/help/sites-classic-ui-authoring/classic-page-author-publish-pages.md#unpublishing-a-page) d’une page ;

* [la modification des propriétés de page ;](/help/sites-classic-ui-authoring/classic-page-author-edit-page-properties.md)

* [la génération de modèles automatique ;](/help/sites-authoring/scaffolding.md)

* [le contexte client.](/help/sites-administering/client-context.md)

## Insertion d’un composant {#inserting-a-component}

### Insertion d’un composant {#inserting-a-component-1}

Après avoir ouvert la page, vous pouvez commencer à ajouter du contenu. Pour ce faire, ajoutez des composants (également appelés paragraphes).

Pour insérer un nouveau composant :

1. Plusieurs méthodes permettent de sélectionner le type de paragraphe à insérer :

   * Double-cliquez sur la zone intitulée **Faire glisser des composants ou des ressources ici...**. La barre d’outils **Insérer un nouveau composant** s’ouvre. Sélectionnez un composant, puis cliquez sur **OK**.

   * Faites glisser un composant depuis la barre d’outils flottante (appelée sidekick) pour insérer un nouveau paragraphe.
   * Cliquez avec le bouton droit de la souris sur un paragraphe existant, puis sélectionnez **Nouveau...**. La barre d’outils Insérer un nouveau composant s’ouvre. Sélectionnez un composant, puis cliquez sur **OK**.

   ![screen_shot_2012-02-15at115605am](assets/screen_shot_2012-02-15at115605am.png)

1. La liste des composants (types de paragraphe) disponibles est affichée dans le sidekick et dans la barre d’outils **Insérer un nouveau composant**. Elles peuvent être divisées en différentes sections (par exemple, Général, Colonnes, etc.), qui peuvent être développées selon les besoins.

   Ces choix peuvent varier en fonction de votre environnement de production. Pour plus d’informations sur les composants, voir [Composants par défaut](/help/sites-classic-ui-authoring/classic-page-author-default-components.md).

1. Insérez le composant de votre choix sur la page. Double-cliquez ensuite sur le paragraphe. Une fenêtre s’ouvre alors pour vous permettre de configurer votre paragraphe et d’ajouter du contenu.

### Insérer un composant à l’aide de l’outil de recherche de contenu {#inserting-a-component-using-the-content-finder}

Vous pouvez également ajouter un nouveau composant à la page en faisant glisser une ressource depuis l’[outil de recherche de contenu](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#the-content-finder). Cela crée automatiquement un composant du type approprié contenant la ressource.

Cette procédure est valide pour les types de ressources suivants (certains dépendent du système de pages/paragraphes) :

| Type de ressource | Type de composant résultant |
|---|---|
| Image | Image |
| Document | Télécharger |
| Produit | Produit |
| Vidéo | Flash |

>[!NOTE]
>
>Ce comportement peut être configuré pour votre installation. Voir [Configuration d’un système de paragraphe afin que le glissement d’une ressource crée une instance de composant](/help/sites-developing/developing-components.md#configuring-a-paragraph-system-so-that-dragging-an-asset-creates-a-component-instance) pour plus de détails.

Pour créer un composant en faisant glisser l’un des types de ressources ci-dessus, suivez ces étapes :

1. Assurez-vous que votre page est en mode [**Modifier**](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#page-modes).
1. Ouvrez l’[outil de recherche de contenu](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#the-content-finder).
1. Faites glisser le composant jusqu’à la position requise. L’[espace réservé du composant](#componentplaceholder) vous indique où sera positionné le composant.

   Un composant, adapté au type de ressource, est créé à l’emplacement requis. Il contient la ressource sélectionnée.

1. [Modifier](#editmovecopypastedelete) le composant, si nécessaire.

## Modifier un composant (contenu et propriétés) {#editing-a-component-content-and-properties}

Pour modifier un paragraphe existant, procédez d’une des manières suivantes :

* **Double-cliquez** sur le paragraphe pour l’ouvrir. Vous voyez la même fenêtre que lorsque vous avez créé le paragraphe avec le contenu existant. Apportez vos modifications et cliquez sur **OK**.

* **Cliquez avec le bouton droit de la souris** sur le paragraphe et cliquez sur **Modifier**.

* **Cliquez** deux fois sur le paragraphe (double-clic lent) pour passer en mode de modification statique. Vous pourrez modifier directement le texte sur la page, plutôt que dans une boîte de dialogue. Dans ce mode, une barre d’outils s’affiche en haut de la page. Il vous suffit d’apporter vos modifications qui seront automatiquement enregistrées.

## Déplacement d’un composant {#moving-a-component}

Pour déplacer un paragraphe :

>[!NOTE]
>
>Vous pouvez également utiliser un [couper/coller](#cut-copy-paste-a-component) pour déplacer un composant.

1. Sélectionnez le paragraphe à déplacer :

   ![screen_shot_2012-02-15at115855am](assets/screen_shot_2012-02-15at115855am.png)

1. Faites glisser le paragraphe vers son nouvel emplacement. AEM indique où le paragraphe peut être déplacé avec une coche verte. Déposez-le à l’emplacement de votre choix.
1. Votre paragraphe est déplacé :

   ![screen_shot_2012-02-15at120030pm](assets/screen_shot_2012-02-15at120030pm.png)

## Supprimer un composant {#deleting-a-component}

Pour supprimer un paragraphe :

1. Sélectionnez le paragraphe et **cliquez avec le bouton droit de la souris** :

   ![screen_shot_2012-02-15at120220pm](assets/screen_shot_2012-02-15at120220pm.png)

1. Sélectionnez **Supprimer** dans le menu. La gestion de contenu web d’AEM vous invite à confirmer la suppression du paragraphe, car cette action est irréversible.
1. Cliquez sur **OK**.

>[!NOTE]
>
>Si vous avez défini vos [Propriétés de l’utilisateur pour afficher la barre d’outils d’édition globale](/help/sites-classic-ui-authoring/author-env-user-props.md), vous pouvez également réaliser certaines actions sur les paragraphes à l’aide des boutons **Copier**, **Couper**, **Coller** et **Supprimer** disponibles.
>
>Divers [raccourcis clavier](/help/sites-classic-ui-authoring/classic-page-author-keyboard-shortcuts.md) sont également disponibles.

## Couper/Copier/Coller un composant {#cut-copy-paste-a-component}

Comme pour la [Suppression d’un composant](#deleting-a-component), vous pouvez copier, couper et coller un composant à l’aide du menu contextuel.

>[!NOTE]
>
>Si vous avez défini vos [Propriétés de l’utilisateur pour afficher la barre d’outils d’édition globale](/help/sites-classic-ui-authoring/author-env-user-props.md), vous pouvez également réaliser certaines actions sur les paragraphes à l’aide des boutons **Copier**, **Couper**, **Coller** et **Supprimer** disponibles.
>
>Divers [raccourcis clavier](/help/sites-classic-ui-authoring/classic-page-author-keyboard-shortcuts.md) sont également disponibles.

>[!NOTE]
>
>Le découpage, la copie et le collage de contenu ne sont pris en charge que sur la même page.

## Composants hérités {#inherited-components}

Les composants hérités peuvent être le produit de divers scénarios :

* De la [Gestion multisite](/help/sites-administering/msm.md), également en combinaison avec la [génération de modèles automatiques](/help/sites-classic-ui-authoring/classic-feature-scaffolding.md#scaffolding-with-msm-inheritance).

* Des [lancements](/help/sites-classic-ui-authoring/classic-launches.md) (quand basés sur une live copy)
* Composants spécifiques, par exemple le système de paragraphes hérité dans Geometrixx.

Vous pouvez annuler (puis réactiver) l’héritage. Selon le composant, vous pouvez effectuer cette opération depuis :

1. **Live Copy**

   Si un composant fait partie d’une Live Copy ou d’un lancement, il est signalé par une icône de cadenas. Vous pouvez cliquer sur le cadenas pour annuler l’héritage.

   * L’icône de cadenas s’affiche lorsque le composant est sélectionné, par exemple :

   ![chlimage_1-72](assets/chlimage_1-72.png)

   * Le cadenas s’affiche également dans la boîte de dialogue des composants, par exemple :

   ![chlimage_1-73](assets/chlimage_1-73.png)

1. **Un système de paragraphes hérité**

   Boîte de dialogue de configuration. Par exemple, comme avec le système de paragraphes hérité dans Geometrixx :

   ![chlimage_1-74](assets/chlimage_1-74.png)

## Ajouter des annotations {#adding-annotations}

Les [annotations](/help/sites-classic-ui-authoring/classic-page-author-annotations.md) permettent à d’autres auteurs et autrices de réagir sur votre contenu. Elles sont principalement destinées à la révision et à la validation.

## Aperçu des pages {#previewing-pages}

Lors de l’aperçu des pages, les deux icônes situées dans la bordure inférieure du sidekick offrent de précieux renseignements :

![Bordure inférieure du sidekick avec une ligne horizontale de sept icônes. Deux icônes au début de la ligne, l’icône Modifier et l’icône du mode Aperçu, sont représentées respectivement par un symbole de crayon et un symbole de loupe.](do-not-localize/chlimage_1-5.png)

* L’icône en forme de crayon indique que vous êtes actuellement en mode d’édition. Vous pouvez alors ajouter, modifier, déplacer ou supprimer du contenu.

  ![Icône Modifier représentée par un symbole de crayon.](do-not-localize/chlimage_1-6.png)

* L’icône en forme de loupe permet de sélectionner le mode d’aperçu. La page s’affiche alors telle qu’elle sera rendue dans l’environnement de publication (une actualisation de page peut s’avérer nécessaire) :

  ![Icône du mode Aperçu indiquée par un symbole de loupe.](do-not-localize/chlimage_1-7.png)

  En mode d’aperçu, le sidekick est réduit. Cliquez sur l’icône de flèche bas pour revenir au mode d’édition :

  ![Barre avec AEM en titre et l’icône du mode de modification à droite du titre, indiquée par une flèche vers le bas.](do-not-localize/chlimage_1-8.png)

## Rechercher et remplacer {#find-replace}

Pour des modifications à plus grande échelle de la même expression, l’option de menu **[Rechercher et remplacer](/help/sites-classic-ui-authoring/author-env-search.md#find-and-replace)** vous permet de rechercher et de remplacer plusieurs instances d’une chaîne dans une section du site web.

## Verrouillage d’une page {#locking-a-page}

AEM permet de verrouiller une page, de sorte que personne d’autre ne puisse en modifier le contenu. Cela s’avère utile lorsque vous apportez de nombreuses modifications à une page spécifique ou lorsque vous devez figer une page pendant un court moment.

>[!CAUTION]
>
>Le verrouillage d’une page doit être utilisé avec précaution, car la seule personne pouvant déverrouiller la page est la personne qui l’a verrouillée (ou un compte disposant de droits d’administrateur).

Pour verrouiller une page, procédez comme suit :

1. Sous l’onglet **Sites web**, sélectionnez la page à verrouiller.
1. Double-cliquez sur la page pour l’ouvrir et la modifier.
1. Sous l’onglet **Page** du sidekick, sélectionnez **Verrouiller la page** :

   ![screen_shot_2012-02-08at15750pm](assets/screen_shot_2012-02-08at15750pm.png)

   Un message indique que votre page est verrouillée pour d’autres utilisateurs. En outre, dans le volet de droite de la variable **Sites web** console, AEM WCM affiche la page comme verrouillée et indique quel utilisateur l’a verrouillée.

   ![screen_shot_2012-02-08at20657pm](assets/screen_shot_2012-02-08at20657pm.png)

## Déverrouillage d’une page {#unlocking-a-page}

Pour déverrouiller une page, procédez comme suit :

1. Sous l’onglet **Sites web**, sélectionnez la page à déverrouiller.
1. Double-cliquez sur la page pour l’ouvrir.
1. Sous l’onglet **Page** du sidekick, sélectionnez **Déverrouiller la page**.

## Annulation et rétablissement des modifications de page {#undoing-and-redoing-page-edits}

Utilisez les raccourcis clavier suivants lorsque le cadre de contenu de la page est ciblé :

* Annuler : Ctrl+Z (Windows) ou Cmd+Z (Mac)
* Rétablir : Ctrl+Y (Windows) ou Cmd+Y (Mac)

Lorsque vous annulez ou rétablissez une opération de suppression, d’ajout ou de déplacement, le ou les paragraphes concernés sont signalés par une mise en surbrillance clignotante (comportement par défaut).

>[!NOTE]
>
>Consultez [Annulation et rétablissement des modifications de page : la théorie](#undoing-and-redoing-page-edits-the-theory) pour en savoir plus sur ce qu’il est possible de faire lorsque vous annulez ou rétablissez des modifications de page.

## Annulation et rétablissement des modifications de page : la théorie {#undoing-and-redoing-page-edits-the-theory}

>[!NOTE]
>
>L’administrateur système peut [configurer divers aspects des fonctions Annuler/Rétablir](/help/sites-administering/config-undo.md) en fonction des exigences de votre instance.

AEM conserve l’historique des actions que vous effectuez et la séquence selon laquelle vous les réalisez. Ainsi, vous annulez plusieurs actions dans l’ordre dans lequel vous les avez effectuées. Vous pouvez ensuite utiliser l’option Rétablir pour appliquer à nouveau une ou plusieurs des actions.

Si vous sélectionnez un élément de la page de contenu, les commandes Annuler et Rétablir s’appliquent à l’élément sélectionné, par exemple un composant de texte.

Le comportement des commandes Annuler et Rétablir est similaire à celui des autres logiciels. Utilisez ces commandes pour restaurer l’état récent de votre page web lorsque vous prenez des décisions sur le contenu. Par exemple, si vous repositionnez un paragraphe de texte sur la page, vous pouvez utiliser la commande Annuler pour le remettre à son emplacement initial. Si vous décidez ensuite de redéplacer le paragraphe, utilisez la commande Rétablir.

>[!NOTE]
>
>Vous pouvez :
>
>* Rétablir les actions tant que vous n’avez pas effectué de modification de page depuis que vous avez utilisé l’option Annuler.
>* Vous pouvez annuler un maximum de 20 actions de modification (paramètre par défaut).
>* Vous pouvez également utiliser les [raccourcis clavier](/help/sites-classic-ui-authoring/classic-page-author-keyboard-shortcuts.md) pour annuler et rétablir.
>

Vous pouvez utiliser les options Annuler et Rétablir pour les types de modifications de page suivants :

* Ajout, modification, suppression et déplacement de paragraphes
* Modification sur place du contenu des paragraphes
* Copie, découpe et collage d’éléments dans une page
* Copie, découpe et collage d’éléments entre plusieurs pages
* Ajout, suppression et modification de fichiers et d’images
* Ajout, suppression et modification d’annotations et d’esquisses
* Modifications apportées à Scaffold
* Ajout et suppression de références
* Modification des valeurs de propriété dans les boîtes de dialogue de composant

Les champs de formulaire dont le rendu des composants de formulaire est effectué ne sont pas censés contenir de valeurs spécifiées lors de la création de pages. Les commandes Annuler et Rétablir n’affectent donc pas les modifications que vous apportez aux valeurs des composants de ce type. Par exemple, vous ne pouvez pas annuler la sélection d’une valeur dans une liste déroulante.

>[!NOTE]
>
>Des autorisations spéciales sont nécessaires pour annuler et rétablir des modifications affectant des fichiers et des images. En outre, l’historique des annulations des modifications apportées aux fichiers et aux images dure quelques heures minimum. Au-delà de cette période, l’annulation des modifications n’est toutefois pas garantie. Votre administrateur peut fournir des autorisations et modifier la durée par défaut de dix heures.
