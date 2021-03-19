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
feature: Mise à niveau
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2159'
ht-degree: 76%

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
* [Mettre à niveau le Schéma de base de données si nécessaire](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#upgradethedatabaseschemaifneeded)
* [Suppression des utilisateurs susceptibles de gêner la mise à niveau](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#delete-users-that-might-hinder-the-upgrade)

* [Effectuez la rotation des fichiers journaux](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#rotate-log-files)

## Vérification de l’espace disque {#ensure-sufficient-disk-space}

Lors de l’exécution de la mise à niveau, en plus des activités de mise à niveau de contenu et du code, une migration du référentiel doit être effectuée. La migration crée une copie du référentiel dans le nouveau format tar de segment. Par conséquent, vous devez disposer de suffisamment d’espace disque pour conserver une seconde version du référentiel, potentiellement plus grande.

## Sauvegarde complète d’AEM  {#fully-back-up-aem}

AEM doit être entièrement sauvegardé avant de commencer la mise à niveau. Veillez à sauvegarder votre référentiel, l’installation de l’application, la banque de données et les instances Mongo, le cas échéant. Pour plus d’informations sur la sauvegarde et la restauration d’une instance AEM, voir [Sauvegarde et restauration](/help/sites-administering/backup-and-restore.md). 

## Sauvegarde des modifications sur /etc  {#backup-changes-etc}

Le processus de mise à niveau permet de gérer et de fusionner le contenu et les configurations existants sous les chemins `/apps` et `/libs` dans le référentiel. Pour les modifications apportées au chemin `/etc`, y compris les configurations Context Hub, il est souvent nécessaire de les réappliquer après la mise à niveau. Bien que la mise à niveau effectue une copie de sauvegarde des modifications qu&#39;elle ne peut pas fusionner sous `/var`, nous vous recommandons de les sauvegarder manuellement avant de commencer la mise à niveau.

## Génération du fichier quickstart.properties {#generate-quickstart-properties}

Lors du démarrage d’AEM depuis le fichier jar, un fichier `quickstart.properties` est généré sous `crx-quickstart/conf`. Si AEM a uniquement été lancé avec le script de démarrage dans le passé, ce fichier ne sera pas présent et la mise à niveau échouera. Veillez à vérifier l’existence de ce fichier et à redémarrer AEM depuis le fichier jar s’il n’existe pas. 

## Configuration de la purge du workflow et du journal d’audit  {#configure-wf-audit-purging}

Les tâches `WorkflowPurgeTask` et `com.day.cq.audit.impl.AuditLogMaintenanceTask` nécessitent des configurations OSGi distinctes et ne fonctionneront pas sans celles-ci. Si elles échouent lors de l’exécution des tâches avant la mise à niveau, les configurations manquantes en sont la cause la plus probable. Par conséquent, veillez à ajouter des configurations OSGi pour ces tâches ou à les supprimer de la liste de tâches d’optimisation avant la mise à niveau si vous ne souhaitez pas les exécuter. La documentation pour la configuration des tâches de purge du workflow se trouve dans la section [Administration des instances de workflow](/help/sites-administering/workflows-administering.md) et la configuration des tâches de maintenance du journal d’audit se trouve dans la section [Maintenance du journal d’audit dans AEM 6](/help/sites-administering/operations-audit-log.md).

Pour la purge du workflow et du journal d’audit dans CQ 5.6 et la purge du journal d’audit dans AEM 6.0, voir [Purge du workflow et des nœuds d’audit](https://helpx.adobe.com/experience-manager/kb/howtopurgewf.html).

## Installation, configuration et exécution des tâches précédant la mise à niveau  {#install-configure-run-pre-upgrade-tasks}

En raison du niveau de personnalisation accordé par AEM, il n’existe généralement pas de méthode uniforme pour effectuer les mises à niveau. Ceci complique la création d’une procédure standard de mise à niveau.

Dans les versions précédentes, il était aussi difficile pour les mises à niveau AEM qui ont été arrêtées ou ont échoué d’êtres enlevées sans risque. Cela a entrainé des situations dans lesquelles il était nécessaire d’effectuer un redémarrage complet d’une mise à niveau, ou des mises à niveau défectueuses ont été appliquées sans aucun avertissement. 

Pour remédier à ces problemes, Adobe a ajouté plusieurs améliorations au processus de mise à niveau en vue de la rendre plus robuste et facile à utiliser. Les tâches de maintenance précédant la niveau, qui auparavant devaient être effectuées manuellement, sont en train d’être optimisées et automatisées. De même, des rapports d’après mise à niveau ont été ajoutés pour assurer un examen complet de la procédure en vue d’identifier plus facilement les problèmes.

Les tâches de maintenance postérieures à la mise à niveau sont actuellement réparties dans différentes interfaces, qui sont partiellement ou totalement exécutées manuellement. L’optimisation de la maintenance avant la mise à niveau apparue dans la version AEM 6.3 permet de déclencher ces tâches de façon unifiée et d’examiner leurs résultats sur demande.

Toutes les tâches comprises dans cette étape d’optimisation postérieure à la mise à niveau sont compatibles avec toutes les versions à partir d’AEM 6.0.

### Configuration  {#how-to-set-it-up}

Dans AEM 6.3 et versions ultérieures, les tâches d’optimisation de la maintenance précédant la mise à niveau sont incluses dans le fichier jar de démarrage rapide. Si vous effectuez une mise à niveau à partir d’une ancienne version d’AEM 6, elles sont disponibles via des packages distincts que vous pouvez télécharger à partir du gestionnaire de modules.

Vous pouvez trouver les modules à ces emplacements :

* [Pour effectuer la mise à jour à partir d’AEM 6.0](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq600/product/pre-upgrade-tasks-content-cq60)

* [Pour effectuer la mise à jour à partir d’AEM 6.1](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq610/product/pre-upgrade-tasks-content-cq61)

* [Pour effectuer la mise à jour à partir d’AEM 6.2](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq620/product/pre-upgrade-tasks-content-cq62)

### Utilisation {#how-to-use-it}

Le composant OSGi `PreUpgradeTasksMBean` est préconfiguré avec une liste de tâches de maintenance bénéficiant déjà de la mise à niveau, pouvant toutes être exécutées simultanément. Vous pouvez configurer les tâches en suivant la procédure ci-dessous :

1. Accédez à la console Web en accédant à *https://serveraddress:serverport/system/console/configMgr*.

1. Recherchez « **preupgradetasks** », puis cliquez sur le premier composant correspondant. Le nom complet du composant est `com.adobe.aem.upgrade.prechecks.mbean.impl.PreUpgradeTasksMBeanImpl`.

1. Modifiez la liste des tâches de maintenance devant être exécutées comme illustré ci-dessous :

   ![1487758925984](assets/1487758925984.png)

La liste des tâches varie selon le mode d’exécution utilisé pour démarrer l’instance. Vous trouverez ci-dessous une description du mode d’exécution pour lequel chaque tâche de maintenance est conçue. 

<table>
 <tbody>
  <tr>
   <td><strong>Tâche</strong></td>
   <td><strong>Mode d’exécution</strong></td>
   <td><strong>Remarques</strong></td>
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

### Configuration par défaut pour les vérifications d’intégrité antérieures à la mise à niveau  {#default-configuration-of-the-pre-upgrade-health-checks}

Le composant OSGi `PreUpgradeTasksMBeanImpl` est préconfiguré avec une liste de balises de vérification de l’intégrité précédant la mise à niveau à exécuter lorsque la méthode `runAllPreUpgradeHealthChecks` est appelée :

* **system** : la balise est utilisée par les vérifications de l’intégrité de la maintenance Granite

* **pre-upgrade** : il s’agit d’une balise personnalisée qui peut être ajoutée à toutes les vérifications d’intégrité dont vous pouvez définir l’exécution·avant une mise à niveau

La liste est modifiable. Vous pouvez utiliser les bouton Plus **(+)** et Moins **(-)** à côté des balises pour ajouter d’autres balises personnalisées ou pour supprimer les balises par défaut.

**Méthodes MBean**

La fonctionnalité bean gérée peut être accessible à l’aide de la [console JMX](/help/sites-administering/jmx-console.md).

Vous pouvez accéder aux MBeans en procédant comme suit : 

1. Accédez à la console JMX à l’adresse *https://serveraddress:serverport/system/console/jmx*.
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
   <td>ACTION </td>
   <td>Exécute toutes les tâches de maintenance de la liste avant la mise à niveau.</td>
  </tr>
  <tr>
   <td><code>runPreUpgradeTask(preUpgradeTaskName)</code></td>
   <td>ACTION </td>
   <td>Exécute la tâche de maintenance avant la mise à niveau avec le nom donné en tant que paramètre.</td>
  </tr>
  <tr>
   <td><code>isRunAllPreUpgradeTaskRunning()</code></td>
   <td>ACTION_INFO</td>
   <td>Vérifie si la tâche <code>runAllPreUpgradeTasksmaintenance</code> est en cours d'exécution.</td>
  </tr>
  <tr>
   <td><code>getAnyPreUpgradeTaskRunning()</code></td>
   <td>ACTION_INFO</td>
   <td>Vérifie si une tâche de maintenance avant la mise à niveau est en cours d’exécution et <br /> renvoie un tableau contenant les noms des tâches en cours d’exécution.</td>
  </tr>
  <tr>
   <td><code>getPreUpgradeTaskLastRunTime(preUpgradeTaskName)</code></td>
   <td>ACTION </td>
   <td>Affiche l’heure exacte d’exécution de la tâche de maintenance avant la mise à niveau avec le nom donné en tant que paramètre.</td>
  </tr>
  <tr>
   <td><code>getPreUpgradeTaskLastRunState(preUpgradeTaskName)</code></td>
   <td>ACTION </td>
   <td>Affiche le dernier état d’exécution de la tâche de maintenance avant la mise à niveau, avec le nom donné en tant que paramètre.</td>
  </tr>
  <tr>
   <td><code>runAllPreUpgradeHealthChecks(shutDownOnSuccess)</code></td>
   <td>ACTION </td>
   <td><p>exécute toutes les vérifications d'intégrité préalables à la mise à niveau et enregistre leur état dans un fichier nommé <code>preUpgradeHCStatus.properties</code> qui se trouve dans le chemin d'accès d'accueil sling. Si le paramètre <code>shutDownOnSuccess</code> est défini sur <code>true</code>, l'instance AEM sera fermée, mais uniquement si toutes les vérifications d'intégrité préalables à la mise à niveau ont l'état OK.</p> <p>Le fichier des propriétés est utilisé comme prérequis pour une future mise à niveau<br /> et le processus de mise à niveau est interrompu si l’exécution de la vérification de l’intégrité avant la mise à niveau<br /> échoue. Si vous souhaitez ignorer le résultat des vérifications d’intégrité<br /> avant la mise à niveau et lancer la mise à niveau, vous pouvez supprimer le fichier.</p> </td>
  </tr>
  <tr>
   <td><code>detectUsageOfUnavailableAPI(aemVersion)</code></td>
   <td>ACTION </td>
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



## Désactivation des modules de connexion personnalisés  {#disable-custom-login-modules}

>[!NOTE]
>
>Cette étape est nécessaire uniquement si vous effectuez une mise à niveau à partir d’une version d’AEM 5. Elle peut être entièrement ignorée pour les mises à niveau des versions ultérieures à AEM 6.

La façon dont les `LoginModules` personnalisés sont configurés pour l&#39;authentification au niveau du référentiel a fondamentalement changé dans Apache Oak.

Dans AEM versions qui utilisaient la configuration CRX2, il a été placé dans le fichier `repository.xml`, tandis qu&#39;à partir de AEM 6, il est effectué dans le service Apache Felix JAAS Configuration Factory via la console Web.

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

## Arrêt de toutes les instances Cold Standby  {#stop-tarmk-coldstandby-instance}

Si vous utilisez TarMK Cold Standby, arrêtez toutes les instances Cold Standby. Cela vous offre une façon efficace de revenir en ligne en cas de problème avec la mise à niveau. Une fois que la mise à niveau a abouti, les instances Cold Standby devront être recréées à partir des instances principales mises à niveau.

## Désactivation des tâches planifiées personnalisées  {#disable-custom-scheduled-jobs}

Désactivez toutes les tâches OSGi planifiées qui sont incluses dans le code de l’application.

## Exécution d’un nettoyage des révisions hors ligne  {#execute-offline-revision-cleanup}

>[!NOTE]
>
>Cette étape est nécessaire uniquement pour les installations TarMK

Si vous utilisez TarMK, vous devez effectuer le nettoyage des révisions hors ligne avant de procéder à la mise à niveau. Ainsi, l’étape de migration du référentiel et les tâches de mise à niveau associées sont nettement plus rapides et permettent de garantir que le nettoyage des révisions en ligne s’exécute correctement une fois la mise à niveau terminée. Pour plus d’informations sur l’exécution du nettoyage des révisions hors ligne, voir [Exécution du nettoyage des révisions hors ligne](/help/sites-deploying/storage-elements-in-aem-6.md#performing-offline-revision-cleanup).

## Exécution du nettoyage de la mémoire de l’entrepôt de données  {#execute-datastore-garbage-collection}

>[!NOTE]
>
>Cette étape est nécessaire uniquement pour les instances exécutant crx3

Après l’exécution du nettoyage des révisions sur les instances CRX3, vous devez procéder au nettoyage de la mémoire de l’entrepôt de données pour supprimer les tâches non référencées dans l’entrepôt de données. Pour obtenir des instructions, consultez la documentation sur le [nettoyage de la mémoire de l’entrepôt de données](/help/sites-administering/data-store-garbage-collection.md). 

## Mettre à niveau le Schéma de base de données si nécessaire {#upgrade-the-database-schema-if-needed}

Habituellement, la pile Apache Oak sous-jacente utilisée AEM pour la persistance prend en charge la mise à niveau du schéma de base de données si nécessaire.

Cependant, il peut arriver que le schéma ne puisse pas être mis à niveau automatiquement. Il s&#39;agit principalement d&#39;environnements de sécurité élevée où la base de données s&#39;exécute sous un utilisateur avec des privilèges très limités. Si cela se produit, AEM continuera à utiliser l&#39;ancien schéma.

Pour éviter cela, vous devez mettre à niveau le schéma en suivant la procédure ci-dessous :

1. Arrêtez l’instance AEM qui doit être mise à niveau.
1. Mettez à niveau le schéma de base de données. Veuillez consulter la documentation relative au type de base de données afin de connaître les outils dont vous avez besoin pour ce faire.

   Pour plus d’informations sur la façon dont Oak gère les mises à niveau de schéma, voir [cette page sur le site Web d’Apache](https://jackrabbit.apache.org/oak/docs/nodestore/document/rdb-document-store.html#upgrade).

1. Passez à l’AEM de mise à niveau.

## Supprimer les utilisateurs susceptibles de gêner la mise à niveau {#delete-users-that-might-hinder-the-upgrade}

>[!NOTE]
>
>Cette tâche de maintenance antérieure à la mise à niveau n&#39;est nécessaire que si :
>
>* Vous effectuez une mise à niveau depuis AEM versions antérieures à AEM 6.3
>* Vous rencontrez les erreurs mentionnées ci-dessous lors de la mise à niveau.

>



Dans certains cas exceptionnels, les utilisateurs du service risquent de se retrouver dans des versions AEM plus anciennes mal balisées en tant qu’utilisateurs réguliers.

Si cela se produit, la mise à niveau échoue avec un message comme celui-ci :

```
ERROR [Apache Sling Repository Startup Thread] com.adobe.granite.repository.impl.SlingRepositoryManager Exception in a SlingRepositoryInitializer, SlingRepository service registration aborted
java.lang.RuntimeException: Unable to create service user [communities-utility-reader]:java.lang.RuntimeException: Existing user communities-utility-reader is not a service user.
```

Pour résoudre ce problème, veillez à effectuer les opérations suivantes :

1. Détacher l’instance du trafic de production
1. Créez une sauvegarde du ou des utilisateurs à l’origine du problème. Vous pouvez le faire via Package Manager. Pour plus d’informations, voir [Comment utiliser des packages.](/help/sites-administering/package-manager.md)
1. Supprimez le ou les utilisateurs à l’origine du problème. Vous trouverez ci-dessous une liste d’utilisateurs susceptibles de tomber sous cette catégorie :

   1. `dynamic-media-replication`
   1. `communities-ugc-writer`
   1. `communities-utility-reader`
   1. `communities-user-admin`
   1. `oauthservice`
   1. `sling-scripting`

## Rotation des fichiers journaux {#rotate-log-files}

Il est conseillé d’archiver vos fichiers journal actuels avant de lancer la mise à niveau. Il sera alors plus facile de surveiller et d’analyser vos fichiers journaux pendant et après la mise à niveau pour identifier et résoudre les problèmes qui peuvent survenir. 
