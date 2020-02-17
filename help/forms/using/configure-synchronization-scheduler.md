---
title: Configuration du planificateur de synchronisation
seo-title: Configuration du planificateur de synchronisation
description: Apprenez à migrer et à synchroniser des ressources, à configurer le planificateur de synchronisation et à organiser les ressources dans des dossiers.
seo-description: Apprenez à migrer et à synchroniser des ressources, à configurer le planificateur de synchronisation et à organiser les ressources dans des dossiers.
uuid: b2c89feb-2947-418a-b343-4c01e453602b
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: 8c8b1998-eab4-4230-b24f-5e96883ba599
docset: aem65
translation-type: tm+mt
source-git-commit: 27695ee7880cfa23d504d723297c9a06729a424b

---


# Configuration du planificateur de synchronisation {#configuring-the-synchronization-scheduler}

Par défaut, le planificateur de synchronisation s’exécute toutes les 3 minutes pour synchroniser toutes les ressources modifiées et mises à jour dans le référentiel via LiveCycle Workbench 11. Les applications contenant des formulaires ou des ressources sont visibles dans l’interface utilisateur d’AEM Forms une fois le processus de synchronisation terminé.

## Modifier l’intervalle du planificateur de synchronisation {#change-interval-of-the-synchronization-scheduler}

Suivez les étapes suivantes pour modifier l’intervalle du planificateur de synchronisation :

1. Connectez-vous au Configuration Manager d’AEM. L’URL de Configuration Manager est `https://[Server]:[Port]/lc/system/console/configMgr`

1. Recherchez et ouvrez le lot **FormsManagerConfiguration.**

1. Choisissez une nouvelle valeur pour l’option de fréquence du **planificateur de synchronisation**.

   Les unités de fréquence se comptent en minutes. Par exemple, pour configurer une exécution du planificateur toutes les 60 minutes, entrez 60.

## Synchronisation des ressources {#synchronizing-assets}

Vous pouvez utiliser l’option **Synchroniser les ressources à partir du référentiel** pour synchroniser manuellement les ressources. Effectuez les opérations suivantes pour synchroniser manuellement les actifs :

1. Connectez-vous à AEM Forms. L’URL par défaut est `https://[Server]:[Port]/lc/aem/forms/`.

   ![Interface utilisateur d’AEM Forms](assets/aem_forms_ui.png)

   **** Figure : Interface utilisateur *d’AEM Forms*

1. Cliquez sur l’icône ![aem6forms_sync](assets/aem6forms_sync.png) dans la barre d’outils. Si vous ne disposez d’aucune ressource dans le dernier chemin configuré, la boîte de dialogue s’affiche comme ci-dessous. Cliquez sur **Démarrer** pour lancer la synchronisation.

   ![Boîte de dialogue de synchronisation](assets/migrate-and-syncronize.png)

   **** Figure : Boîte de dialogue *Synchronisation*

## Dépannage des erreurs de synchronisation {#troubleshooting-synchronization-error}

Vous pouvez créer de nouvelles applications dans le Concepteur de flux de travaux (LiveCycle Workbench).

If the newly created application and a folder at /content/dam/formsanddocuments has identical name, an error &quot;*An asset with the same name as this application already exists at root level.*&quot; est enregistrée.

Pour résoudre le conflit, renommez l’application puis synchronisez manuellement les actifs.

![Conflits dans la boîte de dialogue de synchronisation des ressources](assets/sync-conflict.png)

**** Figure : *Conflits dans la boîte de dialogue de synchronisation des ressources*
