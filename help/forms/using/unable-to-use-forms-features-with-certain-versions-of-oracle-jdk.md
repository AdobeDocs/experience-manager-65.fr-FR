---
title: Impossible d’utiliser Experience Manager Forms avec certaines versions du JDK Oracle.
description: Impossible d’utiliser Experience Manager Forms avec certaines versions du JDK Oracle.
exl-id: 6a8a7cb7-77d6-4bfc-82f3-82d0fddfc10a
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 751e1826ed53df7522418e50a206f0fe622256a4
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 95%
---
# Impossible d’utiliser Experience Manager Forms avec certaines versions du JDK Oracle. {#unable-to-use-forms-with-certain-versions-of-oracle-jdk}

Le problème s’applique aux versions suivantes :

* Experience Manager Forms 6.3
* Experience Manager Forms 6.4
* Formulaires avec Experience Manager 6.5

## Problème {#issue}

L’utilisateur ou l’utilisatrice rencontre l’exception suivante :
`Caused by: javax.xml.xpath.XPathExpressionException: javax.xml.transform.TransformerException: JAXP0801002: the compiler encountered an XPath expression containing '101' operators that exceeds the '100' limit set by 'FEATURE_SECURE_PROCESSING'.`

## Raison {#reason}

L’exception se produit lorsque vous exécutez Experience Manager Forms avec une version du JDK (Java Development Kit) Oracle supérieure ou égale aux versions suivantes :

* [JDK7u341](https://www.oracle.com/java/technologies/javase/7u341-relnotes.html)
* [JDK8u331](https://www.oracle.com/java/technologies/javase/8u331-relnotes.html)
* [JDK11u15](https://www.oracle.com/java/technologies/javase/11-0-15-relnotes.html)

La version ci-dessus et les versions ultérieures de Java incluent de nouvelles limites de traitement XML dans la JVM (Java Virtual Machine), ce qui entraîne l’échec de certaines opérations spécifiques à Forms.

## Solution {#workaround}

1. Arrêtez votre serveur Experience Manager Forms.
1. Configurez l’argument JVM suivant pour votre serveur d’applications :

   `-Djdk.xml.xpathExprOpLimit=2000`

   Il définit la propriété système dans la JVM sur une valeur raisonnablement élevée afin que la limite par défaut ne soit pas atteinte.

1. Démarrez votre serveur Experience Manager Forms.
