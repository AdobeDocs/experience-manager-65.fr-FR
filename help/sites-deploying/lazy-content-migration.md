---
title: Migration différée du contenu
description: Découvrez la migration différée du contenu dans Adobe Experience Manager 6.4.
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: upgrading
docset: aem65
feature: Upgrading
exl-id: 946c7c2a-806b-4461-a38b-9c2e5ef1e958
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '693'
ht-degree: 100%

---

# Migration différée du contenu {#lazy-content-migration}

Pour des raisons de rétrocompatibilité, le contenu et la configuration situés dans **/etc** et **/content** ne seront pas modifiés ni transformés immédiatement par la mise à niveau à partir d’Adobe Experience Manager (AEM) 6.3. Cela permet de s’assurer que les dépendances des applications des clientes et clients sur ces structures restent intactes. Les fonctionnalités relatives à ces structures de contenu restent les mêmes, même si du contenu AEM 6.5 prêt à l’emploi est hébergé à un autre endroit.

Bien que ces emplacements ne soient pas tous transformés automatiquement, il existe quelques `CodeUpgradeTasks` différées ; ce que l’on désigne sous le nom de migration différée du contenu. Cela permet aux utilisateurs de déclencher ces transformations automatiques en redémarrant l’instance avec cette propriété système :

```shell
-Dcom.adobe.upgrade.forcemigration=true
```

Cela entraîne l’exécution de `CodeUpgradeTasks` pendant la migration.

Bien que l’objectif soit une exécution efficace, ce processus de mise à niveau est synchrone et s’accompagne donc d’un temps d’arrêt en fonction de la quantité de contenu à traiter. Adobe vous conseille d’évaluer les temps d’exécution dans un environnement d’évaluation en amont du système de production afin de planifier une fenêtre de maintenance adéquate.

Comme cela nécessite généralement d’ajuster l’application, cette activité doit être effectuée lors du déploiement d’application correspondant.

Vous trouverez, ci-dessous, la liste complète des `CodeUpgradeTasks` introduites dans la version 6.5 :

| **Nom** | **Concerne** **les versions AEM antérieures à** | **Type de** **migration** | **Détails** |
|---|---|---|---|
| `Cq561ProjectContentUpgrade` | &lt; 5.6.1 | Immédiat |  |
| `Cq60MSMContentUpgrade` | &lt; 6.0 | Immédiat | Détecte toutes les `LiveRelationShips` de `VersionStorage` qui ont été supprimées et ajoute une propriété d’exclusion au parent. |
| `Cq61CloudServicesContentUpgrade` | &lt; 6.1 | Immédiat | Restructuration des services cloud pour une configuration sécurisée par défaut |
| `Cq62ConfContentUpgrade` | &lt; 6.2 | Immédiat | Supprime la liaison basée sur les propriétés entre **/content** et **/conf** (remplacée par le mécanisme OSGi), génère la configuration OSGi correspondante. |
| `Cq62FormsContentUpgrade` | &lt; 6.2 | Immédiat | En raison de la gestion via merge_preserve, la règle de refus de sécurisation par défaut remplace les autorisations données, ce qui entraîne la nécessité d’une réorganisation lors de la mise à niveau. |
| `CQ62Html5SmartFileUpgrade` | &lt; 6.2 | Immédiat | Détecte les composants à l’aide du widget Html5SmartFile, recherche les utilisations du composant dans le contenu et restructure la persistance, en déplaçant le fichier binaire d’un niveau vers le bas et en ne le stockant pas au niveau du composant. |
| `Cq62ProjectsCodeUpgrade` | &lt; 6.2 | Immédiat | Déplace les anciens types de projets de **/etc/projects** vers **/content/projects**. |
| `Cq62TargetCampaignsContentUpgrade` | &lt; 6.2 | Immédiat | Crée une couche de conteneur dans la hiérarchie (Zones) et ajuste les références. |
| `Cq62TargetContentUpgrade` | &lt; 6.2 | Immédiat | Définit des noms d’emplacement fixes pour les composants cibles. |
| `Cq62WorkflowContentUpgrade` | &lt; 6.2 | Immédiat | Transformation complexe des modèles de workflow antérieurs aux structures, instances et notifications de la version 6.2, puis fusion à partir de l’emplacement de sauvegarde, à partir de **/var/backup**. |
| `CQ63AssetsMetadataFormsUpdate` | &lt; 6.3 | Immédiat | Déplace les ressources, les schémas de métadonnées personnalisés et les profils de traitement de **/apps** vers **/conf** et convertit les formulaires de schémas de métadonnées et de profils de métadonnées de coral2 à coral3. |
| `CQ63AssetsSearchFacetsUpdate` | &lt; 6.3 | Immédiat | Déplace les ressources et les facettes de recherche personnalisées de **/apps** vers **/conf** et convertit les formulaires de profils de métadonnées et de schéma de métadonnées de coral2 à coral3. |
| `CQ63InboxItemsUpgrade` | &lt; 6.3 | Immédiat | Met à jour InboxItems pour l’ordre des éléments de la boîte de réception (avec ajustement des métadonnées pour un tri efficace). |
| `CQ63MetadataSchemaConfigUpdate` | &lt; 6.3 | Immédiat | Ajuste la propriété metadataSchema sur le dossier en remplaçant les chemins relatifs par **/conf** à la place de **/apps**. |
| `CQ63MobileAppsNavUpgrade` | &lt; 6.3 | Immédiat | Ajuster la structure de navigation |
| `CQ63MonitoringDashboardsConfigUpdate` | &lt; 6.3 | Immédiat | Déplace les configurations personnalisées des tableaux de bord de surveillance à partir de **/libs** et **/apps**. |
| `CQ63ProcessingProfileConfigUpdate` | &lt; 6.3 | Immédiat | Convertit la propriété processingProfile (utilisée jusqu’à la version 6.1) dans Assets afin qu’elle corresponde à la structure de la version 6.3 et des versions ultérieures. Ajuste également les chemins relatifs du profil à **/conf** à la place de **/apps**. |
| `CQ63ToolsMenuEntriesContentUpgrade` | &lt; 6.3 | Immédiat | Tâche de mise à niveau qui supprime les entrées de menu obsolètes de CRXDE Lite et de la console web en cas de mise à niveau. |
| `CQ64CommunitiesConfigsCleanupTask` | &lt; 6.3 | Différé | Déplacement des configurations cloud SRP, des configurations de mots-clés communautaires, nettoyage de **/etc/social** et **/etc/enablement** (toutes les références et données doivent être ajustées lors de l’exécution de la migration différée ; aucune partie de l’application ne doit plus dépendre de cette structure). |
| `CQ64LegacyCloudSettingsCleanupTask` | &lt; 6.4 | Différé | Nettoie **/etc/cloudsettings** (contenant la configuration ContextHub). La configuration est automatiquement migrée lors du premier accès. Si la migration différée du contenu est lancée avec la mise à niveau, ce contenu dans **/etc/cloudsettings** doit être conservé via le package avant la mise à niveau et réinstallé pour que la transformation implicite entre en jeu, avec une désinstallation ultérieure du package après l’achèvement. |
| `CQ64UsersTitleFixTask` | &lt; 6.4 | Différé | Ajuste la structure de titre héritée au titre dans le nœud de profil d’utilisateur ou d’utilisatrice. |
| `CQ64CommerceMigrationTask` | &lt; 6.4 | Différé | Migration du contenu commercial depuis **/etc/commerce** vers **/var/commerce**. Lors de la migration, le contenu est déplacé et les références au contenu déplacé sont mises à jour pour refléter le nouvel emplacement. |
| `CQ65DMMigrationTask` | &lt; 6.5 | Différé | Migration des paramètres de catalogue hérités et des paramètres des services cloud Dynamic Media depuis **/etc** vers **/conf** |
| `CQ65LegacyClientlibsCleanupTask` | &lt; 6.5 | Différé | Nettoyage des clientlibs héritées existantes sous **/etc/clientlibs**. |
