---
title: Rapports sur vos ressources numériques
description: Comprenez les rapports sur vos ressources dans AEM Assets qui vous aident à comprendre l’utilisation, l’activité et le partage de vos ressources numériques.
contentOwner: AG
translation-type: tm+mt
source-git-commit: f66be5de3bbd0051cd677430d5187ace9337b98d
workflow-type: tm+mt
source-wordcount: '977'
ht-degree: 70%

---


# Rapports de ressources  {#asset-reports}

La création de rapports de ressources est un outil essentiel pour évaluer l’utilité de votre déploiement Adobe Experience Manager (AEM) Assets. Avec AEM Assets, vous pouvez générer divers rapports pour vos ressources numériques. Les rapports fournissent des informations utiles concernant votre utilisation du système, la façon dont les utilisateurs interagissent avec les ressources et la façon dont les ressources sont téléchargées et partagées.

Utilisez les informations figurant dans les rapports de manière à obtenir des mesures de succès essentielles pour évaluer l’adoption d’AEM Assets au sein de votre entreprise et par les clients.

La structure de rapports AEM Assets utilise les tâches Sling pour traiter les demandes de rapports de manière asynchrone et ordonnée. Elle est extensible pour les référentiels de grande taille. Le traitement asynchrone des rapports permet de générer des rapports de manière plus efficace et rapide.

L’interface de gestion de rapports est intuitive et inclut des options et des commandes précises pour accéder aux rapports archivés, ainsi qu’afficher les états d’exécution des rapports (réussite, échec et en file d’attente).

Si un rapport est généré, vous êtes averti par un courrier électronique (facultatif) et une notification dans la boîte de réception. Vous pouvez afficher, télécharger ou supprimer un rapport de la page de liste des rapports, où tous les rapports précédemment générés sont affichés.

## Génération de rapports {#generate-reports}

AEM Assets génère les rapports standard suivants :

* Charger
* Téléchargement
* Expiration
* Modification
* Publier
* Publier sur Brand Portal
* Utilisation du disque
* Fichiers
* Partage de liens

Les administrateurs d’AEM peuvent facilement générer et personnaliser ces rapports pour votre implémentation. Un administrateur peut procéder comme suit pour générer un rapport :

1. Dans l’interface d’Experience Manager, cliquez sur **[!UICONTROL Outils]** > **[!UICONTROL Ressources]** > **[!UICONTROL Rapports]**.
   ![](assets/AssetsReportNavigation.png)

1. On the [!UICONTROL Asset Reports] page, click **[!UICONTROL Create]** from the toolbar.
1. From the **[!UICONTROL Create Report]** page, choose the report you want to create and click **[!UICONTROL Next]**.

   ![](assets/choose_report.png)

   >[!NOTE]
   >
   >Avant de générer un rapport **[!UICONTROL Ressource téléchargée]**, assurez-vous que le service de téléchargement de ressources est activé. Dans la console web (`https://[aem_server]:[port]/system/console/configMgr`), ouvrez la configuration **[!UICONTROL Enregistreur d’événements de la gestion des actifs numériques Day CQ]** et, le cas échéant, sélectionnez l’option **[!UICONTROL Ressource téléchargée (TÉLÉCHARGÉE)]** dans Types d’événement.

   >[!NOTE]
   >
   >Par défaut, les fragments de contenu et les partages de lien sont inclus dans le rapport Ressource téléchargée. Sélectionnez l’option appropriée pour créer un rapport de partages de lien ou pour exclure les fragments de contenu du rapport de téléchargement.

1. Configurez les détails du rapport, tels que le titre, la description, la miniature et le chemin du dossier dans le référentiel CRX où le rapport est stocké. By default, the folder path is `/content/dam`. Vous pouvez spécifier un autre chemin.

   ![](assets/report_configuration.png)

   Sélectionnez la période de votre rapport.

   Vous pouvez choisir de générer le rapport maintenant ou à une date et une heure ultérieures.

   >[!NOTE]
   >
   >Si vous choisissez de planifier le rapport ultérieurement, veillez à spécifier la date et l’heure dans les champs Date et heure. Si vous ne spécifiez aucune valeur, le moteur de création de rapports traite le rapport comme devant être généré immédiatement.

   Les champs de configuration peuvent varier en fonction du type de rapport que vous créez. Par exemple, le rapport **[!UICONTROL Utilisation du disque]** fournit des options pour inclure les rendus de ressources lors du calcul de l’espace disque utilisé par les ressources. Vous pouvez choisir d’inclure ou d’exclure des fichiers dans des sous-dossiers pour le calcul de l’utilisation du disque.

   >[!NOTE]
   >
   >Le rapport **[!UICONTROL Utilisation du disque]** n’inclut pas les champs de période, car il indique uniquement l’utilisation actuelle de l’espace disque.

   ![](assets/disk_usage_configuration.png)

   When you create the **[!UICONTROL Files]** report, you can include/exclude sub-folders. Cependant, vous ne pouvez pas inclure les rendus de ressources dans ce rapport.

   ![](assets/files_report.png)

   Le rapport **[!UICONTROL Partage de liens]** affiche des URL vers des ressources partagées avec des utilisateurs externes à partir d’AEM Assets. Celui-ci comprend les ID de courrier électronique de l’utilisateur qui a partagé les ressources, les ID de courrier électronique des utilisateurs avec lesquels les ressources sont partagées, la date de partage et la date d’expiration du lien. Les colonnes ne sont pas personnalisables.

   The **[!UICONTROL Link Share]** report, does not include options for sub-folders and renditions because it merely publishes the shared URLs that appear under `/var/dam/share`.

   ![](assets/link_share.png)

1. Click **[!UICONTROL Next]** from the toolbar.

1. Sur la page **[!UICONTROL Configurer les colonnes]**, certaines colonnes sont sélectionnées pour apparaître dans le rapport par défaut. Vous pouvez sélectionner d’autres colonnes. Désélectionnez une colonne sélectionnée pour l’exclure du rapport.

   ![](assets/configure_columns.png)

   Pour afficher un chemin de propriété ou un nom de colonne personnalisé, configurez les propriétés du binaire de ressource sous le nœud jcr:content dans CRX. Vous pouvez également l’ajouter dans le sélecteur de chemin de propriété.

   ![](assets/custom_columns.png)

1. Click **[!UICONTROL Create]** from the toolbar. Un message indique que la génération du rapport a été lancée.
1. Sur la page Rapports de ressources, l’état de la génération des rapports repose sur l’état actuel de la tâche de rapport, par exemple, Réussite, Échec, En file d’attente ou Planifié. Le même état s&#39;affiche dans la boîte de réception des notifications. Pour vue à la page du rapport, cliquez sur le lien du rapport. Alternatively, select the report, and click **[!UICONTROL View]** from the toolbar.

   ![](assets/report_page.png)

   Click **[!UICONTROL Download]** from the toolbar to download the report in CSV format.

## Ajout de colonnes personnalisées  {#add-custom-columns}

Vous pouvez ajouter des colonnes personnalisées aux rapports suivants pour afficher davantage de données en fonction de vos besoins :

* Charger
* Téléchargement
* Expiration
* Modification
* Publier
* Publier sur Brand Portal
* Fichiers

Pour ajouter des colonnes personnalisées à ces rapports, procédez comme suit :

1. Dans l’interface d’Experience Manager, cliquez sur **[!UICONTROL Outils]** > **[!UICONTROL Ressources]** > **[!UICONTROL Rapports]**.
1. On the [!UICONTROL Asset Reports] page, click **[!UICONTROL Create]** from the toolbar.

1. From the **[!UICONTROL Create Report]** page, choose the report you want to create and click **[!UICONTROL Next]**.
1. Configurez les détails du rapport, tels que le titre, la description, la miniature, le chemin d’accès au dossier et la plage de dates, le cas échéant.

1. Pour afficher une colonne personnalisée, spécifiez son nom sous **[!UICONTROL Colonnes personnalisées]**.

   ![](assets/custom_columns-1.png)

1. Ajoutez le chemin de la propriété sous le nœud `jcr:content` dans CRXDE à l’aide du sélecteur de chemin de propriété. Vous pouvez également saisir le chemin d’accès dans le champ de chemin d’accès à la propriété.

   ![](assets/property_picker.png)

   To add more custom columns, click **[!UICONTROL Add]** and repeat steps 5 and 6.

1. Click **[!UICONTROL Create]** from the toolbar. Un message indique que la génération du rapport a été lancée.

## Configuration du service de purge {#configure-purging-service}

Pour supprimer les rapports dont vous n’avez plus besoin, configurez le service Purge des rapports de la gestion des actifs numériques à partir de la console web afin de purger les rapports existants en fonction de leur quantité et de leur âge.

1. Accédez à la console web (Configuration Manager) à partir de `https://[aem_server]:[port]/system/console/configMgr`.
1. Ouvrez la configuration **[!UICONTROL Service de purge des rapports de la gestion des actifs numériques]**.
1. Spécifiez la fréquence (intervalle) pour le service de purge dans le champ `scheduler.expression.name`. Vous pouvez également configurer l’âge et le seuil de quantité des rapports.
1. Enregistrez les modifications.
