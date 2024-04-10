---
title: Migration différée du contenu
description: Découvrez la migration différée du contenu dans Adobe Experience Manager 6.4.
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
ht-degree: 23%

---

# Migration différée du contenu {#lazy-content-migration}

Pour des raisons de rétrocompatibilité, le contenu et la configuration dans **/etc** et **/content** à compter de Adobe Experience Manager (AEM) 6.3, la mise à niveau n’aura pas d’incidence ou ne transformera pas immédiatement. Cela permet de s’assurer que les dépendances des applications clientes sur ces structures restent intactes. La fonctionnalité relative à ces structures de contenu reste la même, même si le contenu d’une version AEM 6.5 prête à l’emploi est hébergé dans un autre emplacement.

Bien que ces emplacements ne soient pas tous transformés automatiquement, il existe quelques `CodeUpgradeTasks` différées ; ce que l’on désigne sous le nom de migration différée du contenu. Cela permet aux utilisateurs de déclencher ces transformations automatiques en redémarrant l’instance avec cette propriété système :

```shell
-Dcom.adobe.upgrade.forcemigration=true
```

Cela entraîne la `CodeUpgradeTasks` à exécuter pendant la migration.

Bien que l’objectif soit une exécution efficace, ce processus de mise à niveau est synchrone et s’accompagne donc d’un temps d’arrêt qui dépend de la quantité de contenu à traiter. Adobe recommande d’évaluer les temps d’exécution sur un environnement d’évaluation en amont d’un système de production afin de planifier une fenêtre de maintenance correspondante.

Comme cela nécessite généralement d’ajuster l’application, cette activité doit être effectuée avec le déploiement d’application correspondant.

Vous trouverez, ci-dessous, la liste complète des `CodeUpgradeTasks` introduites dans la version 6.5 :

| **Nom** | **Pertinent** **pour les versions AEM antérieures à** | **Migration** **Type** | **Détails** |
|---|---|---|---|
| `Cq561ProjectContentUpgrade` | &lt; 5.6.1 | Immédiat |  |
| `Cq60MSMContentUpgrade` | &lt; 6.0 | Immédiat | Détecte toutes les `LiveRelationShips` de `VersionStorage` qui ont été supprimées et ajoute une propriété d’exclusion au parent. |
| `Cq61CloudServicesContentUpgrade` | &lt; 6.1 | Immédiat | Restructure les services cloud pour une configuration sécurisée par défaut. |
| `Cq62ConfContentUpgrade` | &lt; 6.2 | Immédiat | Supprime la liaison basée sur la propriété de **/content** vers **/conf** (remplacé par le mécanisme OSGi), génère la configuration OSGi correspondante |
| `Cq62FormsContentUpgrade` | &lt; 6.2 | Immédiat | En raison de la gestion de merge_preserve, la règle de refus sécurisée par défaut remplace les autorisations données, ce qui nécessite de réorganiser la mise à niveau |
| `CQ62Html5SmartFileUpgrade` | &lt; 6.2 | Immédiat | Détecte les composants à l’aide du widget Html5SmartFile, recherche les utilisations du composant dans le contenu et restructure la persistance, déplaçant efficacement le binaire d’un niveau vers le bas et ne le stockant pas au niveau du composant. |
| `Cq62ProjectsCodeUpgrade` | &lt; 6.2 | Immédiat | Déplace les projets de style ancien depuis **/etc/projects** vers **/content/projects** |
| `Cq62TargetCampaignsContentUpgrade` | &lt; 6.2 | Immédiat | Ajoute un calque de conteneur à la hiérarchie (zones) et ajuste les références. |
| `Cq62TargetContentUpgrade` | &lt; 6.2 | Immédiat | Définit des noms d’emplacement fixes sur les composants cibles. |
| `Cq62WorkflowContentUpgrade` | &lt; 6.2 | Immédiat | Transformation complexe de modèles de workflow antérieurs à la version 6.2 des structures, instances et notifications, puis refusion à partir de l’emplacement de sauvegarde à partir de **/var/backup** |
| `CQ63AssetsMetadataFormsUpdate` | &lt; 6.3 | Immédiat | Déplace les ressources, les schémas de métadonnées personnalisés et les profils de traitement depuis **/apps** vers **/conf** et traduit le schéma de métadonnées et les formulaires de profils de métadonnées de coral2 vers coral3. |
| `CQ63AssetsSearchFacetsUpdate` | &lt; 6.3 | Immédiat | Déplace les ressources et les facettes de recherche personnalisées depuis **/apps** vers **/conf** et traduit le schéma de métadonnées et les formulaires de profils de métadonnées de coral2 vers coral3. |
| `CQ63InboxItemsUpgrade` | &lt; 6.3 | Immédiat | Met à jour InboxItems pour classer les éléments de boîte de réception (ajustement des métadonnées pour un tri efficace) |
| `CQ63MetadataSchemaConfigUpdate` | &lt; 6.3 | Immédiat | Ajuste la propriété metadataSchema sur le dossier en remplaçant les chemins relatifs par . **/conf** à la place de **/apps** |
| `CQ63MobileAppsNavUpgrade` | &lt; 6.3 | Immédiat | Ajustement de la structure de navigation |
| `CQ63MonitoringDashboardsConfigUpdate` | &lt; 6.3 | Immédiat | Déplace les configurations personnalisées pour les tableaux de bord de surveillance depuis **/libs** et **/apps** |
| `CQ63ProcessingProfileConfigUpdate` | &lt; 6.3 | Immédiat | Traduit la propriété processingProfile (utilisée jusqu’à la version 6.1) dans Assets pour qu’elle corresponde à la structure 6.3 et ultérieure. Ajuste également les chemins relatifs du profil sur . **/conf** à la place de **/apps**. |
| `CQ63ToolsMenuEntriesContentUpgrade` | &lt; 6.3 | Immédiat | Tâche de mise à niveau supprimant les entrées obsolètes du CRXDE Lite et du menu de la console web en cas de mise à niveau. |
| `CQ64CommunitiesConfigsCleanupTask` | &lt; 6.3 | Différé | Déplacement des configurations cloud SRP, configurations des mots-clés de la communauté, nettoyage **/etc/social** et **/etc/enablement** (toutes les références et données doivent être ajustées lors de l’exécution de la migration différée ; aucun composant d’application ne doit plus dépendre de cette structure). |
| `CQ64LegacyCloudSettingsCleanupTask` | &lt; 6.4 | Différé | Nettoyage **/etc/cloudsettings** (contenant la configuration ContextHub). La configuration est automatiquement migrée au premier accès. Si la migration de contenu différée est démarrée avec la mise à niveau de ce contenu dans **/etc/cloudsettings** doit être conservé via le package avant la mise à niveau et réinstallé pour que la transformation implicite s’exécute, avec une désinstallation ultérieure du package une fois l’opération terminée. |
| `CQ64UsersTitleFixTask` | &lt; 6.4 | Différé | Ajuste la structure de titre héritée en titre dans le nœud de profil utilisateur. |
| `CQ64CommerceMigrationTask` | &lt; 6.4 | Différé | Migration du contenu commercial depuis **/etc/commerce** vers **/var/commerce**. Lors de la migration, le contenu est déplacé et les références au contenu déplacé sont mises à jour pour refléter le nouvel emplacement. |
| `CQ65DMMigrationTask` | &lt; 6.5 | Différé | Migration des paramètres de catalogue hérités et des paramètres des services cloud Dynamic Media depuis **/etc** vers **/conf** |
| `CQ65LegacyClientlibsCleanupTask` | &lt; 6.5 | Différé | Nettoyage des clientlibs héritées existantes sous **/etc/clientlibs**. |
