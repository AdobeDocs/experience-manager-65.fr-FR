---
title: Utiliser les versions de pages
description: Découvrez le contrôle de version et apprenez à créer un instantané d’une page à un moment donné.
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
docset: aem65
exl-id: 4eb0de5e-0306-4166-9cee-1297a5cd14ce
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1351'
ht-degree: 100%

---

# Utilisation des versions de page{#working-with-page-versions}

Le contrôle de version permet de créer un « instantané » d’une page à un moment donné. Avec le contrôle de version, vous pouvez effectuer les opérations suivantes :

* Créez une version d’une page.
* Restaurez une version précédente d’une page, notamment afin d’annuler une modification que vous avez apportée à une page.
* Comparez la version actuelle d’une page à une version précédente avec les différences mises en surbrillance dans le texte et les images.

## Création d’une version {#creating-a-new-version}

Pour créer une version d’une page :

1. Dans votre navigateur, ouvrez la page pour laquelle créer une version.
1. Dans le sidekick, sélectionnez l’onglet **Contrôle de version**, puis le sous-onglet **Créer une version**.

   ![screen_shot_2012-02-14at40259pm](assets/screen_shot_2012-02-14at40259pm.png)

1. Entrez un commentaire dans la zone **Commenter** (facultatif).
1. Pour définir un libellé pour la version (facultatif), cliquez sur le bouton **Plus >>** et définissez le **Libellé** pour attribuer un nom à la version. Si le libellé n’est pas défini, la version se voit attribuer un numéro automatiquement incrémenté.
1. Cliquez sur **Créer la version**. Un message grisé apparaît sur la page, indiquant par exemple :
Version 1.2 créée pour : Chemises.

>[!NOTE]
>
>L’activation de la page entraîne la création automatique d’une version.

## Restaurer une version de page à partir du sidekick {#restoring-a-page-version-from-sidekick}

Pour restaurer la version précédente d’une page :

1. Ouvrez la page dont vous souhaitez restaurer une version précédente.
1. Dans le sidekick, sélectionnez l’onglet **Contrôle de version**, puis le sous-onglet **Restaurer une version**.

   ![screen_shot_2012-02-14at42949pm](assets/screen_shot_2012-02-14at42949pm.png)

1. Sélectionnez la version à restaurer, puis cliquez/appuyez sur **Restaurer**.

## Restaurer une version de page à partir de la console {#restoring-a-page-version-from-the-console}

Appliquez cette méthode pour restaurer une version de page. Elle peut également être utilisée pour restaurer des pages qui ont été supprimées :

1. Dans la console **Sites web**, accédez à la page à restaurer et sélectionnez-la.
1. Dans le menu supérieur, sélectionnez **Outils**, puis **Restaurer** :

   ![screen_shot_2012-02-08at41326pm](assets/screen_shot_2012-02-08at41326pm.png)

1. Si vous sélectionnez **Restaurer la version**, les versions de documents dans le dossier actif sont répertoriées. Même si une page a été supprimée, sa dernière version est répertoriée :

   ![screen_shot_2012-02-08at45743pm](assets/screen_shot_2012-02-08at45743pm.png)

1. Sélectionnez la version à restaurer, puis cliquez sur **Restaurer**. AEM restaure les versions (ou arborescences) sélectionnées.

### Restaurer une arborescence à partir de la console {#restoring-a-tree-from-the-console}

Appliquez cette méthode pour restaurer une version de page. Elle peut également être utilisée pour restaurer des pages qui ont été supprimées :

1. Dans la console **Sites web**, accédez au dossier à restaurer et sélectionnez-le.
1. Dans le menu supérieur, sélectionnez **Outils**, puis **Restaurer**.
1. Sélectionnez **Restaurer l’arborescence...** pour afficher une boîte de dialogue qui permet de sélectionner l’arborescence à restaurer :

   ![screen_shot_2012-02-08at45743pm-1](assets/screen_shot_2012-02-08at45743pm-1.png)

1. Cliquez sur **Restaurer**. AEM restaure l’arborescence sélectionnée.

## Comparer à une version précédente {#comparing-with-a-previous-version}

Comparer la version actuelle d’une page à une version précédente :

1. Dans votre navigateur, ouvrez la page que vous souhaitez comparer à une version précédente.
1. Dans le sidekick, sélectionnez l’onglet **Contrôle de version**, puis le sous-onglet **Restaurer une version**.

   ![screen_shot_2012-02-14at42949pm-1](assets/screen_shot_2012-02-14at42949pm-1.png)

1. Sélectionnez la version pour laquelle effectuer la comparaison, puis cliquez sur le bouton **Diff**.
1. Les différences entre la version actuelle et la version sélectionnée sont signalées de la façon suivante :

   * Le texte qui a été supprimé apparaît en rouge et barré.
   * Le texte qui a été ajouté apparaît en vert et en surbrillance.
   * Les images qui ont été ajoutées ou supprimées sont encadrées en vert.

   ![chlimage_1-75](assets/chlimage_1-75.png)

1. Dans le sidekick, sélectionnez le sous-onglet **Restaurer une version** et cliquez sur le bouton **&lt;&lt;Précédent** pour afficher la version actuelle.

## Distorsion du temps Timewarp {#timewarp}

La fonction de distorsion du temps Timewarp permet de simuler l’état ***publié*** d’une page à des moments spécifiques dans le passé.

L’objectif est de vous permettre d’effectuer le suivi du site web publié au moment sélectionné. Cette opération utilise les activations de pages pour déterminer l’état de l’environnement de publication.

Pour ce faire :

* Le système recherche la version de page qui était active à l’heure sélectionnée.
* Ceci signifie que la version affichée a été créée/activée *avant* l’heure sélectionnée dans Timewarp.
* Si vous accédez à une page qui a été supprimée, celle-ci sera également affichée, à condition toutefois que ses anciennes versions soient toujours disponibles dans le référentiel.
* Si aucune version publiée n’est disponible, Timewarp revient à l’état actuel de la page dans l’environnement de création (cela permet d’éviter une erreur 404 qui vous empêcherait de continuer à naviguer).

>[!NOTE]
>
>Si des versions sont supprimées du référentiel, la distorsion du temps n’est pas en mesure d’afficher la vue correcte. Si des éléments destinés au rendu du site web (tels que du code, des feuilles css et des images) ont été modifiés, la vue est différente de ce qu’elle était initialement, étant donné que ces éléments n’ont pas de contrôle de version dans le référentiel.

### Utiliser le calendrier Timewarp {#using-the-timewarp-calendar}

Timewarp est disponible à partir du sidekick.

La version calendrier sert à afficher un jour spécifique :

1. Ouvrez l’onglet **Contrôle de version**, puis cliquez sur **Timewarp** (près du bas du sidekick). La boîte de dialogue suivante s’affiche :

   ![chlimage_1-76](assets/chlimage_1-76.png)

1. À l’aide des sélecteurs de date et d’heure, spécifiez la date/l’heure de votre choix, puis cliquez sur **Ouvrir**.

   Timewarp affiche la page telle qu’elle était publiée avant/à la date choisie.

   >[!NOTE]
   >
   >Timewarp ne fonctionne entièrement que si vous avez publié la page précédemment. Dans le cas contraire, Timewarp affiche la page actuelle dans l’environnement de création.

   >[!NOTE]
   >
   >Si vous accédez à une page qui a été supprimée du référentiel, elle s’affiche correctement si d’anciennes versions sont toujours disponibles dans le référentiel.

   >[!NOTE]
   >
   >Vous ne pouvez pas modifier l’ancienne version de la page. Elle est disponible uniquement à des fins d’affichage. Si vous souhaitez restaurer l’ancienne version, vous pouvez procéder manuellement à l’aide de la fonction [Restaurer](/help/sites-classic-ui-authoring/classic-page-author-work-with-versions.md#restoring-a-page-version-from-sidekick).

1. Une fois la consultation de la page terminée, cliquez sur :

   * **Quitter Timewarp** pour quitter la fonctionnalité et revenir à la page de création en cours.
   * [Afficher la chronologie](#using-the-timewarp-timeline) pour afficher la chronologie.

   ![chlimage_1-77](assets/chlimage_1-77.png)

### Utiliser la frise chronologique de Timewarp {#using-the-timewarp-timeline}

La version de frise chronologique sert à afficher une vue d’ensemble des activités de publication sur la page.

Si vous souhaitez afficher la frise chronologique du document :

1. Pour afficher le journal, effectuez l’une des opérations suivantes :

   1. Ouvrez l’onglet **Contrôle de version**, puis cliquez sur **Distorsion du temps** (près du bas du sidekick).

   1. Utilisez la boîte de dialogue du sidekick qui s’affiche après avoir [utilisé le calendrier de Distorsion du temps](#using-the-timewarp-calendar).

1. Cliquez sur **Afficher le journal** : le journal du document s’affiche, par exemple :

   ![chlimage_1-78](assets/chlimage_1-78.png)

1. Pour naviguer dans la frise chronologique du document, procédez par glisser-déplacer.

   * Toutes les lignes indiquent les versions publiées.
Une nouvelle ligne commence lorsqu’une page est activée. Une nouvelle couleur apparaît chaque fois que le document est modifié.
Dans l’exemple ci-dessous, la ligne rouge indique que la page a été modifiée au cours de la période correspondant à la version verte initiale. La ligne jaune indique que la page a été modifiée pendant la version rouge, etc.

   ![chlimage_1-79](assets/chlimage_1-79.png)

1. Cliquez sur :

   1. Cliquez sur **Aller** pour afficher le contenu de la page publiée au moment sélectionné.
   1. Lorsque ce contenu s’affiche, utilisez **Quitter Timewarp** pour quitter la fonctionnalité et revenir à la page de création en cours.

### Limites du mode Timewarp {#timewarp-limitations}

Timewarp s’efforce de reproduire au mieux une page à un moment donné. Toutefois, en raison de la complexité de la création continue de contenu dans AEM, cela n’est pas toujours possible. Ces restrictions doivent être prises en compte lors de l’utilisation de Timewarp.

* **Timewarp fonctionne sur la base de pages publiées** : toutes les fonctionnalités de Timewarp ne sont disponibles que si vous avez publié la page précédemment. Dans le cas contraire, Timewarp affiche la page actuelle dans l’environnement de création.
* **Timewarp utilise des versions de page** : si vous accédez à une page qui a été supprimée du référentiel, elle s’affiche correctement si d’anciennes versions sont toujours disponibles dans le référentiel.
* **Les versions supprimées affectent Timewarp** : si des versions sont supprimées du référentiel, Timewarp n’est pas en mesure d’afficher la vue correcte.

* **Timewarp est en lecture seule** : vous ne pouvez pas modifier l’ancienne version de la page. Elle est disponible uniquement à des fins d’affichage. Si vous souhaitez restaurer l’ancienne version, vous devrez procéder manuellement à l’aide de la fonction [Restaurer](#main-pars-title-1).

* **Timewarp est uniquement basé sur le contenu de la page.** Si des éléments (tels que des ressources de code, css et d’image) pour le rendu du site web ont été modifiés, la vue diffère de ce qu’elle était initialement. En effet, ces éléments ne sont pas versionnés dans le référentiel.

>[!CAUTION]
>
>La distorsion du temps est conçue pour aider les auteurs et autrices à comprendre et à créer du contenu. Il ne s’agit pas d’un journal d’audit et il n’est pas destiné à des fins juridiques.
