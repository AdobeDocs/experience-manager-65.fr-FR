---
title: Migration différée du contenu
seo-title: Migration différée du contenu
description: En savoir plus sur la migration différée du contenu dans AEM 6.4.
seo-description: En savoir plus sur la migration différée du contenu dans AEM 6.4.
uuid: f5b0aa84-5638-4708-9da2-89964d394632
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: upgrading
discoiquuid: d72b8844-d782-4b5b-8999-338217dbefb9
docset: aem65
translation-type: tm+mt
source-git-commit: 7d93df515bf98f0a947428b8093e059d63b21a34
workflow-type: tm+mt
source-wordcount: '704'
ht-degree: 87%

---


# Migration différée du contenu {#lazy-content-migration}

Dans un souci de compatibilité descendante, le contenu et les données de configuration sous **/etc** et **/content**, à partir d’AEM 6.3, ne sont ni affectés ni transformés juste après la mise à niveau. L’objectif est de garder intactes les dépendances des applications clientes sur ces structures. La fonctionnalité relative à ces structures de contenu reste la même, même si le contenu d’une version prête à l’emploi d’AEM 6.5 est hébergé à un autre endroit.

While not all of those locations may be transformed automatically, there are a few delayed `CodeUpgradeTasks` also referred to as Lazy Content Migration. Cela permet aux clients de déclencher ces transformations automatiques en redémarrant l’instance avec cette propriété système :

```shell
-Dcom.adobe.upgrade.forcemigration=true
```

De ce fait, les `CodeUpgradeTasks` seront exécutées pendant la migration.

Bien que l’objectif de l’opération soit une mise en œuvre efficace, cette mise à niveau est un processus synchrone qui s’accompagne donc d’une période d’indisponibilité qui varie en fonction du volume de contenu qui doit être traité. Il est conseillé d’évaluer les temps d’exécution dans un environnement de déploiement avant de passer à un système de production afin de planifier une fenêtre de maintenance en conséquence.

Étant donné que cette activité nécessite généralement le réglage de l’application, elle doit être effectuée parallèlement au déploiement d’applications correspondant.

Vous trouverez, ci-dessous, la liste complète des `CodeUpgradeTasks` introduites dans la version 6.5 :

| **Nom** | **Convient** **aux versions AEM antérieures à** | **Type de** **migration** | **Détails** |
|---|---|---|---|
| `Cq561ProjectContentUpgrade` | &lt; 5.6.1 | Immédiat |  |
| `Cq60MSMContentUpgrade` | &lt; 6.0 | Immédiat | Détecte toutes les `LiveRelationShips` de `VersionStorage` qui ont été supprimées et ajoute une propriété d’exclusion au parent. |
| `Cq61CloudServicesContentUpgrade` | &lt; 6.1 | Immédiat | Restructure les services cloud pour une configuration sécurisée par défaut. |
| `Cq62ConfContentUpgrade` | &lt; 6.2 | Immédiat | Supprime la liaison basée sur la propriété entre **/content** et **/conf** (remplacée par le mécanisme OSGi) et génère la configuration OSGi correspondante. |
| `Cq62FormsContentUpgrade` | &lt; 6.2 | Immédiat | En raison du traitement de merge_preserve, la règle de refus « sécurisé par défaut » écrase les autorisations données, ce qui rend nécessaire une réorganisation lors de la mise à niveau. |
| `CQ62Html5SmartFileUpgrade` | &lt; 6.2 | Immédiat | Détecte les composants qui utilisent le widget Html5SmartFile, recherche les utilisations du composant dans le contenu et restructure la persistance, abaissant ainsi le fichier binaire d’un niveau, sans le stocker au niveau du composant. |
| `Cq62ProjectsCodeUpgrade` | &lt; 6.2 | Immédiat | Déplace les projets de style précédent de **/etc/projects** vers **/content/projects**. |
| `Cq62TargetCampaignsContentUpgrade` | &lt; 6.2 | Immédiat | Introduit un calque de conteneur dans la hiérarchie (Areas) et ajuste les références. |
| `Cq62TargetContentUpgrade` | &lt; 6.2 | Immédiat | Définit des noms d’emplacement fixes sur les composants cibles. |
| `Cq62WorkflowContentUpgrade` | &lt; 6.2 | Immédiat | Transformation complexe des modèles de workflow avec antidatage des instances, notifications et structures 6.2, suivie de la fusion depuis l’emplacement de secours à partir de **/var/backup**. |
| `CQ63AssetsMetadataFormsUpdate` | &lt; 6.3 | Immédiat | Déplace des ressources, des schémas de métadonnées personnalisés et des profils de traitement depuis **/apps** vers **/conf**, et convertit les formulaires de profils de métadonnées et de schémas de métadonnées coral2 au format coral3. |
| `CQ63AssetsSearchFacetsUpdate` | &lt; 6.3 | Immédiat | Déplace des ressources et des facettes de recherche personnalisées depuis **/apps** vers **/conf**, et convertit les formulaires de profils de métadonnées et de schémas de métadonnées coral2 au format coral3. |
| `CQ63InboxItemsUpgrade` | &lt; 6.3 | Immédiat | Met à jour InboxItems pour le classement des éléments de la boîte de réception (réglage des métadonnées pour un tri efficace) |
| `CQ63MetadataSchemaConfigUpdate` | &lt; 6.3 | Immédiat | Modifie la propriété metadataSchema sur le dossier en définissant les chemins d’accès relatifs sur **/conf** au lieu de **/apps**. |
| `CQ63MobileAppsNavUpgrade` | &lt; 6.3 | Immédiat | Modifie la structure de navigation. |
| `CQ63MonitoringDashboardsConfigUpdate` | &lt; 6.3 | Immédiat | Déplace les configurations personnalisées pour les tableaux de bord de contrôle depuis **/libs** et **/apps**. |
| `CQ63ProcessingProfileConfigUpdate` | &lt; 6.3 | Immédiat | Convertit la propriété processingProfile (utilisée jusqu’à la version 6.1) dans Assets afin de la faire correspondre à la structure 6.3 ou ultérieure. Modifie également les chemins d’accès relatifs du projet sur **/conf** au lieu de **/apps**.  |
| `CQ63ToolsMenuEntriesContentUpgrade` | &lt; 6.3 | Immédiat | Tâche de mise à niveau qui supprime les entrées de menu obsolètes de CRXDE Lite et de la console web dans le cas d’une mise à niveau. |
| `CQ64CommunitiesConfigsCleanupTask` | &lt; 6.3 | Différé | Déplace les configurations cloud SRP et les configurations de mots-clés communautaires, nettoie **/etc/social** et **/etc/enablement** (toutes les références et données, le cas échéant, doivent être modifiées lors de l’exécution de la migration différée ; plus aucune partie de l’application ne doit désormais dépendre de cette structure). |
| `CQ64LegacyCloudSettingsCleanupTask` | &lt; 6.4 | Différé | Nettoie **/etc/cloudsettings** (contenant la configuration ContextHub). La migration de la configuration est effectuée automatiquement lors du premier accès. Si la migration différée du contenu est lancée avec la mise à niveau, le contenu de **/etc/cloudsettings** doit être conservé via le package avant la mise à niveau et réinstallé pour que la transformation implicite soit lancée, avec une désinstallation ultérieure du package une fois la procédure terminée. |
| `CQ64UsersTitleFixTask` | &lt; 6.4 | Différé | Définit la structure de titre héritée sur le titre du nœud de profil utilisateur. |
| `CQ64CommerceMigrationTask` | &lt; 6.4 | Différé | Migrez le contenu commercial de **/etc/commerce** vers **/var/commerce**. Lors de la migration, le contenu est déplacé et les références au contenu déplacé sont mises à jour pour refléter le nouvel emplacement. |
| `CQ65DMMigrationTask` | &lt; 6.5 | Différé | Migration des paramètres de catalogue hérités et des paramètres des services de cloud de médias dynamiques de **/etc** vers **/conf** |
| `CQ65LegacyClientlibsCleanupTask` | &lt; 6.5 | Différé | Nettoyer les clientlibs hérités existants sous **/etc/clientlibs** |
