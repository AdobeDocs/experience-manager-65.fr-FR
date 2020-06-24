---
title: Rapports sur l’utilisation et le partage de vos ressources numériques.
description: Rapports sur vos ressources [!DNL Adobe Experience Manager Assets] dans lesquels vous pouvez comprendre l’utilisation, l’activité et le partage de vos ressources numériques.
contentOwner: AG
translation-type: tm+mt
source-git-commit: a8c4bc1992a48dd01a3f58498e9e924dcc9e886a
workflow-type: tm+mt
source-wordcount: '1049'
ht-degree: 47%

---


# Rapports de ressources  {#asset-reports}

Le rapports des ressources vous permet d’évaluer l’utilité de votre [!DNL Adobe Experience Manager Assets] déploiement. Vous [!DNL Assets]pouvez générer divers rapports pour vos ressources numériques. Les rapports fournissent des informations utiles concernant votre utilisation du système, la façon dont les utilisateurs interagissent avec les ressources et la façon dont les ressources sont téléchargées et partagées.

Use the information in the reports to derive key success metrics to measure the adoption of [!DNL Assets] within your enterprise and by customers.

The [!DNL Assets] reporting framework uses [!DNL Sling] jobs to asynchronously process report requests in an ordered manner. Elle est extensible pour les référentiels de grande taille. Le traitement asynchrone des rapports permet de générer des rapports de manière plus efficace et rapide.

L’interface de gestion de rapports est intuitive et inclut des options et des commandes précises pour accéder aux rapports archivés, ainsi qu’afficher les états d’exécution des rapports (réussite, échec et en file d’attente).

Si un rapport est généré, vous êtes averti par un courrier électronique (facultatif) et une notification dans la boîte de réception. Vous pouvez afficher, télécharger ou supprimer un rapport de la page de liste des rapports, où tous les rapports précédemment générés sont affichés.

## Condition requise {#prerequisite-for-reporting}

Pour générer des rapports, veillez à ce que :

* Activez le service d’enregistrement [!UICONTROL de Événement DAM] Day CQ dans **[!UICONTROL Outils]** > **[!UICONTROL Opérations]** > Console **[!UICONTROL Web.]**
* Sélectionnez les activités ou les événements sur lesquels vous souhaitez effectuer un rapports. Par exemple, pour générer un rapport sur les ressources téléchargées, sélectionnez [!UICONTROL Ressource téléchargée (TÉLÉCHARGÉE)].

![Activer le rapports de ressources dans la console Web](assets/reports-config-day-cq-dam-event-recorder.png)

## Génération de rapports {#generate-reports}

[!DNL Experience Manager Assets] génère les rapports standard suivants pour vous :

* Charger
* Téléchargement
* Expiration
* Modification
* Publier
* [!DNL Brand Portal] publish
* Utilisation du disque
* Fichiers
* Partage de liens

[!DNL Adobe Experience Manager] les administrateurs peuvent facilement générer et personnaliser ces rapports pour votre mise en oeuvre. Un administrateur peut procéder comme suit pour générer un rapport :

1. Dans [!DNL Experience Manager] l’interface, cliquez sur **[!UICONTROL Outils]** > **[!UICONTROL Ressources]** > **[!UICONTROL Rapports]**.

![Page Outils pour parcourir le rapport des ressources](assets/AssetsReportNavigation.png)

1. On the [!UICONTROL Asset Reports] page, click **[!UICONTROL Create]** from the toolbar.
1. From the **[!UICONTROL Create Report]** page, choose the report you want to create and click **[!UICONTROL Next]**.

   ![Sélectionner le type de rapport](assets/choose_report.png)

   >[!NOTE]
   >
   >By default, the Content Fragments and link shares are included in the asset [!UICONTROL Download] report. Sélectionnez l’option appropriée pour créer un rapport de partages de lien ou pour exclure les fragments de contenu du rapport de téléchargement.

   >[!NOTE]
   >
   >Le rapport [!UICONTROL Télécharger] affiche uniquement les détails des ressources sélectionnées individuellement et téléchargées ou téléchargées à l’aide de l’action rapide. Cependant, il n’inclut pas les détails des ressources qui se trouvaient dans un dossier téléchargé.
1. Configurez les détails du rapport, tels que le titre, la description, la miniature et le chemin du dossier dans le référentiel CRX où le rapport est stocké. By default, the folder path is `/content/dam`. Vous pouvez spécifier un autre chemin.

   ![Page pour ajouter des détails sur le rapport](assets/report_configuration.png)

   Sélectionnez la période de votre rapport.

   Vous pouvez choisir de générer le rapport maintenant ou à une date et une heure ultérieures.

   >[!NOTE]
   >
   >Si vous choisissez de planifier le rapport ultérieurement, veillez à spécifier la date et l’heure dans les champs Date et heure. Si vous ne spécifiez aucune valeur, le moteur de création de rapports traite le rapport comme devant être généré immédiatement.

   Les champs de configuration peuvent varier en fonction du type de rapport que vous créez. Par exemple, le rapport **[!UICONTROL Utilisation du disque]** fournit des options pour inclure les rendus de ressources lors du calcul de l’espace disque utilisé par les ressources. Vous pouvez choisir d’inclure ou d’exclure des fichiers dans des sous-dossiers pour le calcul de l’utilisation du disque.

   >[!NOTE]
   >
   >Le rapport **[!UICONTROL Utilisation du disque]** n’inclut pas les champs de période, car il indique uniquement l’utilisation actuelle de l’espace disque.

   ![Page Détails du rapport d&#39;utilisation des disques](assets/disk_usage_configuration.png)

   When you create the **[!UICONTROL Files]** report, you can include/exclude sub-folders. Cependant, vous ne pouvez pas inclure les rendus de ressources dans ce rapport.

   ![Page Détails du rapport Fichiers](assets/files_report.png)

   The **[!UICONTROL Link Share]** report displays URLs to assets that are shared with external users from within [!DNL Assets]. Celui-ci comprend les ID de courrier électronique de l’utilisateur qui a partagé les ressources, les ID de courrier électronique des utilisateurs avec lesquels les ressources sont partagées, la date de partage et la date d’expiration du lien. Les colonnes ne sont pas personnalisables.

   The **[!UICONTROL Link Share]** report, does not include options for sub-folders and renditions because it merely publishes the shared URLs that appear under `/var/dam/share`.

   ![Page de détails du rapport Partage de liens](assets/link_share.png)

1. Click **[!UICONTROL Next]** from the toolbar.

1. Sur la page **[!UICONTROL Configurer les colonnes]**, certaines colonnes sont sélectionnées pour apparaître dans le rapport par défaut. Vous pouvez sélectionner d’autres colonnes. Désélectionnez une colonne sélectionnée pour l’exclure du rapport.

   ![Sélectionner ou désélectionner des colonnes de rapports](assets/configure_columns.png)

   To display a custom column name or property path, configure the properties for the asset binary under the `jcr:content` node in CRX. Vous pouvez également l’ajouter dans le sélecteur de chemin de propriété.

   ![Sélectionner ou désélectionner des colonnes de rapports](assets/custom_columns.png)

1. Click **[!UICONTROL Create]** from the toolbar. Un message indique que la génération du rapport a été lancée.
1. On the [!UICONTROL Asset Reports] page, the report generation status is based on the current state of the report job, for example [!UICONTROL Success], [!UICONTROL Failed], [!UICONTROL Queued], or [!UICONTROL Scheduled]. Le même état s&#39;affiche dans la boîte de réception des notifications. Pour vue à la page du rapport, cliquez sur le lien du rapport. Alternatively, select the report, and click **[!UICONTROL View]** from the toolbar.

   ![Un rapport généré](assets/report_page.png)

   Click **[!UICONTROL Download]** from the toolbar to download the report in CSV format.

## Ajout de colonnes personnalisées  {#add-custom-columns}

Vous pouvez ajouter des colonnes personnalisées aux rapports suivants pour afficher davantage de données en fonction de vos besoins :

* Charger
* Téléchargement
* Expiration
* Modification
* Publier
* [!DNL Brand Portal] publish
* Fichiers

Pour ajouter des colonnes personnalisées à ces rapports, procédez comme suit :

1. Dans le [!DNL Manager interface]menu, cliquez sur **[!UICONTROL Outils]** > **[!UICONTROL Ressources]** > **[!UICONTROL Rapports]**.
1. On the [!UICONTROL Asset Reports] page, click **[!UICONTROL Create]** from the toolbar.

1. From the **[!UICONTROL Create Report]** page, choose the report you want to create and click **[!UICONTROL Next]**.
1. Configurez les détails du rapport, tels que le titre, la description, la miniature, le chemin d’accès au dossier et la plage de dates, le cas échéant.

1. Pour afficher une colonne personnalisée, spécifiez son nom sous **[!UICONTROL Colonnes personnalisées]**.

   ![Spécifier le nom de la colonne personnalisée du rapport](assets/custom_columns-1.png)

1. Ajoutez le chemin de la propriété sous le nœud `jcr:content` dans CRXDE à l’aide du sélecteur de chemin de propriété. Vous pouvez également saisir le chemin d’accès dans le champ de chemin d’accès à la propriété.

   ![Faites correspondre le chemin d’accès à la propriété des chemins dans jcr:content](assets/property_picker.png)

   To add more custom columns, click **[!UICONTROL Add]** and repeat steps 5 and 6.

1. Click **[!UICONTROL Create]** from the toolbar. Un message indique que la génération du rapport a été lancée.

## Configuration du service de purge {#configure-purging-service}

Pour supprimer les rapports dont vous n’avez plus besoin, configurez le service Purge des rapports de la gestion des actifs numériques à partir de la console web afin de purger les rapports existants en fonction de leur quantité et de leur âge.

1. Accédez à la console web (Configuration Manager) à partir de `https://[aem_server]:[port]/system/console/configMgr`.
1. Ouvrez la configuration **[!UICONTROL Service de purge des rapports de la gestion des actifs numériques]**.
1. Spécifiez la fréquence (intervalle) pour le service de purge dans le champ `scheduler.expression.name`. Vous pouvez également configurer l’âge et le seuil de quantité des rapports.
1. Enregistrez les modifications.
