---
title: Développement d’AEM Commerce
description: Découvrir comment générer un projet AEM compatible avec le commerce à l’aide de l’archétype de projet AEM. Découvrez comment créer et déployer le projet dans un environnement de développement local.
topics: Commerce, Development
feature: Commerce Integration Framework
doc-type: tutorial
kt: 5826
thumbnail: 39476.jpg
exl-id: 48479725-8b52-4ff2-a599-d20958b26ee6
solution: Experience Manager,Commerce
source-git-commit: 1751bfb32386685e3a159939113b9667b5e17f0e
workflow-type: tm+mt
source-wordcount: '798'
ht-degree: 94%

---

# Développeur d’AEM Commerce {#develop}

Le développement de projets AEM Commerce basés sur Commerce Integration Framework (CIF) pour AEM suit les mêmes règles et bonnes pratiques que les autres projets d’AEM. Commencez par les examiner :

- [Guide de l’utilisateur pour le développement d’AEM 6.5](/help/sites-developing/getting-started.md)
- [Concepts de base d’AEM](/help/sites-developing/the-basics.md)
- [Développement sur AEM – Conseils et bonnes pratiques](/help/sites-developing/dev-guidelines-bestpractices.md)
- [Création de projets AEM à l’aide d’Apache Maven](/help/sites-developing/ht-projects-maven.md)

## Développement local pour AEM Commerce {#local}

Un environnement de développement local est recommandé pour travailler avec des projets CIF.

>[!NOTE]
>
>Les instructions suivantes vous aident à configurer un environnement de développement d’AEM local pour AEM Commerce à l’aide de CIF avec la cible d’action pour la version 6.5 d’AEM). Si vous utilisez AEM as a Cloud Service, reportez-vous au [AEM Commerce as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content-and-commerce/home.html?lang=fr) la documentation.

Le module complémentaire AEM Commerce pour AEM 6.5, alias CIF, est également disponible pour le développement local et est fourni sous la forme d’un package AEM. Il peut être téléchargé à partir du [portail de distribution de logiciels](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html) en tant que pack de fonctionnalités.

### Logiciels requis

Les logiciels suivants doivent être installés localement :

- AEM 6.5 local
- [Pack de services 7 AEM 6.5](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html) ou ultérieur
- [Java 11](https://downloads.experiencecloud.adobe.com/content/software-distribution/en/general.html)
- [Apache Maven](https://maven.apache.org/) (3.3.9 ou version ultérieure)
- [LTS Node](https://nodejs.org/en/)
- [npm 6+](https://www.npmjs.com/)
- [Git](https://git-scm.com/)

### Accès au module complémentaire CIF

Le module complémentaire CIF peut être téléchargé à partir du [portail de distribution de logiciels](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html), recherchez « module complémentaire AEM Commerce ».

>[!TIP]
>
>Veillez à toujours utiliser la dernière version du module complémentaire CIF.

### Configuration locale

Pour le développement de projet CIF local à l’aide d’AEM et du module complémentaire CIF, procédez comme suit :

1. Procurez-vous la version AEM 6.5 et installez le pack de services AEM 6.5. Le Pack de services 7 d’AEM 6.5 est requis, mais Adobe recommande d’installer le dernier Pack de services disponible.

1. Décompressez le fichier AEM .jar pour créer le dossier `crx-quickstart` et exécutez :

   ```bash
   java -jar <jar name> -unpack
   ```

1. Créez un dossier `crx-quickstart/install`.

1. Copiez tous les packages complémentaires CIF, téléchargés à partir du portail de distribution logicielle, dans le dossier `crx-quickstart/install`.

>[!TIP]
>
>Le package complémentaire CIF peut également être installé via le gestionnaire de packages.

1. Démarrage rapide AEM

Vérifiez la configuration via la console OSGI : `http://localhost:4502/system/console/osgi-installer`. La liste doit inclure les lots liés au package complémentaire CIF, le package de contenu et les configurations OSGI. Assurez-vous que tous les lots sont démarrés.

## Configuration du projet {#project}

Il existe deux façons de démarrer votre projet AEM Commerce à l’aide de CIF.

### Utilisation de l’archétype de projet AEM

L’[archétype de projet AEM](https://github.com/adobe/aem-project-archetype) est le principal outil utilisé pour démarrer un projet préconfiguré afin de démarrer avec CIF. Les composants principaux CIF et toutes les configurations requises peuvent être inclus dans un projet généré avec une option supplémentaire.

>[!TIP]
>
>Utilisez la [version 25 ou ultérieure de l’archétype de projet AEM](https://github.com/adobe/aem-project-archetype/releases) pour générer le projet.

Reportez-vous aux [instructions d’utilisation](https://github.com/adobe/aem-project-archetype#usage) de l’archétype de projet AEM pour savoir comment générer un projet AEM. Pour inclure CIF dans le projet, utilisez l’option `includeCommerce`.

Par exemple :

```bash
mvn -B archetype:generate \
 -D archetypeGroupId=com.adobe.granite.archetypes \
 -D archetypeArtifactId=aem-project-archetype \
 -D aemVersion=6.5.5 \
 -D appTitle="My Site" \
 -D appId="mysite" \
 -D groupId="com.mysite" \
 -D frontendModule=general \
 -D includeExamples=n \
 -D includeCommerce=y
```

Les composants principaux CIF peuvent être utilisés dans n’importe quel projet en incluant le package `all` fourni ou individuellement en utilisant le package de contenu CIF et les bundles OSGI associés. Pour ajouter manuellement des composants principaux CIF à un projet, utilisez les dépendances suivantes :

```java
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>core-cif-components-apps</artifactId>
    <type>zip</type>
    <version>x.y.z</version>
</dependency>
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>core-cif-components-config</artifactId>
    <type>zip</type>
    <version>x.y.z</version>
</dependency>
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>core-cif-components-core</artifactId>
    <version>x.y.z</version>
</dependency>
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>graphql-client</artifactId>
    <version>x.y.z</version>
</dependency>
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>magento-graphql</artifactId>
    <version>x.y.z</version>
</dependency>
```

### Utilisation du magasin de référence Venia AEM

Une deuxième manière de démarrer un projet CIF consiste à cloner et à utiliser le [magasin de référence Venia AEM](https://github.com/adobe/aem-cif-guides-venia). Le magasin de référence Venia AEM est un exemple d’application storefront de référence qui illustre l’utilisation des composants principaux CIF pour AEM. Cette application offre des exemples de bonnes pratiques, ainsi qu’un point de départ potentiel pour développer vos propres fonctionnalités.

Pour commencer à utiliser le magasin de référence Venia AEM, il vous suffit de cloner le [référentiel Git](https://github.com/adobe/aem-cif-guides-venia) et de personnaliser le projet en fonction de vos besoins.

>[!NOTE]
>
>Le projet de magasin de référence Venia contient deux profils de version pour AEM as a Cloud Service et AEM 6.5. Reportez-vous au [fichier readme.md du projet](https://github.com/adobe/aem-cif-guides-venia/blob/main/README.md) pour savoir comment ces profils sont utilisés. Pour AEM 6.5, utilisez le profil `classic`.

### Connexion d’AEM au système Commerce

Pour connecter votre projet au système de commerce, AEM doit être configuré avec le point d’entrée GraphQL de votre système Commerce.

Un projet généré par l’[Archétype de projet AEM](https://github.com/adobe/aem-project-archetype) ou le [Magasin de référence Venia AEM](https://github.com/adobe/aem-cif-guides-venia), ajoutez déjà une [configuration par défaut](https://github.com/adobe/aem-cif-guides-venia/blob/main/ui.config/src/main/content/jcr_root/apps/venia/osgiconfig/config/com.adobe.cq.commerce.graphql.client.impl.GraphqlClientImpl~default.cfg.json), qui doit être ajustée.

Remplacez la valeur de l’`url` dans `com.adobe.cq.commerce.graphql.client.impl.GraphqlClientImpl~default.cfg.json` avec le point d’entrée GraphQL de votre système Commerce utilisé par le projet.

Le module complémentaire Commerce AEM et les composants principaux CIF se connectent au point d’entrée Commerce GraphQL via le serveur AEM et directement via le navigateur. Par défaut, les composants principaux CIF côté client et les outils de création du module complémentaire CIF se connectent à `/api/graphql`. Si nécessaire, vous pouvez l’ajuster via la configuration du Cloud Service CIF (voir ci-dessous).

Le module complémentaire CIF fournit un servlet de proxy GraphQL à l’adresse `/api/graphql`. Si vous ne prévoyez pas d’utiliser un AEM Dispatcher local, il est recommandé de configurer également le servlet proxy GraphQL.

Accédez à http://localhost:4502/system/console/configMgr et créez une configuration OSGI pour le service `Adobe CIF GraphQL Proxy Configuration`. Utilisez le même point d’entrée GraphQL de votre système Commerce que celui utilisé pour le client GraphQL ci-dessus.

## Ressources supplémentaires

- [Archétype de projet AEM](https://github.com/adobe/aem-project-archetype)
- [Magasin de référence Venia AEM](https://github.com/adobe/aem-cif-guides-venia)
