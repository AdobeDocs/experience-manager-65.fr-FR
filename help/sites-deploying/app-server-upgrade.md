---
title: Procédure de mise à niveau pour les installations de serveur d’applications
description: Découvrez comment mettre à niveau des instances AEM qui sont déployées par le biais de serveurs d’applications.
uuid: e4020966-737c-40ea-bfaa-c63ab9a29cee
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
discoiquuid: 1876d8d6-bffa-4a1c-99c0-f6001acea825
docset: aem65
feature: Mise à niveau
exl-id: 86dd10ae-7f16-40c8-84b6-91ff2973a523
source-git-commit: 69d960da90176058e8bb8b685325529e6cc10a31
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 68%

---

# Procédure de mise à niveau pour les installations de serveur d’applications{#upgrade-steps-for-application-server-installations}

Cette section décrit la procédure qui doit être suivie afin de mettre à jour AEM pour les installations de serveur d’applications.

Tous les exemples de cette procédure utilisent Tomcat comme serveur d’applications et impliquent que vous disposez d’une version de travail de AEM déjà déployée. La procédure est destinée à documenter les mises à niveau d’**AEM version 6.4 vers la version 6.5**.

1. D&#39;abord, début TomCat. Dans la plupart des cas, vous pouvez effectuer cette opération en exécutant le script de démarrage du début `./catalina.sh` en exécutant la commande suivante à partir du terminal :

   ```shell
   $CATALINA_HOME/bin/catalina.sh start
   ```

1. Si AEM 6.4 est déjà déployé, vérifiez que les lots fonctionnent correctement en accédant à :

   ```shell
   https://<serveraddress:port>/cq/system/console/bundles
   ```

1. Ensuite, annulez le déploiement AEM 6.4. Cela peut être fait à partir de TomCat App Manager (`http://serveraddress:serverport/manager/html`)

1. Désormais, migrez le référentiel à l’aide de l’outil de migration crx2oak. Pour ce faire, téléchargez la dernière version de crx2oak à partir de [cet emplacement](https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/crx2oak).

   ```shell
   SLING_HOME= $AEM-HOME/crx-quickstart java -Xmx4096m -XX:MaxPermSize=2048M -jar crx2oak.jar --load-profile segment-fds
   ```

1. Supprimez les propriétés requises du fichier sling.properties en procédant comme suit :

   1. Ouvrez le fichier situé dans `crx-quickstart/launchpad/sling.properties`.
   1. Supprimez les propriétés suivantes et enregistrez le fichier :

      1. `sling.installer.dir`

      1. `felix.cm.dir`

      1. `granite.product.version`

      1. `org.osgi.framework.system.packages`

      1. `osgi-core-packages`

      1. `osgi-compendium-services`

      1. `jre-*`

      1. `sling.run.mode.install.options`

1. Supprimez les fichiers et dossiers qui ne sont plus nécessaires. Vous devez précisément supprimer les éléments suivants :

   * Le **dossier launchpad/startup**. Vous pouvez le supprimer en exécutant la commande suivante dans le terminal :`rm -rf crx-quickstart/launchpad/startup`

   * Le fichier **base.jar** : `find crx-quickstart/launchpad -type f -name "org.apache.sling.launchpad.base.jar*" -exec rm -f {} \`

   * Le **fichier BootstrapCommandFile_timestamp.txt** : `rm -f crx-quickstart/launchpad/felix/bundle0/BootstrapCommandFile_timestamp.txt`

   * Supprimez **sling.options.file** en exécutant : `find crx-quickstart/launchpad -type f -name "sling.options.file" -exec rm -rf`

1. Créez à présent les entrepôts de nœuds et de données qui seront utilisés avec AEM 6.5. Pour ce faire, vous devez créer deux fichiers portant les noms suivants sous `crx-quickstart\install` :

   * `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.cfg`
   * `org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.cfg`

   Ces deux fichiers configureront AEM de façon à ce qu’ils utilisent un entrepôt de nœuds TarMK et un entrepôt de données File.

1. Modifiez les fichiers de configuration pour les rendre prêts à l’emploi. Plus précisément :

   * Ajoutez la ligne suivante à `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`:

      `customBlobStore=true`

   * Puis, ajoutez les lignes suivantes à `org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config`:

      ```
      path=./crx-quickstart/repository/datastore
      minRecordLength=4096
      ```

1. Vous pouvez maintenant modifier les modes d’exécution du fichier war d’AEM 6.5. Pour ce faire, créez tout d’abord un dossier temporaire qui héberge le fichier war d’AEM 6.5. Le nom du dossier dans cet exemple est `temp`. Une fois le fichier war copié, extrayez son contenu en exécutant la commande suivante depuis le dossier temp :

   ```
   jar xvf aem-quickstart-6.5.0.war
   ```

1. Une fois le contenu extrait, accédez au dossier **WEB-INF** et modifiez le fichier web.xml afin de modifier les modes d’exécution. Pour trouver l’emplacement où ils sont définis dans le fichier XML, recherchez la chaîne `sling.run.modes`. Une fois que vous l’avez trouvée, définissez les modes d’exécution sur la ligne de code suivante qui, par défaut, est définie sur author :

   ```bash
   <param-value >author</param-value>
   ```

1. Modifiez la valeur d’auteur ci-dessus et définissez les modes d’exécution sur : `author,crx3,crx3tar`. Le dernier bloc de code doit se présenter comme suit :

   ```
   <init-param>
   <param-name>sling.run.modes</param-name>
   <param-value>author,crx3,crx3tar</param-value>
   </init-param>
   <load-on-startup>100</load-on-startup>
   </servlet>
   ```

1. Créez à nouveau le fichier jar avec les contenus modifiés :

   ```bash
   jar cvf aem65.war
   ```

1. Enfin, déployez le nouveau fichier de guerre dans TomCat.
