---
title: Tâches de maintenance avant la mise à niveau
seo-title: Tâches de maintenance avant la mise à niveau
description: Découvrez les tâches de maintenance préalables à la mise à niveau dans AEM.
seo-description: Découvrez les tâches de maintenance préalables à la mise à niveau dans AEM.
uuid: 5da1cfc7-8a10-47b1-aafb-2cd112e3f818
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: upgrading
discoiquuid: 291c91e5-65ff-473d-ac11-3da480239e76
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# Tâches de maintenance avant la mise à niveau{#pre-upgrade-maintenance-tasks}

Avant de démarrer la mise à niveau, il est important de suivre les tâches de maintenance suivantes pour vous assurer que le système est prêt et peut être restauré si des problèmes surviennent :

* [Vérifiez que vous avez suffisamment d’espace disque](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#ensure-sufficient-disk-space)
* [Effectuez une sauvegarde complète d’AEM ](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#fully-back-up-aem)
* [Sauvegardez les modifications sur /etc](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#backup-changes-etc)
* [Générez le fichier quickstart.properties](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#generate-quickstart-properties)
* [Configurez la purge du workflow et du journal d’audit](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#configure-wf-audit-purging)
* [Installez, configurez et exécutez les tâches précédant la mise à niveau](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#install-configure-run-pre-upgrade-tasks)
* [Désactivez les modules personnalisés de connexion](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#disable-custom-login-modules)
* [Supprimez les mises à jour du répertoire /install](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#remove-updates-install-directory)
* [Arrêtez toutes les instances Cold Standby](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#stop-tarmk-coldstandby-instance)
* [Désactivez les tâches planifiées personnalisées](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#disable-custom-scheduled-jobs)
* [Effectuez un nettoyage des révisions hors ligne](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#execute-offline-revision-cleanup)
* [Exécutez le nettoyage de la mémoire de l’entrepôt de données](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#execute-datastore-garbage-collection)
* [Mettre à niveau le schéma de base de données si nécessaire](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#upgradethedatabaseschemaifneeded)
* [Suppression des utilisateurs susceptibles de gêner la mise à niveau](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#delete-users-that-might-hinder-the-upgrade)

* [Effectuez la rotation des fichiers journaux](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#rotate-log-files)

## Vérification de l’espace disque {#ensure-sufficient-disk-space}

Lors de l’exécution de la mise à niveau, en plus des activités de mise à niveau de contenu et du code, une migration du référentiel doit être effectuée. La migration crée une copie du référentiel dans le nouveau format tar de segment. Par conséquent, vous devez disposer de suffisamment d’espace disque pour conserver une seconde version du référentiel, potentiellement plus grande.

## Sauvegarde complète d’AEM {#fully-back-up-aem}

AEM doit être entièrement sauvegardé avant de commencer la mise à niveau. Veillez à sauvegarder votre référentiel, l’installation de l’application, la banque de données et les instances Mongo, le cas échéant. Pour plus d’informations sur la sauvegarde et la restauration d’une instance AEM, voir [Sauvegarde et restauration](/help/sites-administering/backup-and-restore.md). 

## Sauvegarde des modifications sur /etc {#backup-changes-etc}

The upgrade process does a good job of maintaining and merging existing content and configurations from under the `/apps` and `/libs` paths in the repository. For changes made to the `/etc` path, including Context Hub configurations, it is often necessary to re-apply these changes after the upgrade. While the upgrade will make a backup copy of any changes that it cannot merge under `/var`, we recommend backing up these changes manually before beginning the upgrade.

## Génération du fichier quickstart.properties {#generate-quickstart-properties}

Lors du démarrage d’AEM depuis le fichier jar, un fichier `quickstart.properties` est généré sous `crx-quickstart/conf`. Si AEM a uniquement été lancé avec le script de démarrage dans le passé, ce fichier ne sera pas présent et la mise à niveau échouera. Veillez à vérifier l’existence de ce fichier et à redémarrer AEM depuis le fichier jar s’il n’existe pas. 

## Configuration de la purge du workflow et du journal d’audit {#configure-wf-audit-purging}

Les tâches `WorkflowPurgeTask` et `com.day.cq.audit.impl.AuditLogMaintenanceTask` nécessitent des configurations OSGi distinctes et ne fonctionneront pas sans celles-ci. Si elles échouent lors de l’exécution des tâches avant la mise à niveau, les configurations manquantes en sont la cause la plus probable. Par conséquent, veillez à ajouter des configurations OSGi pour ces tâches ou à les supprimer de la liste de tâches d’optimisation avant la mise à niveau si vous ne souhaitez pas les exécuter. La documentation pour la configuration des tâches de purge du workflow se trouve dans la section [Administration des instances de workflow](/help/sites-administering/workflows-administering.md) et la configuration des tâches de maintenance du journal d’audit se trouve dans la section [Maintenance du journal d’audit dans AEM 6](/help/sites-administering/operations-audit-log.md).

Pour la purge du workflow et du journal d’audit dans CQ 5.6 et la purge du journal d’audit dans AEM 6.0, voir [Purge du workflow et des nœuds d’audit](https://helpx.adobe.com/experience-manager/kb/howtopurgewf.html).

## Installation, configuration et exécution des tâches précédant la mise à niveau {#install-configure-run-pre-upgrade-tasks}

En raison du niveau de personnalisation accordé par AEM, il n’existe généralement pas de méthode uniforme pour effectuer les mises à niveau. Ceci complique la création d’une procédure standard de mise à niveau.

Dans les versions précédentes, il était aussi difficile pour les mises à niveau AEM qui ont été arrêtées ou ont échoué d’êtres enlevées sans risque. Cela a entrainé des situations dans lesquelles il était nécessaire d’effectuer un redémarrage complet d’une mise à niveau, ou des mises à niveau défectueuses ont été appliquées sans aucun avertissement. 

Pour remédier à ces problemes, Adobe a ajouté plusieurs améliorations au processus de mise à niveau en vue de la rendre plus robuste et facile à utiliser. Les tâches de maintenance précédant la niveau, qui auparavant devaient être effectuées manuellement, sont en train d’être optimisées et automatisées. De même, des rapports d’après mise à niveau ont été ajoutés pour assurer un examen complet de la procédure en vue d’identifier plus facilement les problèmes.

Les tâches de maintenance postérieures à la mise à niveau sont actuellement réparties dans différentes interfaces, qui sont partiellement ou totalement exécutées manuellement. L’optimisation de la maintenance avant la mise à niveau apparue dans la version AEM 6.3 permet de déclencher ces tâches de façon unifiée et d’examiner leurs résultats sur demande.

Toutes les tâches comprises dans cette étape d’optimisation postérieure à la mise à niveau sont compatibles avec toutes les versions à partir d’AEM 6.0.

### Configuration {#how-to-set-it-up}

Dans AEM 6.3 et versions ultérieures, les tâches d’optimisation de la maintenance précédant la mise à niveau sont incluses dans le fichier jar de démarrage rapide. Si vous effectuez une mise à niveau à partir d’une ancienne version d’AEM 6, elles sont disponibles via des packages distincts que vous pouvez télécharger à partir du gestionnaire de modules.

Vous pouvez trouver les modules à ces emplacements :

* [Pour effectuer la mise à jour à partir d’AEM 6.0](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq600/product/pre-upgrade-tasks-content-cq60)

* [Pour effectuer la mise à jour à partir d’AEM 6.1](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq610/product/pre-upgrade-tasks-content-cq61)

* [Pour effectuer la mise à jour à partir d’AEM 6.2](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq620/product/pre-upgrade-tasks-content-cq62)

### Utilisation {#how-to-use-it}

Le composant OSGi `PreUpgradeTasksMBean` est préconfiguré avec une liste de tâches de maintenance bénéficiant déjà de la mise à niveau, pouvant toutes être exécutées simultanément. Vous pouvez configurer les tâches en suivant la procédure ci-dessous :

1. Go to the Web Console by browsing to *https://serveraddress:serverport/system/console/configMgr*

1. Recherchez « **preupgradetasks** », puis cliquez sur le premier composant correspondant. Le nom complet du composant est `com.adobe.aem.upgrade.prechecks.mbean.impl.PreUpgradeTasksMBeanImpl`.

1. Modifiez la liste des tâches de maintenance devant être exécutées comme illustré ci-dessous :

   ![1487758925984](assets/1487758925984.png)

La liste des tâches varie selon le mode d’exécution utilisé pour démarrer l’instance. Vous trouverez ci-dessous une description du mode d’exécution pour lequel chaque tâche de maintenance est conçue. 

<table>
 <tbody>
  <tr>
   <td><strong>Tâche</strong></td>
   <td><strong>Mode d’exécution</strong></td>
   <td><strong>Notes</strong></td>
  </tr>
  <tr>
   <td><code>TarIndexMergeTask</code></td>
   <td>crx2</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>DataStoreGarbageCollectionTask</code></td>
   <td>crx2</td>
   <td>Exécute le marquage et le balayage. Pour les banques de données partagées, supprimez cette étape et procédez à l’exécution<br /> manuellement ou préparez correctement les instances avant l’exécution. </td>
  </tr>
  <tr>
   <td><code>ConsistencyCheckTask</code></td>
   <td>crx2</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>WorkflowPurgeTask</code></td>
   <td>crx2/crx3</td>
   <td>Doit configurer la configuration OSGi de purge du workflow Adobe Granite avant l’exécution.</td>
  </tr>
  <tr>
   <td><code>GenerateBundlesListFileTask</code></td>
   <td>crx2/crx3</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>RevisionCleanupTask</code></td>
   <td>crx3</td>
   <td>Pour les instances TarMK sur AEM de 6.0 à 6.2, il faut plutôt exécuter manuellement le nettoyage des révisions hors ligne.</td>
  </tr>
  <tr>
   <td><code>com.day.cq.audit.impl.AuditLogMaintenanceTask</code></td>
   <td>crx3</td>
   <td>Doit configurer la configuration OSGi du planificateur de purge de journal d’audit avant l’exécution.</td>
  </tr>
 </tbody>
</table>

>[!CAUTION]
>
>`DataStoreGarbageCollectionTask` appelle l’opération de nettoyage de l’entrepôt de données avec la phase de marquage et de balayage le cas échéant. Pour les déploiements qui utilisent une banque de données partagée, veillez à la reconfigurer correctement ou à préparer l’instance pour éviter la suppression des éléments référencés par une autre instance. Cela peut nécessiter l’exécution manuelle de la phase de marquage sur toutes les instances avant de déclencher cette tâche postérieure à la mise à niveau.

### Configuration par défaut pour les vérifications d’intégrité antérieures à la mise à niveau {#default-configuration-of-the-pre-upgrade-health-checks}

Le composant OSGi `PreUpgradeTasksMBeanImpl` est préconfiguré avec une liste de balises de vérification de l’intégrité précédant la mise à niveau à exécuter lorsque la méthode `runAllPreUpgradeHealthChecks` est appelée :

* **system** : la balise est utilisée par les vérifications de l’intégrité de la maintenance Granite

* **pre-upgrade** : il s’agit d’une balise personnalisée qui peut être ajoutée à toutes les vérifications d’intégrité dont vous pouvez définir l’exécution·avant une mise à niveau

La liste est modifiable. Vous pouvez utiliser les bouton Plus **(+)** et Moins **(-)** à côté des balises pour ajouter d’autres balises personnalisées ou pour supprimer les balises par défaut.

**Méthodes MBean**

La fonctionnalité bean gérée peut être accessible à l’aide de la [console JMX](/help/sites-administering/jmx-console.md).

Vous pouvez accéder aux MBeans en procédant comme suit : 

1. Going to the JMX Console at *https://serveraddress:serverport/system/console/jmx*
1. Recherchez **PreUpgradeTasks** et cliquez sur le résultat

1. Sélectionnez une méthode à partir de la section **Opérations** et sélectionnez **Invoquer** dans la fenêtre suivante.

Vous trouverez ci-dessous la liste de toutes les méthodes disponibles offertes par `PreUpgradeTasksMBeanImpl` :

<table>
 <tbody>
  <tr>
   <td><strong>Nom de méthode</strong></td>
   <td><strong>Type</strong></td>
   <td><strong>Description</strong></td>
  </tr>
  <tr>
   <td><code>getAvailablePreUpgradeTasksNames()</code></td>
   <td>INFO</td>
   <td>Affiche la liste de noms des tâches de maintenance avant la mise à niveau.</td>
  </tr>
  <tr>
   <td><code>getAvailablePreUpgradeHealthChecksTagNames()</code></td>
   <td>INFO</td>
   <td>Affiche la liste des noms de balises des vérifications d’intégrité précédant la mise à niveau.</td>
  </tr>
  <tr>
   <td><code>runAllPreUpgradeTasks()</code></td>
   <td>ACTION</td>
   <td>Exécute toutes les tâches de maintenance de la liste avant la mise à niveau.</td>
  </tr>
  <tr>
   <td><code>runPreUpgradeTask(preUpgradeTaskName)</code></td>
   <td>ACTION</td>
   <td>Exécute la tâche de maintenance avant la mise à niveau avec le nom donné en tant que paramètre.</td>
  </tr>
  <tr>
   <td><code>isRunAllPreUpgradeTaskRunning()</code></td>
   <td>ACTION_INFO</td>
   <td>Checks if the <code>runAllPreUpgradeTasksmaintenance</code> task is currently running.</td>
  </tr>
  <tr>
   <td><code>getAnyPreUpgradeTaskRunning()</code></td>
   <td>ACTION_INFO</td>
   <td>Vérifie si une tâche de maintenance avant la mise à niveau est en cours d’exécution et <br /> renvoie un tableau contenant les noms des tâches en cours d’exécution.</td>
  </tr>
  <tr>
   <td><code>getPreUpgradeTaskLastRunTime(preUpgradeTaskName)</code></td>
   <td>ACTION</td>
   <td>Affiche l’heure exacte d’exécution de la tâche de maintenance avant la mise à niveau avec le nom donné en tant que paramètre.</td>
  </tr>
  <tr>
   <td><code>getPreUpgradeTaskLastRunState(preUpgradeTaskName)</code></td>
   <td>ACTION</td>
   <td>Affiche le dernier état d’exécution de la tâche de maintenance avant la mise à niveau, avec le nom donné en tant que paramètre.</td>
  </tr>
  <tr>
   <td><code>runAllPreUpgradeHealthChecks(shutDownOnSuccess)</code></td>
   <td>ACTION</td>
   <td><p>Runs all the pre-upgrade health checks and saves their status in a file named <code>preUpgradeHCStatus.properties</code> that is located in the sling home path. If the <code>shutDownOnSuccess</code> parameter is set to <code>true</code>, the AEM instance will be shut down, but only if all the pre-upgrade health checks have an OK status.</p> <p>Le fichier des propriétés est utilisé comme prérequis pour une future mise à niveau<br /> et le processus de mise à niveau est interrompu si l’exécution de la vérification de l’intégrité avant la mise à niveau<br /> échoue. Si vous souhaitez ignorer le résultat des vérifications d’intégrité<br /> avant la mise à niveau et lancer la mise à niveau, vous pouvez supprimer le fichier.</p> </td>
  </tr>
  <tr>
   <td><code>detectUsageOfUnavailableAPI(aemVersion)</code></td>
   <td>ACTION</td>
   <td>Répertorie tous les modules importés qui ne fonctionneront plus<br /> lors du passage à la version d’AEM spécifiée. La version cible d’AEM doit être<br /> fournie en tant que paramètre. </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Les méthodes MBean peuvent être invoquées via : 
>
>* La console JMX
>* Toute application externe qui se connecte à JMX
>* cURL
>



## Désactivation des modules de connexion personnalisés {#disable-custom-login-modules}

>[!NOTE]
>
>Cette étape est nécessaire uniquement si vous effectuez une mise à niveau à partir d’une version d’AEM 5. Elle peut être entièrement ignorée pour les mises à niveau des versions ultérieures à AEM 6.

The way custom `LoginModules` are configured for authentication at the repository level has fundamentally changed in Apache Oak.

In AEM versions that used CRX2 configuration was placed in the `repository.xml` file, while from AEM 6 onwards it is done in the Apache Felix JAAS Configuration Factory service via the Web Console.

En conséquence, toute configuration existante doit être désactivée et recréée pour Apache Oak après la mise à niveau.

Pour désactiver les modules personnalisés définis dans la configuration JAAS de `repository.xml`, vous devez modifier la configuration afin d’utiliser le `LoginModule` par défaut, comme dans cet exemple :

```xml
<Security >
             ....
          <!--
                 Use LoginModule authenticating against repository itself
                 -->
                 <LoginModule class = "com.day.crx.core.CRXLoginModule" >
                     <param name = "anonymousId" value = "anonymous" />
                     <param name = "adminId" value ="admin" />
                     <param name = "disableNTLMAuth" value = "true" />
                     <param name = "tokenExpiration" value = "43200000" />
                     <!-- param name="trust_credentials_attribute" value="d5b9167e95dad6e7d3b5d6fa8df48af8"/
                -->
                 </LoginModule >
         </ Security>
```

>[!NOTE]
>
>Pour plus d’informations, voir [Authentification avec le module de connexion externe](https://jackrabbit.apache.org/oak/docs/security/authentication/externalloginmodule.html).
>
>Pour un exemple de configuration `LoginModule` dans AEM 6, voir [Configuration de LDAP avec AEM 6](/help/sites-administering/ldap-config.md).

## Supprimez les mises à jour du répertoire /install {#remove-updates-install-directory}

>[!NOTE]
>
>Ne supprimez les modules du répertoire crx-quickstart/install qu’APRÈS avoir arrêté l’instance AEM. Il s’agit de l’une des dernières étapes avant le lancement de la procédure de mise à niveau statique.

Supprimez tous les Service Packs, les Feature Packs ou les correctifs logiciels qui ont été déployés via le répertoire `crx-quickstart/install` sur le système de fichiers local. Cela empêche l’installation accidentelle d’anciens correctifs et Service Packs sur la nouvelle version d’AEM après la mise à jour.

## Arrêt de toutes les instances Cold Standby {#stop-tarmk-coldstandby-instance}

Si vous utilisez TarMK Cold Standby, arrêtez toutes les instances Cold Standby. Cela vous offre une façon efficace de revenir en ligne en cas de problème avec la mise à niveau. Une fois que la mise à niveau a abouti, les instances Cold Standby devront être recréées à partir des instances principales mises à niveau.

## Désactivation des tâches planifiées personnalisées {#disable-custom-scheduled-jobs}

Désactivez toutes les tâches OSGi planifiées qui sont incluses dans le code de l’application.

## Exécution d’un nettoyage des révisions hors ligne {#execute-offline-revision-cleanup}

>[!NOTE]
>
>Cette étape est nécessaire uniquement pour les installations TarMK

Si vous utilisez TarMK, vous devez effectuer le nettoyage des révisions hors ligne avant de procéder à la mise à niveau. Ainsi, l’étape de migration du référentiel et les tâches de mise à niveau associées sont nettement plus rapides et permettent de garantir que le nettoyage des révisions en ligne s’exécute correctement une fois la mise à niveau terminée. Pour plus d’informations sur l’exécution du nettoyage des révisions hors ligne, voir [Exécution du nettoyage des révisions hors ligne](/help/sites-deploying/storage-elements-in-aem-6.md#performing-offline-revision-cleanup).

## Exécution du nettoyage de la mémoire de l’entrepôt de données {#execute-datastore-garbage-collection}

>[!NOTE]
>
>Cette étape est nécessaire uniquement pour les instances exécutant crx3

Après l’exécution du nettoyage des révisions sur les instances CRX3, vous devez procéder au nettoyage de la mémoire de l’entrepôt de données pour supprimer les tâches non référencées dans l’entrepôt de données. Pour obtenir des instructions, consultez la documentation sur le [nettoyage de la mémoire de l’entrepôt de données](/help/sites-administering/data-store-garbage-collection.md). 

## Mettre à niveau le schéma de base de données si nécessaire {#upgrade-the-database-schema-if-needed}

En règle générale, la pile Apache Oak sous-jacente utilisée par AEM pour la persistance s’occupera de la mise à niveau du schéma de base de données si nécessaire.

Cependant, des cas peuvent se produire lorsque le schéma ne peut pas être mis à niveau automatiquement. Il s’agit principalement d’environnements de haute sécurité dans lesquels la base de données est exécutée sous un utilisateur avec des privilèges très limités. Si cela se produit, AEM continuera à utiliser l’ancien schéma.

Pour éviter cela, vous devez mettre à niveau le schéma en suivant la procédure ci-dessous :

1. Arrêtez l’instance AEM qui doit être mise à niveau.
1. Mettez à niveau le schéma de base de données. Consultez la documentation relative au type de base de données afin de connaître les outils dont vous avez besoin pour y parvenir.

   Pour plus d’informations sur la façon dont Oak gère les mises à niveau de schémas, voir [cette page sur le site Web](https://jackrabbit.apache.org/oak/docs/nodestore/document/rdb-document-store.html#upgrade)d’Apache.

1. Passez à la mise à niveau d’AEM.

## Suppression des utilisateurs susceptibles de gêner la mise à niveau {#delete-users-that-might-hinder-the-upgrade}

>[!NOTE]
>
>Cette tâche de maintenance préalable à la mise à niveau n’est nécessaire que si :
>
>* Vous effectuez une mise à niveau à partir des versions d’AEM antérieures à AEM 6.3
>* Vous rencontrez les erreurs mentionnées ci-dessous lors de la mise à niveau.
>



Dans certains cas exceptionnels, les utilisateurs du service peuvent se retrouver dans des versions plus anciennes d’AEM incorrectement balisées en tant qu’utilisateurs réguliers.

Dans ce cas, la mise à niveau échoue avec un message comme celui-ci :

```
ERROR [Apache Sling Repository Startup Thread] com.adobe.granite.repository.impl.SlingRepositoryManager Exception in a SlingRepositoryInitializer, SlingRepository service registration aborted
java.lang.RuntimeException: Unable to create service user [communities-utility-reader]:java.lang.RuntimeException: Existing user communities-utility-reader is not a service user.
```

Pour résoudre ce problème, procédez comme suit :

1. Détacher l’instance du trafic de production
1. Créez une sauvegarde des utilisateurs à l’origine du problème. Vous pouvez le faire via Package Manager. For more information, see [How to Work with Packages.](/help/sites-administering/package-manager.md)
1. Supprimez le ou les utilisateurs à l’origine du problème. Vous trouverez ci-dessous la liste des utilisateurs qui pourraient appartenir à cette catégorie :

   1. `dynamic-media-replication`
   1. `communities-ugc-writer`
   1. `communities-utility-reader`
   1. `communities-user-admin`
   1. `oauthservice`
   1. `sling-scripting`

## Rotation des fichiers journaux {#rotate-log-files}

Il est conseillé d’archiver vos fichiers journal actuels avant de lancer la mise à niveau. Il sera alors plus facile de surveiller et d’analyser vos fichiers journaux pendant et après la mise à niveau pour identifier et résoudre les problèmes qui peuvent survenir. 
