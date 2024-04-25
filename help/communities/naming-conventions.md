---
title: Conventions de dénomination dans Java&trade ; nom du package
description: Découvrez les conventions de dénomination et l’utilisation des tirets dans Java&trade; nom du package.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 863900c3-5fe8-41a3-a151-466d0c62eeea
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 1%

---

# Conventions de nommage {#naming-conventions}

## Tirets dans le nom de module Java™ {#hyphens-in-java-package-name}

Lors de la création d’un emplacement pour une classe Java™, le nom du package doit correspondre à celui du dossier du référentiel avec tous les tirets dans le chemin correctement placés dans une séquence d’échappement.

Bien que l’utilisation de tirets dans les noms des éléments du référentiel soit une pratique recommandée dans le développement d’AEM, les tirets sont illégaux dans les noms de modules Java™.

La plateforme CRX sous-jacente doit pouvoir distinguer un trait de soulignement réel. `_ `et un trait d’union `-`. Ainsi, dans JCR, le trait d’union doit être remplacé par sa valeur Unicode (u002d) et échappé par un trait de soulignement. `_`.

Par exemple, si le chemin d’accès au référentiel est **/apps/my-example/component/info/Info.java**, le nom du module doit être `java package apps.my_002dexample.component.info;`

Notez qu’un trait de soulignement doit être placé dans une séquence d’échappement de la même manière, de sorte que `_` devient `_005f`.
