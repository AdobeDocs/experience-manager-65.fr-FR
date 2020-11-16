---
title: Les pièges du codage
seo-title: Les pièges du codage
description: Pièges de codage communs à éviter lors du développement pour AEM
seo-description: Pièges de codage communs à éviter lors du développement pour AEM
uuid: e7413bdc-4889-45ff-bdcb-b0893d33a3b7
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 01362026-a696-4a5d-94e9-ea784eaa6e4b
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '99'
ht-degree: 94%

---


# Les pièges du codage{#code-pitfalls}

## Éviter les liaisons Sling dans le code Java {#avoid-sling-bindings-in-java-code}

Les liaisons Sling constituent un moyen inapproprié d’accéder à un service dans 90 % des cas. À la place, il faut utiliser les annotations *@Reference* ou *@Inject*.

## Avoid Thread.interrupt in Java code {#avoid-thread-interrupt-in-java-code}

*Thread.interrupt* est dangereux car il peut fermer des fichiers, y compris des fichiers Lucene et des fichiers cache persistants, s’il est appelé au mauvais moment.

## Éviter de mélanger la synchronisation Java avec ReadWriteLocks {#avoid-mixing-java-synchronization-with-readwritelocks}

Cela peut aboutir à une condition de concurrence dans laquelle le code finit par être bloqué.
