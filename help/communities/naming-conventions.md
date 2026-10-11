---
title: Conventions de dénomination dans Java&trade ; nom du package
description: Découvrez les conventions de nommage et l’utilisation de tirets dans le nom du package Java&trade ;.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 863900c3-5fe8-41a3-a151-466d0c62eeea
solution: Experience Manager
feature: Communities
role: Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: b013f126-a97e-52d1-9f79-cb5bbb12114e
    internal-label: Communities
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 1%
---
# Conventions de nommage {#naming-conventions}

## Tirets dans le nom de package Java™ {#hyphens-in-java-package-name}

Lors de la création d’un emplacement pour une classe Java™, le nom du package doit correspondre à celui de l’emplacement du dossier du référentiel avec tous les tirets du chemin d’accès ayant une séquence d’échappement correcte.

Bien que l’utilisation de tirets dans les noms des éléments de référentiel soit une pratique recommandée dans le développement AEM, les tirets ne sont pas autorisés dans les noms de packages Java™.

La plateforme CRX sous-jacente doit être en mesure de faire la distinction entre un trait de soulignement réel `_ `et un trait d’`-`. Ainsi, dans JCR, le trait d’union doit être remplacé par sa valeur Unicode (u002d) et placé dans une séquence d’échappement avec un trait de soulignement `_`.

Par exemple, si le chemin du référentiel est ****, le nom du package doit être `java package apps.my_002dexample.component.info;`

Notez qu’un trait de soulignement doit également être placé dans une séquence d’échappement, de sorte que `_` devienne `_005f`.
