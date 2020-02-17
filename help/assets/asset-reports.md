---
title: Rapports sur vos ressources numériques
description: Comprenez les rapports sur vos ressources dans AEM Assets qui vous aident à comprendre l’utilisation, l’activité et le partage de vos ressources numériques.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 70a88085a0fd6e949974aa7f1f92fdc3def3d98e

---


# Rapports de ressources {#asset-reports}

La création de rapports de ressources est un outil essentiel pour évaluer l’utilité de votre déploiement Adobe Experience Manager (AEM) Assets. Avec AEM Assets, vous pouvez générer divers rapports pour vos ressources numériques. Les rapports fournissent des informations utiles concernant votre utilisation du système, la façon dont les utilisateurs interagissent avec les ressources et la façon dont les ressources sont téléchargées et partagées.

Utilisez les informations contenues dans les rapports pour dériver des mesures de réussite clés afin de mesurer l’adoption d’AEM Assets au sein de votre entreprise et par les clients.

La structure de création de rapports AEM Assets utilise les tâches Sling pour traiter les demandes de rapports de manière asynchrone et ordonnée. Elle est extensible pour les référentiels de grande taille. Le traitement asynchrone des rapports permet de générer des rapports de manière plus efficace et rapide.

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

1. Tap/click the AEM logo, and go to **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Reports]**.

![Rapport de navigation dans les fichiers](assets/AssetsReportNavigation.png)

1. In the Asset Reports page, tap/click **[!UICONTROL Create]** from the toolbar.
1. Sur la page **[!UICONTROL Créer un rapport]**, sélectionnez le rapport que vous souhaitez créer, puis appuyez/cliquez sur **[!UICONTROL Suivant]**.

   ![select_report](assets/choose_report.png)

   >[!NOTE]
   >
   >Avant de générer un rapport **[!UICONTROL Ressource téléchargée]**, assurez-vous que le service de téléchargement de ressources est activé. From the web console (`https://[aem_server]:[port]/system/console/configMgr`), open the **[!UICONTROL Day CQ DAM Event Recorder]** configuration, and select the **[!UICONTROL Asset Downloaded (DOWNLOADED)]** option in Event Types if not already selected.

   >[!NOTE]
   >
   >Par défaut, les fragments de contenu et les partages de lien sont inclus dans le rapport Ressource téléchargée. Sélectionnez l’option appropriée pour créer un rapport de partages de lien ou pour exclure les fragments de contenu du rapport de téléchargement. 

1. Configurez les détails du rapport, tels que le titre, la description, la miniature et le chemin du dossier dans le référentiel CRX où le rapport est stocké. By default, the folder path is */content/dam*. Vous pouvez spécifier un autre chemin.

   ![report_configuration](assets/report_configuration.png)

   Sélectionnez la période de votre rapport.

   Vous pouvez choisir de générer le rapport maintenant ou à une date et une heure ultérieures.

   >[!NOTE]
   >
   >Si vous décidez de planifier le rapport ultérieurement, veillez à spécifier la date et l’heure dans les champs Date et heure. Si vous ne spécifiez aucune valeur, le moteur de création de rapports traite le rapport comme devant être généré immédiatement.

   Les champs de configuration peuvent varier en fonction du type de rapport que vous créez. Par exemple, le rapport **[!UICONTROL Utilisation du disque]** fournit des options pour inclure les rendus de ressources lors du calcul de l’espace disque utilisé par les ressources. Vous pouvez choisir d’inclure ou d’exclure des fichiers dans des sous-dossiers pour le calcul de l’utilisation du disque.

   >[!NOTE]
   >
   >Le rapport **[!UICONTROL Utilisation du disque]** n’inclut pas les champs de période, car il indique uniquement l’utilisation actuelle de l’espace disque.

   ![disk_usage_configuration](assets/disk_usage_configuration.png)

   When you create the **[!UICONTROL Files]** report, you can include/exclude sub-folders. Cependant, vous ne pouvez pas inclure les rendus de ressources dans ce rapport.

   ![files_report](assets/files_report.png)

   Le rapport **[!UICONTROL Partage de liens]** affiche les URL des ressources qui sont partagées avec des utilisateurs externes à partir d’AEM Assets. Il inclut les adresses électroniques des utilisateurs ayant partagé les ressources et de ceux avec lesquels les ressources sont partagées, ainsi que la date de partage et la date d’expiration du lien. Les colonnes ne sont pas personnalisables.

   The **[!UICONTROL Link Share]** report, does not include options for sub-folders and renditions because it merely publishes the shared URLs that appear under `/var/dam/share`.

   ![link_share](assets/link_share.png)

1. Appuyez/cliquez sur **[!UICONTROL Suivant]** dans la barre d’outils.

1. Sur la page **[!UICONTROL Configurer les colonnes]**, certaines colonnes sont sélectionnées pour apparaître dans le rapport par défaut. Vous pouvez sélectionner d’autres colonnes. Désélectionnez une colonne sélectionnée pour l’exclure du rapport.

   ![configure_columns](assets/configure_columns.png)

   Pour afficher un nom de colonne personnalisé ou un chemin de propriété, configurez les propriétés du fichier binaire sous le noeud jcr:content dans CRX. Vous pouvez également l’ajouter via le sélecteur de chemin de propriété.

   ![custom_columns](assets/custom_columns.png)

1. Tap/click **[!UICONTROL Create]** from the toolbar. Un message indique que la génération du rapport a été lancée.
1. Dans la page Rapports sur les ressources, l’état de génération du rapport dépend de l’état actuel de la tâche du rapport, par exemple Succès, Echec, En file d’attente ou Planifié. Le même état s&#39;affiche dans la boîte de réception des notifications. Pour afficher la page du rapport, appuyez/cliquez sur le lien du rapport. Alternatively, select the report, and tap **[!UICONTROL View]** from the toolbar.

   ![report_page](assets/report_page.png)

   Tap **[!UICONTROL Download]** from the toolbar to download the report in CSV format.

## Ajout de colonnes personnalisées {#add-custom-columns}

Vous pouvez ajouter des colonnes personnalisées aux rapports suivants pour afficher davantage de données en fonction de vos besoins :

* Charger
* Téléchargement
* Expiration
* Modification
* Publier
* Publier sur Brand Portal
* Fichiers

1. Tap/click the AEM logo, and go to **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Reports]**.
1. In the Asset Reports page, tap/click **[!UICONTROL Create]** from the toolbar.

1. Sur la page **[!UICONTROL Créer un rapport]**, sélectionnez le rapport que vous souhaitez créer, puis appuyez/cliquez sur **[!UICONTROL Suivant]**.
1. Configurez les détails du rapport, tels que le titre, la description, la miniature, le chemin d’accès au dossier et la plage de dates, selon le cas.

1. Pour afficher une colonne personnalisée, spécifiez son nom sous **[!UICONTROL Colonnes personnalisées]**.

   ![custom_columns-1](assets/custom_columns-1.png)

1. Add the property path under the `jcr:content` node in CRXDE using the property path picker. Vous pouvez également saisir le chemin d’accès dans le champ de chemin d’accès à la propriété.

   ![property_picker](assets/property_picker.png)

   Pour ajouter d’autres colonnes personnalisées, appuyez/cliquez sur **[!UICONTROL Ajouter]** et répétez les étapes 5 et 6.

1. Tap/click **[!UICONTROL Create]** from the toolbar. Un message indique que la génération du rapport a été lancée.

## Configuration du service de purge {#configure-purging-service}

Pour supprimer les rapports dont vous n’avez plus besoin, configurez le service Purge des rapports de la gestion des actifs numériques à partir de la console web afin de purger les rapports existants en fonction de leur quantité et de leur âge.

1. Access the web console (configuration manager) from `https://[aem_server]:[port]/system/console/configMgr`.
1. Open the **[!UICONTROL DAM Report Purge Service]** configuration.
1. Specify the frequency (time interval) for the purging service in the `scheduler.expression.name` field. Vous pouvez également configurer l’âge et le seuil de quantité des rapports.
1. Enregistrez les modifications.
