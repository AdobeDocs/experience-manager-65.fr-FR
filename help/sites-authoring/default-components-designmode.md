---
title: Configuration de composants en mode de conception
seo-title: Configuration de composants en mode de conception
description: Configuration de composants en mode de conception
seo-description: 'null'
uuid: b9c9792d-4398-446d-8767-44d4e7ce9a2e
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 8ae6817a-16d3-4740-b67a-498e75adf350
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '911'
ht-degree: 83%

---


# Configuration de composants en mode de conception{#configuring-components-in-design-mode}

Lors de l’installation standard d’une instance AEM, plusieurs composants sont immédiatement disponibles dans l’explorateur de composants.

En outre, divers autres composants sont également disponibles. Vous pouvez utiliser le mode Création pour [activer/désactiver ces composants](#enable-disable-components). Une fois activé et situé sur votre page, vous pouvez ensuite utiliser le mode Création pour [configurer les aspects de la conception de composant](#configuring-the-design-of-a-component) en modifiant les paramètres d&#39;attribut.

>[!NOTE]
>
>Il convient de faire attention lors de la modification de ces composants. Les paramètres de conception font souvent partie intégrante du site web. Ils ne doivent donc être modifiés que par une personne disposant des privilèges et de l’expérience appropriés, généralement un administrateur ou un développeur. Pour plus d’informations, voir [Développement de composants](/help/sites-developing/components.md).

>[!NOTE]
>
>Le mode de conception est uniquement disponible pour les modèles statiques. Les modèles créés avec des modèles modifiables doivent être modifiés à l’aide de l’[éditeur de modèles](/help/sites-authoring/templates.md).

>[!NOTE]
>
>Le mode de conception est uniquement disponible pour les configurations de conception stockées en tant que contenu sous ( `/etc`).
>
>À partir de AEM 6.4, il est recommandé de stocker les conceptions en tant que données de configuration sous `/apps` pour prendre en charge les scénarios de déploiement continu. Les conceptions stockées sous `/apps` ne sont pas modifiables au moment de l’exécution et le mode de conception ne sera pas disponible pour les utilisateurs non administrateurs de ces modèles.

Pour ce faire, vous devrez ajouter ou supprimer les composants autorisés dans le système de paragraphes de la page. Le système de paragraphes (`parsys`) est un composant composite qui contient tous les autres composants de paragraphes. Il permet aux auteurs d’ajouter des composants de différents types à une page, car il contient tous les autres composants de paragraphes. Chaque type de paragraphe est représenté en tant que composant.

Par exemple, le contenu d’une page des produits peut contenir un système de paragraphes avec les éléments suivants :

* Une image du produit (sous la forme d’une image ou d’un paragraphe « textimage »)
* La description du produit (sous la forme d’un paragraphe de texte)
* Un tableau de données techniques (sous la forme d’un paragraphe de tableau)
* Un formulaire à remplir par les utilisateurs (sous la forme d’un paragraphe de début de formulaire, d’élément de formulaire et de fin de formulaire)

>[!NOTE]
>
>Reportez-vous aux sections [Développement de composants](/help/sites-developing/components.md) et [Consignes d’utilisation des modèles et des composants](/help/sites-developing/dev-guidelines-bestpractices.md#guidelines-for-using-templates-and-components) pour en savoir plus sur `parsys`.

>[!CAUTION]
>
>La modification de la conception en mode Création, telle que décrite dans cet article, est la méthode recommandée pour définir des conceptions de modèles statiques.
>
>La modification de conceptions dans CRX DE, par exemple, n’est pas recommandée et l’application de ces conceptions risque de provoquer un comportement imprévu. Pour plus d’informations, consultez le document [Modèles de page - Statiques](/help/sites-developing/page-templates-static.md#how-template-designs-are-applied), à l’attention du développeur.

## Activation/désactivation des composants {#enable-disable-components}

Pour activer ou désactiver un composant :

1. Sélectionnez le mode **Conception**.

   ![screen_shot_2018-03-22at103113](assets/screen_shot_2018-03-22at103113.png)

1. Appuyez ou cliquez sur un composant. Lorsqu’il est sélectionné, le composant présente une bordure bleue.

   ![screen_shot_2018-03-22at103204](assets/screen_shot_2018-03-22at103204.png)

1. Cliquez ou appuyez sur l&#39;icône **Parent**.

   ![](do-not-localize/screen_shot_2018-03-22at103204.png)

   Cela a pour effet de sélectionner le système de paragraphes contenant le composant actif.

1. L’icône **Configurer** du système de paragraphes s’affiche dans la barre d’outils du parent. 

   ![](do-not-localize/screen_shot_2018-03-22at103256.png)

   Sélectionnez cette icône pour afficher la boîte de dialogue.

1. Utilisez la boîte de dialogue pour définir les composants disponibles dans l’explorateur de composants lors de la modification de la page en cours.

   ![screen_shot_2018-03-22at103329](assets/screen_shot_2018-03-22at103329.png)

   La boîte de dialogue comporte deux onglets :

   * Composants autorisés
   * Paramètres

   **Composants autorisés**

   Dans l&#39;onglet **Composants autorisés**, vous définissez les composants disponibles pour le paramètre.

   * Les composants sont regroupés en groupes de composants, qui peuvent être développés et réduits.
   * Un groupe entier peut être sélectionné en cochant le nom du groupe, et tous peuvent être désélectionnés en décochant la case.
   * Le signe moins indique qu’au moins un élément du groupe est sélectionné, mais pas tous.
   * Un champ de recherche est disponible pour filtrer un composant en fonction de son nom.
   * Les chiffres à droite du nom du groupe de composants représentent le nombre total de composants sélectionnés dans ce groupe, quel que soit le filtre.

   La configuration s’effectue par composant de page. Si des pages enfants utilisent le même modèle et/ou composant de page (généralement aligné), la même configuration est appliquée au système de paragraphes correspondant.

   >[!NOTE]
   >
   >Les composants de formulaire adaptatif sont conçus pour fonctionner à l’intérieur du conteneur de formulaires adaptatifs afin de tirer parti de l’écosystème de formulaires. Ils doivent donc uniquement être utilisés dans l’éditeur de formulaires adaptatifs et ne fonctionneront pas dans l’éditeur de pages de sites.

   **Paramètres**

   L’onglet **Paramètres** vous permet de définir des options supplémentaires, par exemple dessiner une ancre pour chaque composant, et de définir la marge intérieure des cellules de chaque conteneur.

1. Sélectionnez **Terminé** pour enregistrer la configuration.

## Configuration de la conception d’un composant {#configuring-the-design-of-a-component}

1. Sélectionnez le mode **Conception**.

   ![screen_shot_2018-03-22at103113-1](assets/screen_shot_2018-03-22at103113-1.png)

1. Appuyez ou cliquez sur un composant avec une bordure bleue. Dans cet exemple, un composant d’image à forte identification est sélectionné.

   ![screen_shot_2018-03-22at103434](assets/screen_shot_2018-03-22at103434.png)

1. Utilisez l’icône **Configurer** pour ouvrir la boîte de dialogue.

   ![](do-not-localize/screen_shot_2018-03-22at103256-1.png)

   Dans la boîte de dialogue de conception, vous pouvez configurer le composant en fonction des paramètres de conception disponibles.

   ![screen_shot_2018-03-22at103530](assets/screen_shot_2018-03-22at103530.png)

   La boîte de dialogue comporte trois onglets :

   * Principal
   * Fonctions
   * Styles

   **Propriétés**

   L’onglet **Propriétés** vous permet de configurer les paramètres de conception importants du composant. Par exemple, pour un composant Image, vous pouvez définir la taille maximale et minimale de l’image autorisée.

   **Fonctionnalités**

   L’onglet **Fonctions** permet d’activer ou de désactiver des fonctions supplémentaires du composant. Par exemple, pour un composant Image, vous pouvez définir l’orientation de l’image, les options de recadrage disponibles, et si une image peut être téléchargée.

   **Styles**

   Dans l’onglet **Styles**, vous pouvez définir les styles et les classes CSS à utiliser avec le composant.

   ![screen_shot_2018-03-22at103741](assets/screen_shot_2018-03-22at103741.png)

   Utilisez le bouton **Ajouter** pour ajouter des entrées supplémentaires à la liste de dialogue à entrées multiples.

   ![chlimage_1-94](assets/chlimage_1-94.png)

   Utilisez l&#39;icône ** Supprimer **pour supprimer une entrée d&#39;une liste de dialogue à entrées multiples.

   ![](do-not-localize/screen_shot_2018-03-22at103809.png)

   Utilisez l’icône **Déplacer** pour réorganiser l’ordre des entrées dans une liste de dialogue à entrées multiples.

   ![](do-not-localize/screen_shot_2018-03-22at103816.png)

1. Appuyez ou cliquez sur l’icône **Terminé** pour enregistrer et fermer la boîte de dialogue.

