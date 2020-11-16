---
title: Espaces et entités
seo-title: Développement des services de contenu AEM Mobile
description: Cette page sert de landing page pour le développement de AEM Mobile Content Services.
seo-description: Cette page sert de landing page pour le développement de AEM Mobile Content Services.
uuid: eab5a61b-a9e8-4863-90a3-df1f18510cd8
contentOwner: Jyotika Syal
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
discoiquuid: ef568577-c74e-4fc2-b66e-eedac2948310
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1209'
ht-degree: 4%

---


# Espaces et entités{#spaces-and-entities}

>[!NOTE]
>
>Adobe recommande d’utiliser l’éditeur d’application d’une seule page (SPA) pour les projets nécessitant un rendu côté client basé sur la structure SPA (par exemple, React). [En savoir plus](/help/sites-developing/spa-overview.md).

Un espace est un emplacement pratique pour stocker les entités exposées via l’API REST de Content Services. Cela est particulièrement utile car une application (ou tout canal) peut être associée à de nombreuses entités. Obliger les entités à se trouver dans un espace force la meilleure pratique de regroupement des exigences d’une application. Vous pouvez éventuellement associer une application AEM à un petit nombre d’espaces.

>[!NOTE]
>
>Pour mettre à la disposition de n’importe quel canal de Content Services, il doit se trouver sous un espace.

## Création d’un espace {#creating-a-space}

Si l’utilisateur souhaite exposer un ensemble de contenu et de ressources à une application mobile, il crée l’espace à l’aide du tableau de bord AEM Mobile.

Pour la première fois, si un utilisateur n’a pas configuré les services de contenu pour qu’ils fonctionnent avec des espaces, le tableau de bord AEM Mobile affiche uniquement les applications après avoir sélectionné **Content Services**.

>[!CAUTION]
>
>**Conditions préalables à l’ajout d’un espace**
>
>Cochez la case **Activer AEM Content Services** pour utiliser les espaces et activez-la dans votre tableau de bord d’applications AEM Mobile.
>
>Voir [Administration de Content Services](/help/mobile/developing-content-services.md) pour plus d’informations.

Une fois que vous avez configuré les espaces dans le tableau de bord, procédez comme suit pour créer des espaces :

1. Sélectionnez **Espaces** dans Content Services.

   ![chlimage_1-83](assets/chlimage_1-83.png)

1. Choisissez **Créer** pour créer un espace. Saisissez **Titre**, **Nom** et **Description** pour l’espace.

   Cliquez sur **Créer**.

   ![chlimage_1-84](assets/chlimage_1-84.png)

## Gestion d&#39;un espace {#managing-a-space}

Une fois que vous avez créé un espace, cliquez sur à gauche pour le gérer dans la liste.

Vous pouvez vue les propriétés de l’espace, supprimer l’espace ou publier l’espace et son contenu sur une instance de publication AEM.

![chlimage_1-85](assets/chlimage_1-85.png)

**Affichage et modification des propriétés d&#39;un espace**

1. Sélectionner l&#39;espace dans la liste
1. Choose **Properties** from the toolbar
1. Click **Close** when done

**Publication d&#39;un espace** Lorsqu&#39;un espace est publié, tous les dossiers et entités de cet espace sont également publiés.

1. Sélectionnez l&#39;espace en cliquant sur son icône dans la liste de la console Espace
1. Choisir **l’arborescence de publication**

>[!NOTE]
>
>Vous pouvez **annuler la publication** d’un espace qui supprime l’espace de l’instance de publication.
>
>L’image suivante illustre les actions qui peuvent être effectuées après la publication de l’espace.

![chlimage_1-86](assets/chlimage_1-86.png)

## Utilisation de dossiers dans un espace {#working-with-folders-in-a-space}

Les espaces peuvent inclure des dossiers pour mieux organiser le contenu et les ressources de l’espace. Les utilisateurs peuvent créer leur propre hiérarchie sous un espace.

### Création d’un dossier {#creating-a-folder}

1. Cliquez sur l’espace de la liste dans la console de l’espace et cliquez sur **Créer un dossier.**

   ![chlimage_1-87](assets/chlimage_1-87.png)

1. Saisissez le **titre**, le **nom** et la **description** du dossier.

   ![chlimage_1-88](assets/chlimage_1-88.png)

1. Cliquez sur **Créer** pour créer le dossier dans un espace

## Copie de la langue {#language-copy}

>[!CAUTION]
>
>La copie de langue n’est pas entièrement fonctionnelle dans cette version. Il ne fait que mettre en place la structure.

La fonction Copie **de** langue permet aux auteurs de copier leur copie de langue principale, puis de créer un projet et un flux de travail pour traduire automatiquement le contenu. La copie de langue crée la structure correcte. Une fois que vous avez ajouté un dossier dans un espace, vous pouvez ajouter la copie de langue à votre espace.

>[!NOTE]
>
>Il est recommandé de placer tout contenu pouvant être traduit sous le noeud Copie de langue.

### Ajouter la copie de langue {#adding-language-copy}

1. Une fois l&#39;espace créé, cliquez sur cet espace pour créer une copie de langue.

   Cliquez sur **Créer** , puis sélectionnez Copie **** de langue.

   ![chlimage_1-89](assets/chlimage_1-89.png)

   >[!NOTE]
   >
   >Les noeuds de copie de langue ne peuvent exister qu’en tant qu’enfant direct de l’espace.

1. Sélectionnez **Content Package Language&amp;amp ; ast ;** et saisissez **Title&amp;amp ; ast ;** dans la boîte de dialogue **Créer une copie** de langue.

   Cliquez sur **Créer**.

   ![chlimage_1-90](assets/chlimage_1-90.png)

1. Une fois que vous avez créé une copie de langue, elle apparaît dans votre espace dans les Principal **** linguistiques.

   ![chlimage_1-91](assets/chlimage_1-91.png)

   >[!NOTE]
   >
   >Sélectionnez Principal **** linguistiques pour vue des dossiers de copie de langue.

### Suppression d&#39;un dossier de l&#39;espace {#removing-a-folder-from-the-space}

1. Sélectionner le dossier à partir de la liste du contenu de l&#39;espace
1. Click **Delete** from the toolbar

   >[!NOTE]
   >
   >Pour naviguer dans un dossier et voir son contenu ou ajouter un sous-dossier ou une entité, cliquez sur le titre du dossier dans la liste de contenu de l’espace.

## Utilisation d&#39;entités dans un espace {#working-with-entities-in-a-space}

Les entités représentent le contenu exposé par le biais du point de terminaison du service Web. Les entités sont stockées dans des espaces afin de pouvoir les trouver facilement et de rester indépendantes de la structure de référentiel AEM qui contient leur contenu associé.

Vous pouvez regrouper des entités dans un regroupement logique. Pour ce faire, vous pouvez créer n’importe quel nombre de dossiers.

Si des enfants d’entité, qui sont d’autres entités, sont rassemblés pour la modélisation des données, l’utilisateur développeur peut créer des &quot;modèles de groupe&quot; spécifiques à partir du type de modèle &quot;Groupe d’entités&quot;, fournis prêts à l’emploi.

>[!NOTE]
>
>Les entités sont toujours associées à un espace ; la plupart de l’interface utilisateur de l’entité est donc accessible via la console d’espace.

### Création d&#39;une entité {#creating-an-entity}

1. Ouvrez la console Espace et cliquez sur le titre de l&#39;espace.

   Vous pouvez éventuellement accéder au dossier en cliquant sur le titre du dossier dans la liste.

   ![chlimage_1-92](assets/chlimage_1-92.png)

1. Sélectionnez le modèle de l&#39;entité. Il s&#39;agit du type d&#39;entité que vous souhaitez créer. Cliquez sur Suivant.

   ![chlimage_1-93](assets/chlimage_1-93.png)

   >[!NOTE]
   >
   >Vous avez la possibilité de choisir le modèle **** Ressources, le modèle **** Pages ou un modèle de type d’entité que vous avez créé auparavant.
   >
   >Voir [Création d&#39;un modèle](/help/mobile/administer-mobile-apps.md)pour créer votre entité personnalisée.

1. Saisissez un **titre**, un **nom**, une **description** et des **balises pour l&#39;entité.** Cliquez sur **Créer**.

   ![chlimage_1-94](assets/chlimage_1-94.png)

   Une fois que vous avez terminé, l&#39;entité s&#39;affiche dans les descendants de votre espace.

### Modification d&#39;une entité {#editing-an-entity}

1. Une fois que vous avez créé une entité, accédez à votre dossier ou espace et choisissez votre entité dans la console Espace pour la modifier.

   ![chlimage_1-95](assets/chlimage_1-95.png)

1. Sélectionnez une entité à modifier, puis cliquez sur **Modifier**.

   ![chlimage_1-96](assets/chlimage_1-96.png)

   >[!CAUTION]
   >
   >Selon le modèle que vous choisissez de créer votre entité, l&#39;interface utilisateur sera différente pour les deux, pour la modification et l&#39;affichage des propriétés de votre entité. Pour plus de détails, voir les étapes ci-dessous.

   ***Si vous choisissez le modèle de création de l&#39;entité en tant que modèles*** d&#39;actifs, le fait de cliquer sur **Modifier** vous permet d&#39;ajouter des actifs comme illustré dans la figure ci-dessous :

   ![chlimage_1-97](assets/chlimage_1-97.png)

   Vous pouvez également cliquer sur **Prévisualisation** pour vue du lien json.

   ![chlimage_1-98](assets/chlimage_1-98.png)

   ***Si vous choisissez le modèle de création de l&#39;entité en tant que modèles*** de pages, le fait de cliquer sur **Modifier** vous permet d&#39;ajouter des actifs comme illustré dans la figure ci-dessous :

   ![chlimage_1-99](assets/chlimage_1-99.png)

   Cliquez sur l’icône du **chemin** pour ajouter un fichier.

   ![chlimage_1-100](assets/chlimage_1-100.png)

   >[!NOTE]
   >
   >Une fois que vous avez ajouté une entité, elle doit être enregistrée pour que le lien de la Prévisualisation fonctionne. Pour vue à la prévisualisation, cliquez sur **Enregistrer**. Cliquez sur la **Prévisualisation** pour afficher le fichier json de la ressource ajoutée, comme illustré dans la figure ci-dessous :

   ![chlimage_1-101](assets/chlimage_1-101.png)

   >[!NOTE]
   >
   >Lorsque vous avez terminé d&#39;ajouter des actifs à votre entité, vous pouvez choisir **Enregistrer** pour enregistrer les modifications ou choisir **Enregistrer et fermer** pour enregistrer et rediriger vers la liste de console Space où les entités sont définies.

   De plus, sélectionnez une entité dans la liste de la console d&#39;espace et cliquez sur **Propriétés** pour la vue et modifiez les propriétés d&#39;une entité définie.

   ![chlimage_1-102](assets/chlimage_1-102.png)

   Vous pouvez modifier le titre, la description, les balises et ajouter les actifs à votre entité.

   ![chlimage_1-103](assets/chlimage_1-103.png)

### Suppression d&#39;une entité {#removing-an-entity}

1. Sélectionner l&#39;entité à partir de la liste du contenu de l&#39;espace

   ![chlimage_1-104](assets/chlimage_1-104.png)

1. Cliquez sur **Supprimer** de la barre d&#39;outils pour supprimer l&#39;entité spécifique de l&#39;espace.

### Publication d&#39;une entité {#publishing-an-entity}

Vous avez la possibilité de choisir **Publier l’arborescence** ou Publier **** rapidement pour publier votre entité.

1. Sélectionnez une entité dans la liste de la console d&#39;espace et cliquez sur **Publier l&#39;arborescence **pour publier cette entité et ses enfants.

   ![chlimage_1-105](assets/chlimage_1-105.png)

   **Ou**,

   Cliquez sur Publication **** rapide pour publier cette entité spécifique.
