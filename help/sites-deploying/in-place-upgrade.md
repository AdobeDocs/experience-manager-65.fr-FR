---
title: Exécution d’une mise à niveau statique
seo-title: Exécution d’une mise à niveau statique
description: Découvrez comment effectuer une mise à niveau statique.
seo-description: Découvrez comment effectuer une mise à niveau statique.
uuid: 478cb9db-1ea8-4bdb-b333-411dcbf2d927
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: upgrading
discoiquuid: fcb17227-ff1f-4b47-ae94-6b7f60923876
docset: aem65
translation-type: tm+mt
source-git-commit: b8a532f45f531f36e04ff4b5f0cc2c9e729668bb
workflow-type: tm+mt
source-wordcount: '1275'
ht-degree: 80%

---


# Exécution d’une mise à niveau statique{#performing-an-in-place-upgrade}

>[!NOTE]
>
>Cette page décrit la procédure de mise à niveau pour AEM 6.5. Si une installation est déployée sur un serveur d’application, reportez-vous à la section [Procédure de mise à niveau pour les installations du serveur d’application](/help/sites-deploying/app-server-upgrade.md).

## Procédure pré-mise à niveau {#pre-upgrade-steps}

Avant d’effectuer la mise à niveau, différentes étapes doivent être exécutées. Pour plus d’informations, reportez-vous aux sections [Mise à niveau du code et personnalisations](/help/sites-deploying/upgrading-code-and-customizations.md) et [Tâches de maintenance pré-mise à niveau](/help/sites-deploying/pre-upgrade-maintenance-tasks.md). De plus, assurez-vous que le système répond à la configuration requise pour la nouvelle version d’AEM. Découvrez comment l’outil de détection des motifs peut vous aider à évaluer la complexité de votre mise à niveau. Pour plus d’informations, vous pouvez également consulter la section Portée et exigences de la mise à niveau de la rubrique [Planification de la mise à niveau](/help/sites-deploying/upgrade-planning.md).

<!--Finally, note that the downtime during the upgrade can be significally reduced by indexing the repository **before** performing the upgrade. For more information, see [Using Offline Reindexing To Reduce Downtime During an Upgrade](/help/sites-deploying/upgrade-offline-reindexing.md)-->

## Prérequis pour la migration {#migration-prerequisites}

* **Version Java minimale requise :** L’outil de migration ne fonctionne qu’avec Java 7 et version ultérieure. Notez que pour AEM 6.3, et versions ultérieures, l’environnement JRE 8 d’Oracle et les environnements JRE 7 et 8 d’IBM sont les seules versions prises en charge.

* **Instance mise à niveau :** si vous effectuez une mise à niveau d’une version **antérieure à la version 5.6**, assurez-vous que vous avez effectué une mise à niveau statique vers AEM 6.0 en suivant la procédure décrite dans la version 6.0 de la documentation de mise à niveau.

## Préparation du fichier jar de démarrage rapide AEM {#prep-quickstart-file}

1. Arrêtez l’instance si elle est en cours d’exécution.

1. Téléchargez le nouveau fichier JAR d’AEM et utilisez-le pour remplacer l’ancien en dehors du dossier `crx-quickstart`.

1. Décompressez le nouveau fichier jar de démarrage rapide en exécutant :

   ```shell
   java -Xmx4096m -jar aem-quickstart.jar -unpack
   ```

## Migration du référentiel de contenu {#content-repository-migration}

Cette migration n’est pas requise si vous effectuez une mise à niveau à partir d’AEM 6.3. Pour les versions antérieures à 6.3, Adobe fournit un outil qui permet de faire migrer le référentiel vers la nouvelle version du fichier Oak Segment Tar présente dans AEM 6.3. Fourni dans le cadre du module de démarrage rapide, cet outil est obligatoire pour toutes les mises à niveau qui utilisent TarMK. Les mises à niveau pour les environnements qui utilisent MongoMK n’impliquent pas de migrer le référentiel. Pour plus d’informations sur les avantages du nouveau format de fichier TAR Segment, reportez-vous à la section [Questions fréquentes sur la migration vers le fichier TAR d’Oak Segment](/help/sites-deploying/revision-cleanup.md#online-revision-cleanup-frequently-asked-questions).

The actual migration is performed using the standard AEM quickstart jar file, executed with a new `-x crx2oak` option which executes the crx2oak tool in order to simplify the upgrade and make it more robust.

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

Where `<<YOUR_PROFILE>>` and `<<ADDITIONAL_FLAGS>>` are replaced with the profile and flags listed in the following table:

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
   <td>Reportez-vous à la section Dépannage ci-dessous.</td>
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
   <td>Reportez-vous à la section Dépannage ci-dessous.</td>
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
   <td>Aucune migration n’est nécessaire</td>
   <td> </td>
  </tr>
 </tbody>
</table>

**Où :**

* `mongo-host` est l’adresse IP du serveur MongoDB (par exemple, 127.0.0.1).

* `mongo-port` est le port du serveur MongoDB (par exemple : mai 2017)

* `mongo-database-name` représente le nom de la base de données (par exemple : aem-author)

**Vous pouvez également avoir besoin de commutateurs supplémentaires pour les scénarios suivants :**

* If you are performing the upgrade on a Windows system where Java memory mapping is not handled correctly, please add the `--disable-mmap` parameter to the command.

* If you are using Java 7, add the `-XX:MaxPermSize=2048m` parameter just after the `-Xmx` parameter.

Pour plus d’informations sur l’utilisation de l’outil crx2oak, reportez-vous à la section [Utilisation de l’outil de migration CRX2Oak](/help/sites-deploying/using-crx2oak.md). Le fichier JAR auxiliaire de crx2oak peut être mis à niveau manuellement, si nécessaire, en le remplaçant manuellement par des versions récentes après la décompression du démarrage rapide. Son emplacement dans le dossier d’installation AEM est le suivant : `<aem-install>/crx-quickstart/opt/extensions/crx2oak.jar`. La dernière version de l’outil de migration CRX2Oak peut être téléchargée sur Adobe Repository, à l’adresse : [https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/crx2oak/](https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/crx2oak/)

Si la migration a réussi, l’outil quitte avec un code de sortie égal à 0. Cherchez également des messages AVERTISSEMENT et ERREUR dans le fichier `upgrade.log`, disponible sous `crx-quickstart/logs` dans le répertoire d’installation d’AEM, car ils peuvent indiquer des erreurs non fatales qui se sont produites lors de la migration.

Check the configuration files beneath `crx-quickstart/install` folder. Si une migration est nécessaire, ils sont mis à jour de manière à refléter le référentiel cible.

**Remarque sur magasins de données :**

Lorsque `FileDataStore` est la nouvelle valeur par défaut pour des installations AEM 6.3, l’utilisation d’un magasin de données externe n’est pas nécessaire. Même si les meilleures pratiques recommandent d’utiliser un magasin de données externe pour les déploiements en environnement de production, cela n’est pas un prérequis pour la mise à niveau. En raison de la complexité existante lors de la mise à niveau d’AEM, il est recommandé d’effectuer la mise à niveau sans migrer le magasin de données. Si vous le souhaitez, vous pouvez effectuer la migration du magasin de données séparément.

## Dépannage des problèmes de migration {#troubleshooting-migration-issues}

Veuillez ignorer cette section si vous effectuez une mise à niveau à partir de la version 6.3. Même si les profils crx2oak fournis doivent répondre aux besoins de la plupart des clients, des paramètres supplémentaires sont parfois nécessaires. Si une erreur se produit lors de la migration, certains aspects de l’environnement peuvent nécessiter des options de configuration supplémentaires. Si c’est le cas, l’erreur qui se produit est probablement la suivante :

**Les points de contrôle ne sont pas copiés, car aucun magasin de données externe n’a été spécifié. De ce fait, le référentiel sera entièrement réindexé au premier démarrage. Utilisez --skip-checkpoints pour forcer la migration ou reportez-vous à https://jackrabbit.apache.org/oak/docs/migration.html#Checkpoints_migration pour plus d’informations.**

Pour une raison quelconque, la procédure de migration doit accéder aux fichiers binaires du magasin de données et ne le trouve pas. In order to specify your datastore configuration, include the following flags in the `<<ADDITIONAL_FLAGS>>` portion of your migration command:

**Pour les magasins de données S3 :**

```shell
--src-s3config=/path/to/SharedS3DataStore.config --src-s3datastore=/path/to/datastore
```

Where `/path/to/SharedS3DataStore.config` represents the path to your S3 datastore config file and `/path/to/datastore` represents the path to your S3 datastore.

**Pour les magasins de données de fichier :**

```shell
--src-datastore=/path/to/datastore
```

Where `/path/to/datastore` represents the path to your File Datastore.

## Exécution de la mise à niveau {#performing-the-upgrade}

**Si vous utilisez S3 :**

1. Supprimez les fichiers JAR sous `crx-quickstart/install` associés à une version antérieure du connecteur S3.

1. Download the latest release of the 1.10.x S3 connector from [https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/com.adobe.granite.oak.s3connector/](https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/com.adobe.granite.oak.s3connector/)

1. Extract the package to a temporary folder and copy the contents of `jcr_root/libs/system/install` to the `crx-quickstart/install` folder.

### Détermination de la commande de démarrage de mise à niveau appropriée {#determining-the-correct-upgrade-start-command}

Pour effectuer la mise à niveau, il est important de démarrer AEM à l’aide du fichier JAR pour activer l’instance. For upgrading to 6.5, please also see other content restructuring and migration options in [Lazy Content Migration](/help/sites-deploying/lazy-content-migration.md) that you can choose with the upgrade command.

>[!IMPORTANT]
>
>Si vous exécutez Oracle Java 11 (ou en général les versions de Java ultérieures à la version 8), des modifications supplémentaires doivent être ajoutées à votre ligne de commande lors du démarrage d’AEM. Pour plus d’informations, voir Considérations [relatives à](/help/sites-deploying/custom-standalone-install.md#java-considerations)Java 11.

Notez que le démarrage d’AEM à partir du script de démarrage ne lance pas la mise à niveau. La plupart des clients démarrent AEM à l’aide du script de démarrage et ont personnalisé ce script de démarrage de manière à inclure des commutateurs pour les configurations d’environnement, comme les paramètres de mémoire, les certificats de sécurité, etc. Pour cette raison, il est recommandé de suivre cette procédure pour déterminer la commande de mise à niveau appropriée :

1. Sur une instance d’AEM en cours d’exécution, exécutez les opérations ci-dessous dans une ligne de commande :

   ```shell
   ps -ef | grep java
   ```

1. Recherchez le processus AEM. Il ressemblera à quelque chose comme :

   ```shell
   /usr/bin/java -server -Xmx1024m -XX:MaxPermSize=256M -Djava.awt.headless=true -Dsling.run.modes=author,crx3,crx3tar -jar crx-quickstart/app/cq-quickstart-6.2.0-standalone-quickstart.jar start -c crx-quickstart -i launchpad -p 4502 -Dsling.properties=conf/sling.properties
   ```

1. Modifiez la commande en remplaçant le chemin d’accès dans le fichier JAR existant (`crx-quickstart/app/aem-quickstart*.jar` dans ce cas) par le nouveau fichier JAR qui est un frère du dossier `crx-quickstart`. À l&#39;aide de notre commande précédente, nous prendrions la commande suivante :

   ```shell
   /usr/bin/java -server -Xmx1024m -XX:MaxPermSize=256M -Djava.awt.headless=true -Dsling.run.modes=author,crx3,crx3tar -jar cq-quickstart-6.5.0.jar -c crx-quickstart -p 4502 -Dsling.properties=conf/sling.properties
   ```

   Cela permet de s’assurer que tous les paramètres de mémoire appropriés, modes d’exécution personnalisés et autres paramètres d’environnement sont appliqués pour la mise à niveau. Une fois que la mise à niveau est terminée, l’instance peut être démarrée à partir du script de démarrage lors des démarrages ultérieurs.

## Déploiement de la base de code mise à niveau {#deploy-upgraded-codebase}

Une fois que la procédure de mise à niveau statique est terminée, la base de code mise à jour doit être déployé. La procédure de mise à jour de la base de code pour qu’elle fonctionne dans la version cible d’AEM est disponible dans la page [Mise à niveau du code et personnalisations](/help/sites-deploying/upgrading-code-and-customizations.md).

## Exécution des vérifications et du dépannage post-mise à niveau {#perform-post-upgrade-check-troubleshooting}

Reportez-vous à la section [Vérifications et dépannage post-mise à niveau](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md).
