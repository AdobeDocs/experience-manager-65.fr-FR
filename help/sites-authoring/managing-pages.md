---
title: Créer et organiser des pages avec AEM
description: Découvrez comment créer et gérer des pages avec Adobe Experience Manager.
exl-id: 74576e51-4b4e-464e-a0b8-0fae748a505d
source-git-commit: cc63291c32f7a234398ebe8bf67ab53aaf8fa90f
workflow-type: tm+mt
source-wordcount: '2436'
ht-degree: 97%

---

# Création et organisation des pages {#creating-and-organizing-pages}

Cette section décrit comment créer et gérer des pages avec Adobe Experience Manager (AEM) afin de [créer du contenu](/help/sites-authoring/editing-content.md) sur ces dernières.

>[!NOTE]
>
>Votre compte doit avoir les [droits d’accès](/help/sites-administering/security.md) ainsi que les [autorisations](/help/sites-administering/security.md#permissions) nécessaires pour agir sur ces pages ; par exemple, créer, copier, déplacer, modifier et supprimer.
>
>En cas de problème, contactez votre administrateur système.

>[!NOTE]
>
>Il existe un certain nombre de [raccourcis clavier](/help/sites-authoring/keyboard-shortcuts.md) à utiliser à partir de la console Sites web qui facilitent l’organisation des pages.

## Organisation du site web {#organizing-your-website}

En tant qu’auteur, vous devez organiser votre site web dans AEM. Cela implique de créer et de nommer vos pages de contenu de façon à ce que :

* vous puissiez les trouver facilement dans l’environnement de création ;
* les visiteurs sur votre site puissent facilement les parcourir dans l’environnement de publication.

Vous pouvez également vous aider de [dossiers](#creating-a-new-folder) pour organiser votre contenu.

La structure d’un site web peut être comparée à celle d’un arbre qui soutient vos pages de contenu. Les noms de ces pages de contenu sont utilisés pour former des URL qui indiquent les titres lorsque le contenu des pages est affiché.

Vous trouverez ci-dessous un exemple provenant du site We.Retail, qui permet d’accéder à une page de shorts de randonnée (`desert-sky-shorts`) :

* Environnement de création
  `https://localhost:4502/editor.html/content/we-retail/us/en/products/equipment/hiking/desert-sky-shorts.html`

* Environnement de publication
  `https://localhost:4503/content/we-retail/us/en/products/equipment/hiking/desert-sky-shorts.html`

Selon la configuration de votre instance, le segment `/content` peut être facultatif dans l’environnement de publication.

```xml
 /content
 /we-retail
  /us
   /en
    /products
     /equipment
      /hiking
       /desert-sky-shorts
       /hiking-poles
       /...
      /running...
      /surfing...
      /...
     /seasonal...
     /...
    /about-us
    /experience
    /...
   /es...
  /de...
  /fr...
  /...
 /...
```

Cette structure peut être visualisée à partir de la console **Sites**, dans laquelle vous pouvez [accéder aux pages de votre site web](/help/sites-authoring/basic-handling.md#navigating) et y effectuer des opérations. Vous pouvez également créer des sites et des [pages](#creating-a-new-page).

À n’importe quel point, la branche ascendante est visible à partir du chemin de navigation dans la barre d’en-tête :

![caop-01](assets/caop-01.png)

### Conventions de dénomination des pages {#page-naming-conventions}

Lors de la création d’une page, il y a deux champs clés :

* **[Titre](#title)** :

   * Il s’affiche pour l’utilisateur dans la console et dans la partie supérieure du contenu de la page lors de la modification.
   * Ce champ est obligatoire.

* **[Nom](#name)** :

   * Il est utilisé pour générer l’URI.
   * L’entrée utilisateur pour ce champ est facultative. S’il n’est pas spécifié, le nom est dérivé du titre. Consultez la section [Restrictions de nom de page et bonnes pratiques](/help/sites-authoring/managing-pages.md#page-name-restrictions-and-best-practices) pour plus d’informations.

#### Restrictions de nom de page et bonnes pratiques {#page-name-restrictions-and-best-practices}

Le **Titre** et le **Nom** de la page peuvent être créés séparément, mais ils sont associés :

* lors de la création d’une page, seul le champ **Titre** est requis. Si aucun **nom** n’est indiqué lors de la création de la page, AEM génère un nom à partir des 64 premiers caractères du titre (examinez la validation présentée ci-dessous). Seuls les 64 premiers caractères sont utilisés dans le cadre de la bonne pratique définie pour les noms de pages courts.

* Si un nom de page est spécifié manuellement par l’auteur, la limite de 64 caractères ne s’applique pas, mais d’autres limitations techniques sur la longueur du nom de la page peuvent s’appliquer.

>[!NOTE]
>
>Lorsque vous définissez un nom de page, une règle de base à respecter consiste à faire en sorte que le nom de la page reste court, mais aussi significatif que possible pour faciliter la compréhension du lecteur. Consultez le [Guide de style W3C](https://www.w3.org/Provider/Style/TITLE.html) sur l’élément `title` pour obtenir des informations supplémentaires.
>
>N’oubliez pas que certains navigateurs (par exemple, les anciennes versions d’IE) n’acceptent que les URL n’excédant pas une certaine longueur. C’est pourquoi il existe également une raison technique à garder les noms de pages courts.

Lors de la création d’une page, AEM [valide son nom en fonction des conventions](/help/sites-developing/naming-conventions.md) imposées par AEM et JCR.

Les caractères minimum autorisés sont :

* De « a » à « z »
* De « A » à « Z »
* De « 0 » à « 9 »
* `_` (trait de soulignement)
* `-` (tiret/signe moins)

Vous trouverez la liste complète et détaillée des caractères autorisés dans les [conventions de dénomination](/help/sites-developing/naming-conventions.md).

>[!NOTE]
>
>Si AEM est exécuté sur un [déploiement de gestionnaire de persistance MongoMK](/help/sites-deploying/recommended-deploys.md), les noms de page sont limités à 150 caractères.

#### Titre {#title}

Si vous n’indiquez qu’un **titre** de page lors de la création d’une page, AEM utilise le **nom** de la page de cette chaîne et [valide le nom en fonction des conventions](/help/sites-developing/naming-conventions.md) imposées par AEM et JCR. Un champ **Titre** contenant des caractères non valides sera accepté, mais les caractères non valides seront remplacés pour le nom dérivé. Par exemple :

| Titre | Nom dérivé |
|---|---|
| Schön | schoen.html |
| SC%&amp;&#42;ç+ | sc---c-.html |

#### Nom {#name}

Si vous indiquez un **nom** de page lors de la création d’une page, AEM [valide le nom en fonction des conventions](/help/sites-developing/naming-conventions.md) imposées par AEM et JCR. Vous ne pouvez pas utiliser de caractères non valides dans le champ **Nom**. Lorsque AEM détecte des caractères non valides, le champ est mis en surbrillance avec un message d’explication.

![caop-02](assets/caop-02.png)

>[!NOTE]
>
>Vous devez éviter d’utiliser un code à deux lettres tel que défini par la norme ISO-639-1 comme nom de page, sauf s’il s’agit d’une racine de langue.
>
>Pour plus d’informations, voir [Préparation du contenu pour la traduction](/help/sites-administering/tc-prep.md).

### Modèles {#templates}

Dans AEM, un modèle spécifie un type de page spécialisé. Un modèle sera utilisé comme base pour toute nouvelle page créée.

Le modèle définit la structure d’une page, y compris une miniature et d’autres propriétés. Par exemple, vous pouvez avoir des modèles distincts pour les pages de produits, les plans de site et les coordonnées. Les modèles sont constitués de [composants](#components).

AEM comporte plusieurs modèles prêts à l’emploi. Les modèles disponibles dépendent du site web individuel. Les champs clés sont les suivants :

* **Titre**
Titre affiché sur la page web obtenue.

* **Nom**
Utilisé lors de l’attribution du nom de la page.

* **Modèle**
Liste des modèles utilisables lors de la génération de la nouvelle page.

>[!NOTE]
>
>Si cette option est configurée sur votre instance, [les auteurs de modèles peuvent créer des modèles avec l’éditeur de modèles](/help/sites-authoring/templates.md).

### Composants {#components}

Les composants sont des éléments fournis par AEM pour vous permettre d’ajouter des types spécifiques de contenu. Des [composants « prêts à l’emploi »](/help/sites-authoring/default-components-console.md) sont fournis avec AEM pour procurer une fonctionnalité complète. Il s’agit des composants suivants :

* Texte
* Image
* Diaporama
* Vidéo
* Et bien plus encore.

Une fois que vous avez créé et ouvert une page, vous pouvez [ajouter du contenu à l’aide de composants](/help/sites-authoring/editing-content.md#insertinganewparagraph), disponibles dans le [navigateur de composants](/help/sites-authoring/author-environment-tools.md#componentbrowser).

>[!NOTE]
>
>La [console Composants](/help/sites-authoring/default-components-console.md) affiche un aperçu des composants sur votre instance.

## Gestion des pages {#managing-pages}

### Création d’une page {#creating-a-new-page}

Avant de pouvoir commencer à créer du contenu, vous devez créer une page, à moins que toutes les pages n’aient été créées pour vous à l’avance :

1. Ouvrez la console Sites (par exemple, [https://localhost:4502/sites.html/content](https://localhost:4502/sites.html/content)).
1. Accédez à l’emplacement où créer la page.
1. Ouvrez le sélecteur de liste déroulante avec l’option **Créer** de la barre d’outils, puis sélectionnez **Page** dans la liste :

   ![caop-03](assets/caop-03.png)

1. À la première étape de l’assistant, vous pouvez effectuer l’une des opérations suivantes :

   * Sélectionnez le modèle à utiliser pour créer la page, puis cliquez ou appuyez sur **Suivant** pour poursuivre.

   * Cliquez/appuyez sur **Annuler** pour interrompre le processus.

   ![caop-04](assets/caop-04.png)

1. À l’étape finale de l’assistant, vous pouvez effectuer l’une des opérations suivantes :

   * Utilisez les trois onglets pour accéder aux [propriétés de la page](/help/sites-authoring/editing-page-properties.md) à attribuer à la nouvelle page, puis cliquez ou appuyez sur **Créer** pour réellement créer la page.

   * Utilisez **Précédent** pour revenir à la sélection de modèle.

   Les champs clés sont les suivants :

   * **Titre** :

      * Il est visible par la personne utilisatrice et est obligatoire.

   * **Nom** :

      * Il est utilisé pour générer l’URI. S’il n’est pas spécifié, le nom est dérivé du titre.
      * Si vous indiquez un **nom** de page lors de la création d’une page, AEM [valide le nom en fonction des conventions](/help/sites-developing/naming-conventions.md) imposées par AEM et JCR.

      * Vous **ne pouvez pas utiliser de caractères non valides** dans le champ **Nom**. Lorsqu’AEM détecte des caractères non valides, le champ est mis en surbrillance et un message d’explication s’affiche et indique les caractères à supprimer/remplacer.

   >[!NOTE]
   >
   >Voir [Conventions de dénomination de page](#page-naming-conventions).

   Les informations minimales requises pour créer une page sont le **Titre**.

   ![caop-05](assets/caop-05.png)

1. Cliquez ou appuyez sur **Créer** pour terminer le processus et créer la page. La boîte de dialogue de confirmation vous demande si vous souhaitez **ouvrir** immédiatement la page ou revenir à la console (**Terminé**) :

   ![chlimage_1-118](assets/chlimage_1-118.png)

   >[!NOTE]
   >
   >Si vous créez une page en utilisant un nom qui existe déjà à cet emplacement, le système génère automatiquement une variante du nom en y ajoutant un numéro. Par exemple, si `winter` existe déjà, le nom de la nouvelle page sera `winter0`.

1. Si vous revenez à la console, la nouvelle page est présentée :

   ![caop-06](assets/caop-06.png)

>[!CAUTION]
>
>Une fois qu’une page a été créée, son modèle ne peut plus être modifié, à moins de [créer un lancement avec un nouveau modèle](/help/sites-authoring/launches-creating.md#create-launch-with-new-template) ; vous perdrez alors tout contenu déjà existant.

### Ouverture d’une page pour la modifier {#opening-a-page-for-editing}

Après avoir créé une page ou accédé à une page existante (dans la console), vous pouvez l’ouvrir pour la modifier :

1. Ouvrez la console **Sites**.
1. Accédez à la page à modifier.
1. Sélectionnez votre page à l’aide de l’une des options suivantes :

   * [Actions rapides](/help/sites-authoring/basic-handling.md#quick-actions)
   * Le [mode de sélection](/help/sites-authoring/basic-handling.md#navigatingandselectionmode) et la barre d’outils

   Sélectionnez ensuite l’icône **Modifier** :

   ![screen_shot_2018-03-22at105355](assets/screen_shot_2018-03-22at105355.png)

1. La page s’ouvre ; vous pouvez [la modifier](/help/sites-authoring/editing-content.md#touchoptimizedui) selon vos besoins.

>[!NOTE]
>
>L’accès à d’autres pages à partir de l’Éditeur de page n’est possible qu’en mode Aperçu, car les liens ne sont pas actifs dans le mode d’édition.

### Copier et coller une page {#copying-and-pasting-a-page}

Vous pouvez copier une page ainsi que toutes ses sous-pages à un nouvel emplacement :

1. Dans la console **Sites**, accédez à la page à copier.
1. Sélectionnez votre page à l’aide de l’une des options suivantes :

   * [Actions rapides](/help/sites-authoring/basic-handling.md#quick-actions)
   * Le [mode de sélection](/help/sites-authoring/basic-handling.md#navigatingandselectionmode) et la barre d’outils

   Puis l’icône **Copier** la page :

   ![screen_shot_2018-03-22at105425](assets/screen_shot_2018-03-22at105425.png)

   >[!NOTE]
   >
   >Si vous êtes en mode de sélection, la page est fermée dès qu’elle est copiée.

1. Accédez à l’emplacement destiné à la nouvelle copie de la page.
1. L’icône **Coller** est disponible avec une flèche déroulante directement à droite :

   ![Coller](assets/paste-without-children.png)

   Vous pouvez effectuer l’une des actions suivantes :
   * Sélectionner l’icône de page **Coller** : une copie de la page d’origine et de toutes les pages enfants sera créée à cet emplacement.
   * Sélectionner la flèche déroulante pour afficher l’option **Coller sans enfants**. Une copie de la page d’origine sera créée à cet emplacement ; les pages enfants ne seront pas copiées.

   >[!NOTE]
   >
   >Si vous copiez la page à un emplacement où il existe une page du même nom que l’original, le système génère automatiquement une variante du nom en y ajoutant un numéro. Par exemple, si `winter` existe déjà, `winter` deviendra `winter1`.

### Déplacement ou modification du nom d’une page {#moving-or-renaming-a-page}

>[!NOTE]
>
>La modification du nom d’une page est également soumise aux [Conventions de dénomination de page](#page-naming-conventions) lors de la spécification du nouveau nom de la page.

>[!NOTE]
>
>Une page ne peut être déplacée qu’à un emplacement où le modèle sur lequel la page est basée est autorisé. Pour plus d’informations, voir [Disponibilité des modèles](/help/sites-developing/templates.md#template-availability).

La procédure pour déplacer ou renommer une page est plus ou moins la même et est gérée par le même assistant. Cet assistant permet d’effectuer les opérations suivantes :

* Renommer une page sans la déplacer
* Déplacer la page sans la renommer
* Déplacer et renommer une page simultanément

AEM vous offre la possibilité de mettre à jour les liens internes qui font référence à la page renommée ou déplacée. Cette opération peut être effectuée page par page afin d’offrir une flexibilité totale.

1. Accédez à la page à déplacer.
1. Sélectionnez votre page à l’aide de l’une des options suivantes :

   * [Actions rapides](/help/sites-authoring/basic-handling.md#quick-actions)
   * Le [mode de sélection](/help/sites-authoring/basic-handling.md#navigatingandselectionmode) et la barre d’outils

   Sélectionnez ensuite l’icône **Déplacer** la page :

   ![screen_shot_2018-03-22at105534](assets/screen_shot_2018-03-22at105534.png)

   L’assistant de déplacement de page s’ouvre alors.

1. À l’étape **Renommer** de l’assistant, vous pouvez effectuer l’une des opérations suivantes :

   * Spécifiez le nom à attribuer à la page après son déplacement et cliquez/appuyez sur **Suivant** pour poursuivre.

   * Cliquez/appuyez sur **Annuler** pour interrompre le processus.

   ![caop-07](assets/caop-07.png)

   Le nom de la page peut rester identique si vous déplacez uniquement la page.

   >[!NOTE]
   >
   >Si vous déplacez la page à un emplacement où il existe une page du même nom, le système génère automatiquement une variante du nom en y ajoutant un numéro. Par exemple, si `winter` existe déjà, `winter` deviendra `winter1`.

1. À l’étape **Sélectionner une destination** de l’assistant, vous pouvez effectuer l’une des opérations suivantes :

   * Utilisez la [vue Colonne](/help/sites-authoring/basic-handling.md#column-view) pour accéder au nouvel emplacement de la page :

      * Sélectionnez la destination en cliquant sur sa miniature.
      * Cliquez sur **Suivant** pour continuer.

   * Utilisez **Précédent** pour revenir à la spécification du nom de page.

   >[!NOTE]
   >
   >Par défaut, le parent de la page que vous déplacez/renommez est sélectionné comme destination.

   ![caop-08](assets/caop-08.png)

   >[!NOTE]
   >
   >Si vous déplacez la page à un emplacement où il existe une page du même nom, le système génère automatiquement une variante du nom en y ajoutant un numéro. Par exemple, si `winter` existe déjà, `winter` deviendra `winter1`.

1. Si la page est liée ou référencée, ou si elle a été publiée, les détails seront répertoriés dans l’étape **Ajuster/republier**.

   Vous pouvez indiquer quelles pages sont les pages à adapter et/ou à republier.

   >[!NOTE]
   >
   >Si la page n’est ni liée ni référencée, cette étape ne sera pas disponible.

   ![caop-09](assets/caop-09.png)

1. Si vous sélectionnez **Déplacer**, le processus se terminera et votre page sera déplacée ou renommée selon les besoins.

>[!NOTE]
>
>Si la page a déjà été publiée, son déplacement la dépublie automatiquement. Par défaut, elle sera republiée une fois le déplacement terminé, mais ce paramètre peut être modifié en décochant le champ **Republier** à l’étape **Ajuster/Republier**.

>[!NOTE]
>
>Si la page n’est pas référencée, les étapes **Ajuster/republier** sont ignorées.

#### Actions asynchrones {#asynchronous-actions}

Les actions de déplacement de page sont toujours traitées de manière asynchrone, ce qui permet à l’utilisateur de continuer à créer dans l’interface utilisateur sans entraves.

* L’utilisateur doit définir quand l’opération asynchrone doit être effectuée.
   * **Maintenant** : l’exécution de la tâche asynchrone commence immédiatement.
   * **Plus tard** : l’utilisateur peut définir le moment où la tâche asynchrone débutera.

  ![Déplacement de page asynchrone](assets/asynchronous-page-move.png)

L’état des tâches asynchrones peut être vérifié dans le [**tableau de bord État des tâches asynchrones**](/help/sites-administering/asynchronous-jobs.md#monitor-the-status-of-asynchronous-operations) en sélectionnant **Navigation globale** -> **Outils** -> **Opérations** -> **Tâches**.

>[!NOTE]
>
>Pour plus d’informations sur le traitement asynchrone des tâches et sur la manière de configurer la limite pour les actions de déplacement/modification du nom de page, consultez le document [Tâches asynchrones](/help/sites-administering/asynchronous-jobs.md) dans le guide de l’utilisateur relatif à l’administration.

>[!NOTE]
>
>Pour le traitement asynchrone des déplacements de page, vous avez besoin d’AEM version 6.5.3.0 ou ultérieure.

### Suppression d’une page {#deleting-a-page}

1. Accédez à la page que vous souhaitez supprimer.
1. En [mode de sélection](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources), sélectionnez la page requise, puis utilisez la commande **Supprimer** de la barre d’outils :

   ![screen_shot_2018-03-22at105622](assets/screen_shot_2018-03-22at105622.png)

   >[!NOTE]
   >
   >Par mesure de sécurité, l’icône **Supprimer la page** n’est pas disponible en tant qu’action rapide.

1. Une boîte de dialogue de confirmation s’affiche, utilisez :

   * **Annuler** pour abandonner l’opération.
   * **Supprimer** pour confirmer l’action :

      * Si la page ne comporte aucune référence, elle est supprimée.
      * Si la page comporte des références, un message vous informe qu’**une ou plusieurs pages sont référencées.** Vous pouvez sélectionner **Forcer la suppression** ou **Annuler**.

>[!NOTE]
>
>Si la page est déjà publiée, sa publication est automatiquement annulée avant la suppression.

### Verrouillage d’une page {#locking-a-page}

Vous pouvez [verrouillage/déverrouillage d’une page](/help/sites-authoring/editing-content.md#locking-a-page) depuis une console ou lors de la modification d’une page individuelle. Les informations sur les pages verrouillées s’affichent également aux deux emplacements.

![screen_shot_2018-03-22at105713](assets/screen_shot_2018-03-22at105713.png) ![screen_shot_2018-03-22at105720](assets/screen_shot_2018-03-22at105720.png)

### Création d’un dossier {#creating-a-new-folder}

Vous pouvez créer des dossiers pour classer vos fichiers et vos pages.

>[!NOTE]
>
>Les dossiers sont également soumis aux [Conventions de dénomination de page](#page-naming-conventions) lors de la spécification du nouveau nom de dossier.

>[!CAUTION]
>
>* Les dossiers ne peuvent être créés que directement sous **Sites** ou sous d’autres dossiers. Ils ne peuvent pas être créés sous une page.
>* Les opérations standard (déplacer, copier, coller, supprimer, publier, dépublier et afficher/modifier les propriétés) peuvent être effectuées sur un dossier.
>* Dans une Live Copy, les dossiers ne peuvent pas être sélectionnés.
>

1. Ouvrez la console **Sites** et accédez à l’emplacement requis.
1. Pour ouvrir la liste des options, sélectionnez **Créer** dans la barre d’outils
1. Sélectionnez **Dossier** pour ouvrir la boîte de dialogue. Vous pouvez y entrer le **nom** et le **titre** :

   ![chlimage_1-119](assets/chlimage_1-119.png)

1. Pour créer le dossier, sélectionnez **Créer**.
