---
title: Traiter les actifs à l’aide de workflows
description: Traitement des ressources pour convertir des formats, créer des rendus, gérer des ressources, valider des ressources et exécuter des workflows.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 5069c2cd26e84866d72a61d36de085dadd556cdd
workflow-type: tm+mt
source-wordcount: '975'
ht-degree: 27%

---


# Traiter les ressources numériques {#process-assets}

[!DNL Adobe Experience Manager Assets] vous permet de travailler sur vos ressources numériques de plusieurs manières pour permettre un traitement robuste des ressources. Vous pouvez utiliser les méthodes de traitement par défaut ou personnalisées pour assurer l&#39;achèvement des processus d&#39;entreprise de bout en bout, les audits et la conformité, la découverte et la distribution, ainsi que la qualité de base de vos ressources numériques. Vous pouvez exécuter les tâches de gestion des ressources tout en respectant l’échelle et la personnalisation requises.

## Comprendre les workflows {#understand-workflows}

Pour le traitement des ressources, [!DNL Experience Manager] utilise des workflows. Les workflows permettent d’automatiser la logique ou les activités métier. Les étapes granulaires permettant d’accomplir des tâches spécifiques sont fournies par défaut et les développeurs peuvent créer leurs propres étapes personnalisées. Ces étapes peuvent être combinées dans un ordre logique pour créer des workflows. Par exemple, un processus peut appliquer un filigrane aux images téléchargées en fonction de critères spécifiques, tels que le dossier dans lequel elles sont téléchargées, la résolution de l’image, etc. Un autre exemple est un processus configuré pour le filigrane et qui permet d’ajouter simultanément des métadonnées, de créer des rendus, d’ajouter des balises intelligentes et de publier sur une banque de données.

## Workflows par défaut disponibles dans [!DNL Experience Manager] {#default-workflows}

Par défaut, toutes les ressources téléchargées sont traitées à l’aide du processus [!UICONTROL DAM Update Asset] . Le processus s’exécute pour chaque ressource téléchargée et exécute les tâches de gestion des ressources de base telles que la génération de rendu, l’écriture différée des métadonnées, l’extraction de page, l’extraction du média et le transcodage.

Pour afficher les différents modèles de processus disponibles par défaut, voir **[!UICONTROL Outils > Processus > Modèles]** dans [!DNL Experience Manager].

![Certains flux de travaux par défaut](assets/aem-default-workflows.png)

*Figure : Certains des workflows par défaut disponibles dans[!DNL Experience Manager].*

## Apply workflows to process assets {#applying-workflows-to-assets}

L’application de workflow aux ressources numériques est identique à l’application de workflow aux pages d’un site web. For a complete guide on how to create and use workflows, see [start workflows](/help/sites-authoring/workflows-participating.md).

Utilisez les workflows dans les ressources numériques pour activer les ressources ou créer des filigranes. La plupart des workflow destinés aux ressources sont automatiquement activés, comme le workflow permettant de créer automatiquement un rendu après la modification d’une image.

>[!NOTE]
>
>If a workflow available in Classic UI is not available in Touch-enabled UI such as [!UICONTROL Request to Activate] and [!UICONTROL Request to Deactivate], see [make workflow models](/help/sites-developing/workflows-models.md#classic2touchui).

## Application d’un workflow à une ressource {#apply-a-workflow-to-an-asset}

<!-- 
TBD: Add animated GIF for these steps instead of all these screenshots.
-->
Pour appliquer un processus à une ressource, procédez comme suit :

1. Accédez à l’emplacement de la ressource pour laquelle vous souhaitez début un processus, puis cliquez sur la ressource pour ouvrir la page de la ressource. Sélectionnez **[!UICONTROL Chronologie]** dans le menu pour afficher la chronologie.

   ![chronologie-1](assets/timeline.png)

1. Click **[!UICONTROL Actions]** at the bottom to open the list of actions available for the asset.

1. Click **[!UICONTROL Start Workflow]** from the list.

1. Dans la section **[!UICONTROL Démarrer le workflow]**, sélectionnez un modèle de workflow dans la liste.

1. (Facultatif) Spécifiez un titre pour le processus qui peut être utilisé pour référencer l’instance du processus.

   ![sélectionnez un processus, fournissez un titre et cliquez sur début.](assets/start-workflow.png)

1. Click **[!UICONTROL Start]** and then click **[!UICONTROL Proceed]**. Chaque étape du workflow s’affiche en tant qu’événement dans la chronologie.

   ![chlimage_1-256](assets/chlimage_1-52.png)

## Application d’un workflow à plusieurs ressources {#applying-a-workflow-to-multiple-assets}

1. From the [!DNL Assets] console, navigate to the location of the assets for which you want to start a workflow, and select the assets. Sélectionnez **[!UICONTROL Chronologie]** dans le menu pour afficher la chronologie.

   ![screen_shot_2019-03-06at123325pm](assets/chlimage_1-136.png)

1. Cliquez sur **[!UICONTROL Actions]** ![chevron vers le haut](assets/do-not-localize/chevron-up-icon.png) en bas.
1. Cliquez sur **[!UICONTROL Démarrer le workflow]**. Dans la section **[!UICONTROL Démarrer le workflow]**, sélectionnez un modèle de workflow dans la liste.

   ![Processus de début](assets/start-workflow.png)

1. (Facultatif) Spécifiez le titre du workflow, qui peut permettre de référencer l’instance du workflow.
1. Cliquez sur **[!UICONTROL Démarrer]**, puis sur **[!UICONTROL Confirmer]** dans la boîte de dialogue. Le workflow s’exécute sur toutes les ressources sélectionnées.

## Application d’un workflow à plusieurs dossiers {#applying-a-workflow-to-multiple-folders}

La procédure à suivre pour appliquer un workflow à plusieurs dossiers est similaire à celle observée permettant d’appliquer un workflow à plusieurs ressources. Select the folders in the [!DNL Assets] interface, and perform steps 2-7 of the procedure [apply a workflow to multiple assets](/help/assets/assets-workflow.md#applying-a-workflow-to-multiple-assets).

## Application d’un workflow à une collection {#applying-a-workflow-to-a-collection}

Voir [appliquer un processus à une collection](/help/assets/managing-collections-touch-ui.md#running-a-workflow-on-a-collection).

## Début automatique d’un processus pour traiter les ressources de manière conditionnelle {#auto-execute-workflow-on-some-assets}

Les administrateurs peuvent configurer le processus pour exécuter et traiter automatiquement les ressources en fonction de conditions prédéfinies. Cette fonctionnalité s’avère utile pour les utilisateurs et les marketeurs de la gamme d’activités, par exemple pour créer un processus personnalisé sur des dossiers spécifiques. Disons que tous les fichiers provenant de la prise de vue d&#39;une agence peuvent être marqués d&#39;un filigrane ou que tous les fichiers téléchargés par un indépendant peuvent être traités pour créer des rendus spécifiques.

Pour un modèle de processus, les utilisateurs peuvent créer un lanceur de processus qui l’exécute. Un lanceur de processus surveille les modifications dans le référentiel de contenu et exécute le processus lorsque les conditions prédéfinies sont remplies. Les administrateurs peuvent donner accès aux marketeurs pour créer les workflows et configurer le lanceur. Les utilisateurs peuvent modifier le processus de mise à jour des actifs  DAM par défaut afin d’ajouter les étapes supplémentaires requises pour traiter des actifs spécifiques. Le processus s’exécute sur tous les fichiers nouvellement transférés. Utilisez l’une des méthodes suivantes pour limiter l’exécution des étapes supplémentaires sur des ressources spécifiques :

* Effectuez une copie du flux de travail [!UICONTROL DAM Update Asset] et modifiez-le pour qu’il s’exécute sur une hiérarchie de dossiers spécifique. Cette approche est utile pour quelques dossiers.
* Les étapes de traitement supplémentaires peuvent être ajoutées à l’aide d’un fractionnement [](/help/sites-developing/workflows-step-ref.md#or-split) OU applicable de manière conditionnelle au plus grand nombre de dossiers requis.

## Bonnes pratiques et restrictions {#best-practices-limitations-tips}

* Pour la conception des workflows, prenez en compte vos besoins pour tous les types de rendus. Si vous ne prévoyez pas la nécessité d’un rendu futur, supprimez son étape de création dans le workflow. Il est impossible par la suite de supprimer les rendus en masse. Les rendus superflus peuvent occuper beaucoup d’espace de stockage suite à une utilisation prolongée d’[!DNL Experience Manager]. Pour les ressources individuelles, vous pouvez supprimer manuellement les rendus à l’aide de l’interface utilisateur. Si plusieurs ressources sont concernées, vous pouvez, au choix, personnaliser [!DNL Experience Manager] pour supprimer des rendus spécifiques, ou supprimer les ressources et les charger à nouveau.
* Par défaut, le processus de mise à jour des ressources  DAM comprend quelques étapes pour créer des miniatures et des rendus Web. Si des rendus par défaut sont supprimés du flux de travail, l’interface utilisateur de [!DNL Assets] ne s’affiche pas correctement.

>[!MORELIKETHIS]
>
>* [Demander et participer aux workflows](/help/sites-authoring/workflows.md)
>* [Créer des modèles de processus et étendre les fonctionnalités de processus](/help/sites-developing/workflows.md)
>* [Méthodes d’exécution des workflows](/help/sites-administering/workflows-starting.md)
>* [Meilleures pratiques de flux de travaux](/help/sites-developing/workflows-best-practices.md)
>* [Article de la communauté sur la modification d’une ressource à l’aide du processus](https://helpx.adobe.com/fr/experience-manager/using/modify_asset_workflow.html)

