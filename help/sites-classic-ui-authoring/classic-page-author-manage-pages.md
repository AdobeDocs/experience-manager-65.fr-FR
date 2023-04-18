---
title: Création et organisation des pages
description: Cette section décrit comment créer et gérer des pages avec AEM afin que vous puissiez ensuite créer du contenu sur ces pages.
uuid: 47ce137a-7a85-4b79-b4e0-fdf08a9e77bd
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 14b8758b-f164-429a-b299-33b0703f8bec
exl-id: bd2636d1-6f13-4c6c-b8cd-3bed9e83a101
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: tm+mt
source-wordcount: '1910'
ht-degree: 48%

---

# Création et organisation des pages{#creating-and-organizing-pages}

Cette section décrit comment créer et gérer des pages avec Adobe Experience Manager (AEM) afin que vous puissiez ensuite [créer du contenu](/help/sites-classic-ui-authoring/classic-page-author-edit-content.md) sur ces pages.

>[!NOTE]
>
>Votre compte a besoin de la fonction [droits d’accès appropriés](/help/sites-administering/security.md) et [permissions](/help/sites-administering/security.md#permissions) pour agir sur les pages, par exemple, créer, copier, déplacer, modifier, supprimer.
>
>En cas de problème, contactez votre administrateur système.

## Organisation du site web {#organizing-your-website}

En tant qu’auteur, vous devez organiser votre site web dans AEM. Cela implique de créer et de nommer vos pages de contenu de façon à ce que :

* vous puissiez les trouver facilement dans l’environnement de création ;
* les visiteurs sur votre site puissent facilement les parcourir dans l’environnement de publication.

Vous pouvez également vous aider de [dossiers](#creating-a-new-folder) pour organiser votre contenu.

La structure d’un site Web peut être comparée à celle d’un *arbre* qui soutient vos pages de contenu. Les noms de ces pages de contenu sont utilisés pour former des URL qui indiquent les titres lorsque le contenu des pages est affiché.

Vous trouverez ci-dessous un extrait du site Geometrixx ; par exemple, où est accessible la page `Triangle` :

* Environnement de création

   `http://localhost:4502/cf#/content/geometrixx/en/products/triangle.html`

* Environnement de publication

   `http://localhost:4503/content/geometrixx/en/products/triangle.html`

   Selon la configuration de votre instance, le segment `/content` peut être facultatif dans l’environnement de publication.

```xml
  /content
    /geometrixx
      /en
        /toolbar...
        /products
          /triangle
            /overview
            /features
          /square...
          /circle...
          /...
        /...
      /fr...
      /de...
      /es...
      /...
    /...
```

Cette structure est visible à partir de la console Sites web, que vous pouvez utiliser pour [parcourir l’arborescence](/help/sites-classic-ui-authoring/author-env-basic-handling.md#main-pars-text-15).

![chlimage_1-151](assets/chlimage_1-151.png)

### Conventions de dénomination des pages {#page-naming-conventions}

Lors de la création d’une page, il y a deux champs clés :

* **[Titre](#title)** :

   * Il s’affiche pour l’utilisateur dans la console et dans la partie supérieure du contenu de la page lors de la modification.
   * Ce champ est obligatoire.

* **[Nom](#name)** :

   * Il est utilisé pour générer l’URI.
   * L’entrée utilisateur pour ce champ est facultative. S’il n’est pas spécifié, le nom est dérivé du titre.

Lors de la création d’une page, AEM [valide le nom de la page en fonction des conventions](/help/sites-developing/naming-conventions.md) imposées par AEM et JCR.

La mise en œuvre et la liste des caractères autorisés diffère légèrement en fonction de l’IU (ils sont plus étendus pour l’IU activée pour les écrans tactiles), mais les caractères autorisés minimum sont les suivants :

* &quot;a&quot; à &quot;z&quot;
* &quot;A&quot; à &quot;Z&quot;
* &#39;0&#39; à &#39;9&#39;
* _ (trait de soulignement)
* `-` (tiret/signe moins)

Utilisez uniquement ces caractères si vous souhaitez vous assurer qu’ils sont acceptés/utilisés (si vous avez besoin des détails complets de tous les caractères autorisés, reportez-vous à la section [les conventions de dénomination ;](/help/sites-developing/naming-conventions.md)).

#### Titre {#title}

Si vous n’indiquez qu’un **titre** de page lors de la création d’une page, AEM utilise le **nom** de la page de cette chaîne et [valide le nom en fonction des conventions](/help/sites-developing/naming-conventions.md) imposées par AEM et JCR. Dans les deux interfaces utilisateur a **Titre** Le champ contenant des caractères non valides sera accepté, mais les caractères non valides seront remplacés pour le nom dérivé. Par exemple :

| Titre | Nom dérivé |
|---|---|
| Schön | schoen.html |
| SC%&amp;&amp;ast;ç+ | sc---c-.html |

#### Nom {#name}

Si vous indiquez un **nom** de page lors de la création d’une page, AEM [valide le nom en fonction des conventions](/help/sites-developing/naming-conventions.md) imposées par AEM et JCR.

Dans l’IU classique, vous **ne pouvez pas entrer de caractères non valides** dans le champ **Nom**.

>[!NOTE]
>Dans l’IU activée pour les écrans tactiles, vous **ne pouvez pas utiliser de caractères non valides** dans le champ **Nom**. Lorsqu’AEM détecte des caractères non valides, le champ est mis en surbrillance et un message d’explication s’affiche et indique les caractères à supprimer/remplacer.

>[!NOTE]
>
>Évitez d’utiliser un code à deux lettres, tel que défini par la norme ISO-639-1, sauf s’il s’agit d’une racine de langue.
>
>Voir [Préparation du contenu à traduire](/help/sites-administering/tc-prep.md) pour plus d’informations.

### Modèles {#templates}

Dans AEM, un modèle spécifie un type de page spécialisé. Un modèle sera utilisé comme base pour toute nouvelle page en cours de création.

Le modèle définit la structure d’une page ; y compris une miniature et d’autres propriétés. Par exemple, vous pouvez avoir des modèles distincts pour les pages de produits, les plans de site et les informations de contact. Les modèles se composent de [components](#components).

AEM comporte plusieurs modèles prêts à l’emploi. Les modèles proposés dépendent du site web individuel et des informations qui doivent être fournies (lors de la création d’une page) de l’interface utilisée. Les champs clés sont les suivants :

* **Titre**
Titre affiché sur la page web obtenue.

* **Nom**
Utilisé lors de l’attribution du nom de la page.

* **Modèle**
Liste des modèles utilisables lors de la génération de la nouvelle page.

### Composants {#components}

Les composants sont les éléments fournis par AEM afin que vous puissiez ajouter des types de contenu spécifiques. Des composants prêts à l’emploi sont fournis avec AEM pour procurer une fonctionnalité complète ; il s’agit des composants suivants :

* Texte
* Image
* Slideshow
* Vidéo
* beaucoup plus

Une fois que vous avez créé et ouvert une page, vous pouvez [ajouter du contenu à l’aide des composants](/help/sites-classic-ui-authoring/classic-page-author-edit-content.md#insertinganewparagraph), disponibles dans le [sidekick](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#sidekick).

## Gestion des pages {#managing-pages}

### Création d’une page {#creating-a-new-page}

Avant de pouvoir commencer à créer du contenu, vous devez créer une page, à moins que toutes les pages n’aient été créées pour vous à l’avance :

1. Dans la **Sites web** , sélectionnez le niveau auquel vous souhaitez créer une page.

   Dans l’exemple suivant, vous créez une page sous le niveau **Produits** - affiché dans le volet de gauche ; le volet de droite affiche les pages qui existent déjà au niveau sous **Produits**.

   ![screen_shot_2012-02-15at114413am](assets/screen_shot_2012-02-15at114413am.png)

1. Dans le **Nouveau...** (cliquez sur la flèche en regard de l’option **Nouveau...**), sélectionnez **Nouvelle page...**. Le **Créer une page** s’ouvre.

   Cliquer **Nouveau...** agit également comme un raccourci vers la fonction **Nouvelle page...** .

1. Le **Créer une page** vous permet d’effectuer les opérations suivantes :

   * Fournissez une **Titre**; s’affiche pour l’utilisateur.
   * Fournissez une **Nom**; il est utilisé pour générer l’URI. S’il n’est pas spécifié, le nom est dérivé du titre.

      * Si vous indiquez le **nom** d’une page lors de la création d’une page, AEM [valide le nom en fonction des conventions](/help/sites-developing/naming-conventions.md) imposées par AEM et JCR.
      * Dans l’IU classique, vous **ne pouvez pas entrer de caractères non valides** dans le champ **Nom**.
   * Cliquez sur le modèle à utiliser pour créer la page.

      Le modèle sert de base à la nouvelle page. par exemple, pour déterminer la mise en page de base d’une page de contenu.
   >[!NOTE]
   >
   >Voir [Conventions de dénomination des pages](#page-naming-conventions).

   Les informations minimales requises pour créer une page sont les suivantes : **Titre** et le modèle requis.

   ![screen_shot_2012-02-15at114845am](assets/screen_shot_2012-02-15at114845am.png)

   >[!NOTE]
   >
   >Si vous souhaitez utiliser des caractères Unicode dans les URL, définissez la propriété d’alias (`sling:alias`) ([propriétés de page](/help/sites-classic-ui-authoring/classic-page-author-edit-page-properties.md)).

1. Cliquez sur **Créer** pour créer la page. Vous revenez au **Sites web** console où vous pouvez voir une entrée pour la nouvelle page.

   La console fournit des informations sur la page (par exemple, lorsqu’elle a été modifiée pour la dernière fois et par qui) qui est mise à jour selon les besoins.

   >[!NOTE]
   >
   >Vous pouvez également créer une page lorsque vous modifiez une page existante. Utilisez l’option **Créer une page enfant** de l’onglet **Page** du sidekick pour créer une page directement sous la page en cours de modification.

### Ouverture d’une page pour la modifier {#opening-a-page-for-editing}

Vous pouvez ouvrir la page à [modifié](/help/sites-classic-ui-authoring/classic-page-author-edit-content.md#editing-a-component-content-and-properties) par l’une des méthodes suivantes :

* De **Sites web** console, vous pouvez **double-clic** l’entrée de page pour l’ouvrir en vue de la modifier.

* Dans la console **Sites web**, **cliquez avec le bouton droit** (menu contextuel) sur l’élément de page, puis sélectionnez **Ouvrir** dans le menu.

* Après avoir ouvert une page, vous pouvez accéder à d’autres pages du site (en vue de les modifier) en cliquant sur des liens hypertexte.

### Copier et coller une page {#copying-and-pasting-a-page}

Lors de la copie, vous pouvez copier :

* une seule page
* une page ainsi que toutes les sous-pages ;

1. Dans la **Sites web** , sélectionnez la page à copier.

   >[!NOTE]
   >
   >À ce stade, il n’est pas pertinent de copier une seule page ou les sous-pages sous-jacentes.

1. Cliquez sur **Copier**.

1. Accédez au nouvel emplacement et cliquez sur :

   * **Coller** - pour coller la page avec toutes les sous-pages
   * **Maj + Coller** - pour coller uniquement la page sélectionnée

   Les pages sont collées au nouvel emplacement.

   >[!NOTE]
   >
   >Le nom de la page peut être ajusté automatiquement si une page existante porte déjà le même nom.

   >[!NOTE]
   >
   >Utilisez l’option **Copier la page** dans l’onglet **Page** du sidekick. Cela ouvre une boîte de dialogue dans laquelle vous pouvez spécifier la destination, etc.

### Déplacement ou changement de nom de page {#moving-or-renaming-page}

>[!NOTE]
>
>Le changement de nom d’une page est également soumis au [Conventions de dénomination des pages](#page-naming-conventions) lors de la spécification du nouveau nom de page.

La procédure pour déplacer ou renommer une page est la même. Avec la même action, vous pouvez :

* déplacer une page vers un nouvel emplacement ;
* renommer une page au même emplacement ;
* déplacer une page vers un nouvel emplacement et la renommer en même temps.

AEM vous offre la possibilité de mettre à jour les liens internes vers la page renommée ou déplacée. Cette opération peut être effectuée page par page afin d’offrir une flexibilité totale.

Pour déplacer ou renommer une page :

1. Plusieurs méthodes permettent de déclencher un déplacement :

   * Dans la console **Sites web**, cliquez sur la page pour la sélectionner, puis sélectionnez **Déplacer**.
   * Dans la **Sites web** , vous pouvez également sélectionner l’élément de page, puis **clic droit** et sélectionnez **Déplacer..**
   * Lorsque vous modifiez une page, vous pouvez sélectionner **Déplacer la page** de la **Page** de l’onglet du sidekick.

1. La fenêtre **Déplacer** s’ouvre ; vous pouvez saisir un nouvel emplacement, un nouveau nom pour la page, ou les deux.

   ![screen_shot_2012-02-15at121336pm](assets/screen_shot_2012-02-15at121336pm.png)

   La page répertorie également toutes les pages qui font référence à la page en cours de déplacement. Selon l’état de la page de référence, vous pouvez ajuster ces liens sur et/ou republier les pages.

1. Renseignez les champs suivants, selon le cas :

   * **Destination**

      Utilisez le plan du site (disponible via le sélecteur déroulant) pour sélectionner l’emplacement où la page doit être déplacée.

      Si vous renommez uniquement la page, ignorez ce champ.

   * **Déplacer**

      Indiquez la page à déplacer, ce champ est généralement complété par défaut, selon la méthode de déplacement utilisée et l’endroit où vous avez lancé l’opération.

   * **Renommer en**

      Le libellé de la page active s’affiche par défaut. Indiquez le nouveau libellé de page, le cas échéant.

   * **Régler**

      Mettez à jour les liens de la page répertoriée qui pointent vers la page déplacée : par exemple, si la page A contient des liens vers la page B, AEM ajuste les liens de la page A au cas où vous déplaceriez la page B.

      Cette option peut être sélectionnée/désélectionnée pour chaque page de référence.

   * **Republier**

      Publie à nouveau la page de référence ; ici encore, cette option peut être sélectionnée pour chaque page.
   >[!NOTE]
   >
   >Si la page a déjà été activée, le fait de la déplacer la désactivera automatiquement. Par défaut, elle sera réactivée une fois le déplacement terminé. Vous pouvez toutefois changer ce comportement en désélectionnant l’option **Republier** pour la page dans la fenêtre **Déplacer**.

1. Cliquez sur **Déplacer**, puis sur **OK** pour confirmer l’opération.

   >[!NOTE]
   >
   >Le titre de la page n’est pas mis à jour.

### Suppression d’une page {#deleting-a-page}

1. Vous pouvez supprimer une page à différents emplacements :

   * Dans le **Sites web** console, cliquez pour sélectionner la page, puis cliquez avec le bouton droit et sélectionnez **Supprimer** dans le menu qui s’affiche.
   * Dans le **Sites web** console, cliquez pour sélectionner la page, puis sélectionnez **Supprimer** dans le menu de la barre d’outils.
   * Dans le sidekick, utilisez **Page** pour sélectionner **Supprimer la page** : supprime la page actuellement ouverte.

1. Une fois que vous avez choisi de supprimer une page, vous devez confirmer la requête, car l’action ne peut pas être annulée.

   >[!NOTE]
   >
   >Après la suppression, si la page a été publiée, vous pouvez restaurer la dernière version (ou une version spécifique), mais cela peut ne pas avoir exactement le même contenu que votre dernière version si d’autres modifications ont été apportées. Voir [Restauration de pages](/help/sites-classic-ui-authoring/classic-page-author-work-with-versions.md#restoringpages) pour plus de détails.

>[!NOTE]
>
>Si une page est déjà activée, elle est automatiquement désactivée avant suppression.

### Verrouillage d’une page    {#locking-a-page}

Vous pouvez [verrouiller ou déverrouiller une page](/help/sites-classic-ui-authoring/classic-page-author-edit-content.md#locking-a-page) à partir d’une console ou lorsque vous modifiez une page. Les deux environnements indiquent également si une page est verrouillée ou non.

### Création d’un dossier {#creating-a-new-folder}

>[!NOTE]
>
>Les dossiers sont également soumis aux [Conventions de dénomination des pages](#page-naming-conventions) lors de la spécification du nouveau nom de dossier.

1. Ouvrez le **Sites web** et accédez à l’emplacement requis.
1. Dans le menu **Nouveau...** (cliquez sur la flèche en regard de l’option **Nouveau...**), sélectionnez **Nouveau dossier...**.
1. La boîte de dialogue **Créer un dossier** s’affiche. Vous pouvez saisir un **nom** et un **titre** :

   ![chlimage_1-152](assets/chlimage_1-152.png)

1. Pour créer le dossier, sélectionnez **Créer**.
