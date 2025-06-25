---
title: Déploiement et maintenance
description: Découvrez comment commencer à installer AEM.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
docset: aem65
exl-id: 3df0662a-0768-4b56-8b94-c517657b4bd9
solution: Experience Manager, Experience Manager Sites
feature: Deploying
role: Admin
source-git-commit: f96b178ae84b4b930b59e36d4994970682c53dbd
workflow-type: ht
source-wordcount: '1779'
ht-degree: 100%

---

# Déploiement et maintenance {#deploying-and-maintaining}

Dans cette page, vous trouverez les éléments suivants :

* [Concepts de base](#basic-concepts)

   * [Qu’est-ce qu’AEM ?](#what-is-aem)
   * [Déploiements standards](#typical-deployment-scenarios)

      * [On-Premise](#on-premise)
      * [Managed Services utilisant Cloud Manager](#managed-services-using-cloud-manager)

* [Prise en main](#getting-started)

   * [Prérequis](#prerequisites)
   * [Obtention du logiciel](#getting-the-software)
   * [Installation locale par défaut](#default-local-install)
   * [Installation des instances d’auteur et de publication](#author-and-publish-installs)
   * [Répertoire d’installation décompressé](#unpacked-install-directory)
   * [Démarrer et arrêter](#starting-and-stopping)

Une fois que vous serez à l’aise avec ces principes fondamentaux, vous pourrez lire des informations plus détaillées et avancées dans les pages secondaires suivantes :

* [Exigences techniques](/help/sites-deploying/technical-requirements.md)
* [Déploiements recommandés](/help/sites-deploying/recommended-deploys.md)
* [Installation autonome personnalisée](/help/sites-deploying/custom-standalone-install.md)
* [Installation du serveur d’applications](/help/sites-deploying/application-server-install.md)
* [Résolution des problèmes](/help/sites-deploying/troubleshooting.md)
* [Début et arrêt d’AEM à partir de la ligne de commande](/help/sites-deploying/command-line-start-and-stop.md)
* [Configuration](/help/sites-deploying/configuring.md)
* [Mise à niveau vers AEM 6.5](/help/sites-deploying/upgrade.md)
* [eCommerce](/help/commerce/cif-classic/deploying/ecommerce.md)
* [Articles sur la procédure de configuration](/help/sites-deploying/ht-deploy.md)
* [Console web](/help/sites-deploying/web-console.md)
* [Résolution des problèmes liés à la réplication](/help/sites-deploying/troubleshoot-rep.md)
* [Bonnes pratiques](/help/sites-deploying/best-practices.md)
* [Déploiement de Communities](/help/communities/deploy-communities.md)
* [Introduction à la plateforme AEM](/help/sites-deploying/platform.md)
* [Instructions de performance](/help/sites-deploying/performance-guidelines.md)
* [Prise en main d’AEM Mobile](/help/mobile/getting-started-aem-mobile.md)
* [Qu’est-ce qu’AEM Screens ?](https://experienceleague.adobe.com/docs/experience-manager-screens/user-guide/aem-screens-introduction.html?lang=fr)

## Concepts de base {#basic-concepts}

### Qu’est-ce qu’AEM ? {#what-is-aem}

Adobe Experience Manager est un système client-serveur web qui permet de créer, de gérer et de déployer des sites web commerciaux et des services associés. Cette solution associe dans un seul package intégré plusieurs fonctions de niveau application et de niveau infrastructure.

Au niveau de l’infrastructure, AEM fournit les éléments suivants :

* **Serveur d’applications web** : AEM peut être déployé en mode autonome (il comprend un serveur web Jetty intégré) ou en tant qu’application web au sein d’un serveur d’applications tiers.
* **Infrastructure d’application web** : AEM intègre le framework d’application web Sling, qui simplifie l’écriture d’applications web RESTful orientées contenu.
* **Référentiel de contenu** : AEM comprend un référentiel de contenu Java™ (JCR), un type de base de données hiérarchique conçu spécifiquement pour les données non structurées et semi-structurées. Le référentiel stocke non seulement le contenu destiné à l’utilisateur ou à l’utilisatrice, mais également l’ensemble du code, des modèles et des données internes utilisés par l’application.

Sur cette base, AEM propose également un certain nombre de fonctionnalités au niveau de l’application pour la gestion des éléments suivants :

* **Sites Web**
* **Applications mobiles**
* **Publications numériques**
* **Formulaires et documents**
* **Ressources numériques**
* **Communities**
* **Commerce en ligne**

Enfin, les clientes et clients peuvent utiliser ces infrastructures et blocs de création de niveau application pour créer des solutions personnalisées en concevant leurs propres applications.

Le serveur AEM est **basé sur Java** et s’exécute sous la plupart des systèmes d’exploitation qui prennent en charge cette plateforme. Toutes les interactions client avec AEM passent par un **navigateur Web**.

>[!NOTE]
>
>Les fonctionnalités d’AEM Forms, telles que les formulaires adaptatifs, disponibles dans AEM 6.5 QuickStart, sont uniquement destinées à des fins d’exploration et d’évaluation. Pour une utilisation à des fins de production, il est essentiel d’obtenir une licence valide pour AEM Forms, car la fonctionnalité de formulaires adaptatifs nécessite une licence appropriée.

### Scénarios de déploiement standard {#typical-deployment-scenarios}

Dans la terminologie AEM, une « instance » est une copie d’AEM exécutée sur un serveur. Les installations AEM impliquent généralement au moins deux instances, souvent exécutées sur des machines distinctes :

* **Création** : instance AEM utilisée pour créer, télécharger et modifier du contenu et assurer l’administration du site web. Une fois que le contenu est publié, il est répliqué sur l’instance de publication.
* **Publication** : instance AEM qui diffuse le contenu publié au public.

Ces instances sont identiques en termes de logiciel installé. Elles se différencient uniquement par leur configuration. En outre, la plupart des installations utilisent un Dispatcher :

* **Dispatcher** : serveur web statique (Apache httpd, Microsoft® IIS, etc.) augmenté avec le module de Dispatcher AEM. Ce module met en cache les pages Web produites par l’instance de publication pour améliorer les performances.

Il existe de nombreuses options avancées et des variantes de cette configuration, mais le modèle de base de création, de publication et de Dispatcher est au cœur de la plupart des déploiements. Commençons par nous concentrer sur une configuration simple. Nous aborderons ensuite les options de déploiement avancé.

Les sections suivantes décrivent les deux scénarios :

* **On-Premise** : instance AEM déployée et gérée dans votre environnement d’entreprise.

* **Managed Services - Cloud Manager pour Adobe Experience Manager** : AEM déployé et géré par Adobe Managed Services.

### On-Premise {#on-premise}

Vous pouvez installer AEM sur des serveurs dans votre environnement d’entreprise. Les instances d’installation standard incluent les environnements de développement, de test et de publication. Reportez-vous à [Prise en main](/help/sites-deploying/deploy.md#getting%20started) pour obtenir des informations de base sur la façon d’obtenir le logiciel AEM à installer en local.

Pour en savoir plus sur les déploiements On-Premise standard, reportez-vous à [Déploiements recommandés](/help/sites-deploying/recommended-deploys.md).

### Managed Services avec Cloud Manager {#managed-services-using-cloud-manager}

AEM Managed Services est une solution complète pour la gestion de l’expérience digitale. Elle offre les avantages de la solution de diffusion d’expérience dans le cloud tout en conservant tous les avantages en termes de contrôle, de sécurité et de personnalisation d’un déploiement On-Premise. AEM Managed Services permet aux clients de se lancer plus rapidement en se déployant sur le cloud et en s’appuyant sur les meilleures pratiques et sur l’assistance technique d’Adobe. Les entreprises et les utilisateurs et utilisatrices professionnel(le)s peuvent impliquer leurs clientes et clients dans un laps de temps minimal, accroître leur part de marché et se concentrer sur la création de campagnes marketing innovantes tout en réduisant la charge sur les services informatiques.

Avec AEM Managed Services, les clientes et clients peuvent bénéficier des avantages suivants :

**Un délai de mise sur le marché plus rapide :** avec l’infrastructure cloud flexible d’Adobe Managed Services, les entreprises peuvent rapidement planifier, lancer et optimiser des expériences numériques réussies. Adobe gère l’architecture cloud sans autre investissement en capital, matériel ou logiciel, et les ingénieur(e)s des solutions clientes Adobe contribuent à l’architecture AEM, la configuration, la personnalisation pour la connexion aux applications back-end et les bonnes pratiques de mise en production.

**De meilleures performances** : fournit des expériences numériques fiables pour votre entreprise avec quatre options de disponibilité du service : 99,5 %, 99,9 %, 99,95 % et 99,99 %. De plus, elle permet des modèles de sauvegarde automatique et de reprise sur sinistre multimodes pour assurer la fiabilité et la gestion des imprévus.

**Des coûts informatiques optimisés :** la proactivité des conseils et de l’expertise aide les organisations à toujours disposer de la dernière version d’AEM. Adobe Platinum Maintenance and Support est automatiquement inclus dans les nouveaux déploiements d’AMS Enterprise/Basic, offrant une expertise technique et une expérience opérationnelle pour aider les entreprises à gérer leurs applications critiques. Les fonctionnalités de base gratuites d’Analytics ou de Target offrent une valeur supplémentaire, en particulier pour les moyennes entreprises ayant des besoins limités en matière d’analyse et de personnalisation.

**Des niveaux de sécurité élevés :** garantit la sécurité physique, du réseau et des données au niveau de l’entreprise en hébergeant les applications clientes dans une installation à accès restreint, derrière des systèmes de pare-feu ou dans un cloud privé virtuel. Ils comprennent des machines virtuelles à client(e) unique avec un chiffrement de stockage des données, des antivirus et une isolation des données robustes.

**Cloud Manager :** composant de l’offre Managed Services d’Adobe Experience Manager, Cloud Manager est un portail en libre-service qui permet aux entreprises de gérer elles-mêmes Adobe Experience Manager dans le cloud. Il inclut un pipeline d’intégration et de distribution continues (CI/CD) qui permet aux équipes informatiques et aux partenaires d’implémentation d’accélérer la livraison de personnalisations ou de mises à jour sans compromettre les performances ou la sécurité. Cloud Manager est uniquement disponible pour les clients et clientes Adobe Managed Service.

Pour en savoir plus sur Cloud Manager et ses ressources, consultez le [**Guide d’utilisation Cloud Manager**](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/introduction.html?lang=fr).

## Prise en main {#getting-started}

### Prérequis {#prerequisites}

Alors que les instances de production sont généralement exécutées sur des ordinateurs dédiés exécutant un système d’exploitation officiellement pris en charge (voir [Exigences techniques](/help/sites-deploying/technical-requirements.md)), le serveur Experience Manager s’exécute sur n’importe quel système prenant en charge [**Java™ Standard Edition 8**](https://www.oracle.com/java/technologies/downloads/#java8).

Pour se familiariser avec AEM et développer sur AEM, il est courant d’utiliser une instance installée sur un ordinateur local exécutant Apple OS X ou les versions de bureau de Microsoft® Windows ou Linux®.

Côté client, AEM fonctionne avec tous les navigateurs modernes (**Microsoft® Edge**, **Internet Explorer** 11, **Chrome **51 ou version ultérieure****, **Firefox **47 ou version ultérieure, **Safari 8 ou version ultérieure**) sous les systèmes d’exploitation de tablette et de poste de travail. Pour plus d’informations, consultez [Plateformes client prises en charge](/help/sites-deploying/technical-requirements.md#supported-client-platforms).

### Obtention du logiciel {#getting-the-software}

Les clients qui disposent d’un contrat d’assistance et de maintenance valide doivent avoir reçu un e-mail de notification comportant un code pour télécharger AEM à partir du [**site Web de licences Adobe**](https://licensing.adobe.com/). Les partenaires Business peuvent demander un accès pour le téléchargement auprès de [**spphelp@adobe.com**](mailto:spphelp@adobe.com).

Le package logiciel AEM est disponible sous deux formes :

* **cq-quickstart-6.5.0.jar :** un fichier *jar* exécutable et autonome qui comprend tous les éléments nécessaires pour démarrer.

* **cq-quickstart-6.5.0.war :** un fichier *war* pour un déploiement sur un serveur d’application tiers.

La section qui suit décrit une **installation autonome**. Pour plus d’informations sur l’installation d’AEM sur un serveur d’applications, voir [Installation du serveur d’applications](/help/sites-deploying/application-server-install.md).

### Installation locale par défaut {#default-local-install}

1. Créez un répertoire d’installation sur votre ordinateur local. Par exemple :

   Emplacement d’installation UNIX® : **/opt/aem**

   Emplacement d’installation de Windows : **`C:\Program Files\aem`**

   Il est aussi courant d’installer les exemples d’instance dans un dossier sur le bureau. Dans tous les cas, Adobe désigne cet emplacement de manière générique comme :

   `<aem-install>`

   *Le chemin d’accès au répertoire de fichiers doit comporter uniquement des caractères US-ASCII.*

1. Placez les fichiers **jar** et **license** dans ce répertoire :

   ```shell
   <aem-install>/
       cq-quickstart-6.5.0.jar
       license.properties
   ```

   Si vous ne fournissez pas de fichier `license.properties`, AEM redirige au démarrage votre navigateur vers un écran de **bienvenue** dans lequel vous pouvez saisir une clé de licence. Si vous ne disposez pas d’une clé de licence valide, vous devez en demander une à Adobe.

1. Pour démarrer l’instance dans un environnement d’interface utilisateur graphique, double-cliquez sur le fichier **`cq-quickstart-6.5.0.jar`**.

   Vous pouvez également lancer AEM à partir d’une ligne de commande :

   ```shell
       java -Xmx1024M -jar cq-quickstart-6.5.0.jar
   ```

AEM va prendre quelques minutes pour décompresser le fichier jar, s’installer et démarrer. La procédure ci-dessus entraîne :

* une instance de **création AEM**
* s’exécutant sur **localhost**
* sur le port **4502**

Pour accéder à l’instance, faites pointer le navigateur sur :

**`https://localhost:4502`**

L’instance de création est alors automatiquement configurée pour se connecter à une **instance de publication** sur **`localhost:4503`**.

### Installation des instances d’auteur et de publication {#author-and-publish-installs}

L’installation par défaut (instance de **création** sur **`localhost:4502`**) peut être modifiée en renommant le fichier `jar` avant de le lancer pour la première fois. Le modèle de dénomination est :

**`cq-<instance-type>-p<port-number>.jar`**

Par exemple, renommer le fichier en

**`cq-author-p4502.jar`**

et le lancer entraîne l’exécution d’une instance de création sur **`localhost:4502`**.

De même, renommer le fichier et le lancer

**`cq-publish-p4503.jar`**

entraîne l’exécution d’une instance de publication sur **`localhost:4503`**.

Vous installerez par exemple ces deux instances dans :

`<aem-install>/author` et

**`<aem-install>/publish`**

Pour plus d’informations sur la personnalisation de votre installation, reportez-vous aux sections suivantes :

* [Installation autonome personnalisée](/help/sites-deploying/custom-standalone-install.md)
* [Modes d’exécution](/help/sites-deploying/configure-runmodes.md)

### Répertoire d’installation décompressé {#unpacked-install-directory}

Lorsque le fichier jar quickstart est lancé pour la première fois, il est décompressé dans le même répertoire dans un nouveau sous-répertoire appelé `crx-quickstart`. Vous devez disposer des éléments suivants :

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

Si l’instance a été installée à partir de l’interface utilisateur, une fenêtre de navigateur s’ouvre automatiquement. Une fenêtre d’application de bureau s’ouvre également et affiche l’hôte et le port de l’instance, ainsi qu’un bouton bascule activé/désactivé :

![Écran de démarrage](assets/screen_shot_.png)

### Démarrer et arrêter {#starting-and-stopping}

Une fois AEM décompressé et démarré pour la première fois, double-cliquez sur le fichier jar dans le répertoire d’installation pour lancer simplement l’instance. Cela ne la réinstalle pas.

Pour arrêter l’instance de l’interface utilisateur graphique, cliquez simplement sur le bouton **activer/désactiver** dans la fenêtre de l’application de bureau.

Vous pouvez également arrêter et démarrer AEM à partir de la ligne de commande. Si vous avez déjà installé l’instance une première fois, les **scripts de ligne de commande** se trouvent à cet emplacement :

**`<aem-install>/crx-quickstart/bin/`**

Ce dossier contient les scripts shell bash UNIX® suivants :

* **`start`** : démarre l’instance.
* `stop` : arrête l’instance.
* **`status`** : signale le statut de l’instance.
* **`quickstart`** : utilisé pour configurer les informations de démarrage, si nécessaire.

Il existe également des fichiers **`bat`** équivalents pour Windows. Pour plus d’informations, voir :

* [Début et arrêt d’AEM à partir de la ligne de commande](/help/sites-deploying/command-line-start-and-stop.md)

AEM démarre et redirige automatiquement le navigateur web vers la page adéquate. Il s’agit généralement de la page de connexion, par exemple :

`https://localhost:4502/`

![écran de connexion](assets/screen_shot_2019-04-08at83533am.png)

Une fois la connexion effectuée, vous avez accès à AEM. Pour plus d’informations, en fonction de votre rôle, voir :

* [Création](/help/sites-authoring/first-steps.md)
* [Administration](/help/sites-administering/home.md)
* [Développement](/help/sites-developing/getting-started.md)
* [Gestion](/help/managing/best-practices.md)

## Déploiement avancé {#advanced-deployment}

La section ci-dessus devrait vous donner une bonne compréhension des principes de base de l’installation d’AEM. Cependant, l’installation d’un système de production complet d’AEM peut être bien plus complexe. Pour une couverture complète de l’installation avancée, consultez les sous-pages suivantes :

* [Exigences techniques](/help/sites-deploying/technical-requirements.md)
* [Déploiements recommandés](/help/sites-deploying/recommended-deploys.md)
* [Installation autonome personnalisée](/help/sites-deploying/custom-standalone-install.md)
* [Installation du serveur d’applications](/help/sites-deploying/application-server-install.md)
* [Résolution des problèmes](/help/sites-deploying/troubleshooting.md)
* [Début et arrêt d’AEM à partir de la ligne de commande](/help/sites-deploying/command-line-start-and-stop.md)
* [Configuration](/help/sites-deploying/configuring.md)
* [Mise à niveau vers AEM 6.5](/help/sites-deploying/upgrade.md)
* [eCommerce](/help/commerce/cif-classic/deploying/ecommerce.md)
* [Articles sur la procédure de configuration](/help/sites-deploying/ht-deploy.md)
* [Console web](/help/sites-deploying/web-console.md)
* [Résolution des problèmes liés à la réplication](/help/sites-deploying/troubleshoot-rep.md)
* [Bonnes pratiques](/help/sites-deploying/best-practices.md)
* [Déploiement de Communities](/help/communities/deploy-communities.md)
* [Introduction à la plateforme AEM](/help/sites-deploying/platform.md)
* [Instructions de performance](/help/sites-deploying/performance-guidelines.md)
* [Prise en main d’AEM Mobile](/help/mobile/getting-started-aem-mobile.md)
* [Qu’est-ce qu’AEM Screens ?](https://experienceleague.adobe.com/docs/experience-manager-screens/user-guide/aem-screens-introduction.html?lang=fr)
