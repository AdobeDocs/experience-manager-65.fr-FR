---
title: Utilisation de Maven pour les communautés
seo-title: Utilisation de Maven pour les communautés
description: JAR de l’API AEM Communities et JAR de l’API Uber d’AEM
seo-description: JAR de l’API AEM Communities et JAR de l’API Uber d’AEM
uuid: ea37a89a-db6c-4018-8ab9-f5717e6c0421
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: a726c904-aadd-4678-be84-9e05808ab8be
translation-type: tm+mt
source-git-commit: f05d7c19e3284c0627e29b9590db4749be100229
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 2%

---


# Utilisation de Maven pour les communautés {#using-maven-for-communities}

## Présentation {#overview}

Cette section de la documentation AEM Communities s&#39;ajoute à :

* [Création de projets AEM à l’aide d’Apache Maven](../../help/sites-developing/ht-projects-maven.md).

Il existe désormais deux artefacts &quot;uber&quot; qui remplacent des artefacts individuels :

* JAR de l’API [Communautés AEM](#communities-api-jar-artifact)
* JAR de l’API [Uber AEM](../../help/sites-developing/ht-projects-maven.md#what-is-the-uberjar)

## Artefact JAR de l&#39;API Communautés {#communities-api-jar-artifact}

Voici un exemple de GAV pour le jar API AEM Communities :

```xml
<dependency>
    <groupId>com.adobe.cq.social</groupId>
    <artifactId>cq-socialcommunities-api</artifactId>
    <version>1.11.170</version>
    <scope>provided</scope>
</dependency>
```

Assurez-vous que la version spécifiée correspond à la version du package Communities installée pour les AEM Communities. Pour vérifier le numéro de version installé :

1. Connectez-vous avec des privilèges d’administration.
1. Accédez à [Package Manager](../../help/sites-administering/package-manager.md). For example, [http://localhost:4502/crx/packmgr/](http://localhost:4502/crx/packmgr/)

1. Recherchez le package : `cq-socialcommunities-pkg-1.x.xxx`
1. Extrayez la version du nom du package :
   * La première version d’AEM 6.3 est la version 1.11.170.
   * Les packs de fonctionnalités seront des versions 1.12.xxx.

>[!NOTE]
>
>Il est recommandé de rester à jour avec la dernière version des communautés.
>
>Consultez la section [Dernières versions](deploy-communities.md#latest-releases) pour identifier la version la plus récente.


## Exemple de dépendance Maven {#maven-dependency-example}

Le jar de l&#39;API Communautés doit être spécifié avant le jar de l&#39;API Uber.

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
