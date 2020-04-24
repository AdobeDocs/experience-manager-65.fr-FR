---
title: Conventions de dénomination
seo-title: Conventions de dénomination
description: Tirets dans le nom du package Java
seo-description: Tirets dans le nom du package Java
uuid: 48086e6c-c35b-4ffc-b216-d01feca7bf9a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 5271feb9-70c6-4c82-8ac7-34a63d80e3aa
translation-type: tm+mt
source-git-commit: 22e853ecaf2696c7329a81bb9d375b1dbc74452c

---


# Conventions de dénomination {#naming-conventions}

## Tirets dans le nom du package Java {#hyphens-in-java-package-name}

Lors de la création d’un emplacement pour une classe Java, sachez que le nom du package doit correspondre à celui du dossier du référentiel avec tous les tirets du chemin d’accès correctement protégés.

Bien que l’utilisation de tirets dans les noms des éléments du référentiel soit une pratique recommandée dans le développement d’AEM, les tirets ne sont pas autorisés dans les noms de packages Java.

La plate-forme CRX sous-jacente doit être en mesure de faire la distinction entre un trait de soulignement réel `_ `et un trait d’union `-`. Ainsi, dans le JCR, le trait d’union doit être remplacé par sa valeur unicode (u002d) et s’échapper par un trait de soulignement `_`.

Par exemple, si le chemin d’accès au référentiel est **/apps/my-example/component/info/Info.java**, le nom du package doit être : `java package apps.my_002dexample.component.info;`

Vous remarquerez qu’un trait de soulignement doit également être échappé, de telle sorte que `_` cela devienne `_005f`.
