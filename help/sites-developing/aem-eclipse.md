---
title: AEM Developer Tools for Eclipse
description: AEM Developer Tools for Eclipse
uuid: 566e49f2-6f28-4aa7-bfe0-b5f9675310bf
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: a2ae76a8-50b0-4e43-b791-ad3be25b8582
exl-id: 00473769-c447-4966-a71e-117c669e0151
source-git-commit: 4fd5e9a1bc603202ee52e85a1c09125b13cec315
workflow-type: tm+mt
source-wordcount: '788'
ht-degree: 62%

---

# AEM Developer Tools for Eclipse{#aem-developer-tools-for-eclipse}

![Motif d’image circulaire pour AEM Developer Tools for Eclipse.](do-not-localize/chlimage_1-9.png)

## Présentation {#overview}

&quot;AEM Developer Tools&quot; est un plug-in Eclipse basé sur la variable [Module externe Eclipse pour Apache Sling](https://sling.apache.org/documentation/development/ide-tooling.html) publié sous la licence Apache 2.

Il offre plusieurs fonctionnalités qui facilitent le développement d’AEM :

* Intégration transparente avec les instances AEM via Eclipse Server Connector.
* Synchronisation pour les bundles de contenu et d’OSGI
* Prise en charge du débogage avec fonctionnalité de remplacement de code à chaud.
* Démarrage simple de projets AEM par l’intermédiaire d’un assistant de création de projet spécifique.
* Modification facile des propriétés JCR.

## Conditions requises {#requirements}

Avant d’utiliser les outils de développement AEM, procédez comme suit :

* Télécharger et installer [Eclipse IDE pour les développeurs Java™ EE](https://www.eclipse.org/downloads/packages/release/luna/r/eclipse-ide-java-ee-developers). Les outils de développement AEM prennent actuellement en charge Eclipse Kepler ou une version plus récente.

* Peut être utilisé avec AEM version 5.6.1 ou supérieure
* Configurez l’installation d’Eclipse pour vous assurer de disposer d’au moins 1 Go de mémoire de segment en modifiant votre fichier de configuration `eclipse.ini` de la manière décrite dans les [questions fréquentes Eclipse](https://wiki.eclipse.org/FAQ_How_do_I_increase_the_heap_size_available_to_Eclipse%3F).

>[!NOTE]
>
>Sur macOS, cliquez avec le bouton droit de la souris **Eclipse.app**, puis sélectionnez **Afficher le contenu du module** pour rechercher votre `eclipse.ini`.

## Installation de AEM Developer Tools for Eclipse {#how-to-install-the-aem-developer-tools-for-eclipse}

Une fois les [conditions préalables](#requirements) ci-dessus réunies, vous pouvez installer le plug-in comme suit :

1. Parcourez les **AEM Outils de développement** site web `https://eclipse.adobe.com/aem/dev-tools/`.

1. Copiez le **lien d’installation**.

   Vous pouvez également télécharger une archive au lieu d’utiliser le lien d’installation. Cela permet l’installation hors ligne, mais les notifications de mise à jour automatiques ne sont pas visibles.

1. Dans Eclipse, ouvrez le menu **Aide**.
1. Cliquez sur **Installer un nouveau logiciel**.
1. Cliquez sur **Add...** (Ajouter).
1. Dans **Nom** saisissez AEM Outils de développement.
1. Dans **Location** (Emplacement), copiez l’URL d’installation.
1. Cliquez sur **OK**.
1. Cochez les plug-ins **AEM** et **Sling**.
1. Cliquez sur **Next** (Suivant).
1. Cliquez sur **Suivant**.
1. Acceptez les contrats de licence et cliquez sur **Terminer**.
1. Cliquez sur **Oui** pour redémarrer Eclipse.

## Importation de projets existants {#how-to-import-existing-projects}

>[!NOTE]
>
>Consultez [Comment utiliser un bundle dans Eclipse quand il a été téléchargé depuis AEM](https://stackoverflow.com/questions/29699726/how-to-work-with-a-bundle-in-eclipse-when-it-was-downloaded-from-aem/29705407#29705407).

## La perspective AEM {#the-aem-perspective}

Les outils de développement AEM d’Eclipse sont fournis avec une perspective qui vous offre un contrôle total sur vos projets et instances AEM.

![chlimage_1-2](assets/chlimage_1-2a.jpeg)

## Exemple de projet multi-module {#sample-multi-module-project}

Les &quot;outils de développement d’AEM&quot; incluent un exemple de projet multimodule qui vous permet de vous familiariser rapidement avec la configuration d’un projet dans Eclipse. Ils servent également de guide des bonnes pratiques pour plusieurs fonctionnalités AEM. [En savoir plus sur l’archétype du projet](https://github.com/adobe/aem-project-archetype).

Pour créer l’exemple de projet, procédez comme suit :

1. Dans le menu **Fichier** > **Nouveau** > **Projet**, accédez à la section **AEM** et sélectionnez **Exemple de projet multi-module AEM**.

   ![chlimage_1-69](assets/chlimage_1-69a.png)

1. Cliquez sur **Suivant**.

   >[!NOTE]
   >
   >Cette étape peut prendre un certain temps car m2eclipse doit analyser les catalogues de l’archétype.

   ![chlimage_1-70](assets/chlimage_1-70a.png)

1. Choisissez **com.adobe.granite.archetypes : sample-project-archetype : (numéro le plus élevé)** dans le menu, puis cliquez sur **Suivant**.

   ![chlimage_1-71](assets/chlimage_1-71a.png)

1. Remplissez un **Nom**, **Identifiant de groupe** et un **ID d’artefact** pour l’exemple de projet. Vous pouvez également choisir de définir certaines propriétés avancées.

   ![chlimage_1-72](assets/chlimage_1-72a.png)

1. Configurez maintenant un serveur AEM auquel Eclipse peut se connecter.

   Pour utiliser la fonction de débogueur, assurez-vous d’avoir commencé AEM en mode de débogage, ce qui peut être réalisé en ajoutant le code suivant à la ligne de commande :

   ```
       -nofork -agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=10123
   ```

   ![chlimage_1-73](assets/chlimage_1-73a.png)

1. Cliquez sur **Finish** (Terminer). La structure du projet est créée.

   >[!NOTE]
   >
   >Sur une nouvelle installation (plus précisément : si les dépendances Maven n’ont jamais été téléchargées), vous risquez de créer le projet avec des erreurs. Dans ce cas, suivez la procédure décrite à la section [Résolution d’une définition de projet non valide](#resolving-invalid-project-definition).

## Résolution des problèmes {#troubleshooting}

### Résolution d’une définition de projet non valide {#resolving-invalid-project-definition}

Pour résoudre des dépendances et une définition de projet non valides, procédez comme suit :

1. Sélectionnez tous les projets créés.
1. Faites un clic-droit. Dans le menu **Maven**, sélectionnez **Mettre à jour les projets**.
1. Cochez **Force Updates of Snapshot/Releases** (Forcer les mises à jour d’instantané/de versions).
1. Cliquez sur **OK**. Eclipse essaie de télécharger les dépendances demandées.

### Activation de la saisie semi-automatique de la bibliothèque de balises dans les fichiers JSP {#enabling-tag-library-autocompletion-in-jsp-files}

L’auto-remplissage de la bibliothèque de balises est prête à l’emploi, étant donné que les dépendances appropriées sont ajoutées au projet. Il existe un problème connu lors de l’utilisation de l’AEM Uber Jar, qui n’inclut pas les fichiers tld et TagExtraInfo nécessaires.

Pour contourner ce problème, assurez-vous que l’artefact org.apache.sling.scripting.jsp.taglib se trouve dans le chemin d’accès aux classes avant l’AEM Uber Jar. Pour les projets Maven, placez la dépendance suivante dans le fichier pom.xml avant le fichier Uber Jar.

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

* Le guide d’utilisation](https://sling.apache.org/documentation/development/ide-tooling.html) d’[**Apache Sling IDE tooling for Eclipse** vous guide parmi les concepts généraux, l’intégration des serveurs et les fonctionnalités de déploiement pris en charge par les outils de développement AEM.
* La section [Dépannage](https://sling.apache.org/documentation/development/ide-tooling.html#troubleshooting).
* La [liste des problèmes connus](https://sling.apache.org/documentation/development/ide-tooling.html#known-issues).

La documentation officielle [Eclipse](https://www.eclipse.org/) suivante peut vous aider à configurer votre environnement :

* [Prise en main d’Eclipse](https://eclipseide.org/getting-started/)
* [Système d’aide d’Eclipse Luna](https://help.eclipse.org/latest/index.jsp)
* [Intégration Maven (m2eclipse)](https://www.eclipse.org/m2e/)
