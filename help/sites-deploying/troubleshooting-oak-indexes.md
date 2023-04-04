---
title: Dépannage des index Oak
seo-title: Troubleshooting Oak Indexes
description: Comment détecter et corriger une réindexation lente.
uuid: 6567ddae-128c-4302-b7e8-8befa66b1f43
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: ea70758f-6726-4634-bfb4-a957187baef0
exl-id: 85981463-189c-4f50-9d21-1d2f734b960a
source-git-commit: 9defa6d1843007e9375d839f72f6993c691a37c0
workflow-type: tm+mt
source-wordcount: '1474'
ht-degree: 38%

---

# Dépannage des index Oak{#troubleshooting-oak-indexes}

## Réindexation lente  {#slow-re-indexing}

AEM processus de réindexation interne collecte les données du référentiel et les stocke dans les index Oak afin de prendre en charge l’interrogation performante du contenu. Dans des circonstances exceptionnelles, le processus peut être lent, voire bloqué. Cette page sert de guide de dépannage pour aider à identifier si l’indexation est lente, trouver la cause et résoudre le problème.

Il est important de faire la distinction entre la réindexation qui prend un temps incorrectement long et la réindexation qui prend beaucoup de temps parce qu’elle indexe de grandes quantités de contenu. Par exemple, le temps nécessaire pour indexer le contenu est mis à l’échelle avec la quantité de contenu, de sorte que les référentiels de production volumineux prennent plus de temps à réindexer que les petits référentiels de développement.

Voir [Bonnes pratiques relatives aux requêtes et à l’indexation](/help/sites-deploying/best-practices-for-queries-and-indexing.md) pour plus d’informations sur quand et comment réindexer le contenu.

## Détection initiale {#initial-detection}

L’indexation lente de la détection initiale nécessite de parcourir les MBeans JMX `IndexStats`. Sur l’instance AEM affectée, procédez comme suit :

1. Ouvrez la console web, cliquez sur l’onglet JMX ou rendez-vous sur https://&lt;host>:&lt;port>/system/console/jmx (par exemple, [http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx)).
1. Accédez aux MBeans `IndexStats`.
1. Ouvrez le MBeans `IndexStats` pour « `async` » et « `fulltext-async` ».

1. Pour les deux MBeans, vérifiez si les horodatages **Done** et **LastIndexTime** datent de moins de 45 minutes.

1. Pour un MBean, si la valeur temporelle (**Done** ou **LastIndexedTime**) date de plus de 45 minutes, alors la tâche d’indexation a échoué ou prend trop de temps. Ce problème entraîne l’obsolescence des index asynchrones.

## L’indexation est suspendue après un arrêt forcé {#indexing-is-paused-after-a-forced-shutdown}

Un arrêt forcé entraîne AEM suspension de l’indexation asynchrone pendant 30 minutes au maximum après le redémarrage. En outre, il faut généralement 15 minutes supplémentaires pour terminer la première passe de réindexation, pour un total d’environ 45 minutes (en revenant à la variable [Détection initiale](/help/sites-deploying/troubleshooting-oak-indexes.md#initial-detection) période de 45 minutes). Si l’indexation est suspendue après un arrêt forcé :

1. Tout d’abord, déterminez si l’instance d’AEM a été arrêtée de manière forcée (le processus d’AEM a été interrompu par la force ou une panne d’alimentation s’est produite) et redémarrez ultérieurement.

   * [La journalisation AEM](/help/sites-deploying/configure-logging.md) peut être consultée à cet effet.

1. Si l’arrêt forcé s’est produit, au redémarrage, AEM arrête automatiquement la réindexation pendant 30 minutes au maximum.
1. Patientez environ 45 minutes pour que AEM reprenne les opérations d’indexation asynchrones normales.

## Pool de threads surchargé {#thread-pool-overloaded}

>[!NOTE]
>
>Pour AEM 6.1, assurez-vous que le [CFP 11 AEM 6.1](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=fr) est installé.

Dans des circonstances exceptionnelles, le pool de threads utilisé pour gérer l’indexation asynchrone peut devenir surchargé. Pour isoler le processus d’indexation, un pool de threads peut être configuré afin d’empêcher le travail d’autres AEM d’interférer avec la capacité d’index du contenu d’une manière opportune d’Oak. Dans ce cas, procédez comme suit :

1. Définissez un nouveau pool de threads isolé à utiliser par le planificateur Apache Sling pour l’indexation asynchrone :

   * Sur l’instance affectée, accédez à la console web AEM OSGi > Configuration > Planificateur Apache Sling ou rendez-vous sur https://&lt;hôte>:&lt;port>/system/console/configMgr (par exemple, [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)).
   * Ajoutez une entrée au champ &quot;Pools de threads autorisés&quot; avec la valeur &quot;oak&quot;.
   * Pour enregistrer les modifications, cliquez sur **Enregistrer** en bas à droite.

   ![chlimage_1-119](assets/chlimage_1-119.png)

1. Vérifiez que le nouveau pool de threads du planificateur Apache Sling est enregistré et s’affiche dans la console web d’état du planificateur Apache Sling.

   * Accédez à la console web AEM OSGi > Statut > Planificateur Sling ou rendez-vous sur https://&lt;hôte>:&lt;port>/system/console/status-slingscheduler (par exemple, [http://localhost:4502/system/console/status-slingscheduler](http://localhost:4502/system/console/status-slingscheduler)).
   * Vérifiez que les entrées de pool suivantes existent :

      * ApacheSlingoak
      * ApacheSlingdefault

   ![chlimage_1-120](assets/chlimage_1-120.png)

## La file d&#39;attente d&#39;observation est pleine {#observation-queue-is-full}

Si trop de modifications et de validations sont effectuées dans le référentiel dans un délai court, l’indexation peut être retardée en raison d’une file d’attente d’observation complète. Tout d’abord, déterminez si la file d’attente d’observation est pleine :

1. Accédez à la console web et cliquez sur l’onglet JMX ou rendez-vous sur https://&lt;hôte>:&lt;port>/system/console/jmx (par exemple, [http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx)).
1. Ouvrez le MBean Statistiques de référentiel Oak et déterminez si une valeur `ObservationQueueMaxLength` est supérieure à 10 000. 

   * Lors de l’exécution d’opérations normales, cette valeur maximale doit toujours finalement se réduire à zéro (surtout dans la section `per second`). Vérifiez donc que la mesure en secondes de `ObservationQueueMaxLength` est de 0.
   * Si les valeurs sont supérieures ou égales à 10 000 et augmentent régulièrement, cela indique qu’au moins une file d’attente (peut-être plus) ne peut pas être traitée aussi rapidement que de nouvelles modifications (validations) se produisent.
   * Chaque file d’attente d’observation a une limite (10 000 par défaut) et si la file d’attente atteint cette limite, son traitement se dégrade.
   * Lorsque vous utilisez MongoMK, comme la longueur des files d’attente augmente beaucoup, la performance du cache Oak interne se détériore. Cette corrélation peut être vue dans un `missRate` augmenté pour le cache `DocChildren` dans le MBean de statistiques `Consolidated Cache`.

1. Pour éviter de dépasser les limites acceptables des files d’attente d’observation, il est recommandé de :

   * Réduisez le taux constant de validations. De courts pics de validations sont acceptables, mais le taux constant doit être réduit.
   * Augmentez la taille de `DiffCache` tel que décrit dans [Conseils de réglages de performance > Réglage du stockage Mongo > Taille du cache des documents](https://experienceleague.adobe.com/docs/experience-manager-64/deploying/configuring/configuring-performance.html?lang=en).

## Identification et correction d’un processus de réindexation bloqué {#identifying-and-remediating-a-stuck-re-indexing-process}

La réindexation peut être considérée comme &quot;complètement bloquée&quot; dans deux conditions :

* La réindexation est lente, au point où aucune progression significative n’est signalée dans les fichiers journaux concernant le nombre de noeuds parcourus.

   * Par exemple, s’il n’y a aucun message sur une heure ou si la progression est si lente qu’il faut une semaine ou plus pour finir.

* La réindexation est bloquée dans une boucle infinie si des exceptions répétées apparaissent dans les fichiers journaux (par exemple, `OutOfMemoryException`) dans le thread d’indexation. La répétition d’une ou de plusieurs mêmes exceptions dans le journal indique qu’Oak tente d’indexer la même chose à plusieurs reprises, mais échoue sur le même problème.

Pour identifier et corriger un processus de réindexation bloqué, procédez comme suit :

1. Pour identifier la cause de l’indexation bloquée, les informations suivantes doivent être collectées :

   * Collectez 5 minutes de thread dump, un thread dump toutes les 2 secondes.
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

   * Le redémarrage de l’AEM peut résoudre le problème en cas de charge simultanée élevée (débordement de la file d’attente d’observation ou autre problème similaire).
   * Si un redémarrage ne permet pas de résoudre le problème, signalez-le à l’[Assistance clientèle d’Adobe](https://experienceleague.adobe.com/?support-solution=General&amp;lang=fr&amp;support-tab=home#support) et fournissez toutes les informations collectées lors de l’étape 1.

## Abandon sécurisé de la réindexation asynchrone {#safely-aborting-asynchronous-re-indexing}

La réindexation peut être abandonnée en toute sécurité (arrêtée avant d’être terminée) via le `async, async-reindex`et f `ulltext-async` pistes d’indexation ( `IndexStats` Mbean). Pour plus d’informations, consultez la documentation Apache Oak dans la section [Abandon de la réindexation](https://jackrabbit.apache.org/oak/docs/query/indexing.html#abort-reindex). Tenez également compte des points suivants :

* La réindexation des index de propriété Lucene et Lucene peut être abandonnée, car ils sont naturellement asynchrones.
* La réindexation des index de propriété Oak ne peut être abandonnée que si la réindexation a été lancée via l’événement `PropertyIndexAsyncReindexMBean`.

Pour annuler la réindexation en toute sécurité, procédez comme suit :

1. Identifiez le MBean IndexStats qui contrôle la piste de réindexation qui doit être arrêtée.

   * Accédez au MBean IndexStats approprié via la console JMX en accédant à la console web OSGi AEM > Principal > JMX ou à https://&lt;hôte>:&lt;port>/system/console/jmx (par exemple, [http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx)).
   * Ouvrez le MBean IndexStats en fonction de la piste de réindexation que vous souhaitez arrêter ( `async`, `async-reindex`ou `fulltext-async`)

      * Pour identifier la piste appropriée et donc l’instance MBean IndexStats, regardez la propriété « async » des index Oak. La propriété &quot;async&quot; contient le nom de la piste : `async`, `async-reindex`ou `fulltext-async`.
      * La piste est également disponible en accédant à AEM Gestionnaire d’index dans la colonne &quot;Async&quot;. Pour accéder au gestionnaire d’index, accédez à Opérations > Diagnostic > Gestionnaire d’index.

   ![chlimage_1-121](assets/chlimage_1-121.png)

1. Invoquez la commande `abortAndPause()` sur le MBean `IndexStats` approprié.
1. Marquez la définition d’index Oak de manière appropriée pour empêcher la reprise de la réindexation lorsque la piste d’indexation reprend.

   * Lors de la réindexation d’une **existant** index, définissez la propriété reindex sur false

      * `/oak:index/someExistingIndex@reindex=false`
   * Ou sinon, pour un **new** index, soit :

      * Définissez la propriété type sur disabled

         * `/oak:index/someNewIndex@type=disabled`
      * ou supprimer entièrement la définition d’index

   Validez les modifications apportées au référentiel une fois l’opération terminée.

1. Enfin, reprenez l’indexation asynchrone sur la piste d’indexation abandonnée.

   * Dans le MBean `IndexStats` qui a envoyé la commande `abortAndPause()` à l’étape 2, invoquez la commande `resume()`.

## Prévention de la réindexation lente {#preventing-slow-re-indexing}

Il est préférable de procéder à une réindexation pendant les périodes de silence (par exemple, pas lors d’une ingestion de contenu importante), et idéalement pendant les fenêtres de maintenance lorsque AEM chargement est connu et contrôlé. Assurez-vous également que la réindexation n’a pas lieu pendant d’autres activités de maintenance.
