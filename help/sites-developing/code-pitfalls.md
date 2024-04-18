---
title: Les pièges du codage
description: Pièges de codage courants à éviter lors du développement pour AEM
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: c448c5d5-def8-4c1a-8db4-41eb49d0cd20
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '89'
ht-degree: 100%

---

# Les pièges du codage{#code-pitfalls}

## Éviter les liaisons Sling dans le code Java {#avoid-sling-bindings-in-java-code}

Les liaisons Sling constituent un moyen inapproprié d’accéder à un service dans 90 % des cas. Vous devez utiliser à la place les annotations *@Reference* ou *@Inject*.

## Éviter d’insérer Thread.interrupt dans le code Java {#avoid-thread-interrupt-in-java-code}

*Thread.interrupt* est dangereux, car, appelé au mauvais moment, il peut fermer des fichiers, y compris des fichiers Lucene et des fichiers de cache persistants.

## Éviter de mélanger la synchronisation Java avec ReadWriteLocks {#avoid-mixing-java-synchronization-with-readwritelocks}

La situation peut entraîner une condition de concurrence dans laquelle le code finira par se bloquer.
