---
title: Déploiement et maintenance
seo-title: Déploiement et maintenance
description: Découvrez comment démarrer l’installation d’AEM.
seo-description: Découvrez comment démarrer l’installation d’AEM.
uuid: 4429ac4d-abd7-47d8-b19d-773accb7cc7a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: e48cc0ed-688c-44c8-b6d6-5f3c8593a295
docset: aem65
translation-type: tm+mt
source-git-commit: cb07e24b01084f57ad46615cb463ad5a0329c181
workflow-type: tm+mt
source-wordcount: '1833'
ht-degree: 79%

---


# Déploiement et maintenance{#deploying-and-maintaining}

Cette page contient les sections suivantes :

* [Concepts de base](#basic-concepts)

   * [Présentation d’AEM](#what-is-aem)
   * [Déploiements standards](#typical-deployment-scenarios)

      * [On-Premise](#on-premise)
      * [Managed Services utilisant Cloud Manager](#managed-services-using-cloud-manager)

* [Prise en main](#getting-started)

   * [Conditions préalables](#prerequisites)
   * [Obtention du logiciel](#getting-the-software)
   * [Installation locale par défaut](#default-local-install)
   * [Installations des instances de création et de publication](#author-and-publish-installs)
   * [Répertoire d’installation décompressé](#unpacked-install-directory)
   * [Démarrage et arrêt](#starting-and-stopping)

Une fois que vous serez familiarisé avec ces principes fondamentaux, vous pourrez lire des informations plus détaillées et avancées dans les pages secondaires suivantes :

* [Exigences techniques](/help/sites-deploying/technical-requirements.md)
* [Déploiements recommandés](/help/sites-deploying/recommended-deploys.md)
* [Installation autonome personnalisée](/help/sites-deploying/custom-standalone-install.md)
* [Installation du serveur d’applications](/help/sites-deploying/application-server-install.md)
* [Résolution des incidents](/help/sites-deploying/troubleshooting.md)
* [Début et arrêt d’AEM à partir de la ligne de commande](/help/sites-deploying/command-line-start-and-stop.md)
* [Configuration](/help/sites-deploying/configuring.md)
* [Mise à niveau vers AEM 6.5](/help/sites-deploying/upgrade.md)
* [Commerce électronique](/help/sites-deploying/ecommerce.md)
* [Articles sur la procédure de configuration](/help/sites-deploying/ht-deploy.md)
* [Console web](/help/sites-deploying/web-console.md)
* [Réplication de dépannage](/help/sites-deploying/troubleshoot-rep.md)
* [Bonnes pratiques](/help/sites-deploying/best-practices.md)
* [Déploiement des communautés](/help/communities/deploy-communities.md)
* [Introduction à la plateforme AEM](/help/sites-deploying/platform.md)
* [Instructions de performance](/help/sites-deploying/performance-guidelines.md)
* [Prise en main d’AEM Mobile](/help/mobile/getting-started-aem-mobile.md)
* [Présentation d’AEM Screens](https://docs.adobe.com/content/help/fr-FR/experience-manager-screens/user-guide/aem-screens-introduction.html)

## Concepts de base {#basic-concepts}

### Présentation d’AEM{#what-is-aem}

Adobe Experience Manager est un système client-serveur web qui permet de créer, de gérer et de déployer des sites web commerciaux et des services associés. Cette solution associe dans un seul package intégré plusieurs fonctions de niveau application et de niveau infrastructure.

Au niveau infrastructure, AEM fournit les éléments suivants :

* **Serveur d’applications web** : AEM peut être déployé en mode autonome (il comprend un serveur web Jetty intégré) ou en tant qu’application web au sein d’un serveur d’applications tiers.
* **Infrastructure d’application web** : AEM intègre l’infrastructure d’application web Sling qui simplifie l’écriture d’applications web REST orientées contenu.
* **Référentiel de contenu** : AEM comprend un référentiel de contenu Java (JCR). Il s’agit d’un type de base de données hiérarchique destiné aux données semi-structurées et non structurées. Le référentiel stocke le contenu affiché aux utilisateurs et l’ensemble du code, des modèles et des données internes utilisés par l’application.

Sur cette base, AEM propose également plusieurs fonctions de niveau application pour la gestion des éléments suivants :

* **Sites web**
* **Applications mobiles**
* **Publications numériques**
* **Formulaires**
* **Ressources numériques**
* **Communities**
* **Commerce en ligne**

Enfin, les clients peuvent utiliser ces blocs de construction de niveau application et de niveau infrastructure pour créer des solutions personnalisées en concevant leurs propres applications.

The AEM server is **Java-based** and runs on most operating systems that support that platform. All client interaction with AEM is done through a **web browser**.

### Scénarios de déploiement classique {#typical-deployment-scenarios}

Dans la terminologie AEM, une « instance » est une copie d’AEM s’exécutant sur un serveur. En règle générale, les installations d’AEM impliquent au moins deux instances qui s’exécutent généralement sur des ordinateurs distincts :

* **Création** : instance AEM utilisée pour créer, télécharger et modifier du contenu et assurer l’administration du site web. Une fois que le contenu est publié, il est répliqué sur l’instance de publication.
* **Publication** : instance AEM qui diffuse le contenu publié au public.

Ces instances sont identiques en termes de logiciels installés. Seule leur configuration diffère. La plupart des installations utilisent en outre un dispatcher :

* **Dispatcher** : serveur web statique (httpd Apache, Microsoft IIS, etc.) amélioré avec le module de dispatcher AEM. Ce module met en cache les pages web produites par l’instance de publication pour améliorer les performances.

Cette configuration comporte de nombreuses options et peut être élaborée de manière différente. Elle est toutefois au cœur de la plupart des déploiements. Nous commencerons par nous concentrer sur une configuration relativement simple. Nous aborderons ensuite les options de déploiement avancé.

Les sections suivantes décrivent les deux scénarios :

* **On-Premise** : AEM déployé et géré dans votre environnement d’entreprise.

* **Managed Services - Cloud Manager pour Adobe Experience Manager** : AEM déployé et géré par Adobe Managed Services.

### On-Premise {#on-premise}

Vous pouvez installer AEM sur des serveurs dans votre environnement d’entreprise. Les instances d’installation standard incluent les environnements de développement, de test et de publication. Reportez-vous à la section[ Prise en main](/help/sites-deploying/deploy.md#getting%20started) pour obtenir des informations de base sur la façon d’obtenir le logiciel AEM à installer en local.

Pour en savoir plus sur les déploiements On-Premise classiques, reportez-vous[ aux déploiements recommandés](/help/sites-deploying/recommended-deploys.md).

### Managed Services utilisant Cloud Manager {#managed-services-using-cloud-manager}

AEM Managed Services est une solution complète pour la gestion de l’expérience numérique. Il offre les avantages de la solution de diffusion d’expérience dans le cloud tout en conservant tous les avantages en termes de contrôle, de sécurité et de personnalisation d’un déploiement sur site. AEM Managed Services permet aux clients de se lancer plus rapidement en se déployant sur le cloud et en s’appuyant sur les meilleures pratiques et sur l’assistance technique d’Adobe. Les organisations et les utilisateurs professionnels peuvent engager les clients en un minimum de temps, générer des parts de marché et se concentrer sur la création de campagnes marketing innovantes tout en réduisant les charges informatiques.

Avec AEM Managed Services, les clients peuvent bénéficier des avantages suivants :

**Un délai de mise sur le marché plus rapide :** avec l’infrastructure cloud flexible d’Adobe Managed Services, les entreprises peuvent rapidement planifier, lancer et optimiser des expériences numériques réussies. Adobe gère l’architecture du cloud sans avoir besoin de capital, de matériel ou de logiciels supplémentaires et les ingénieurs de réussite client de l’Adobe, vous aident à concevoir AEM architecture, à configurer et à personnaliser la connexion aux applications dorsales et les meilleures pratiques de mise en service.

**Meilleures performances :** fournit des expériences numériques fiables pour votre entreprise avec quatre options de disponibilité du service : 99,5 %, 99,9 %, 99,95 % et 99,99 %. De plus, il permet des modèles de sauvegarde automatique et de reprise après sinistre multimode pour garantir la fiabilité et la gestion des situations d&#39;urgence.

**Coûts informatiques optimisés :** les conseils et l’expertise proactifs aident les organisations à rester à jour en ce qui concerne la dernière version d’AEM. Adobe Platinum Maintenance and Support est automatiquement inclus dans les nouveaux déploiements d’AMS Enterprise/Basic, offrant une expertise technique et une expérience opérationnelle pour aider les entreprises à gérer leurs applications critiques. Les fonctionnalités de base gratuites Analytics ou Target offrent une valeur ajoutée, en particulier pour les PME ayant des besoins limités en matière d’analyse et de personnalisation.

**Sécurité élevée :** garantit la sécurité physique, du réseau et des données au niveau de l’entreprise en hébergeant les applications clientes dans une installation à accès restreint, derrière des systèmes de pare-feu ou dans un cloud privé virtuel. Cela comprend des machines virtuelles à client unique avec un chiffrement du stockage des données, des antiviraux et une isolation des données.

**Cloud Manager :** composant de l’offre Managed Services d’Adobe Experience Manager, Cloud Manager est un portail en libre-service qui permet aux entreprises de gérer elles-mêmes Adobe Experience Manager dans le cloud. Il inclut un pipeline d’intégration et de distribution continues (CI/CD) qui permet aux équipes informatiques et aux partenaires d’implémentation d’accélérer la livraison de personnalisations ou de mises à jour sans compromettre les performances ou la sécurité. Cloud Manager est uniquement disponible pour les clients d’Adobe Managed Service.

Pour en savoir plus sur Cloud Manager et ses ressources, consultez le [**Guide de l’utilisateur Cloud Manager**](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html).

## Prise en main {#getting-started}

### Conditions préalables {#prerequisites}

While production instances are usually run on dedicated machines running an officially supported OS (see [Technical Requirements](/help/sites-deploying/technical-requirements.md)), the Experience Manager server will actually run on any system that supports [**Java Standard Edition 8**](https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).

Pour se familiariser avec AEM et développer sur AEM, il est courant d’utiliser une instance installée sur un ordinateur local exécutant Apple OS X ou les versions de bureau de Microsoft Windows ou Linux.

On the client-side, AEM works with all modern browsers (**Microsoft Edge**, **Internet Explorer** 11, **Chrome **51+** **, **Firefox **47+, **Safari** 8+) on both desktop and tablet operating systems. See [Supported Client Platforms](/help/sites-deploying/technical-requirements.md#supported-client-platforms) for details.

### Obtention du logiciel {#getting-the-software}

Customers with a valid maintenance and support contract should have received a mail notification with a code and be able to download AEM from the [**Adobe Licensing Website**](https://licensing.adobe.com/). Business partners can request download access from [**spphelp@adobe.com**](mailto:spphelp@adobe.com).

Le package logiciel AEM est disponible sous deux formes :

* **cq-quickstart-6.5.0.jar :** Un fichier *jar* exécutable autonome qui comprend tout ce qui est nécessaire pour être opérationnel.

* **cq-quickstart-6.5.0.war :** Fichier *war* à déployer sur un serveur d’applications tiers.

In the following section we describe the **standalone installation**. Pour plus d’informations sur l’installation d’AEM au sein d’un serveur d’applications, voir [Installation sur un serveur d’applications](/help/sites-deploying/application-server-install.md).

### Installation locale par défaut {#default-local-install}

1. Créez un répertoire d’installation sur votre ordinateur local. Par exemple :

   UNIX install location: **/opt/aem**

   Emplacement d&#39;installation de Windows : **`C:\Program Files\aem`**

   Il est aussi courant d’installer les exemples d’instance dans un dossier sur le bureau. Dans tous les cas, cet emplacement est défini de manière générique en tant que  :

   `<aem-install>`

   *Notez que le chemin d’accès au répertoire de fichiers doit comporter uniquement des caractères US-ASCII.*

1. Place the **jar** and **license **files in this directory:

   ```shell
   <aem-install>/
       cq-quickstart-6.5.0.jar
       license.properties
   ```

   If you do not provide a `license.properties` file, AEM will redirect your browser to a **Welcome** screen on startup, where you can enter a license key. Si vous ne disposez pas d’une clé de licence valide, vous devez en demander une à Adobe.

1. To start up the instance in a GUI environment, just double-click the **`cq-quickstart-6.5.0.jar`** file.

   Vous pouvez également lancer AEM à partir d’une ligne de commande. Pour une machine virtuelle JAVA 32 bits, saisissez la commande suivante :

   ```shell
       java -Xmx1024M -jar cq-quickstart-6.5.0.jar
   ```

   Pour une machine virtuelle 64 bits, saisissez la commande suivante :

   ```shell
       java -XX:MaxPermSize=256m -Xmx1024M -jar cq-quickstart-6.5.0.jar
   ```

AEM prend quelques minutes pour décompresser le fichier jar, s’installer et démarrer. Le résultat de la procédure ci-dessus est :

* instance de **création AEM**
* s’exécutant sur **localhost**
* sur le port **4502**

Pour accéder à l’instance, faites pointer le navigateur sur :

**`https://localhost:4502`**

L’instance de création est alors automatiquement configurée pour se connecter à une **instance de publication** sur **`localhost:4503`**.

### Installations des instances de création et de publication {#author-and-publish-installs}

L’installation par défaut (instance de **création** sur **`localhost:4502`**) peut être modifiée en renommant le fichier `jar` avant de le lancer pour la première fois. Le modèle de dénomination est :

**`cq-<instance-type>-p<port-number>.jar`**

Par exemple, renommer le fichier en

**`cq-author-p4502.jar`**

et le lancer entraîne l’exécution d’une instance de création sur **`localhost:4502`**.

De même, renommer le fichier en

**`cq-publish-p4503.jar`**

et le lancer entraîne l’exécution d’une instance de publication sur **`localhost:4503`**.

Vous installerez par exemple ces deux instances dans :

`<aem-install>/author`et

**`<aem-install>/publish`**

Pour plus d’informations sur la personnalisation de votre installation, reportez-vous aux sections suivantes :

* [Installation autonome personnalisée](/help/sites-deploying/custom-standalone-install.md)
* [Modes d’exécution](/help/sites-deploying/configure-runmodes.md)

### Répertoire d’installation décompressé {#unpacked-install-directory}

When the quickstart jar is launched for the first time it will unpack itself into the same directory under a new sub-directory called `crx-quickstart`. Vous devez obtenir le résultat suivant :

```xml
<aem-install>/
    license.properties
    cq-quickstart-6.5.0.jar
    crx-quickstart/
        app/
        bin/
        conf/
        launchpad/
        logs/
        metrics/
        monitoring/
        opt/
        repository/
        threaddumps/
        eula-de_DE.html
        eula-en_US.html
        eula-fr_FR.html
        eula-ja_JP.html
        readme.txt
```

Si l’instance a été installée à partir de l’interface utilisateur, une fenêtre de navigateur s’ouvre automatiquement et une fenêtre d’application de bureau s’ouvre, affichant également l’hôte et le port de l’instance ainsi qu’un commutateur on/off :

![écran de démarrage](assets/screen_shot_.png)

>[!NOTE]
>
>Si vous utilisez des liens symboliques, consultez la section sur les [problèmes liés aux liens symboliques](https://helpx.adobe.com/experience-manager/kb/changing-symlink.html).

### Starting and Stopping {#starting-and-stopping}

Une fois AEM décompressé et démarré pour la première fois, un double-clic sur le fichier jar dans le répertoire d’installation démarre l’instance. Celle-ci n’est pas réinstallée.

Pour arrêter l’instance dans l’interface utilisateur graphique, cliquez sur le bouton bascule **activé/désactivé** dans la fenêtre de l’application de bureau.

Vous pouvez également arrêter et démarrer AEM à partir d’une ligne de commande. Assuming you have already installed the instance for the first time, the **command-line scripts** are located here:

**`<aem-install>/crx-quickstart/bin/`**

Ce dossier contient les scripts shell bash Unix :

* **`start`**: Début de l’instance
* `stop`: Arrête l&#39;instance
* **`status`**: Signale l&#39;état de l&#39;instance
* **`quickstart`**: utilisé pour configurer les informations de démarrage, si nécessaire.

Il existe également des fichiers **`bat`** équivalents pour Windows. Pour plus d’informations, voir :

* [Début et arrêt d’AEM à partir de la ligne de commande](/help/sites-deploying/command-line-start-and-stop.md)

AEM démarre et redirige automatiquement le navigateur web vers la page adéquate. Il s’agit généralement de la page de connexion, par exemple :

`https://localhost:4502/`

![écran de connexion](assets/screen_shot_2019-04-08at83533am.png)

Une fois connecté, vous avez accès à AEM. Pour plus d’informations en fonction de votre rôle, reportez-vous aux sections suivantes :

* [Création  ](/help/sites-authoring/home.md)
* [Administration](/help/sites-administering/home.md)
* [Développement](/help/sites-developing/home.md)
* [Gestion](/help/managing/best-practices.md)

## Déploiement avancé {#advanced-deployment}

La section ci-dessus doit vous permettre de bien comprendre les principes fondamentaux d’une installation AEM. L’installation d’un système de production d’AEM peut toutefois être beaucoup plus complexe. Pour obtenir des informations pour une installation avancée, reportez-vous aux pages secondaires suivantes :

* [Exigences techniques](/help/sites-deploying/technical-requirements.md)
* [Déploiements recommandés](/help/sites-deploying/recommended-deploys.md)
* [Installation autonome personnalisée](/help/sites-deploying/custom-standalone-install.md)
* [Installation du serveur d’applications](/help/sites-deploying/application-server-install.md)
* [Résolution des incidents](/help/sites-deploying/troubleshooting.md)
* [Début et arrêt d’AEM à partir de la ligne de commande](/help/sites-deploying/command-line-start-and-stop.md)
* [Configuration](/help/sites-deploying/configuring.md)
* [Mise à niveau vers AEM 6.5](/help/sites-deploying/upgrade.md)
* [Commerce électronique](/help/sites-deploying/ecommerce.md)
* [Articles sur la procédure de configuration](/help/sites-deploying/ht-deploy.md)
* [Console web](/help/sites-deploying/web-console.md)
* [Réplication de dépannage](/help/sites-deploying/troubleshoot-rep.md)
* [Bonnes pratiques](/help/sites-deploying/best-practices.md)
* [Déploiement des communautés](/help/communities/deploy-communities.md)
* [Introduction à la plateforme AEM](/help/sites-deploying/platform.md)
* [Instructions de performance](/help/sites-deploying/performance-guidelines.md)
* [Prise en main d’AEM Mobile](/help/mobile/getting-started-aem-mobile.md)
* [Présentation d’AEM Screens](https://docs.adobe.com/content/help/fr-FR/experience-manager-screens/user-guide/aem-screens-introduction.html)
