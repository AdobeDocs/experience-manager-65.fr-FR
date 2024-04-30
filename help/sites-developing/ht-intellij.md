---
title: Comment développer des projets AEM à l’aide d’IntelliJ IDEA
description: Découvrez comment utiliser IntelliJ IDEA pour développer des projets Adobe Experience Manager.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
exl-id: 5a79c79b-df65-4cb2-b9d4-eda994c992ec
solution: Experience Manager, Experience Manager Sites
feature: Developing,Developer Tools
role: Developer
source-git-commit: 305227eff3c0d6414a5ae74bcf3a74309dccdd13
workflow-type: tm+mt
source-wordcount: '640'
ht-degree: 100%

---

# Comment développer des projets AEM à l’aide d’IntelliJ IDEA{#how-to-develop-aem-projects-using-intellij-idea}

## Vue d’ensemble {#overview}

Pour commencer un développement AEM sur IntelliJ, les étapes suivantes sont nécessaires.

Chaque étape est expliquée en détail dans la suite de cette rubrique.

* Installer IntelliJ
* Configurer votre projet AEM basé sur Maven
* Préparer la prise en charge JSP pour IntelliJ dans le fichier POM Maven
* Importer le projet Maven dans IntelliJ

>[!NOTE]
>
>Ce guide est basé sur IntelliJ IDEA Ultimate Edition 12.1.4 et AEM 5.6.1.

### Installer IntelliJ IDEA {#install-intellij-idea}

Téléchargez IntelliJ IDEA à partir de [la page de téléchargements de JetBrains](https://www.jetbrains.com/idea/download/).

Suivez ensuite les instructions d’installation fournies dans cette page.

### Configurer votre projet AEM basé sur Maven {#set-up-your-aem-project-based-on-maven}

Ensuite, configurez le projet en utilisant Maven comme décrit à la rubrique [Création de projets AEM à l’aide d’Apache Maven](/help/sites-developing/ht-projects-maven.md).

Pour commencer à travailler sur des projets AEM dans IntelliJ IDEA, la configuration de base fournie dans la rubrique [Prise en main en 5 minutes](https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html) est suffisante.

### Préparer la prise en charge JSP pour IntelliJ IDEA {#prepare-jsp-support-for-intellij-idea}

IntelliJ IDEA peut également fournir une assistance sur l’utilisation de JSP, par exemple :

* le remplissage automatique des bibliothèques de balises ;
* la reconnaissance des objets définis par `<cq:defineObjects />` et `<sling:defineObjects />`.

Pour que cela fonctionne, suivez les instructions de la section [Comment travailler avec des JSP](/help/sites-developing/ht-projects-maven.md#how-to-work-with-jsps) de la rubrique [Création de projets AEM à l’aide d’Apache Maven](/help/sites-developing/ht-projects-maven.md).

### Importation du projet Maven {#import-the-maven-project}

1. Ouvrez la boîte de dialogue d’**importation** dans IntelliJ IDEA en

   * sélectionnant **Importer un projet** dans l’écran de bienvenue si aucun projet n’est ouvert ;
   * sélectionnant **Fichier -> Importer projet** dans le menu principal.

1. Dans la boîte d’importation, sélectionnez le fichier POM du projet.

   ![chlimage_1-45](assets/chlimage_1-45a.png)

1. Continuez avec les paramètres par défaut comme indiqué dans la boîte de dialogue ci-dessous.

   ![chlimage_1-46](assets/chlimage_1-46a.png)

1. Passez d’une boîte de dialogue à la suivante en cliquant sur **Suivant** et, dans la dernière, sur **Terminer**.
1. Vous êtes désormais prêt pour le développement d’AEM à l’aide d’IntelliJ IDEA.

   ![chlimage_1-47](assets/chlimage_1-47a.png)

### Déboguer des JSP avec IntelliJ IDEA {#debugging-jsps-with-intellij-idea}

Les étapes suivantes sont nécessaires pour déboguer des JSP avec IntelliJ IDEA.

* Configuration d’une facette web dans le projet
* Installation du plugin de prise en charge de JSR45
* Configuration d’un profil de débogage
* Configurer AEM pour le mode de débogage

#### Configuration d’une facette web dans le projet {#set-up-a-web-facet-in-the-project}

IntelliJ IDEA doit comprendre où trouver les JSP pour le débogage. Étant donné que IDEA ne peut pas interpréter les paramètres `content-package-maven-plugin`, il doit être configuré manuellement.

1. Accédez à **Fichier > Structure du projet**.
1. Sélectionnez le module **Content**.
1. Cliquez sur **+** au-dessus de la liste des modules et sélectionnez **Web**.
1. Sélectionnez le `content/src/main/content/jcr_root subdirectory` de votre projet en tant que répertoire de ressources web, comme illustré dans la capture d’écran ci-dessous.

![chlimage_1-48](assets/chlimage_1-48a.png)

#### Installation du plugin de prise en charge de JSR45 {#install-the-jsr-support-plugin}

1. Accédez au volet **Plug-ins** des paramètres IntelliJ IDEA.
1. Accédez au plugin **Intégration de JSR45** et cochez la case à côté de lui.
1. Cliquez sur **Appliquer**.
1. Redémarrez IntelliJ IDEA lorsque vous y êtes invité.

![chlimage_1-49](assets/chlimage_1-49a.png)

#### Configuration d’un profil de débogage {#configure-a-debug-profile}

1. Accédez à **Exécuter > Modifier les configurations**.
1. Appuyez sur **+** et sélectionnez **JSR45 à distance**.
1. Dans la boîte de configuration, sélectionnez **Configurer** en face de **Serveur d’applications** et configurez un serveur Générique.
1. Définissez la page de démarrage sur une URL appropriée si vous souhaitez ouvrir un navigateur lorsque vous commencez le débogage.
1. Supprimez toutes les tâches **Avant le lancement** si vous utilisez vlt autosync ou configurez les tâches Maven appropriées dans le cas contraire.
1. Dans le volet **Démarrage/Connexion**, modifiez le port, le cas échéant.
1. Copiez les arguments de ligne de commande proposés par IntelliJ IDEA.

![chlimage_1-50](assets/chlimage_1-50a.png) ![chlimage_1-51](assets/chlimage_1-51a.png)

#### Configurer AEM pour le mode de débogage {#configure-aem-for-debug-mode}

La dernière étape requise consiste à démarrer AEM avec les options JVM proposées par IntelliJ IDEA.

Lancez directement le fichier JAR d’AEM et ajoutez ces options, par exemple avec la ligne de commande suivante :

`java -Xdebug -Xrunjdwp:transport=dt_socket,address=58242,suspend=n,server=y -Xmx1024m -jar cq-quickstart-6.5.0.jar`

Vous pouvez également ajouter ces options au script de démarrage dans `crx-quickstart/bin/start` comme indiqué ci-dessous.

```shell
# ...

# default JVM options
if [ -z "$CQ_JVM_OPTS" ]; then
 CQ_JVM_OPTS='-server -Xmx1024m -Djava.awt.headless=true'
fi

CQ_JVM_OPTS="$CQ_JVM_OPTS -Xdebug -Xrunjdwp:transport=dt_socket,address=58242,suspend=n,server=y"

# ...
```

#### Démarrer le débogage {#start-debugging}

La configuration est à présent terminée pour le débogage de vos JSP dans AEM.

1. Sélectionnez **Exécuter -> Déboguer -> Votre profil de débogage**.
1. Définissez des points d’arrêt dans votre code de composant.
1. Accédez à une page dans votre navigateur.

![chlimage_1-52](assets/chlimage_1-52a.png)

### Débogage des lots avec IntelliJ IDEA {#debugging-bundles-with-intellij-idea}

Le code des lots peut être débogué à l’aide d’une connexion de débogage à distance générique standard. Vous pouvez suivre la [Documentation Jetbrain sur le débogage à distance](https://www.jetbrains.com/help/idea/remote-debugging-with-product.html#remote-interpreter).
