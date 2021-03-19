---
title: Meilleures pratiques en matière de workflow
seo-title: Meilleures pratiques en matière de workflow
description: Meilleures pratiques en matière de workflow
seo-description: 'null'
uuid: 79be4055-c2ef-428e-9054-103c6cfde1d2
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 0be8b88c-6f57-4dcc-ae11-77b378a2decd
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1924'
ht-degree: 91%

---


# Meilleures pratiques en matière de workflow{#workflow-best-practices}

Les workflows vous permettent d’automatiser les activités d’Adobe Experience Manager (AEM).

Ils représentent généralement une bonne partie du traitement effectué dans un environnement AEM. Par conséquent, lorsque des étapes de workflow personnalisées ne sont pas écrites conformément aux meilleures pratiques ou lorsque des workflows standard (prêts à l’emploi) ne sont pas configurés pour s’exécuter le plus efficacement possible, cela peut avoir une incidence sur le système.

Il est donc vivement conseillé de planifier soigneusement vos implémentations de workflow.

## Configuration {#configuration}

Lors de la configuration des processus de workflow (qu’ils soient personnalisés et/ou standard), vous devez tenir compte de plusieurs éléments.

### Workflows transitoires {#transient-workflows}

Pour optimiser les charges d’assimilation élevées, vous pouvez définir un [workflow comme étant transitoire](/help/sites-developing/workflows.md#transient-workflows).

Lorsqu’un workflow est transitoire, les données d’exécution liées aux étapes intermédiaires ne sont pas conservées dans le JCR lors de leur exécution (les rendus en sortie sont, bien évidemment, conservés).

Cela peut se traduire par divers avantages :

* Réduction du temps de traitement des workflows pouvant atteindre 10 %.
* Réduction sensible de la croissance du référentiel.
* Il n’y a plus de workflow CRUD à purger.
* Cela réduit, en outre, le nombre de fichiers TAR à compacter.

>[!CAUTION]
>
>Si votre entreprise impose la conservation/l’archivage des données d’exécution de workflow à des fins d’audit, n’activez pas cette fonctionnalité.

### Optimisation des workflows DAM {#tuning-dam-workflows}

Pour obtenir des conseils en matière d’optimisation des performances pour les workflows DAM, reportez-vous au [Guide d’optimisation des performances d’AEM Assets](/help/assets/performance-tuning-guidelines.md).

### Configuration du nombre maximum de workflows simultanés {#configure-the-maximum-number-of-concurrent-workflows}

AEM peut autoriser l’exécution simultanée de plusieurs threads de workflow. Par défaut, le nombre de threads est configuré sur la moitié du nombre de cœurs de processeur du système.

Si les workflows en cours d’exécution consomment de nombreuses ressources système, AEM risque de tomber à court de ressources pour effectuer d’autres tâches, telles que le rendu de l’interface utilisateur de création. Par conséquent, le système peut afficher une certaine lenteur au cours d’activités telles qu’un téléchargement massif d’images.

Pour remédier à ce problème, Adobe recommande de configurer le **nombre maximal de tâches en parallèle** sur une valeur comprise entre 50 % et 75 % du nombre de cœurs de processeur du système. Cela devrait laisser suffisamment de capacité de réaction au système lors du traitement de ces workflows.

Pour configurer **Nombre maximal de tâches parallèles**, vous pouvez effectuer l&#39;une des opérations suivantes :

* Configurez la **[configuration OSGi](/help/sites-deploying/configuring-osgi.md)** à partir de la console Web AEM ; pour **File d&#39;attente : Granite Workflow Queue** (une **configuration de la file d’attente de travaux Apache Sling**).

* Configurez la file d&#39;attente à partir de l&#39;option **Sling Jobs** de la console Web AEM ; pour **Configuration de la file d&#39;attente de travaux : Granite Workflow Queue**, `http://localhost:4502/system/console/slingevent`.

En outre, il existe une configuration distincte pour la **file d&#39;attente de travaux de processus externe Granite Workflow**. Elle est utilisée pour les processus de workflow qui lancent des fichiers binaires externes, tels que **InDesign Server** ou **Image Magick**.

### Configuration de différentes files d’attente de tâches  {#configure-individual-job-queues}

Dans certains cas, il peut être utile de configurer différentes files d’attente pour contrôler des threads simultanés, ou d’autres options de file d’attente, sur la base d’une tâche individuelle. Vous pouvez ajouter et configurer une file d’attente distincte à partir de la console web via la fabrique **Configuration de la file d’attente de tâches Apache Sling**. Pour rechercher la rubrique appropriée à liste, exécutez le modèle de votre flux de travail et recherchez-le dans la console **Sling Jobs** ; par exemple, à `http://localhost:4502/system/console/slingevent`.

Des files d’attente individuelles peuvent également être ajoutées pour les workflows transitoires.

### Configuration de la purge des workflows {#configure-workflow-purging}

Dans une installation standard, AEM fournit une console de maintenance dans laquelle il est possible de planifier et de configurer des activités de maintenance quotidiennes et hebdomadaires ; par exemple, à l’adresse :

`http://localhost:4502/libs/granite/operations/content/maintenance.html`

Par défaut, la **Période de maintenance hebdomadaire** comporte une tâche **Purge du workflow**, mais celle-ci doit être configurée avant l’exécution. Pour configurer des purges de workflow, une nouvelle **configuration de la purge du workflow d’Adobe Granite** doit être ajoutée dans la console web.

Pour plus d’informations sur les tâches de maintenance dans AEM, consultez le [Tableau de bord des opérations](/help/sites-administering/operations-dashboard.md).

## Personnalisation  {#customization}

Lorsque vous créez des processus de workflow personnalisés, vous devez tenir compte de plusieurs éléments.

### Emplacements {#locations}

Les définitions de modèles de workflow, lanceurs, scripts et notifications sont conservées dans le référentiel en fonction de leur type ; par exemple, prêt à l’emploi, personnalisé, etc.

>[!NOTE]
>
>Voir aussi [Restructuration du référentiel dans AEM 6.5](/help/sites-deploying/repository-restructuring.md).

#### Emplacements – Modèles de workflow {#locations-workflow-models}

Les modèles de workflow sont stockés dans le référentiel en fonction de leur type :

* Les conceptions de workflow standard sont conservées à l’emplacement suivant :

   `/libs/settings/workflow/models/`

   >[!CAUTION]
   >
   >Veuillez ne pas :
   >
   >* placer vos modèles de workflow personnalisés dans ce dossier,
   >* modifier tout élément dans `/libs`

   >
   >car les modifications peuvent être écrasées lors de la mise à niveau ou lors de l’installation de correctifs logiciels, de Service Packs ou de packs de correctifs cumulatifs.

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
   >Si ces conceptions sont modifiées à l’aide de l’*IU AEM*, les détails seront copiés aux nouveaux emplacements.

#### Emplacements – Lanceurs de workflow  {#locations-workflow-launchers}

Les définitions du lanceur de workflow sont également stockées dans le référentiel en fonction de leur type :

* Les lanceurs de workflow prêts à l’emploi (ou standard) sont conservés à l’emplacement suivant :

   `/libs/settings/workflow/launcher/`

   >[!CAUTION]
   >
   >Veuillez ne pas :
   >
   >* placer vos lanceurs de workflow personnalisés dans ce dossier,
   >* modifier tout élément dans `/libs`

   >
   >car les modifications peuvent être écrasées lors de la mise à niveau ou lors de l’installation de correctifs logiciels, de Service Packs ou de packs de correctifs cumulatifs.

* Les lanceurs de workflow personnalisés sont conservés à l’emplacement suivant :

   ```
   /conf/global/settings/workflow/launcher/...
   ```

* Les lanceurs de workflow hérités sont conservés à l’emplacement suivant :

   `/etc/workflow/launcher/`

   >[!NOTE]
   >
   >Si ces définitions sont modifiées à l’aide de l’*IU AEM*, les détails seront copiés aux nouveaux emplacements.

#### Emplacements – Scripts de workflow  {#locations-workflow-scripts}

Les scripts de workflow sont également stockés dans le référentiel en fonction de leur type :

* Les scripts de workflow prêts à l’emploi (ou standard) sont conservés à l’emplacement suivant :

   `/libs/workflow/scripts/`

   >[!CAUTION]
   >
   >Veuillez ne pas :
   >
   >* placer vos scripts de workflow personnalisés dans ce dossier,
   >* modifier tout élément dans `/libs`

   >
   >car les modifications peuvent être écrasées lors de la mise à niveau ou lors de l’installation de correctifs logiciels, de Service Packs ou de packs de correctifs cumulatifs.

* Les scripts de workflow personnalisés sont conservés à l’emplacement suivant :

   ```
   /apps/workflow/scripts/...
   ```

* Les scripts de workflow hérités sont conservés à l’emplacement suivant :

   `/etc/workflow/scripts/`

#### Emplacements – Notifications de workflow {#locations-workflow-notifications}

Les notifications de workflow sont également stockées dans le référentiel en fonction de leur type :

* Les définitions de notification de workflow prêtes à l’emploi (ou standard) sont conservées à l’emplacement suivant :

   `/libs/settings/workflow/notification/`

   >[!CAUTION]
   >
   >Veuillez ne pas :
   >
   >* placer vos définitions de notification de workflow personnalisées dans ce dossier,
   >* modifier tout élément dans `/libs`

   >
   >car les modifications peuvent être écrasées lors de la mise à niveau ou lors de l’installation de correctifs logiciels, de Service Packs ou de packs de correctifs cumulatifs.

* Les définitions de notification de workflow personnalisées sont conservées à l’emplacement suivant :

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

Comme dans tout développement personnalisé, il est recommandé d’utiliser, dans la mesure du possible, la session d’un utilisateur :

* pour une meilleure conformité avec les directives de sécurité ;
* pour permettre au système de gérer l’ouverture et la fermeture de la session.

Lors de la mise en œuvre d’un processus de workflow :

* Une session de workflow est fournie et doit être utilisée, sauf s’il y a une bonne raison de ne pas le faire.
* Vous ne devez pas créer de sessions à partir des étapes de workflow, car cela entraîne des incohérences au niveau des états, ainsi que de possibles problèmes de simultanéité dans le moteur de workflow.
* Vous ne devez pas acquérir une nouvelle session JCR depuis une étape de workflow. Vous devez plutôt adapter la session de workflow fournie par l’API Étape du processus à une session JCR. Par exemple :

```
public void execute(WorkItem item, WorkflowSession workflowSession, MetaDataMap args) throws WorkflowException {
        // to obtain a jcr session:
        javax.jcr.Session jcrSession = workflowSession.adaptTo(javax.jcr.Session.class);

        // to obtain a sling resource resolver:
        org.apache.sling.api.resource.ResourceResolver slingResourceResolver = workflowSession.adaptTo(org.apache.sling.api.resource.ResourceResolver.class);
```

Enregistrement d’une session :

* Dans un processus de processus, si `WorkflowSession` est utilisé pour modifier le référentiel, n&#39;enregistrez pas explicitement la session. Le processus enregistre la session une fois terminée.
* `Session.Save` ne doit pas être appelée à partir d’une étape de processus :

   * Il est recommandé d’adapter la session JCR du workflow ; une opération `save` n’est donc pas nécessaire, car le moteur de workflow enregistre automatiquement la session une fois l’exécution du workflow terminée.
   * Il est déconseillé qu’une étape du processus crée sa propre session JCR.

* En supprimant les enregistrements inutiles, vous pouvez réduire la surcharge et améliorer ainsi l’efficacité des workflows.

>[!CAUTION]
>
>Si vous créez quand même votre propre session JCR malgré ces recommandations, vous devrez l’enregistrer.

### Réduction du nombre/de la portée des lanceurs {#minimize-the-number-scope-of-launchers}

Un écouteur est responsable de tous les [lanceurs de workflow](/help/sites-administering/workflows-starting.md#workflows-launchers) qui sont enregistrés :

* Il recherche les modifications au niveau de tous les chemins d’accès spécifiés dans les propriétés d’expansion de nom de fichier des autres lanceurs.
* Lorsqu’un événement est distribué, le moteur de workflow évalue chaque lanceur afin de déterminer s’il doit s’exécuter.

Créer trop de lanceurs ralentira l’exécution du processus d’évaluation.

Si vous créez un chemin d’expansion de nom de fichier à la racine du référentiel d’un seul lanceur, le moteur de workflow va rechercher et évaluer les événements de création/modification sur chaque nœud du référentiel. C’est pourquoi il est recommandé de ne créer que des lanceurs qui sont nécessaires et de faire en sorte que le chemin d’expansion de nom de fichier soit aussi ciblé que possible.

Compte tenu de l’incidence de ces lanceurs sur le comportement des workflows, il peut également s’avérer utile de désactiver tout lanceur prêt à l’emploi qui n’est pas utilisé.

### Améliorations de la configuration pour les lanceurs {#configuration-enhancements-for-launchers}

La configuration personnalisée de [lanceur](/help/sites-administering/workflows-starting.md#workflows-launchers) a été améliorée pour prendre en charge les éléments suivants :

* Plusieurs conditions liées par l’opérateur « AND ».
* Conditions « OR » au sein d’une seule condition.
* Activation/désactivation des lanceurs selon qu’un indicateur de fonction est activé ou désactivé.
* Prise en charge d’expressions régulières (regex) dans des conditions de lanceur.

### Ne pas lancer de workflows à partir d’autres workflows {#do-not-start-workflows-from-other-workflows}

Les workflows peuvent occasionner une surcharge considérable, tant sur le plan des objets créés en mémoire que des nœuds suivis dans le référentiel. Pour cette raison, il est préférable de faire en sorte qu’un workflow effectue son traitement en interne plutôt que de lancer des workflows supplémentaires.

Il peut s’agir, par exemple, d’un workflow qui implémente une procédure métier sur un jeu de contenu, puis active ce contenu. Il est préférable de créer un processus de workflow personnalisé qui active chacun de ces nœuds, plutôt que de lancer un modèle **Activer le contenu** pour chacun des nœuds de contenu qui doivent être publiés. Cette méthode requiert certes des tâches de développement supplémentaires, mais elle s’avère plus efficace que de lancer une instance de workflow distincte pour chaque activation.

Autre exemple : un workflow qui traite plusieurs nœuds, crée un module de workflow, puis active ledit module. Plutôt que de créer le module et de lancer ensuite un workflow distinct avec le module comme charge utile, vous pouvez modifier la charge utile de votre workflow dans l’étape qui crée le module, puis appeler l’étape pour activer le module au sein du même modèle de workflow.

### Avance du gestionnaire {#handler-advance}

Lors de la conception d’un modèle de workflow, vous avez la possibilité d’activer l’avance du gestionnaire sur les étapes de votre workflow. Vous pouvez également ajouter du code à votre étape de workflow afin de déterminer l’étape qui doit être exécutée ensuite et procéder à son exécution.

Il est recommandé d’utiliser l’avance du gestionnaire, car elle offre les meilleures performances.

### Phases de processus {#workflow-stages}

Vous pouvez définir des [phases de processus](/help/sites-developing/workflows.md#workflow-stages), puis affecter des tâches/étapes à une phase spécifique.

Ces informations sont utilisées pour afficher la progression d’un workflow lorsque vous cliquez sur l’onglet [**Informations du processus** d’un élément de travail dans la **Boîte de réception**](/help/sites-authoring/workflows-participating.md#opening-a-workflow-item-to-view-details-and-take-actions). Les modèles de workflow existants peuvent être modifiés pour ajouter des phases.

### Étape Activer le processus de page {#activate-page-process-step}

L’étape **Activer le processus de page** active les pages à votre place. Cependant, elle ne recherche pas automatiquement les ressources DAM référencées et ne les active pas.

C’est un point dont vous devez tenir compte si vous prévoyez d’utiliser cette étape dans le cadre d’un modèle de workflow.

### Remarques concernant la mise à niveau {#upgrade-considerations}

Lors de la mise à niveau de votre instance :

* Assurez-vous que les modèles de workflow personnalisés ont été sauvegardés avant de mettre à niveau une instance.
* vérifiez qu’aucun de vos workflows personnalisés n’est enregistré [sous](#locations) :

   * `/libs/settings/workflow/models/projects`

>[!NOTE]
>
>Voir aussi [Restructuration du référentiel dans AEM 6.5](/help/sites-deploying/repository-restructuring.md).

## Outils système {#system-tools}

De nombreux outils système disponibles pour faciliter la surveillance, la gestion et le dépannage des workflows. Tous les exemples d’URL ci-dessous utilisent `localhost:4502`, mais doivent être disponibles sur toute instance d’auteur ( `<hostname>:<port>`).

### Console de gestion des tâches Sling {#sling-job-handling-console}

`http://localhost:4502/system/console/slingevent`

La console de gestion des tâches Sling affiche les éléments suivants :

* Statistiques sur l’état des tâches dans le système depuis le dernier redémarrage.
* Elle affiche également les configurations de toutes les files d’attente de tâches et fournit un raccourci permettant de les modifier dans le gestionnaire de configuration.

### Outil Rapport de workflow {#workflow-report-tool}

L’outil de création de rapports sur les workflows va être supprimé de la version 6.3 afin d’éviter une dégradation des performances.

### MBean des opérations de maintenance des workflows {#workflow-maintenance-operations-mbean}

`http://localhost:4502/system/console/jmx/com.adobe.granite.workflow:type=Maintenance`

Le MBean de maintenance des workflows expose plusieurs routines de maintenance bien utiles, telles que la purge des workflows terminés et la récupération de statistiques sur les workflows.

## Informations supplémentaires {#further-information}

Pour plus d’informations, voir :

* [Utilisation des workflows](/help/sites-authoring/workflows.md)
* [Administration des workflows](/help/sites-administering/workflows.md)
* [Développement et extension des workflows](/help/sites-developing/workflows.md)
* [Optimisation des performances](/help/sites-deploying/configuring-performance.md)