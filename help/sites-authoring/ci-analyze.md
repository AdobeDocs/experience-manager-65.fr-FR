---
title: Analyser les performances de page
seo-title: Analyzing Page Performance
description: Utilisez la page Content Insight pour analyser les performances de la page que vous créez.
seo-description: Use the Content Insight page to analyze the performance of the page that you are authoring
uuid: 563d3e98-20d9-4cca-a174-bafd6e65c1bb
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 57cd61d5-78f2-4f8c-99ee-75e100c052ef
docset: aem65
exl-id: 14484a90-4e44-4c85-9411-b78ed11dc70d
source-git-commit: 75c6bb87bb06c5ac9378ccebf193b5416c080bb1
workflow-type: tm+mt
source-wordcount: '666'
ht-degree: 19%

---

# Analyser les performances de page{#analyzing-page-performance}

Ouvrez le [Content Insight](/help/sites-authoring/content-insights.md) pour analyser les performances de la page que vous créez. Configurez la période de création de rapports pour cibler votre analyse.

## Ouverture d’Analytics et de Recommendations pour une page {#opening-analytics-and-recommendations-for-a-page}

Procédez comme suit pour afficher Analytics et Recommendations pour une page :

1. Accédez à la page que vous souhaitez analyser.
1. Dans la barre d’outils, cliquez ou appuyez sur **Analyses et recommandations**.

   >[!NOTE]
   >
   >Les analyses et recommandations pour une page s’affichent uniquement si vous avez configuré l’[intégration d’AEM avec Adobe Analytics](/help/sites-administering/adobeanalytics-connect.md).

   ![screen-shot_2019-03-05at115319](assets/screen-shot_2019-03-05at115319.png)

### Modification de la période de création de rapports {#changing-the-reporting-period}

Modifiez les aspects suivants liés au temps des rapports d’analyse :

* Période pendant laquelle générer les rapports.
* Granularité des données.

Les outils permettant de modifier les aspects temporels des rapports s’affichent en haut de la page Content Insight. ![chlimage_1-126](assets/chlimage_1-126.png)

#### Modification de la période de création de rapports {#changing-the-reporting-period-1}

Modifiez la période de création de rapports de la page Content Insight afin de concentrer votre analyse de l’activité de la page sur une période spécifique. Lorsque vous modifiez la période de création de rapports, les rapports sont automatiquement actualisés. La zone ombrée de la période représente la période du rapport. Les dates sur la période passent de gauche à droite.

![chlimage_1-127](assets/chlimage_1-127.png)

Pour modifier la période de création de rapports d’une page Content Insight :

1. Si la période n’apparaît pas en haut de la page, cliquez ou appuyez sur l’icône Activer/désactiver la période .

   ![Activer/désactiver la période](do-not-localize/chlimage_1-22.png)

1. Pour modifier la date de début de la période de création de rapports, faites glisser le cercle qui s’affiche sur le côté gauche de la zone ombrée jusqu’à la date de début souhaitée.

   Si vous ne pouvez pas voir le côté gauche de la zone ombrée, utilisez la barre de défilement pour l’afficher.

1. Pour modifier la date de fin de la période de rapport, faites glisser le cercle qui s’affiche sur le côté droit de la zone ombrée jusqu’à la date de fin souhaitée.

#### Modification de la granularité de la période de création de rapports {#changing-the-granularity-of-the-reporting-period}

Permet de modifier la durée de chaque point de données dans un rapport. Par exemple, lorsque la granularité Semaine est sélectionnée, chaque point de données du rapport Vues représente le nombre de vues pour une semaine.

![screen_shot_2017-11-29at141001](assets/screen_shot_2017-11-29at141001.png)

La granularité affecte les rapports qui tracent les données par rapport au temps, tels que les rapports Pages vues et Moyenne des minutes d’engagement. La granularité affecte également l’échelle de la période.

1. Si le contrôle de granularité n’apparaît pas, cliquez ou appuyez sur l’icône Activer/désactiver la granularité .

   ![chlimage_1-128](assets/chlimage_1-128.png)

1. Cliquez ou appuyez sur la granularité souhaitée. Une fois sélectionné, le rapport est automatiquement mis à jour pour refléter la granularité.

### Attribution de tâches à Recommendations pour l’optimisation pour les moteurs de recherche {#assigning-tasks-for-seo-recommendations}

Utilisez le rapport Recommendations d’optimisation pour les moteurs de recherche pour créer des tâches visant à améliorer la visibilité des pages. Pour chaque recommandation du rapport qui ne comporte pas de coche, vous pouvez créer une tâche que vous affectez à un utilisateur pour effectuer le travail requis.

![chlimage_1-129](assets/chlimage_1-129.png)

Le statut de la recommandation d’optimisation pour les moteurs de recherche indique quand la tâche est créée mais pas encore terminée.

![chlimage_1-130](assets/chlimage_1-130.png)

Une fois créée, la tâche apparaît dans la liste Tâches de l’utilisateur. Pour plus d’informations sur les tâches, consultez [Utilisation de tâches](/help/sites-authoring/task-content.md).

Utilisez la procédure suivante pour créer une tâche pour une recommandation d’optimisation pour les moteurs de recherche.

1. Cliquez ou appuyez sur l’icône d’informations de la recommandation d’optimisation pour les moteurs de recherche.

   ![Icône Informations](do-not-localize/chlimage_1-23.png)

1. Cliquez sur l’icône en forme de triangle encerclé qui s’affiche en regard de l’icône d’information.

   ![chlimage_1-131](assets/chlimage_1-131.png)

1. Renseignez les champs de formulaire qui s’affichent, puis appuyez sur Créer :

   * Projet : Sélectionnez le projet dans lequel créer la tâche.
   * Nom : Nom qui identifie la tâche. Le nom par défaut est le titre de la recommandation d’optimisation pour les moteurs de recherche.
   * Attribuer à : Sélectionnez l’utilisateur auquel la tâche doit être affectée. Commencez à saisir le nom de l’utilisateur pour filtrer la liste.
   * Description : Description de l’activité requise pour terminer la tâche. La description par défaut correspond aux informations accompagnant la recommandation d’optimisation pour les moteurs de recherche.
   * Priorité des tâches : Priorité de la tâche.
   * Date d’échéance : Date à laquelle la tâche doit être terminée.

   **Remarque :** la tâche créée inclut également le chemin d’accès à la page à laquelle la recommandation d’optimisation pour les moteurs de recherche s’applique.

1. Cliquez ou appuyez sur Terminé pour fermer le message Tâche créée.
