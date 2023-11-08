---
title: Récupération de l’espace mémoire de l’entrepôt de données
seo-title: Data Store Garbage Collection
description: Découvrez comment configurer le nettoyage de la mémoire d’entrepôt de données pour libérer de l’espace disque.
seo-description: Learn how to configure Data Store Garbage Collection to free up disk space.
uuid: 49488a81-986a-4d1a-96c8-aeb6595fc094
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 5b1e46c5-7e56-433e-b62e-2a76ea7be0fd
docset: aem65
exl-id: 0dc4a8ce-5b0e-4bc9-a6f5-df2a67149e22
source-git-commit: 941e5d7574d31622f50e50e717c21cd2eba2e602
workflow-type: tm+mt
source-wordcount: '1884'
ht-degree: 66%

---

# Récupération de l’espace mémoire de l’entrepôt de données {#data-store-garbage-collection}

Lorsqu’une ressource WCM conventionnelle est supprimée, la référence à l’enregistrement d’entrepôt de données sous-jacent peut être supprimée de la hiérarchie de nœud, mais l’enregistrement d’entrepôt de données lui-même est conservé. Cet enregistrement d’entrepôt de données non référencé devient alors &quot;ordure&quot; qui n’a pas besoin d’être conservée. Dans les cas où plusieurs ressources de mémoire existent, il est préférable de les éliminer pour préserver de l’espace et optimiser les performances de sauvegarde et de maintenance du système de fichiers.

Le plus souvent, une application WCM tend à collecter des informations, mais à ne pas les supprimer aussi souvent. Bien que de nouvelles images soient ajoutées qui remplacent même les anciennes versions, le système de contrôle de version conserve encore l’ancienne version et prend sa restauration en charge si nécessaire. Ainsi, la majorité du contenu que nous pensons ajouter au système est définitivement stocké. Quelle est donc la source type de &quot;déchets&quot; dans le référentiel que nous pourrions vouloir nettoyer ?

AEM utilise le référentiel comme stockage pour plusieurs activités internes et de maintenance :

* Packages créés et téléchargés
* Fichiers temporaires créés pour la réplication de publication
* Payloads des workflows
* Ressources créées temporairement lors du rendu de la gestion des ressources numériques

Lorsque l’un de ces objets temporaires est assez volumineux pour devoir être stocké dans l’entrepôt de données et lorsque cet objet n’est plus utilisé, l’enregistrement d’entrepôt de données lui-même demeure en tant que « données à nettoyer ». Dans une application de création/publication WCM standard, le processus d’activation de publication constitue généralement la plus grande source de données à nettoyer de ce type. Lorsque des données sont répliquées en publication, elles sont d’abord regroupées dans des collections ayant un format de données efficace nommé « Durbo » et stockées dans le référentiel, sous `/var/replication/data`. Les lots de données dépassent souvent en taille le seuil de taille critique du magasin de données et finissent donc par être stockés comme des enregistrements de magasins de données. Lorsque la réplication est terminée, le nœud dans `/var/replication/data` est supprimé, mais l’enregistrement du magasin de données demeure en tant que « données à nettoyer ».

Les packages constituent une autre source de données à nettoyer récupérables. Les données de package, comme tout le reste, sont stockées dans le référentiel et, donc, pour les packages dont la taille dépasse 4 Ko, dans l’entrepôt de données. Au cours d’un projet de développement ou au fil du temps, lors de la maintenance d’un système, les modules peuvent être créés et reconstruits de nombreuses fois, chaque version entraînant un nouvel enregistrement de l’entrepôt de données, rendant orphelin l’enregistrement de la version précédente.

## Comment fonctionne le nettoyage de la mémoire d’entrepôt de données ? {#how-does-data-store-garbage-collection-work}

Si le référentiel a été configuré avec un entrepôt de données externe, le [nettoyage de la mémoire d’entrepôt de données est exécuté automatiquement](/help/sites-administering/data-store-garbage-collection.md#automating-data-store-garbage-collection) dans le cadre de la période de maintenance hebdomadaire. L’administrateur système peut également [exécuter le nettoyage de la mémoire du magasin de données manuellement](#running-data-store-garbage-collection) selon les besoins. En général, il est recommandé d’effectuer le nettoyage de la mémoire d’entrepôt de données périodiquement, mais de prendre en compte les facteurs suivants lors de la planification du nettoyage de la mémoire d’entrepôt de données :

* Le nettoyage de la mémoire d’entrepôt de données prend du temps et peut avoir un impact sur les performances. Il doit donc être planifié en conséquence.
* La suppression des enregistrements de mémoire d’entrepôt de données n’affecte pas les performances normales. Il ne s’agit donc pas d’une optimisation des performances.
* Si l’utilisation du stockage et les facteurs connexes tels que les temps de sauvegarde ne sont pas un problème, le nettoyage de la mémoire d’entrepôt de données peut être différé en toute sécurité.

Le nettoyeur de la mémoire d’entrepôt de données prend d’abord note de l’horodatage actuel lorsque le processus commence. La collecte est ensuite effectuée à l’aide d’un algorithme de modèle de marquage/balayage à plusieurs passages.

Lors de la première phase, le collecteur de mémoire d’entrepôt de données effectue une traversée complète de tout le contenu du référentiel. Pour chaque objet de contenu qui contient une référence à un enregistrement d’entrepôt de données, il localise le fichier dans le système de fichiers, exécutant une mise à jour de métadonnées (en modifiant l’attribut « dernière modification » ou MTIME). À ce stade, les fichiers accessibles par cette phase deviennent plus récents que l’horodatage de ligne de base initial.

Lors de la seconde phase, le nettoyeur de la mémoire d’entrepôt de données traverse la structure de répertoires physique d’un entrepôt de données à peu près comme une opération de recherche. Il examine l’attribut &quot;last modified&quot; ou MTIME du fichier et détermine ce qui suit :

* Si l’attribut MTIME est plus récent que l’horodatage de base initial, le fichier a été trouvé lors de la première phase ou il s’agit d’un fichier entièrement nouveau qui a été ajouté au référentiel pendant l’exécution du processus de nettoyage. Dans l’un ou l’autre de ces cas, l’enregistrement est considéré comme actif et le fichier ne doit pas être supprimé.
* Si le MTIME est antérieur à l’horodatage initial de la ligne de base, le fichier n’est pas un fichier activement référencé et il est considéré comme une mémoire pouvant être supprimée.

Cette approche fonctionne bien pour un nœud unique avec un entrepôt de données privé. Toutefois, l’entrepôt de données peut être partagé, et si c’est le cas, les références en direct potentiellement actives aux enregistrements d’entrepôt de données d’autres référentiels ne sont pas vérifiées, et les fichiers référencés actifs peuvent être supprimés par erreur. Il est impératif que l’administrateur système comprenne la nature partagée de l’entrepôt de données avant de planifier un nettoyage de la mémoire et n’utilise que le simple processus de nettoyage de la mémoire d’entrepôt de données intégré lorsqu’il est connu que l’entrepôt de données n’est pas partagé.

>[!NOTE]
>
>Lorsque le nettoyage de la mémoire est effectué dans une configuration d’entrepôt de données partagé ou en cluster (avec Mongo ou Segment Tar), le journal peut contenir des avertissements sur l’impossibilité de supprimer certains ID de blob. Ces avertissements se produisent, car les ID de blob supprimés durant un nettoyage précédent sont à nouveau référencés de manière incorrecte par d’autres nœuds partagés ou clusters qui n’ont pas d’informations sur les suppressions des ID. Lorsque le nettoyage est effectué, un avertissement est donc enregistré dans le journal après une tentative de suppression d’un ID qui avait déjà été supprimé lors du précédent nettoyage. Ce comportement n’a toutefois aucune incidence sur les performances ou la fonctionnalité.

## Exécution du nettoyage de la mémoire d’entrepôt de données {#running-data-store-garbage-collection}

Il existe trois façons d’exécuter le nettoyage de la mémoire d’entrepôt de données, selon la configuration de l’entrepôt de données sur laquelle AEM s’exécute :

1. Via le [nettoyage de révision](/help/sites-deploying/revision-cleanup.md) : un mécanisme de récupération de l’espace mémoire généralement utilisé pour le nettoyage des entrepôts de nœuds.

1. Via [Nettoyage de la mémoire d’entrepôt de données](/help/sites-administering/data-store-garbage-collection.md#running-data-store-garbage-collection-via-the-operations-dashboard) - un mécanisme de nettoyage de la mémoire spécifique aux entrepôts de données externes, disponible dans le tableau de bord des opérations.
1. Via le [Console JMX](/help/sites-administering/jmx-console.md).

Si TarMK est utilisé comme entrepôt de nœuds et entrepôt de données, le nettoyage de révision peut être utilisé pour le nettoyage de la mémoire de l’entrepôt de nœuds et l’entrepôt de données. Cependant, si un entrepôt de données externe est configuré comme entrepôt de données de système de fichiers, le nettoyage de la mémoire d’entrepôt de données doit être explicitement déclenché séparément du nettoyage de révision. Le nettoyage de la mémoire d’entrepôt de données peut être déclenché par le biais du tableau de bord des opérations ou de la console JMX.

Le tableau ci-dessous indique le type de nettoyage de la mémoire d’entrepôt de données qui doit être utilisé pour tous les déploiements d’entrepôt de données pris en charge dans AEM 6 :

<table>
 <tbody>
  <tr>
   <td><strong>Magasin de nœuds</strong><br /> </td>
   <td><strong>Magasin de données</strong></td>
   <td><strong>Mécanisme de récupération de l’espace mémoire</strong><br /> </td>
  </tr>
  <tr>
   <td>TarMK</td>
   <td>TarMK</td>
   <td>Nettoyage des révisions (les binaires sont alignés avec le magasin de segments)</td>
  </tr>
  <tr>
   <td>TarMK</td>
   <td>Système de fichiers externe</td>
   <td><p>Tâche de nettoyage de la mémoire du magasin de données via le tableau de bord des opérations</p> <p>Console JMX</p> </td>
  </tr>
  <tr>
   <td>MongoDB</td>
   <td>MongoDB</td>
   <td><p>Tâche de nettoyage de la mémoire du magasin de données via le tableau de bord des opérations</p> <p>Console JMX</p> </td>
  </tr>
  <tr>
   <td>MongoDB</td>
   <td>Système de fichiers externe</td>
   <td><p>Tâche de nettoyage de la mémoire du magasin de données via le tableau de bord des opérations</p> <p>Console JMX</p> </td>
  </tr>
 </tbody>
</table>

### Exécution du nettoyage de la mémoire du magasin de données via le tableau de bord des opérations {#running-data-store-garbage-collection-via-the-operations-dashboard}

La période de maintenance hebdomadaire intégrée, disponible via le [tableau de bord des opérations](/help/sites-administering/operations-dashboard.md), contient une tâche intégrée pour déclencher le nettoyage de la mémoire du magasin de données à 1 heure du matin le dimanche.

Si vous devez exécuter le nettoyage de la mémoire d’entrepôt de données en dehors de cette période, il peut être déclenché manuellement via le tableau de bord des opérations.

Avant d’exécuter le nettoyage de la mémoire d’entrepôt de données, vous devez vérifier qu’aucune sauvegarde n’est en cours d’exécution à ce moment-là.

1. Ouvrez le tableau de bord des opérations en procédant comme suit : **Navigation** -> **Outils** -> **Opérations** -> **Maintenance**.
1. Cliquez ou appuyez sur **Période de maintenance hebdomadaire**.

   ![chlimage_1-64](assets/chlimage_1-64.png)

1. Sélectionnez la tâche **Nettoyage de la mémoire du magasin de données**, puis cliquez ou appuyez sur l’icône **Exécuter**.

   ![chlimage_1-65](assets/chlimage_1-65.png)

1. Le nettoyage de la mémoire du magasin de données s’exécute et son statut s’affiche sur le tableau de bord.

   ![chlimage_1-66](assets/chlimage_1-66.png)

>[!NOTE]
>
>La tâche de nettoyage de la mémoire du magasin de données est uniquement visible si vous avez configuré un magasin de données basé sur les fichiers. Consultez [Configuration de magasins de nœuds et de données dans AEM 6](/help/sites-deploying/data-store-config.md#file-data-store) pour obtenir des informations sur la configuration d’un magasin de données basé sur les fichiers.

### Exécution du nettoyage de la mémoire d’entrepôt de données via la console JMX {#running-data-store-garbage-collection-via-the-jmx-console}

Cette section aborde le nettoyage de la mémoire d’entrepôt de données via la console JMX. Si votre installation est configurée sans entrepôt de données externe, ceci ne s’applique pas. Au lieu de cela, consultez les instructions sur l’exécution du nettoyage de révision sous [Maintenance du référentiel](/help/sites-deploying/storage-elements-in-aem-6.md#maintaining-the-repository).

>[!NOTE]
>
>Si vous exécutez TarMK avec un magasin de données externe, vous devez exécuter le nettoyage de révision d’abord pour que le nettoyage soit efficace.

Pour exécuter la récupération de l’espace mémoire :

1. Dans la console de gestion OSGi Apache Felix, mettez en surbrillance le **Principal** et sélectionnez **JMX** dans le menu suivant.
1. Ensuite, recherchez puis cliquez sur le bouton **Gestionnaire de référentiel** MBean (ou accédez à `https://<host>:<port>/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Drepository+manager%2Ctype%3DRepositoryManagement`).
1. Cliquez sur **startDataStoreGC(boolean markOnly)**.
1. enter &quot;`true`&quot; pour la variable `markOnly` si nécessaire :

   | **Option** | **Description** |
   |---|---|
   | boolean markOnly | Définissez cette variable sur true pour marquer uniquement les références et ne pas effectuer de balayage dans l’opération de marquage et de balayage. Ce mode doit être utilisé lorsque le BlobStore sous-jacent est partagé entre plusieurs référentiels. Pour tous les autres cas, définissez ce paramètre sur false pour effectuer le nettoyage complet de la mémoire. |

1. Cliquez sur **Invoquer**. CRX effectue la récupération de l’espace mémoire et indique quand celle-ci est terminée.

>[!NOTE]
>
>Le nettoyage de la mémoire du magasin de données ne collecte pas les fichiers qui ont été supprimés au cours des dernières 24 heures.

>[!NOTE]
>
>La tâche de nettoyage de la mémoire du magasin de données ne commence que si vous avez configuré un magasin de données basé sur les fichiers. Si aucun magasin de données de fichier externe n’a été configuré, la tâche renvoie le message `Cannot perform operation: no service of type BlobGCMBean found` après l’appel. Consultez [Configuration de magasins de nœuds et de données dans AEM 6](/help/sites-deploying/data-store-config.md#file-data-store) pour obtenir des informations sur la configuration d’un magasin de données basé sur les fichiers.

## Automatisation du nettoyage de la mémoire d’entrepôt de données {#automating-data-store-garbage-collection}

Si possible, le nettoyage de la mémoire d’entrepôt de données doit être exécuté lorsque la charge du système est faible, par exemple, le matin.

La période de maintenance hebdomadaire intégrée, disponible via le [tableau de bord des opérations](/help/sites-administering/operations-dashboard.md), contient une tâche intégrée pour déclencher le nettoyage de la mémoire d’entrepôt de données à 1 heure du matin le dimanche. Vous devez également vérifier qu’aucune sauvegarde n’est en cours à ce moment. Le début de la fenêtre de maintenance peut être personnalisé au besoin à partir du tableau de bord.

>[!NOTE]
>
>La raison pour laquelle vous pouvez ne pas l’exécuter simultanément est que les anciens fichiers (et inutilisés) du magasin de données sont également sauvegardés, de sorte que s’il est nécessaire de restaurer une ancienne révision, les fichiers binaires figurent encore dans la sauvegarde.

Si vous ne souhaitez pas exécuter le nettoyage de la mémoire du magasin de données avec la période de maintenance hebdomadaire dans le tableau de bord des opérations, vous pouvez également l’automatiser à l’aide des clients HTTP wget ou curl. Voici un exemple illustrant comment automatiser la sauvegarde à l’aide de la commande curl :

>[!CAUTION]
>
>Dans les exemples de commande `curl` suivants, il se peut que divers paramètres doivent être configurés pour votre instance. Par exemple, le nom d’hôte (`localhost`), le port (`4502`), le mot de passe administrateur (`xyz`) et divers paramètres pour le nettoyage effectif de la mémoire du magasin de données.

Voici un exemple de commande curl invoquant le nettoyage de la mémoire du magasin de données via la ligne de commande :

```shell
curl -u admin:admin -X POST --data markOnly=true  https://localhost:4503/system/console/jmx/org.apache.jackrabbit.oak"%"3Aname"%"3Drepository+manager"%"2Ctype"%"3DRepositoryManagement/op/startDataStoreGC/boolean
```

La commande curl est immédiatement renvoyée.

## Vérification de la cohérence de l’entrepôt de données {#checking-data-store-consistency}

La vérification de la cohérence de l’entrepôt de données signale les fichiers binaires d’entrepôt de données manquants, mais encore référencés. Pour lancer une vérification de cohérence, procédez comme suit :

1. Accédez à la console JMX. Pour plus d’informations sur l’utilisation de la console JMX, consultez [cet article](/help/sites-administering/jmx-console.md#using-the-jmx-console).
1. Recherchez l’entrée MBean **BlobGarbageCollection** et cliquez dessus.
1. Cliquez sur le lien `checkConsistency()`.

Une fois la vérification de cohérence terminée, un message affiche le nombre de fichiers binaires signalés comme manquants. Si le nombre est supérieur à 0, vérifiez le fichier journal `error.log` pour obtenir plus de détails sur les fichiers manquants.

Vous trouverez ci-dessous un exemple de la façon dont les fichiers binaires manquants sont répertoriés dans les journaux :

```xml
11:32:39.673 INFO [main] MarkSweepGarbageCollector.java:600 Consistency check found [1] missing blobs
```

```xml
11:32:39.673 WARN [main] MarkSweepGarbageCollector.java:602 Consistency check failure intheblob store : DataStore backed BlobStore [org.apache.jackrabbit.oak.plugins.blob.datastore.OakFileDataStore], check missing candidates in file /tmp/gcworkdir-1467352959243/gccand-1467352959243
```
