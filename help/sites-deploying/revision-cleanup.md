---
title: Nettoyage des révisions
seo-title: Nettoyage des révisions
description: Découvrez comment utiliser la fonction de nettoyage des révisions dans AEM 6.3.
seo-description: Découvrez comment utiliser la fonction de nettoyage des révisions dans AEM 6.3.
uuid: 321f5038-44b0-4f1e-a1aa-2d29074eed70
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: f03ebe60-88c0-4fc0-969f-949490a8e768
translation-type: tm+mt
source-git-commit: 2fc35bfd93585a586cb1d4e3299261611db49ba6
workflow-type: tm+mt
source-wordcount: '5916'
ht-degree: 67%

---


# Nettoyage des révisions{#revision-cleanup}

## Présentation {#introduction}

Chaque mise à jour du référentiel crée une nouvelle révision de contenu. Par conséquent, à chaque mise à jour, la taille du référentiel augmente. Pour éviter une croissance incontrôlée au référentiel, il faut nettoyer les anciennes révisions pour libérer de l’espace sur le disque. Cette fonctionnalité de maintenance est appelée le nettoyage des révisions. Elle est disponible sous forme de programme hors ligne depuis AEM 6.0.

Une version en ligne de cette fonctionnalité, baptisée Nettoyage des révisions en ligne, a été introduite dans AEM 6.3. Comparé au nettoyage des révisions hors ligne où l’instance AEM doit être arrêtée, le nettoyage des révisions en ligne peut être exécuté en maintenant l’instance AEM en ligne. Le nettoyage des révisions en ligne est activé par défaut, car il s’agit de la méthode recommandée pour effectuer un nettoyage des révisions.

**Remarque**: [Consultez la vidéo](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/revision-cleanup-technical-video-use.html) pour obtenir une introduction et savoir comment utiliser le nettoyage de la révision en ligne.

Le processus de nettoyage des révisions en ligne s’effectue en trois phases : **l’estimation**, **la compression** et **le nettoyage**. L’estimation permet de déterminer s’il est nécessaire d’exécuter la phase suivante (compressions) selon la quantité de mémoire pouvant être libérée. Pendant la phase de compression, les segments et les fichiers tar sont réécrits en omettant tout contenu inutilisé. La phase de nettoyage permet de supprimer par la suite les anciens segments, y compris toute la mémoire qu’ils peuvent contenir. Généralement, le mode hors ligne permet de récupérer plus d’espace, car le mode en ligne doit prendre en compte le système opérationel d’AEM, ce qui empêche certains segments d’être collectés.

Pour plus de détails sur le processus de nettoyage des révisions, consulter les liens suivants :

* [Exécution du nettoyage des révisions en ligne](/help/sites-deploying/revision-cleanup.md#how-to-run-online-revision-cleanup)
* [FAQ concernant le nettoyage des révisions en ligne](/help/sites-deploying/revision-cleanup.md#online-revision-cleanup-frequently-asked-questions)
* [Exécution du nettoyage des révisions hors ligne](/help/sites-deploying/revision-cleanup.md#how-to-run-offline-revision-cleanup)

Additionally, you can also read the [official Oak documentation.](https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html)

### When to use Online Revision Cleanup as opposed to Offline Revision Cleanup? {#when-to-use-online-revision-cleanup-as-opposed-to-offline-revision-cleanup}

**Il est recommandé de procéder au nettoyage des révisions en ligne.** L’utilisation du nettoyage des révisions hors ligne doit être limitée à des cas exceptionnels, par exemple, avant d’effectuer une migration vers un nouveau format de stockage ou si le service clientèle d’Adobe vous demande de le faire.

## Comment exécuter le nettoyage des révisions en ligne ?{#how-to-run-online-revision-cleanup}

Le nettoyage des révisions en ligne est programmé par défaut pour s’exécuter automatiquement une fois par jour sur les instances de publication et d’auteur d’AEM. Vous devez simplement définir la fenêtre de maintenance pendant une période où le niveau d’activité de l’utilisateur est aussi bas que possible. La nettoyage des révisions en ligne peut être configuré comme suit :

1. In the main AEM window, go to **Tools - Operations - Dashboard - Maintenance** or point your browser to: `https://serveraddress:serverport/libs/granite/operations/content/maintenance.html`

   ![chlimage_1-90](assets/chlimage_1-90.png)

1. Hover over **Daily Maintenance Window** and click the **Settings** icon.

   ![chlimage_1-91](assets/chlimage_1-91.png)

1. Enter the desired values (recurrence, start time, end time) and click **Save**.

   ![chlimage_1-92](assets/chlimage_1-92.png)

Autrement, si vous desirez effectuer le nettoyage manuellement vous pouvez :

1. Go to **Tools - Operations - Dashboard - Maintenance** or browse directly to `https://serveraddress:serverport/libs/granite/operations/content/maintenance.html`
1. Click the **Daily Maintenance Window**.
1. Hover over the **Revision Cleanup** icon.
1. Cliquez sur **Exécuter**.

   ![chlimage_1-93](assets/chlimage_1-93.png)

### Exécution du nettoyage des révisions en ligne après le nettoyage des révisions hors ligne {#running-online-revision-cleanup-after-offline-revision-cleanup}

Le processus de nettoyage des révisions récupère les anciennes révisions par génération. Cela signifie qu’une nouvelle génération est créée et conservée sur le disque chaque fois que vous exécutez le nettoyage des révisions. Il existe toutefois une différence entre les deux types de nettoyage des révisions : le nettoyage des révisions hors ligne conserve une génération tandis que le nettoyage des révisions en ligne conserve deux générations. So, when you run online revision cleanup **after** offline revision cleanup the following happens:

1. Une fois la première révision en ligne nettoyée, le référentiel sera de taille doublon. Cela est dû au fait que deux générations sont à présent conservées sur le disque.
1. Au cours des exécutions suivantes, le référentiel croît temporairement pendant la création de la nouvelle génération, puis se stabilise à nouveau à sa taille après la première exécution, à mesure que le processus de nettoyage de la révision en ligne récupère la génération précédente.

Gardez également à l’esprit qu’en fonction du type et du nombre de validations, la taille de chaque génération peut varier par rapport à la précédente. La taille finale peut donc varier d’une exécution à l’autre.

C’est pourquoi il est recommandé d’opter pour une taille de disque au moins deux à trois fois supérieure à celle estimée initialement pour le référentiel.

## Modes de compression complète et de compression des révisions les plus récentes  {#full-and-tail-compaction-modes}

**aem 6.5** introduit **deux nouveaux modes** pour la phase de **compaction** du processus de nettoyage de la révision en ligne :

* The **full compaction** mode rewrites all the segments and tar files in the whole repository. La phase de nettoyage suivante peut donc supprimer un maximum d’informations parasites du référentiel. Étant donné qu’une compression complète affecte l’ensemble du référentiel, cette opération nécessite une quantité considérable de ressources systèmes et demande beaucoup de temps. La compression complète correspond à la phase de compression dans AEM 6.3.
* The **tail compaction** mode rewrites only the most recent segments and tar files in the repository. Il s’agit des segments et fichiers tar qui ont été ajoutés depuis la dernière exécution d’une compression, de quelque type que ce soit. La phase de nettoyage suivante peut donc ne supprimer que les informations parasites contenues dans la partie récente du référentiel. Étant donné que ce mode de compression ne concerne qu’une partie du référentiel, il consomme beaucoup moins de ressources système qu’une compression complète et s’avère bien plus rapide.

Ces modes de compression constituent un compromis entre efficacité et consommation des ressources : bien que moins efficace, la compression des révisions les plus récentes a également un impact moindre sur le fonctionnement normal du système. La compression complète, en revanche, s’avère plus efficace, mais a davantage de répercussions sur le fonctionnement normal du système. 

AEM 6.5 s’enrichit également d’un mécanisme de déduplication du contenu plus efficace au cours de la compression, ce qui a pour effet de réduire l’empreinte du référentiel sur le disque.

Les deux graphiques ci-dessous présentent les résultats des tests réalisés en laboratoire interne. Ils illustrent la réduction des délais d’exécution moyens et de l’empreinte moyenne sur le disque dans AEM 6.5 par rapport à AEM 6.3 :

![onrc-duration-6_4vs63](assets/onrc-duration-6_4vs63.png) ![segmentstore-6_4vs63](assets/segmentstore-6_4vs63.png)

### Procédure de configuration des modes de compression complète et de compression des révisions les plus récentes {#how-to-configure-full-and-tail-compaction}

La configuration par défaut prévoit l’exécution d’une compression des révisions les plus récentes en semaine et d’une compression complète le dimanche. The default configuration can be changed by using the new configuration value `full.gc.days` of the `RevisionCleanupTask` [maintenance task](/help/sites-deploying/revision-cleanup.md#how-to-run-online-revision-cleanup).

When you configure the `full.gc.days` value be aware that full compaction will run during the day(s) defined in the value and tail compaction will run during the days that are not defined in the value. Par exemple, si vous configurez la compression complète pour qu’elle s’exécute le dimanche, la compression des révisions les plus récentes sera exécutée du lundi au samedi. Si vous planifiez l’exécution d’une compression complète pour tous les jours de la semaine, aucune compression des révisions les plus récentes ne sera effectuée.

Veuillez également tenir compte des points suivants :

* **La compaction** de la queue est moins efficace et a moins d&#39;impact sur les opérations normales du système. Elle est donc destinée à être exécutée pendant les jours ouvrables.
* **La compaction** complète est plus efficace mais a également un impact plus important sur les opérations normales du système. Il est donc conseillé de l’exécuter en dehors des jours ouvrables.
* L’exécution des deux modes de compression doit être planifiée en dehors des heures de pointe.

### Résolution des incidents {#troubleshooting}

Lorsque vous utilisez les nouveaux modes de compression, gardez à l’esprit les points suivants :

* Vous pouvez surveiller les activités d’entrée/sortie (E/S), par exemple : opérations d’E/S, processeur en attente des E/S, taille de la file d’attente de validation… Cela permet de déterminer si le système devient tributaire des entrées-sorties et doit faire l’objet d’une augmentation de capacité.
* The `RevisionCleanupTaskHealthCheck` indicates the overall health status of the Online Revision Cleanup. Elle fonctionne de la même manière que dans AEM 6.3 et ne fait pas la distinction entre les deux modes de compression.
* Les messages de journal contiennent des informations importantes concernant les modes de compression. Par exemple, au lancement du nettoyage des révisions en ligne, les messages de journal correspondants indiquent le mode de compression. De plus, dans certains cas limites d’exécution, le système revient au mode de compression complète alors que l’exécution d’une compression des révisions les plus récentes était programmée ; les messages de journal font alors état de cette modification. Les exemples de messages de journal ci-dessous indiquent le mode de compression et le changement de mode opéré :

```
TarMK GC: running tail compaction
TarMK GC: no base state available, running full compaction instead
```

### Limites connues {#known-limitations}

Dans certains cas, basculer entre les deux modes de compression a pour effet de retarder le processus de nettoyage. Plus exactement, la taille du référentiel augmente après une compression complète (elle est multipliée par deux). L’espace supplémentaire sera récupéré lors de l’opération de compression des révisions les plus récentes suivante, le référentiel retrouvant alors une taille inférieure à celle qu’il avait avant la compression complète. Il est également conseillé d’éviter les exécutions de tâches de maintenance en parallèle.

**Il est recommandé d’opter pour une taille de disque au moins deux à trois fois supérieure à celle estimée initialement pour le référentiel.**

## Foire aux questions sur le nettoyage des révisions en ligne {#online-revision-cleanup-frequently-asked-questions}

### Remarques concernant la mise à niveau AEM 6.5 {#aem-upgrade-considerations}

<table>
 <tbody>
  <tr>
   <td>Questions </td>
   <td>Réponses</td>
  </tr>
  <tr>
   <td>De quoi dois-je tenir compte lorsque j’effectue une mise à niveau vers AEM 6.5 ?</td>
   <td><p>Le format de persistance de TarMK change avec AEM 6.5. Ces modifications ne nécessitent aucune étape de migration proactive. Les référentiels existants font l’objet d’une migration progressive, un processus totalement transparent pour l’utilisateur. Le processus de migration est lancé la première fois qu’AEM 6.5 (ou les outils associés) accède(nt) au référentiel.</p> <p><strong>Une fois la migration vers le format de persistance AEM 6.5 initiée, le référentiel ne peut plus être rétabli au format de persistance AEM 6.3 précédent.</strong></p> </td>
  </tr>
 </tbody>
</table>

### Migration vers Oak Segment Tar {#migrating-to-oak-segment-tar}

<table>
 <tbody>
  <tr>
   <td><strong>Questions</strong></td>
   <td><strong>Réponses</strong></td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Pourquoi dois-je faire migrer le référentiel ?</strong></td>
   <td><p>Dans AEM 6.3, des changements au format de l'enregistrement étaient nécessaires, en particulier pour améliorer le rendement et l'efficacité du nettoyage de la révision en ligne. Ces modifications ne sont pas rétrocompatibles, et les référentiels créés avec l’ancien Oak Segment (AEM 6.2 et versions antérieures) doivent être migrés.</p> <p>Autres avantages liés au changement de format du stockage :</p>
    <ul>
     <li>Meilleure évolutivité (taille de segment optimisée).</li>
     <li><a href="/help/sites-administering/data-store-garbage-collection.md" target="_blank">Nettoyage plus rapide de la mémoire d’entrepôt de données</a>.<br /> </li>
     <li>Travail de base pour les prochaines améliorations.</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Le format Tar précédent est-il toujours pris en charge ?</strong></td>
   <td>Seul le nouveau format Oak Segment Tar est pris en charge dans AEM 6.3.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>La migration du contenu est-elle toujours obligatoire ?</strong></td>
   <td>Oui. À moins de commencer avec une nouvelle instance, vous aurez toujours à effectuer une migration du contenu.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Puis-je effectuer la mise à niveau vers la version 6.3 et effectuer la migration ultérieurement (par exemple, en utilisant une autre fenêtre de maintenance) ?</strong></td>
   <td>Non, comme nous l’avons expliqué ci-dessus, la migration du contenu est obligatoire.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Les temps d’interruption peuvent-ils être évités durant la migration ?</strong></td>
   <td>Non. C’est une opération unique qui ne peut pas être entreprise sur une instance en cours d’exécution.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Que se passe-t-il si j’exécute accidentellement le mauvais format de référentiel ?</strong></td>
   <td>If you try to run the oak-segment module against an oak-segment-tar repository (or vice versa), startup will fail with an <em>IllegalStateException</em> with the message "Invalid segment format". Il n’y aura aucune corruption de données.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Une réindexation des index de recherche est-elle nécessaire ?</strong></td>
   <td>Non. La migration du segment de chêne vers le segment de chêne-goudron introduit des modifications dans le format de conteneur. Les données contenues ne sont pas affectées et ne sont pas modifiées.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Comment calculer au mieux l’espace disque attendu pendant et après la migration ?</strong></td>
   <td>La migration équivaut à recréer l’entrepôt de segments dans un nouveau format. Cela peut être utilisé pour calculer l’espace disque supplémentaire nécessaire durant la migration. Après la migration, l’ancien entrepôt de segments peut être supprimé pour récupérer de l’espace.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Comment estimer au mieux la durée de la migration ?</strong></td>
   <td>Migration performance can be greatly improved if <a href="/help/sites-deploying/revision-cleanup.md#how-to-run-offline-revision-cleanup">offline revision cleanup</a> is executed prior to the migration. Nous conseillons à tous les clients de l’exécuter en tant que conditions préalables à la mise à niveau. En général, la durée de la migration doit être similaire à la durée de la tâche de nettoyage de la révision hors ligne, en supposant que la tâche de nettoyage de la révision hors ligne a été exécutée avant la migration.</td>
   <td> </td>
  </tr>
 </tbody>
</table>

### Exécution du nettoyage des révisions en ligne {#running-online-revision-cleanup}

<table>
 <tbody>
  <tr>
   <td><strong>Questions</strong></td>
   <td><strong>Réponses</strong></td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>À quelle fréquence le nettoyage des révisions en ligne doit-il être exécuté ?</strong></td>
   <td>Une fois par jour. C’est la configuration par défaut dans le tableau des opérations.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Comment puis-je configurer l’heure de début de la tâche de maintenance du nettoyage des révisions en ligne ?</strong></td>
   <td>See the <a href="/help/sites-deploying/revision-cleanup.md#how-to-run-online-revision-cleanup">How to run Online Revision Cleanup</a> section. </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Existe-t-il une fréquence maximale ne devant pas être dépassée pour le nettoyage des révisions en ligne ?</strong></td>
   <td>Il est recommandé d’exécuter le nettoyage des révisions en ligne une fois par jour, tel que configuré par défaut.<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Quels sont les indicateurs clés permettant de déterminer à quelle fréquence le nettoyage des révisions en ligne doit être effectué ?</strong></td>
   <td>Il n’est pas nécessaire de déterminer la fréquence, étant donné que le nettoyage des révisions en ligne est configuré en tant que tâche de maintenance et s’exécute automatiquement de façon quotidienne.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Pourquoi le nettoyage des révisions en ligne ne récupère-t-il pas de l’espace lorsqu’il est exécuté pour la première fois ?</strong></td>
   <td>Le nettoyage des révisions en ligne récupère les anciennes révisions par génération. Une nouvelle génération est générée à chaque fois que le nettoyage des révisions est exécuté. Seul le contenu vieux d’au moins deux générations sera récupéré, ce qui signifie que lors d’une première exécution, rien n’est récupéré.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Pourquoi le premier nettoyage des révisions en ligne ne permet-il pas de récupérer de l’espace lorsqu’il est exécuté après le nettoyage des révisions hors ligne ?</strong></td>
   <td><p>Alors que le nettoyage des révisions en ligne récupère les deux dernières générations, le processus hors ligne ne récupère que la dernière génération. Dans le cas d’un tout nouveau référentiel, le nettoyage en ligne ne récupère aucun espace lorsqu’il est exécuté pour la première fois après le nettoyage hors ligne, car il n’y a aucune génération suffisamment ancienne pour être récupérée.</p> <p>Lisez également la section « Exécution du nettoyage des révisions en ligne après le nettoyage des révisions hors ligne » de <a href="/help/sites-deploying/revision-cleanup.md#how-to-run-online-revision-cleanup">ce chapitre</a>.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>L’auteur et la publication ont-ils des fenêtres de nettoyage des révisions en ligne différentes ?</strong></td>
   <td>Cela dépend des heures de travail et des modèles de trafic de la présence en ligne du client. Les fenêtres de maintenance doivent être configurées en dehors des heures de production principales pour assurer la meilleure efficacité de nettoyage. S’il existe plusieurs instances de publication AEM (ferme TarMK), les fenêtres de maintenance pour le nettoyage des révisions en ligne doivent être fragmentées.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Existe-t-il des conditions préalables pour exécuter le nettoyage des révisions en ligne ?</strong></td>
   <td><p>Le nettoyage de la révision en ligne est disponible uniquement avec AEM versions 6.3 et ultérieures. Aussi, si vous utilisez une ancienne version d’AEM, vous devrez effectuer une migration vers le nouvel <a href="/help/sites-deploying/revision-cleanup.md#migrating-to-oak-segment-tar">Oak Segment Tar</a>.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Quels sont les facteurs qui déterminent la durée du nettoyage des révisions en ligne ?</strong></td>
   <td>Les facteurs sont les suivants :<br />
    <ul>
     <li>Taille du référentiel</li>
     <li>Charge sur le système (demandes par minute, surtout les opérations d’écriture)</li>
     <li>Modèle d’activité (lectures et écritures)</li>
     <li>Spécifications matérielles (performances du processeur, mémoire, IOPS)</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Les auteurs peuvent-ils travailler pendant l’exécution du nettoyage des révisions en ligne ?</strong></td>
   <td>Oui, le nettoyage des révisions en ligne gère les écritures simultanées. Toutefois, le nettoyage des révisions en ligne fonctionne plus rapidement et plus efficacement sans transactions d’écriture simultanées. Il est recommandé de planifier la tâche de maintenance de nettoyage en ligne durant une période relativement calme sans beaucoup de trafic.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Quelles sont les conditions minimales requises en matière d’espace disque et de mémoire de tas lors de l’exécution du nettoyage des révisions en ligne ?</strong></td>
   <td><p>L’espace disque est surveillé en permanence lors du nettoyage des révisions en ligne. Si l’espace disque passe en dessous d’une certaine valeur, le processus est annulé. La valeur critique par défaut est de 25 % de l’encombrement sur le disque du référentiel, et elle n’est pas configurable.</p> <p><strong>Il est recommandé d’opter pour une taille de disque au moins deux à trois fois supérieure à celle estimée initialement pour le référentiel.</strong></p> <p>L’espace de tas libre est surveillé en permanence lors du processus de nettoyage. Si l’espace de tas disponible passe en dessous d’une certaine valeur, le processus est annulé. La valeur critique est configurée via org.apache.jackrabbit.oak.segment.SegmentNodeStoreService#MEMORY_THRESHOLD. La valeur par défaut est 15%.</p> <p>Les recommandations sur le dimensionnement du tas de compression minimal ne sont pas séparées des recommandations sur le dimensionnement de la mémoire AEM. En règle générale : <strong>si une instance AEM est suffisamment bien dimensionnée pour gérer les cas d’utilisation et la charge utile attendue, le processus de nettoyage obtiendra suffisamment de mémoire.</strong></p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Quel est l’impact attendu sur les performances pendant l’exécution du nettoyage des révisions en ligne ?</strong></td>
   <td>Le nettoyage des révisions en ligne est un processus en arrière-plan qui lit et écrit sur le référentiel en même temps que les opérations normales du système. En particulier, il est peut-être nécessaire d’acquérir un accès exclusif au référentiel pendant une courte période, ce qui empêche toute autre thread d’écrire dans le référentiel.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Quelle est la durée estimée d’exécution du nettoyage des révisions en ligne ?</strong></td>
   <td>Cela ne devrait pas prendre plus de 2 heures d’après les derniers tests de performance que nous avons réalisés en interne.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Que faire si le nettoyage des révisions en ligne dure plus longtemps ?</strong></td>
   <td>
    <ul>
     <li>Assurez-vous qu’il est exécuté tous les jours.<br /> </li>
     <li>Assurez-vous qu’il est exécuté pendant les activités minimales du référentiel en configurant les fenêtres de maintenance dans le Tableau de bord des opérations en conséquence.</li>
     <li>Faites évoluer les ressources du système (processeur, mémoire, E/S).</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Que se passe-t-il si le nettoyage des révisions en ligne dépasse la fenêtre de maintenance configurée ?</strong></td>
   <td>Assurez-vous que d’autres tâches de maintenance ne retardent pas son exécution. Cela peut être le cas s’il y a plus de tâches de maintenance que de nettoyage des révisions en ligne exécutées dans la même fenêtre de maintenance. Notez que les tâches de maintenance suivantes sont exécutées consécutivement, sans ordre configurable.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Pourquoi le nettoyage de la mémoire est-il ignoré ?</strong></td>
   <td><p>Le nettoyage des révisions requiert une phase d’estimation pour décider s’il y a suffisamment de contenu inutilisé à nettoyer. L’estimateur compare la taille actuelle à la taille du référentiel après la dernière compression. Si la taille dépasse le delta configuré, le nettoyage sera effectué. Le delta de taille est défini à 1 Go. Cela signifie que si la taille du référentiel n'a pas augmenté de 1 Go depuis la dernière exécution de nettoyage, la nouvelle itération de nettoyage de révision sera ignorée. </p> <p>Vous trouverez, ci-dessous, des entrées de journaux pertinentes pour la phase d’estimation :</p>
    <ul>
     <li>Revision GC will run: <em>Size delta is N% or N/N (N/N bytes), so running compaction</em></li>
     <li>Revision GC will <strong>not</strong> run: <em>Size delta is N% or N/N (N/N bytes), so skipping compaction for now</em></li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Est-il possible d’annuler en toute sécurité la compression automatique si l’impact sur les performances est trop élevé ?</strong></td>
   <td>Oui. Depuis AEM 6.3, il peut également être arrêté par l’intermédiaire de la fenêtre des tâches de maintenance du tableau de bord des opérations ou via JMX.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Si l’instance AEM est arrêtée pendant une tâche de nettoyage programmée, le processus s’arrête-t-il de manière sécurisée ou l’arrêt est-il bloqué jusqu’à la réalisation complète de la compression ?</strong></td>
   <td>Le nettoyage des révisions est interrompu et le référentiel va s’arrêter en toute sécurité.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Que se passe-t-il si le système tombe en panne pendant le nettoyage des révisions en ligne ?</strong></td>
   <td>Il n’existe aucun risque de corruption des données dans ce cas. Le reste des résidus sera nettoyé lors de la prochaine exécution.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Qu’arrive-t-il lorsque vous n’effectuez pas le nettoyage des révisions en ligne ?</strong></td>
   <td>Le niveau de performances se dégrade au fil du temps.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Quelles révisions sont collectées ?</strong></td>
   <td>Par défaut, le nettoyage des révisions en ligne collecte uniquement les révisions datant d’au moins 24 heures.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Que se passe-t-il en cas d'interférence excessive des écritures simultanées dans le référentiel ?</strong></td>
   <td><p>S’il y a des écritures simultanées sur le système, le nettoyage des révisions en ligne peut nécessiter un accès exclusif à l’écriture pour pouvoir effectuer les changements à la fin d’un cycle de compression. The system will go into <strong>forceCompact mode</strong>, as explained in more detail in the <a href="https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html" target="_blank">oak documentation</a>. Pendant la compression forcée, un dispositif exclusif de verrouillage de l’écriture est acquis pour effectuer les modifications sans aucune écriture simultanée perturbatrice. Pour limiter l’impact sur les délais de réponse, une valeur de délai d’expiration peut être définie. Cette valeur est définie sur 1 minute par défaut, ce qui signifie que si la compression en force ne se termine pas dans un délai d’une minute, le processus de compression sera interrompu au profit d’autres commits simultanés.</p> <p>La durée du pacte de force dépend des facteurs suivants :</p>
    <ul>
     <li>matériel : spécifiquement IOPS. La durée décroît lorsqu’il y a plus d’IOPS.</li>
     <li>taille de l’entrepôt de segments : la durée augmente en fonction de la taille de l’entrepôt de segments.</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><p><strong>Comment le nettoyage des révisions en ligne est-il exécuté sur une instance de secours ?</strong></p> </td>
   <td><p>Dans une configuration Cold Standby, seule l’instance principale doit être configurée pour exécuter le nettoyage des révisions en ligne. Sur l’instance de secours, le nettoyage des révisions en ligne n’a pas besoin d’être programmé de manière spécifique.</p> <p>L'opération correspondante sur une instance Secondaire est le nettoyage automatique, ce qui correspond à la phase de nettoyage de la révision en ligne. Le nettoyage automatique est exécuté sur l’instance de secours après l’exécution du nettoyage des révisions en ligne sur l’instance principale. </p> <p>Les phase de compression et d’estimation ne sont pas exécutées sur l’instance de secours.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Le nettoyage des révisions hors ligne peut-il libérer plus d’espace disque que le nettoyage des révisions en ligne ?</strong></td>
   <td><p>Le nettoyage des révisions hors ligne peut supprimer instantanément les anciennes révisions, alors que le nettoyage des révisions en ligne doit tenir compte des anciennes révisions qui sont toujours référencées par la pile de l’application. Le premier peut donc supprimer les résidus de manière plus agressive que le second, où l’effet est amortit au bout de quelques cycles de nettoyage de la mémoire.</p> <p>Lisez également la section « Exécution du nettoyage des révisions en ligne après le nettoyage des révisions hors ligne » de <a href="/help/sites-deploying/revision-cleanup.md#how-to-run-online-revision-cleanup">ce chapitre</a>.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Observations relatives aux opérations de fichiers mappés par la mémoire</td>
   <td>
    <ul>
     <li><strong>Sur les environnements</strong>Windows, l’accès régulier aux fichiers est toujours appliqué, de sorte que l’accès mappé à la mémoire n’est pas utilisé. En règle générale, toute la RAM disponible doit être allouée au tas et la taille de segmentCache doit être augmentée. Vous augmentez le segmentCache en ajoutant l’option segmentCache.size à org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config (par exemple, segmentCache.size=20480). N’oubliez pas de laisser de la mémoire vive pour le système d’exploitation et d’autres processus.</li>
     <li><strong>Dans les environnements non Windows</strong>, augmentez la taille de la mémoire physique pour améliorer le mappage de mémoire du référentiel.</li>
    </ul> </td>
   <td>
    <ul>
     <li> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### Surveillance du nettoyage des révisions en ligne {#monitoring-online-revision-cleanup}

<table>
 <tbody>
  <tr>
   <td><strong>Que doit-on surveiller pendant le nettoyage de la révision en ligne ?</strong></td>
   <td>
    <ul>
     <li>L'espace disque doit être surveillé lorsque le nettoyage de révision en ligne est activé. S’il n’y a pas sufisamment d’espace disque, soit le processus de nettoyage ne sera pas lancé, ou il sera arrêté de manière préventive. </li>
     <li>Vérifiez les journaux pendant la durée d’exécution du nettoyage des révisions en ligne. Cela ne devrait pas durer plus de 2 heures. </li>
     <li>Nombre de points de contrôle. S’il existe plus de 3 points de contôle durant l’exécution de la compression, il est recommandé de nettoyer les points de contôle.</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Comment vérifier si le nettoyage de la révision en ligne a réussi ?</strong></td>
   <td><p>Vous pouvez vérifier si le nettoyage de la révision en ligne s'est terminé correctement en vérifiant les journaux.</p> <p>Par exemple, "<code>TarMK GC #{}: compaction completed in {} ({} ms), after {} cycles</code>" désigne l’étape de compactage terminée avec succès, sauf si elle est précédée du message "<code>TarMK GC #{}: compaction gave up compacting concurrent commits after {} cycles</code>", ce qui signifie qu’il y a eu trop de charges simultanées.</p> <p>En conséquence, il existe un message "<code>TarMK GC #{}: cleanup completed in {} ({} ms</code>" pour que l’étape de nettoyage soit terminée avec succès.</p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><strong>Où trouver les statistiques des dernières exécutions de nettoyage de révision en ligne ?</strong></td>
   <td><p>Le statut, les progrès et les statistiques sont exposés via JMX (<code>SegmentRevisionGarbageCollection</code> MBean). Pour plus de détails sur le <code>SegmentRevisionGarbageCollection</code> MBean, lisez le paragraphe <a href="https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html#monitoring-via-jmx" target="_blank"></a>suivant.</p> <p>L’avancement peut être suivi via l’ <code>EstimatedRevisionGCCompletion</code> attribut de la variable <code>SegmentRevisionGarbageCollection MBean.</code></p> <p>Vous pouvez obtenir une référence du MBean à l’aide du <code>ObjectName org.apache.jackrabbit.oak:name="Segment node store revision garbage collection",type="SegmentRevisionGarbageCollection”</code>.</p> <p>N’oubliez pas que les statistiques sont dospnibles uniquement avec le dernier démarrage de système. L’outil de surveillance externe peut être utilisé pour conserver les données au-delà de la disponibilité d’AEM. See <a href="/help/sites-administering/operations-dashboard.md#monitoring-with-nagios" target="_blank">the AEM documentation for attaching health checks to Nagios as an example for an external monitoring tool</a>.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Quelles sont les entrées de journal pertinentes ?</strong></td>
   <td>
    <ul>
     <li>Le nettoyage de la révision en ligne a démarré / arrêté
      <ul>
       <li>Le nettoyage de la révision en ligne se compose de trois phases : estimation, compaction et nettoyage. La phase d’estimation peut forcer l’omission des phases de compression et de nettoyager si le référentiel ne contient pas suffisament de résidus. Dans la dernière version de l'AEM, le message "<code>TarMK GC #{}: estimation started</code>" marque le début de l'estimation, "<code>TarMK GC #{}: compaction started, strategy={}</code>" marque le début de compaction et "T<code>arMK GC #{}: cleanup started. Current repository size is {} ({} bytes</code>" le début du nettoyage.</li>
      </ul> </li>
     <li>Espace disque gagné par le nettoyage de la révision
      <ul>
       <li>L'espace n'est récupéré que lorsque la phase de nettoyage est terminée. La fin de la phase de nettoyage est marquée par le message "T<code>arMK GC #{}: cleanup completed in {} ({} ms</code>". La dimension après nettoyage est {} ({} octets) et l’espace récupéré{} ({} octets). Le poids/la profondeur de la carte de compression est {}/{} ({} octets/{}).”.</li>
      </ul> </li>
     <li>Un problème s'est produit lors du nettoyage de la révision
      <ul>
       <li>Il y a de nombreuses conditions d'échec, toutes sont marquées par des messages de journal WARN ou ERROR commençant par "TarMK GC".</li>
      </ul> </li>
    </ul> <p>Consultez également la section <a href="/help/sites-deploying/revision-cleanup.md#troubleshooting-based-on-error-messages">Résolution des problèmes en fonction des messages</a> d’erreur ci-dessous.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Comment vérifier combien d'espace a été récupéré après le nettoyage de la révision en ligne ?</strong></td>
   <td>Un message se trouve dans le journal à la fin du cycle de nettoyage : "<code>TarMK GC #3: cleanup completed</code>" qui comprend la taille du référentiel et la quantité de déchets récupérés.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Comment vérifier l'intégrité du référentiel une fois le nettoyage de la révision en ligne terminé ?</strong></td>
   <td><p>Une vérification de l'intégrité du référentiel n'est pas nécessaire après le nettoyage de la révision en ligne. </p> <p>Cependant, vous pouvez effectuer les actions suivantes pour vérifier l’état du référentiel après le nettoyage :</p>
    <ul>
     <li>Vérification de la <a href="/help/sites-deploying/consistency-check.md" target="_blank">traversée du référentiel</a></li>
     <li>Utilisez l'outil d'exécution de chêne une fois le processus de nettoyage terminé pour vérifier les incohérences. Pour plus d'informations sur la façon de procéder, consultez la Documentation <a href="https://github.com/apache/jackrabbit-oak/blob/trunk/oak-doc/src/site/markdown/nodestore/segment/overview.md#check" target="_blank">Apache.</a> Vous n'avez pas besoin de fermer AEM pour exécuter l'outil.</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Comment détecter si le nettoyage de la révision en ligne a échoué et quelles sont les étapes à restaurer ?</strong></td>
   <td>Les conditions d'échec sont marquées par les messages du journal WARN ou ERROR commençant par "TarMK GC". Consultez également la section <a href="/help/sites-deploying/revision-cleanup.md#troubleshooting-based-on-error-messages">Résolution des problèmes en fonction des messages</a> d’erreur ci-dessous.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Quelles sont les informations exposées dans le bilan d'intégrité du nettoyage de révision ? Comment et quand contribue-t-elle aux niveaux d’état codés par des couleurs ?  </strong></td>
   <td><p>Le bilan de santé du nettoyage de la révision fait partie du Tableau de bord <a href="/help/sites-administering/operations-dashboard.md#health-reports" target="_blank">d'</a>exploitation.<br /> </p> <p>The status will be <strong>GREEN</strong> if the last execution of the Online Revision Cleanup maintenance task has completed succesfully.</p> <p>Il sera <strong>JAUNE</strong> si la tâche de maintenance de nettoyage de révision en ligne a été annulée une fois.<br /> </p> <p>It will be <strong>RED</strong> if the Online Revision Cleanup maintenance task was cancelled three times in a row. <strong>Dans ce cas, une interaction manuelle est nécessaire</strong> ou le nettoyage de la révision en ligne est susceptible d'échouer à nouveau. Pour plus d'informations, consultez la section <a href="/help/sites-deploying/revision-cleanup.md#troubleshooting-online-revision-cleanup">Résolution des problèmes</a> ci-dessous.<br /> </p> <p>Veuillez aussi noter que l’état de la vérification de l’intégrité sera réinitialisé après le redémarrage du système. Par conséquent, une instance fraîchement redémarrée affiche un état vert sur la vérification d’intégrité du nettoyage des révisions. L’outil de surveillance externe peut être utilisé pour conserver les données au-delà de la disponibilité d’AEM. See <a href="/help/sites-administering/operations-dashboard.md#monitoring-with-nagios">the AEM documentation for attaching health checks to Nagios as an example for an external monitoring tool</a>.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><p><strong>Comment surveiller le nettoyage automatique sur une instance Secondaire ?</strong></p> </td>
   <td><p>Le statut, les progrès et les statistiques sont exposés via JMX en utilisant le <code>SegmentRevisionGarbageCollection</code> MBean. Consultez également la documentation <a href="https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html#monitoring-via-jmx" target="_blank">sur les chênes</a>ci-dessous. </p> <p>Vous pouvez obtenir une référence du MBean en utilisant le <code>ObjectName org.apache.jackrabbit.oak:name="Segment node store revision garbage collection",type="SegmentRevisionGarbageCollection”</code>.</p> <p>Notez que les statistiques sont disponibles uniquement à partir du dernier démarrage du système. L’outil de surveillance externe peut être utilisé pour conserver les données au-delà de la disponibilité d’AEM. Voir également <a href="/help/sites-administering/operations-dashboard.md#monitoring-with-nagios" target="_blank">la documentation AEM pour l'attachement des contrôles d'intégrité à Nagios comme exemple d'outil</a>de surveillance externe.</p> <p>Les fichiers de journal peuvent aussi être utilisés pour vérifier l’état, le progrès et les statistiques du nettoyage automatique.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><p><strong>Que doit-on surveiller pendant le nettoyage automatique sur une instance Secondaire ?</strong></p> </td>
   <td>
    <ul>
     <li>L'espace disque doit être surveillé lors de l'exécution du nettoyage automatique.</li>
     <li>Le délai d’exécution (via les journaux) pour vous assurer que 2 heures ne sont pas dépassées.</li>
     <li>Taille de la banque de segments après l’exécution du nettoyage automatique. La taille de l’entrepôt de segments sur l’instance de secours doit être à peu près le même que celle de l’instance principale.</li>
    </ul> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

### Dépannage du nettoyage des révisions en ligne {#troubleshooting-online-revision-cleanup}

<table>
 <tbody>
  <tr>
   <td><strong>Quel est le pire qui puisse arriver si vous n’exécutez pas le nettoyage des révisions en ligne ?</strong></td>
   <td>L’instance AEM ne disposera plus d’espace disque, ce qui causera des pannes de production.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Un trafic élevé d’utilisateurs risque-t-il de causer des problémes d’exécution du nettoyage des révisions en ligne sur une instance de publication ?</strong></td>
   <td>Le trafic élevé d’utilisateurs peut impacter la réussite de l’exécution de la phase de compression.<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>D’après la vérification d’intégrité et les entrées du journal, le processus de nettoyage des révisions en ligne a échoué trois fois de suite. Que doit-on faire pour assurer le succès du nettoyage des révisions en ligne ?</strong></td>
   <td>Vous pouvez prendre plusieurs mesures pour trouver et résoudre le problème:<br />
    <ul>
     <li>Tout d’abord, vérifiez les entrées du journal.<br /> </li>
     <li>En fonction des informations contenues dans les journaux, prenez une mesure appropriée :
      <ul>
       <li>If the logs show five missed compact cycles and a timeout on the <code>forceCompact</code> cycle, schedule the maintenance window to a quiet time when the amount of repository writes is low. You can check repository writes in the repositoy metrics monitoring tool located at <em>https://serveraddress:serverport/libs/granite/operations/content/monitoring/page.html</em></li>
       <li>Si le nettoyage est arrêté à la fin de la fenêtre de maintenance, assurez-vous que la configuration de la fenêtre de maintenance dans l’interface utilisateur des tâches de maintenance est suffisamment volumineuse. </li>
       <li>Si la mémoire disponible est insuffisante, assurez-vous que l’instance contienne suffisament de mémoire.</li>
       <li>En cas de délai de réponse, l’entrepôt de segments peut augmenter de façon excessive au point où il devient impossible d’effectuer un nettoyage des révisions en ligne, même avec une fenêtre de maintenance plus longue. Par exemple, si aucun nettoyage des révisions en ligne n’a réussi au cours de la dernière semaine, il est recommandé de planifier une maintenance hors ligne et d’effectuer le nettoyage des révisions hors ligne en vue de convertir la taille de l’entrepôt de segments à une dimension plus gérable.</li>
      </ul> </li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Que doit-on faire une fois l’alerte de vérification d’intégrité activée ?</strong></td>
   <td>Voir le point précédent.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Que se passe-t-il lorsque le nettoyage des révisions en ligne est à court de temps pendant la fenêtre maintenance planifiée ?</strong></td>
   <td>Le nettoyage des révisions en ligne sera annulé et le restant sera supprimé. Il recommencera la prochaine fois que la fenêtre de maintenance est planifiée.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>What is causing <code>SegmentNotFoundException</code> instances to be logged in the <code>error.log</code> and how can I recover?</strong></td>
   <td><p>A <code>SegmentNotFoundException</code> is logged by the TarMK when it tries to access a storage unit (a segment) that it can not find. Il existe trois scénarios pouvant causer ce problème :</p>
    <ol>
     <li>Une application qui contourne les systèmes d’accès recommandés (comme Sling et l’API JCR) et utilise un niveau API/SPI plus bas pour accéder au référentiel, puis dépasse la période de validité d’un segment. En d’autres termes, il conserve une référence à une entité plus longue que la durée de rétention octroyée par le nettoyage des révisions en ligne (24 heures par défaut). Ce cas est transitoire et ne conduit pas à la corruption des données. Pour récupérer, l'outil d'exécution de chêne doit être utilisé pour confirmer la nature transitoire de l'exception (la vérification d'exécution de chêne ne doit pas signaler d'erreurs). Pour ce faire, l’instance doit être mise hors ligne et redémarrée ensuite.</li>
     <li>Un événement externe a causé la corruption des données sur le disque. Il peut s’agir d’une panne du disque, d’un espace disque saturé ou d’une modification accidentelle des fichiers de données requis. Dans ce cas, une instance doit être déconnectée et réparée avec la vérification exécutée par Oak. For more details on how to perform the oak-run check, read the following <a href="https://github.com/apache/jackrabbit-oak/blob/trunk/oak-doc/src/site/markdown/nodestore/segment/overview.md#check" target="_blank">Apache documentation</a>.</li>
     <li>All other occurrences should addressed through the <a href="https://helpx.adobe.com/fr/marketing-cloud/contact-support.html" target="_blank">Adobe Customer Care</a>.</li>
    </ol> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

### Dépannage basé sur les messages d’erreur {#troubleshooting-based-on-error-messages}

Le fichier error.log sera détaillé en cas d&#39;incident au cours du processus de nettoyage des révisions en ligne. La matrice suivante vise à expliquer les messages les plus courants et à fournir des solutions possibles :

| **Phase** | **Messages du journal** | **Explication** | **Étapes suivantes** |
|---|---|---|---|
|  |  |  |  |
| Estimation | TarMK GC #2 : estimation ignorée car la compaction est suspendue | La phase d&#39;estimation est ignorée lorsque la compaction est désactivée sur le système par configuration. | Activation du nettoyage des révisions en ligne. |
|  | TarMK GC #2 : estimation interrompue : ${REASON}. Skipping compaction. | La phase d&#39;estimation s&#39;est terminée prématurément. Quelques exemples d’événements qui peuvent interrompre la phase d’estimation : pas suffisamment de mémoire ou d’espace disque sur le système hôte. | Dépend de la raison donnée. |
| Compaction | TarMK GC #2 : compaction suspendue | Tant que la phase de compaction est interrompue par la configuration, ni la phase d&#39;estimation ni la phase de compaction ne seront exécutées. | Activez le nettoyage des révisions en ligne. |
|  | TarMK GC #2 : compaction annulée : ${REASON}. | La phase de compaction s&#39;est terminée prématurément. Quelques exemples d’événements qui peuvent interrompre la phase de compression : pas suffisamment de mémoire ou d’espace disque sur le système hôte. De plus, la compression peut être annulée en désactivant le système ou en l’annulant de façon explicite par le biais des interfaces d’administration telles que la fenêtre de maintenance dans le tableau des opérations. | Dépend de la raison donnée. |
|  | TarMK GC #2 : échec de compaction en 32,902 min (1974140 ms), après 5 cycles | Ce message ne signifie pas qu’il y a eu une erreur irrécupérable, mais seulement que la compaction a été arrêtée après un certain nombre de tentatives. Lisez également le paragraphe [](https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html#how-does-compaction-works-with-concurrent-writes)suivant. | Lisez la documentation [](https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html#how-does-compaction-works-with-concurrent-writes)Oak suivante et la dernière question de la section Nettoyage [de la révision en ligne](/help/sites-deploying/revision-cleanup.md#running-online-revision-cleanup) en cours. |
| Nettoyage | TarMK GC #2 : nettoyage interrompu | Le nettoyage a été annulé en arrêtant le référentiel. Aucun impact sur la cohérence n’est attendu. En outre, l’espace disque ne sera probablement pas pleinement récupéré. Il sera récupéré lors du prochain cycle de nettoyage des révisions.  | Découvrir pourquoi le référentiel a été arrêté et essayer d’éviter de le désactiver pendant les fenêtres de maintenance. |

## Exécution du nettoyage des révisions hors ligne {#how-to-run-offline-revision-cleanup}

>[!CAUTION]
>
>Les différentes versions de l’outil exécuté par Oak doivent être utilisées en fonction de la version d’Oak que vous utilisez avec votre installation AEM. Vérifiez les exigences de version énumérés ci-dessous avant d’utiliser l’outil :
>
>* For Oak versions **1.0.0 through 1.0.11** or **1.1.0 through 1.1.6**, use Oak-run version** 1.0.11**
   >
   >
* Pour des versions d’Oak **plus récentes que celle ci-dessus**, utilisez la version d’Oak-run qui correspond au système Oak de votre installation AEM. 

>



Adobe provides a tool called **Oak-run** for performing revision cleanup. Il peut être téléchargé à l’emplacement suivant :

[https://repo1.maven.org/maven2/org/apache/jackrabbit/oak-run/](https://repo1.maven.org/maven2/org/apache/jackrabbit/oak-run/)

L’outil est un jar exécutable qui peut être exécuté manuellement pour compresser le référentiel. Le processus est appelé nettoyage des révisions hors ligne, car le référentiel doit être desactivé pour pouvoir exécuter correctement l’outil. Veillez à planifier le nettoyage en fonction de la période de maintenance. 

For tips on how to increase the performance of the cleanup process, see [Increasing the Performance of Offline Revision Cleanup](/help/sites-deploying/revision-cleanup.md#increasing-the-performance-of-offline-revision-cleanup).

>[!NOTE]
>
>Vous pouvez également effacer les anciens points de contrôle avant que la maintenance ait lieu (étapes 2 et 3 de la procédure ci-dessous). Cette méthode s’adresse uniquement aux instances comportant plus de 100 points de contrôle. 

1. Vérifiez systématiquement que vous disposez d’une sauvegarde récente de l’instance AEM.

   Arrêtez AEM.

1. (Facultatif) Utilisez l’outil pour trouver des anciens points de contrôle :

   ```xml
   java -jar oak-run.jar checkpoints install-folder/crx-quickstart/repository/segmentstore
   ```

1. (Facultatif) Ensuite, supprimez les points de contrôle non-référencés :

   ```xml
   java -jar oak-run.jar checkpoints install-folder/crx-quickstart/repository/segmentstore rm-unreferenced
   ```

1. Exécutez la compression et attendez qu’elle soit terminée :

   ```xml
   java -jar -Dsun.arch.data.model=32 oak-run.jar compact install-folder/crx-quickstart/repository/segmentstore
   ```

### Amélioration de la performance du nettoyage des révisions hors ligne {#increasing-the-performance-of-offline-revision-cleanup}

L’outil oak-run présente plusieurs fonctionnalités ayant pour but d’améliorer les performances du processus de nettoyage des révisions et de réduire la fenêtre de maintenance autant que possible.

La liste comprend plusieurs paramètres de ligne de commande, comme décrit ci-dessous :

* **-mmap.** Vous pouvez définir cette variable sur true ou false. S’il est défini sur true, l’accès mappé par la mémoire est utilisé. S’il est défini sur false, l’accès aux fichiers est utilisé. S’il n’est pas spécifié, l’accès mappé par la mémoire est utilisé sur les systèmes 64 bits et l’accès aux fichiers est utilisé sur les systèmes 32 bits. Sous Windows, l’accès standard aux fichiers est toujours appliqué et cette option est ignorée. **Ce paramètre a remplacé le paramètre -Dtar.memoryMapped.**

* **-Dupdate.limit**. Définit le seuil de vidage d’une transaction temporaire sur le disque. La valeur par défaut est 10000.   

* **-Dcompress-interval**. Nombre de saisies du plan de compression à conserver jusqu’à la compression du plan actuel. La valeur par défaut est de 1000000. Vous devez augmenter cette valeur à un nombre plus élevé pour un débit plus rapide, si vous disposez de suffisamment de mémoire. **Ce paramètre a été supprimé dans Oak version 1.6 et est sans effet.**

* **-Dcompaction-progress-log**. Le nombre de nœuds compressés qui seront inscrits dans le journal. La valeur par défaut est 150000, ce qui signifie que les 150000 premiers noeuds compactés seront enregistrés pendant l’opération. Utilisez ce paramètre conjointement avec le paramètre suivant répertoriées ci-dessous.

* **-Dtar.PersistCompactionMap.** Définissez ce paramètre sur true pour utiliser l’espace disque au lieu de la mémoire de tas pour la persistance de la carte de compaction. Requires the oak-run tool **versions 1.4** and higher. Pour plus de détails, reportez-vous à la question 3 dans la section [FAQ sur le nettoyage des révisions hors ligne. ](/help/sites-deploying/revision-cleanup.md#offline-revision-cleanup-frequently-asked-questions) **Ce paramètre a été supprimé dans Oak version 1.6 et est sans effet.**

* **--force.** Force la compression et ignore une version d’entrepôt de segments sans correspondance.

>[!CAUTION]
>
>Using the `--force` parameter will upgrade the segment store to the latest version, which is incompatible with older Oak versions. Veuillez également tenir compte du fait qu’il est impossible de revenir à la version antérieure. En règle générale, l’utilisation de ces paramètres doit être réservée aux utilisateurs qui disposent des connaissances appropriées.

Un exemple de paramètre utilisé :

```xml
java -Dupdate.limit=10000 -Dcompaction-progress-log=150000 -Dlogback.configurationFile=logback.xml -Xmx8g -jar oak-run-*.jar checkpoints <repository>
```

### Autres méthodes pour déclencher le nettoyage des révisions {#additional-methods-of-triggering-revision-cleanup}

Outre celles présentées ci-dessus, vous pouvez également déclencher le mécanisme de nettoyage des révisions à l’aide de la console JMX, comme suit :

1. Open the JMX Console by going to [http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx)
1. Click the **RevisionGarbageCollection** MBean.
1. In the next window, click **startRevisionGC()** and then **Invoke** to start the Revision Garbage Collection job.

### FAQ sur le nettoyage des révisions hors ligne {#offline-revision-cleanup-frequently-asked-questions}

<table>
 <tbody>
  <tr>
   <td><strong>Quels sont les facteurs qui déterminent la durée du nettoyage des révisions hors ligne ?</strong></td>
   <td><p>La taille du référentiel et la quantité de révisions devant être nettoyées déterminent la durée du nettoyage.</p> </td>
  </tr>
  <tr>
   <td><strong>Quelle différence y a-t-il entre une révision et une version de page ?</strong></td>
   <td>
    <ul>
     <li><strong>Révision du chêne :</strong> Oak organise tout le contenu dans une grande arborescence composée de noeuds et de propriétés. Chaque aperçu ou révision de cet ensemble de contenus inaltérables, ainsi que les modifications de l’arborescence sont indiqués sous forme de séquence de nouvelles révisions. En règle générale, chaque modification de contenu déclenche une nouvelle révision. Voir aussi <a href="https://jackrabbit.apache.org/dev/ngp.html" target="_blank"> Suivre le lien</a>.</li>
     <li><strong>Version de la page :</strong> Le contrôle de version crée un "instantané" d’une page à un moment donné. En règle générale, une nouvelle version est créée lorsqu’une page est activée. For more information, see <a href="/help/sites-authoring/working-with-page-versions.md" target="_blank">Working with Page Versions</a>.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Comment accélérer la tâche de nettoyage des révisions hors ligne si elle n’est pas terminée au bout de 8 heures ?</strong></td>
   <td>If the revision task does not complete within 8 hours and the <a href="/help/sites-administering/operations-dashboard.md#diagnosis-tools" target="_blank">thread dumps</a> reveal that the main hotspot is <code>InMemoryCompactionMap.findEntry</code>, use the following parameter with the oak-run tool <strong>versions 1.4 </strong>or higher: <code>-Dtar.PersistCompactionMap=true</code>. Be aware that the <code>-Dtar.PersistCompactionMap</code> parameter has been removed in Oak version 1.6.</td>
  </tr>
 </tbody>
</table>

