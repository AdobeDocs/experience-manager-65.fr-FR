---
title: Utilisation de Maven pour Communities
seo-title: Utilisation de Maven pour Communities
description: Fichier jar de l’API Uber AEM
seo-description: Fichier jar de l’API Uber AEM
uuid: ea37a89a-db6c-4018-8ab9-f5717e6c0421
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: a726c904-aadd-4678-be84-9e05808ab8be
exl-id: 3df90511-e43e-442b-bf73-44c22c1886b7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 0%

---

# Utilisation de Maven pour Communities {#using-maven-for-communities}

## Présentation {#overview}

Cette section de la documentation d’AEM Communities s’ajoute aux éléments suivants :

* [Création de projets AEM à l’aide d’Apache Maven](../../help/sites-developing/ht-projects-maven.md).

Il n’existe qu’un seul artefact &quot;uber&quot; qui remplace les artefacts individuels :

* AEM [Jar de l’API Uber](../../help/sites-developing/ht-projects-maven.md#what-is-the-uberjar)

>[!NOTE]
>
>À partir d’AEM version 6.4, les API Communities ne sont pas publiées explicitement. Toutes les API Communities sont désormais incluses dans le jar Uber lui-même.
>
>Il est recommandé de rester à jour avec la version la plus récente de Communities.
>
>Voir la section [Dernières versions](deploy-communities.md#latest-releases) pour identifier la version la plus récente.

## Exemple de dépendance Maven {#maven-dependency-example}

```xml
<dependency>
    <groupId>com.adobe.aem</groupId>
    <artifactId>uber-jar</artifactId>
    <version>6.5.7</version>
    <scope>provided</scope>
</dependency>
```

>[!NOTE]
>
>Voir [AEM référentiel Uber jar](https://mvnrepository.com/artifact/com.adobe.aem/uber-jar) pour identifier le dernier artefact Uber jar.

<!--
There are now two "uber" artifacts that replace individual artifacts:

* AEM [Communities API jar](#communities-api-jar-artifact)
* AEM [Uber API jar](../../help/sites-developing/ht-projects-maven.md#what-is-the-uberjar)

## Communities API Jar Artifact {#communities-api-jar-artifact}

Following is an example of a GAV for the AEM Communities API jar:

```xml
<dependency>
    <groupId>com.adobe.cq.social</groupId>
    <artifactId>cq-socialcommunities-api</artifactId>
    <version>1.11.170</version>
    <scope>provided</scope>
</dependency>

```

Ensure thet the version specified corresponds with the Communities package version installed for AEM Communities. To verify the installed version number:

1. Log in with adminstrative privileges.
1. Browse to [Package Manager](../../help/sites-administering/package-manager.md). For example, [http://localhost:4502/crx/packmgr/](http://localhost:4502/crx/packmgr/)

1. Locate the package: `cq-socialcommunities-pkg-1.x.xxx`
1. Extract the version from the package name:
   * First version for AEM 6.3 is version 1.11.170.
   * Feature packs will be versions 1.12.xxx.

>[!NOTE]
>
>It is recommended to keep up-to-date with the most recent Communities release.
>
>Visit the [Latest Releases](deploy-communities.md#latest-releases) section to identify the most recent version.

## Maven Dependency Example {#maven-dependency-example}

The Communities API jar must be specified before the Uber API jar.

```xml
<dependency>
    <groupId>com.adobe.cq.social</groupId>
    <artifactId>cq-socialcommunities-api</artifactId>
    <version>1.11.170</version>
    <scope>provided</scope>
</dependency>
<dependency>
    <groupId>com.adobe.aem</groupId>
    <artifactId>uber-jar</artifactId>
    <version>6.3.0</version>
    <scope>provided</scope>
    <classifier>apis</classifier>
</dependency>
```
-->
