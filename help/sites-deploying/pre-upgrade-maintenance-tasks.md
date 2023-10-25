---
title: Tâches de maintenance avant la mise à niveau
seo-title: Pre-Upgrade Maintenance Tasks
description: Découvrez les tâches préalables à la mise à niveau recommandées pour AEM.
seo-description: Learn about the pre-upgrade tasks in AEM.
uuid: 5da1cfc7-8a10-47b1-aafb-2cd112e3f818
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: upgrading
discoiquuid: 291c91e5-65ff-473d-ac11-3da480239e76
docset: aem65
feature: Upgrading
exl-id: 37d4aee4-15eb-41ab-ad71-dfbd5c7910f8
source-git-commit: e54c1d422f2bf676e8a7b0f50a101e495c869c96
workflow-type: tm+mt
source-wordcount: '2031'
ht-degree: 99%

---

# Tâches de maintenance avant la mise à niveau{#pre-upgrade-maintenance-tasks}

Avant de commencer la mise à niveau, il est important d’effectuer ces tâches de maintenance pour vous assurer que le système est prêt et peut être restauré en cas de problème :

* [Vérification de la disponibilité de l’espace disque nécessaire](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#ensure-sufficient-disk-space)
* [Sauvegarde complète d’AEM](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#fully-back-up-aem)
* [Sauvegarde des modifications sur /etc](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#backup-changes-etc)
* [Génération du fichier quickstart.properties](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#generate-quickstart-properties)
* [Configuration de la purge du workflow et du journal d’audit](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#configure-wf-audit-purging)
* [Installation, configuration et exécution des tâches précédant la mise à niveau](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#install-configure-run-pre-upgrade-tasks)
* [Désactivation des modules de connexion personnalisés](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#disable-custom-login-modules)
* [Suppression des mises à jour du répertoire /install](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#remove-updates-install-directory)
* [Arrêt de toutes les instances Cold Standby](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#stop-tarmk-coldstandby-instance)
* [Désactivation des tâches planifiées personnalisées](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#disable-custom-scheduled-jobs)
* [Exécution d’un nettoyage des révisions hors ligne](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#execute-offline-revision-cleanup)
* [Exécution de la récupération de l’espace mémoire du magasin de données](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#execute-datastore-garbage-collection)
* [Mise à niveau du schéma de base de données si nécessaire](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#upgradethedatabaseschemaifneeded)
* [Suppression des utilisateurs susceptibles d’entraver la mise à niveau](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#delete-users-that-might-hinder-the-upgrade)

* [Rotation des fichiers journaux](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#rotate-log-files)

## Vérification de la disponibilité de l’espace disque nécessaire {#ensure-sufficient-disk-space}

Lors de l’exécution de la mise à niveau, en plus des activités de mise à niveau de contenu et de code, une migration du référentiel doit être effectuée. La migration crée une copie du référentiel au nouveau format de segment Tar. Par conséquent, vous avez besoin de suffisamment d’espace disque pour conserver une seconde version potentiellement plus grande de votre référentiel.

## Sauvegarde complète d’AEM {#fully-back-up-aem}

AEM doit être entièrement sauvegardé avant le début de la mise à niveau. Veillez à sauvegarder votre référentiel, l’installation de l’application, le magasin de données et les instances Mongo, le cas échéant. Pour plus d’informations sur la sauvegarde et la restauration d’une instance AEM, reportez-vous à la section [Sauvegarde et restauration](/help/sites-administering/backup-and-restore.md).

## Sauvegarde des modifications sur /etc {#backup-changes-etc}

Le processus de mise à niveau est utile dans le maintien et la fusion du contenu existant et des configurations à partir des chemins d’accès `/apps` et `/libs` dans le référentiel. Pour les modifications apportées au chemin d’accès `/etc`, y compris les configurations Context Hub, il est souvent nécessaire de réappliquer ces modifications après la mise à niveau. Alors que la mise à niveau crée une copie de sauvegarde de toutes les modifications qui ne peuvent pas fusionner sous `/var`, nous vous recommandons de sauvegarder ces modifications manuellement avant le début de la mise à niveau.

## Générer le fichier quickstart.properties {#generate-quickstart-properties}

Lors du démarrage d’AEM depuis le fichier jar, un fichier `quickstart.properties` est généré sous `crx-quickstart/conf`. Si AEM a uniquement été démarré avec le script de démarrage dans le passé, ce fichier n’est pas présent et la mise à niveau échoue. Assurez-vous de vérifier l’existence de ce fichier et redémarrez AEM à partir du fichier jar s’il n’est pas présent.

## Configuration de la purge du workflow et du journal d’audit {#configure-wf-audit-purging}

Les tâches `WorkflowPurgeTask` et `com.day.cq.audit.impl.AuditLogMaintenanceTask` nécessitent des configurations OSGi distinctes et ne fonctionneront pas sans celles-ci. Si elles échouent lors de l’exécution de la tâche avant la mise à niveau, des configurations manquantes en sont la raison la plus probable. Par conséquent, veillez à ajouter des configurations OSGi pour ces tâches ou à les supprimer complètement de la liste des tâches d’optimisation avant la mise à niveau si vous ne souhaitez pas les exécuter. Vous trouverez la documentation relative à la configuration des tâches de purge des workflows dans la section [Administration des instances de workflow](/help/sites-administering/workflows-administering.md) et la configuration de la tâche de maintenance du journal d’audit dans la section [Maintenance du journal d’audit dans AEM 6](/help/sites-administering/operations-audit-log.md).

Pour la purge des workflows et des journaux d’audit sur CQ 5.6, ainsi que la purge des journaux d’audit sur AEM 6.0, reportez-vous à la section [Purge des nœuds de workflow et d’audit](https://helpx.adobe.com/fr/experience-manager/kb/howtopurgewf.html).

## Installation, configuration et exécution des tâches précédant la mise à niveau {#install-configure-run-pre-upgrade-tasks}

En raison du niveau de personnalisation accordé par AEM, il n’existe généralement pas de méthode uniforme pour effectuer les mises à niveau. Ainsi, la création d’une procédure normalisée pour les mises à niveau est un processus difficile.

Dans les versions précédentes, il était également difficile pour les mises à niveau d’AEM ayaqnt été arrêtées ou ayant échoué de reprendre en toute sécurité. Ce problème entraînait des situations où le redémarrage de la procédure de mise à niveau complète était nécessaire ou dans lesquelles des mises à niveau défectueuses étaient effectuées sans déclencher d’avertissement.

Pour résoudre ces problèmes, Adobe a ajouté plusieurs améliorations au processus de mise à niveau, le rendant plus résilient et plus convivial. Les tâches de maintenance préalables à la mise à niveau qui devaient auparavant être effectuées manuellement sont optimisées et automatisées. En outre, des rapports après la mise à niveau ont été ajoutés afin que le processus puisse être entièrement examiné dans l’espoir que les problèmes éventuels soient plus facilement détectés.

Les tâches de maintenance préalables à la mise à niveau sont actuellement réparties sur différentes interfaces, qui sont partiellement ou entièrement exécutées manuellement. L’optimisation de la maintenance avant la mise à niveau introduite dans AEM 6.3 permet de déclencher ces tâches de manière unifiée et d’examiner leur résultat à la demande.

Toutes les tâches incluses dans l’étape d’optimisation avant la mise à niveau sont compatibles avec toutes les versions à partir d’AEM 6.0.

### Méthode de configuration {#how-to-set-it-up}

Dans AEM version 6.3 et ultérieure, les tâches d’optimisation de la maintenance avant la mise à niveau sont incluses dans le fichier jar de démarrage rapide.

<!-- URLs below are all 404s. This content should probably be removed because it is entirely obsolete.

If you are upgrading from an older version of AEM 6, they are made available through separate packages that you can download from the Package Manager.

You can find the packages at these locations:

* [For upgrading from AEM 6.0](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq600/product/pre-upgrade-tasks-content-cq60)

* [For upgrading from AEM 6.1](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq610/product/pre-upgrade-tasks-content-cq61)

* [For upgrading from AEM 6.2](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq620/product/pre-upgrade-tasks-content-cq62) -->

### Utilisation {#how-to-use-it}

Le composant OSGi `PreUpgradeTasksMBean` est préconfiguré avec une liste de tâches de maintenance bénéficiant déjà de la mise à niveau, pouvant toutes être exécutées simultanément. Vous pouvez configurer les tâches en suivant la procédure ci-dessous :

1. Accédez à la console web en vous rendant sur *https://serveraddress:serverport/system/console/configMgr*.

1. Recherchez « **preupgradetasks** », puis cliquez sur le premier composant correspondant. Le nom complet du composant est `com.adobe.aem.upgrade.prechecks.mbean.impl.PreUpgradeTasksMBeanImpl`.

1. Modifiez la liste des tâches de maintenance devant être exécutées comme illustré ci-dessous :

   ![1487758925984](assets/1487758925984.png)

La liste des tâches varie en fonction du mode d’exécution utilisé pour démarrer l’instance. Vous trouverez ci-dessous une description du mode d’exécution pour lequel chaque tâche de maintenance est conçue.

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
   <td>Exécute un marquage et un balayage. Pour les magasins de données partagés, supprimez cette étape et exécutez<br /> manuellement ou préparez correctement les instances avant l’exécution.</td>
  </tr>
  <tr>
   <td><code>ConsistencyCheckTask</code></td>
   <td>crx2</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>WorkflowPurgeTask</code></td>
   <td>crx2/crx3</td>
   <td>Doit configurer la configuration OSGi de purge du workflow Granite d’Adobe avant l’exécution.</td>
  </tr>
  <tr>
   <td><code>GenerateBundlesListFileTask</code></td>
   <td>crx2/crx3</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>RevisionCleanupTask</code></td>
   <td>crx3</td>
   <td>Pour les instances TarMK sur AEM 6.0 à 6.2, exécutez manuellement le nettoyage des révisions hors ligne à la place.</td>
  </tr>
  <tr>
   <td><code>com.day.cq.audit.impl.AuditLogMaintenanceTask</code></td>
   <td>crx3</td>
   <td>Doit configurer la configuration OSGi du planificateur de purge du journal d’audit avant l’exécution.</td>
  </tr>
 </tbody>
</table>

>[!CAUTION]
>
>La `DataStoreGarbageCollectionTask` appelle l’opération de récupération de l’espace mémoire du magasin de données avec la phase de marquage et de balayage, le cas échéant. Pour les déploiements qui utilisent un magasin de données partagé, veillez à le reconfigurer correctement ou à préparer l’instance afin d’éviter la suppression des éléments référencés par une autre instance. Ce processus peut nécessiter l’exécution manuelle de la phase de marquage sur toutes les instances avant de déclencher cette tâche préalable à la mise à niveau.

### Configuration par défaut des contrôles de l’intégrité avant la mise à niveau {#default-configuration-of-the-pre-upgrade-health-checks}

Le composant OSGi `PreUpgradeTasksMBeanImpl` est préconfiguré avec une liste de balises de vérification de l’intégrité précédant la mise à niveau à exécuter lorsque la méthode `runAllPreUpgradeHealthChecks` est appelée :

* **système** : balise utilisée par les contrôles de l’intégrité de la maintenance Granite

* **avant la mise à niveau** : balise personnalisée qui peut être ajoutée à toutes les vérifications d’intégrité dont vous pouvez définir l’exécution avant une mise à niveau

La liste peut être modifiée. Vous pouvez utiliser les boutons plus **(+)** et moins **(-)** en plus des balises pour ajouter d’autres balises personnalisées ou supprimer les balises par défaut.

**Méthodes MBean**

La fonctionnalité Bean gérée est accessible à l’aide de la [console JMX](/help/sites-administering/jmx-console.md).

Vous pouvez accéder aux MBeans en procédant comme suit :

1. Accédez à la console JMX à l’adresse *https://serveraddress:serverport/system/console/jmx*.
1. Recherchez **PreUpgradeTasks** et cliquez sur le résultat.

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
   <td>Affiche la liste des noms des tâches de maintenance disponibles avant la mise à niveau.</td>
  </tr>
  <tr>
   <td><code>getAvailablePreUpgradeHealthChecksTagNames()</code></td>
   <td>INFO</td>
   <td>Affiche la liste des noms des balises de vérification d’intégrité avant la mise à niveau.</td>
  </tr>
  <tr>
   <td><code>runAllPreUpgradeTasks()</code></td>
   <td>ACTION</td>
   <td>Exécute toutes les tâches de maintenance avant la mise à niveau de la liste.</td>
  </tr>
  <tr>
   <td><code>runPreUpgradeTask(preUpgradeTaskName)</code></td>
   <td>ACTION</td>
   <td>Exécute la tâche de maintenance avant la mise à niveau avec le nom donné en tant que paramètre.</td>
  </tr>
  <tr>
   <td><code>isRunAllPreUpgradeTaskRunning()</code></td>
   <td>ACTION_INFO</td>
   <td>Vérifie si la tâche <code>runAllPreUpgradeTasksmaintenance</code> est en cours d’exécution.</td>
  </tr>
  <tr>
   <td><code>getAnyPreUpgradeTaskRunning()</code></td>
   <td>ACTION_INFO</td>
   <td>Vérifie si une tâche de maintenance avant la mise à niveau est en cours d’exécution et<br /> renvoie un tableau contenant les noms des tâches en cours d’exécution.</td>
  </tr>
  <tr>
   <td><code>getPreUpgradeTaskLastRunTime(preUpgradeTaskName)</code></td>
   <td>ACTION</td>
   <td>Affiche l’heure d’exécution exacte de la tâche de maintenance avant la mise à niveau avec le nom donné en tant que paramètre.</td>
  </tr>
  <tr>
   <td><code>getPreUpgradeTaskLastRunState(preUpgradeTaskName)</code></td>
   <td>ACTION</td>
   <td>Affiche le dernier état d’exécution de la tâche de maintenance avant la mise à niveau avec le nom donné en tant que paramètre.</td>
  </tr>
  <tr>
   <td><code>runAllPreUpgradeHealthChecks(shutDownOnSuccess)</code></td>
   <td>ACTION</td>
   <td><p>Exécute toutes les vérifications d’intégrité avant la mise à niveau et enregistre leur statut dans un fichier nommé <code>preUpgradeHCStatus.properties</code> situé sur le chemin d’accès Sling de l’accueil. Si le paramètre <code>shutDownOnSuccess</code> est défini sur <code>true</code>, l’instance AEM est arrêtée, mais uniquement lorsque toutes les vérifications d’intégrité avant la mise à niveau ont le statut « OK ».</p> <p>Le fichier de propriétés est utilisé comme prérequis pour toute mise à niveau ultérieure<br /> et le processus de mise à niveau est arrêté si l’exécution de la vérification de l’intégrité précédant la mise à niveau<br /> a échoué. Si vous souhaitez tout de même ignorer le résultat des vérifications d’intégrité<br /> avant la mise à niveau et lancer la mise à niveau, vous pouvez supprimer le fichier.</p> </td>
  </tr>
  <tr>
   <td><code>detectUsageOfUnavailableAPI(aemVersion)</code></td>
   <td>ACTION</td>
   <td>Répertorie tous les packages importés qui ne fonctionneront plus lors<br /> de la mise à niveau à la version d’AEM spécifiée. La version AEM cible doit être<br /> indiquée en tant que paramètre.</td>
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
>Cette étape est nécessaire uniquement si vous effectuez une mise à niveau à partir d’une version d’AEM 5. Elle peut être entièrement ignorée pour les mises à niveau à partir des versions plus anciennes à AEM 6.

La manière dont les modules de connexion `LoginModules` sont configurés pour l’authentification au niveau du référentiel a complètement changé dans Apache Oak.

Dans les versions d’AEM qui utilisaient CRX2, la configuration était placée dans le fichier `repository.xml` du référentiel alors qu’à partir de la version 6 et suivantes, cette opération est effectuée dans le service Apache Felix JAAS Configuration Factory via la console web.

En conséquence, toute configuration existante doit être désactivée et recréée pour Apache Oak après la mise à niveau.

Pour désactiver les modules personnalisés définis dans la configuration JAAS de `repository.xml`, vous devez modifier la configuration pour utiliser la valeur `LoginModule` par défaut, comme dans l’exemple suivant :

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
>Pour plus d’informations, consultez la section [Authentification avec le module de connexion externe](https://jackrabbit.apache.org/oak/docs/security/authentication/externalloginmodule.html).
>
>Pour un exemple de configuration de `LoginModule` dans AEM 6, consultez la section [Configuration de LDAP avec AEM 6](/help/sites-administering/ldap-config.md).

## Suppression des mises à jour du répertoire /install {#remove-updates-install-directory}

>[!NOTE]
>
>Supprimez uniquement les packages du répertoire crx-quickstart/install APRÈS avoir arrêté l’instance AEM. Cette étape est l’une des dernières avant de commencer la procédure de mise à niveau statique.

Supprimez tous les packs de services, les packs de fonctionnalités ou les correctifs logiciels qui ont été déployés via le répertoire `crx-quickstart/install` sur le système de fichiers local. Cela évite l’installation accidentelle d’anciens correctifs et packs de services en plus de la nouvelle version d’AEM une fois la mise à jour terminée.

## Arrêt de toutes les instances Cold Standby {#stop-tarmk-coldstandby-instance}

Si vous utilisez un secours différé TarMK, arrêtez tous les secours différés. Cela garantit un moyen efficace de revenir en ligne en cas de problèmes lors de la mise à niveau. Une fois la mise à niveau terminée, les secours différés doivent être reconstruits à partir des instances principales mises à niveau.

## Désactivation des tâches planifiées personnalisées {#disable-custom-scheduled-jobs}

Désactivez toutes les tâches OSGi planifiées incluses dans le code de votre application.

## Exécution d’un nettoyage des révisions hors ligne {#execute-offline-revision-cleanup}

>[!NOTE]
>
>Cette étape n’est nécessaire que pour les installations TarMK.

Si vous utilisez TarMK, vous devez exécuter le nettoyage des révisions hors ligne avant la mise à niveau. Cela permet à l’étape de migration du référentiel et aux tâches de mise à niveau suivantes de s’exécuter beaucoup plus rapidement et de garantir que le nettoyage des révisions en ligne peut s’exécuter correctement une fois la mise à niveau terminée. Pour plus d’informations sur l’exécution du nettoyage des révisions hors ligne, reportez-vous à la section [Exécution du nettoyage des révisions hors ligne](/help/sites-deploying/storage-elements-in-aem-6.md#performing-offline-revision-cleanup).

## Exécution de la récupération de l’espace mémoire du magasin de données {#execute-datastore-garbage-collection}

>[!NOTE]
>
>Cette étape n’est nécessaire que pour les instances exécutant crx3.

Après avoir exécuté le nettoyage des révisions sur les instances CRX3, vous devez exécuter la récupération de l’espace mémoire du magasin de données pour supprimer tous les objets blob non référencés dans le magasin de données. Pour obtenir des instructions, consultez la documentation sur la [récupération de l’espace mémoire du magasin de données](/help/sites-administering/data-store-garbage-collection.md).

## Mise à niveau du schéma de base de données si nécessaire {#upgrade-the-database-schema-if-needed}

En règle générale, la pile Apache Oak sous-jacente utilisée par AEM pour la persistance s’occupe de la mise à niveau du schéma de base de données, si nécessaire.

Cependant, il peut arriver que le schéma ne puisse pas être mis à niveau automatiquement. Il s’agit principalement d’environnements de sécurité élevée dans lesquels la base de données s’exécute sous un utilisateur ou une utilisatrice avec des privilèges limités. Lorsqu’un tel scénario se produit, AEM continue à utiliser l’ancien schéma.

Pour éviter qu’un tel scénario ne se produise, mettez à niveau le schéma en procédant comme suit :

1. Arrêtez l’instance AEM qui doit être mise à niveau.
1. Mettez à niveau le schéma de la base de données. Consultez la documentation relative au type de base de données pour savoir quels outils sont nécessaires pour obtenir le résultat.

   Pour plus d’informations sur la façon dont Oak gère les mises à niveau des schémas, consultez [cette page sur le site web d’Apache](https://jackrabbit.apache.org/oak/docs/nodestore/document/rdb-document-store.html#upgrade).

1. Continuez la mise à niveau d’AEM.

## Suppression des utilisateurs susceptibles d’entraver la mise à niveau {#delete-users-that-might-hinder-the-upgrade}

>[!NOTE]
>
>Cette tâche de maintenance avant la mise à niveau n’est nécessaire que si :
>
>* vous effectuez une mise à niveau à partir des versions d’AEM antérieures à AEM 6.3 ;
>* vous rencontrez les erreurs mentionnées ci-dessous lors de la mise à niveau.
>

Il existe des cas exceptionnels où les utilisateurs et utilisatrices du service peuvent se retrouver dans des versions AEM plus anciennes mal balisées en tant qu’utilisateurs ou utilisatrices standard.

Si un tel scénario se produit, la mise à niveau échoue avec un message similaire à celui-ci :

```
ERROR [Apache Sling Repository Startup Thread] com.adobe.granite.repository.impl.SlingRepositoryManager Exception in a SlingRepositoryInitializer, SlingRepository service registration aborted
java.lang.RuntimeException: Unable to create service user [communities-utility-reader]:java.lang.RuntimeException: Existing user communities-utility-reader is not a service user.
```

Pour contourner ce problème, procédez comme suit :

1. Désolidarisez l’instance du trafic d’exploitation.
1. Créez une sauvegarde d’un ou de plusieurs utilisateurs ou utilisatrices à l’origine du problème. Vous pouvez effectuer cette tâche à l’aide du gestionnaire de modules. Pour plus d’informations sur les packages, consultez la rubrique [Utilisation des packages](/help/sites-administering/package-manager.md).
1. Supprimez un ou plusieurs utilisateurs ou utilisatrices à l’origine du problème. Vous trouverez ci-dessous une liste d’utilisateurs qui peuvent appartenir à cette catégorie :

   1. `dynamic-media-replication`
   1. `communities-ugc-writer`
   1. `communities-utility-reader`
   1. `communities-user-admin`
   1. `oauthservice`
   1. `sling-scripting`

## Rotation des fichiers journaux {#rotate-log-files}

Nous vous recommande d’archiver vos fichiers journaux actuels avant de commencer la mise à niveau. Cela facilite la surveillance et l’analyse de vos fichiers journaux pendant et après la mise à niveau pour identifier et résoudre les problèmes qui peuvent surgir.
