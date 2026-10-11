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
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: c5d917df-d8bd-5e97-a117-6dde1e9f7103
    internal-label: Developing
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
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
