---
title: Bonnes pratiques en matière de workflow
description: Découvrez les bonnnes pratiques d’utilisation des workflows dans Adobe Experience Manager.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
exl-id: 14775476-6fe5-4583-8ab5-b55fef892174
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '1925'
ht-degree: 100%

---

# Bonnes pratiques en matière de workflow{#workflow-best-practices}

Les workflows vous permettent d’automatiser les activités d’Adobe Experience Manager (AEM).

Ils représentent souvent une grande partie du traitement effectué dans un environnement AEM. Ainsi, lorsque les étapes de workflow personnalisées ne sont pas écrites conformément aux bonnes pratiques ou que les workflows prêts à l’emploi ne sont pas configurés pour s’exécuter aussi efficacement que possible, cela peut nuire au système.

Il est donc vivement conseillé de planifier soigneusement vos implémentations de workflow.

## Configuration {#configuration}

Lors de la configuration de processus de workflows (personnalisés et/ou prêts à l’emploi), il convient de garder quelques éléments à l’esprit.

### Workflows transitoires {#transient-workflows}

Pour optimiser les charges d’ingestion élevées, vous pouvez définir un [workflow comme transitoire](/help/sites-developing/workflows.md#transient-workflows).

Lorsqu’un workflow est transitoire, les données d’exécution liées aux étapes de travail intermédiaires ne sont pas conservées dans JCR lors de leur exécution (les rendus de sortie sont conservés).

Les avantages sont notamment :

* Une réduction du temps de traitement du workflow ; jusqu’à 10 %.
* Une réduction considérable de la croissance du référentiel.
* Plus aucun workflow CRUD n&#39;est nécessaire pour la purge.
* Une réduction en outre du nombre de fichiers TAR à compacter.

>[!CAUTION]
>
>Si votre entreprise impose la conservation/l’archivage des données d’exécution de workflow à des fins d’audit, n’activez pas cette fonctionnalité.

### Optimiser les workflows DAM {#tuning-dam-workflows}

Pour obtenir des instructions sur l’optimisation des performances des workflows DAM, consultez le [guide sur l’optimisation des performances des ressources AEM](/help/assets/performance-tuning-guidelines.md).

### Configurer le nombre maximum de workflows simultanés {#configure-the-maximum-number-of-concurrent-workflows}

AEM peut permettre à plusieurs threads de workflows de s’exécuter simultanément. Par défaut, le nombre de threads est configuré pour correspondre à la moitié du nombre de cœurs de processeur du système.

Dans les cas où les workflows en cours d’exécution sont gourmands en ressources système, cela peut signifier qu’AEM ne peut plus utiliser grand-chose pour d’autres tâches, telles que le rendu de l’interface utilisateur de création. Par conséquent, le système peut être lent lors d’activités telles que le chargement massif d’images.

Pour résoudre ce problème, Adobe recommande de configurer le **Nombre maximal de tâches parallèles** pour qu’il soit compris entre la moitié et les trois quarts du nombre de cœurs de processeur du système. Cela devrait laisser suffisamment de capacité de réaction au système lors du traitement de ces workflows.

Pour configurer la valeur **Nombre maximal de tâches en parallèle**, vous pouvez effectuer l’une des opérations suivantes :

* Définissez la **[Configuration OSGi](/help/sites-deploying/configuring-osgi.md)** à partir de la console web AEM ; pour **File d’attente : file d’attente du workflow Granite** (une **Configuration de la file d’attente des tâches Apache Sling**).

* Configurez la file d’attente à partir de l’option **Tâches Sling** de la console web AEM ; pour la **Configuration de la file d’attente des tâches : file d’attente du workflow Granite**, à l’adresse `http://localhost:4502/system/console/slingevent`.

Il existe, en outre, une configuration distincte pour la **File d’attente des tâches de processus externes du workflow Granite**. Cela est utilisé pour les processus de workflow qui lancent des binaires externes, tels qu’**InDesign Server** ou **Image Magick**.

### Configurer des files d’attente de tâches individuelles {#configure-individual-job-queues}

Dans certains cas, il est utile de configurer des files d’attente de tâches individuelles pour contrôler les threads simultanés ou d’autres options de file d’attente, sur une base de tâches individuelles. Vous pouvez ajouter et configurer une file d’attente individuelle depuis la console web via la fabrique de **configuration de la file d’attente de tâches Apache Sling**. Pour localiser la rubrique à répertorier, exécutez le modèle du workflow et recherchez-le dans la console **Tâches Sling** ; par exemple, à l’adresse `http://localhost:4502/system/console/slingevent`.

Des files d’attente individuelles peuvent également être ajoutées pour les workflows transitoires.

### Configurer la purge de workflow {#configure-workflow-purging}

Dans une installation standard, AEM fournit une console de maintenance où vous pouvez planifier et configurer les activités de maintenance quotidiennes et hebdomadaires ; par exemple, à :

`http://localhost:4502/libs/granite/operations/content/maintenance.html`

Par défaut, la **Fenêtre de maintenance hebdomadaire** a une tâche de **Purge de workflow**, mais celle-ci doit être configurée avant son exécution. Pour configurer les purges de workflow, vous devez ajoutez une nouvelle **Configuration de la purge de workflow Adobe Granite** dans la console web.

Pour plus de détails sur les tâches de maintenance dans AEM, consultez le [Tableau de bord des opérations](/help/sites-administering/operations-dashboard.md).

## Personnalisation {#customization}

Lors de l’écriture de processus de workflows personnalisés, vous devez prendre en compte un certain nombre d’éléments.

### Emplacements {#locations}

Les définitions de modèles de workflow, lanceurs, scripts et notifications sont conservées dans le référentiel en fonction de leur type ; par exemple, prêt à l’emploi, personnalisé, etc.

>[!NOTE]
>
>Consultez également la section [Restructuration du référentiel dans AEM 6.5](/help/sites-deploying/repository-restructuring.md).

#### Emplacements - Modèles de workflow {#locations-workflow-models}

Les modèles de workflow sont stockés dans le référentiel selon leur type :

* Les conceptions de workflow prêtes à l’emploi se trouvent dans le chemin d’accès suivant :

  `/libs/settings/workflow/models/`

  >[!CAUTION]
  >
  >Ne pas :
  >
  >* placer vos modèles de workflow personnalisés dans ce dossier ;
  >* modifier des éléments dans `/libs`,
  >
  >Car les modifications peuvent être remplacées lors de la mise à niveau ou lors de l’installation de correctifs, de groupes de correctifs cumulatifs ou de service packs.

* Les conceptions de workflow personnalisées sont conservées sous :

  ```
  /conf/global/settings/workflow/models/...
  ```

* Les conceptions de workflow d’exécution (standard et personnalisées) sont conservées à l’emplacement suivant :

  `/var/workflow/models/`

* Les conceptions de workflow héritées (au moment de la création et de l’exécution) sont conservées à l’emplacement suivant :

  `/etc/workflow/models/`

  >[!NOTE]
  >
  >Si ces conceptions sont modifiées *à l’aide de l’interface utilisateur d’AEM*, les détails seront alors copiés vers les nouveaux emplacements.

#### Emplacements - Lanceurs de workflow {#locations-workflow-launchers}

Les définitions de lanceur de workflow sont également stockées dans le référentiel selon leur type :

* Les lanceurs de workflow prêts à l’emploi sont conservés à l’emplacement suivant :

  `/libs/settings/workflow/launcher/`

  >[!CAUTION]
  >
  >Ne pas :
  >
  >* placer vos lanceurs de workflow personnalisés dans ce dossier ;
  >* modifier des éléments dans `/libs`,
  >
  >Car les modifications peuvent être remplacées lors de la mise à niveau ou lors de l’installation de correctifs, de groupes de correctifs cumulatifs ou de service packs.

* Les lanceurs de workflow personnalisés sont conservés sous :

  ```
  /conf/global/settings/workflow/launcher/...
  ```

* Les lanceurs de workflow hérités sont conservés à l’emplacement suivant :

  `/etc/workflow/launcher/`

  >[!NOTE]
  >
  >Si ces définitions sont modifiées *à l’aide de l’interface utilisateur d’AEM*, les détails seront alors copiés vers les nouveaux emplacements.

#### Emplacements - Scripts de workflow {#locations-workflow-scripts}

Les scripts de workflow sont également stockés dans le référentiel selon leur type :

* Les scripts de workflow prêts à l’emploi sont conservés à l’emplacement suivant :

  `/libs/workflow/scripts/`

  >[!CAUTION]
  >
  >Ne pas :
  >
  >* placer vos scripts de workflow personnalisés dans ce dossier ;
  >* modifier des éléments dans `/libs`,
  >
  >Car les modifications peuvent être remplacées lors de la mise à niveau ou lors de l’installation de correctifs, de groupes de correctifs cumulatifs ou de service packs.

* Les scripts de workflow personnalisés sont conservés sous :

  ```
  /apps/workflow/scripts/...
  ```

* Les scripts de workflow hérités sont conservés à l’emplacement suivant :

  `/etc/workflow/scripts/`

#### Emplacements - Notifications de workflow {#locations-workflow-notifications}

Les notifications de workflow sont également stockées dans le référentiel selon leur type :

* Les définitions de notification de workflow prêtes à l’emploi sont conservées à l’emplacement suivant :

  `/libs/settings/workflow/notification/`

  >[!CAUTION]
  >
  >Ne pas :
  >
  >* placer vos définitions de notification de workflow personnalisées dans ce dossier ;
  >* modifier des éléments dans `/libs`,
  >
  >Car les modifications peuvent être remplacées lors de la mise à niveau ou lors de l’installation de correctifs, de groupes de correctifs cumulatifs ou de service packs.

* Les définitions de notification de workflow personnalisées sont conservées sous :

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

### Traiter les sessions {#process-sessions}

Comme dans tout développement personnalisé, il est toujours recommandé d’utiliser la session d’un utilisateur ou d’une utilisatrice lorsque cela est possible :

* pour un meilleur respect des consignes de sécurité ;
* pour permettre au système de gérer l’ouverture et la fermeture de la session.

Lors de la mise en œuvre d’un processus de workflow :

* Une session de workflow est fournie et doit être utilisée, sauf s’il y a une bonne raison de ne pas le faire.
* De nouvelles sessions ne doivent pas être créées à partir d’étapes de workflow, car cela entraîne des incohérences dans les états ainsi que d’éventuels problèmes de simultanéité dans le moteur de workflow.
* Vous ne devez pas acquérir une nouvelle session JCR à partir d’une étape de processus dans un workflow ; vous devez adapter la session de workflow fournie par l’API Process Step à une session jcr. Par exemple :

```
public void execute(WorkItem item, WorkflowSession workflowSession, MetaDataMap args) throws WorkflowException {
        // to obtain a jcr session:
        javax.jcr.Session jcrSession = workflowSession.adaptTo(javax.jcr.Session.class);

        // to obtain a sling resource resolver:
        org.apache.sling.api.resource.ResourceResolver slingResourceResolver = workflowSession.adaptTo(org.apache.sling.api.resource.ResourceResolver.class);
```

Enregistrer une session :

* Dans un processus de workflow, si `WorkflowSession` est utilisé pour modifier le référentiel, n’enregistrez pas explicitement la session ; le workflow s’en chargera une fois l’opération terminée.
* `Session.Save` ne doit pas être appelé depuis l’intérieur d’une étape de workflow :

   * Il est recommandé d’adapter la session JCR du workflow ; une opération `save` n’est donc pas nécessaire, car le moteur de workflow enregistre automatiquement la session une fois l’exécution du workflow terminée.
   * Il est déconseillé qu’une étape du processus crée sa propre session jcr.

* En éliminant les enregistrements inutiles, vous pouvez réduire le traitement et ainsi rendre les workflows plus efficaces.

>[!CAUTION]
>
>Si vous créez quand même votre propre session JCR malgré ces recommandations, vous devrez l’enregistrer.

### Minimiser le nombre/la portée des lanceurs {#minimize-the-number-scope-of-launchers}

Il existe un écouteur responsable de tous les [lanceurs de workflow](/help/sites-administering/workflows-starting.md#workflows-launchers) enregistrés :

* Il écoutera les changements sur tous les chemins spécifiés dans les propriétés glob des autres lanceurs.
* Lorsqu’un événement est distribué, le moteur de workflow évalue ensuite chaque lanceur pour déterminer s’il doit s’exécuter.

Créer trop de lanceurs ralentira le processus d’évaluation.

La création d&#39;un chemin glob à la racine du référentiel sur un seul lanceur obligerait le moteur de workflow à écouter et à évaluer les événements de création/modification sur chaque nœud du référentiel. Pour cette raison, il est recommandé de créer uniquement les lanceurs nécessaires et de faire en sorte que le chemin glob soit aussi spécifique que possible.

En raison de l’impact de ces lanceurs sur le comportement du workflow, il peut également être utile de désactiver tous les lanceurs prêts à l’emploi qui ne sont pas utilisés.

### Améliorations de la configuration pour les lanceurs {#configuration-enhancements-for-launchers}

La [configuration de lanceur](/help/sites-administering/workflows-starting.md#workflows-launchers) personnalisée a été améliorée afin de prendre en charge les éléments suivants :

* Avoir plusieurs conditions « AND » mises ensemble.
* Avoir des conditions OR dans une seule condition.
* Désactiver/activer les lanceurs selon qu’un indicateur de fonctionnalité est activé ou désactivé.
* Prise en charge d’expressions régulières (regex) dans des conditions de lanceur.

### Ne démarrez pas de workflows à partir d’autres workflows {#do-not-start-workflows-from-other-workflows}

Les workflows peuvent entraîner une surcharge importante, à la fois en termes d’objets créés en mémoire et de nœuds suivis dans le référentiel. Pour cette raison, il est préférable qu’un workflow effectue son traitement lui-même plutôt que de démarrer des workflows supplémentaires.

Par exemple, un workflow qui implémente un processus d’entreprise sur un ensemble de contenu, puis active ce contenu. Il est préférable de créer un processus de workflow personnalisé qui active chacun de ces nœuds, plutôt que de démarrer un modèle **Activer le contenu** pour chacun des nœuds de contenu qui doivent être publiés. Cette approche nécessitera un travail de développement supplémentaire, mais est plus efficace une fois exécutée que le démarrage d’une instance de workflow séparée pour chaque activation.

Un autre exemple serait un workflow qui traite plusieurs nœuds, crée un package de workflow, puis active ce package. Plutôt que de créer le package, puis de démarrer un workflow séparé avec le package défini comme charge utile, vous pouvez modifier la charge utile de votre workflow lors de l’étape de création du package, et appeler ensuite l’étape pour activer le package dans le même modèle de workflow.

### Avance du gestionnaire {#handler-advance}

Lors de la conception d’un modèle de workflow, vous avez la possibilité d’activer l’avance du gestionnaire dans les étapes de votre workflow. Vous pouvez également ajouter du code à votre étape de workflow pour déterminer la prochaine étape à exécuter, puis l’exécuter.

Il est recommandé d’utiliser l’avance du gestionnaire, car elle offre de meilleures performances.

### Phases de workflow {#workflow-stages}

Vous pouvez définir des [phases de workflow](/help/sites-developing/workflows.md#workflow-stages), puis affecter des tâches/étapes à une phase spécifique du workflow.

Ces informations sont utilisées pour afficher la progression d’un workflow lorsque vous cliquez sur l’onglet [**Informations sur le workflow** d’un élément de travail dans la **Boîte de réception**](/help/sites-authoring/workflows-participating.md#opening-a-workflow-item-to-view-details-and-take-actions). Les modèles de workflow existants peuvent être modifiés pour ajouter des phases.

### Étape Activer le processus des pages {#activate-page-process-step}

L’étape **Activer le processus des pages** activera les pages pour vous, mais elle ne trouvera pas automatiquement les ressources DAM référencées et ne les activera pas non plus.

Tenez compte de ce point si vous envisagez d’utiliser cette étape dans le cadre d’un modèle de workflow.

### Considérations relatives à la mise à niveau {#upgrade-considerations}

Lors de la mise à niveau de votre instance :

* assurez-vous que tous les modèles de workflow personnalisés ont été sauvegardés avant la mise à niveau d&#39;une instance.
* vérifiez qu’aucun de vos workflows personnalisés n’est stocké dans l’[ emplacement](#locations) :

   * `/libs/settings/workflow/models/projects`

>[!NOTE]
>
>Consultez également la section [Restructuration du référentiel dans AEM 6.5](/help/sites-deploying/repository-restructuring.md).

## Outils système {#system-tools}

De nombreux outils système sont disponibles pour faciliter la surveillance, la maintenance et le dépannage des workflows. Tous les exemples d’URL ci-dessous utilisent `localhost:4502`. Cependant, ces URL doivent être disponibles sur toute instance de création (`<hostname>:<port>`).

### Console de gestion des tâches Sling {#sling-job-handling-console}

`http://localhost:4502/system/console/slingevent`

La console de gestion des tâches Sling affichera :

* Les statistiques sur l’état des tâches dans le système depuis le dernier redémarrage.
* Elle affiche également les configurations de toutes les files d’attente de tâches et fournit un raccourci permettant de les modifier dans le gestionnaire de configuration.

### Outil de création de rapports de workflows {#workflow-report-tool}

L’outil de création de rapports de workflows est supprimé dans la version 6.3 pour éviter une dégradation des performances.

### MBean des opérations de maintenance des workflows {#workflow-maintenance-operations-mbean}

`http://localhost:4502/system/console/jmx/com.adobe.granite.workflow:type=Maintenance`

Le MBean de maintenance des workflows expose plusieurs routines de maintenance bien utiles, telles que la purge des workflows terminés et la récupération de statistiques sur les workflows.

## Informations supplémentaires {#further-information}

Pour plus d’informations, consultez :

* [Utilisation des workflows](/help/sites-authoring/workflows.md)
* [Administration des workflows](/help/sites-administering/workflows.md)
* [Développement et extension des workflows](/help/sites-developing/workflows.md)
* [Optimisation des performances](/help/sites-deploying/configuring-performance.md)
