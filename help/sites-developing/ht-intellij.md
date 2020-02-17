---
title: Développement de projets AEM à l’aide de IntelliJ IDEA
seo-title: Développement de projets AEM à l’aide de IntelliJ IDEA
description: Utilisation d’IntelliJ IDEA pour développer des projets AEM
seo-description: Utilisation d’IntelliJ IDEA pour développer des projets AEM
uuid: 382b5008-2aed-4e08-95be-03c48f2b549e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: df6410a2-794e-4fa2-ae8d-37271274d537
translation-type: tm+mt
source-git-commit: b3e1493811176271ead54bae55b1cd0cf759fe71

---


# Développement de projets AEM à l’aide de IntelliJ IDEA{#how-to-develop-aem-projects-using-intellij-idea}

## Présentation {#overview}

Pour commencer le développement d’AEM avec IntelliJ, procédez comme suit :

Chacune des étapes suivantes est expliquée plus en détail dans le reste de cette rubrique d’aide.

* Installation de IntelliJ
* Configuration du projet AEM basé sur Maven
* Préparation de la prise en charge des JSP pour IntelliJ dans le POM Maven
* Importation du projet Maven dans IntelliJ

>[!NOTE]
>
>Ce guide est basé sur IntelliJ IDEA Ultimate Edition 12.1.4 et AEM 5.6.1.

### Installation de IntelliJ IDEA {#install-intellij-idea}

Téléchargez IntelliJ IDEA depuis la page [des téléchargements de JetBrains](https://www.jetbrains.com/idea/download/index.html).

Puis, suivez les instructions d’installation de cette page.

### Configuration du projet AEM basé sur Maven {#set-up-your-aem-project-based-on-maven}

Next, set up your project using Maven as described in [How-To Build AEM Projects using Apache Maven](/help/sites-developing/ht-projects-maven.md).

To start working with AEM projects in IntelliJ IDEA, the basic setup in [Getting Started in 5 Minutes](https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html) is sufficient.

### Préparation de la prise en charge des JSP pour IntelliJ IDEA {#prepare-jsp-support-for-intellij-idea}

IntelliJ IDEA peut également fournir une aide pour l’utilisation des JSP, par exemple

* le renseignement automatique des bibliothèques de balises
* awareness of objects defined by `<cq:defineObjects />` and `<sling:defineObjects />`

For that to work, follow the instructions on [How-To Work with JSPs](/help/sites-developing/ht-projects-maven.md#how-to-work-with-jsps) in [How-To Build AEM Projects using Apache Maven](/help/sites-developing/ht-projects-maven.md).

### Importation du projet Maven {#import-the-maven-project}

1. Open the **Import** dialog in IntelliJ IDEA by

   * selecting **Import Project** on the welcome screen if you have no project open yet
   * selecting **File -> Import Project** from the main menu

1. Dans la boîte d’importation, sélectionnez le fichier POM du projet.

   ![chlimage_1-45](assets/chlimage_1-45a.png)

1. Continuez avec les paramètres par défaut comme indiqué dans la boîte de dialogue ci-dessous.

   ![chlimage_1-46](assets/chlimage_1-46a.png)

1. Continue through the following dialogs by clicking **Next** and **Finish**.
1. Vous êtes désormais prêt pour le développement d’AEM à l’aide de IntelliJ IDEA

   ![chlimage_1-47](assets/chlimage_1-47a.png)

### Débogage des JSP avec IntelliJ IDEA {#debugging-jsps-with-intellij-idea}

Les étapes suivantes sont requises pour le débogage des JSPs avec IntelliJ IDEA

* Configuration d’une facette Web dans le projet
* Installation du plugin de prise en charge de JSR45
* Configuration d’un profil de débogage
* Configuration d’AEM pour le mode débogage

#### Configuration d’une facette Web dans le projet {#set-up-a-web-facet-in-the-project}

IntelliJ IDEA doit comprendre où trouver les JSP pour débogage. Comme IDEA ne peut pas interpréter les paramètres `content-package-maven-plugin`, ils doivent être configurés manuellement.

1. Go to **File -> Project Structure**
1. Select the **Content** module
1. Click **+** above the list of modules and select **Web**
1. En tant que répertoire des ressources Web, sélectionnez le nom `content/src/main/content/jcr_root subdirectory` de votre projet comme illustré dans la capture d’écran ci-dessous.

![chlimage_1-48](assets/chlimage_1-48a.png)

#### Installation du plugin de prise en charge de JSR45 {#install-the-jsr-support-plugin}

1. Go to the **Plugins** pane in the IntelliJ IDEA settings
1. Navigate to the **JSR45 Integration** Plugin and select the check box next to it
1. Cliquez sur **Appliquer**
1. Redémarrez IntelliJ IDEA lorsque vous y êtes invité

![chlimage_1-49](assets/chlimage_1-49a.png)

#### Configuration d’un profil de débogage {#configure-a-debug-profile}

1. Go to **Run -> Edit Configurations**
1. Hit the **+** and select **JSR45 Remote**
1. In the configuration dialog, select **Configure** next to **Application Server** and configure a Generic server
1. Définissez la page de démarrage sur une URL appropriée si vous souhaitez ouvrir un navigateur lorsque vous commencez le débogage.
1. Remove all **Before launch** tasks if you use vlt autosync, or configure appropriate Maven tasks if you don&#39;t
1. On the **Startup/Connection** pane, adjust the port if required
1. Copiez les arguments de ligne de commande que IntelliJ IDEA propose

![chlimage_1-50](assets/chlimage_1-50a.png) ![chlimage_1-51](assets/chlimage_1-51a.png)

#### Configuration d’AEM pour le mode débogage {#configure-aem-for-debug-mode}

La dernière étape requise consiste à démarrer AEM avec les options JVM proposées par IntelliJ IDEA.

Vous pouvez réaliser cette opération en lançant le fichier jar AEM directement et en ajoutant ces options, par exemple avec la ligne de commande suivante :

`java -Xdebug -Xrunjdwp:transport=dt_socket,address=58242,suspend=n,server=y -Xmx1024m -XX:MaxPermSize=256M -jar cq-quickstart-5.6.1.jar`

Vous pouvez également ajouter ces options au script de démarrage dans `crx-quickstart/bin/start` comme indiqué ci-dessous.

```shell
# ...

# default JVM options
if [ -z "$CQ_JVM_OPTS" ]; then
 CQ_JVM_OPTS='-server -Xmx1024m -XX:MaxPermSize=256M -Djava.awt.headless=true'
fi

CQ_JVM_OPTS="$CQ_JVM_OPTS -Xdebug -Xrunjdwp:transport=dt_socket,address=58242,suspend=n,server=y"

# ...
```

#### Lancement du débogage {#start-debugging}

Vous êtes désormais prêt à déboguer les JSP dans AEM.

1. Select **Run -> Debug -> Your Debug Profile**
1. Définissez des points d’arrêt dans le code du composant
1. Accédez à une page du navigateur

![chlimage_1-52](assets/chlimage_1-52a.png)

### Débogage des lots avec IntelliJ IDEA {#debugging-bundles-with-intellij-idea}

Le code des lots peut être débogué à l’aide d’une connexion de débogage à distance générique standard. Vous pouvez consulter la [documentation Jetbrain sur le débogage à distance](https://www.jetbrains.com/idea/webhelp/run-debug-configuration-remote.html).
