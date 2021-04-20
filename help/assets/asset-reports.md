---
title: Rapports sur l’utilisation et le partage des ressources
description: Des rapports sur vos ressources dans  [!DNL Adobe Experience Manager Assets]  vous permettent de comprendre l’utilisation, l’activité et le partage de vos ressources numériques.
contentOwner: AG
role: Business Practitioner, Administrator
feature: Asset Reports,Asset Management
translation-type: tm+mt
source-git-commit: aec4530fa93eacd151ca069c2da5d1bc92408e10
workflow-type: tm+mt
source-wordcount: '1146'
ht-degree: 88%

---


# Rapports de ressources {#asset-reports}

Les rapports de ressources vous permettent d’évaluer l’utilité de votre déploiement [!DNL Adobe Experience Manager Assets]. Avec [!DNL Assets], vous pouvez générer divers rapports pour vos ressources numériques. Les rapports fournissent des informations utiles concernant votre utilisation du système, la façon dont les utilisateurs interagissent avec les ressources et la façon dont les ressources sont téléchargées et partagées.

Utilisez les informations figurant dans les rapports de manière à obtenir des mesures de succès essentielles pour évaluer l’adoption d’[!DNL Assets] au sein de votre entreprise et par les clients.

Le framework de création de rapports [!DNL Assets] exploite des tâches [!DNL Sling] de façon à traiter de manière asynchrone les demandes de rapports en respectant l’ordre. Il est extensible pour les référentiels de grande taille. Le traitement asynchrone des rapports permet de générer des rapports de manière plus efficace et rapide.

L’interface de gestion de rapports est intuitive et inclut des options et des commandes précises pour accéder aux rapports archivés, ainsi qu’afficher les états d’exécution des rapports (réussite, échec et en file d’attente).

Si un rapport est généré, vous êtes averti par un courrier électronique (facultatif) et une notification dans la boîte de réception. Vous pouvez afficher, télécharger ou supprimer un rapport de la page de liste des rapports, où tous les rapports précédemment générés sont affichés.

## Prérequis {#prerequisite-for-reporting}

Pour générer des rapports, procédez comme suit :

* Activez le service [!UICONTROL Day CQ DAM Événement Recorder] depuis **[!UICONTROL Outils]** > **[!UICONTROL Opérations]** > **[!UICONTROL Console Web]**.
* Sélectionnez les activités ou les événements sur lesquels vous souhaitez effectuer un rapports. Par exemple, pour générer un rapport sur les ressources téléchargées, sélectionnez [!UICONTROL Ressource téléchargée (TÉLÉCHARGÉE)].

![Activer le rapports de ressources dans la console Web](assets/reports-config-day-cq-dam-event-recorder.png)

## Génération de rapports {#generate-reports}

[!DNL Experience Manager Assets] génère les rapports standard suivants :

* Chargement
* Téléchargement
* Expiration
* Modification
* Publication
* Publier sur [!DNL Brand Portal]
* Utilisation du disque
* Fichiers
* Partage de liens

Les administrateurs d’[!DNL Adobe Experience Manager] peuvent facilement générer et personnaliser ces rapports pour votre implémentation. Un administrateur peut procéder comme suit pour générer un rapport :

1. Dans l’interface [!DNL Experience Manager], cliquez sur **[!UICONTROL Outils]** > **[!UICONTROL Ressources]** > **[!UICONTROL Rapports]**.

   ![Page Outils pour parcourir le rapport des ressources](assets/AssetsReportNavigation.png)

1. Sur la page [!UICONTROL Rapports de ressources], cliquez sur **[!UICONTROL Créer]** dans la barre d’outils.
1. Sur la page **[!UICONTROL Créer un rapport]**, sélectionnez le rapport que vous souhaitez créer, puis cliquez sur **[!UICONTROL Suivant]**.

   ![Sélectionner le type de rapport](assets/choose_report.png)

   >[!NOTE]
   >
   >Par défaut, les fragments de contenu et les partages de lien sont inclus dans le rapport [!UICONTROL Ressource téléchargée]. Sélectionnez l’option appropriée pour créer un rapport de partages de lien ou pour exclure les fragments de contenu du rapport de téléchargement.

   >[!NOTE]
   >
   >Le rapport [!UICONTROL Télécharger] affiche uniquement les détails des ressources téléchargées après sélection individuelle ou téléchargées à l’aide de l’action rapide. Cependant, il n’inclut pas les détails des ressources figurant dans un dossier téléchargé.

1. Configurez les détails du rapport, tels que le titre, la description, la miniature et le chemin du dossier dans le référentiel CRX où le rapport est stocké. Par défaut, le chemin du dossier est `/content/dam`. Vous pouvez spécifier un autre chemin.

   ![Page d’ajout de détails de rapport](assets/report_configuration.png)

   Sélectionnez la période de votre rapport.

   Vous pouvez choisir de générer le rapport maintenant ou à une date et une heure ultérieures.

   >[!NOTE]
   >
   >Si vous choisissez de planifier le rapport à une date ultérieure, veillez à spécifier la date et l’heure dans les champs Date et Heure. Si vous ne spécifiez aucune valeur, le moteur de création de rapports traite le rapport comme devant être généré immédiatement.

   Les champs de configuration peuvent varier en fonction du type de rapport que vous créez. Par exemple, le rapport **[!UICONTROL Utilisation du disque]** fournit des options pour inclure les rendus de ressources lors du calcul de l’espace disque utilisé par les ressources. Vous pouvez choisir d’inclure ou d’exclure les ressources figurant dans les sous-dossiers pour le calcul de l’utilisation du disque.

   >[!NOTE]
   >
   >Le rapport **[!UICONTROL Utilisation du disque]** n’inclut pas les champs de période, car il indique uniquement l’utilisation actuelle de l’espace disque.

   ![Page Détails du rapport Utilisation du disque](assets/disk_usage_configuration.png)

   Lorsque vous créez le rapport **[!UICONTROL Fichiers]**, vous pouvez inclure/exclure les sous-dossiers. Cependant, vous ne pouvez pas inclure les rendus de ressources dans ce rapport.

   ![Page Détails du rapport Fichiers](assets/files_report.png)

   Le rapport **[!UICONTROL Partage de liens]** affiche les URL des ressources qui sont partagées avec des utilisateurs externes à partir d’[!DNL Assets]. Celui-ci comprend les ID de courrier électronique de l’utilisateur qui a partagé les ressources, les ID de courrier électronique des utilisateurs avec lesquels les ressources sont partagées, la date de partage et la date d’expiration du lien. Les colonnes ne sont pas personnalisables.

   Le rapport **[!UICONTROL Partage de liens]** n’inclut pas d’options pour les sous-dossiers et les rendus, car il ne publie que les URL partagées qui apparaissent sous `/var/dam/share`.

   ![Page Détails du rapport Partage de liens](assets/link_share.png)

1. Cliquez sur **[!UICONTROL Suivant]** dans la barre d’outils.

1. Sur la page **[!UICONTROL Configurer les colonnes]**, certaines colonnes sont sélectionnées pour apparaître dans le rapport par défaut. Vous pouvez sélectionner plus de colonnes. Annule la sélection d&#39;une colonne pour l&#39;exclure dans le rapport.

   ![Sélectionner ou annuler la sélection des colonnes de rapports](assets/configure_columns.png)

   Pour afficher un chemin de propriété ou un nom de colonne personnalisé, configurez les propriétés du binaire de ressource sous le nœud `jcr:content` dans CRX. Vous pouvez également l’ajouter dans le sélecteur de chemin de propriété.

   ![Sélectionner ou annuler la sélection des colonnes de rapports](assets/custom_columns.png)

1. Cliquez sur **[!UICONTROL Créer]** dans la barre d’outils. Un message indique que la génération du rapport a été lancée.
1. Sur la page [!UICONTROL Rapports de ressources], l’état de la génération des rapports repose sur l’état actuel de la tâche de rapport ; par exemple [!UICONTROL Réussite], [!UICONTROL Échec], [!UICONTROL En file d’attente] ou [!UICONTROL Planifié]. Le même état s’affiche dans la boîte de réception des notifications. Pour afficher la page du rapport, cliquez sur le lien du rapport. Vous pouvez également sélectionner le rapport et cliquer sur **[!UICONTROL Afficher]** dans la barre d’outils.

   ![Un rapport généré](assets/report_page.png)

   Cliquez sur **[!UICONTROL Télécharger]** dans la barre d’outils pour télécharger le rapport au format CSV.

## Ajout de colonnes personnalisées {#add-custom-columns}

Vous pouvez ajouter des colonnes personnalisées aux rapports suivants pour afficher davantage de données en fonction de vos besoins :

* Chargement
* Téléchargement
* Expiration
* Modification
* Publication
* Publier sur [!DNL Brand Portal]
* Fichiers

Pour ajouter des colonnes personnalisées à ces rapports, procédez comme suit :

1. Dans le [!DNL Manager interface], cliquez sur **[!UICONTROL Outils]** > **[!UICONTROL Ressources]** > **[!UICONTROL Rapports]**.
1. Sur la page [!UICONTROL Rapports de ressources], cliquez sur **[!UICONTROL Créer]** dans la barre d’outils.

1. Sur la page **[!UICONTROL Créer un rapport]**, sélectionnez le rapport que vous souhaitez créer, puis cliquez sur **[!UICONTROL Suivant]**.
1. Configurez les détails du rapport, tels que le titre, la description, la miniature, le chemin du dossier et la période, le cas échéant.

1. Pour afficher une colonne personnalisée, spécifiez son nom sous **[!UICONTROL Colonnes personnalisées]**.

   ![Spécifier le nom de la colonne personnalisée du rapport](assets/custom_columns-1.png)

1. Ajoutez le chemin de la propriété sous le nœud `jcr:content` dans CRXDE à l’aide du sélecteur de chemin de propriété. Vous pouvez également saisir le chemin d’accès dans le champ de chemin d’accès à la propriété.

   ![Faites correspondre le chemin de la propriété des chemins dans jcr:content](assets/property_picker.png)

   Pour ajouter d’autres colonnes personnalisées, cliquez sur **[!UICONTROL Ajouter]** et répétez les étapes 5 et 6.

1. Cliquez sur **[!UICONTROL Créer]** dans la barre d’outils. Un message indique que la génération du rapport a été lancée.

## Configuration du service de purge {#configure-purging-service}

Pour supprimer les rapports dont vous n’avez plus besoin, configurez le service Purge des rapports de la gestion des actifs numériques à partir de la console web afin de purger les rapports existants en fonction de leur quantité et de leur âge.

1. Accédez à la console web (Configuration Manager) à partir de `https://[aem_server]:[port]/system/console/configMgr`.
1. Ouvrez la configuration **[!UICONTROL Service de purge des rapports de la gestion des actifs numériques]**.
1. Spécifiez la fréquence (intervalle) pour le service de purge dans le champ `scheduler.expression.name`. Vous pouvez également configurer l’âge et le seuil de quantité des rapports.
1. Enregistrez les modifications.

## Informations, conseils et limites de dépannage {#best-practices-and-limitations}

* Si certains rapports ou nombres des rapports ne sont pas disponibles ou comme prévu, veillez à ce que le service [!UICONTROL Enregistreur de Événement DAM CQ Day ] soit activé.

* Supprimez les rapports qui ne sont plus requis. Utilisez les options de configuration du service de purge de rapports DAM pour configurer les critères de purge des rapports.

* Si le rapport d’utilisation des disques n’est pas généré et si vous utilisez [!DNL Dynamic Media], assurez-vous que toutes les ressources sont traitées correctement. Pour résoudre ce problème, retraitez les ressources puis générez de nouveau le rapport.
