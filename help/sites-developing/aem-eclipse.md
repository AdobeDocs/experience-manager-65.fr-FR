---
title: AEM Developer Tools for Eclipse
description: Découvrez les outils de développement Adobe Experience Manager pour Eclipse.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
exl-id: 00473769-c447-4966-a71e-117c669e0151
source-git-commit: b703f356f9475eeeafb1d5408c650d9c6971a804
workflow-type: tm+mt
source-wordcount: '792'
ht-degree: 98%

---

# Outils de développement AEM pour Eclipse{#aem-developer-tools-for-eclipse}

![Motif d’image circulaire pour AEM Developer Tools pour Eclipse.](do-not-localize/chlimage_1-9.png)

## Vue d’ensemble {#overview}

« AEM Developer Tools » est un plug-in Eclipse basé sur le [plug-in Eclipse pour Apache Sling](https://sling.apache.org/documentation/development/ide-tooling.html) disponible avec Apache License 2.

Il offre plusieurs fonctionnalités qui facilitent le développement d’AEM :

* Intégration transparente avec les instances AEM via Eclipse Server Connector.
* Synchronisation pour les bundles de contenu et d’OSGI
* Prise en charge du débogage avec fonctionnalité de remplacement de code à chaud.
* Bootstrap simple de projets AEM avec un assistant de création de projet spécifique.
* Modification facile des propriétés JCR.

## Conditions requises {#requirements}

Avant d’utiliser les outils de développement AEM, effectuez les étapes suivantes :

* Téléchargez et installez [Eclipse IDE pour les développeurs et développeuses Java™ EE](https://www.eclipse.org/downloads/packages/release/luna/r/eclipse-ide-java-ee-developers). Les outils de développement AEM prennent actuellement en charge Eclipse Kepler ou une version plus récente.

* Peut être utilisé avec AEM version 5.6.1 ou supérieure
* Configurez votre installation Eclipse pour vous assurer de disposer d’au moins 1 Go de mémoire de tas en modifiant votre fichier de configuration `eclipse.ini` de la manière décrite dans la [FAQ Eclipse](https://wiki.eclipse.org/FAQ_How_do_I_increase_the_heap_size_available_to_Eclipse%3F).

>[!NOTE]
>
>Sous macOS, cliquez avec le bouton droit sur **Eclipse.app**, puis sélectionnez **Afficher le contenu du package** pour rechercher votre `eclipse.ini`.

## Installation de AEM Developer Tools for Eclipse {#how-to-install-the-aem-developer-tools-for-eclipse}

Une fois les [conditions préalables](#requirements) ci-dessus réunies, vous pouvez installer le plug-in comme suit :

1. Accédez au site web **AEM Developer Tools** à l’adresse `https://eclipse.adobe.com/aem/dev-tools/`.

1. Copiez le **lien d’installation**.

   Notez que vous pouvez également télécharger une archive au lieu d’utiliser le lien d’installation. Cela permet l’installation hors ligne, mais les notifications de mise à jour automatiques ne sont alors pas activées.

1. Dans Eclipse, ouvrez le menu **Aide**.
1. Cliquez sur **Installer un nouveau logiciel**.
1. Cliquez sur **Add...** (Ajouter).
1. Dans le champ **Nom**, saisissez AEM Developer Tools.
1. Dans **Location** (Emplacement), copiez l’URL d’installation.
1. Cliquez sur **OK**.
1. Cochez les deux plug-ins **AEM** et **Sling**.
1. Cliquez sur **Next** (Suivant).
1. Cliquez sur **Suivant**.
1. Acceptez les contrats de licence et cliquez sur **Terminer**.
1. Cliquez sur **Oui** pour redémarrer Eclipse.

## Importation de projets existants {#how-to-import-existing-projects}

>[!NOTE]
>
>Consultez [Comment utiliser un bundle dans Eclipse quand il a été téléchargé depuis AEM](https://stackoverflow.com/questions/29699726/how-to-work-with-a-bundle-in-eclipse-when-it-was-downloaded-from-aem/29705407#29705407).

## La perspective AEM {#the-aem-perspective}

AEM Developer Tools for Eclipse est proposé avec une perspective offrant un contrôle total sur vos projets et instances AEM.

![chlimage_1-2](assets/chlimage_1-2a.jpeg)

## Exemple de projet multi-module {#sample-multi-module-project}

« AEM Developer Tools » contient un exemple de projet multi-module qui vous permet de vous familiariser rapidement avec la configuration d’un projet dans Eclipse. Considérez-le également comme un guide de bonnes pratiques pour plusieurs fonctionnalités d’AEM. [En savoir plus sur l’archétype du projet](https://github.com/adobe/aem-project-archetype).

Pour créer l’exemple de projet, procédez comme suit :

1. Dans le menu **Fichier** > **Nouveau** > **Projet**, accédez à la section **AEM** et sélectionnez **Exemple de projet multi-module AEM**.

   ![chlimage_1-69](assets/chlimage_1-69a.png)

1. Cliquez sur **Suivant**.

   >[!NOTE]
   >
   >Cette étape peut prendre un certain temps, car m2eclipse doit analyser les catalogues d’archétypes.

   ![chlimage_1-70](assets/chlimage_1-70a.png)

1. Choisissez **com.adobe.granite.archetypes : sample-project-archetype : (numéro le plus élevé)** dans le menu, puis cliquez sur **Suivant**.

   ![chlimage_1-71](assets/chlimage_1-71a.png)

1. Saisissez un **Nom**, un **ID de groupe** et un **ID d’artefact** pour l’exemple de projet. Vous pouvez également choisir de définir certaines propriétés avancées.

   ![chlimage_1-72](assets/chlimage_1-72a.png)

1. Configurez maintenant un serveur AEM auquel Eclipse peut se connecter.

   Pour utiliser la fonctionnalité de débogage, vous devez avoir démarré AEM en mode débogage, ce qui peut être réalisé, par exemple, en ajoutant ce qui suit à la ligne de commande :

   ```
       -nofork -agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=10123
   ```

   ![chlimage_1-73](assets/chlimage_1-73a.png)

1. Cliquez sur **Finish** (Terminer). La structure du projet est créée.

   >[!NOTE]
   >
   >Sur une nouvelle installation (plus précisément : si les dépendances Maven n’ont jamais été téléchargées), vous risquez de créer le projet avec des erreurs. Dans ce cas, suivez la procédure décrite dans la section [Résoudre une définition de projet non valide](#resolving-invalid-project-definition).

## Résolution des problèmes {#troubleshooting}

### Résolution d’une définition de projet non valide {#resolving-invalid-project-definition}

Pour résoudre des dépendances et une définition de projet non valides, procédez comme suit :

1. Sélectionnez tous les projets créés.
1. Faites un clic-droit. Dans le menu **Maven**, sélectionnez **Mettre à jour les projets**.
1. Cochez **Force Updates of Snapshot/Releases** (Forcer les mises à jour d’instantané/de versions).
1. Cliquez sur **OK**. Eclipse essaie de télécharger les dépendances demandées.

### Activer l’auto-remplissage de la bibliothèque de balises dans les fichiers JSP {#enabling-tag-library-autocompletion-in-jsp-files}

L’auto-remplissage de la bibliothèque de balises est prête à l’emploi, étant donné que les dépendances appropriées sont ajoutées au projet. Il existe un problème connu lors de l’utilisation de l’archive AEM Uber Jar, qui n’inclut pas les fichiers tld et TagExtraInfo nécessaires.

Pour contourner ce problème, assurez-vous que l’artefact org.apache.sling.scripting.jsp.taglib est présent dans le chemin d’accès aux classes avant l’archive AEM Uber Jar. Pour les projets Maven, placez la dépendance suivante dans le fichier pom.xml avant le fichier Uber Jar.

```xml
<dependency>
  <groupId>org.apache.sling</groupId>
  <artifactId>org.apache.sling.scripting.jsp.taglib</artifactId>
  <scope>provided</scope>
</dependency>
```

Assurez-vous d’ajouter la version appropriée pour votre déploiement d’AEM.

## Informations supplémentaires {#more-information}

Le site Web officiel Apache Sling IDE tooling for Eclipse fournit des informations utiles :

* Le [**guide d’utilisation Apache Sling IDE tooling for Eclipse**](https://sling.apache.org/documentation/development/ide-tooling.html) vous guide parmi les concepts généraux, l’intégration des serveurs et les fonctionnalités de déploiement pris en charge par AEM Development Tools.
* La section [Dépannage](https://sling.apache.org/documentation/development/ide-tooling.html#troubleshooting).
* La [liste des problèmes connus](https://sling.apache.org/documentation/development/ide-tooling.html#known-issues).

La documentation officielle [Eclipse](https://www.eclipse.org/) suivante peut vous aider à configurer votre environnement :

* [Prise en main d’Eclipse](https://eclipseide.org/getting-started/)
* [Système d’aide d’Eclipse Luna](https://help.eclipse.org/latest/index.jsp)
* [Intégration Maven (m2eclipse)](https://www.eclipse.org/m2e/)
