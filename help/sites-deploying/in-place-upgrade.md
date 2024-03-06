---
title: Effectuer une mise à niveau statique
description: Découvrez comment effectuer une mise à niveau statique pour AEM 6.5.
topic-tags: upgrading
feature: Upgrading
exl-id: aef6ef00-993c-4252-b0ad-ddc4917beaf7
source-git-commit: 9d497413d0ca72f22712581cf7eda1413eb8d643
workflow-type: tm+mt
source-wordcount: '1214'
ht-degree: 82%

---

# Effectuer une mise à niveau statique{#performing-an-in-place-upgrade}

>[!NOTE]
>
>Cette page décrit la procédure de mise à niveau pour AEM 6.5. Si une installation est déployée sur un serveur d’applications, reportez-vous à la section [Procédure de mise à niveau pour les installations de serveur d’applications](/help/sites-deploying/app-server-upgrade.md).

## Étapes préalables à la mise à niveau {#pre-upgrade-steps}

Avant d’exécuter votre mise à niveau, plusieurs étapes doivent être réalisées. Voir [Mise à niveau du code et des personnalisations](/help/sites-deploying/upgrading-code-and-customizations.md) et [Tâches de maintenance avant la mise à niveau](/help/sites-deploying/pre-upgrade-maintenance-tasks.md) pour plus d’informations. Veillez également à ce que votre système réponde aux exigences de la nouvelle version d’AEM. Découvrez comment l’outil de détection des motifs peut vous aider à estimer la complexité de votre mise à niveau. Consultez également la section Portée et exigences de la mise à niveau de la [Planification de la mise à niveau](/help/sites-deploying/upgrade-planning.md) pour plus d’informations.

<!--Finally, the downtime during the upgrade can be significally reduced by indexing the repository **before** performing the upgrade. For more information, see [Using Offline Reindexing To Reduce Downtime During an Upgrade](/help/sites-deploying/upgrade-offline-reindexing.md)-->

## Conditions préalables à la migration {#migration-prerequisites}

* **Version Java minimale requise :** l’outil de migration ne fonctionne qu’avec les versions 7 et ultérieures de Java. Notez que pour AEM 6.3, et versions ultérieures, l’environnement JRE 8 d’Oracle et les environnements JRE 7 et 8 d’IBM sont les seules versions prises en charge.

* **Instance mise à niveau :** si vous mettez à niveau à partir d’une version **plus ancienne que 5.6**, vérifiez que vous avez effectué une mise à niveau statique vers AEM 6.0 en suivant la procédure décrite dans la version 6.0 de la documentation de mise à niveau.

## Préparation du fichier jar de démarrage rapide AEM {#prep-quickstart-file}

1. Arrêtez l’instance si elle est en cours d’exécution.

1. Téléchargez le nouveau fichier JAR d’AEM et utilisez-le pour remplacer l’ancien en dehors du dossier `crx-quickstart`.

1. Décompressez le nouveau fichier jar de démarrage rapide en exécutant :

   ```shell
   java -Xmx4096m -jar aem-quickstart.jar -unpack
   ```

## Migration du référentiel de contenu {#content-repository-migration}

Cette migration n’est pas requise si vous effectuez une mise à niveau à partir d’AEM 6.3. Pour les versions antérieures à la version 6.3, Adobe fournit un outil qui peut être utilisé pour migrer le référentiel vers la nouvelle version de Oak Segment Tar présent dans AEM 6.3. Il est fourni avec le module de démarrage rapide et est obligatoire pour toutes les mises à niveau qui utiliseront TarMK. Les mises à niveau pour les environnements qui utilisent MongoMK ne nécessitent pas de migration du référentiel. Pour plus d’informations sur les avantages du nouveau format Segment Tar, voir la section [Questions fréquentes sur la migration vers Oak Segment Tar](/help/sites-deploying/revision-cleanup.md#online-revision-cleanup-frequently-asked-questions).

La migration réelle est effectuée à l’aide du fichier jar de démarrage rapide standard d’AEM, exécuté avec une nouvelle `-x crx2oak` qui exécute l&#39;outil crx2oak pour simplifier la mise à niveau et la rendre plus robuste.

>[!NOTE]
>
>Si vous effectuez une migration du contenu du référentiel TarMK avec l’extension de démarrage rapide CRX2Oak, vous pouvez supprimer le mode d’exécution **samplecontent** en ajoutant la commande suivante à la ligne de commande de migration :
>
>* `--promote-runmode nosamplecontent`
>

Pour déterminer la commande à exécuter, utilisez la commande suivante :

```shell
java -Xmx4096m -jar aem-quickstart.jar -v -x crx2oak -xargs -- --load-profile <<YOUR_PROFILE>> <<ADDITIONAL_FLAGS>>
```

Où `<<YOUR_PROFILE>>` et `<<ADDITIONAL_FLAGS>>` sont remplacés par le profil et les indicateurs figurant dans le tableau suivant :

<table>
 <tbody>
  <tr>
   <td><strong>Référentiel source</strong></td>
   <td><strong>Référentiel cible</strong></td>
   <td><strong>Profil</strong></td>
   <td><strong>Indicateurs supplémentaires</strong><br /> </td>
  </tr>
  <tr>
   <td>crx2 ou TarMK avec <code>FileDataStore</code></td>
   <td>TarMK</td>
   <td>segment-fds</td>
   <td>Voir la section Dépannage ci-dessous.</td>
  </tr>
  <tr>
   <td>crx2</td>
   <td>MongoMK</td>
   <td>mongo-from-crx2 </td>
   <td><code>-T mongo-uri=mongo://mongo-host:mongo-port -T mongo-db=mongo-database-name</code></td>
  </tr>
  <tr>
   <td>TarMK ou crx2 avec <code>S3DataStore</code></td>
   <td>TarMK</td>
   <td>segment-custom-ds</td>
   <td>Voir la section Dépannage ci-dessous.</td>
  </tr>
  <tr>
   <td>TarMK sans magasin de données</td>
   <td>TarMK</td>
   <td>segment-no-ds</td>
   <td> </td>
  </tr>
  <tr>
   <td>MongoMK</td>
   <td>MongoMK</td>
   <td>Aucune migration n’est nécessaire.</td>
   <td> </td>
  </tr>
 </tbody>
</table>

**Où :**

* `mongo-host` correspond à l’IP du serveur MongoDB (par exemple, 127.0.0.1) ;

* `mongo-port` correspond au port du serveur MongoDB (par exemple, 27017) ;

* `mongo-database-name` représente le nom de la base de données (par exemple : aem-auteur).

**Vous pouvez également avoir besoin de commutateurs supplémentaires pour les scénarios suivants :**

* Si vous effectuez la mise à niveau sur un système Windows où le mappage de la mémoire Java n’est pas géré correctement, ajoutez le `--disable-mmap` à la commande.

Pour plus d’informations sur l’utilisation de l’outil crx2oak, voir Utilisation de l’[outil de migration CRX2Oak](/help/sites-deploying/using-crx2oak.md). Le fichier JAR d’assistance crx2oak peut être mis à niveau manuellement si nécessaire, en le remplaçant manuellement par des versions plus récentes après avoir décompressé le démarrage rapide. Son emplacement dans le dossier d’installation AEM est le suivant : `<aem-install>/crx-quickstart/opt/extensions/crx2oak.jar`. La dernière version de l’outil de migration CRX2Oak peut être téléchargée sur Adobe Repository, à l’adresse : [https://repo1.maven.org/maven2/com/adobe/granite/crx2oak/](https://repo1.maven.org/maven2/com/adobe/granite/crx2oak/)

Si la migration a réussi, l’outil quitte avec un code de sortie égal à 0. Cherchez également des messages AVERTISSEMENT et ERREUR dans le fichier `upgrade.log`, disponible sous `crx-quickstart/logs` dans le répertoire d’installation d’AEM, car ils peuvent indiquer des erreurs non fatales qui se sont produites lors de la migration.

Vérifiez les fichiers de configuration dans le dossier `crx-quickstart/install`. Si une migration était nécessaire, ceux-ci sont mis à jour pour refléter le référentiel cible.

**Remarque sur les magasins de données :**

Lorsque `FileDataStore` est la nouvelle valeur par défaut pour des installations AEM 6.3, l’utilisation d’un magasin de données externe n’est pas nécessaire. Bien que l’utilisation d’un magasin de données externe soit recommandée comme une bonne pratique pour les déploiements de production, il ne s’agit pas d’une condition préalable à la mise à niveau. En raison de la complexité déjà présente dans la mise à niveau d’AEM, Adobe recommande d’effectuer la mise à niveau sans effectuer de migration du magasin de données. Si vous le souhaitez, une migration d’un magasin de données peut être exécutée par la suite dans le cadre d’un effort distinct.

## Résolution des problèmes de migration {#troubleshooting-migration-issues}

Ignorez cette section si vous effectuez une mise à niveau depuis la version 6.3. Bien que les profils crx2oak fournis répondent aux besoins de la plupart des clients, des paramètres supplémentaires sont parfois nécessaires. Si vous rencontrez une erreur lors de la migration, il est possible que certains aspects de votre environnement nécessitent des options de configuration supplémentaires. Si tel est le cas, l’erreur suivante se produira probablement :

**Les points de contrôle ne sont pas copiés, car aucun entrepôt de données externe n’a été spécifié. Cela entraînera la réindexation complète du référentiel au premier démarrage. Utilisez --skip-checkpoints pour forcer la migration ou consultez https://jackrabbit.apache.org/oak/docs/migration.html#Checkpoints_migration pour en savoir plus.**

Pour une raison quelconque, le processus de migration doit accéder aux fichiers binaires dans le magasin de données et ne peut pas les trouver. Pour spécifier la configuration de votre banque de données, incluez les indicateurs suivants dans la variable `<<ADDITIONAL_FLAGS>>` partie de la commande de migration :

**Pour les magasins de données S3 :**

```shell
--src-s3config=/path/to/SharedS3DataStore.config --src-s3datastore=/path/to/datastore
```

Où `/path/to/SharedS3DataStore.config` représente le chemin d’accès au fichier de configuration de votre magasin de données S3, et `/path/to/datastore` représente le chemin d’accès à votre magasin de données S3.

**Pour les magasins de données de fichier :**

```shell
--src-datastore=/path/to/datastore
```

Où `/path/to/datastore` représente le chemin d’accès à votre magasin de données de fichier.

## Exécution de la mise à niveau {#performing-the-upgrade}

**Si vous utilisez S3 :**

1. Supprimez les fichiers JAR sous `crx-quickstart/install` associés à une version antérieure du connecteur S3.

1. Téléchargez la dernière version du connecteur S3 1.10.x sur [https://repo1.maven.org/maven2/com/adobe/granite/com.adobe.granite.oak.s3connector/](https://repo1.maven.org/maven2/com/adobe/granite/com.adobe.granite.oak.s3connector/).

1. Extrayez le package dans un dossier temporaire et copiez le contenu de `jcr_root/libs/system/install` dans le dossier `crx-quickstart/install`.

### Détermination de la commande de démarrage de mise à niveau appropriée {#determining-the-correct-upgrade-start-command}

Pour exécuter la mise à niveau, il est important de démarrer AEM à l’aide du fichier jar pour faire apparaître l’instance. Pour passer à la version 6.5, voir les autres options de migration et de restructuration de contenu dans [Migration différée du contenu](/help/sites-deploying/lazy-content-migration.md) que vous pouvez choisir avec la commande de mise à niveau.

>[!IMPORTANT]
>
>Si vous exécutez Oracle Java 11 (ou généralement des versions de Java plus récentes que 8), des commutateurs supplémentaires doivent être ajoutés à votre ligne de commande lors du démarrage de l’AEM. Pour plus d’informations, consultez la section [Considérations sur Java 11](/help/sites-deploying/custom-standalone-install.md#java-considerations).

Notez que le démarrage d’AEM à partir du script de démarrage ne lance pas la mise à niveau. La plupart des clients AEM à l’aide du script de démarrage et ont personnalisé ce script de démarrage afin d’inclure des commutateurs pour les configurations d’environnement telles que les paramètres de mémoire, les certificats de sécurité, etc. Pour cette raison, Adobe recommande de suivre cette procédure pour déterminer la commande de mise à niveau appropriée :

1. Sur une instance d’AEM en cours d’exécution, exécutez les opérations ci-dessous dans une ligne de commande :

   ```shell
   ps -ef | grep java
   ```

1. Recherchez le processus AEM. Le code se présente comme suit :

   ```shell
   /usr/bin/java -server -Xmx1024m -Djava.awt.headless=true -Dsling.run.modes=author,crx3,crx3tar -jar crx-quickstart/app/cq-quickstart-6.5.0-standalone-quickstart.jar start -c crx-quickstart -i launchpad -p 4502 -Dsling.properties=conf/sling.properties
   ```

1. Modifiez la commande en remplaçant le chemin d’accès dans le fichier JAR existant (`crx-quickstart/app/aem-quickstart*.jar` dans ce cas) par le nouveau fichier JAR qui est un frère du dossier `crx-quickstart`. Avec la commande précédente comme exemple, la commande serait la suivante :

   ```shell
   /usr/bin/java -server -Xmx1024m -Djava.awt.headless=true -Dsling.run.modes=author,crx3,crx3tar -jar cq-quickstart-6.5.0.jar -c crx-quickstart -p 4502 -Dsling.properties=conf/sling.properties
   ```

   Cela permet de s’assurer que tous les paramètres de mémoire appropriés, les modes d’exécution personnalisés et d’autres paramètres d’environnement sont appliqués pour la mise à niveau. Une fois la mise à niveau terminée, l’instance peut être lancée à partir du script de démarrage lors des prochains lancements.

## Déployer le base de code mise à niveau {#deploy-upgraded-codebase}

Une fois la mise à niveau statique terminée, la base de code mise à niveau doit être déployée. La procédure de mise à jour de la base de code pour qu’elle fonctionne dans la version cible d’AEM est disponible dans la page [Mise à niveau du code et personnalisations](/help/sites-deploying/upgrading-code-and-customizations.md).

## Effectuer les vérifications et le dépannage après la mise à niveau {#perform-post-upgrade-check-troubleshooting}

Voir [Vérifications et dépannage après une mise à niveau](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md).
