---
title: AEM Developer Tools for Eclipse
description: Découvrez les outils de développement Adobe Experience Manager pour Eclipse.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
exl-id: 00473769-c447-4966-a71e-117c669e0151
solution: Experience Manager, Experience Manager Sites
feature: Developing,Developer Tools
role: Developer
source-git-commit: 5bd621b14e3bcd21431c1df5629fe4669b14052c
workflow-type: tm+mt
source-wordcount: '1216'
ht-degree: 39%

---


# Outils de développement AEM pour Eclipse {#aem-developer-tools-for-eclipse}

![Logo Outils de développement Experience Manager pour Eclipse](assets/eclipse-logo.png)

## Vue d’ensemble {#overview}

Les _outils de développement Experience Manager pour Eclipse_ sont un plug-in Eclipse basé sur le [plug-in Eclipse pour Apache Sling](https://sling.apache.org/documentation/development/ide-tooling.html) disponible avec Apache License 2.

Il offre plusieurs fonctionnalités qui facilitent le développement d’AEM :

* Intégration transparente avec les instances AEM via Eclipse Server Connector
* Synchronisation pour les bundles de contenu et d’OSGi
* Prise en charge du débogage avec fonctionnalité de remplacement de code à chaud
* Démarrage simple de projets AEM par l’intermédiaire d’un assistant de création de projet spécifique
* Modification facile des propriétés JCR

## Conditions requises {#requirements}

Avant d’utiliser AEM Developer Tools, vous devez :

* Téléchargez et installez [Eclipse IDE pour Enterprise Java et Web Developers.](https://www.eclipse.org/downloads/packages/)
   * La version 1.4.0 des outils de développement AEM pour Eclipse est compatible avec Eclipse 2022-12 (4.26) ou une version ultérieure et nécessite l’exécution de Java 17 ou une version ultérieure.
* Configurez votre installation Eclipse pour vous assurer de disposer d’au moins 1 Go de mémoire de tas en modifiant votre fichier de configuration `eclipse.ini` comme décrit dans la [FAQ Eclipse.](https://wiki.eclipse.org/FAQ_How_do_I_increase_the_heap_size_available_to_Eclipse%3F)

>[!NOTE]
>
>Sur macOS, vous devez cliquer avec le bouton droit de la souris sur **Eclipse.app**, puis sélectionner **Afficher le contenu du package** pour rechercher votre `eclipse.ini`.

## Comment installer AEM Developer Tools pour Eclipse {#how-to-install-the-aem-developer-tools-for-eclipse}

Lorsque vous avez rempli les [conditions requises](#requirements) ci-dessus, vous pouvez installer le plug-in des outils de développement comme suit :

1. Ouvrez le [site web AEM Developer Tools.](https://eclipse.adobe.com/)

1. Copiez le **lien d’installation**.

   * Vous pouvez également télécharger une archive au lieu d’utiliser le lien d’installation.
   * Cette méthode permet une installation hors ligne, mais vous ne recevez pas de notifications de mise à jour automatique.

1. Dans Eclipse, ouvrez le menu **Aide**.
1. Cliquez sur **Installer un nouveau logiciel**.
1. Cliquez sur **Add...** (Ajouter).
1. Dans le champ **Nom**, saisissez `AEM Developer Tools`.
1. Dans le champ **Emplacement**, copiez l’URL d’installation.
1. Cliquez sur **Add** (Ajouter).
1. Cochez les plug-ins **AEM** et **Sling**.
1. Cliquez sur **Next** (Suivant).
1. Dans la fenêtre **Détails de l’installation**, passez en revue les éléments à installer et cliquez de nouveau sur **Suivant**.
1. Acceptez les contrats de licence et cliquez sur **Finish** (Terminer).
1. Dans la boîte de dialogue **Autorités d’approbation** qui s’affiche, sélectionnez l’`https://eclipse.adobe.com` d’autorité/de site et cliquez sur **Approbation sélectionnée**.
1. Dans la boîte de dialogue **Artefacts d’approbation** qui s’affiche, sélectionnez les signataires de code et cliquez sur **Approbation sélectionnée**.
1. Cliquez sur **Redémarrer maintenant** pour redémarrer Eclipse.

## La perspective d’AEM {#the-aem-perspective}

Dans Eclipse, une **perspective** détermine les actions et les vues disponibles dans une fenêtre et permet une interaction axée sur les tâches avec les ressources. Pour plus d’informations sur les perspectives, consultez la [documentation Eclipse.](https://help.eclipse.org/latest/index.jsp).

Les _outils de développement Experience Manager pour Eclipse_ offrent une perspective AEM qui vous offre un contrôle total sur vos projets et instances AEM. Pour ouvrir la perspective AEM :

1. Dans la barre de menus Eclipse, sélectionnez **Fenêtre** > **Perspective** > **Ouvrir la perspective** > **Autre**.
1. Sélectionnez **AEM** dans la boîte de dialogue et cliquez sur **Ouvrir**.

![La perspective AEM dans Eclipse](assets/eclipse-aem-perspective.png)

## Exemple de projet multi-module {#sample-multi-module-project}

Les _outils de développement Experience Manager pour Eclipse_ sont fournis avec un exemple de projet multi-module qui vous permet de vous familiariser rapidement avec la configuration d’un projet dans Eclipse. Il sert également de guide des bonnes pratiques pour plusieurs fonctionnalités d’AEM, en tirant parti de l’[archétype de projet AEM.](https://github.com/adobe/aem-project-archetype)

Pour créer l’exemple de projet, procédez comme suit :

1. Dans le menu **Fichier** > **Nouveau** > **Projet**, accédez à la section **AEM** et sélectionnez **Exemple de projet multi-module AEM**.

   ![Exemple de projet multi-module AEM](assets/aem-sample-project.png)

1. Cliquez sur **Next** (Suivant).

   >[!NOTE]
   >
   >Cette étape peut prendre un certain temps, car [m2eclipse](https://eclipse.dev/m2e/) doit analyser les catalogues d’archétypes.

1. `com.adobe.aem : aem-project-archetype : <highest-number>` doit être sélectionné automatiquement dans la liste déroulante **Archétype**. Sélectionnez une version précédente, le cas échéant. Cliquez sur **Suivant**.

   ![Sélectionnez la version de l’archétype](assets/select-archetype.png)

1. Fournissez les champs suivants pour l’exemple de projet :

   * **Name** (Nom)
   * **Group Id** (ID de groupe)
   * **Artifact Id** (ID d’artefact)
   * **appId** : vous devrez peut-être développer les options **Advanced** (Avancé) pour définir cette valeur.
   * **appTitle** : vous devrez peut-être développer les options **Advanced** pour définir cette valeur.
   * **Package** : vous devrez peut-être développer les options **Advanced** pour définir cette valeur.

   ![Définition des propriétés d’archétype](assets/archetype-properties.png)

1. Cliquez sur **Next** (Suivant).

1. Configurez un serveur AEM auquel Eclipse se connecte en sélectionnant **Configurer un nouveau serveur** et en fournissant un nom de serveur et les informations de connexion nécessaires.

   ![Connexion au serveur AEM](assets/connect-server.png)

   * Pour utiliser la fonctionnalité de débogage, vous devez démarrer AEM en mode débogage en fournissant le paramètre `-agentlib`, par exemple :

   ```text
   $ java -agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=*:5005 -jar aem-author-p4502.jar
   ```

   >[!TIP]
   >
   >Pour plus d’informations sur le débogage de votre projet s’exécutant sur un SDK AEM local, consultez le document [&#x200B; Débogage à distance du SDK AEM &#x200B;](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-sdk/remote-debugging).

1. Cliquez sur **Finish** (Terminer).

La structure du projet est créée. Le téléchargement des artefacts nécessaires au projet peut prendre un certain temps.

>[!NOTE]
>
>Lors d’une nouvelle installation ou lorsque les dépendances Maven n’ont pas été téléchargées précédemment, Eclipse peut signaler que le projet a été créé avec des erreurs. Dans ce cas, suivez la procédure décrite dans la section [Résolution d’une définition de projet non valide](#resolving-invalid-project-definition).

## Comment importer des projets existants {#how-to-import-existing-projects}

Utilisez la fonction **Nouveau projet** pour créer la structure de projet de base.

1. Suivez les instructions pour créer un [exemple de projet multi-module](#sample-multi-module-project) qui crée une structure de projet de base avec une séparation saine des préoccupations :

   * `PROJECT.ui.apps` pour le contenu `/apps` et `/etc`
   * `PROJECT.ui.content` pour le `/content` qui est créé
   * `PROJECT.core` pour les lots Java
   * `PROJECT.it.launcher` et `PROJECT.it.tests` pour les tests d’intégration

1. Remplacez le contenu de votre projet `PROJECT.ui.apps` par les dossiers `apps` et `etc` de votre package :

   1. Dans le panneau **Explorateur de projets**, développez `PROJECT.ui.apps` > `src` > `main` > `content` > `jcr_root` > `apps`.
   1. Cliquez avec le bouton droit sur le dossier `apps` et choisissez **Afficher dans** > **Explorateur système**.
   1. Supprimez les dossiers `apps` et `etc`.
   1. Au même emplacement, placez les dossiers `apps` et `etc` de votre package de contenu.
   1. Dans Eclipse, cliquez avec le bouton droit sur le projet `PROJECT.ui.apps` et sélectionnez **Actualiser**.

1. Faites ensuite de même pour `PROJECT.ui.content` et remplacez son dossier de contenu par celui de vos packages :

   1. Dans le panneau **Explorateur de projets**, développez `PROJECT.ui.content` > `src` > `main` > `content` > `jcr_root` > `content`.
   1. Cliquez avec le bouton droit sur le dossier de contenu le plus profond et sélectionnez **Afficher dans** > **Explorateur système**.
   1. Supprimez le dossier de contenu à cet endroit.
   1. Placez le dossier de contenu de votre package de contenu au même emplacement.
   1. Dans Eclipse, cliquez avec le bouton droit sur le projet `PROJECT.ui.content` et sélectionnez **Actualiser**.

1. Mettez à jour les fichiers `filter.xml` de ces deux projets pour qu’ils correspondent au contenu de votre package de contenu en ouvrant le fichier `META-INF/vault/filter.xml` de votre package de contenu dans un éditeur de texte/code distinct.

   * Voici un exemple de l’aspect que peut avoir votre fichier `filter.xml` :

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <workspaceFilter version="1.0">
       <filter root="/apps/foo"/>
       <filter root="/apps/foundation/components/bar"/>
       <filter root="/etc/designs/foo"/>
       <filter root="/content/foo"/>
       <filter root="/content/dam/foo"/>
       <filter root="/content/usergenerated/content/foo"/>
   </workspaceFilter>
   ```

1. En ce qui concerne le contenu de votre package qui a été divisé en deux projets, vous devez également diviser ces règles de filtrage en deux et mettre à jour les fichiers `filter.xml` des deux projets en conséquence.

   1. Dans Eclipse, ouvrez `PROJECT.ui.apps/src/main/content/META-INF/filter.xml`.
   1. Remplacez le contenu de l’élément `<workspaceFilter>` par les règles de votre package qui commencent par `/apps` et `/etc`.
      * Par exemple :

        ```xml
        <?xml version="1.0" encoding="UTF-8"?>
        <workspaceFilter version="1.0">
           <filter root="/apps/foo"/>
           <filter root="/apps/foundation/components/bar"/>
           <filter root="/etc/designs/foo"/>
        </workspaceFilter>
        ```

   1. Ouvrez ensuite `PROJECT.ui.content/src/main/content/META-INF/filter.xml`.
   1. Remplacez les règles par celles de votre package qui commencent par `/content`.
      * Par exemple :

        ```xml
        <?xml version="1.0" encoding="UTF-8"?>
        <workspaceFilter version="1.0">
           <filter root="/content/foo"/>
           <filter root="/content/dam/foo"/>
           <filter root="/content/usergenerated/content/foo"/>
        </workspaceFilter>
        ```

1. Veillez à enregistrer toutes vos modifications. Vous pouvez désormais synchroniser ce nouveau contenu avec votre instance AEM.

1. Dans le panneau **Serveurs**, assurez-vous que la connexion est démarrée, et si oui, ne la démarrez pas.

1. Cliquez sur l’icône **Nettoyer et publier**.

Une fois cette opération terminée, votre package doit s’exécuter sur votre instance. Lors de l’enregistrement, toute modification est automatiquement synchronisée dans l’instance.

Si vous souhaitez recréer un package à partir de votre projet, cliquez avec le bouton droit de la souris sur le `PROJECT.ui.apps` ou le `PROJECT.ui.content`, puis sélectionnez **Exécuter en tant que** > **Installation Maven**.

Vous disposez désormais d’un dossier cible contenant votre package (nommé par exemple `PROJECT.ui.apps-0.0.1-SNAPSHOT.zip`).

## Résolution des problèmes {#troubleshooting}

### Résolution d’une définition de projet non valide {#resolving-invalid-project-definition}

Pour résoudre des dépendances et une définition de projet non valides, procédez comme suit :

1. Sélectionnez tous les projets créés.
1. Faites un clic-droit.
1. Dans le menu contextuel, sélectionnez **Maven** > **Mettre à jour les projets**.
1. Cochez **Force Updates of Snapshot/Releases** (Forcer les mises à jour d’instantané/de versions).
1. Cliquez sur **OK**.

Eclipse télécharge les dépendances requises. Cela peut prendre un moment.

## Informations supplémentaires {#more-information}

Le site web officiel Apache Sling IDE tooling for Eclipse fournit des informations supplémentaires utiles :

* Le guide d’utilisation [**Apache Sling IDE tooling for Eclipse** &#x200B;](https://sling.apache.org/documentation/development/ide-tooling.html) vous guide parmi les concepts généraux, l’intégration des serveurs et les fonctionnalités de déploiement pris en charge par les outils de développement AEM.
* [Résolution des problèmes liés à l’outil IDE Apache Sling](https://sling.apache.org/documentation/development/ide-tooling.html#troubleshooting)
* [Liste des problèmes connus](https://sling.apache.org/documentation/development/ide-tooling.html#known-issues)

La documentation officielle [Eclipse](https://www.eclipse.org/) suivante peut vous aider à configurer votre environnement :

* [Prise en main d’Eclipse](https://eclipseide.org/getting-started/)
* [Système d’aide d’Eclipse Luna](https://help.eclipse.org/latest/index.jsp)
* [Intégration Maven (m2eclipse)](https://www.eclipse.org/m2e/)
