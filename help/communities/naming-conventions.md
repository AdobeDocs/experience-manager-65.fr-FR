---
title: Conventions de dénomination dans le nom du package Java
description: Tirets dans le nom de module Java
uuid: 48086e6c-c35b-4ffc-b216-d01feca7bf9a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 5271feb9-70c6-4c82-8ac7-34a63d80e3aa
exl-id: 863900c3-5fe8-41a3-a151-466d0c62eeea
source-git-commit: a2fd3c0c1892ac648c87ca0dec440e22144c37a2
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 1%

---

# Conventions de nommage {#naming-conventions}

## Tirets dans le nom de module Java {#hyphens-in-java-package-name}

Lors de la création d’un emplacement pour une classe Java, sachez que le nom du module doit correspondre à celui du dossier du référentiel avec tous les tirets dans le chemin d’accès correctement placés dans une séquence d’échappement.

Bien que l’utilisation de tirets dans les noms des éléments du référentiel soit une pratique recommandée dans le développement d’AEM, les tirets ne sont pas autorisés dans les noms de modules Java.

La plateforme CRX sous-jacente doit pouvoir distinguer un trait de soulignement réel. `_ `et un trait d’union `-`. Ainsi, dans JCR, le trait d’union doit être remplacé par sa valeur Unicode (u002d) et échappé par un trait de soulignement. `_`.

Par exemple, si le chemin d’accès au référentiel est **/apps/my-example/component/info/Info.java**, le nom du module doit être `java package apps.my_002dexample.component.info;`

Notez qu’un trait de soulignement doit être placé dans une séquence d’échappement de la même manière, de sorte que `_` devient `_005f`.
