---
title: Développer le commerce AEM
description: Découvrir comment générer un projet AEM compatible avec le commerce à l’aide de l’archétype de projet AEM. Découvrez comment créer et déployer le projet dans un environnement de développement local.
topics: Commerce, Development
feature: Commerce Integration Framework
doc-type: tutorial
kt: 5826
thumbnail: 39476.jpg
translation-type: tm+mt
source-git-commit: da538dac17b4c6182b44801b4c79d6cdbf35f640
workflow-type: tm+mt
source-wordcount: '874'
ht-degree: 37%

---


# Développement du commerce AEM {#develop}

Le développement de projets de commerce AEM basés sur le cadre d&#39;intégration commerciale (CIF) pour AEM suit les mêmes règles et pratiques exemplaires que les autres projets d&#39;AEM. Veuillez d’abord examiner les éléments suivants :

- [Guide de l’utilisateur pour le développement d’AEM 6.5](/help/sites-developing/home.md)
- [Concepts de base d’AEM](/help/sites-developing/the-basics.md)
- [Développement sur AEM – Conseils et meilleures pratiques](/help/sites-developing/dev-guidelines-bestpractices.md)
- [Création de projets AEM à l’aide d’Apache Maven](/help/sites-developing/ht-projects-maven.md)

## Développement local pour le commerce AEM {#local}

Un environnement de développement local est recommandé pour travailler avec des projets CIF.

>[!NOTE]
>
>Les instructions suivantes vous aident à configurer un environnement de développement AEM local pour AEM Commerce à l’aide de CIF avec une cible d’action pour l’ 6.5). Si vous utilisez AEM en tant que Cloud Service, consultez la documentation [AEM Commerce en tant que Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content-and-commerce/home.html).

L&#39;Ajoute commerciale AEM pour AEM 6.5 aka. L&#39;Ajoute-On du FCI est également disponible pour le développement local et est fourni sous forme d&#39;un forfait AEM. Il peut être téléchargé à partir du [portail de distribution de logiciels](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html) en tant que Feature Pack.

### Logiciels requis

Les logiciels suivants doivent être installés localement :

- AEM local 6.5
- [AEM 6.5 Service Pack](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)  7 ou version ultérieure
- [Java 11](https://downloads.experiencecloud.adobe.com/content/software-distribution/en/general.html)
- [Apache Maven](https://maven.apache.org/) (3.3.9 ou version ultérieure)
- [Noeud LTS](https://nodejs.org/en/)
- [npm 6+](https://www.npmjs.com/)
- [Git](https://git-scm.com/)

### Accès à l&#39;Ajoute CIF

Le module complémentaire CIF peut être téléchargé à partir du [portail de distribution de logiciels](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html), à la recherche de &quot;module complémentaire Commerce AEM&quot;.

>[!TIP]
>
>Veillez à toujours utiliser la dernière version du module complémentaire CIF.

### Configuration locale

Pour le développement de projets locaux du FIC à l&#39;aide de l&#39;AEM et du module complémentaire du FIC, procédez comme suit :

1. Procurez-vous la version AEM 6.5 et installez AEM 6.5 Service Pack. AEM 6.5 Service Pack 7 est requis, mais nous vous recommandons d&#39;installer le dernier Service Pack disponible.

1. Décompressez le fichier AEM .jar pour créer le dossier `crx-quickstart` et exécutez :

   ```bash
   java -jar <jar name> -unpack
   ```

1. Créez un dossier `crx-quickstart/install`.

1. Copiez le module complémentaire CIF complet, téléchargé depuis le portail de distribution de logiciels, dans le dossier `crx-quickstart/install`.

>[!TIP]
>
>Le module complémentaire CIF peut également être installé via Package Manager.

1. Début du AEM démarrage rapide

Vérifiez la configuration via la console OSGI : `http://localhost:4502/system/console/osgi-installer`. La liste doit inclure les lots de module complémentaire CIF, les configurations content-package et OSGI. Assurez-vous que tous les lots sont démarrés.

## Configuration du projet {#project}

Il existe deux façons de début de votre projet AEM Commerce à l’aide de CIF.

### Utilisation de l’archétype de projet AEM

L’[archétype de projet AEM](https://github.com/adobe/aem-project-archetype) est le principal outil utilisé pour démarrer un projet préconfiguré afin de démarrer avec CIF. Les composants de base CIF et toutes les configurations requises peuvent être inclus dans un projet généré avec une option supplémentaire.

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

Les composants de base CIF peuvent être utilisés dans n&#39;importe quel projet, soit en incluant le package `all` fourni, soit en utilisant le package de contenu CIF et les lots OSGI connexes. Pour ajouter manuellement des composants principaux CIF à un projet, utilisez les dépendances suivantes :

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

Une deuxième manière de démarrer un projet CIF consiste à cloner et à utiliser le [magasin de référence Venia AEM](https://github.com/adobe/aem-cif-guides-venia). Le magasin de référence Venia AEM est un exemple d’application storefront de référence qui illustre l’utilisation des composants principaux CIF pour AEM. Il s’agit d’un ensemble d’exemples de bonnes pratiques et d’un point de départ potentiel pour développer votre propre fonctionnalité.

Pour commencer avec le Venia Reference Store, il vous suffit de cloner le [référentiel Git](https://github.com/adobe/aem-cif-guides-venia) et de personnaliser le projet en fonction de vos besoins.

>[!NOTE]
>
>Le projet de magasin de référence Venia contient deux profils de version pour AEM as a Cloud Service et AEM 6.5. Reportez-vous au [fichier readme.md du projet](https://github.com/adobe/aem-cif-guides-venia/blob/main/README.md) pour savoir comment ces profils sont utilisés. Pour AEM 6.5, utilisez le profil `classic`.

### Connecter AEM au système commercial

Pour connecter votre projet au système de commerce AEM doit être configuré avec le point de terminaison GraphQL de votre système de commerce.

Les deux, un projet généré par l&#39;archétype de projet [AEM ](https://github.com/adobe/aem-project-archetype) ou le [magasin de référence Venia ](https://github.com/adobe/aem-cif-guides-venia), incluent déjà une configuration [par défaut](https://github.com/adobe/aem-cif-guides-venia/blob/main/ui.config/src/main/content/jcr_root/apps/venia/osgiconfig/config/com.adobe.cq.commerce.graphql.client.impl.GraphqlClientImpl~default.cfg.json) qui doit être ajustée.

Remplacez la valeur de `url` dans `com.adobe.cq.commerce.graphql.client.impl.GraphqlClientImpl~default.cfg.json` par le point de terminaison GraphQL de votre système commercial utilisé par le projet.

L&#39;Ajoute de commerce et les composants principaux de CIF se connectent au point de terminaison GraphQL de commerce via le serveur AEM et directement via le navigateur. Par défaut, les composants principaux CIF côté client et les outils de création CIF Ajoute-On se connectent à `/api/graphql`. Si nécessaire, il est possible de l&#39;ajuster via la configuration du Cloud Service CIF (voir ci-dessous).

Le module complémentaire CIF fournit une servlet proxy GraphQL à `/api/graphql`. Si vous ne prévoyez pas d’utiliser un répartiteur d’AEM local, il est recommandé de configurer également la servlet proxy GraphQL.

Accédez à http://localhost:4502/system/console/configMgr et créez une configuration OSGI pour le service `Adobe CIF GraphQL Proxy Configuration`. Utilisez le même point de terminaison GraphQL de votre système commercial que celui utilisé pour le client GraphQL ci-dessus.

## Ressources supplémentaires

- [Archétype de projet AEM](https://github.com/adobe/aem-project-archetype)
- [Magasin de référence Venia AEM](https://github.com/adobe/aem-cif-guides-venia)
