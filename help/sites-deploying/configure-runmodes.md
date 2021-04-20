---
title: Modes d’exécution
seo-title: Modes d’exécution
description: Découvrez comment optimiser une instance AEM dans des buts précis en utilisant les modes d’exécution.
seo-description: Découvrez comment optimiser une instance AEM dans des buts précis en utilisant les modes d’exécution.
uuid: 8a0c6e5c-4fae-43e2-b745-eee58f346ceb
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: 12329e26-40bc-4c94-bc60-6d9cbd01345f
feature: Configuring
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '766'
ht-degree: 85%

---


# Modes d’exécution{#run-modes}

Les modes d’exécution permettent d’optimiser votre instance AEM pour des buts précis : par exemple, pour la création ou la publication, le test, le développement, un intranet ou à d’autres fins.

Vous pouvez :

* [Définir des collections de paramètres de configuration pour chaque mode d’exécution](#defining-configuration-properties-for-a-run-mode).

   Un ensemble de paramètres de configuration de base est appliqué à tous les modes d’exécution, puis vous pouvez ajuster les ensembles ajoutés en fonction de l’objectif de votre environnement spécifique. Ils sont appliqués au besoin.

* [Définir des lots supplémentaires à installer pour un mode spécifique](#defining-additional-bundles-to-be-installed-for-a-run-mode).

L’ensemble des paramètres et des définitions sont stockés dans le référentiel et activé en définissant le **mode d’exécution**.

## Modes d’exécution d’installation {#installation-run-modes}

Les modes d’exécution d’installation (ou fixes) sont utilisés lors de l’installation, puis restent fixes pendant toute la durée de vie de l’instance. Ils ne peuvent pas être modifiés.

Les modes d’exécution d’installation sont fournis prêts à l’emploi :

* `author`
* `publish`
* `samplecontent`
* `nosamplecontent`

Ce sont deux paires de modes d’exécution mutuellement exclusifs. Par exemple, vous pouvez :

* définissez `author` ou `publish`, mais pas les deux en même temps.

* combiner `author` avec `samplecontent` ou `nosamplecontent` (mais pas les deux)

>[!CAUTION]
>
>Lorsque vous utilisez l’un des modes d’exécution ci-dessus (author, publish, samplecontent, nosamplecontent), la valeur utilisée lors de l’installation définit le mode d’exécution pour *toute la durée de vie* de cette installation.
>
>Vous *ne pouvez pas* modifier ces modes d’exécution après l’installation.

## Modes d’exécution personnalisés {#customized-run-modes}

Vous pouvez également créer vos propres modes d’exécution personnalisés. Ils peuvent être combinés pour créer différents scénarios, par exemple :

* `author` + `development`

* `publish` +  `test`

* `publish` + `test` + `golive`

* `publish` +  `intranet`

* le cas échéant.

Les modes d’exécution personnalisés peuvent également être sélectionnés à chaque démarrage.

## Utilisation des modes samplecontent et nosamplecontent {#using-samplecontent-and-nosamplecontent}

Ces modes permettent de contrôler l’utilisation d’un échantillon de contenu. L’échantillon de contenu est défini avant que le démarrage rapide soit créé et peut comporter des modules, des configurations, etc. :

* Le mode d’exécution `samplecontent` (mode par défaut) installe ce contenu.

* Le mode d’exécution `nosamplecontent` n’installe pas l’échantillon de contenu.

Le mode d’exécution nosamplecontent est conçu pour les installations de production.

## Définition des propriétés de configuration d’un mode d’exécution  {#defining-configuration-properties-for-a-run-mode}

Une collection de valeurs pour les propriétés de configuration, utilisée pour un mode d’exécution spécifique, peut être enregistrée dans le référentiel.

Le mode d’exécution est indiqué par un suffixe ajouté au nom du dossier. Cela permet de stocker toutes les configurations dans un seul référentiel. Par exemple :

* `config`

   Applicable à tous les modes d’exécution

* `config.author`

   Utilisé pour le mode d’exécution Auteur

* `config.publish`

   Utilisé pour le mode d’exécution Publication

* `config.<run-mode>`

   Utilisé pour le mode d’exécution applicable, par exemple, config

Pour plus d’informations sur la définition des différents nœuds de configuration dans ces dossiers et sur la création de configurations pour des combinaisons de plusieurs modes d’exécution, voir [Configuration OSGi dans le référentiel](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository).

>[!NOTE]
>
>Pour les [modes d’exécution d’installation](#installation-run-modes) (author, par exemple), le mode d’exécution ne peut pas être modifié après l’installation. Cependant, les modifications apportées aux différentes propriétés de configuration seront appliquées au redémarrage.

## Définition de lots supplémentaires à installer pour un mode d’exécution  {#defining-additional-bundles-to-be-installed-for-a-run-mode}

Il est également possible de spécifier des lots supplémentaires à installer pour un mode d’exécution en particulier. Pour ces définitions, les dossiers d’installation sont utilisés pour contenir les lots. Là aussi, le mode d’exécution est indiqué par un préfixe :

* `install.author`
* `install.publish`

Ces dossiers sont de type `nt:folder` et doivent contenir le lot approprié.

## Démarrage de CQ avec un mode d’exécution spécifique {#starting-cq-with-a-specific-run-mode}

Si vous avez défini des configurations pour plusieurs modes d’exécution, vous devez définir celle à utiliser au démarrage. Différentes méthodes permettent de spécifier le mode d’exécution à utiliser. La séquence de résolution est la suivante :

1. [ `sling.properties` approuvé](#using-the-sling-properties-file)
1. [ `-r` option](#using-the-r-option)
1. [propriétés système (`-D`)](#using-a-system-property-in-the-start-script)

1. [Détection du nom de fichier](#filename-detection-renaming-the-jar-file)

Lorsque vous utilisez un serveur d’application, vous pouvez également [définir le mode d’exécution dans web.xml](#defining-the-run-mode-in-web-xml-with-application-server).

### Utilisation du fichier sling.properties {#using-the-sling-properties-file}

Vous pouvez utiliser le fichier `sling.properties` pour définir le mode d’exécution requis :

1. Modifiez le fichier de configuration :

   `<cq-installation-dir>/crx-quickstart/conf/sling.properties`

1. Ajoutez les propriétés suivantes ; l’exemple suivant est destiné à author :

   `sling.run.modes=author`

### Utilisation de l’option -r {#using-the-r-option}

Un mode d&#39;exécution personnalisé peut être activé à l&#39;aide de l&#39;option `-r` lors du lancement du démarrage rapide. Par exemple, utilisez la commande ci-dessous pour lancer une instance AEM avec le mode d’exécution défini sur dev. ``

```shell
java -jar cq-56-p4545.jar -r dev
```

### Utilisation d’une propriété système dans le script de démarrage {#using-a-system-property-in-the-start-script}

Une propriété système dans le script de démarrage peut être utilisée pour spécifier le mode d’exécution.

* Par exemple, utilisez les méthodes suivantes pour lancer une instance en tant qu’instance de publication de production située aux Etats-Unis :

   `-Dsling.run.modes=publish,prod,us`

### Détection de nom de fichier : attribution d’un nouveau nom au fichier JAR {#filename-detection-renaming-the-jar-file}

Les deux modes d&#39;exécution d&#39;installation suivants peuvent être activés en renommant le fichier JAR d&#39;installation avant l&#39;installation :

* publish
* Auteur 

Le fichier JAR doit suivre la convention de dénomination :

`cq5-<run-mode>-p<port-number>`

Par exemple, définissez le mode d’exécution `publish` en nommant le fichier JAR :

`cq5-publish-p4503`

### Définition du mode d’exécution dans le fichier web.xml (avec un serveur d’application) {#defining-the-run-mode-in-web-xml-with-application-server}

Lorsque vous utilisez un serveur d’application, vous pouvez également configurer la propriété :

`sling.run.modes`

dans le fichier :

`WEB-INF/web.xml`

Il se trouve dans le fichier `war` d’AEM et doit être mis à jour avant le déploiement.

Pour plus d’informations, voir [Installation d’AEM avec un serveur d’application](/help/sites-deploying/application-server-install.md).
