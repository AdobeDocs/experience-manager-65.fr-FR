---
title: Bonnes pratiques en matière de workflow
seo-title: Workflow Best Practices
description: Découvrez les bonnes pratiques relatives à l’utilisation des workflows dans Adobe Experience Manager.
seo-description: null
uuid: 79be4055-c2ef-428e-9054-103c6cfde1d2
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 0be8b88c-6f57-4dcc-ae11-77b378a2decd
exl-id: 14775476-6fe5-4583-8ab5-b55fef892174
source-git-commit: 10b370fd8f855f71c6d7d791c272137bb5e04d97
workflow-type: tm+mt
source-wordcount: '1925'
ht-degree: 22%

---

# Bonnes pratiques en matière de workflow{#workflow-best-practices}

Les workflows vous permettent d’automatiser les activités d’Adobe Experience Manager (AEM).

Elles représentent souvent une grande partie du traitement qui se produit dans un environnement AEM. Par conséquent, lorsque les étapes de workflow personnalisées ne sont pas écrites selon les bonnes pratiques ou que les workflows d’usine ne sont pas configurés pour s’exécuter aussi efficacement que possible, le système peut en pâtir.

Il est donc vivement conseillé de planifier soigneusement vos implémentations de workflow.

## Configuration {#configuration}

Lors de la configuration des processus de workflow (personnalisés et/ou prêts à l’emploi), certains éléments doivent être pris en compte.

### Workflows transitoires {#transient-workflows}

Pour optimiser les charges d’ingestion élevées, vous pouvez définir une [workflow en tant que transitoire](/help/sites-developing/workflows.md#transient-workflows).

Lorsqu’un workflow est transitoire, les données d’exécution liées aux étapes intermédiaires ne sont pas conservées dans le JCR lors de leur exécution (les rendus de sortie sont conservés).

Les avantages peuvent être les suivants :

* Réduction du temps de traitement des workflows, jusqu’à 10 %.
* Réduire considérablement la croissance du référentiel.
* Il n’est plus nécessaire de purger les workflows CRUD.
* En outre, il réduit le nombre de fichiers TAR à compresser.

>[!CAUTION]
>
>Si votre entreprise impose la conservation/l’archivage des données d’exécution de workflow à des fins d’audit, n’activez pas cette fonctionnalité.

### Optimisation des workflows DAM {#tuning-dam-workflows}

Pour obtenir des instructions relatives à l’optimisation des performances des workflows DAM, voir la section [Guide d’optimisation des performances d’AEM Assets](/help/assets/performance-tuning-guidelines.md).

### Configuration du nombre maximal de workflows simultanés {#configure-the-maximum-number-of-concurrent-workflows}

AEM peut permettre l’exécution simultanée de plusieurs threads de workflow. Par défaut, le nombre de threads est configuré pour être la moitié du nombre de coeurs de processeur sur le système.

Dans les cas où les workflows en cours d’exécution nécessitent des ressources système, cela peut signifier qu’AEM n’a plus grand chose à utiliser pour d’autres tâches, comme le rendu de l’interface utilisateur de création. Par conséquent, le système peut être lent lors d’activités telles que le téléchargement massif d’images.

Pour résoudre ce problème, Adobe recommande de configurer le nombre de **Tâches parallèles maximales** soit entre la moitié et les trois quarts du nombre de coeurs de processeur sur le système. Cela devrait laisser suffisamment de capacité de réaction au système lors du traitement de ces workflows.

Pour configurer la valeur **Nombre maximal de tâches en parallèle**, vous pouvez effectuer l’une des opérations suivantes :

* Définissez la **[Configuration OSGi](/help/sites-deploying/configuring-osgi.md)** à partir de la console web AEM ; pour **File d’attente : file d’attente du workflow Granite** (une **Configuration de la file d’attente des tâches Apache Sling**).

* Configurez la file d’attente à partir de l’option **Tâches Sling** de la console web AEM ; pour la **Configuration de la file d’attente des tâches : file d’attente du workflow Granite**, à l’adresse `http://localhost:4502/system/console/slingevent`.

Il existe, en outre, une configuration distincte pour la **File d’attente des tâches de processus externes du workflow Granite**. Il est utilisé pour les processus de workflow qui lancent des fichiers binaires externes, tels que **InDesign Server** ou **Image Magick**.

### Configuration de files d’attente de tâches individuelles {#configure-individual-job-queues}

Dans certains cas, il est utile de configurer des files d’attente individuelles pour contrôler les threads simultanés, ou d’autres options de file d’attente, sur une base de tâche individuelle. Vous pouvez ajouter et configurer une file d’attente individuelle à partir de la console web via le **Configuration de la file d’attente des tâches Apache Sling** fabrique. Pour trouver la rubrique appropriée à répertorier, exécutez le modèle de votre workflow et recherchez-la dans le **Tâches Sling** console, par exemple, à l’adresse `http://localhost:4502/system/console/slingevent`.

Des files d’attente individuelles peuvent également être ajoutées pour les workflows transitoires.

### Configuration de la purge des workflows {#configure-workflow-purging}

Dans une installation standard, AEM fournit une console de maintenance dans laquelle les activités de maintenance quotidiennes et hebdomadaires peuvent être planifiées et configurées, par exemple :

`http://localhost:4502/libs/granite/operations/content/maintenance.html`

Par défaut, la variable **Période de maintenance hebdomadaire** a une **Purge du workflow** , mais cela doit être configuré avant son exécution. Pour configurer les purges des workflows, une nouvelle **Configuration de la purge du workflow Adobe Granite** doit être ajouté à la console Web.

Pour plus d’informations sur les tâches de maintenance dans AEM, voir la section [Tableau de bord des opérations](/help/sites-administering/operations-dashboard.md).

## Personnalisation {#customization}

Lors de l’écriture de processus de workflow personnalisés, certains éléments doivent être pris en compte.

### Emplacements {#locations}

Les définitions des modèles de workflow, lanceurs, scripts et notifications sont conservées dans le référentiel en fonction de leur type, c’est-à-dire prêtes à l’emploi, personnalisées, etc.

>[!NOTE]
>
>Consultez également la section [Restructuration du référentiel dans AEM 6.5](/help/sites-deploying/repository-restructuring.md).

#### Emplacements - Modèles de processus {#locations-workflow-models}

Les modèles de workflow sont stockés dans le référentiel en fonction de leur type :

* Les conceptions de workflow d’usine sont conservées à l’emplacement suivant :

  `/libs/settings/workflow/models/`

  >[!CAUTION]
  >
  >Ne pas :
  >
  >* placer vos modèles de workflow personnalisés dans ce dossier ;
  >* modifier des éléments dans `/libs`,
  >
  >Comme toute modification peut être écrasée lors de la mise à niveau ou lors de l’installation de correctifs, de correctifs cumulatifs ou de Service Packs.

* Les conceptions de workflow personnalisées sont conservées sous :

  ```
  /conf/global/settings/workflow/models/...
  ```

* Les conceptions de workflow d’exécution (standard et personnalisées) sont conservées à l’emplacement suivant :

  `/var/workflow/models/`

* Les conceptions de workflow héritées (au moment de la création et de l’exécution) sont conservées à l’emplacement suivant :

  `/etc/workflow/models/`

  >[!NOTE]
  >
  >Si ces conceptions sont modifiées *à l’aide de l’interface utilisateur AEM*, les détails seront alors copiés vers les nouveaux emplacements.

#### Emplacements - Lanceurs de workflow {#locations-workflow-launchers}

Les définitions du lanceur de workflow sont également stockées dans le référentiel en fonction de leur type :

* Les lanceurs de workflow d’usine sont conservés à l’emplacement suivant :

  `/libs/settings/workflow/launcher/`

  >[!CAUTION]
  >
  >Ne pas :
  >
  >* placer vos lanceurs de workflow personnalisés dans ce dossier ;
  >* modifier des éléments dans `/libs`,
  >
  >Comme toute modification peut être écrasée lors de la mise à niveau ou lors de l’installation de correctifs, de correctifs cumulatifs ou de Service Packs.

* Les lanceurs de workflow personnalisés sont conservés sous :

  ```
  /conf/global/settings/workflow/launcher/...
  ```

* Les lanceurs de workflow hérités sont conservés à l’emplacement suivant :

  `/etc/workflow/launcher/`

  >[!NOTE]
  >
  >Si ces définitions sont modifiées *à l’aide de l’interface utilisateur AEM*, les détails seront alors copiés vers les nouveaux emplacements.

#### Emplacements - Scripts de workflow {#locations-workflow-scripts}

Les scripts de workflow sont également stockés dans le référentiel en fonction de leur type :

* Les scripts de workflow d’usine sont conservés à l’emplacement suivant :

  `/libs/workflow/scripts/`

  >[!CAUTION]
  >
  >Ne pas :
  >
  >* placer vos scripts de workflow personnalisés dans ce dossier ;
  >* modifier des éléments dans `/libs`,
  >
  >Comme toute modification peut être écrasée lors de la mise à niveau ou lors de l’installation de correctifs, de correctifs cumulatifs ou de Service Packs.

* Les scripts de workflow personnalisés sont conservés sous :

  ```
  /apps/workflow/scripts/...
  ```

* Les scripts de workflow hérités sont conservés à l’emplacement suivant :

  `/etc/workflow/scripts/`

#### Emplacements - Notifications de workflow {#locations-workflow-notifications}

Les notifications de workflow sont également stockées dans le référentiel en fonction de leur type :

* Les définitions de notification de workflow d&#39;usine sont conservées sous le chemin suivant :

  `/libs/settings/workflow/notification/`

  >[!CAUTION]
  >
  >Ne pas :
  >
  >* placer les définitions de notification de workflow personnalisées dans ce dossier ;
  >* modifier des éléments dans `/libs`,
  >
  >Comme toute modification peut être écrasée lors de la mise à niveau ou lors de l’installation de correctifs, de correctifs cumulatifs ou de Service Packs.

* Les définitions de notification de workflow personnalisées sont conservées sous :

  ```
  /conf/global/settings/workflow/notification/...
  ```

  >[!NOTE]
  >
  >Si vous souhaitez remplacer un texte de notification de workflow, créez un chemin superposé sous :
  >
  >
  >`/conf/global/settings/workflow/notification/<path-under-libs>`

* Les définitions de notification de workflow héritées sont conservées à l’emplacement suivant :

  `/etc/workflow/notification/`

### Sessions de processus {#process-sessions}

Comme dans tout développement personnalisé, il est toujours recommandé d’utiliser la session d’un utilisateur lorsque cela est possible :

* pour une meilleure conformité avec les directives de sécurité
* pour permettre au système de gérer l’ouverture et la fermeture de la session.

Lors de l’implémentation d’un processus de workflow :

* Une session de workflow est fournie et doit être utilisée, sauf s’il y a une bonne raison de ne pas le faire.
* Les nouvelles sessions ne doivent pas être créées à partir des étapes du workflow, car cela entraîne des incohérences dans le ou les états ainsi que des problèmes de simultanéité possibles dans le moteur de workflow.
* Vous ne devez pas acquérir une nouvelle session JCR à partir d’une étape de processus dans un workflow ; vous devez adapter la session de workflow fournie par l’API Étape du processus à une session JCR. Par exemple :

```
public void execute(WorkItem item, WorkflowSession workflowSession, MetaDataMap args) throws WorkflowException {
        // to obtain a jcr session:
        javax.jcr.Session jcrSession = workflowSession.adaptTo(javax.jcr.Session.class);

        // to obtain a sling resource resolver:
        org.apache.sling.api.resource.ResourceResolver slingResourceResolver = workflowSession.adaptTo(org.apache.sling.api.resource.ResourceResolver.class);
```

Enregistrer une session :

* Dans un processus de workflow, si `WorkflowSession` est utilisé pour modifier le référentiel, n’enregistrez pas explicitement la session ; le workflow s’en chargera une fois l’opération terminée.
* `Session.Save` ne doit pas être appelé depuis l’intérieur d’une étape de workflow :

   * Il est recommandé d’adapter la session JCR du workflow ; une opération `save` n’est donc pas nécessaire, car le moteur de workflow enregistre automatiquement la session une fois l’exécution du workflow terminée.
   * il n’est pas recommandé qu’une étape de processus crée sa propre session jcr.

* En éliminant les enregistrements inutiles, vous pouvez réduire les frais généraux et ainsi rendre les workflows plus efficaces.

>[!CAUTION]
>
>Si, malgré les recommandations ici, vous créez votre propre session jcr, elle doit être enregistrée.

### Réduction du nombre/de la portée des lanceurs {#minimize-the-number-scope-of-launchers}

Il y a un écouteur responsable de tous les [lanceurs de workflow](/help/sites-administering/workflows-starting.md#workflows-launchers) qui sont enregistrés :

* Il écoute les modifications à tous les chemins spécifiés dans les propriétés d’extension de nom de fichier des autres lanceurs.
* Lorsqu’un événement est distribué, le moteur de workflow évalue chaque lanceur pour déterminer s’il doit s’exécuter.

La création d’un trop grand nombre de lanceurs ralentit l’exécution du processus d’évaluation.

La création d’un chemin d’extension métacaractère à la racine du référentiel sur un seul lanceur obligerait le moteur de workflow à écouter et à évaluer les événements de création/modification sur chaque noeud du référentiel. C’est pourquoi il est recommandé de ne créer que les lanceurs nécessaires et de rendre le chemin d’accès à l’extension métacaractère aussi spécifique que possible.

En raison de l’impact de ces lanceurs sur le comportement du workflow, il peut également s’avérer utile de désactiver les lanceurs prêts à l’emploi qui ne sont pas utilisés.

### Améliorations de la configuration pour les lanceurs {#configuration-enhancements-for-launchers}

La [configuration de lanceur](/help/sites-administering/workflows-starting.md#workflows-launchers) personnalisée a été améliorée afin de prendre en charge les éléments suivants :

* Posséder plusieurs conditions &quot;ET&quot; ensemble.
* Posséder des conditions OU dans une seule condition.
* Désactivez/activez les lanceurs selon qu’un indicateur de fonctionnalité est activé ou désactivé.
* Prise en charge d’expressions régulières (regex) dans des conditions de lanceur.

### Ne pas démarrer les workflows à partir d’autres workflows {#do-not-start-workflows-from-other-workflows}

Les workflows peuvent entraîner une surcharge importante, à la fois en termes d’objets créés en mémoire et de noeuds suivis dans le référentiel. Pour cette raison, il est préférable qu’un workflow effectue son traitement en lui-même plutôt que de démarrer des workflows supplémentaires.

Par exemple, un workflow implémente un processus d’entreprise sur un ensemble de contenu, puis active ce contenu. Il est préférable de créer un processus de workflow personnalisé qui active chacun de ces noeuds, plutôt que de démarrer une **Activer le contenu** modèle pour chacun des noeuds de contenu qui doivent être publiés. Cette approche nécessite un travail de développement supplémentaire, mais elle est plus efficace lors de l’exécution que de démarrer une instance de workflow distincte pour chaque activation.

Un autre exemple serait un workflow qui traite plusieurs noeuds, crée un module de workflow, puis active ce module. Plutôt que de créer le module, puis de démarrer un workflow distinct avec le module comme charge utile, vous pouvez modifier la charge utile de votre workflow dans l’étape qui crée le module, puis appeler l’étape pour activer le module dans le même modèle de workflow.

### Avance du gestionnaire {#handler-advance}

Lors de la conception d’un modèle de workflow, vous avez la possibilité d’activer l’avance du gestionnaire sur les étapes de votre workflow. Vous pouvez également ajouter du code à votre étape de workflow pour déterminer l’étape qui doit être exécutée ensuite, puis l’exécuter.

Il est recommandé d’utiliser l’avance du gestionnaire, car elle offre de meilleures performances.

### Phases de workflow {#workflow-stages}

Vous pouvez définir [étapes de workflow](/help/sites-developing/workflows.md#workflow-stages), puis attribuez des tâches/étapes à une étape de workflow spécifique.

Ces informations sont utilisées pour afficher la progression d&#39;un workflow lorsque vous cliquez sur le bouton [**Informations sur le workflow** de l’onglet d’un élément de travail à partir de **Boîte de réception**](/help/sites-authoring/workflows-participating.md#opening-a-workflow-item-to-view-details-and-take-actions). Les modèles de workflow existants peuvent être modifiés pour ajouter des phases.

### Étape Activer le processus de page {#activate-page-process-step}

La variable **Activer le processus de page** Cette étape active les pages à votre place, mais elle ne recherche pas automatiquement les ressources DAM référencées et les active également.

Gardez à l’esprit que cette étape doit être utilisée dans le cadre d’un modèle de workflow.

### Considérations relatives à la mise à niveau {#upgrade-considerations}

Lors de la mise à niveau de votre instance :

* assurez-vous que tous les modèles de workflow personnalisés sont sauvegardés avant la mise à niveau d’une instance.
* confirmez qu’aucun de vos workflows personnalisés n’est stocké sous le [location](#locations):

   * `/libs/settings/workflow/models/projects`

>[!NOTE]
>
>Consultez également la section [Restructuration du référentiel dans AEM 6.5](/help/sites-deploying/repository-restructuring.md).

## Outils système {#system-tools}

De nombreux outils système sont disponibles pour faciliter la surveillance, la maintenance et la résolution des problèmes des workflows. Tous les exemples d’URL ci-dessous utilisent `localhost:4502`. Cependant, ces URL doivent être disponibles sur toute instance de création (`<hostname>:<port>`).

### Console de gestion des tâches Sling {#sling-job-handling-console}

`http://localhost:4502/system/console/slingevent`

La console de gestion des tâches Sling affiche :

* Statistiques sur l’état des tâches dans le système depuis le dernier redémarrage.
* Elle affiche également les configurations de toutes les files d’attente de tâches et fournit un raccourci permettant de les modifier dans le gestionnaire de configuration.

### Outil Rapport de workflow {#workflow-report-tool}

L’outil de création de rapports de workflow est supprimé dans la version 6.3 afin d’éviter une dégradation des performances.

### MBean des opérations de maintenance des workflows {#workflow-maintenance-operations-mbean}

`http://localhost:4502/system/console/jmx/com.adobe.granite.workflow:type=Maintenance`

Le MBean de maintenance des workflows expose plusieurs routines de maintenance bien utiles, telles que la purge des workflows terminés et la récupération de statistiques sur les workflows.

## Informations supplémentaires {#further-information}

Pour plus d’informations, consultez :

* [Utilisation des workflows](/help/sites-authoring/workflows.md)
* [Administration des workflows](/help/sites-administering/workflows.md)
* [Développement et extension des workflows](/help/sites-developing/workflows.md)
* [Optimisation des performances](/help/sites-deploying/configuring-performance.md)
