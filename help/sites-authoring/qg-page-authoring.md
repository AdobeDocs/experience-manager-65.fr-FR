---
title: Guide rapide pour la création de pages
description: Guide rapide de haut niveau sur les principales actions de création de contenu de page
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
docset: aem65
exl-id: a7e16555-9bbe-4da2-817c-4495a0193f3f
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User,Admin,Architect,Developer
source-git-commit: 9a3008553b8091b66c72e0b6c317573b235eee24
workflow-type: tm+mt
source-wordcount: '1540'
ht-degree: 100%

---

# Guide rapide pour la création de pages{#quick-guide-to-authoring-pages}

Ces procédures sont conçues comme un guide rapide (de haut niveau) des principales actions de la création de contenu de page dans AEM.

Elles :

* ne doivent pas être considérées comme étant exhaustives ;
* fournissent des liens vers la documentation détaillée.

Pour obtenir des détails complets sur la création dans AEM, consultez :

* [Premières étapes pour les auteurs](/help/sites-authoring/first-steps.md)
* [Création de pages](/help/sites-authoring/page-authoring.md)

## Quelques conseils rapides {#a-few-quick-hints}

Avant de vous donner un aperçu des détails, voici quelques conseils et astuces généraux qui méritent d’être gardés à l’esprit.

### La console Sites {#sites-console}

* **Créer**

   * Ce bouton est disponible sur de nombreuses consoles ; les options présentées sont contextuelles et peuvent varier en fonction du scénario.

* Réorganisation des pages dans un dossier

   * Vous pouvez le faire dans [Affichage en liste](/help/sites-authoring/basic-handling.md#list-view). Les modifications sont appliquées et visibles dans d’autres affichages.

#### Création de pages {#page-authoring}

* Liens de navigation

   * ***Les liens ne sont pas disponibles pour la navigation*** lorsque vous êtes en mode d’**édition**. Pour naviguer avec des liens, vous devez [prévisualiser la page](/help/sites-authoring/editing-content.md#previewing-pages) en utilisant soit :

      * [Mode Aperçu](/help/sites-authoring/editing-content.md#preview-mode)
      * [Afficher comme publié(e)](/help/sites-authoring/editing-content.md#view-as-published)

* Les versions ne sont pas lancées/créées à partir de l’éditeur de pages. Cette opération s’effectue dans la console Sites (via l’option **Créer** ou [Journal](/help/sites-authoring/basic-handling.md#timeline) pour une ressource sélectionnée).

>[!NOTE]
>
>Il existe plusieurs raccourcis clavier qui peuvent faciliter l’expérience de création.
>
>* [Raccourcis clavier lors de la modification de pages](/help/sites-authoring/page-authoring-keyboard-shortcuts.md)
>* [Raccourcis clavier pour les consoles](/help/sites-authoring/keyboard-shortcuts.md)
>

### Recherche de votre page {#finding-your-page}

Il existe plusieurs moyens de rechercher une page. Vous pouvez soit naviguer, soit effectuer une recherche en procédant comme suit :

1. Ouvrez la console **Sites** à l’aide de l’option **Sites** dans [Navigation globale](/help/sites-authoring/basic-handling.md#global-navigation). Une liste déroulante s’affiche lorsque vous sélectionnez le lien Adobe Experience Manager (en haut à gauche).

1. Naviguez dans l’arborescence en appuyant/cliquant sur la page appropriée. La représentation des ressources de page dépend de la vue que vous utilisez - [Carte, Liste ou Colonne](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources) :

   ![screen_shot_2018-03-21at160214](assets/screen_shot_2018-03-21at160214.png)

1. Remontez dans l’arborescence à l’aide du [chemin de navigation de l’en-tête](/help/sites-authoring/basic-handling.md#theheaderwithbreadcrumbs) pour revenir à l’emplacement sélectionné :

   ![qgtap-01](assets/qgtap-01.png)

1. Vous pouvez également [Rechercher](/help/sites-authoring/search.md) une page. Vous pouvez sélectionner votre page dans les résultats affichés.

   ![qgtap-03](assets/qgtap-03.png)

### Création d’une page {#creating-a-new-page}

Pour [créer une page](/help/sites-authoring/managing-pages.md#creating-a-new-page) :

1. [Accédez à l’emplacement](#finding-your-page) où créer la page.
1. Utilisez l’icône **Créer** puis sélectionnez **Page** dans la liste :

   ![qgtap-02](assets/qgtap-02.png)

1. Un assistant s’ouvre, qui vous aidera à collecter les informations nécessaires pour la [création de votre nouvelle page](/help/sites-authoring/managing-pages.md#creating-a-new-page). Suivez les instructions à l’écran.

### Sélection de la page pour d’autres actions {#selecting-your-page-for-further-action}

Vous pouvez sélectionner une page afin d’agir sur celle-ci. La sélection d’une page met automatiquement à jour la barre d’outils afin que les actions relatives à cette ressource s’affichent.

La sélection d’une page dépend de la vue utilisée dans la console :

1. Mode Colonnes :

   * Cliquez sur la miniature de la ressource requise ; une coche apparaît sur la miniature afin d’indiquer que la page a été sélectionnée.

1. Vue Liste :

   * Cliquez sur la miniature de la ressource requise ; une coche apparaît sur la miniature afin d’indiquer que la page a été sélectionnée.

1. Vue Carte :

   * Passez en mode de sélection en [sélectionnant la ressource requise](/help/sites-authoring/basic-handling.md#viewingandselectingyourresources) avec :

      * Appareil mobile : maintenez appuyé
      * Ordinateur de bureau : en cliquant sur l’icône d’[action rapide](/help/sites-authoring/basic-handling.md#quick-actions) en forme de coche (illustrée ci-dessous).

   ![screen_shot_2018-03-21at160503](assets/screen_shot_2018-03-21at160503.png)

   * Une coche apparaît sur la carte afin d’indiquer que la page a été sélectionnée.

   >[!NOTE]
   >
   >En mode de sélection, l’icône **Sélectionner** (coche) est transformée en icône **Désélectionner** (croix).

### Actions rapides (mode Carte/Bureau seulement) {#quick-actions-card-view-desktop-only}

Les [actions rapides](/help/sites-authoring/basic-handling.md#quick-actions) sont disponibles :

1. [Accédez à la page](#finding-your-page) sur laquelle vous souhaitez effectuer une action.
1. Placez le pointeur de la souris sur la carte qui représente la ressource requise. Les actions rapides s’affichent :

   ![screen_shot_2018-03-21at160503-1](assets/screen_shot_2018-03-21at160503-1.png)

### Modification du contenu de votre page {#editing-your-page-content}

1. [Accédez à la page](#finding-your-page) que vous souhaitez modifier.
1. [Ouvrez la page pour modification](/help/sites-authoring/managing-pages.md#opening-a-page-for-editing) à l’aide de l’icône Modifier (crayon) :

   ![screen_shot_2018-03-21at160607](assets/screen_shot_2018-03-21at160607.png)

   Vous pouvez y accéder comme suit :

   * [Actions rapides (mode Carte/Bureau uniquement)](#quick-actions-card-view-desktop-only) pour la ressource appropriée.
   * La barre d’outils [une fois la page sélectionnée](#selectiingyourpageforfurtheraction).

1. Lorsque l’éditeur s’ouvre, vous pouvez :

   * [Ajouter un nouveau composant à votre page](/help/sites-authoring/editing-content.md#inserting-a-component) en procédant comme suit :

      * Ouvrez le panneau latéral.
      * Sélectionnez l’onglet des composants (l’[explorateur de composants](/help/sites-authoring/author-environment-tools.md#components-browser)).
      * Faites glisser le composant requis sur la page.

     Vous pouvez ouvrir (et fermer) le panneau latéral en cliquant sur l’icône suivante :

     ![Ouvir le panneau latéral](do-not-localize/screen_shot_2018-03-21at160738.png)

   * [Modifiez le contenu d’un composant existant](/help/sites-authoring/editing-content.md#edit-configure-copy-cut-delete-paste) sur la page :

      * Ouvrez la barre d’outils du composant en appuyant ou en cliquant dessus. Utilisez l’icône **Modifier** (crayon) pour ouvrir la boîte de dialogue.
      * Ouvrez l’éditeur statique du composant en maintenant appuyé ou en double-cliquant lentement. Les actions disponibles s’affichent (pour certains composants, la sélection est limitée).
      * Pour afficher toutes les actions disponibles, passez en mode plein écran en cliquant sur l’icône suivante :

     ![Mode Plein écran](do-not-localize/screen_shot_2018-03-21at160706.png)

   * [Configurez les propriétés d’un composant existant :](/help/sites-authoring/editing-content.md#component-edit-dialog)

      * Ouvrez la barre d’outils du composant en appuyant ou en cliquant dessus. Utilisez l’icône **Configurer** (clé à molette) pour ouvrir la boîte de dialogue.

   * [Déplacer un composant](/help/sites-authoring/editing-content.md#moving-a-component) d’une des manières suivantes :

      * Faites glisser le composant vers son nouvel emplacement.
      * Ouvrez la barre d’outils du composant en appuyant ou en cliquant dessus. Utilisez les icônes **Couper**, puis **Coller** au besoin.

   * [Copiez (et collez)](/help/sites-authoring/editing-content.md#edit-configure-copy-cut-delete-paste) un composant :

      * Ouvrez la barre d’outils du composant en appuyant ou en cliquant dessus. Utilisez les icônes **Copier**, puis **Coller** au besoin.

   >[!NOTE]
   >
   >Vous pouvez **coller** les composants sur la même page ou sur une autre. Si vous collez un composant sur une autre page qui était déjà ouverte avant l’opération de couper/copier, il vous faut actualiser la page en question.

   * [Supprimer](/help/sites-authoring/editing-content.md#edit-configure-copy-cut-delete-paste) un composant :

      * Ouvrez la barre d’outils du composant (en appuyant ou en cliquant dessus), puis cliquez sur l’icône **Supprimer**.

   * [Ajouter des annotations](/help/sites-authoring/annotations.md#annotations) à la page :

      * Sélectionnez le mode **Annoter** (icône de bulle). Ajoutez des annotations à l’aide de l’icône **Ajouter une annotation** (plus). Quittez le mode Annotation en cliquant sur X en haut à droite.

     ![Annoter](do-not-localize/screen_shot_2018-03-21at160813.png)

   * [Prévisualiser une page](/help/sites-authoring/editing-content.md#preview-mode) (pour vérifier comment elle apparaîtra dans l’environnement de publication) :

      * Sélectionnez **Aperçu** dans la barre d’outils.

   * Revenez au mode d’édition (ou sélectionnez un autre mode) à l’aide du sélecteur déroulant **Modifier**.

   >[!NOTE]
   >
   >Pour naviguer en suivant les liens figurant dans le contenu, vous devez utiliser le [mode Aperçu](/help/sites-authoring/editing-content.md#preview-mode).

### Modification des propriétés de page {#editing-the-page-properties}

Il existe deux (principales) méthodes de [modification des propriétés de page](/help/sites-authoring/editing-page-properties.md) :

* Dans la console **Sites** :

   1. [Accédez à la page](#finding-your-page) que vous souhaitez publier.
   1. Sélectionnez l’icône **Propriétés** depuis :

      * [Actions rapides (mode Carte/Bureau uniquement)](#quick-actions-card-view-desktop-only) pour la ressource appropriée.
      * La barre d’outils [une fois la page sélectionnée](#selectiingyourpageforfurtheraction).

  ![screen_shot_2018-03-21at160850](assets/screen_shot_2018-03-21at160850.png)

   1. Les propriétés de la page s’affichent. Vous pouvez effectuer des mises à jour selon les besoins, puis les enregistrer à l’aide de la fonction Enregistrer.

* Lors de la [modification de votre page](#editing-your-page-content) :

   1. Ouvrez le menu **Informations sur la page**.
   1. Sélectionnez **Ouvrir les propriétés** pour ouvrir la boîte de dialogue de modification des propriétés.

  ![screen_shot_2018-03-21at160920](assets/screen_shot_2018-03-21at160920.png)

### Publication de la page (ou dépublication) {#publishing-your-page-or-unpublishing}

Il existe deux méthodes principales pour [publier votre page](/help/sites-authoring/publishing-pages.md) (et la dépublier) :

* Dans la console **Sites** :

   1. [Accédez à la page](#finding-your-page) que vous souhaitez publier.
   1. Cliquez sur l’icône **Publication rapide** dans :

      * [Actions rapides (mode Carte/Bureau uniquement)](#quick-actions-card-view-desktop-only) pour la ressource appropriée.
      * La barre d’outils, [une fois votre page sélectionnée](#selectiingyourpageforfurtheraction) (permet également d’accéder à l’option [Publier ultérieurement](/help/sites-authoring/publishing-pages.md#main-pars-title-12)).

  ![screen_shot_2018-03-21at160957](assets/screen_shot_2018-03-21at160957.png)

* Lors de la [modification de votre page](#editing-your-page-content) :

   1. Ouvrez le menu **Informations sur la page**.
   1. Sélectionnez **Publier la page**.

  ![screen_shot_2018-03-21at161026](assets/screen_shot_2018-03-21at161026.png)

* La dépublication d’une page à partir de la console ne peut se faire que par l’intermédiaire de l’option **Gérer la publication**, disponible uniquement sur la barre d’outils (et non via les actions rapides).

  L’option **Dépublier la page** est toujours disponible via le menu **Informations sur la page** dans l’éditeur.

  ![screen_shot_2018-03-21at161059](assets/screen_shot_2018-03-21at161059.png)

  Voir [Publication de pages](/help/sites-authoring/publishing-pages.md#unpublishing-pages) pour plus d’informations.

### Déplacement, copier-coller ou suppression d’une page {#move-copy-and-paste-or-delete-your-page}

Ces actions peuvent toutes être déclenchées en suivant ces étapes :

1. [Accédez à la page](#finding-your-page) que vous souhaitez déplacer, copier et coller ou supprimer.
1. Sélectionnez l’icône de copie (puis de collage), de déplacement ou de suppression selon vos besoins à l’aide de l’une des méthodes suivantes :

   * [Actions rapides (vue Carte/Bureau uniquement)](#quick-actions-card-view-desktop-only) pour la ressource appropriée.
   * La barre d’outils [une fois la page sélectionnée](#selecting-your-page-for-further-action).

   Ensuite, en fonction de l’action sélectionnée :

   * Copier :

      * Accédez au nouvel emplacement, puis collez.

   * Déplacer :

      * L’assistant s’ouvre pour collecter les informations nécessaires au déplacement de la page. Suivez les instructions s’affichant à l’écran.

   * Supprimer :

      * Le système vous invite à confirmer l’action.

   >[!NOTE]
   >
   >La suppression n’est pas proposée comme action rapide.

### Verrouillage d’une page (puis déverrouillage) {#locking-your-page-then-unlocking}

Le [verrouillage d’une page](/help/sites-authoring/editing-content.md#locking-a-page) empêche d’autres auteurs de travailler dessus en même temps que vous. L’icône/le bouton Verrouiller (et Déverrouiller) est accessible :

* La barre d’outils [une fois la page sélectionnée](#selecting-your-page-for-further-action).
* Dans le [menu déroulant Informations sur la page](#editing-the-page-properties) lors de la modification d’une page.
* Dans la barre d’outils de la page lors de la modification d’une page (si la page est verrouillée).

Par exemple, l’icône de verrouillage se présente comme suit :

![screen_shot_2018-03-21at161124](assets/screen_shot_2018-03-21at161124.png)

### Accès aux références de page {#accessing-page-references}

Un [accès rapide aux références](/help/sites-authoring/author-environment-tools.md#references) depuis et vers une page est possible dans le rail de références.

1. Sélectionnez les **Références** à l’aide de l’icône de la barre d’outils (avant ou après la [sélection d’une page](#selecting-your-page-for-further-action)) :

   ![screen_shot_2018-03-21at161210](assets/screen_shot_2018-03-21at161210.png)

   Une liste des types de références s’affiche :

   ![screen-shot_2019-03-05at114412](assets/screen-shot_2019-03-05at114412.png)

1. Appuyez ou cliquez sur le type de référence requis pour afficher d’autres détails et, le cas échéant, effectuer d’autres actions.

### Création d’une version d’une page {#creating-a-version-of-your-page}

Pour créer une [version](/help/sites-authoring/working-with-page-versions.md) de votre page :

1. Pour ouvrir le rail de la chronologie, sélectionnez la **[Chronologie](/help/sites-authoring/basic-handling.md#timeline)** à l’aide de l’icône de la barre d’outils (avant ou après la [sélection d’une page](#selecting-your-page-for-further-action)) :

   ![screen_shot_2018-03-21at161355](assets/screen_shot_2018-03-21at161355.png)

1. Cliquez sur la flèche Haut en bas à droite de la colonne Chronologie pour afficher d’autres boutons, y compris **Enregistrer comme version**.

   ![screen-shot_2019-03-05at114600](assets/screen-shot_2019-03-05at114600.png)

1. Sélectionnez **Enregistrer comme version**, puis **Créer**.

### Restauration/comparaison d’une version d’une page {#restoring-comparing-a-version-of-your-page}

Le même mécanisme de base est appliqué pour restaurer ou pour comparer des versions d’une page :

1. Sélectionnez la **[Chronologie](/help/sites-authoring/basic-handling.md#timeline)** à l’aide de l’icône de la barre d’outils (avant ou après la [sélection d’une page](#selecting-your-page-for-further-action)) :

   ![screen_shot_2018-03-21at161355-1](assets/screen_shot_2018-03-21at161355-1.png)

   Si une version de votre page a déjà été enregistrée, elle est répertoriée dans la chronologie.

1. Cliquez sur la version à restaurer ; cela permet d’afficher d’autres boutons d’action :

   * **Revenir à cette version**

      * La version est restaurée.

   * **Afficher les différences**

      * La page s’ouvre avec les différences (entre les deux versions) mises en surbrillance.
