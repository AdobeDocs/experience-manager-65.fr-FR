---
title: Configuration des composants par défaut en mode de conception
description: Configuration des composants Adobe Experience Manager en mode de conception.
exl-id: 5e232886-75c1-4f0f-b359-4739ae035fd3
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User,Admin,Developer
source-git-commit: c77849740fab51377ce60aff5f611e0408dca728
workflow-type: tm+mt
source-wordcount: '905'
ht-degree: 100%

---

# Configuration des composants par défaut en mode de conception{#configuring-components-in-design-mode}

Pour les installations prêtes à l’emploi de l’instance d’AEM, une sélection de composants est immédiatement disponible dans l’explorateur de composants.

D’autres composants sont également disponibles. Vous pouvez utiliser le mode de conception pour [activer/désactiver ces composants](#enable-disable-components). Une fois ces composants activés et situés sur votre page, utilisez le mode de conception pour [configurer différents aspects de la conception](#configuring-the-design-of-a-component) en modifiant les paramètres d’attribut.

>[!NOTE]
>
>La modification de ces composants doit être effectuée avec soin. Les paramètres de conception font souvent partie intégrante de la conception de l’ensemble du site web. Ils ne doivent donc être modifiés que par une personne disposant des privilèges et de l’expérience appropriés, souvent un administrateur ou une administratrice ou un développeur ou une développeuse. Pour plus d’informations, consultez [Développement de composants](/help/sites-developing/components.md).

>[!NOTE]
>
>Le mode de conception n’est disponible que pour les modèles statiques. Les modèles créés avec des modèles modifiables doivent être modifiés à l’aide de l’[éditeur de modèles](/help/sites-authoring/templates.md).

>[!NOTE]
>
>Le mode de conception est uniquement disponible pour les configurations de conception stockées en tant que contenu sous (`/etc`).
>
>À partir d’AEM 6.4, il est recommandé de stocker les conceptions en tant que données de configuration sous `/apps` pour prendre en charge les scénarios de déploiement continus. Les conceptions stockées sous `/apps` ne sont pas modifiables à l’exécution, et les utilisateurs non administrateurs n’auront pas accès au mode de conception pour les modèles en question.

Pour ce faire, vous devrez ajouter ou supprimer les composants autorisés dans le système de paragraphes de la page. Le système de paragraphes (`parsys`) est un composant composite qui contient tous les autres composants de paragraphes. Le système de paragraphes permet aux auteurs ou autrices d’ajouter des composants de différents types à une page, car il contient tous les autres composants de paragraphe. Chaque type de paragraphe est représenté en tant que composant.

Par exemple, le contenu d’une page produit peut contenir un système de paragraphes contenant les éléments suivants :

* Une image du produit (sous la forme d’une image ou d’un paragraphe textimage)
* La description du produit (sous forme de paragraphe de texte)
* Un tableau contenant des données techniques (sous la forme d’un paragraphe de tableau)
* Un formulaire rempli par les utilisateurs et utilisatrices (au début du formulaire, à l’élément de formulaire et au paragraphe de fin du formulaire)

>[!NOTE]
>
>Reportez-vous aux sections [Développement de composants](/help/sites-developing/components.md) et [Consignes d’utilisation des modèles et des composants](/help/sites-developing/dev-guidelines-bestpractices.md#guidelines-for-using-templates-and-components) pour en savoir plus sur `parsys`.

>[!CAUTION]
>
>La modification de la conception en mode Création, telle que décrite dans cet article, est la méthode recommandée pour définir des conceptions de modèles statiques.
>
>La modification de conceptions dans CRX DE, par exemple, n’est pas recommandée, car l’application de ces conceptions risque de provoquer un comportement imprévu. Pour plus d’informations, consultez le document [Modèles de page - Statiques](/help/sites-developing/page-templates-static.md#how-template-designs-are-applied), à l’attention du développeur.

## Activer/désactiver des composants {#enable-disable-components}

Pour activer ou désactiver un composant :

1. Sélectionnez le mode **Conception**.

   ![screen_shot_2018-03-22at103113](assets/screen_shot_2018-03-22at103113.png)

1. Cliquez sur un composant. Une bordure bleue apparaît autour du composant lorsqu’il est sélectionné.

   ![screen_shot_2018-03-22at103204](assets/screen_shot_2018-03-22at103204.png)

1. Cliquez sur l’icône **Parent**.

   ![Parent](do-not-localize/screen_shot_2018-03-22at103204.png)

   Cette action a pour effet de sélectionner le système de paragraphes contenant le composant actif.

1. L’icône **Configurer** du système de paragraphes s’affiche dans la barre d’actions du parent.

   ![Configurer](do-not-localize/screen_shot_2018-03-22at103256.png)

   Sélectionnez cette icône pour afficher la boîte de dialogue.

1. Utilisez la boîte de dialogue pour définir les composants disponibles dans l’explorateur de composants lors de la modification de la page en cours.

   ![screen_shot_2018-03-22at103329](assets/screen_shot_2018-03-22at103329.png)

   La boîte de dialogue comporte deux onglets :

   * Composants autorisés
   * Paramètres

   **Composants autorisés**

   Dans l’onglet **Composants autorisés**, vous définissez les composants disponibles pour le système de paragraphes (parsys).

   * Les composants sont regroupés par groupes de composants, qui peuvent être développés et réduits.
   * Vous pouvez sélectionner un groupe entier en cochant le nom du groupe et tout peut être désélectionné en décochant la case.
   * Un signe moins représente au moins un élément, mais tous les éléments d’un groupe ne sont pas sélectionnés.
   * Une recherche est disponible pour filtrer un composant par nom.
   * Les nombres répertoriés à droite du nom du groupe de composants représentent le nombre total de composants sélectionnés dans ces groupes, quel que soit le filtre.

   Vous définissez la configuration par composant de page. Si les pages enfants utilisent le même modèle et/ou composant de page (généralement aligné), la même configuration est appliquée au système de paragraphes correspondant.

   >[!NOTE]
   >
   >Les composants de formulaires adaptatifs sont conçus pour fonctionner dans le conteneur de formulaires adaptatifs afin de tirer profit de l’écosystème Forms. Par conséquent, ces composants doivent être utilisés uniquement dans l’éditeur de formulaires adaptatifs et ne fonctionneront pas dans l’éditeur de page Sites.

   **Paramètres**

   Sur l’onglet **Paramètres**, vous pouvez définir d’autres options telles que dessiner une ancre pour chaque composant et définir la dilatation des cellules de chaque conteneur.

1. Sélectionnez **Terminé** pour enregistrer la configuration.

## Configuration de la conception d’un composant {#configuring-the-design-of-a-component}

1. Sélectionnez le mode **Conception**.

   ![screen_shot_2018-03-22at103113-1](assets/screen_shot_2018-03-22at103113-1.png)

1. Cliquez sur un composant avec une bordure bleue. Dans cet exemple, un composant d’image principale est sélectionné.

   ![screen_shot_2018-03-22at103434](assets/screen_shot_2018-03-22at103434.png)

1. Utilisez l’icône **Configurer** pour ouvrir la boîte de dialogue.

   ![Icône de configuration](do-not-localize/screen_shot_2018-03-22at103256-1.png)

   Dans la boîte de dialogue de conception, vous pouvez configurer le composant en fonction des paramètres de conception disponibles.

   ![screen_shot_2018-03-22at103530](assets/screen_shot_2018-03-22at103530.png)

   La boîte de dialogue se compose de trois onglets :

   * Principal
   * Fonctions
   * Styles

   **Propriétés**

   L’onglet **Propriétés** vous vous permet de configurer les paramètres de conception importants du composant. Par exemple, pour un composant d’image, vous pouvez définir la taille maximale et minimale autorisée de l’image.

   **Fonctionnalités**

   L’onglet **Fonctions** vous permet d’activer ou de désactiver des fonctionnalités supplémentaires du composant. Par exemple, pour un composant d’image, vous pouvez définir l’orientation de l’image, les options de recadrage disponibles et si une image peut être téléchargée.

   **Styles**

   L’onglet **Styles** vous permet de définir les classes et les styles CSS à utiliser avec le composant.

   ![screen_shot_2018-03-22at103741](assets/screen_shot_2018-03-22at103741.png)

   Utilisez le bouton **Ajouter** pour ajouter des entrées supplémentaires à la liste de dialogue à entrées multiples.

   ![Ajouter une entrée supplémentaire](assets/chlimage_1-94.png)

   Utilisez l’icône **Supprimer** pour supprimer une entrée de liste de boîte de dialogue à entrées multiples.

   ![Supprimer](do-not-localize/screen_shot_2018-03-22at103809.png)

   Utilisez l’icône **Déplacer** pour réorganiser l’ordre des entrées dans une liste de boîte de dialogue à entrées multiples.

   ![Déplacer](do-not-localize/screen_shot_2018-03-22at103816.png)

1. Cliquez sur l’icône **Terminé** pour enregistrer et fermer la boîte de dialogue.
