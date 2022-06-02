---
title: Impossible d’utiliser Experience Manager Forms avec certaines versions du JDK Oracle
seo-title: Unable to use Experience Manager Forms with certain versions of Oracle JDK
description: Impossible d’utiliser Experience Manager Forms avec certaines versions du JDK Oracle
seo-description: Unable to use Experience Manager Forms with certain versions of Oracle JDK
source-git-commit: 91b012f8024350effc19613bcecfc42dee4130d9
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 5%

---

# Impossible d’utiliser Experience Manager Forms avec certaines versions du JDK Oracle {#unable-to-use-forms-with-certain-versions-of-oracle-jdk}

Le problème s’applique aux versions suivantes :

* Experience Manager 6.3 Forms
* Experience Manager 6.4 Forms
* Experience Manager 6.5 Forms

## Problème {#issue}

L’utilisateur rencontre l’exception suivante :
`Caused by: javax.xml.xpath.XPathExpressionException: javax.xml.transform.TransformerException: JAXP0801002: the compiler encountered an XPath expression containing '101' operators that exceeds the '100' limit set by 'FEATURE_SECURE_PROCESSING'.`

## Raison {#reason}

L’exception se produit lorsque vous exécutez Experience Manager Forms avec la version Oracle JDK (Java Development Kit) supérieure ou égale aux versions suivantes :

* [JDK7u341](https://www.oracle.com/java/technologies/javase/7u341-relnotes.html)
* [JDK8u331](https://www.oracle.com/java/technologies/javase/8u331-relnotes.html)
* [JDK11u15](https://www.oracle.com/java/technologies/javase/11-0-15-relnotes.html)

La version ci-dessus et les versions ultérieures de Java incluent de nouvelles limites de traitement XML dans la JVM (Java Virtual Machine), ce qui entraîne l’échec de certaines opérations spécifiques à Forms.

## Solution {#workaround}

1. Arrêtez votre serveur Experience Manager Forms.
1. Configurez l’argument JVM suivant pour votre serveur d’applications :

   `-Djdk.xml.xpathExprOpLimit=2000`

   Il définit la propriété système dans la JVM sur une valeur raisonnablement élevée afin que la limite par défaut ne soit pas atteinte.

1. Démarrez votre serveur Experience Manager Forms.
