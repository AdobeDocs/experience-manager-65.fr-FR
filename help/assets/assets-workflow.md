---
title: Traiter les ressources pour exécuter les processus d’entreprise, effectuer des audits, assurer la conformité et maintenir une intégrité de base
description: Traitement des ressources pour convertir des formats, créer des rendus, gérer des ressources, valider des ressources et exécuter des  de.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 82ed39dac05591b9bdc9fda101ed450c2096dc60

---


# Traiter les fichiers numériques {#process-assets}

[!DNL Adobe Experience Manager Assets] vous permet de travailler sur vos ressources numériques de plusieurs manières afin de permettre un traitement robuste des ressources. Vous pouvez utiliser les méthodes de traitement par défaut ou personnalisées pour assurer l’achèvement des processus d’entreprise de bout en bout, les audits et la conformité, la découverte et la distribution, ainsi que l’intégrité de base de vos ressources numériques. Vous pouvez exécuter le de gestion des ressources tout en atteignant l’échelle et la personnalisation requises.

## Comprendre les {#understand-workflows}

Pour le traitement des ressources, [!DNL Experience Manager] utilise des .  aider à automatiser la logique métier ou . Les étapes granulaires permettant d’accomplir des  spécifiques sont fournies par défaut et les développeurs peuvent créer leurs propres étapes personnalisées. Ces étapes peuvent être combinées dans un ordre logique pour créer des  de. Par exemple, un flux de travail peut appliquer un filigrane aux images téléchargées en fonction d’un critère spécifique, tel que le dossier dans lequel elles sont téléchargées, la résolution de l’image, etc. Un autre exemple est un flux de travail configuré pour le filigrane et qui permet simultanément d’ajouter des métadonnées, de créer des rendus, d’ajouter des balises intelligentes et de publier du contenu dans une banque de données.

##  par défaut disponible dans [!DNL Experience Manager]{#default-workflows}

Par défaut, toutes les ressources téléchargées sont traitées à l’aide du processus [!UICONTROL DAM Update Asset] . Le flux de travail s’exécute pour chaque ressource téléchargée et effectue des de gestion des ressources de base, tels que la génération de rendus, l’écriture différée des métadonnées, les  de page, les de médias, leet le transcodage.

Pour afficher les différents modèles de flux de travail disponibles par défaut, voir **[!UICONTROL Outils > Processus > Modèles]** dans [!DNL Experience Manager].

![Certains flux de travaux par défaut](assets/aem-default-workflows.png)

*Figure : Certains flux de travaux par défaut disponibles dans[!DNL Experience Manager]*

## Apply workflows to process assets {#applying-workflows-to-assets}

L’application de workflow aux ressources numériques est identique à l’application de workflow aux pages d’un site web. For a complete guide on how to create and use workflows, see [start workflows](/help/sites-authoring/workflows-participating.md).

Utilisez les workflows dans les ressources numériques pour activer les ressources ou créer des filigranes. La plupart des workflow destinés aux ressources sont automatiquement activés, comme le workflow permettant de créer automatiquement un rendu après la modification d’une image.

>[!NOTE]
>
>If a workflow available in Classic UI is not available in Touch enabled UI, like [!UICONTROL Request to Activate] and [!UICONTROL Request to Deactivate], see [make workflow models](/help/sites-developing/workflows-models.md#classic2touchui).

## Application d’un workflow à une ressource {#apply-a-workflow-to-an-asset}

<!-- 
TBD: Add animated GIF for these steps instead of all these screenshots.
-->
Pour appliquer un processus à une ressource, procédez comme suit :

1. Accédez à l’emplacement de la ressource pour laquelle vous souhaitez un flux de travail, puis cliquez sur la ressource pour ouvrir la page de la ressource. Sélectionnez **[!UICONTROL Chronologie]** dans le menu pour afficher la chronologie.

   ![chronologie-1](assets/timeline.png)

1. Click **[!UICONTROL Actions]** at the bottom to open the list of actions available for the asset.

1. Click **[!UICONTROL Start Workflow]** from the list.

1. Dans la section **[!UICONTROL Démarrer le workflow]**, sélectionnez un modèle de workflow dans la liste.

   ![chlimage_1-254](assets/chlimage_1-50.png)

1. (Facultatif) Spécifiez un titre pour le flux de travaux qui peut être utilisé pour référencer l’instance du flux de travaux.

   ![chlimage_1-255](assets/chlimage_1-51.png)

1. Click **[!UICONTROL Start]** and then click **[!UICONTROL Proceed]**. Chaque étape du workflow s’affiche en tant qu’événement dans la chronologie.

   ![chlimage_1-256](assets/chlimage_1-52.png)

## Application d’un workflow à plusieurs ressources {#applying-a-workflow-to-multiple-assets}

1. Dans la console Ressources, accédez à l’emplacement des ressources pour lesquelles vous souhaitez démarrer un workflow, puis sélectionnez les ressources. Sélectionnez **[!UICONTROL Chronologie]** dans le menu pour afficher la chronologie.

   ![screen_shot_2019-03-06at123325pm](assets/chlimage_1-136.png)

1. Cliquez sur **[!UICONTROL Actions]** dans la partie inférieure.

   ![chlimage_1-30](assets/chlimage_1-137.png)

1. Cliquez sur **[!UICONTROL Démarrer le workflow]**. Dans la section **[!UICONTROL Démarrer le workflow]**, sélectionnez un modèle de workflow dans la liste.

   ![chlimage_1-31](assets/chlimage_1-138.png)

1. (Facultatif) Spécifiez le titre du workflow, qui peut permettre de référencer l’instance du workflow.
1. Cliquez sur **[!UICONTROL Démarrer]**, puis sur **[!UICONTROL Confirmer]** dans la boîte de dialogue. Le workflow s’exécute sur toutes les ressources sélectionnées.

## Application d’un workflow à plusieurs dossiers {#applying-a-workflow-to-multiple-folders}

La procédure à suivre pour appliquer un workflow à plusieurs dossiers est similaire à celle observée permettant d’appliquer un workflow à plusieurs ressources. Select the folders in the [!DNL Assets] interface, and perform steps 2-7 of the procedure [apply a workflow to multiple assets](/help/assets/assets-workflow.md#applying-a-workflow-to-multiple-assets).

## Apply a workflow to a collection {#applying-a-workflow-to-a-collection}

Voir [Application d’un processus à une collection](/help/assets/managing-collections-touch-ui.md#running-a-workflow-on-a-collection).

## automatique d’un flux de travail pour traiter les ressources de manière conditionnelle {#auto-execute-workflow-on-some-assets}

Les administrateurs peuvent configurer le processus pour exécuter et traiter automatiquement les ressources en fonction de conditions prédéfinies. Cette fonctionnalité est utile aux utilisateurs et aux marketeurs de la ligne de conduite, par exemple, pour créer un flux de travail personnalisé sur des dossiers spécifiques. Supposons que tous les fichiers de la photographie d&#39;une agence peuvent être marqués d&#39;un filigrane ou que tous les fichiers téléchargés par un indépendant puissent être traités pour créer des rendus spécifiques.

Pour un modèle de processus, les utilisateurs peuvent créer un lanceur de processus qui l’exécute. Un lanceur de processus surveille les modifications dans le référentiel de contenu et exécute le processus lorsque les conditions prédéfinies sont remplies. Les administrateurs peuvent donner accès aux spécialistes du marketing pour créer le  du et configurer le lanceur. Les utilisateurs peuvent modifier le flux de travail [!UICONTROL DAM Update Asset] par défaut pour ajouter les étapes supplémentaires requises pour traiter des ressources spécifiques. Le processus s’exécute sur tous les fichiers nouvellement transférés. Utilisez l’une des méthodes suivantes pour limiter l’exécution des étapes supplémentaires sur des ressources spécifiques :

* Effectuez une copie du flux de travail [!UICONTROL DAM Update Asset] et modifiez-le pour l’exécuter sur une hiérarchie de dossiers spécifique. Cette approche est utile pour quelques dossiers.
* Les étapes de traitement supplémentaires peuvent être ajoutées à l’aide d’un fractionnement [OU](/help/sites-developing/workflows-step-ref.md#or-split) applicable de manière conditionnelle au plus grand nombre de dossiers requis.

>[!MORELIKETHIS]
>
>* [Demander et participer aux  de](/help/sites-authoring/workflows.md)
>* [Création de modèles de processus et extension de la fonctionnalité de processus](/help/sites-developing/workflows.md)
>* [Méthodes d’exécution du](/help/sites-administering/workflows-starting.md)
>* [Meilleures pratiques de flux](/help/sites-developing/workflows-best-practices.md)
>* [Article de la communauté sur la modification d’un fichier à l’aide d’un processus](https://helpx.adobe.com/fr/experience-manager/using/modify_asset_workflow.html)

