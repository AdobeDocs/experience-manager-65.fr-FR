---
title: Balises intelligentes améliorées
description: Balises intelligentes améliorées
contentOwner: AG
translation-type: tm+mt
source-git-commit: abc4821ec3720969bf1c2fb068744c07477aca46

---


# Balises intelligentes améliorées {#enhanced-smart-tags}

## Présentation des balises intelligentes améliorées {#overview-of-enhanced-smart-tags}

Les entreprises qui traitent les ressources numériques utilisent de plus en plus le vocabulaire contrôlé par taxonomie dans les métadonnées des ressources. Il comprend essentiellement une liste des mots-clés que les employés, les partenaires et les clients utilisent fréquemment pour mentionner et rechercher des ressources numériques d’une classe particulière. Le balisage des ressources avec vocabulaire contrôlé par taxonomie permet de s’assurer que les ressources peuvent être facilement identifiées et récupérées par des recherches reposant sur les balises.

Comparé aux vocabulaires des langages naturels, le balisage des ressources numériques basé sur la taxonomie métier aide à les aligner avec les activités d’une entreprise et à assurer que les ressources les mieux adaptées apparaissent dans les recherches.

Par exemple, un constructeur de voitures peut baliser les images de voitures avec les noms de modèles afin d’afficher uniquement les images appropriées lors de recherches d’images de différents modèles pour concevoir une campagne de promotion.

Pour que le service de contenu dynamique applique les balises adéquates, vous devez l’entraîner à reconnaître votre taxonomie. Pour entraîner le service, regroupez tout d’abord un ensemble de ressources et de balises qui décrivent le mieux ces ressources. Appliquez ces balises sur les ressources et exécutez un workflow d’entraînement pour aider le service à apprendre.

Une fois une balise entraînée et prête, le service peut appliquer ces balises sur les ressources par un workflow de balisage.

En arrière-plan, le service de contenu intelligent utilise la structure Adobe Sensei AI pour former son algorithme de reconnaissance d’image à la structure des balises et à la taxonomie commerciale. Cette intelligence de contenu est ensuite utilisée pour appliquer les balises pertinentes sur un ensemble de ressources différentes.

Smart Content Service est un service cloud hébergé sur les E/S Adobe. Pour l’utiliser dans Adobe Experience Manager, l’administrateur système doit intégrer votre instance Experience Manager aux E/S Adobe.

En résumé, voici les principales étapes pour utiliser le service de contenu dynamique :

* Intégration
* Passage en revue des ressources et des balises (définition de la taxonomie)
* Entraînement du service de contenu dynamique
* Balisage automatique

![organigramme](assets/flowchart.gif)

## Conditions préalables {#prerequisites}

Avant de pouvoir utiliser le service de contenu dynamique, assurez-vous de respecter les conditions suivantes pour créer une intégration sur Adobe I/O :

* L’organisation doit disposer d’un compte Adobe ID pourvu de droits d’administrateur.
* Le service de contenu dynamique est activé pour votre organisation.

## Intégration {#onboarding}

Le service de contenu dynamique est disponible à l’achat en tant que module complémentaire d’Experience Manager. Après l’achat, un courrier électronique est envoyé à l’administrateur de votre entreprise avec un lien vers les E/S Adobe.

L’administrateur peut suivre le lien pour intégrer Smart Content Service à Experience Manager. To integrate the service with Experience Manager Assets, see [Configure Smart Tags](config-smart-tagging.md).

Le processus d’intégration est terminé lorsque l’administrateur configure le service et ajoute des utilisateurs dans Experience Manager.

>[!NOTE]
>
>Si vous utilisez Experience Manager 6.3 ou une version antérieure et que vous avez besoin du service de balisage pour vos ressources, voir Balises [intelligentes](https://helpx.adobe.com/experience-manager/6-3/assets/using/touch-ui-smart-tags.html). Les balises intelligentes n’utilisent pas les dernières fonctionnalités d’IA et sont donc moins précises que le service de balisage intelligent amélioré.

## Vérification des ressources et des balises {#reviewing-assets-and-tags}

Après intégration, commencez par identifier un ensemble de balises qui décrit le mieux ces images dans le contexte de votre entreprise.

Ensuite, passez en revue les images de façon à identifier une série d’images qui représentent le mieux votre produit pour un besoin particulier de votre entreprise. Vérifiez que les ressources figurant dans la série sélectionnée sont conformes aux [instructions d’entraînement du service de contenu dynamique](smart-tags-training-guidelines.md).

Ajoutez les ressources à un dossier, puis appliquez les balises à chaque ressource sur la page de propriétés. Exécutez ensuite le workflow d’entraînement sur ce dossier. La série de ressources sélectionnée permet au service de contenu dynamique d’entraîner efficacement plus de ressources avec vos définitions de taxonomie.

>[!NOTE]
>
>1. L’entraînement est un processus irrévocable. Adobe recommande de bien passer en revue les balises dans la série de ressources sélectionnée bien avant d’entraîner le service de contenu dynamique sur les balises.
>1. Please do read [Smart Content Service training guidelines](smart-tags-training-guidelines.md) before starting training for any tag.
>1. Lorsque vous entraînez le service de contenu dynamique pour la première fois, Adobe recommande de réaliser l’entraînement sur au moins deux balises distinctes.


## Formation de Smart Content Service {#training-the-smart-content-service}

Pour que le service de contenu dynamique reconnaisse votre taxonomie métier, exécutez-la sur une série de ressources qui incluent déjà des balises correspondant à votre entreprise. Après l’entraînement, le service peut appliquer la même taxonomie sur un ensemble de ressources similaire.

Vous pouvez entraîner plusieurs fois le service afin d’améliorer sa capacité à appliquer les balises appropriées. Après chaque cycle d’entraînement, exécutez un workflow de balisage et vérifiez que vos ressources sont correctement balisées.

Vous pouvez entraîner le service de contenu dynamique périodiquement ou en fonction des besoins.

>[!NOTE]
>
>Le workflow d’entraînement s’exécute sur les dossiers uniquement.

### Entraînement périodique {#periodic-training}

Vous pouvez activer le service de contenu dynamique afin qu’il s’entraîne périodiquement sur les ressources et les balises associées au sein d’un dossier. Open the [!UICONTROL Properties] page of your asset folder, select **[!UICONTROL Enable Smart Tags]** under the **[!UICONTROL Details]** tab, and save the changes.

![enable_smart_tags](assets/enable_smart_tags.png)

Une fois cette option sélectionnée pour un dossier, Experience Manager exécute automatiquement un processus de formation afin de former Smart Content Service aux ressources du dossier et à leurs balises. Par défaut, le workflow d’entraînement s’exécute sur une base hebdomadaire à 0 h 30 le samedi.

### Entraînement à la demande {#on-demand-training}

Vous pouvez entraîner le service de contenu dynamique chaque fois que cela est nécessaire à partir de la console Processus.

1. Dans l’interface d’Experience Manager, accédez à **[!UICONTROL Outils > Processus > Modèles]**.
1. From the **[!UICONTROL Workflow Models]** page, select the **[!UICONTROL Smart Tags Training]** workflow and then click **[!UICONTROL Start Workflow]** from the toolbar.
1. Dans la boîte de dialogue **[!UICONTROL Exécuter le processus]**, localisez le dossier de charge utile qui comprend les ressources balisées pour entraîner le service.
1. Indiquez le titre du workflow et ajoutez un commentaire. Then, click **[!UICONTROL Run]**. Les ressources et les balises sont soumises à l’entraînement.

   ![workflow_dialog](assets/workflow_dialog.png)

>[!NOTE]
>
>Une fois que les ressources d’un dossier sont traitées pour la formation, seules les ressources modifiées sont traitées lors des cycles de formation suivants.

### Rapports de formation {#viewing-training-reports}

Pour vérifier que le service de contenu dynamique est entraîné sur vos balises dans la série de ressources d’entraînement, examinez le rapport de workflow d’entraînement dans la console Rapports.

1. Dans l’interface d’Experience Manager, accédez à **[!UICONTROL Outils > Ressources > Rapports]**.
1. In the **[!UICONTROL Asset Reports]** page, click **[!UICONTROL Create]**.
1. Select the **[!UICONTROL Smart Tags Training]** report, and then click **[!UICONTROL Next]** from the toolbar.
1. Indiquez un titre et une description pour le rapport. Sous **[!UICONTROL Planifier le rapport]**, laissez l’option **[!UICONTROL Maintenant]** sélectionnée. Si vous souhaitez planifier le rapport pour une date ultérieure, sélectionnez **[!UICONTROL Plus tard]** et spécifiez une date et une heure. Then, click **[!UICONTROL Create]** from the toolbar.
1. Dans la page **[!UICONTROL Rapports de ressources]**, sélectionnez le rapport que vous avez généré. To view the report, click **[!UICONTROL View]** from the toolbar.
1. Passez en revue les détails du rapport.

   Le rapport affiche l’état d’identification des balises que vous avez formées. La couleur verte de la colonne **[!UICONTROL État de l’entraînement]** indique que le service de contenu dynamique est entraîné pour la balise. La couleur jaune indique que le service n’est pas complètement entraîné pour une balise particulière. Dans ce cas, ajoutez d’autres images avec la balise particulière et exécutez le processus d’entraînement pour l’entraînement complet du service sur la balise.

   Si vous ne voyez pas vos balises dans ce rapport, lancez à nouveau le workflow d’entraînement pour ces balises.

1. To download the report, select it from the list, and click **[!UICONTROL Download]** from the toolbar. Le rapport est téléchargé sous forme de feuille de calcul Microsoft Excel.

## Baliser automatiquement les fichiers {#tagging-assets-automatically}

Après avoir entraîné le service de contenu dynamique, vous pouvez déclencher le workflow de balisage pour appliquer automatiquement les balises appropriées sur une autre série de ressources similaire.

Vous pouvez exécuter le workflow de balisage périodiquement ou au besoin.

>[!NOTE]
>
>Le workflow de balisage s’exécute sur les ressources et les dossiers.

### Balisage périodique {#periodic-tagging}

Vous pouvez activer le service de contenu dynamique de façon à ce qu’il balise périodiquement les ressources au sein d’un dossier. Open the properties page of your asset folder, select **[!UICONTROL Enable Smart Tags]** under the **[!UICONTROL Details]** tab, and save the changes.

Une fois cette option sélectionnée pour un dossier, Smart Content Service balise automatiquement les fichiers qu’il contient. Par défaut, le processus de balisage s’exécute tous les jours à 12h00.

### Balisage à la demande {#on-demand-tagging}

Vous pouvez déclencher le workflow de balisage à partir des emplacements suivants pour baliser instantanément vos ressources :

* Console de processus
* Chronologie

>[!NOTE]
>
>Si vous exécutez le workflow de balisage à partir de la chronologie, vous pouvez appliquer des balises sur un maximum de 15 ressources à la fois.

#### Tag assets from the workflow console {#tagging-assets-from-the-workflow-console}

1. Dans l’interface d’Experience Manager, accédez à **[!UICONTROL Outils > Processus > Modèles]**.
1. From the **[!UICONTROL Workflow Models]** page, select the **[!UICONTROL DAM Smart Tags Assets]** workflow and then click **[!UICONTROL Start Workflow]** from the toolbar.

   ![dam_smart_tag_workflow](assets/dam_smart_tag_workflow.png)

1. In the **[!UICONTROL Run Workflow]** dialog, browse to the payload folder containing assets on which you want to apply your tags automatically.
1. Indiquez un titre pour le workflow et un commentaire facultatif. Cliquez sur **[!UICONTROL Exécuter]**.

   ![tagging_dialog](assets/tagging_dialog.png)

   Accédez au dossier de ressources et passez en revue les balises pour vérifier que le service de contenu dynamique a correctement balisé vos ressources. Pour plus d’informations, voir [Gestion des balises intelligentes](managing-smart-tags.md).

#### Tag assets from the timeline {#tagging-assets-from-the-timeline}

1. Depuis l’interface utilisateur Assets, sélectionnez le dossier contenant les ressources ou des ressources spécifiques auxquelles vous souhaitez appliquer des balises intelligentes.
1. Dans le coin supérieur gauche, ouvrez le **[!UICONTROL journal]**.
1. Ouvrez les actions dans la partie inférieure de la barre latérale gauche et cliquez sur **[!UICONTROL Flux de travaux]**.

   ![_workflow](assets/start_workflow.png)

1. Sélectionnez le workflow **[!UICONTROL Balisage intelligent des ressources (gestion des actifs numériques)]** et spécifiez un titre pour le workflow.
1. Cliquez sur **[!UICONTROL Démarrer]**. Le workflow applique vos balises sur les ressources. Accédez au dossier de ressources et passez en revue les balises pour vérifier que le service de contenu dynamique a correctement balisé vos ressources. For details, see [manage Smart Tags](managing-smart-tags.md).

>[!NOTE]
>
>Lors des cycles de balisage suivants, seules les ressources modifiées sont à nouveau balisées avec des balises nouvellement formées. Toutefois, même les ressources non modifiées sont balisées si l’écart entre le dernier cycle de balisage et le cycle de balisage actuel du processus de balisage dépasse 24 heures. Pour les  de balisage périodiques, les fichiers non modifiés sont balisés lorsque l’intervalle de temps dépasse 6 mois.
