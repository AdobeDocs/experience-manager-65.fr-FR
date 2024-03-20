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
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '693'
ht-degree: 23%

---

# Migration différée du contenu {#lazy-content-migration}

Pour des raisons de compatibilité descendante, de contenu et de configuration dans **/etc** et **/content** à partir de Adobe Experience Manager (AEM) 6.3 ne sera pas modifié ni transformé immédiatement avec la mise à niveau. Cela permet de s’assurer que les dépendances des applications client sur ces structures restent intactes. Les fonctionnalités relatives à ces structures de contenu restent les mêmes même si le contenu d’une AEM 6.5 prête à l’emploi est hébergé à un autre endroit.

Bien que ces emplacements ne soient pas tous transformés automatiquement, il existe quelques `CodeUpgradeTasks` différées ; ce que l’on désigne sous le nom de migration différée du contenu. Cela permet aux utilisateurs de déclencher ces transformations automatiques en redémarrant l’instance avec cette propriété système :

```shell
-Dcom.adobe.upgrade.forcemigration=true
```

Cela entraîne la `CodeUpgradeTasks` à exécuter lors de la migration.

Bien que l’objectif soit une exécution efficace, ce processus de mise à niveau est synchrone et s’accompagne donc d’un temps d’arrêt en fonction de la quantité de contenu à traiter. Adobe recommande d’évaluer les temps d’exécution sur un environnement intermédiaire avant un système de production afin de planifier une fenêtre de maintenance correspondante.

Comme cela nécessite généralement d’ajuster l’application, cette activité doit être effectuée avec le déploiement d’application correspondant.

Vous trouverez, ci-dessous, la liste complète des `CodeUpgradeTasks` introduites dans la version 6.5 :

| **Nom** | **Pertinent** **pour les versions AEM antérieures** | **Migration** **Type** | **Détails** |
|---|---|---|---|
| `Cq561ProjectContentUpgrade` | &lt; 5.6.1 | Immédiat |  |
| `Cq60MSMContentUpgrade` | &lt; 6.0 | Immédiat | Détecte toutes les `LiveRelationShips` de `VersionStorage` qui ont été supprimées et ajoute une propriété d’exclusion au parent. |
| `Cq61CloudServicesContentUpgrade` | &lt; 6.1 | Immédiat | Restructuration des services cloud pour une configuration sécurisée par défaut |
| `Cq62ConfContentUpgrade` | &lt; 6.2 | Immédiat | Supprime la liaison basée sur la propriété de **/content** to **/conf** (remplacé par le mécanisme OSGi), génère la configuration OSGi correspondante. |
| `Cq62FormsContentUpgrade` | &lt; 6.2 | Immédiat | En raison de la gestion de merge_preserve, la règle de refus sécurisée par défaut remplace les autorisations données, ce qui entraîne la nécessité de réorganiser lors de la mise à niveau. |
| `CQ62Html5SmartFileUpgrade` | &lt; 6.2 | Immédiat | Détecte les composants à l’aide du widget Html5SmartFile, recherche les utilisations du composant dans le contenu et restructure la persistance, déplaçant ainsi le binaire d’un niveau vers le bas et ne le stockant pas au niveau du composant. |
| `Cq62ProjectsCodeUpgrade` | &lt; 6.2 | Immédiat | Déplace les anciens projets de style de **/etc/projects** to **/content/projects** |
| `Cq62TargetCampaignsContentUpgrade` | &lt; 6.2 | Immédiat | Introduit un calque de conteneur dans la hiérarchie (Zones) et ajuste les références. |
| `Cq62TargetContentUpgrade` | &lt; 6.2 | Immédiat | Définit des noms d’emplacement fixes pour les composants cibles. |
| `Cq62WorkflowContentUpgrade` | &lt; 6.2 | Immédiat | Transformation complexe des modèles de workflow antérieurs à la version 6.2 des structures, instances et notifications, puis fusion à partir de l’emplacement de sauvegarde depuis **/var/backup** |
| `CQ63AssetsMetadataFormsUpdate` | &lt; 6.3 | Immédiat | Déplace des ressources, des schémas de métadonnées personnalisés et des profils de traitement depuis **/apps** to **/conf** et convertit les formulaires de profils de métadonnées et de schéma de métadonnées de coral2 à coral3. |
| `CQ63AssetsSearchFacetsUpdate` | &lt; 6.3 | Immédiat | Déplace les ressources et les facettes de recherche personnalisées depuis **/apps** to **/conf** et convertit les formulaires de profils de métadonnées et de schéma de métadonnées de coral2 à coral3. |
| `CQ63InboxItemsUpgrade` | &lt; 6.3 | Immédiat | Met à jour InboxItems pour l’ordre des éléments de la boîte de réception (ajustement des métadonnées pour un tri efficace) |
| `CQ63MetadataSchemaConfigUpdate` | &lt; 6.3 | Immédiat | Ajuste la propriété metadataSchema sur le dossier en remplaçant les chemins relatifs par **/conf** à la place de **/apps** |
| `CQ63MobileAppsNavUpgrade` | &lt; 6.3 | Immédiat | Ajustement de la structure de navigation |
| `CQ63MonitoringDashboardsConfigUpdate` | &lt; 6.3 | Immédiat | Déplace les configurations personnalisées des tableaux de bord de surveillance depuis **/libs** et **/apps** |
| `CQ63ProcessingProfileConfigUpdate` | &lt; 6.3 | Immédiat | Traduit la propriété processingProfile (utilisée jusqu’à la version 6.1) dans Assets afin qu’elle corresponde à la structure 6.3 et versions ultérieures. Ajuste également les chemins relatifs du profil à **/conf** à la place de **/apps**. |
| `CQ63ToolsMenuEntriesContentUpgrade` | &lt; 6.3 | Immédiat | Tâche de mise à niveau qui supprime les entrées de menu obsolètes du CRXDE Lite et de la console web en cas de mise à niveau. |
| `CQ64CommunitiesConfigsCleanupTask` | &lt; 6.3 | Différé | Déplacement des configurations cloud SRP, des configurations de mots-clés communautaires, nettoyage **/etc/social** et **/etc/enablement** (toutes les références et données doivent être ajustées lors de l’exécution de la migration différée ; aucune partie de l’application ne doit plus dépendre de cette structure). |
| `CQ64LegacyCloudSettingsCleanupTask` | &lt; 6.4 | Différé | Nettoie **/etc/cloudsettings** (contenant la configuration ContextHub). La configuration est automatiquement migrée lors du premier accès. Si la migration différée du contenu est lancée avec la mise à niveau de ce contenu dans **/etc/cloudsettings** doit être conservé via le package avant l&#39;upgrade et réinstallé pour que la transformation implicite entre en jeu, ainsi qu&#39;une désinstallation ultérieure du package après l&#39;achèvement. |
| `CQ64UsersTitleFixTask` | &lt; 6.4 | Différé | Ajuste la structure de titre héritée au titre dans le noeud de profil utilisateur. |
| `CQ64CommerceMigrationTask` | &lt; 6.4 | Différé | Migration du contenu commercial depuis **/etc/commerce** vers **/var/commerce**. Lors de la migration, le contenu est déplacé et les références au contenu déplacé sont mises à jour pour refléter le nouvel emplacement. |
| `CQ65DMMigrationTask` | &lt; 6.5 | Différé | Migration des paramètres de catalogue hérités et des paramètres des services cloud Dynamic Media depuis **/etc** vers **/conf** |
| `CQ65LegacyClientlibsCleanupTask` | &lt; 6.5 | Différé | Nettoyage des clientlibs héritées existantes sous **/etc/clientlibs**. |
