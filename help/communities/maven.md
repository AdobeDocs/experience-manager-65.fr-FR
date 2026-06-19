---
title: Utilisation de Maven pour Communities
description: Découvrez le jar de l’API Adobe Experience Manager Uber à utiliser dans Communities.
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 3df90511-e43e-442b-bf73-44c22c1886b7
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1c2c350e91fe9a0a67618ea4ec00d4a8b4e3f0ca
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 0%

---

# Utilisation de Maven pour Communities {#using-maven-for-communities}

## Vue d’ensemble {#overview}

Cette section de la documentation des communautés Adobe Experience Manager (AEM) comprend les éléments suivants :

* [Création de projets AEM à l’aide d’Apache Maven](../../help/sites-developing/ht-projects-maven.md).

Un seul artefact « uber » remplace les artefacts individuels :

* AEM [jar de l’API Uber](../../help/sites-developing/ht-projects-maven.md#what-is-the-uberjar)

>[!NOTE]
>
>À partir de la version 6.4 d’AEM, les API de Communities ne sont pas publiées explicitement. Toutes les API de Communities sont désormais incluses dans le fichier JAR Uber lui-même.
>
>Restez à jour avec la version la plus récente de Communities.
>
>Consultez la section [Dernières versions](deploy-communities.md#latest-releases) qui vous permet d’identifier la version la plus récente.

## Exemple de dépendance Maven

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
>Consultez le [référentiel Uber jar d’](https://mvnrepository.com/artifact/com.adobe.aem/uber-jar) où vous pouvez identifier le dernier artefact Uber jar.

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
   * Feature packs is versions 1.12.xxx.

>[!NOTE]
>
>It is recommended to keep up-to-date with the most recent Communities release.
>
>Visit the [Latest Releases](deploy-communities.md#latest-releases) section to identify the most recent version.

## Maven Dependency Example

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
