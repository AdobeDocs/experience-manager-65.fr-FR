---
title: Dépannage des index Oak
description: Découvrez comment savoir si l’indexation est lente, en trouver la cause et résoudre le problème.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
exl-id: 85981463-189c-4f50-9d21-1d2f734b960a
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '1387'
ht-degree: 100%

---

# Dépannage des index Oak{#troubleshooting-oak-indexes}

## Réindexation lente  {#slow-re-indexing}

Le processus de réindexation interne d’AEM collecte les données du référentiel et les stocke dans les index Oak afin de prendre en charge l’interrogation performante du contenu. Dans des circonstances exceptionnelles, le processus peut être lent, voire bloqué. Cette page sert de guide de dépannage pour aider à identifier si l’indexation est lente, trouver la cause et résoudre le problème.

Il est important de faire la distinction entre une réindexation qui prend trop de temps et une réindexation qui prend beaucoup de temps parce qu’elle indexe de grandes quantités de contenu. Par exemple, le temps nécessaire pour indexer le contenu est proportionnel à la quantité de contenu, de sorte que les référentiels de production volumineux prennent plus de temps à réindexer que les petits référentiels de développement.

Voir [Bonnes pratiques relatives aux requêtes et à l’indexation](/help/sites-deploying/best-practices-for-queries-and-indexing.md) pour plus d’informations sur quand et comment réindexer le contenu.

## Détection initiale {#initial-detection}

L’indexation lente de la détection initiale nécessite de parcourir les MBeans JMX `IndexStats`. Sur l’instance AEM affectée, procédez comme suit :

1. Ouvrez la console web, cliquez sur l’onglet JMX ou rendez-vous sur https://&lt;host>:&lt;port>/system/console/jmx (par exemple, [http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx)).
1. Accédez aux MBeans `IndexStats`.
1. Ouvrez le MBeans `IndexStats` pour « `async` » et « `fulltext-async` ».

1. Pour les deux MBeans, vérifiez si les horodatages **Done** et **LastIndexTime** datent de moins de 45 minutes.

1. Pour un MBean, si la valeur temporelle (**Done** ou **LastIndexedTime**) date de plus de 45 minutes, alors la tâche d’indexation a échoué ou prend trop de temps. Ce problème rend les index asynchrones obsolètes.

## L’indexation est suspendue après un arrêt forcé. {#indexing-is-paused-after-a-forced-shutdown}

En cas d’arrêt forcé, AEM suspend l’indexation asynchrone pendant 30 minutes au maximum après le redémarrage. Il faut généralement 15 minutes supplémentaires pour terminer la première phase de réindexation, pour un total d’environ 45 minutes (ce qui correspond au délai de [détection initiale](/help/sites-deploying/troubleshooting-oak-indexes.md#initial-detection) de 45 minutes). Si l’indexation est suspendue après un arrêt forcé :

1. Tout d’abord, déterminez si l’instance d’AEM a été arrêtée de manière forcée (le processus AEM a été interrompu par la force ou à cause d’une coupure de courant) et redémarré ultérieurement.

   * [La journalisation AEM](/help/sites-deploying/configure-logging.md) peut être consultée à cet effet.

1. En cas d’arrêt forcé, AEM suspend automatiquement la réindexation pendant 30 minutes au maximum lors du redémarrage.
1. Patientez environ 45 minutes pour qu’AEM reprenne les opérations d’indexation asynchrones normales.

## Pool de threads surchargé {#thread-pool-overloaded}

>[!NOTE]
>
>Pour AEM 6.1, assurez-vous que le [CFP 11 AEM 6.1](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=fr) est installé.

Dans des circonstances exceptionnelles, le pool de threads utilisé pour gérer l’indexation asynchrone peut être surchargé. Pour isoler le processus d’indexation, vous pouvez configurer un pool de threads afin d’éviter qu’une autre tâche d’AEM interfère avec la capacité d’indexer du contenu en temps voulu d’Oak. Dans ce cas, procédez comme suit :

1. Définissez un nouveau pool de threads isolé à utiliser par le planificateur Apache Sling pour l’indexation asynchrone :

   * Sur l’instance affectée, accédez à la console web AEM OSGi > Configuration > Planificateur Apache Sling ou rendez-vous sur https://&lt;hôte>:&lt;port>/system/console/configMgr (par exemple, [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)).
   * Ajoutez une entrée au champ « Pools de threads autorisés » avec la valeur « oak ».
   * Pour enregistrer les modifications, cliquez sur **Enregistrer** en bas à droite.

   ![chlimage_1-119](assets/chlimage_1-119.png)

1. Vérifiez que le nouveau pool de threads du planificateur Apache Sling est enregistré et s’affiche dans la console web Statut du planificateur Apache Sling.

   * Accédez à la console web AEM OSGi > Statut > Planificateur Sling ou rendez-vous sur https://&lt;hôte>:&lt;port>/system/console/status-slingscheduler (par exemple, [http://localhost:4502/system/console/status-slingscheduler](http://localhost:4502/system/console/status-slingscheduler)).
   * Vérifiez que les entrées de pool suivantes existent :

      * ApacheSlingoak
      * ApacheSlingdefault

   ![chlimage_1-120](assets/chlimage_1-120.png)

## La file d’attente d’observation est pleine. {#observation-queue-is-full}

Si trop de modifications et de validations sont effectuées dans le référentiel dans un délai court, l’indexation peut être retardée, car la file d’attente d’observation est pleine. Tout d’abord, déterminez si la file d’attente d’observation est pleine :

1. Accédez à la console web et cliquez sur l’onglet JMX ou rendez-vous sur https://&lt;hôte>:&lt;port>/system/console/jmx (par exemple, [http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx)).
1. Ouvrez le MBean Statistiques de référentiel Oak et déterminez si une valeur `ObservationQueueMaxLength` est supérieure à 10 000.

   * Lors de l’exécution d’opérations normales, cette valeur maximale doit toujours finalement se réduire à zéro (surtout dans la section `per second`). Vérifiez donc que la mesure en secondes de `ObservationQueueMaxLength` est de 0.
   * Si les valeurs sont supérieures ou égales à 10 000 et augmentent régulièrement, cela indique que le traitement d’au moins une file d’attente (peut-être plus) ne suit pas le rythme des nouvelles modifications (validations).
   * Chaque file d’attente d’observation a une limite (10 000 par défaut) et le traitement ralentit au-dessus de cette limite.
   * Lorsque vous utilisez MongoMK, comme la longueur des files d’attente augmente beaucoup, la performance du cache Oak interne se détériore. Cette corrélation peut être vue dans un `missRate` augmenté pour le cache `DocChildren` dans le MBean de statistiques `Consolidated Cache`.

1. Pour éviter de dépasser les limites acceptables des files d’attente d’observation, il est recommandé de :

   * réduire le taux constant de validations. De courts pics de validations sont acceptables, mais il faut réduire le taux constant.
   * Augmentez la taille de `DiffCache` tel que décrit dans [Conseils de réglages de performance > Réglage du stockage Mongo > Taille du cache des documents](/help/sites-deploying/configuring-performance.md).

## Identifier et corriger un processus de réindexation bloqué {#identifying-and-remediating-a-stuck-re-indexing-process}

La réindexation peut être considérée comme « complètement bloquée » dans deux conditions :

* La réindexation est lente, au point où aucune progression significative n’est signalée dans les fichiers journaux concernant le nombre de nœuds parcourus.

   * Par exemple, s’il n’y a aucun message pendant une heure ou si la progression est si lente qu’il faut une semaine ou plus pour terminer.

* La réindexation est bloquée dans une boucle sans fin si des exceptions répétées apparaissent dans les fichiers journaux (par exemple, `OutOfMemoryException`) dans le thread d’indexation. La répétition d’une ou de plusieurs exceptions identiques dans le journal indique qu’Oak tente d’indexer la même chose à plusieurs reprises, mais échoue à cause du même problème à chaque fois.

Pour identifier et corriger un processus de réindexation bloqué, procédez comme suit :

1. Pour identifier la cause de l’indexation bloquée, collectez les informations suivantes :

   * Collectez 5 minutes d’instantanés de thread, un instantané de thread toutes les 2 secondes.
   * [Définition du niveau DEBUG et des journaux pour les appenders](/help/sites-deploying/configure-logging.md).

      * *org.apache.jackrabbit.oak.plugins.index.AsyncIndexUpdate*
      * *org.apache.jackrabbit.oak.plugins.index.IndexUpdate*

   * Rassemblez les données du MBean asynchrone `IndexStats` :

      * Accédez à le console web OSGi AEM > Principal > JMX > IndexStat > async

        ou rendez-vous sur [http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Dasync%2Ctype%3DIndexStats](http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Dasync%2Ctype%3DIndexStats).

   * Utilisez le [mode console de oak-run.jar](https://github.com/apache/jackrabbit-oak/tree/trunk/oak-run) pour collecter les informations de ce qui se trouve sous le nœud *`/:async`*.
   * Collectez une liste des points de contrôle du référentiel à l’aide du MBean `CheckpointManager` :

      * Console web OSGi AEM > Principal > JMX > CheckpointManager > listCheckpoints()

        ou rendez-vous sur [http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3DSegment+node+store+checkpoint+management%2Ctype%3DCheckpointManager](http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3DSegment+node+store+checkpoint+management%2Ctype%3DCheckpointManager).

1. Après la collecte de toutes les informations décrites à l’étape 1, redémarrez AEM.

   * Le redémarrage d’AEM peut résoudre le problème dans le cas d’une charge simultanée élevée (débordement de la file d’attente d’observation ou situation similaire).
   * Si un redémarrage ne permet pas de résoudre le problème, signalez-le à l’[Assistance clientèle d’Adobe](https://experienceleague.adobe.com/?support-solution=General&amp;lang=fr&amp;support-tab=home#support) et fournissez toutes les informations collectées lors de l’étape 1.

## Abandon sécurisé de la réindexation asynchrone {#safely-aborting-asynchronous-re-indexing}

La réindexation peut également être annulée (arrêtée avant qu’elle ne soit terminée) via les pistes d’indexation `async, async-reindex` et `ulltext-async` (MBean `IndexStats`). Pour plus d’informations, consultez la documentation Apache Oak dans la section [Abandon de la réindexation](https://jackrabbit.apache.org/oak/docs/query/indexing.html#abort-reindex). Tenez également compte des points suivants :

* La réindexation des index Lucene et des propriétés Lucene peut être annulée, car elle est naturellement asynchrone.
* La réindexation des index de propriété Oak ne peut être annulée si la réindexation a été initiée via le `PropertyIndexAsyncReindexMBean`.

Pour annuler la réindexation en toute sécurité, procédez comme suit :

1. Identifiez le MBean IndexStats qui contrôle la piste de réindexation qui doit être arrêtée.

   * Accédez au MBean IndexStats approprié via la console JMX en accédant à la console web OSGi d’AEM > Principal > JMX ou à https://&lt;host>:&lt;port>/system/console/jmx (par exemple, [http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx)).
   * Ouvrez le MBean IndexStats basé sur la piste de réindexation que vous souhaitez arrêter (`async`, `async-reindex` ou `fulltext-async`).

      * Pour identifier la piste appropriée et donc l’instance MBean IndexStats, regardez la propriété « async » des index Oak. La propriété « async » contient le nom de piste `async`, `async-reindex` ou `fulltext-async`.
      * La piste est également disponible dans la colonne « Async » du gestionnaire d’index d’AEM. Pour accéder au gestionnaire d’index, accédez à Opérations > Diagnostic > Gestionnaire d’index.

   ![chlimage_1-121](assets/chlimage_1-121.png)

1. Invoquez la commande `abortAndPause()` sur le MBean `IndexStats` approprié.
1. Marquez la définition d’index Oak de manière appropriée pour éviter la reprise de la réindexation lors du redémarrage de la piste d’indexation.

   * Lors de la réindexation d’un index **existant**, définissez la propriété Reindex sur false.

      * `/oak:index/someExistingIndex@reindex=false`

   * Ou sinon, pour un **nouvel** index, procédez d’une des manières suivantes :

      * définissez la propriété de type sur désactivé ;

         * `/oak:index/someNewIndex@type=disabled`

      * ou supprimez entièrement la définition de l’index.

   Validez les modifications apportées au référentiel une fois l’opération terminée.

1. Enfin, reprenez l’indexation asynchrone sur la piste d’indexation annulée.

   * Dans le MBean `IndexStats` qui a envoyé la commande `abortAndPause()` à l’étape 2, invoquez la commande `resume()`.

## Prévenir la réindexation lente {#preventing-slow-re-indexing}

Il est préférable de procéder à la réindexation pendant les périodes calmes (et non pas pendant une grande ingestion de contenu, par exemple) et idéalement pendant les fenêtres de maintenance lorsque la charge d’AEM est connue et contrôlée. En outre, assurez-vous que la réindexation n’a pas lieu en même temps que d’autres activités de maintenance.
