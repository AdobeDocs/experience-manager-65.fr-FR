---
title: Configurer le planificateur de synchronisation
description: Découvrez comment migrer et synchroniser des ressources, configurer le planificateur de synchronisation et utiliser des dossiers pour classer les ressources.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
docset: aem65
role: Admin,User
exl-id: 34db1f76-ee40-4612-85da-22041e7560fb
solution: Experience Manager, Experience Manager Forms
feature: Workbench,Adaptive Forms
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 36ac8e9c-5c7a-56d8-af5e-39399fd7b101
    internal-label: Workbench
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 88%
---
# Configurer le planificateur de synchronisation {#configuring-the-synchronization-scheduler}

Par défaut, le planificateur de synchronisation s’exécute toutes les 3 minutes pour synchroniser toutes les ressources modifiées et mises à jour dans le référentiel via LiveCycle Workbench 11. Les applications contenant des formulaires ou des ressources sont visibles dans l’interface utilisateur d’AEM Forms une fois le processus de synchronisation terminé.

## Modifier l’intervalle du planificateur de synchronisation {#change-interval-of-the-synchronization-scheduler}

Effectuez les étapes suivantes pour modifier l’intervalle du planificateur de synchronisation :

1. Connectez-vous à AEM Configuration Manager. L’URL de Configuration Manager est la suivante : `https://'[server]:[port]'/lc/system/console/configMgr`.

1. Recherchez et ouvrez le bundle **FormsManagerConfiguration**.

1. Choisissez une nouvelle valeur pour l’option de fréquence du **planificateur de synchronisation**.

   Les unités de fréquence se comptent en minutes. Par exemple, pour configurer l’exécution du planificateur toutes les 60 minutes, saisissez 60.

## Synchronisation des ressources {#synchronizing-assets}

Vous pouvez utiliser l’option **Synchroniser les ressources à partir du référentiel** pour synchroniser manuellement les ressources. Effectuez les opérations suivantes pour synchroniser manuellement les actifs :

1. Connectez-vous à AEM Forms. L’URL par défaut est `https://'[server]:[port]'/lc/aem/forms/`.

   ![Interface utilisateur d’AEM Forms](assets/aem_forms_ui.png)

   **Figure :** *interface utilisateur d’AEM Forms*

1. Cliquez sur l’icône ![aem6forms_sync](assets/aem6forms_sync.png) dans la barre d’outils. Si vous ne disposez d’aucune ressource dans le dernier chemin configuré, la boîte de dialogue s’affiche comme ci-dessous. Cliquez sur **Démarrer** pour lancer la synchronisation.

   ![Boîte de dialogue de synchronisation](assets/migrate-and-syncronize.png)

   **Figure :** *boîte de dialogue de synchronisation*

## Correction de l’erreur de synchronisation {#troubleshooting-synchronization-error}

Vous pouvez créer de nouvelles applications dans le concepteur de workflow (LiveCycle Workbench).

Si une application que vous venez de créer et un dossier se trouvant sous /content/dam/formsanddocuments portent le même nom, une erreur « *Une ressource portant le même nom que cette application existe déjà au niveau racine.* » s’affiche. est consignée.

Pour résoudre le conflit, renommez l’application puis synchronisez manuellement les actifs.

![Conflits dans la boîte de dialogue de synchronisation des ressources](assets/sync-conflict.png)

**Figure :** *conflits dans la boîte de dialogue de synchronisation des ressources*
