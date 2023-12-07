---
title: Les pièges du codage
description: Pièges de codage courants à éviter lors du développement pour AEM
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: c448c5d5-def8-4c1a-8db4-41eb49d0cd20
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '89'
ht-degree: 28%

---

# Les pièges du codage{#code-pitfalls}

## Éviter les liaisons Sling dans le code Java {#avoid-sling-bindings-in-java-code}

Les liaisons Sling constituent un moyen inapproprié d’accéder à un service dans 90 % des cas. Vous devez utiliser à la place *@Reference* ou *@Inject* annotations.

## Éviter d’insérer Thread.interrupt dans le code Java {#avoid-thread-interrupt-in-java-code}

*Thread.interrupt* est dangereux, car il peut fermer des fichiers, y compris des fichiers Lucene et des fichiers de cache persistants, lorsqu’il est appelé au mauvais moment.

## Évitez de mélanger la synchronisation Java avec ReadWriteLocks {#avoid-mixing-java-synchronization-with-readwritelocks}

Cela peut entraîner une situation de concurrence dans laquelle le code finira par se bloquer.
