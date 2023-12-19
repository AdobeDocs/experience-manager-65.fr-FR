---
title: Traitement des ressources à l’aide de workflows
description: Traitement des ressources pour convertir des formats, créer des rendus, gérer des ressources, valider des ressources et exécuter des workflows.
contentOwner: AG
feature: Workflow, Renditions
role: User, Admin
exl-id: e7c84385-efb3-4997-83ff-7a7f31582469
source-git-commit: 941e5d7574d31622f50e50e717c21cd2eba2e602
workflow-type: tm+mt
source-wordcount: '962'
ht-degree: 97%

---

# Traitement des ressources numériques {#process-assets}

[!DNL Adobe Experience Manager Assets] vous permet de travailler sur vos ressources numériques de différentes manières pour permettre un traitement des ressources robuste. Vous pouvez utiliser les méthodes de traitement par défaut ou personnalisées pour garantir la fin des processus d’entreprise de bout en bout, les audits et la conformité, la découverte et la distribution, ainsi que l’intégrité de base de vos ressources numériques. Vous pouvez effectuer les tâches de gestion des ressources tout en respectant l’échelle et la personnalisation requises.

## Présentation des workflows {#understand-workflows}

Pour le traitement des ressources, [!DNL Experience Manager] utilise des workflows. Les workflows permettent d’automatiser la logique commerciale ou les activités. Chaque étape permettant d’accomplir des tâches spécifiques sont fournies par défaut et les développeurs peuvent créer leurs propres étapes personnalisées. Ces étapes peuvent être combinées dans un ordre logique pour créer des workflows. Par exemple, un workflow permet d’appliquer un filigrane sur les images téléchargées en fonction d’un critère spécifique, tel que le dossier vers lequel elles sont téléchargées, la résolution de l’image, etc. Un autre exemple est un workflow configuré pour ajouter un filigrane et simultanément des métadonnées, créer des rendus, ajouter des balises intelligentes et publier dans un magasin de données.

## Workflows par défaut disponibles dans [!DNL Experience Manager] {#default-workflows}

Par défaut, toutes les ressources chargées sont traitées à l’aide du workflow [!UICONTROL Ressource de mise à jour de la gestion des ressources numériques]. Le workflow s’exécute pour chaque ressource chargée et exécute les tâches de gestion des ressources de base telles que la génération de rendu, l’écriture différée des métadonnées, l’extraction de page, l’extraction de médias et le transcodage.

Pour consulter les différents modèles de workflow disponibles par défaut, consultez **[!UICONTROL Outils > Processus > Modèles]** dans [!DNL Experience Manager].

![Quelques workflows par défaut](assets/aem-default-workflows.png)

*Image : quelques workflows par défaut disponibles dans [!DNL Experience Manager].*

## Application de workflows pour le traitement de ressources {#applying-workflows-to-assets}

L’application de workflow aux ressources numériques est identique à l’application de workflow aux pages d’un site Web. Pour obtenir des informations complètes sur la création et l’utilisation de processus, reportez-vous à la section [démarrer des workflows](/help/sites-authoring/workflows-participating.md).

Utilisez les workflows dans les ressources numériques pour activer les ressources ou créer des filigranes. La plupart des workflows des ressources sont automatiquement activés. Par exemple, le workflow qui crée automatiquement un rendu après la modification d’une image est automatiquement activé.

>[!NOTE]
>
>Si un workflow disponible dans l’interface utilisateur classique ne l’est pas dans l’interface utilisateur tactile, comme [!UICONTROL Demande d’activation] et [!UICONTROL Demande de désactivation[, consultez ]Rendre les modèles de workflow disponibles dans l’interface utilisateur tactile](/help/sites-developing/workflows-models.md#classic2touchui).

## Application d’un workflow à une ressource {#apply-a-workflow-to-an-asset}

<!-- 
TBD: Add animated GIF for these steps instead of all these screenshots.
-->
Pour appliquer un workflow à une ressource, procédez comme suit :

1. Accédez à l’emplacement de la ressource pour laquelle vous souhaitez commencer un workflow et cliquez sur la ressource pour afficher la page de ressource. Sélectionnez **[!UICONTROL Chronologie]** dans le menu pour afficher la chronologie.

   ![chronologie-1](assets/timeline.png)

1. Cliquez sur **[!UICONTROL Actions]** dans la partie inférieure pour afficher la liste des actions disponibles pour la ressource.

1. Cliquez sur **[!UICONTROL Démarrer le workflow]** dans la liste.

1. Dans la section **[!UICONTROL Démarrer le processus]**, sélectionnez un modèle de workflow dans la liste.

1. (Facultatif) Indiquez un titre pour le processus qui peut servir à référencer l’instance du workflow.

   ![Sélectionnez un workflow, fournissez un titre et cliquez sur démarrer](assets/start-workflow.png)

1. Cliquez sur **[!UICONTROL Démarrer]** et sur **[!UICONTROL Oui]**. Chaque étape du workflow s’affiche en tant qu’événement dans la chronologie.

   ![chlimage_1-256](assets/chlimage_1-52.png)

## Application d’un workflow à plusieurs ressources {#applying-a-workflow-to-multiple-assets}

1. Dans la console [!DNL Assets], accédez à l’emplacement des ressources pour lesquelles vous souhaitez démarrer un workflow, puis sélectionnez les ressources. Sélectionnez **[!UICONTROL Chronologie]** dans le menu pour afficher la chronologie.

   ![screen_shot_2019-03-06at123325pm](assets/chlimage_1-136.png)

1. Cliquez sur **[!UICONTROL Actions]** ![chevron vers le haut](assets/do-not-localize/chevron-up-icon.png) en bas.
1. Cliquez sur **[!UICONTROL Démarrer le processus]**. Dans la section **[!UICONTROL Démarrer le processus]**, sélectionnez un modèle de workflow dans la liste.

   ![Démarrer le processus](assets/start-workflow.png)

1. (Facultatif) Spécifiez le titre du workflow, qui peut permettre de référencer l’instance du workflow.
1. Cliquez sur **[!UICONTROL Démarrer]**, puis sur **[!UICONTROL Confirmer]** dans la boîte de dialogue. Le workflow s’exécute sur toutes les ressources que vous avez sélectionnées.

## Application d’un workflow à plusieurs dossiers {#applying-a-workflow-to-multiple-folders}

La procédure à suivre pour appliquer un workflow à plusieurs dossiers est similaire à celle observée permettant d’appliquer un workflow à plusieurs ressources. Sélectionnez les dossiers dans l’interface [!DNL Assets] et suivez les étapes 2 à 7 de la section [Application d’un workflow à plusieurs ressources](/help/assets/assets-workflow.md#applying-a-workflow-to-multiple-assets).

## Application d’un workflow à une collection {#applying-a-workflow-to-a-collection}

Consultez [Appliquer un workflow à une collection](/help/assets/manage-collections.md#running-a-workflow-on-a-collection).

## Démarrage automatique d’un workflow pour traiter les ressources de manière conditionnelle {#auto-execute-workflow-on-some-assets}

Les administrateurs peuvent configurer un workflow pour exécuter et traiter automatiquement les ressources en fonction de conditions prédéfinies. Cette fonctionnalité est utile pour les utilisateurs et les spécialistes du marketing du secteur, par exemple pour créer un workflow personnalisé sur des dossiers spécifiques. Disons que toutes les ressources de la séance photo d’une agence peuvent recevoir un filigrane ou que toutes les ressources téléchargées par un programme de travail indépendant peuvent être traitées pour créer des rendus spécifiques.

Pour chaque modèle de workflow, les utilisateurs peuvent créer un lanceur de workflow qui l’exécute. Un lanceur de workflow surveille les modifications du référentiel de contenu et exécute le workflow lorsque les conditions prédéfinies sont remplies. Les administrateurs peuvent donner accès aux spécialistes marketing pour leur permettre de créer les workflows et de configurer le lanceur. Les utilisateurs peuvent modifier le workflow [!UICONTROL Ressource de mise à jour de la gestion des ressources numériques] par défaut pour ajouter les étapes supplémentaires requises pour traiter des ressources spécifiques. Le workflow s’exécute sur toutes les ressources nouvellement chargées. Utilisez l’une des méthodes suivantes pour limiter l’exécution des étapes supplémentaires sur des ressources spécifiques :

* Effectuez une copie du workflow [!UICONTROL Ressource de mise à jour de la gestion des ressources numériques] et modifiez-la pour l’exécuter sur une hiérarchie de dossiers spécifique. Cette approche est utile pour quelques dossiers.
* Les étapes de traitement supplémentaires peuvent être ajoutées à l’aide d’une [Division OU](/help/sites-developing/workflows-step-ref.md#or-split) qui s’applique de manière conditionnelle au plus grand nombre de dossiers requis.

## Bonnes pratiques et restrictions {#best-practices-limitations-tips}

* Pour la conception des workflows, prenez en compte vos besoins pour tous les types de rendus. Si vous ne prévoyez pas la nécessité d’un rendu futur, supprimez son étape de création dans le workflow. Il est impossible par la suite de supprimer les rendus en masse. Les rendus non souhaités peuvent occuper de l’espace de stockage après une utilisation prolongée de [!DNL Experience Manager]. Pour les ressources individuelles, vous pouvez supprimer manuellement les rendus à l’aide de l’interface utilisateur. Si plusieurs ressources sont concernées, vous pouvez, au choix, personnaliser [!DNL Experience Manager] pour supprimer des rendus spécifiques, ou supprimer les ressources et les charger à nouveau.
* Par défaut, le workflow [!UICONTROL Ressource de mise à jour de la gestion des ressources numériques] comprend quelques étapes pour créer des miniatures et des rendus Web. Si des rendus par défaut sont supprimés du workflow, l’interface utilisateur d’[!DNL Assets] ne s’affiche pas correctement.

>[!MORELIKETHIS]
>
>* [Application et participation aux workflows](/help/sites-authoring/workflows.md)
>* [Création de modèles de workflow et extension de la fonctionnalité de workflow](/help/sites-developing/workflows.md)
>* [Méthodes d’exécution de workflows](/help/sites-administering/workflows-starting.md)
>* [Bonnes pratiques relatives aux workflows](/help/sites-developing/workflows-best-practices.md)
