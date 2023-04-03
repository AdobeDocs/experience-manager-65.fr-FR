---
title: Modes d’exécution
seo-title: Run Modes
description: Découvrez comment régler votre instance AEM à des fins spécifiques à l’aide des modes d’exécution.
seo-description: Learn how to tune your AEM instance for specific purposes by using run modes.
uuid: 8a0c6e5c-4fae-43e2-b745-eee58f346ceb
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: 12329e26-40bc-4c94-bc60-6d9cbd01345f
feature: Configuring
exl-id: 6d03cb1d-500e-4a23-80e5-347a43dff30e
source-git-commit: 7d91fbdaae7ade27e9d6bf42bbcd5b16d3f6e358
workflow-type: tm+mt
source-wordcount: '747'
ht-degree: 51%

---

# Modes d’exécution{#run-modes}

Les modes d’exécution vous permettent d’ajuster votre instance AEM à des fins spécifiques. par exemple, auteur ou publication, test, développement, intranet ou autre.

Vous pouvez :

* [Définition de collections de paramètres de configuration pour chaque mode d’exécution](#defining-configuration-properties-for-a-run-mode).

   Un ensemble de paramètres de configuration de base est appliqué à tous les modes d’exécution, puis vous pouvez ajuster les ensembles ajoutés en fonction de l’objectif de votre environnement spécifique. Ils sont appliqués selon les besoins.

* [Définir des lots supplémentaires à installer pour un mode particulier](#defining-additional-bundles-to-be-installed-for-a-run-mode).

L’ensemble des paramètres et des définitions sont stockés dans le référentiel et activé en définissant le **mode d’exécution**.

## Modes d’exécution d’installation {#installation-run-modes}

Les modes d’exécution d’installation (ou fixes) sont utilisés lors de l’installation, puis restent fixes pendant toute la durée de vie de l’instance. Ils ne peuvent pas être modifiés.

Les modes d’exécution d’installation sont fournis prêts à l’emploi :

* `author`
* `publish`
* `samplecontent`
* `nosamplecontent`

Voici deux paires de modes d’exécution qui sont mutuellement exclusifs. Par exemple, vous pouvez :

* définir le mode `author` ou `publish`, mais pas les deux en même temps ;

* combiner le mode `author` au mode `samplecontent` ou `nosamplecontent` (mais pas aux deux).

>[!CAUTION]
>
>Lors de l’utilisation de l’un des modes d’exécution ci-dessus (author, publish, samplecontent, nosamplecontent), la valeur utilisée au moment de l’installation définit le mode d’exécution pour la variable *durée complète* de cette installation.
>
>Pour ces modes d’exécution : *cannot* modifiez-les après l’installation.

## Modes d’exécution personnalisés {#customized-run-modes}

Vous pouvez également créer vos propres modes d’exécution personnalisés. Elles peuvent être combinées pour couvrir des scénarios tels que :

* `author` + `development`

* `publish` + `test`

* `publish` + `test` + `golive`

* `publish` + `intranet`

* le cas échéant.

Les modes d’exécution personnalisés peuvent également être sélectionnés à chaque démarrage.

## Utilisation de samplecontent et nosamplecontent {#using-samplecontent-and-nosamplecontent}

Ces modes permettent de contrôler l’utilisation d’un exemple de contenu. L’exemple de contenu est défini avant la création du démarrage rapide et peut inclure des modules, des configurations, etc :

* Le mode d’exécution `samplecontent` (mode par défaut) installe ce contenu.

* Le mode d’exécution `nosamplecontent` n’installe pas l’échantillon de contenu.

Le mode d’exécution nosamplecontent est conçu pour les installations de production.

## Définition des propriétés de configuration pour un mode d’exécution {#defining-configuration-properties-for-a-run-mode}

Une collection de valeurs pour les propriétés de configuration, utilisée pour un mode d’exécution particulier, peut être enregistrée dans le référentiel.

Le mode d’exécution est indiqué par un suffixe sur le nom du dossier. Vous pouvez ainsi stocker toutes les configurations dans un seul référentiel sous la forme . Par exemple :

* `config`

   Applicable à tous les modes d’exécution

* `config.author`

   Utilisé pour le mode d’exécution auteur

* `config.publish`

   Utilisé pour le mode d’exécution de publication

* `config.<run-mode>`

   Utilisé pour le mode d’exécution applicable, par exemple « config »

Voir [Configuration OSGi dans le référentiel](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository) pour plus d’informations sur la définition des différents noeuds de configuration dans ces dossiers et sur la création de configurations pour des combinaisons de plusieurs modes d’exécution.

>[!NOTE]
>
>Pour [Modes d’exécution d’installation](#installation-run-modes) (auteur, par exemple) le mode d’exécution ne peut pas être modifié après l’installation. Toutefois, les modifications apportées aux propriétés de configuration individuelles prennent effet au redémarrage.

## Définition des lots supplémentaires à installer pour un mode d’exécution {#defining-additional-bundles-to-be-installed-for-a-run-mode}

Vous pouvez également spécifier des lots supplémentaires qui doivent être installés pour un mode d’exécution particulier. Pour ces définitions, les dossiers d’installation sont utilisés pour contenir les lots. Là aussi, le mode d’exécution est indiqué par un préfixe :

* `install.author`
* `install.publish`

Ces dossiers sont de type `nt:folder` et doivent contenir le lot approprié.

## Démarrage de CQ avec un mode d’exécution spécifique {#starting-cq-with-a-specific-run-mode}

Si vous avez défini des configurations pour plusieurs modes d’exécution, vous devez définir celle qui doit être utilisée au démarrage. Il existe plusieurs méthodes pour spécifier le mode d’exécution à utiliser. l’ordre de résolution est le suivant :

1. [Propriétés système (](#using-a-system-property-in-the-start-script)
1. [ ](#using-the-sling-properties-file)
1. [ ](#using-the-r-option)
1. [Détection du nom de fichier](#filename-detection-renaming-the-jar-file)

Lorsque vous utilisez un serveur d’application, vous pouvez également [définir le mode d’exécution dans web.xml](#defining-the-run-mode-in-web-xml-with-application-server).

### Utilisation du fichier sling.properties {#using-the-sling-properties-file}

Vous pouvez utiliser le fichier `sling.properties` pour définir le mode d’exécution requis :

1. Modifiez le fichier de configuration :

   `<cq-installation-dir>/crx-quickstart/conf/sling.properties`

1. Ajoutez les propriétés suivantes. L’exemple suivant concerne le mode d’exécution auteur :

   `sling.run.modes=author`

### Utilisation de l’option -r {#using-the-r-option}

Un mode d’exécution personnalisé peut être activé à l’aide de l’option `-r` lors du lancement du démarrage rapide. Par exemple, utilisez la commande ci-dessous pour lancer une instance AEM avec le mode d’exécution défini sur dev. ``

```shell
java -jar cq-56-p4545.jar -r dev
```

### Utilisation d’une propriété système dans le script de démarrage {#using-a-system-property-in-the-start-script}

Une propriété système dans le script de démarrage peut être utilisée pour spécifier le mode d’exécution.

* Par exemple, utilisez le code ci-dessous pour lancer une instance de publication d’exploitation localisée aux États-Unis :

   `-Dsling.run.modes=publish,prod,us`

### Détection de nom de fichier : attribution d’un nouveau nom au fichier JAR {#filename-detection-renaming-the-jar-file}

Les deux modes d’exécution d’installation ci-dessous peuvent être activés en renommant le fichier JAR d’installation avant l’installation :

* publication
* auteur

Le fichier jar doit utiliser la convention d’affectation des noms :

`cq5-<run-mode>-p<port-number>`

Par exemple, définissez le mode d’exécution `publish` en nommant le fichier JAR :

`cq5-publish-p4503`

### Définition du mode d’exécution dans web.xml (avec le serveur d’applications) {#defining-the-run-mode-in-web-xml-with-application-server}

Lorsque vous utilisez un serveur d’applications, vous pouvez également configurer la propriété :

`sling.run.modes`

dans le fichier :

`WEB-INF/web.xml`

Il se trouve dans le fichier `war` d’AEM et doit être mis à jour avant le déploiement.

Pour plus d’informations, consultez [Installation d’AEM avec un serveur d’application](/help/sites-deploying/application-server-install.md).
