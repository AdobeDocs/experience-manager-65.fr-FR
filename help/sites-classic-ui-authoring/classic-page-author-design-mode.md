---
title: Configurer des composants en mode de conception
description: Lorsque l’instance d’AEM est installée telle quelle, plusieurs composants sont immédiatement disponibles dans le sidekick. En outre, divers autres composants sont également disponibles. Vous pouvez utiliser le mode de conception pour activer/désactiver ces composants.
uuid: 2cd5dad0-2f9c-4f34-aae8-1638d1445eb3
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 10466b49-f8bd-4c2c-8106-b0c7ba054989
docset: aem65
exl-id: cb2d2d0d-feb4-4b89-8325-80f735816904
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: ht
source-wordcount: '500'
ht-degree: 100%

---

# Configurer des composants en mode de conception{#configuring-components-in-design-mode}

Lorsque l’instance d’AEM est installée telle quelle, plusieurs composants sont immédiatement disponibles dans le sidekick.

D’autres composants sont également disponibles. Vous pouvez utiliser le mode de conception pour [activer/désactiver ces composants](#enabledisablecomponentsusingdesignmode). Une fois ces composants activés et situés sur votre page, utilisez le mode de conception pour [configurer différents aspects de la conception](#configuringcomponentsusingdesignmode) en modifiant les paramètres d’attribut.

>[!NOTE]
>
>Soyez prudent lors de la modification de ces composants. Les paramètres de conception font souvent partie intégrante du site web. Ils ne doivent donc être modifiés que par une personne disposant des privilèges (et de l’expérience) appropriés, généralement un administrateur ou un développeur. Pour plus d’informations, reportez-vous à la section [Développement de composants](/help/sites-developing/components.md).

Pour ce faire, vous devrez en réalité ajouter ou supprimer les composants autorisés dans le système de paragraphes de la page. Le système de paragraphes (`parsys`) est un composant composite qui contient tous les autres composants de paragraphes. Le système de paragraphes permet aux auteurs ou autrices d’ajouter des composants de différents types à une page, car il contient tous les autres composants de paragraphe. Chaque type de paragraphe est représenté en tant que composant.

Par exemple, le contenu d’une page produit peut contenir un système de paragraphes contenant les éléments suivants :

* Une image du produit (sous la forme d’une image ou d’un paragraphe textimage)
* La description du produit (sous forme de paragraphe de texte)
* Un tableau contenant des données techniques (sous la forme d’un paragraphe de tableau)
* Un formulaire rempli par les utilisateurs et utilisatrices (au début du formulaire, à l’élément de formulaire et au paragraphe de fin du formulaire)

>[!NOTE]
>
>Reportez-vous aux sections [Développement de composants](/help/sites-developing/components.md#paragraphsystem) et [Consignes d’utilisation des modèles et des composants](/help/sites-developing/dev-guidelines-bestpractices.md#guidelines-for-using-templates-and-components) pour en savoir plus sur `parsys`.

## Activer/désactiver des composants {#enable-disable-components}

En mode de conception, le sidekick est réduit et vous avez la possibilité de configurer les composants accessibles pour la création :

1. Pour passer en mode de conception, ouvrez une page à modifier et cliquez sur l’icône du sidekick :

   ![](do-not-localize/chlimage_1.png)

1. Cliquez sur **Modifier** dans le système de paragraphes (**Conception de paragraphe**).

   ![screen_shot_2012-02-08at102726am](assets/screen_shot_2012-02-08at102726am.png)

1. Une boîte de dialogue s’ouvre, répertoriant les groupes de composants affichés dans le sidekick, ainsi que les composants individuels qu’ils contiennent.

   Sélectionnez les composants à ajouter ou à supprimer dans le sidekick.

   ![screen_shot_2012-02-08at103407am](assets/screen_shot_2012-02-08at103407am.png)

1. Le sidekick se réduit en mode de conception. En cliquant sur la flèche, vous pouvez agrandir le sidekick et revenir au mode d’édition :

   ![](do-not-localize/sidekick-collapsed.png)

## Configurer la conception d’un composant {#configuring-the-design-of-a-component}

En mode de conception, vous pouvez également configurer des attributs pour les composants individuels. Chaque composant possède ses propres paramètres. L’exemple suivant illustre le composant **Image** :

1. Pour passer en mode de conception, ouvrez une page à modifier et cliquez sur l’icône du sidekick :

   ![](do-not-localize/chlimage_1-1.png)

1. Vous pouvez configurer la conception des composants.

   Par exemple, si vous cliquez sur **Modifier** sur le composant Image (**Conception d’image**), vous pouvez configurer les paramètres spécifiques au composant :

   ![chlimage_1-5](assets/chlimage_1-5.png)

1. Cliquez sur **OK** pour enregistrer vos modifications.

1. Le sidekick se réduit en mode de conception. En cliquant sur la flèche, vous pouvez agrandir le sidekick et revenir au mode d’édition :

   ![](do-not-localize/sidekick-collapsed-1.png)
