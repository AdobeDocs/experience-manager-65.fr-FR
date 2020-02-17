---
title: Rapports prédéfinis dans Process Reporting
seo-title: Rapports prédéfinis dans Process Reporting
description: Requête pour les données de processus d’AEM Forms sur JEE afin de créer des rapports sur les processus à long terme, la durée du processus et le volume de flux de travail
seo-description: Requête pour les données de processus d’AEM Forms sur JEE afin de créer des rapports sur les processus à long terme, la durée du processus et le volume de flux de travail
uuid: 704a8886-90ea-4793-a3fc-f998f878c928
content-type: reference
topic-tags: process-reporting
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 3d93375e-ec37-4445-96ea-d315676787b4
docset: aem65
translation-type: tm+mt
source-git-commit: d9975c0dcc02ae71ac64aadb6b4f82f7c993f32c

---


# Rapports prédéfinis dans Process Reporting {#pre-defined-reports-in-process-reporting}

## Rapports prédéfinis dans les rapports de processus {#pre-defined-reports-in-process-reporting-1}

Les rapports de processus AEM Forms sont livrés avec les rapports *prêts à l’emploi* suivants :

* **[Processus](#long-running-processes)**à long terme : Rapport de tous les processus AEM Forms qui ont pris plus d’une durée spécifiée à terminer
* **[Graphique](#process-duration-report)**de durée du processus : Rapport d’un processus AEM Forms spécifié par durée
* **[Volume](#workflow-volume-report)**du flux de travail : Rapport des instances en cours d’exécution et terminées du processus spécifié par date

## Processus à long terme {#long-running-processes}

Le rapport Processus à long terme affiche les processus AEM Forms qui ont pris plus d’une durée spécifiée pour être terminés.

### Pour exécuter un rapport Processus à long terme {#to-execute-a-long-running-process-report}

1. Pour afficher la liste des rapports prédéfinis dans Process Reporting, dans l’arborescence **Process Reporting** , cliquez sur le **noeud Rapports **Noeud.
1. Cliquez sur le noeud de rapport Processus **à** long terme.

   ![long_running_node](assets/long_running_node.png)

   Lorsque vous sélectionnez un rapport, le panneau Paramètres **du** rapport s’affiche à droite de l’arborescence.

   ![panneau des paramètres de rapport des processus à long terme](assets/report_parameters_panel.png)

   Paramètres:

   * **Durée**(*obligatoire*) : Spécifiez une durée et une unité de temps. Affichez tous les processus AEM Forms qui ont été exécutés pendant plus de la durée spécifiée.
   * **Démarré après** (*facultatif*) : Sélectionnez une date. Filtrez le rapport pour afficher les instances de processus qui ont commencé après la date spécifiée.
   * **Démarré avant** (*facultatif*) : Sélectionnez une date. Filtrez le rapport pour afficher les instances de processus qui ont commencé avant la date spécifiée.

1. Cliquez sur **Aller** pour exécuter le rapport.

   Le rapport s’affiche dans le panneau **Rapport **situé à droite de la fenêtre **Process Reporting** .

   ![long_running_processes](assets/long_running_processes.png)

   Utilisez les options dans le coin supérieur droit du panneau **Rapport **pour effectuer les opérations suivantes sur le rapport.

   * **Actualiser**: Actualise le rapport avec les dernières données stockées
   * **Modifier la couleur** de la légende : Sélectionner et modifier la couleur de la légende du rapport
   * **Exporter au format CSV**: Exportez et téléchargez les données du rapport dans un fichier séparé par des virgules.

## Rapport Durée du processus {#process-duration-report}

Le rapport Durée du processus affiche le nombre d’instances d’un processus Forms par nombre de jours d’exécution de chaque instance.

### Pour exécuter un rapport Durée du processus {#to-execute-a-process-duration-report}

1. Pour afficher les rapports prédéfinis dans Process Reporting, dans l’arborescence **Process Reporting** , cliquez sur le **noeud Rapports **Noeud.
1. Cliquez sur le noeud de rapport Durée des **processus** .

   ![process_length_node](assets/process_duration_node.png)

   Lorsque vous sélectionnez un rapport, le panneau Paramètres **du** rapport s’affiche à droite de l’arborescence.

   ![panneau des paramètres de rapport des processus à long terme](assets/process_duration_params.png)

   Paramètres:

   * **Sélectionner le processus **(*obligatoire*) : Sélectionnez un processus AEM Forms.

1. Cliquez sur **Aller **pour exécuter le rapport.

   Le rapport s’affiche dans le panneau **Rapport **à droite de la fenêtre Process Reporting.

   ![process_length_report](assets/process_duration_report.png)

   Utilisez les options dans le coin supérieur droit du panneau **Rapport **pour effectuer les opérations suivantes sur le rapport.

   * **Actualiser**: Actualise le rapport avec les dernières données stockées
   * **Modifier la couleur** de la légende : Sélectionner et modifier la couleur de la légende du rapport
   * **Exporter au format CSV**: Exportez et téléchargez les données du rapport dans un fichier séparé par des virgules.

## Rapport Volume du flux de travail {#workflow-volume-report}

Le rapport Volume de processus affiche le nombre d’instances en cours d’exécution et terminées d’un processus AEM Forms par jour calendaire.

### Pour exécuter un rapport Volume de flux de travail {#to-execute-a-workflow-volume-report}

1. Pour afficher les rapports prédéfinis dans Process Reporting, dans la vue **arborescence Création de rapports de processus, cliquez sur le noeud **Rapports **Rapports.
1. Cliquez sur le noeud de rapport Volume **de** processus.

   ![workflow_volume_node](assets/workflow_volume_node.png)

   Lorsque vous sélectionnez un rapport, le panneau Paramètres **du** rapport s’affiche à droite de l’arborescence.

   ![panneau des paramètres de rapport des processus à long terme](assets/workflow_volume_params.png)

   Paramètres:

   * **Sélectionner le processus **(*obligatoire*) : Sélectionnez un processus AEM Forms.

   * **Démarré après** (*facultatif*) : Sélectionnez une date. Filtre le rapport pour afficher les instances de processus qui ont commencé après la date spécifiée.

   * **Démarré avant** (*facultatif*) : Sélectionnez une date. Filtre le rapport pour afficher les instances de processus qui ont commencé avant la date spécifiée.

1. Cliquez sur **Aller **pour exécuter le rapport.

   Le rapport s’affiche dans le panneau **Rapport **situé à droite de la fenêtre **Process Reporting** .

   ![workflow_volume_report](assets/workflow_volume_report.png)

   Utilisez les options dans le coin supérieur droit du panneau **Rapport **pour effectuer les opérations suivantes sur le rapport.

   * **Actualiser**: Actualise le rapport avec les dernières données stockées
   * **Modifier la couleur** de la légende : Sélectionner et modifier la couleur de la légende du rapport
   * **Exporter au format CSV**: Exportez et téléchargez les données du rapport dans un fichier séparé par des virgules.

[Contacter le support technique](https://www.adobe.com/account/sign-in.supportportal.html)
