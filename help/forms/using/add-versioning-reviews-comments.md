---
title: Ajoutez des versions, des commentaires et des annotations au formulaire adaptatif AEM version 6.5.
description: Utilisez les composants principaux de formulaire adaptatif d’AEM 6.5 pour ajouter des commentaires, des annotations et des versions à un formulaire adaptatif.
feature: Adaptive Forms, Core Components
role: User, Developer, Admin
source-git-commit: a4e155de8a4f60d3746cecea110466b1d5d44dbb
workflow-type: tm+mt
source-wordcount: '625'
ht-degree: 0%

---

# Contrôle de version, révision et commentaires sur un formulaire adaptatif

<!--
<span class="preview"> This feature is under the Early Adopter Program. You can write to aem-forms-ea@adobe.com from your official email id to join the early adopter program and request access to the capability. </span>
-->

<span class="preview"> Cette fonctionnalité est fournie dans le cadre du programme d’adoption précoce. Si vous souhaitez participer à notre programme d&#39;accès anticipé pour cette fonctionnalité, envoyez un email depuis votre adresse officielle à aem-forms-ea@adobe.com pour demander l&#39;accès à </span>.

Les composants principaux de formulaire adaptatif permettent aux auteurs de formulaires d’ajouter des versions, des commentaires et des annotations aux formulaires. Ces fonctionnalités simplifient le développement de formulaires en permettant aux utilisateurs de créer et gérer plusieurs versions, de collaborer par le biais de commentaires et d’ajouter des notes à des sections de formulaire spécifiques, ce qui améliore l’expérience de création de formulaires.

## Prérequis {#prerequisite-versioning}

Pour utiliser les fonctions de contrôle de version, de commentaire et d’annotation dans un formulaire adaptatif, assurez-vous que les [composants principaux de formulaire adaptatif](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/adaptive-forms-core-components/enable-adaptive-forms-core-components) sont activés dans votre environnement Forms AEM 6.5.

## Contrôle de version des formulaires adaptatifs {#adaptive-form-versioning}

Le contrôle de version de formulaire adaptatif permet d’ajouter des versions à un formulaire. Les auteurs de formulaires peuvent facilement créer plusieurs versions d’un formulaire et enfin utiliser celle qui convient aux objectifs de l’entreprise. En outre, les utilisateurs de formulaires peuvent également rétablir les versions précédentes du formulaire. Cela permet également aux auteurs de comparer deux versions d’un formulaire en les prévisualisant, ce qui leur permet d’analyser les formulaires mieux du point de vue de l’interface utilisateur. Allons plus en détail pour chaque fonctionnalité de contrôle de version de formulaire adaptatif :

### Création d’une version de formulaire {#create-a-form-version}

Pour créer une version d’un formulaire, procédez comme suit :

1. Dans votre environnement AEM Forms, accédez au **[!UICONTROL formulaire]**&quot;**[!UICONTROL Forms et documents]** et sélectionnez votre **formulaire**.
1. Dans la liste déroulante de sélection du panneau de gauche, sélectionnez **[!UICONTROL Versions]**.
   ![Sélectionner un formulaire](assets/select-a-form.png)
1. Cliquez sur les **trois points** situés dans le panneau inférieur gauche, puis cliquez sur **[!UICONTROL Enregistrer comme version]**.
1. Attribuez un libellé à la version du formulaire. Vous pouvez également ajouter des informations sur le formulaire par le biais d’un commentaire.
   ![Créer une version de formulaire](assets/create-a-form-version.png)

### Mettre à jour une version de formulaire {#update-a-form-version}

Une fois le formulaire modifié et mis à jour, vous ajoutez une nouvelle version au formulaire. Suivez les étapes de la dernière section pour nommer une nouvelle version du formulaire, comme illustré dans l’image :

![Mettre à jour une version de formulaire](assets/update-a-form-version.png)

### Rétablissement d’une version de formulaire {#revert-a-form-version}

Pour rétablir la version précédente d’un formulaire, sélectionnez une version de formulaire, cliquez sur **[!UICONTROL Revenir à cette version]**.

![Rétablir la version de formulaire](assets/revert-form-version.png)

### Comparaison des versions de formulaire {#compare-form-versions}

Les auteurs de formulaires peuvent comparer deux versions différentes d’un formulaire à des fins d’aperçu. Pour comparer des versions, sélectionnez une version de formulaire et cliquez sur **[!UICONTROL Comparer à actuel]**. Il affiche deux versions de formulaire différentes en mode d’aperçu.

![Comparer des versions de formulaire](assets/compare-form-versions.png)

## Ajouter des commentaires {#add-comments}

Une révision est un mécanisme qui permet à un ou plusieurs réviseurs de commenter des formulaires. Tout utilisateur de formulaire peut commenter un formulaire ou le réviser au moyen de commentaires. Pour commenter un formulaire, sélectionnez un **[!UICONTROL formulaire]** et ajoutez un **[!UICONTROL commentaire]** au formulaire.

>[!NOTE]
> Lorsque vous utilisez des commentaires dans les composants principaux de formulaire adaptatif comme décrit ci-dessus, la fonctionnalité de formulaire, [l’ajout de réviseurs aux formulaires](/help/forms/using/create-reviews-forms.md), est désactivée.


![Ajouter des commentaires sur un formulaire](assets/form-comments.png)

## Ajout d’annotations {#adaptive-form-annotations}

Dans de nombreux cas, les utilisateurs d’un groupe de formulaires doivent ajouter des annotations à un formulaire à des fins de révision, par exemple sur un onglet ou des composants spécifiques d’un formulaire. Dans ce cas, les auteurs peuvent utiliser des annotations.
Pour ajouter des annotations à un formulaire, procédez comme suit :

1. Ouvrez un formulaire en mode **[!UICONTROL Modifier]** .

1. Cliquez sur l’icône **ajouter** située dans le rail supérieur droit comme indiqué dans l’image.
   ![Annotation](assets/annotation.png)

1. Cliquez maintenant sur l’icône **Ajouter** située dans le rail supérieur gauche comme indiqué dans l’image pour ajouter l’annotation.
   ![Ajouter une annotation](assets/add-annotation.png)

1. Vous pouvez désormais ajouter des commentaires, dessiner des esquisses de plusieurs couleurs pour former des composants.

1. Pour afficher toutes les annotations ajoutées à un formulaire, sélectionnez le formulaire. Vous verrez que les annotations ajoutées dans le panneau de gauche sont affichées dans l’image.

   ![Voir annotations ajoutées](assets/see-annotations.png)

## Voir également

* [Comparaison des composants principaux de Forms adaptatif](/help/forms/using/compare-forms-core-components.md)
